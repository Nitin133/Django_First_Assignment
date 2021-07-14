# Django_First_Assignment

An [HTTP request](https://rapidapi.com/blog/api-glossary/http-request-methods/) is an action to be performed on a resource identified by a given Request-URL. 

An [HTTP response](https://www.ibm.com/support/knowledgecenter/SSGMCP_5.3.0/com.ibm.cics.ts.internet.doc/topics/dfhtl22.html) is made by a server to a client. 

In this assignment, we would learn about different types of HTTP requests and Responses in Django. Django uses request and response objects to pass state through the system.

When a client requests a resource, an HttpRequest object is created, and correspond view function is called that returns the HttpResponse object.

To handle request and response, Django provides HttpRequest and HttpResponse/JsonResponse, classes

Some More details can be found here https://docs.djangoproject.com/en/3.1/ref/request-response/

This assignment will cover 4 HTTP request types i.e GET, POST, PUT, DELETE, and 2 response types HttpResponse and JsonResponse. 

At a High level, the Django application will perform different HTTP requests to perform some logical operations

### Some Guide for urls.py:
1. **Name in Django URL** -> name is used for accessing that URL from your Django / Python code. 
2. For example you have this in simpleapp/urls.py
3. **url(r'^main/', views.main, name='main')**
4. In point 2, "main" is the name of this URL
5. **URL namespaces** -> URL namespaces allow you to uniquely reverse named URL patterns even if different applications use the same URL names. 
At Line 21 in first_assignment/urls.py, path('', include(('simpleapp.urls', 'simpleapp'),namespace='simpleapp') ), **namespace='simpleapp'** is set
Remember, Both Name and Namespace are important for the assignment
6. For this assignment's test cases we have used some predefined names and namespace
7. Those names are defined below in the problem statement describes as "Django Url name"
8. Please make sure you use those names in Django URLs or else your assignment's test will fail
9. Summary: Namespace is "simpleapp" set in first_assignment/urls.py file and name is to be set for each URL in simpleapp/urls which is stated in the problem statement 

### API

API, short for Application Programming Interface, refers to a part of a computer program designed to be used or manipulated by another program, as opposed to an interface designed to be used or manipulated by a human
API contains the following parts
1. Base URL -> All requests we make to the API must begin with this portion of the URL. All APIs have a base URL like this one that is the same across all requests to the API. Our base URL is
```
http://127.0.0.1/
```
2. Url Path -> paths are endpoints (resources), such as /users or /reports/summary/, that your API exposes. In Django url file, we set these paths
3. Together they form an API. So suppose if you find /simple/?id=10, it means API for that URL is http://127.0.0.1/users/?id=10
4. **OR** /simple/10 is http://127.0.0.1/simple/10 
5. **OR** /simple/ -d 'id=10' is 
http://127.0.0.1/simple/
Body: {'id':'10'}


### API Testing
Once you create APIs, you have to test it
The recommended way to do API testing is through Postman or curl
We would be Using Postman to test these Apis
Postman is a scalable API testing tool 
Please follow this tutorial if you are new to Postman https://www.guru99.com/postman-tutorial.html OR https://www.youtube.com/watch?v=UTxmq4nmJ74
Postman Input/output Screenshots are attached after each use case below


Problem Statement
Create a Django Application with the Name "**simpleapp**". Following are some use cases 
1. Calculate the square of a given Number
2. Check whether a string is a palindrome
3. Add all the numbers in an array

## Part 1: Calculate the square of a Number
With following HTTP requests types GET, PUT, POST, DELETE

Calculate the square of a Number passed

Django URL name: array_addition

Parameter Name: number

1. GET:
```
# With No parameter passed
/simpleapp/
Response -> "Send Parameter number in url"
```
    /simpleapp/?number=10
    Response -> Square of Number 10 is 100"
```
Incorrect parameter Passed
 /simpleapp/?no.=10
    Response -> Square of Number 10 is 100"
```

![Image](./files/get_default.png)
![Image](./files/get_1.png)
![Image](./files/get_incorrect.png)


2. POST:
```
# With No data passed
    /simpleapp/
Response -> "Send Parameter number in data"
```
    /simpleapp/ -d "number=15"
    Response -> {"data": "Square of Number 15 is 225"}
```
Incorrect parameter Passed
/simpleapp/ -d "no.=15"
Response -> "Send Parameter number in data"
```
![Image](./files/post_default.png)
![Image](./files/post_1.png)
![Image](./files/post_incorrect.png)


3. PUT : 
```
# With No parameter passed
/simpleapp/
Response -> "Send Parameter as /simpleapp/<number>"
```
    /simpleapp/15
    Response -> {"data": "Square of Number 15 is 225"}

![Image](./files/put_default.png)
![Image](./files/put_1.png)

4. DELETE :
```
# With No parameter passed
/simpleapp/
Response -> "Send Parameter as /simpleapp/<number>"
```
    /simpleapp/15
    Response -> {"data": "Square of Number 15 is 225"}

![Image](./files/delete_default.png)
![Image](./files/delete_1.png)

#### Example Curl requests

curl -X POST "http://127.0.0.1:8000/simpleapp/" -d "number=10"

{"data": "Square of Number 10 is 100"}



## Part 2: Check whether a string is a palindrome
With the following HTTP requests types GET, PUT, POST, DELETE Check whether a string is a palindrome

Django URL name: palindrome_check

Parameter Name: string
1. GET
```
# With No parameter passed
/palindrome_check/
Response -> "Send Parameter string in URL to check palindrome"
```
    /palindrome_check/?string=calender
    Response -> "<b>calender</b> is not a palindrome"
```
Incorrect parameter Passed
/palindrome_check/?text=hello
Response -> "Send Parameter string in url to check palindrome"
```

![Image](./files/get_palindrome_default.png)
![Image](./files/get_palindrome_1.png)
![Image](./files/get_palindrome_incorrect.png)

2. POST
```
# With No data passed
/palindrome_check/
Response -> "Send Parameter string in data to check palindrome"
```
    /palindrome_check/ -d "string=abbbba"
    Response -> {"result": "abbbba is a palindrome"}
```
/palindrome_check/ -d "text=jjj"
Response -> "Send Parameter string in data to check palindrome"
```

![Image](./files/post_palindrome_default.png)
![Image](./files/post_palindrome_1.png)
![Image](./files/post_palindrome_incorrect.png)

3. PUT
```
# With No parameter passed
/palindrome_check/
Response -> "Send parameter as /palindrome_check/<string>"
```
    /palindrome_check/abbbba
    Response -> '{"result": "abbbba is a palindrome"}

![Image](./files/put_palindrome_default.png)
![Image](./files/put_palindrome_1.png)

4. DELETE
```
# With No parameter passed
    /palindrome_check/
    Response -> "Send parameter as /palindrome_check/<string>"
```
    /palindrome_check/abbbba
    Response -> '{"result": "abbbba is a palindrome"}
    
![Image](./files/delete_palindrome_default.png)
![Image](./files/delete_palindrome_1.png)

#### Example Curl Requests

curl -X PUT "http://127.0.0.1:8000/palindrome_check/a"

{"result": "a is a palindrome"}

curl -X POST "http://127.0.0.1:8000/palindrome_check/" -d "string=12"

{"result": "12 is not a palindrome"}


## Part 3: Add all the numbers separated by Comma
With the following HTTP requests types GET, POST add all the numbers separated by Comma


Django URL name: index

Parameter Name: array

1. GET
```
# With No parameter passed
    /array_addition/
    Response -> "Send Parameter array as comma seperated numbers 2,3,4,5"
```
    /array_addition/?array=100,200,300,1000
    Response -> "<h1>Sum is 1600</h1>"
```
    /array_addition/?array=1,-1,-3,3
    Response -> "<h1>Sum is 0</h1>"
```
    Incorrect Parameter
    /array_addition/?list=1,-1,-3,3
    Response -> "Send Parameter array as comma seperated numbers 2,3,4,5"
```
```
![Image](./files/get_array_default.png)
![Image](./files/get_array_1.png)
![Image](./files/get_array_2.png)
![Image](./files/get_array_incorrect.png)


2. POST

```
    #With No data passed
    /array_addition/
    Response -> "Send Parameter array in data as comma seperated numbers 2,3,4,5"
```
    /array_addition/ -d "array=22,25,100,3"
    Response -> {"sum": "150"}
```
Incorrect Parameter
/array_addition/ -d "list=22,25,100,3"
Response -> {"sum": "150"}
```

![Image](./files/post_array_default.png)
![Image](./files/post_array_1.png)
![Image](./files/post_array_incorrect.png)

## Installation Steps
1. Open up your Terminal / Command Line
2. git clone the repository
3. cd into the directory of the step (the one you just git cloned)
4. make sure you have python3 installed
5. Install virtualenv by following the steps 
```
Mac
python3 -m pip install --user virtualenv
python3 -m venv env
source env/bin/activate

Windows
py -m pip install --user virtualenv
py -m venv env
.\env\Scripts\activate
```
6. Run 
```
python -m pip install -r requirements/requirements.txt
```
6. No Database setup needs to be done. Do not edit Database settings in settings.py

7. If everything runs fine till here, create the application using the command
```
python manage.py startapp simpleapp
```
8. Now uncomment the following lines
```
Line 21 in first_assignment/urls.py -> path('', include(('simpleapp.urls', 'simpleapp'),namespace='simpleapp') ),
Line 40 in first_assignment/settings.py -> 'simpleapp',
```
Now Create File simpleapp/urls.py and add lines
```
from django.urls import path

from . import views
urlpatterns = []
```
9. Run 
```
python manage.py makemigrations
```
10. Now Run the Server using command
```
python manage.py runserver
```
11.  Great! Start Coding the assignment for above usecase
12. After Finishing the assignment, you can test them locally using command 
```
coverage run --source='.' manage.py test --no-input
```
12. Push the code into the repo using git, Check Pull Requests Tab. Open PR #1
13. Check if all the tests are Passed
14. Contact TA for the review

Video links

![Video 1](./files/video_1.mov)

![Video 2](./files/video_2.mov)
