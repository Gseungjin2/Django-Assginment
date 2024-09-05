# 1. 프로젝트 세팅

## 1.1 가상환경 구축하는 방법
* pyenv virtualenv 3.12.2 create_virtual_name
* pyenv local create_virtual_name
* poetry init
* poetry shell
* charm .

## 1.2 Django 설치및 프로젝트 구성
* poetry add django
* django-admin startproject create_pro_name
* django-admin startapp create_app_naem
```
* templats 경로 지정

config/settings.py

    TEMPLATES = [
      {
          'DIRS': [BASE_DIR / 'templates'],
      }
    ]
```
```
* static 경로지정

config/settings.py

  STATIC_URL = 'static/'
  STATIC_DIRS = BASE_DIR / 'static'
  STATICFILES_DIRS = [
      STATIC_DIRS,
  ]
  STATIC_ROOT = BASE_DIR / '.static_root'
```
```
* media 경로지정

config/settings.py

  # Media files
  MEDIA_URL = 'media/'
  MEDIA_ROOT = BASE_DIR / 'media'
```
## 2.1 데이터베이스 모델 정의하기
```
* app/models
  from django.db import moedels

  class Book(models.Model):
    rank = models.integer('책_순위')
    title = models.CharField('책제목', max_length=100)
    review = models.TextField()
```
## 2.2 각 필드별 특징 정리
```
1. CharField
  역할: 짧은 문자열을 저장할 때 사용됩니다.
  특징: 최대 길이를 max_length로 지정해야 함.
  주로 제목, 이름, 간단한 설명 등을 저장하는 데 적합함.

2. TextField
  역할: 길이에 제한이 없는 긴 텍스트를 저장할 때 사용됩니다.
  특징: 길이 제한 없이 텍스트를 저장 가능.
  주로 본문, 설명, 코멘트 등의 긴 내용을 저장하는 데 적합함.

3. IntegerField
  역할: 정수 값을 저장할 때 사용됩니다.
  특징: 숫자(정수)만 저장 가능.
  가격, 재고, 판매량 등 수량이나 숫자를 다룰 때 사용.

4. ForeignKey
  역할: 다른 모델과의 관계를 나타내는 외래 키를 정의할 때 사용됩니다.
  특징: 다른 모델과 1 관계를 나타냄.
  외래 키가 참조하는 객체가 삭제되었을 때 동작을 on_delete 옵션으로 지정해야 함.

5. choices
  역할: 필드에 선택할 수 있는 옵션을 제공할 때 사용됩니다.
  특징 choices에 지정한 값 중 하나만 선택할 수 있음.
  드롭다운 메뉴와 같은 UI에서 옵션을 제공할 때 유용.

6. default
  역할: 필드의 기본값을 설정할 때 사용됩니다.
  특징: 해당 필드에 값이 주어지지 않았을 때 자동으로 설정될 값.
```
## 2.3 migration에 대해서 정리하기
```
Migrations 정리
  Django에서 데이터베이스 스키마를 관리하고, 변경 사항을 추적하며 데이터베이스에 반영하는 메커니즘입니다.모델을 변경하거나 새로운 모델을 추가하면,
  이 변경 사항을 데이터베이스에도 반영해야 하는데, 이를 자동으로 처리해주는 것이 Django의 마이그레이션 시스템이다.
```
## 3.1 jinja 문법 정리하기
```
* Jinja는 Python 기반의 템플릿 엔진으로, 웹 프레임워크인 Flask와 Django에서 자주 사용됩니다. HTML이나 XML과 같은 마크업 언어에서 변수를 출력하거나 조건문, 반복문 등을 사용할 수 있게 해준다.
 
1. 변수 출력: {{ 변수 }}

2. 주석
기본 문법: {# 주석 내용 #}

3. 조건문
기본 문법: {% if 조건 %} ... {% endif %}

4. 반복문
기본 문법: {% for item in list %} ... {% endfor %}

5. 필터
기본 문법: {{ 변수 | 필터 }}

6. 매크로 (Macros)
기본 문법: {% macro name(params) %} ... {% endmacro %}
```
## 3.2 blok 사용법
```
* block은 템플릿에서 콘텐츠를 재정의하거나 확장할 때 사용하는 Jinja의 중요한 기능입니다. 주로 상속받은 템플릿에서 개별적으로 콘텐츠를 바꾸는 용도로 사용된다.

기본 문법
{% block 블록이름 %}
  <!-- 콘텐츠 -->
{% endblock %}
```
## 4.1 FBV란?
* FBV(Function-Based View)**는 Django에서 사용되는 함수 기반의 뷰를 의미합니다. Django에서는 뷰를 함수로 정의할 수 있으며,
  이를 통해 URL 요청에 대한 처리를 합니다. 간단한 요청 처리나 로직 구현 시 직관적이고 코드가 간결해지며, 작은 애플리케이션에서 자주 사용된다.

## 4.2 간단한 View 메소드 작성법
```
render 예시

from django.shortcuts import render

def bookmark(request):
    context = {'bookmarks': bookmarks}
    return render(request, 'bookmark_list', context)

redirect 예시

from django.shortcuts import redirect

def contact_view(request):
    if request.method == 'POST':
        return redirect('/') 
    return render(request, 'bookmark_list.html')
```
## 5.1 URL 엔드포인트란?
* URL 엔드포인트는 사용자가 웹 브라우저에서 입력한 특정 URL이 웹 애플리케이션의 특정 뷰(view)로 연결되는 지점을 의미합니다.

## 5.2 urlpatterns
* urlpatterns**는 Django에서 URL과 뷰를 매핑하는 리스트입니다. 각 URL 패턴을 path() 또는 re_path()로 정의하며,
  URL 요청이 들어왔을 때 어떤 뷰가 실행될지를 결정한다.

## 5.3 URL Include 개념 및 방법
* Django 프로젝트는 여러 앱(app)으로 나뉘어 관리될 수 있으며, 각각의 앱은 자체적인 urls.py 파일을 가질 수 있습니다. 
  URL Include는 각 앱의 urls.py를 메인 프로젝트의 urls.py에 포함시켜, URL 관리를 모듈화하고 조직적으로 관리하는 방법이다.

## 5.4 path
* path()**는 Django에서 URL 패턴을 정의할 때 사용하는 함수입니다. 간단한 경로 매칭을 제공하며, 
  URL 경로와 뷰 함수 또는 클래스 기반 뷰를 연결하는 역할을 한다.

## 5.5 include
* include()**는 Django에서 URL 패턴을 다른 URL 설정 파일로 나눌 때 사용하는 함수입니다. 
  주로 URL 패턴을 모듈화하여 각각의 앱이 독립적으로 URL 패턴을 관리하도록 할 때 사용됩니다.

```
예시

from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('shop/', include('shop.urls')),
]

* shop/urls.py의 URL 패턴을 shop/ 경로에 포함시켜, /shop/으로 시작하는 URL이 해당 앱으로 연결된다.
```

