<h1>JDBC</h1>
자바프로그램이 DB와 연결되어 데이터를 주고 받을 수 있게 해주는 API<br>

<h4>실행 순서</h4>
JDBC 드라이버 로딩 -> getConnection으로 연결 -> Statement 객체 생성 -> 쿼리 실행 -> 결과 사용 -> 각 객체 종료<br>

<h4>객체 설명</h4>
1. DriverManager<br>
DBMS와 통신을 담당하는 자바 클래스<br>
DBMS 별로 알맞는 드라이버 필요 ex) com.mysql.jdbc.Driver<br>
<br>
2. Connection<br>
DB에 접속하기 위한 메서드를 가진 인터페이스, DB통신은 커넥션 객체를 통해서만 이루어짐<br>
<br>
3. Statement , PreparedStatement<br>
Connection 클래스에서 메서드를 호출해 생성되는 객체<br>
쿼리를 싱행시키기 위한 객체<br>
*Statement , PreparedStatement 차이점*<br>
가장 큰 차이는 캐시의 사용여부<br>
이유 : Statement 는 쿼리를 실행할 때 SQL문을 수행하는 과정에서 매번 컴파일을 한다.<br>
PreparedStatement는 틀을 컴파일하고 결과만 저장 그 후 set~메서드로 값을 넣어주고 해당 틀에 맞춰 넣은 후 실행<br>
TODO.. 좀 더 정확한 내용 추후 추가<br>
<br>
4. ResultSet<br>
조회 쿼리는 결과를 반환 해당 객체는 결과를 담고있음<br>
조회를 위한 여러 메서드가 있으면 next()로 순차조회 함<br>
<br>
ps. 객체는 꼭 close를 해야함(예전에 안닫았다가 DBconnection을 다 연결하고 있어서 에러났던 적이 있음<br>
<br>

<h1>INDEX</h1>
결론부터 말하자면 인덱스는 데이터 찾는 속도를 빠르게 하기 위해 사용하는 것<br>
Select는 더 빠르지만 다른 DML을 사용할때는 상황에 따라 달라짐<br>
(INSERT 경우는 특히 효율이 안좋아짐 Why? 데이터가 추가되는데 인덱스 페이지에 저장되어 있던 탐색 위치가 수정되기 때문에)<br>
WHERE절을 사용해야 효과가있다(당연한 얘기)<br>
<br>
효율적으로 인덱스를 설정하는 기준<br>

<h4>1.카디널리티</h4>
카디널리티 : 전체 행에 대한 특정 컬럼의 중복 수치 => 컬럼의 중복 값이 '적을수록' 카디널리티가 '높다'<br>
카디널리티가 높을수록 인덱스 설정에 좋다.<br>
이유 : 중복값이 낮은 데이터일수록 그만큼 많은 데이터가 걸러짐 => 성능이 좋아짐<br>

<h4>2.선택도</h4>
선택도 : 특정 값의 컬럼 수 / 총 컬럼수<br>
선택도가 낮을수록 설정에 좋다. => 최대한 고유값 값일수록 좋다.<br>
1번과 비슷한 이유

