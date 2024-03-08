
# 1. 개발환경 

개발툴(IDE)- Eclipse

데이터베이스 관리 (DBMS) - Oracle

웹 애플리케이션 (WAS) - Tomcat9

!dependency 추가 
- JSTL(JSP 표준 태그 라이브러리)
- JDBC(데이터베이스 연동 및 쿼리 실행을 위한 자바API)

#### 컨넥션풀 설정 - 톰캣 conf 폴더에 있는 context.xml 파일 맨 하다 <Manager  --> 아래 추가

            <Resource
             name="jdbc/oracle"
             auth = "Container"
             type="javax.sql.DataSource"
             driverClassName="oracle.jdbc.OracleDriver"
             url="jdbc:oracle:thin:@localhost:1521:XE"
             username="webdb"
             password="12345"
             maxActive="50"
             maxWait="-1" />

# 2. 게시판 만들기 - SQL문  



1. webdb 사용자 생성


        CREATE USER webdb IDENTIFIED BY 12345;
        
        GRANT CONNECT, RESOURCE TO webdb;

2. webdb로 로그인

   ![image](https://github.com/nowod9712/JSP_board/assets/154123670/76fda530-856c-429e-a809-38d982dafcfc)


3.Board 테이블과 시퀀스 생성

        create table board(
            num number primary key,
            title varchar2(50) not null,
            writer varchar2(50) not null,
            content varchar2(100),
            regdate date,
            cnt number default 0
        );
    
        create sequence board_seq
            start with 1
            increment by 1
            maxvalue 99999
            nocache
            nocycle
            noorder;

4. CRUD 처리 구문

   
        --삽입
        insert into board(num, title, writer, content, regdate, cnt)
            values(board_seq.nextval, '제목1', '작성자1', '내용1', sysdate, 0);
        
        --조회
        select num, title, writer, content, regdate, cnt from board;
        
        --수정
        update board set title='제목수정', content='내용수정' where num=1;

        --삭제
        delete from board where num=1;

        --반드시 커밋할 것!!
        commit;    
