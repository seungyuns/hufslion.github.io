---
layout: post      # 수정 NO 
title: 예비세션_승윤 # 글 제목으로 수정
category: Session # 본인에게 맞는 카테고리명을 적으세요
--- 

 예비 세션: 페이스북 구현하기 _ 승윤.

# VS코드로 간단한 페이스북 구현하기.
---
<br>

*1. 페이스북 프로젝트를 담을 폴더 생성. *

2. VS코드 프로젝트 생성 및 실행.
```python 
  python –m venv myvenv
  
  source myvenv/Scripts/activate
```
&nbsp;3. 장고 설치하기.
```python 
  pip install django  
```
&nbsp;4. 프로젝트 생성하기.
```pyhton
  django-admin startproject facebook
```
&nbsp;5. 만든 프로젝트로 경로이동 후 서버돌려보기(django 페이지 확인).
```pyhton
  cd facebook
  
  python manage.py runserver
```
&nbsp;6. 앱 생성하기.
```python
  python manage.py startapp facebookapp
```
&nbsp;7. 프로젝트 폴더안 setting.py파일에 만든 앱 등록해주기.<br> &nbsp;&nbsp;&nbsp;(installed_apps 리스트 안에 --> <app이름>.apps.<첫글자대문자 app이름>Config)
```python 
  INSTALLED_APPS = [
    'facebookapp.apps.FacebookappConfig',
    ....생략
  ]
```
&nbsp;8. 만든 앱 폴더에 templates 폴더 생성 --> 안에 home.html 파일 추가.
&nbsp;9. views.py 폴더에 함수추가.
```python
  def home(request):
    return render(request, 'home.html')
```

  
  
