Flask Examples 
=================

RESTFUL API endpoints built using Flask Framework (http://flask.pocoo.org/) and Sqlalchemy
(http://www.sqlalchemy.org/)

Requirements
------------
- Python 3
- Docker
- Docker-Compose


Installation
-------------

Create the docker environmnet with the following commands:
```
  cd dtools
  docker-compose up
```


Unit Tests
------------

Run the unit test suite with the following command:

```
python3 manage.py test --q src/tests/
```

To run all the tests inside one file:

```
python3 manage.py test --q src/tests/test_app.py 
```


To run a specific test:

```
python3 manage.py test --q src/tests/test_app.py::test_app_config
```



SqlAlchemy ORM
-----------------




DataBase Connection
---------------------



4. Create database:

        python manage.py syncdb


5. Run app:

        python manage.py runserver


User API
----------

The main goal is desing and built a RestFull API that handles user registration and login for a new service 
(let's say a music service but could be anything). The API format will be JSON. The first thing that we must do
is define a root url: ::

    http://[hostname]/mymusic/api/v1.0/


After that we will define the User Resource urls that will allows to create, query, update, delete an user.


Create an User
--------------

POST request to create an user: ::

    curl -X POST localhost:5000/mymusic/api/v1.0/users/ -H "Content-Type: application/json" \
         -d '{"username": "maigfrga", "email": "maigfrga@gmail.com", \
              "last_name": "franco", "first_name": "manuel"}'



This request will return a json with the user information, access_token included: ::

        {
          "user": {
            "access_token": "dda568fe6781259a1f9b910c6704b4da", 
            "email": "maigfrga@gmail.com", 
            "first_name": "manuel", 
            "id": 1, 
            "last_name": "franco", 
            "username": "maigfrga"
          }
        }



Authentication
--------------

GET, PUT, DELETE request requires authentication, the API expects two headers **api_access_token** and **api_username** the next example will return user information, authentication is required: ::


    curl  localhost:5000/mymusic/api/v1.0/users/ -H "api_access_token: dda568fe6781259a1f9b910c6704b4da" \
         -H "api_username: maigfrga"


This call will return the user data: ::

    {
        "access_token": "dda568fe6781259a1f9b910c6704b4da", 
        "email": "maigfrga@gmail.com", 
        "first_name": "manuel", 
        "id": 1, 
        "last_name": "franco", 
        "username": "maigfrga"
    }





Update an user
--------------

Perform a PUT request will update the user resource: ::


        curl -X PUT  localhost:5000/mymusic/api/v1.0/users/ -H "Content-Type: application/json" \
             -H "api_access_token: dda568fe6781259a1f9b910c6704b4da" \
             -H "api_username: maigfrga" -d '{"last_name": "last name modified"}'



Delete an user
--------------

Perform  a DELETE request will delete the user resource: ::

        curl -X DELETE  localhost:5000/mymusic/api/v1.0/users/  \
         -H "api_access_token: dda568fe6781259a1f9b910c6704b4da" \
         -H "api_username: maigfrga"


Useful commands
-------------------


### Kill all running docker containers:


 docker kill $(docker ps | grep pg | awk '{print $1}')
    


See also
---------
[Flask Framework Website](http://flask.pocoo.org)

[Flask python3 support](http://flask.pocoo.org/docs/python3/)

[Sqlalchemy Website](http://www.sqlalchemy.org/)

[Designing a RESTful API with Python and Flask](http://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask)

[Unit testing framework](http://docs.python.org/2/library/unittest.html)

[argparse — Parser for command-line options, arguments and sub-commands](http://docs.python.org/dev/library/argparse.html)

[Python @property versus getters and setters](http://stackoverflow.com/questions/6618002/python-property-versus-getters-and-setters)
