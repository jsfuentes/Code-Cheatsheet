# Router

In the `app/urls.py`, add if it doesn't exist

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:question_id>/results', views.detail, name='detail'),
]
```

Then in the `project/urls.py`, where polls is the app folder name

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')), #sends remaining url to the includes
    path('', admin.site.urls),
]
```

