# Project : `mywebsite`
## App name : `blog`

```
(Project ROOT)
    > blog/ 
        > migrations
        > templates/
            > blog/
                > post_detail.html
                > post_form.html
            > base_generic.html
            > index.html
        > models.py
        > urls.py
        > views.py

    > mywebsite
        > settings.py
        > urls.py
    > static(부트스트랩 템플릿)
        > css
        > demo-images
        > fonts
        > images
        > js
    > manage.py

### Model
- **`Posting`** [글]
    - `title` : `CharField(200)`  [제목]
    - `title_image` : Imagefield(blank=True) [이미지 첨부]
    - `content` : `TextField()`   [내용]
    - `create_Date` : DateTimeField [최초 작성 시간]
    - `update_Date`: DateTimeField [수정 시간]
    - `category` : ManyToMany [분류]
   |미리보기: 300자까지|


### URL conf
```python
from django.urls import path
from . import views

** app_name** = 'blog'

urlpatterns = [
    # blog/create/
    path('', views.index, name='index'),
    path("post/<int:pk>", views.PostDetailview.as_view(), name="post"),
    path("post/create", views.PostCreate.as_view(), name="post_create"),
]
```

### Views
```python
from django.shortcuts import render
from blog.models import Category, Post
from django.views import generic
from django.contrib.auth.mixins import LoginRequiredMixin
from django.views.generic.edit import CreateView

def create_posting(request):
    내림차순

class PostDetailview(generic.DetailView):
    model = Post

class PostCreate(LoginRequiredMixin, CreateView):
    model = Post
    fields = ["title", "title_image", "content", "category"]


 Create Posting
    - `POST`
        - 새로운 Posting을 작성하는`post_form.html`을 제공
    
- Posting Index
    - 전체 Posting들을 조회하는 `index.html`을 제공
    - 상세 페이지로 이동할 수 있는 링크로 구성

- Posting Detail
    - 특정 Posting을 조회하는 `detail.html` 제공
    - Posting의 `title`/`content`/`image` 를 보여준다.
