# 표준프레임워크 템플릿 프로젝트 내부업무 시스템

※ 본 프로젝트는 학습을 위해 표준프레임워크에서 제공하는 내부업무 시스템 템플릿을 가져와 일부를 수정한 프로젝트입니다.

## 프로젝트 소개

### 가져온 템플릿 개요

내부업무 기능 구현 시 필수적인 부분만 사용 가능하도록 경량화 된 실행환경 제공  
메인 페이지, 업무사용자 관리, 공지사항 관리, 게시판 관리, 권한 관리, 프로그램 관리, 메뉴 관리 기능을 제공
템플릿: https://github.com/eGovFramework/egovframe-enterprise-business-template

### 데이터 베이스 정보
템플릿에서 지원하는 5개의 데이터베이스 중 MySQL을 선택해서 템플릿에서 지원하는 DB구성을 다운받아 사용했다. 좋아요 기능을 담당하는 lettnbbslike 테이블을 추가하였다. 해당 테이블은 LIKE_ID라는 ids에서 관리되는 ID값, NTT_ID라는 해당하는 게시글을 지정할 때 사용하는 게시글의 ID값, USER_ID라는 해당하는 유저를 지정할 때 쓰는 해당 유저의 유니크ID값, LIKE_HATE라는 좋아요인지 싫어요인지를 구별하는 값을 가지는 컬럼들을 가진다.

## 좋아요 기능의 구현

### VO
게시글의 정보를 담는 BoardVO에 like, likeCnt, hateCnt 속성을 추가했다. 이들은 각각 jsp에서 넘어오는 좋아요, 싫어요의 상태, 해당 게시글의 좋아요 개수, 해당 게시글의 싫어요 개수를 뜻한다. 
좋아요 정보를 DB에 저장하고 DB에서 가져오기 위한 VO인 LikeVO를 새로 만들었는데 userId, nttId, likeHate, likeId라는 lettnbbslike 테이블의 컬럼들과 대응되는 속성들을 가진다.

### jsp
게시된 글을 볼 때 나타나는 EgovNoticeInquire.jsp 파일에 좋아요, 싫어요 버튼을 추가하고 각각 111, 222을 frm이라는 post의 like 속성에 넣고 submit하게 하는 fn_egov_like함수와 fn_egov_hate 함수를 추가하였다.

### controller
좋아요 버튼이나 싫어요 버튼을 눌렀을 때 호출되는 like.do에 매핑된 like 함수를 만들고 likeVO에 정보를 담은 뒤 bbsMngService.manageLike를 호출한 후 selectBoardArticle.do로 리다이렉트하는 기능을 구현하였다. 이때 세션에 정보를 담는 것을 유사하게 구현하기 위해 전역변수에 정보를 저장해놓도록 기능을 구현해놓았다.

### service

### DAO

### SQL

## 환경 설정
프로젝트에서 사용된 환경 프로그램 정보는 다음과 같다.
| 프로그램 명 | 버전 명 |
| :--------- | :------ |
| java | 1.8 이상 |
| maven | 3.8.4 |

## 프로젝트 실행

1. eclipse 하단의 Servers 탭을 클릭하고, 마우스 우클릭하여 **New > Server** 를 선택하여 서버를 설치한다.

2. 생성 또는 복사된 소스 내부의 DATABASE 폴더 내 dml, ddl을 참고하여 연결하고자 하는 DB에 테이블 생성 및 기초 데이터를 생성한다.  
   dml 및 ddl은 5가지 데이터베이스(Altibase, Cubrid, MySQL, Oracle, Tibero)를 지원한다.

![new_template_ebt_run1](https://user-images.githubusercontent.com/3771788/229034630-011a963b-e06b-4e72-8e0a-7ead977280a9.jpg)

3. [템플릿 구성 및 환경설정](https://www.egovframe.go.kr/wiki/doku.php?id=egovframework:let4:configration) 문서를 참고하여 템플릿 환경설정을 수행한다.

4. 실행할 프로젝트를 마우스 우클릭하고 **Run As > Run on Server** 를 선택한다.

