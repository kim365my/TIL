---
tag : 스타일시트
---

# 개요
- JS 기반 프레임워크 : 프레임워크 기반의 JS APP과 함께 사용가능
- CSS 기반 프레임워크 : 기본적인 JS 컴포넌트 제공 안함

# JS 기반 프레임워크
## Reactstrap
## Materal UI
## Railwind CSS
## Chakra


# CSS 기반 프레임워크
## 부트스트랩 Bootstrop
- CDN 연결링크
	```html
	<link rel="stylesheet" href="https://unpkg.com/bootstrap@3.3.7/dist/css/bootstrap.min.css">
	```
- 테이블 클래스명
	- `panel_header`
	- `panel-body`
	- `table`
- 버튼
	- btn btn-primary
	- btn btn-secondary
- 자주 사용하는 폼
	```html
	<!DOCTYPE html>
	<html>
	<head>
	<meta charset="UTF-8">
	<title>액션태그 포워드 로그인</title>
	<link rel="stylesheet" href="https://unpkg.com/bootstrap@3.3.7/dist/css/bootstrap.min.css">
	</head>
	<body>
		<h2>타이틀</h2>
		<div class="panel-heading">
			<h3>로그인</h3>
		</div>
		<div class="panel-body">
			<form action="./02_ActionTagForwardCtrl.jsp" method="post">
				<table class="table">
					<tr>
						<td>아이디 : </td>
						<td><input type="text" name="id"></td>
					</tr>
					<tr>
						<td>비밀번호 : </td>
						<td><input type="password" name="password"></td>
					</tr>
					<tr>
                            <td colspan="2">
                                <input type="submit" value="제출" class="btn btn-primary">
                                <input type="reset" value="리셋" class="btn btn-secondary">
                            </td>
					</tr>
				</table>
			</form>
		</div>
	</body>
	</html>
	```


## Moterialize CSS

## Bulma