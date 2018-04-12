# Django 사용해보기!

## 1. Django란?
 - 파이썬으로 만든 웹 어플리케이션 프레임워크.
 - 기본적으로 프레임워크에 필요한 기능(회원가입, 로그인, 관리자 도구, 파일 업로드 등)이 미리 구현되어 있음.
 - 설치가 간편하여 빠르게 구축할 수 있음.

## 2. Django 설치하기
 ### 1. 설치 전 준비물 : python(django의 기반 언어), virtualenv(가상환경 설정 도구), pip(python 언어용 패키지 관리 시스템)
 - 가상환경을 사용하는 이유? : 파이썬2와 3이 호환이 되지 않는 것이 가장 큰 이유이다. 또한, 각자의 작업환경이 다른데 이를 무시하고 작업할 경우 호환이 되지 않아 공동작업이 어려울 수 있다.
 - virtualenv와 pip는 pipenv로 한번에 해결할 수도 있다.
 
 ### 2. 설치단계
 - python 설치 : 패키지 인스톨러를 통해 설치하기 때문에 어려운 작업은 아니다.
 - pip 설치 : 각 OS별로 설치법이 다르다. [참고 사이트(코딩도장)](http://codingdojang.com/scode/371)
 - virtualenv 설치 : 앞서 설치한 pip를 통해 virtualenv 패키지를 설치할 수 있다.
 - 가상환경 세팅 : 가상환경을 구축하고자 하는 폴더를 생성한 후 폴더안에서 'virtualenv 가상환경명'으로 생성 가능하다.
 - 가상환경 접속 : virtualenv로 가상환경 세팅 후 가상환경명\Scripts\Activate(윈도우 기준) 명령어를 실행하면, 가상환경으로 접속할 수 있다.
 - django 설치 : pip install django 명령을 실행하면 자동적으로 django 패키지가 설치된다.
 ![가상환경 세팅부터 django 설치 요약 스크린샷](https://github.com/pleasantlife/SayHelloToDjango/blob/master/virtual%20environment%20setup.png)
 - 프로젝트 생성 : 'django-admin startproject 프로젝트명' 명령어를 실행하여 프로젝트를 생성한다.
 - 어플리케이션 생성 : 프로젝트 폴더로 들어간 후, 'django-admin startapp 어플리케이션명' 명령어를 실행하여 어플리케이션을 생성한다.
 ![프로젝트 생성, 어플리케이션 생성 요약 스크린샷](https://github.com/pleasantlife/SayHelloToDjango/blob/master/django%20admin%20install.png)
 - 서버 구동 : manage.py가 위치한 폴더에서 'python manage.py runserver' 명령을 실행하면 서버 구동 완료.
 - 구동 확인 : 웹브라우저에서 127.0.0.1:8000에 접속했을 때, django 기본 페이지가 나오면 구동이 제대로 되고 있는 것이다.
 - 이 상태에서는 메인페이지 이외에는 접속할 수 없다.


## 3. admin 페이지 접속하기
 - 서버 구동이 완료되었다고 해서 admin 페이지에 접속할 수 있는 것은 아니다.
 - admin 페이지는 구성이 완료되었으나, admin 페이지는 계정이 필요하기 때문이다. 따라서, superuser 계정을 만들어야 한다.
 - 먼저, 'python manage.py makemigrations'와 'python manage.py migrate' 명령을 연속으로 입력해준다. (두 명령을 한번에 할 수도
 있으나, 안정적인 db 업데이트를 위해 나누어 수행하는 것을 권장한다.)
 - db 업데이트가 완료되면 manage.py 파일이 위치한 폴더에서 'python manage.py createsuperuser' 명령을 실행하고, username(id), 이메일주소, 비밀번호를 입력하면 superuser 계정 생성이 완료된다.

## 4. 간단한 설정
 - 환경설정에서는 언어, 시간대, 환경변수, 설치된 라이브러리 관리, 데이터베이스 관리 등을 할 수 있다.
 - 환경설정은 프로젝트 폴더 내의 settings.py에서 원하는 코드를 넣어서 설정한다.
### 4-1. 한국어 언어/ 한국 시간대 설정
 - 언어 : settings.py에서 'LANGUAGE_CODE'를 'ko-kr'로 변경한다.
 - 시간대 : settings.py에서 'TIME_ZONE'를 'Asia/Seou'로 변경한다.
```python
#settings.py 예시
LANGUAGE_CODE = 'ko-kr'

TIME_ZONE = 'Asia/Seoul'
```  


## 5. Restful API 만들기
 - Restful API? : 서버에서 데이터베이스의 Create, Read, Update, Delete가 가능하도록 짜여진 API를 말한다.
 - Django의 라이브러리인 'djangorestframework'를 이용하면 django로 Restful API를 만들 수 있다.
 - django의 데이터베이스에 Json 타입 데이터를 보내 추가하거나, 데이터베이스의 내용을 Json으로 받아볼 수 있도록 해준다.

### 3-1. DjangoRestFramework 적용하기
 - 설치 : 'pip install djangorestframework' 명령어로 설치한다.
 - django 서버에 적용 : 원하는 프로젝트의 settings.py 파일에서 INSTALLED_APP 부분에 'rest_framework'를 추가한다.
```python
# 문자열 배열의 마지막에도 쉼표를 꼭 넣어야 한다.
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework',
]
```