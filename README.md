# 커맨드 라인에서 공간데이터 분석하기

**공간데이터분석(spatial analysis)**은 
기하학적, 지리학적 정보를 포함한 
공간데이터(spatial data)의 분석이다.
특히 **공간통계(spatial statistics)**는 
공간적 변동과 오차를 통계적으로 모델링한 분석이다.
(<https://en.wikipedia.org/wiki/Spatial_analysis>)

공간데이터 분석은 많은 경우 **GIS(Geographic Information Systems)** 
소프트웨어에 의존한다.
GIS는 공간적(spatial) 혹은 지리적(geographical data)를
수집, 저장, 처리, 분석, 관리, 표현(present)하는 시스템이다.
(<https://en.wikipedia.org/wiki/Geographic_information_system>)

## 기본개념
우선 다음의 개념을 확실히 익혀두자:

- raster
- vector
- projection

## 공간데이터 분석 툴
공간데이터 분석은 
내용 자체도 어렵지만 툴링(tooling 혹은 tool chain)도
파편화(fragmentation)되어있다.
공간데이터 분석을 위한 소프트웨어를 일부 소개하면 다음과 같다:

1. ArcGIS: 상업용 GIS.
2. QGIS (<http://www.qgis.org/en/site/>):Open Source 데스크탑 GIS.
3. GDAL - Geospatial Data Abstraction Library (<http://www.gdal.org/>): 
    - 라이브러리
    - 커맨드 라인 유틸리티  
4. GRASS GIS (Geographic Resources Analysis Support System <https://grass.osgeo.org/>): 오픈소스 GIS
    - GUI
    - QGIS에서 호출 가능.
5. R : 통계자료 분석 소프트웨어. <https://cran.r-project.org/web/views/Spatial.html> 에서 보듯이
    다양한 공간데이터분석 라이브러리가 있다. 중요한 라이브러리는 다음과 같다. `install.packages()` 명령을 사용하여
    설치하도록 하자.
    - `sp`: Classes and Methods for Spatial Data
    - `raster`: Geographic Data Analysis and Modeling
6. 파이썬(Python): 범용 자료 소프트웨어. 중요한 라이브러리는 다음과 같다.
    - PySAL: <https://pysal.readthedocs.org/en/latest/>. `pip install pysal`로 설치하도록 하자.
    - GDAL: <https://pypi.python.org/pypi/GDAL/>. `pip install gdal`로 설치.

## 왜 커맨드 라인인가?
커맨드 라인의 장점은:

1. 코드를 형상관리할 수 있다.
2. 분석이 재현가능(reproducible)하다.


## 환경설정
맥 OSX 환경을 가정한다. (리눅스는 비슷하다. 윈도우즈도 여러 실행화일이 존재한다)

### QGIS
QGIS설치를 위해서는 <http://www.qgis.org/en/site/forusers/download.html> 를 방문해서 설치한다.
다운로드 페이지에서 설명하듯이 QGIS에서 사용할 
GDAL 라이브러리(GDAL Complete)를 따로 설치한다.
좀 특이한, 그렇게 공식 페이지 같지 않은
KyngChaos QGIS download page (<http://www.kyngchaos.com/software/qgis>)에서 다음 소프트웨어를 설치해야 한다:

- GDAL Complete
- Matplotlib Python module
- QGIS

QGIS에서 설치한 GDAL라이브러리는 디렉토리 XXX 에 인스톨된다.
(2015년 8월 현재 버전은 GDAL 1.11)
(확인: GDAL 커맨드 라인 명령을 사용하기 위해서는 위의 디렉토리를 패스에 넣어주던가, 
GDAL을 따로 설치해도 된다.)

### 파이썬 GDAL 바인딩
파이썬은 일단 anaconda 파이썬을 설치하도록 하자. (<http://continuum.io/downloads>)
anaconda 파이썬이 설치된 후,
커맨드에서 다음을 실행하면 gdal library 와 파이썬 바인딩이 설치된다.

    conda install gdal
    
(2015년 8월 현재 버전은 gdal-2.0.0-np1)
커맨드라인 명령어는 다음 디렉토리에 연결되므로 따로 PATH를 지정할 필요가 없다.

    ~/anaconda/bin/gdalinfo


### GDAL
위에서 보았듯이 QGIS나 파이썬에서 GDAL 라이브러리를 설치하는 것이 
GDAL을 사용하는 가장 자연스러운 방법이다.

하지만 따로 GDAL을 설치해야 한다면,
가장 쉬운 방법은 Homebrew (<http://brew.sh/>)를 사용하는 것이다.
홈브루를 설치한 후, 다음 명령을 실행하여 GDAL을 설치한다.

    brew install gdal

(2015년 8월 현재 버전은 gdal-2.0.0-np1)
커맨드라인을 연결하기 위해서는 다음 라인을 .bashrc 혹은 .zshrc에 추가하도록 하자:

    PATH=$PATH:/usr/local/Cellar/gdal/1.11.2_1/bin    

## 커맨드 라인 사용예
TBA
