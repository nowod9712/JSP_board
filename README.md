
!게시판 만들기 


SQL문 --
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

commit;    
