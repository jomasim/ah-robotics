[![Build Status](https://travis-ci.org/andela/ah-robotics.svg?branch=develop)](https://travis-ci.org/andela/ah-robotics)
[![Coverage Status](https://coveralls.io/repos/github/andela/ah-robotics/badge.svg?branch=develop)](https://coveralls.io/github/andela/ah-robotics?branch=develop)
[![Maintainability](https://api.codeclimate.com/v1/badges/fe82140229df3317bb50/maintainability)](https://codeclimate.com/github/andela/ah-robotics/maintainability)

# Authors Haven - A Social platform for the creative at heart

## Vision

Create a community of like minded authors to foster inspiration and innovation
by leveraging the modern web.

---

## Application local setup

### Technologies used to build and run application

1. [Brew](https://brew.sh/)
2. [Python](https://www.python.org/downloads/)
3. [Django](https://www.djangoproject.com/)
4. [DjangoRestFrameWork](https://www.django-rest-framework.org/)
5. [Virtualenv](https://virtualenv.pypa.io/en/latest/installation/)
6. [PostgreSQL](https://www.codementor.io/engineerapart/getting-started-with-postgresql-on-mac-osx-are8jcopb)

### Getting Started

1. Open terminal and clone the repo:

    `git clone https://github.com/andela/ah-robotics.git`

2. Change directory into the cloned repository.

    `cd ah-robotics`

3. Checkout to the Chore branch

    `git checkout ch-update-readme-163092870`

4. Create a virtual environment by running the following commands:

    `virtualenv -p python3 env`

    or

    `python3 -m virtualenv env`

5. Once the virtual environment has been setup, activate it and install the packages required by the project,
    these are contained in the file named `requirements.txt`

      `source env/bin/activate`

      `pip install -r requirements.txt`

### setting up the database

> Ensure PostgreSQL is installed and is running psql, follow these steps to create a new user and a database which will be used in the application.

  1. Start the postgres database server using the command:
  
      `pg_ctl -D /usr/local/var/postgres start`

  2. Run psql interactive terminal

      `psql postgres`

  3. Create a new user:

      `CREATE USER sample_username WITH PASSWORD 'sample_password';`

  4. Grant privileges to the user:

      `ALTER USER sample_username CREATEDB;`

  5. Create a database:

      `CREATE DATABASE sample_database_name WITH OWNER sample_username;`
  6. Create a .env as guided by the .env_example and add the following configuration variables

      ```source-json
      source env/bin/activate
      export DB_NAME="database_name"
      export DB_USER="sample_username"
      export DB_PASS="sample_password"
      export DB_HOST="host_name_eg_localhost"
      export DB_PORT="port_number_eg_5432"
      export TIME_DELTA="30"
      export EMAIL_HOST="smtp.gmail.com"
      export EMAIL_HOST_USER="testmail@mail.com"
      export EMAIL_HOST_PASSWORD="pass21234"
      export EMAIL_PORT=587
      export CLOUDINARY_NAME="cloudinary_name"
      export CLOUDINARY_KEY="cloudinary_key"
      export CLOUDINARY_SECRET="cloudinary_secret"
      ```

  7. Source .env to set the configuration variables:

      `source .env`
  8. Run migrations to create the tables in the database:

      ```source-json
      python manage.py makemigrations
      python manage.py migrate
      ```
  9. Collect static files

    python manage.py collectstatic

---

### Run The Server

Once everything has been setup, to run the application run the command:

   `python manage.py runserver`

The application can be accessed in the url <http://localhost:8000>

---

## Testing

To run the application run the command:

   `python manage.py test`

To determine test coverage on the application:

   `coverage run --source=authors/ manage.py test`

   `coverage report`

---

## API Spec

The preferred JSON object to be returned by the API should be structured as follows:

### Users (for authentication)

```source-json
{
  "user": {
    "email": "jake@jake.jake",
    "token": "jwt.token.here",
    "username": "jake",
    "bio": "I work at statefarm",
    "image": null
  }
}
```

### Profile

```source-json
{
  "profile": {
    "username": "jake",
    "bio": "I work at statefarm",
    "image": "image-link",
    "following": false
  }
}
```

### Single Article

```source-json
{
  "article": {
    "slug": "how-to-train-your-dragon",
    "title": "How to train your dragon",
    "description": "Ever wonder how?",
    "body": "It takes a Jacobian",
    "tagList": ["dragons", "training"],
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:48:35.824Z",
    "favorited": false,
    "favoritesCount": 0,
    "author": {
      "username": "jake",
      "bio": "I work at statefarm",
      "image": "https://i.stack.imgur.com/xHWG8.jpg",
      "following": false
    }
  }
}
```

### Multiple Articles

```source-json
{
  "articles":[{
    "slug": "how-to-train-your-dragon",
    "title": "How to train your dragon",
    "description": "Ever wonder how?",
    "body": "It takes a Jacobian",
    "tagList": ["dragons", "training"],
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:48:35.824Z",
    "favorited": false,
    "favoritesCount": 0,
    "author": {
      "username": "jake",
      "bio": "I work at statefarm",
      "image": "https://i.stack.imgur.com/xHWG8.jpg",
      "following": false
    }
  }, {

    "slug": "how-to-train-your-dragon-2",
    "title": "How to train your dragon 2",
    "description": "So toothless",
    "body": "It a dragon",
    "tagList": ["dragons", "training"],
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:48:35.824Z",
    "favorited": false,
    "favoritesCount": 0,
    "author": {
      "username": "jake",
      "bio": "I work at statefarm",
      "image": "https://i.stack.imgur.com/xHWG8.jpg",
      "following": false
    }
  }],
  "articlesCount": 2
}
```

### Single Comment

```source-json
{
  "comment": {
    "id": 1,
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:22:56.637Z",
    "body": "It takes a Jacobian",
    "author": {
      "username": "jake",
      "bio": "I work at statefarm",
      "image": "https://i.stack.imgur.com/xHWG8.jpg",
      "following": false
    }
  }
}
```

### Multiple Comments

```source-json
{
  "comments": [{
    "id": 1,
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:22:56.637Z",
    "body": "It takes a Jacobian",
    "author": {
      "username": "jake",
      "bio": "I work at statefarm",
      "image": "https://i.stack.imgur.com/xHWG8.jpg",
      "following": false
    }
  }],
  "commentsCount": 1
}
```

### List of Tags

```source-json
{
  "tags": [
    "reactjs",
    "angularjs"
  ]
}
```

### Errors and Status Codes

If a request fails any validations, expect errors in the following format:

```source-json
{
  "errors":{
    "body": [
      "can't be empty"
    ]
  }
}
```

### Other status codes

401 for Unauthorized requests, when a request requires authentication but it isn't provided

403 for Forbidden requests, when a request may be valid but the user doesn't have permissions to perform the action

404 for Not found requests, when a resource can't be found to fulfill the request

## Endpoints

### Authentication

`POST /api/users/login`

Example request body:

```source-json
{
  "user":{
    "email": "jake@jake.jake",
    "password": "jakejake"
  }
}
```

No authentication required, returns a User

Required fields: `email`, `password`

### Registration

`POST /api/users`

Example request body:

```source-json
{
  "user":{
    "username": "Jacob",
    "email": "jake@jake.jake",
    "password": "jakejake"
  }
}
```

No authentication required, returns a User

Required fields: `email`, `username`, `password`

### Get Current User

`GET /api/user`

Authentication required, returns a User that's the current user

### Update User

`PUT /api/user`

Example request body:

```source-json
{
  "user":{
    "email": "jake@jake.jake",
    "bio": "I like to skateboard",
    "image": "https://i.stack.imgur.com/xHWG8.jpg"
  }
}
```

Authentication required, returns the User

Accepted fields: `email`, `username`, `password`, `image`, `bio`

### Get Profile

`GET /api/profiles/:username`

Authentication optional, returns a Profile

### Follow user

`POST /api/profiles/:username/follow`

Authentication required, returns a Profile

No additional parameters required

### Unfollow user

`DELETE /api/profiles/:username/follow`

Authentication required, returns a Profile

No additional parameters required

### List Articles

`GET /api/articles`

Returns most recent articles globally by default, provide `tag`, `author` or `favorited` query parameter to filter results

Query Parameters:

Filter by tag:

`?tag=AngularJS`

Filter by author:

`?author=jake`

Favorited by user:

`?favorited=jake`

Limit number of articles (default is 20):

`?limit=20`

Offset/skip number of articles (default is 0):

`?offset=0`

Authentication optional, will return multiple articles, ordered by most recent first

### Feed Articles

`GET /api/articles/feed`

Can also take `limit` and `offset` query parameters like List Articles

Authentication required, will return multiple articles created by followed users, ordered by most recent first.

### Get Article

`GET /api/articles/:slug`

No authentication required, will return single article

### Create Article

`POST /api/articles`

Example request body:

```source-json
{
  "article": {
    "title": "How to train your dragon",
    "description": "Ever wonder how?",
    "body": "You have to believe",
    "tagList": ["reactjs", "angularjs", "dragons"]
  }
}
```

Authentication required, will return an Article

Required fields: `title`, `description`, `body`

Optional fields: `tagList` as an array of Strings

### Update Article

`PUT /api/articles/:slug`

Example request body:

```source-json
{
  "article": {
    "title": "Did you train your dragon?"
  }
}
```

Authentication required, returns the updated Article

Optional fields: `title`, `description`, `body`

The `slug` also gets updated when the `title` is changed

### Delete Article

`DELETE /api/articles/:slug`

Authentication required

### Add Comments to an Article

`POST /api/articles/:slug/comments`

Example request body:

```source-json
{
  "comment": {
    "body": "His name was my name too."
  }
}
```

Authentication required, returns the created Comment
Required field: `body`

### Get Comments from an Article

`GET /api/articles/:slug/comments`

Authentication optional, returns multiple comments

### Delete Comment

`DELETE /api/articles/:slug/comments/:id`

Authentication required

### Favorite Article

`POST /api/articles/:slug/favorite`

Authentication required, returns the Article
No additional parameters required

### Unfavorite Article

`DELETE /api/articles/:slug/favorite`

Authentication required, returns the Article

No additional parameters required

### Get Tags

`GET /api/tags`
