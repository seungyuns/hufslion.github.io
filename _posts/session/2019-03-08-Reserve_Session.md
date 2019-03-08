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
* keep: 추후 공통html에 다른 내용이 들어갈 부분을 block으로 지정해주고, 들어가는 내용을 block으로 지정해 줘야함.   

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
* static파일을 사용할 html 상단에, static파일 불러오기.
```python
 {% load staticfiles %}
```
&nbsp;**22. 상단 디테일 잡기.**
* style 가장 상단에 기본 페이지 사이즈 조절 속성 추가(사이즈를 가장 쉽게 조절해주는 규칙적용, 관례적)
```css
{box-sizing: border-box; margin:0; padding:0;} 
```
* 검색창(.searchbar) width:100%로 만들고, border-radius: 4px.
* 상단(.header) 높이를 42px로 변경
* 검색창(.searchbar) padding:6px; margin-top:7px; 속성을 넣어 가운데 위치하게 만들기, color:#ffffff 입력.
* 버튼1을 이미지 파일로 변경
```html
<img src="/static/ic_pencil.jpg" width="22px" style="margin:9px 0 0 13px">
```
* 버튼2를 이미지 파일로 변경
```html
<img src="/static/ic_info.jpg" width="22px" style="margin:9px 0 0 13px">
```
&nbsp;**23. 하단 디테일 잡기.**
* tab1,2,3,4 style에 width:25% 속성 추가.
* 가운데 정렬을 위해 .footer style에 text-align:center 추가.
* 탭1을 이미지 파일로 변경 
```html
<img src="/static/ic_pencil.jpg" width="22px" style="margin:9px 0 0 13px">
```
* 탭2를 이미지 파일로 변경
```html
<img src="/static/ic_pencil.jpg" width="22px" style="margin:9px 0 0 13px">
```
* 탭3을 이미지 파일로 변경
```html
<img src="/static/ic_pencil.jpg" width="22px" style="margin:9px 0 0 13px">
```
* 탭4를 이미지 파일로 변경
```html
<img src="/static/ic_pencil.jpg" width="22px" style="margin:9px 0 0 13px">
```
* 하단(.footer)에 position:fixed; bottom: 0; left:0; right:0; 속성 추가. 
* .container의 height를 삭제하기.
* style최상단에 body{background-color: #d7d8dc;} 추가. (body의 배경색을 변경하면 웹화면 자체의 배경 색상을 변경하게됨.) 

&nbsp;**24. home.html 틀잡기. feed 생성**
* 공통(base.html)만들때 keep해둔 block 지정해주기. (content가 들어갈 부분을 지정해주기) base.html container에 블록 지정.
```python 
   <div class="container">
        {%block contents%}
        
        {%endblock%}    
    </div>
 ```
 * home.html 에 기본 html틀 잡고, block으로 감싸주기.
```html
{%extends 'base.html' %}
{%block contents%}
         
<div class="container">
    <div class="feed">
        <h3 class="name"> 이름</h3>
        <div class="date">날짜 </div>
        <a class="title"> 글 제목</a>
        <p class="content"> 글 내용</p>
        <div class="accessory">
            <img src="/static/ic_like.jpg" width="16px"> Like <img src="/static/ic_conmment.jpg" width="16px"> Comments
        </div>
    </div>
</div>

{%endblock%}  
```
&nbsp;**25. feed 속성 추가**
* 바탕 속성
```css
  .feed{
        background-color: #ffffff;
        border-top: 1px solid #c0c0c0;
        broder-bottom: 1px solid #c0c0c0;
        margin: 7px 0;
        padding: 12px;
    }
```
* 글자 속성
```css
 .date{
        color:#999;
        margin-bottom:10px;
    }
    .title{
        color:#6184dd;
        font-weight:600;
    }
    .content{
        margin-top:5px;
    }
    .accessory{
        border-top: 1px solid #eee;
        padding-top:10px;
        maargin-top:10px;
        color: #999;
        font-size:14px;
    }
```
&nbsp;**26. feed 속성 추가**
