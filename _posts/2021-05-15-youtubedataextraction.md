---
layout: post
title: 손수민든 유튜브 자막과 댓글 수집
subtitle: 
#gh-repo: daattali/beautiful-jekyll
tags: [데이터수집]
comments: true
---

안녕하세요 여러분~! 다시 돌아왔습니당 ㅎㅎ   
이번엔 다른 주제를 가지고 말이죠~  
오늘은 어떤 신나는 코드를 **손수민들어** 볼까요~? 두구두구두구두구  
  
  
그건 바로 ㅎㅅㅎ~! 파이썬을 이용하여 유튜브의 자막과 댓글을 수집해 보는 것입니당~!! 
![wow_gif](/assets/img/wow.gif)  
ㄴㅇㄱ 상상치 못한 정체!  
  
그게 가능하다고?!  
네 가능합니다. 바로 손수민든 코드와 함께라면 말이죠.  
지금바로 시작하시죠.  

제가 수집할 유튜브 비디오는 바로 문명특급의 최신 동영상입니다.  
![video_jpg](/assets/img/youtube.JPG)  
다음과 같이 올라온지 얼마 안됐는데 조회수가 100만회를 훌쩍 넘는 인기 동영상 이군요.  
이 동영상의 데이터를 수집하기 좋은 이유는 바로 한국어 자막이 등록되어 있다는 점입니다.  
아직 한국어는 speech to text가 잘 되어있지 않아서 한국 유튜브의 경우 한글 자막이 흔치 않은데 이 영상은 정말 다행히도 한글 자막이 있습니다. 

![video_jpg](/assets/img/comment.JPG)  

또한 이 영상은 댓글이 3000개가 넘어갑니다. 이 영상을 본 사람들이 영상에 대해 어떻게 생각하는지 궁금한데 3000개를 다 읽기에는 무리가 있겠죠?  
그래서 3000개가 넘어가는 댓글을 csv파일에 저장하고, 후에 분석하는데 사용하기 좋은 형태로 만들어 봅시다!  
시작해볼까요~?  
  
먼저 자막을 추출해 봅시다. 자막은 txt파일에 저장할 예정입니다!  
자막을 추출하기 위해 Youtube Transcript API를 사용할 예정입니다!  
https://pypi.org/project/youtube-transcript-api/  
진짜 간단해요. 누가 만들어뒀는지 정말 감사합니다...  

```
from youtube_transcript_api import YouTubeTranscriptApi

YouTubeTranscriptApi.get_transcript(video_id)
```
다음과 같이 라이브러리를 임포트 해주고, video_id에 자막을 추출할 비디오의 아이디를 넣으면 됩니다.  
그리고 한번 쏴주면
```
[
    {
        'text': 'Hey there',
        'start': 7.58,
        'duration': 6.13
    },
    {
        'text': 'how are you',
        'start': 14.08,
        'duration': 7.58
    },
    # ...
]
```  
다음과같이 딕셔너리 형태로 텍스트, 텍스트의 시작시간, 지속시간을 반환해준다고 합니다.  
한번 저 위의 유튜브로 시도해볼까요~?  
유튜브의 비디오 아이디는 다음과 같이 v= 뒤에 있는 부분이 비디오 아이디입니다.

오호라 저희가 수집할 비디오의 아이디는 , v=6tcX2hbQkDM 에서 6tcX2hbQkDM 요 아이가 되겠군요.  
정말 간단하게 video_id에 6tcX2hbQkDM를 넣어주고 돌려보겠습니당! 
앗차차! 저는 구글 colab환경에서 실행했는데, 저 라이브러리를 import 할려면 실행전에  
```
!pip install youtube_transcript_api
```
다음과 같이 pip install을 진행해 줍시다.  
그리고 추출을 해봅시다!

```
from youtube_transcript_api import YouTubeTranscriptApi

YouTubeTranscriptApi.get_transcript("6tcX2hbQkDM")
```  
근데 결과가  
![err_jpg](/assets/img/err.JPG)  
이렇게 영상의 자막을 추출할 수 없다는 에러가 뜹니다.  
슬프군요.  
삽질했습니다.  
프로젝트에서 사용했던 영상말고 새로운걸 하고 싶었으나 엄청난 삽질이었군요.  

그냥 하던걸로 보여드리겠습니다.  
저희 고독한 늑대 둘의 분석에 사용한 유튜버 중 하나인, FunForLouis 채널입니다.  
![funforlouis_jpg](/assets/img/FunForLouis.JPG)  
  
```
YouTubeTranscriptApi.get_transcript("jtnBf3qptGM")
```
다음과 같이 한번 쏴보면  
![dictlist_jpg](/assets/img/diclist.JPG)  
다음과 같이 진짜 diclist로 반환을 해주는군요.  

그러나 여기엔 시작시간이랑 지속시간이 들어있습니다.  
저는 굳이 이것도 같이 분석을 하진 않았기에, 요 친구들은 빼고 txt파일에 저장해 봅시다.  
  
