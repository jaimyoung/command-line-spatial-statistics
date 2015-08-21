# 기본 GDAL과 OGR 명령어
래스터 데이터와 벡터 데이터를 처리하는 방법을 알아보자.
기본적 연산은 다음과 같다.

1. 데이터 화일의 정보 알아내기 (`gdalinfo`, `ogrinfo`)
1. 행 선택하기 
1. 행 연산하기
1. 프로젝션 변환하기

시범데이터로는 내추럴어쓰(Natural Earth, 혹은 NE) 자료를 사용하도록 하겠다.
<http://www.naturalearthdata.com/downloads/>
특히 1:50m 자료를 사용한다.

- 컬추럴벡터: Admin 0 - Countries <http//www.naturalearthdata.com/download/50m/cultural/ne_50m_admin_0_countries.zip>
- 래스터: 1:50m Natural Earth I with Shaded Relief <http//www.naturalearthdata.com/download/50m/raster/NE1_50M_SR.zip>


## 래스터 데이터 처리를 위한 GDAL 명령어
### 1. gdalinfo for basic info
래스터 데이터의 내용을 알아내는 명령은 gdalinfo <http://www.gdal.org/gdalinfo.html> 이다.

    gdalinfo $raster_fname

중요한 정보는

- Driver: GTiff/GeoTIFF
- Size : 
- Coordinate System: AUTHORITY["EPSG","4326"]] 등등
- Corner coordinates:
- 각 밴드에 대한 Band number, Type, NoData Value, Metadata (statistics min, max, mean, SD)

### 2. gdalwarp for most operations
TBD



## 벡터 데이터 처리를 위한 OGR 명령어
### 1. ogrinfo for basic info
벡터 데이터 화일의 내용을 알아내는 명령은 ogrinfo <http://www.gdal.org/ogrinfo.html> 이다.
기본적 용법은:

    ogrinfo $shp_fname  # 래이어를 보여준다다
    ogrinfo -so $shp_fname $layer_name
    ogrinfo -al -so $shp_fname  # 모든 래이어 (-al = all layer)의 정보를 보여준다.
    
여기서 -so = summary only 플래그를 사용하지 않으면 불필요하게 많은 정보가 출력된다.
핵심 정보는:

- Geometry: polygon? point? ...
- Projection
- Feature 갯수
- Extent
- 애트리뷰트(attribute) 변수이름, 타입(Integer, String, Real, ...), precision 혹은 스트링 길이

### 2. ogr2ogr for subsetting
변수(attribute)값에 기반해 Subsetting을 위해서는 다음 명령을 사용한다.

    ogr2ogr -where "name='United States'" \
        -f "ESRI Shapefile" \
        ne-50m-usa.shp \
        ne_50m_admin_0_countries/ne_50m_admin_0_countries.shp

여기서 where 문에서 사용할 변수이름과 값은 QGIS를 사용해서 얻어내면 된다.

### 3. ogr2ogr for changing projection
위의 화일을 NAD83 / Maryland 로 바꾸기 휘해서는 

    ogr2ogr -f "ESRI Shapefile" \
        -t_srs EPSG:26985 \
        ne-50m-usa-nad83.shp \
        ne-50m-usa.shp

여기서 프로젝션 이름을 알아내는대는 QGIS가 도움이 된다.
EPSG은 NAD83 / Maryland (in meters, not feet)이다.


## 래스터와 벡터 데이터를 함께 처리하는 명령어들

# 벡터데이터로 래스터데이터 subset하기
<http://gis.stackexchange.com/questions/45053/gdalwarp-cutline-along-with-shapefile>
페이지를 참조하자.

    gdalwarp -cutline INPUT.shp INPUT.tif OUTPUT.tif

    gdalwarp -cutline INPUT.shp -crop_to_cutline -dstalpha INPUT.tif OUTPUT.tif

