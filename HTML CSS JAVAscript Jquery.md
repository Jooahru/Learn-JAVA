## 2021 03 31

* HTML 실습 코드 

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="UTF-8">
  <title>Insert title here</title>
  </head>
  <body>
  <h1 id="here">k digital 과정</h1>
  <h3>web client 과목</h3>
  <h5>html 태그</h5>
  <p> 현재 우리는 html 태그 가운데 <br><b>글자 크기</b>와 관련된 태그를 출력중입니다</p>
  <hr>
  <p> 현재 우리는 html 태그 가운데  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;<i>글자 크기</i>와 관련된 태그를 출력중입니다</p>
  <hr>
  <a href="http://www.multicampus.co.kr"> 다른페이지로 이동</a><br>
  <a href="first.html"> 현재서버의 현재프로젝트의 first.html파일로 이동</a><br>
  <a href="/프로젝트명/first.html"> 현재서버의 다른 프로젝트의 first.html파일로 이동</a><br>
  <a href="#here"> 현재파일의 첫부분 이동</a><br>
  
  <h1> 목록 태그</h1>
  <ol type="a"> 
  <li>자바</li>
  <li>sql</li>
  <li>jquery</li>
  <li>spring</li>
  <li>jsp</li>
  </ol>
  
  <ul type="square"> 
  <li>자바</li>
  <li>sql</li>
  <li>jquery</li>
  <li>spring</li>
  <li>jsp</li>
  </ul>
  
  <table border="3">
  <tr><th>번호</th><th>제목</th><th>작성자</th><th>조회수</th></tr>
  <tr><td>1</td><td>1행 2열 데이터</td><td>1행 3열 데이터</td><td>1행 4열 데이터</td></tr>
  <tr><td>2</td><td>2행 2열 데이터</td><td>2행 3열 데이터</td><td>2행 4열 데이터</td></tr>
  <tr><td>3</td><td>3행 2열 데이터</td><td>3행 3열 데이터</td><td>3행 4열 데이터</td></tr>
  </table>
  
  <table border="3">
  <caption> 로그인 테이블</caption>
  <tr><td>로그인아이디입력</td><td>xxxxx</td><td rowspan="2">로그인버튼</td></tr>
  <tr><td>암호입력</td><td>xxxxx</td></tr>
  </table>
  
  <table border="3">
  <caption> 로그인 테이블2</caption>
  <tr><td>로그인아이디입력</td><td>xxxxx</td></tr>
  <tr><td>암호입력</td><td>xxxxx</td></tr>
  <tr><td colspan="2">로그인버튼</td></tr>
  </table>
  
  </body>
  </html>
  ```

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="UTF-8">
  <title>Insert title here</title>
  </head>
  <body>
  <h1>입력(키보드,마우스) 양식태그</h1>
  <form action="입력값 전송받을 파일">
  아이디입력 : <input type = "text" name = "id"><br>
  암호입력: <input type= "password" name="pw"><br>
  권한: <input type="hidden" name="role" value="admin"><br>
  성별: <input type="radio" name="gender" value="male"> 남자
  <input type="radio" name="gender" value="female">여자<br>
  수강과목:
  <input type="checkbox" name="subjet" value="java">자바
  <input type="checkbox" name="subjet" value="oracle">오라클
  <input type="checkbox" name="subjet" value="html">html
  <input type="checkbox" name="subjet" value="jsp">jsp<br>
  사진:
  <input type="image" name="myimage" src="images/google.png"><br>
  자기소개서파일:
  <input type="file" name="myfile"><br>
  html5(브라우저마다 모양 다르다)
  <input type="color"><br>
  <input type="datetime-local"><br>
  <input type="number"><br>
  
  <textarea rows="5" cols="100"><</textarea><br>
  
  <select multiple="multiple">
  	<optgroup label="중식">
  		<option> 짜장면</option>
  		<option> 짬뽕</option>
  	</optgroup>
  
  	<optgroup label="분식">
  		<option> 라면</option>	
  		<option> 떡볶이</option>
  	</optgroup>
  	<optgroup label="기타">
  		<option> 한식</option>
  		<option> 안먹음</option>
  	</optgroup>
  	
  </select>
  
  
  <input type=button value="기능"><br>
  <input type=reset value="입력취소"><br>
  <input type=submit value=로그인>
  
  </form>
  
  <img src="images/google.png">
  
  </body>
  </html>
  ```

  