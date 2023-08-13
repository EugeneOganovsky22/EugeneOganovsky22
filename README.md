# Файл urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('news/<:news_id>/', views.news_detail, name='news_detail'),
]

# Файл views.py
from django.shortcuts import render
from .models import News

def index(request):
    news_list = News.objects.all()
    return render(request, 'news/index.html', {'news_list': news_list})

def news_detail(request, news_id):
    news = News.objects.get(id=news_id)
    return render(request, 'news/detail.html', {'news': news})

# Файл models.py
from django.db import models

class News(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    pub_date = models.DateTimeField(' published')

# Файл index.html
{% for news in news_list    <h2>{{ news.title }}</h2>
    <p>{{ news.content }}</p>
    <p>{{ news.pub_date }}</p>
{% endfor %}

# Файл detail.html
<h2>{{ news.title }}</h2>
<p>{{ news.content }}</p>
<p>{{ news.pub_date }}</p>
