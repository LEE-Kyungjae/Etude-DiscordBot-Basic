# simple_discord_bot
간단한 기본적인 디스코드봇입니다.

## 들어가기에 앞서
디스코드 봇은 다양한 언어로 만들수있습니다.
자바스크립트,파이썬,자바 모두 가능합니다.
자바스크립트의 자료가 가장많고 그다음으로 파이썬 자료가 좀 있으나 최근에 바뀐 정책에 따라 개발한 자료가 조금 부족한 감이 있습니다. 자바의경우 자료가 많이 부족합니다. 각자 언어마다 장단점이 있으니 확인해보시고 개발하시는것을 추천합니다.

자바개발시 https://github.com/discord-jda/JDA 를 참고하자!

## 앱만들기
https://discord.com/developers/applications (디스코드 개발자 포탈)에 들어가셔서 로그인하시고, 앱등록을 하셔야합니다. Applications - New Application 버튼을 누르시고 이름과 팀(개인)을 정합니다.

## 토큰(token)
앱에 들어갑니다. 토큰을 발급받는데 토큰은 한번만 보여줍니다. 토큰은 재발급만 가능하고 기존 토큰을 다시볼수없으므로 따로 적어둡니다.
토큰은 파이썬 코드작성할때 필요합니다. 잊어버렸다면 재발급을 받습니다.

guildId 는 디스코드 서버
## 디스코드 봇 초대하기
이제 봇을 디스코드 본인 서버에 불러옵니다. 불러오기위해서는 OAuth2탭에 들어가서 OAuth2 URL Generator 에 bot을 체크,체크하면 BOT PERMISSIONS이 보일겁니다. 해당부분에서 .Administrator을 체크합니다.(임의로 권한 설정해도되는데 편의상 어드민으로)
그후 맨밑에 GENERATED URL에 있는 링크를 Copy해서 브라우저에 붙여넣으면 해당권한으로 봇을 서버에 초대할수있습니다.
## 파이썬 Setup
이제 파이썬 코드를 작성합니다.
파이썬을 설치합니다. https://www.python.org/downloads/ 에서 최신버전 파이썬을 다운로드하고 설치합니다.

ctrl+R 을 누르고 cmd를 입력한후 Enter을 치면 cmd(명령프롬프트)가 실행됩니다.(윈도우키누르고 명령 프롬프트 검색해도 됩니다.) 맥은 terminal치시면 나옵니다.
cmd에서 python을 치고 엔터를 눌렀을때 error가 뜨면 대부분 환경변수 문제입니다. 검색해서 해결하시길바랍니다.

cmd에서 pip 이라는 커멘드를 이용해 파이썬 모듈을 다운로드 할수있습니다.
모듈은 이미 코딩된 파이썬 기능(코드)입니다. 우리는 코딩할때 해당 기능(코드)들을 가져와서 사용만 잘하면 됩니다.
검색하시면 다양한 모듈들을 가져올수있습니다.
우리가 사용할 모듈은 discord,youtube_dl,load_dotenv 등등 입니다. import해서 기능을 사용할수없다면 그때가서 다운로드하시면 됩니다.
cmd에서 이런식으로 다운가능합니다.
pip install discord
pip install asyncio

## 커멘드
디스코드 서버에서 !hello 를 입력하면 봇이 hi라고 답변한다했을때 !를 prefix(프리픽스)라고 부릅니다. 뒤에오는 hello는 커멘드입니다.
프리픽스는 커멘드라는것을 알기쉽게, 실수로 커멘드를 사용하지않도록 하는 역할을 했습니다.
과거에는 !?@#%^& 과같은 봇마다 다양한 prefix를 사용한적이 있습니다. 하지만 디스코드측에서 봇이 항상 유저들의 텍스트를 확인한다는점에서 보안상의 문제가있다 판단해서 막았습니다. 자세한내용은 찾아보시면 더 정확합니다.
지금도 !?@#%^&같은 프리픽스를 통해 만들수있습니다. 다만 메시지 전체를 읽어서 !를 찾는형태입니다. 따라서 비효율적이므로 디스코드가 하라는대로 하는게 좋습니다.
디스코드측에서는 " / "를 권장합니다. 슬래시커멘드는 서버관리자가 사용할만한 기능들을 제공하는 프리픽스였습니다. 누군가를 차단하거나 추방하거나등등을 해오던 프리픽스였습니다. 프리픽스 통합에 따라 우리는 슬래시커멘드를 이용해서 커멘드를 만들어야합니다. 기존에 디스코드 자체 슬래시커멘드와 겹치지않도록 개발합시다.
또한 /로 통합되면서 바뀐점이 있습니다. 슬래시커멘드를 사용하려면 직접 디스코드측에 해당 커멘드를 사용하도록 허가요청을 보내야합니다.
간단하게 생각해서 문서를 보내면 됩니다. 문서를 보내는법은 HTTP프로토콜, HTTP라고 약속한 형태로 보내야합니다. 
HTTP는 헤더와 바디라는게 존재하는데 헤더에는 "Authorization": "Bot 앱토큰" 이라는 텍스트가 들어가야하고 바디에는 JSON이라는 문서작성법으로 형태로 작성해서 보내면됩니다.
걱정하지않으셔도됩니다. 보내는건 python이 알아서 보내줄겁니다! python의 requests라는 모듈을 다운받아서 보내면 끝입니다.
request.py파일을 확인해보시길 바랍니다.

## env

