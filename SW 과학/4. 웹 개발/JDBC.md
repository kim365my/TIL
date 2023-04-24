---
tag : 백엔드
---


# 개요
> 자바를 통해서 DB에 접근할 수 있는 기술? 암튼 그렇대

# JDBC를 이용해서 DB 접속흐름
```java
Class.forName("oracle.jdbc.driver.OracleDrvier");
String url = "jdbc:orcle:thin:@localhost:1521:xe";
Connection conn = DriverManager.getConnection(url, "hr", "hr");
// DB 접속 코드 작성 생략
// 자원 반납 필수
ptsml.close();
rs.close();
conn.close();
```
- webapp -> lib 파일에 jar06파일 저장해두기
- 이외에는 [[커넥션 풀 API]]에서 했던 것과 동일하지만, 자원반납하는거나 jsp 페이지마다 작성하는게 귀찮음
- 

