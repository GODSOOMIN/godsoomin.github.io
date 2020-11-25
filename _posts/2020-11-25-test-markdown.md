---
layout: post
title: 손수민든 데이터 시각화
subtitle: 파이썬 folium 라이브러리와 서울시 행정구 geo_json을 이용한 시각화
#gh-repo: daattali/beautiful-jekyll
tags: [시각화]
comments: true
---

헬로 여러분들 ~ 요즈음 미세먼지가 심각해졌죠?  
빨래 널어야하는데 빨래에 미세먼지가 철-썩- 달라붙을까봐 걱정 또 걱정이네요~  
여름에는 장마여서 못널어~ 겨울에는 얼어서 못널어~ 봄과 가을에는 미세먼지 때문에 못 널어~  
더 넓은 집으로 이사가서 건조기를 얼른 장만해야겠어요!  

아무튼 잡담은 그만하고   
오늘은 미세먼지 데이터를 활용하여 시각화를 손수민들어 볼거에요~  
파이썬과 데이터만 있으면 어디든 갈 수 있죠.  

우리가 만들건  
![map_img](/assets/img/map.JPG) 
이러한 결과를 만들어 볼 것이고요~  
먼저 데이터 출처는 [서울특별시 대기환경정보](https://cleanair.seoul.go.kr/2020/) 입니다.  

데이터는 2019년도 구별 미세먼지 평균 값을 사용했고요  
```
import pandas as pd

file_path = 'pm10.csv'
pm10 = pd.read_csv(file_path)

pm10

```
요로코롬 코드를 작성해서 확인해보니  

![list_img](/assets/img/list.JPG)  
이렇게 생겼습니다.  

파이썬의 folium 라이브러리를 사용하여서
이걸 수치를 지도에 매핑시켜서 한눈에 비교해 봅시다!  


다행히도 https://github.com/southkorea/seoul-maps 위 깃헙 주소에서  
서울시의 행정구를 polygon으로 나눈 geojson파일을 제공 하고있습니다!


```
import pandas as pd
import folium
import json

file_path = 'pm10.csv'
pm10 = pd.read_csv(file_path)


geo_path = 'seoul_municipalities_geo_simple.json'
geo_json = json.load(open(geo_path,encoding="utf-8"))

latitude = 37.715133
longtitude = 126.734086


m = folium.Map([latitude, longtitude])

folium.Choropleth(
    geo_data=geo_json,
    name='mymap',
    data=pm10,
    columns=['name', 'avg'],
    key_on='feature.properties.name',
    fill_color='YlOrBr',
    fill_opacity=0.7,
    line_opacity=0.2,
    legend_name='pm10'
).add_to(m)

m

```  


먼저 folium과 json을 import 해주고  
위에서 불러온 미세먼지 파일도 데려와줍니다!  
그리고 지도의 중심이 될, 서울시의 중심 위도와 경도(latitude, longtitude)를 설정해주시고요,
이제 지도에 데이터를 매핑시켜봅시다.  
geo_data에는 우리의 geo_json파일을,  
data에는 우리의 미세먼지 농도 파일을 넣어주시고  
columns에는 미세먼지 파일의 두 칼럼 이름을 넣어줍시다!  
또한 json파일의 행정구 이름과 미세먼지 농도 파일의 행정구 이름을 매핑시켜주시고요  
fill_color에는 미세먼지 색깔과 비슷한 옐로우 오렌지 브라운으로 색칠해 줍시당 ㅎㅎ  
투명도를 적절히 원하는 대로 설정해주시고 ! 이제 두둥! 실행시켜봅시다.!

![map_img](/assets/img/map.JPG) 


참 간단하고 쉽죠?  
읽어주셔서 감사합니다. ㅎㅎ 
꾸벅 (_ _ )b
