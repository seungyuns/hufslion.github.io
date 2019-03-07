---
layout: post      # 수정 NO 
title: 예비세션_승윤 # 글 제목으로 수정
category: Session # 본인에게 맞는 카테고리명을 적으세요
--- 

 예비 세션: 페이스북 구현하기 _ 승윤.

# VS코드로 간단한 페이스북 구현하기.
---
<br>

&nbsp;**1. 페이스북 프로젝트를 담을 폴더 생성.**

&nbsp;**2. VS코드 프로젝트 생성 및 실행.**
```console 
  python –m venv myvenv
  
  source myvenv/Scripts/activate
```
&nbsp;**3. 장고 설치하기.**
```console 
  pip install django  
```
&nbsp;**4. 프로젝트 생성하기.**
```console
  django-admin startproject facebook
```
&nbsp;**5. 만든 프로젝트로 경로이동 후 서버돌려보기(django 페이지 확인).**
```console
  cd facebook
  
  python manage.py runserver
```
&nbsp;**6. 앱 생성하기.**
```console
  python manage.py startapp facebookapp
```
&nbsp;**7. 프로젝트 폴더안 setting.py파일에 만든 앱 등록해주기.<br> &nbsp;&nbsp;&nbsp;(installed_apps 리스트 안에 --> <app이름>.apps.<첫글자대문자 app이름>Config)**
```python 
  INSTALLED_APPS = [
    'facebookapp.apps.FacebookappConfig',
    ....생략
  ]
```
&nbsp;**8. 만든 앱 폴더에 templates 폴더 생성 --> 안에 home.html 파일 추가.**

&nbsp;**9. views.py 파일에 함수추가.**
```python
  def home(request):
    return render(request, 'home.html')
```
&nbsp;**10. url.py 파일에 views파일 임포트 및 경로설정.**
```python
 import facebookapp.views
 
 urlpatterns = [
    path('admin/', admin.site.urls),
    path('', facebookapp.views.home, name='home'),
]
```
&nbsp;**11. 최상단 폴더에 (manage.py가 있는 폴더) template폴더 생성 후 base.html 파일 추가.**

&nbsp;**12. setting.py파일 내 템플릿(TEMPLATES) 디렉토리 리스트에 공통 templates가 있는 경로 입력.**
```python 
 'DIRS': ['facebook/templates']
```
&nbsp;**13. setting.py파일 내 템플릿(TEMPLATES) 디렉토리 리스트에 공통 templates가 있는 경로 입력.**

&nbsp;**14. base.html에 기본 틀 잡아주기.**
```html
 <body>
    <style>
    </style>
    <div class="header">
        <div class="btn1">버튼1</div>
        <div class="search">
            <input type="text" class="searchbar" placeholder="Search">
        </div>
        <div class="btn2">버튼2</div>
    </div>
    <div class="container">
        내용물
    </div>
    <div class="footer">
        <div class="tab1">탭1</div>
        <div class="tab2">탭2</div>
        <div class="tab3">탭3</div>
        <div class="tab4">탭4</div>
    </div>
</body>
```
&nbsp;**15. home.html에서 공통파일(base.html) 불러오기.**
```python
 {%extends 'base.html' %}
```
&nbsp;**16. 확인하기 쉽게 base.html에 기본 css 입히기.**
```html
<style>
    .header {
        background-color: #475d9f;
        color: #fff;
    }
    .container {
        background-color: #d7d8dc;
    }
    .footer {
        background-color: gray;
    }
</style>
```
&nbsp;**17. 내용물 부분 .container 클래스 div 높이를 500px로 조정**
```css
 .container {     
    background-color: #d7d8dc;     
    height: 500px;
 }
```
&nbsp;**18. header안에 있는 버튼1, search, 버튼2 요소들을 한줄에 오도록 만들기.<br> &nbsp;이때 ﬂoat:left, ﬂoat:right을 사용해 띄워줄 수도 있고, position:absolute을 사용해 위치를 지정해줄 수도 있으며, dispaly:inline-block으로 한줄에 오게할 수 있습니다. 이번에는 position:absolute을 사용합니다.<br>&nbsp;
position:absolute 사용시 주의할 점은 같은 div 안에 있는 모든 요소가 absolute일 때 그 div에 반드시 높이값을 지정주어야 한다는 것 입니다. (absolute은 공중에 떠있는 상태기 때문에 안 쪽의 모든 요소가 absolute라면 내용물이 없다고 판단하여 높이가 0이 되기 때문)** 
```html
<style>
    .header {
        background-color: #475d9f;
        color: #fff;
        border-bottom: 1px solid #2c3863;
        height: 50px;
    }
    .btn1 {
        position: absolute;
        left: 10px;
    }
    .search {
        position: absolute;
        left: 100px;
        right: 100px;
   }
    .btn2 {
        position: absolute;
        right: 10px;
    }
    .container {
        background-color: #d7d8dc;
        height: 500px;
    }
    .footer {
        background-color: gray;
    }
</style>
```

&nbsp;**19. 이번에는 float:left방식으로 .footer안에 있는 탭1,2,3,4가 한줄에 오도록 만들기 <br>&nbsp; position:absoulte와 마찬가지로 height를 지정해주어야 한다.**
```css
    .footer {
        border-top: 1px solid #cccccc;
        background-color: #fafafa;
        height: 50px;
    }
    .tab1 {
        float: left;
    }
    .tab2 {
        float: left;
    }
    .tab3 {
        float: left;
    }
    .tab4 {
        float: left;
    }
 ```
&nbsp;**20. searchbar 테두리 넣기, 배경 색상 변경.**
```css
.searchbar {     
        border: 1px solid #2c3863;     
        background-color: #323f6b; 
    }
```
&nbsp;**21. 이미지 다운로드 및 static파일 생성**
* http://bit.ly/2z4e1rt
* facebookapp폴더에 static파일 생성. 
* 다운받은 이미지파일 static파일에 넣기.
* setting.py 파일 static파일 위치와 모을 위치 명시.
```python 
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'facebookapp', 'static')
]
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```
* 지정한 위치로 static파일 모으기.
```console
 python manage.py collectstatic
```


&nbsp;**21. 디테일 잡기.**
* tab1,2,3,4 style에 width:25% 속성 추가.
* 가운데 정렬을 위해 .footer style에 text-align:center 추가.
* 
