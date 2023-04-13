---
aliases : Application Programming Interface, 요청과 응답을 주고 받을 수 있게 만든 체계
---
- API 문서를 이해하기 위해서는 APP, web, [[데이터베이스]], 이미지 처리를 이해해야 함
	-   오픈 API 문서는 열람가능 → 공부하자
	    -   네이버
	        [네이버 오픈API 종류 - Open API 가이드](https://developers.naver.com/docs/common/openapiguide/apilist.md)
	-   변동 가능한 정보는 API로 서버에서 불러오게 만든다 

# 개요

📌 **API** : 클라이언트, 서버와 같은 서로 다른 프로그램에서 요청과 응답을 주고 받을 수 있게 만든 체계 (= SW가 다른 SW의 기능을 쓰기 위해 중간에 필요한 체계) *SW : 소프트웨어
```mermaid
graph LR;
PC --API--- SW
```
- 클라이언트에서 요청을 보내면, 서버에서 요청을 받아서 응답을 줌
    그 응답을 주는 걸 사전에 어떻게 할 건지 정해두는 것을 API라고 함
    API= 메뉴판(ex 네이버웹툰 get요청을 받아서 웹툰을 보여주는 웹 사이트) 
    - API는 서버 개발자가 개발, 결과물 서버 프로그램
- API를 만들 때 데이터를 주고 받는 기능도 함께 넣음
    - [[JSON]] 형식 / 과거에는 [[XML]] 형식이 자주 쓰임
- 서버 개발자가 개발 \ 클라이언트 개발자는 API를 사용 (API 문서 서비스 : 깃북(GitBook))
- SDK는 다른 소프트웨어에서 제공해주는 API를 말함 ex) 구글 지도 SDK 등
- **API 요청** : 요청 Request ↔ 응답 Response
    ex) HTTP 상태 코드
    숫자를 통해 오류의 내역을 표시 ex) 성공하면 200번대(201, 202 등)
---
- API 사양(=구현체) : API 호출을 다시 정의
- API 호출 = 서브루틴 = 메소드 요청= 통신엔드포인트
- 연관문서 : [[Web API]]
---
# 연관문서