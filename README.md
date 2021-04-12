# Todo List

## Django Side

1. Install and setup (Django)

   1. `pip install django`
   1. `pip install django-rest-framework `
   1. `pip install django-cors-headers `
   1. `pip install djoser`
   1. `pip install pillow`

1. Setup settings.py install REST

```python
INSTALLED_APPS = [
    'rest_framework',
    'rest_framework.authtoken',
    'corsheaders',
    'djoser',
]

```

1. Then config urls

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/v1/', include('djoser.urls')),
    path('api/v1/', include('djoser.urls.authtoken')),
]
```

1. makemigration `python3 manage.py makemigration`
1. migrate `python3 manage.py migrate`
1. create super user `python3 manage.py createsuperuser`

## Vue Side

1. Install and setup (Vue)
   `npm install -g @vue/cli`
1. Include Font Awesome
1. Set up the base template
1. Create django app and models for products
1. Create serializer and views for the products
1. Create simple front page (latest products)
1. View a product
   1. Create viewset in Django
   1. Create vue page for showing product
   1. Add link to detail page
1. Setup opp Vuex / State
