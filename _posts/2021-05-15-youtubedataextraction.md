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