```
srt = YouTubeTranscriptApi.get_transcript("jtnBf3qptGM")
with open('yourfile_path.txt','w') as f:
  f.writelines('%s\n' % i['text'] for i in srt)
```
단 세줄만에 자막을 읽고, 이를 한줄 씩 텍스트 파일에 저장하는 코드입니다.  
파일을 오픈하고, 각 라인에 딕셔너리의 text만을 추출하여 작성하는 코드입니다.  
원래는 정말 복잡한 코드였는데 이렇게 간단하게 표현할 수 있네요.  
전 이렇게 간단한 코드를 볼때마다 30분을 달리고 냉수를 먹은 것처럼 시원한 감정을 느낍니다.  
클린한 코드를 작성할 수 있도록 더욱더 노력해야겠습니다.  
앗차차. 진짜로 저장이 잘되었나 확인해볼까요?  
![res0_jpg](/assets/img/res0.JPG) 
저장이 잘 된 모습입니다. ㅎㅎ 이제 이 텍스트 파일을 가지고 후에 텍스트 분석도 할 수 있겠죠~?  
  
  
이제 유튜브 생산자인 유튜버의 자막 추출을 완료하였으니까, 이제 유튜브 소비자인 시청자의 댓글도 수집해 볼까용~?  
댓글을 수집하는데는 google-api-python-client를 사용하였습니다.  
이걸 이용해서 youtube data api v3를 사용할 예정입니당~  
https://pypi.org/project/google-api-python-client/  

앗차차. 자막을 추출하기전에 google api key가 필요합니다. 
https://console.cloud.google.com/apis  
여기루 들어가서,  
![apikey_jpg](/assets/img/apikey.JPG)  
다음과 같이 파란동그라미를 눌러 호다다닥 만들어옵시다.  
그리고 코드를 작성하기 전, 라이브러리를 임포트해주고 api key를 변수에 저장해 둡시다.  

```
!pip install google-api-python-client
import pandas
from googleapiclient.discovery import build
api_key = your_api_key
```
이렇게요! 참 쉽죠?  

이제 api를 쏴서 한번 코멘트를 추출해 봅시당!  

```
comments = list()
  api_obj = build('youtube', 'v3', developerKey=api_key)


  response = api_obj.commentThreads().list(part='snippet,replies', videoId=video_id, maxResults=100).execute()
 
  while response:
      for item in response['items']: 
          comment = item['snippet']['topLevelComment']['snippet']
          comments.append([comment['textDisplay'], comment['authorDisplayName'], comment['publishedAt'], comment['likeCount']])
 
          if item['snippet']['totalReplyCount'] > 0:
              for reply_item in item['replies']['comments']:
                  reply = reply_item['snippet']
                  comments.append([reply['textDisplay'], reply['authorDisplayName'], reply['publishedAt'], reply['likeCount']])
 
      if 'nextPageToken' in response:
          response = api_obj.commentThreads().list(part='snippet,replies', videoId=video_id, pageToken=response['nextPageToken'], maxResults=100).execute()
      else:
          break
```

먼저 댓글 하나하나를 저장해둘 comments 리스트를 선언합니다. 여기엔 이제 댓글들이 하나하나 들어갈 것입니다.  

그리고 api의 response를 받습니다. 그리고 response의 끝까지 while문으로 훑어줍니다. 
response는 json 형태인데, item안에 topLevelComment가있고 또 그안에 snippet이 있습니다.  

그 안에서 textDisplay는 댓글을 뜻하고, authorDisplayName은 댓글을 단 유저의 이름, publishedAt은 댓글이 달린 날짜, likeCount는 좋아요의 갯수를 말합니다.  
이렇게 돌 때마다 comments에 append가 됩니당.  
그리고 만약 답글이 있다면, 답글을 체크한 후에 답글 역시 comments에 append해줍니다.  
그리고, 댓글은 한 요청당 100개씩 받아오는데, 이를 댓글의 갯수 끝까지 받아옵니당.  
만일 다 받아왔다면 break로 빠져나와줍니다.  

한번 잘 저장되었는지 확인해 볼까요?  

![res1_jpg](/assets/img/res1.JPG)  

리스트로 잘 받아와 졌군요. 이 친구를 조금 더 보기 좋게, 저장하기 좋게 DataFrame으로 다뤄 봅시다.  

```
df = pandas.DataFrame(comments,columns=['comment', 'id', 'date', 'num_likes'])
```  

칼럼에 넣고싶은 칼럼명을 넣습니다. 그리고 우리의 사랑스러운 리스트 comments를 넣어주고 데이터프레임 객체를 생성합니다.  
잘되었나 결과를 확인해 볼까요?  
![res2_jpg](/assets/img/res2.JPG)  
잘되었군요! 이제 이 결과를 csv파일로 저장하는 일만 남았습니다.  
```
df.to_csv('yourfilepath.csv', encoding = 'utf-8-sig',index = False)
```
저장할 파일 경로를 설정하고, 인코딩은 utf-8-sig로 해줍니다. 저는 이상하게 utf-8로 저장을 해두면, 나중에 다시 불러올 때 글자가 깨지더라고요.  
근데 얘는 안깨져서 이렇게 저장을 해둡니다.  
그리고 index는 False로 해둡니다.  
잘 저장되었나 확인해볼까요?  
![res3_jpg](/assets/img/res3.JPG)  
잘 저장이 된 모습입니다.  
이걸로 이제 유튜브의 데이터를 extract 할 수 있는 능력을 가지게 되었답니다.  
데이터 분석의 핵심중 핵심은 역시 데이터를 추출 할 수 있는 능력 아닐까요?  
이제 이 추출한 데이터를 분석한결과는 저희 고독한 늑대 둘의 논문을 참고해주세요!  
읽어주셔서 감사합니다.  
행복한 여름 되시길 바랄게요~  



