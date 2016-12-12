# DB16_SignUp

[데이터베이스 요구사항]

1. 학과는 학과이름, 캠퍼스구분을 가진다.
2. 학생은 학번, 이름, 입학년도, 학적, 재학학년, 전화번호, 이메일을 가진다.
3. 교수는 아이디, 이름, 전화번호, 이메일을 가진다.
4. 과목은 학수번호, 이수구분, 과목명, 학점, 제한인원, 수강인원, 강의시간, 강의실, 비고를 가진다.
5. 졸업요건은 학번, 학과, 전공, MSC, 일반교양, 핵심교양, 교양, 총학점을 가진다.
6. 학생과 교수는 단 하나의 학과에 속한다.
7. 한 학과는 여러개의 과목을 주관한다.
8. 교수는 여러 과목을 지도한다.
9. 학생은 여러 과목을 수강신청한다.
10. 한 과목은 여러명의 학생이 속할수 있고, 단 한명의 교수가 지도한다.
11. 학생은 해당학과 해당학번의 졸업요건을 확인할 수 있다.
12. 학생은 자신의 이전까지 수강기록을 확인할 수 있다.
13. 학생은 수강신청한 과목을 수강철회할 수 있다.
14. 학과는 여러개의 졸업요건을 가진다.
15. 한 학생은 중복된 시간에 여러 강의를 수강신청 할 수 없다.
16. 학생은 과목을 이수구분, 과목명, 학점, 시간등의 조건을 사용하여 검색할 수 있다.
17. 한 과목의 수강인원은 제한인원을 넘길 수 없다.
18. 학생은 현재까지 수강신청한 과목을 볼 수 있다.
19. 학생은 남아있는(자신이 수강한 이외) 졸업요건을 확인할 수 있다.


CREATE TABLE Department(
dp_name VARCHAR(45) not null,
office VARCHAR(45),
phone VARCHAR(45),
homepage VARCHAR(45),
primary key(pr_id));

create table Professor(
pr_id varchar(45) not null,
dp_name varchar(45),
passwd varchar(45),
phone varchar(45),
name varchar(45),
email varchar(45),
primary key(pr_id),
foreign key(dp_name) references Department(dp_name));

create table Student(
st_id varchar(45) not null,
passwd varchar(45),
dp_name varchar(45),
grade varchar(45),
phone varchar(45),
email varchar(45),
primary key(st_id),
foreign key(dp_name) references Department(dp_name));

create table Division(
division varchar(45) not null,
area varchar(45) not null,
primary key(division, area));

create table Subject(
sb_id varchar(45),
division varchar(45),
area varchar(45),
pr_id varchar(45),
name varchar(45),
credits int(11),
minPerson int(11),
regPerson int(11),
totPerson int(11),
time varchar(45),
classroom varchar(45),
campus varchar(45),
note varchar(45),
time1 varchar(45),
time2 varchar(45),
time3 varchar(45),
primary key(sb_id),
foreign key(division) references Division(division),
foreign key(area) references Division(area),
foreign key(pr_id) references Professor(pr_id));

create table Register(
st_id varchar(45),
sb_id varchar(45),
retake varchar(45),
primary key (st_id, sb_id),
foreign key (st_id) references Student(st_id),
foreign key(sb_id) references Subject(sb_id));
