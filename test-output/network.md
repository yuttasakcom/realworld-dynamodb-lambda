```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-kj77zn@email.com",
    "username": "author-kj77zn",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-kj77zn@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1rajc3em4iLCJpYXQiOjE1ODA0MjM4MDgsImV4cCI6MTU4MDU5NjYwOH0.z9ou8SStl9JEZrzVXP_2_6xHAZhPd27fpWkM-qxrNzM",
    "username": "author-kj77zn",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-4p68ya@email.com",
    "username": "authoress-4p68ya",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-4p68ya@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy00cDY4eWEiLCJpYXQiOjE1ODA0MjM4MDksImV4cCI6MTU4MDU5NjYwOX0.12H3EsskhcNWVVTY8ERs_1vFt0OodapLGrcgk9cKVto",
    "username": "authoress-4p68ya",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-g67xlj@email.com",
    "username": "non-author-g67xlj",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-g67xlj@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItZzY3eGxqIiwiaWF0IjoxNTgwNDIzODA5LCJleHAiOjE1ODA1OTY2MDl9.sN1rFwjTM1P-88DJygI7P4slnOLTc3vB-VpNCqtUTw0",
    "username": "non-author-g67xlj",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-plz49m",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423809174,
    "updatedAt": 1580423809174,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-543wtc",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423809213,
    "updatedAt": 1580423809213,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-plz49m
```
```
200 OK

{
  "article": {
    "createdAt": 1580423809174,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-plz49m",
    "updatedAt": 1580423809174,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-543wtc
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1580423809213,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-543wtc",
    "updatedAt": 1580423809213,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/9f0d4w
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [9f0d4w]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-543wtc

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1580423809213,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-543wtc",
    "updatedAt": 1580423809213,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-543wtc

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1580423809213,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-543wtc",
    "updatedAt": 1580423809213,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-543wtc

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1580423809213,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-543wtc",
    "updatedAt": 1580423809213,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-543wtc

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-543wtc

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-543wtc

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-543wtc

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-543wtc]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-543wtc

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-kj77zn]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-plz49m/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1580423809174,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-plz49m",
    "updatedAt": 1580423809174,
    "favoritedBy": [
      "non-author-g67xlj"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-plz49m
```
```
200 OK

{
  "article": {
    "createdAt": 1580423809174,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-plz49m",
    "updatedAt": 1580423809174,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-plz49m/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-plz49m_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-plz49m_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-plz49m/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1580423809174,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-plz49m",
    "updatedAt": 1580423809174,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-plz49m
```
```
200 OK

{}
```
```
GET /articles/title-plz49m
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-plz49m]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-543wtc
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-kj77zn]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "c0lg0m",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-sg5ibf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810234,
    "updatedAt": 1580423810234,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "c0lg0m",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "6s2l72",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mkqd2c",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810272,
    "updatedAt": 1580423810272,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "6s2l72",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "c0qy75",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-9t50zv",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810299,
    "updatedAt": 1580423810299,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "c0qy75",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "611oix",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-lr1ran",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810324,
    "updatedAt": 1580423810324,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "611oix",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ppjd1i",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-v1cb72",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810348,
    "updatedAt": 1580423810348,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ppjd1i",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "l194b0",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2qq5z1",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810373,
    "updatedAt": 1580423810373,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "l194b0",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "gfcx2o",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-4kw0kc",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810398,
    "updatedAt": 1580423810398,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "gfcx2o",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tf2d3r",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-img122",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810421,
    "updatedAt": 1580423810421,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tf2d3r",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "r1z3ys",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-xdlsd5",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810451,
    "updatedAt": 1580423810451,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "r1z3ys",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "4bnjc3",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-j3z9g9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810478,
    "updatedAt": 1580423810478,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "4bnjc3",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "otwqc6",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-o8sgh6",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810508,
    "updatedAt": 1580423810508,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "otwqc6",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "2dx9qv",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-d98m7y",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810535,
    "updatedAt": 1580423810535,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "2dx9qv",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "j89bbq",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ggi12m",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810559,
    "updatedAt": 1580423810559,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "j89bbq",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "82pwog",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-w3srb4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810582,
    "updatedAt": 1580423810582,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "82pwog",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "adjl0h",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3ymz7n",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810606,
    "updatedAt": 1580423810606,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "adjl0h",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "5f8ogg",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wzep10",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810630,
    "updatedAt": 1580423810630,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "5f8ogg",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "yacxf4",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-f51znb",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810662,
    "updatedAt": 1580423810662,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "yacxf4",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "qdvdjg",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-18tgfi",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810688,
    "updatedAt": 1580423810688,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "qdvdjg",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "xah7dl",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-dv7hhn",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810717,
    "updatedAt": 1580423810717,
    "author": {
      "username": "authoress-4p68ya",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "xah7dl",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "xtnstj",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-xxxwmf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423810760,
    "updatedAt": 1580423810760,
    "author": {
      "username": "author-kj77zn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "xtnstj",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "xtnstj"
      ],
      "createdAt": 1580423810760,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxxwmf",
      "updatedAt": 1580423810760,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "xah7dl"
      ],
      "createdAt": 1580423810717,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dv7hhn",
      "updatedAt": 1580423810717,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qdvdjg",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810688,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-18tgfi",
      "updatedAt": 1580423810688,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yacxf4"
      ],
      "createdAt": 1580423810662,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f51znb",
      "updatedAt": 1580423810662,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5f8ogg",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810630,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wzep10",
      "updatedAt": 1580423810630,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "adjl0h",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810606,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ymz7n",
      "updatedAt": 1580423810606,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "82pwog",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810582,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3srb4",
      "updatedAt": 1580423810582,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j89bbq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810559,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ggi12m",
      "updatedAt": 1580423810559,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2dx9qv",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810535,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-d98m7y",
      "updatedAt": 1580423810535,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "otwqc6",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810508,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o8sgh6",
      "updatedAt": 1580423810508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4bnjc3",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810478,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j3z9g9",
      "updatedAt": 1580423810478,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r1z3ys",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810451,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xdlsd5",
      "updatedAt": 1580423810451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "tf2d3r"
      ],
      "createdAt": 1580423810421,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-img122",
      "updatedAt": 1580423810421,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gfcx2o",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810398,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kw0kc",
      "updatedAt": 1580423810398,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l194b0",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810373,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2qq5z1",
      "updatedAt": 1580423810373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ppjd1i",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810348,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1cb72",
      "updatedAt": 1580423810348,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "611oix",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810324,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lr1ran",
      "updatedAt": 1580423810324,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0qy75",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810299,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9t50zv",
      "updatedAt": 1580423810299,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6s2l72",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810272,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mkqd2c",
      "updatedAt": 1580423810272,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0lg0m",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810234,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sg5ibf",
      "updatedAt": 1580423810234,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "tf2d3r"
      ],
      "createdAt": 1580423810421,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-img122",
      "updatedAt": 1580423810421,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qdvdjg",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810688,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-18tgfi",
      "updatedAt": 1580423810688,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "adjl0h",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810606,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ymz7n",
      "updatedAt": 1580423810606,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2dx9qv",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810535,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-d98m7y",
      "updatedAt": 1580423810535,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r1z3ys",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810451,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xdlsd5",
      "updatedAt": 1580423810451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l194b0",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810373,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2qq5z1",
      "updatedAt": 1580423810373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0qy75",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810299,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9t50zv",
      "updatedAt": 1580423810299,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-4p68ya
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "xah7dl"
      ],
      "createdAt": 1580423810717,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dv7hhn",
      "updatedAt": 1580423810717,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yacxf4"
      ],
      "createdAt": 1580423810662,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f51znb",
      "updatedAt": 1580423810662,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "adjl0h",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810606,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ymz7n",
      "updatedAt": 1580423810606,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j89bbq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810559,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ggi12m",
      "updatedAt": 1580423810559,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "otwqc6",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810508,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o8sgh6",
      "updatedAt": 1580423810508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r1z3ys",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810451,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xdlsd5",
      "updatedAt": 1580423810451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gfcx2o",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810398,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kw0kc",
      "updatedAt": 1580423810398,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ppjd1i",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810348,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1cb72",
      "updatedAt": 1580423810348,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0qy75",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810299,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9t50zv",
      "updatedAt": 1580423810299,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0lg0m",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810234,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sg5ibf",
      "updatedAt": 1580423810234,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-g67xlj
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-kj77zn&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "xtnstj"
      ],
      "createdAt": 1580423810760,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxxwmf",
      "updatedAt": 1580423810760,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qdvdjg",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810688,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-18tgfi",
      "updatedAt": 1580423810688,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-kj77zn&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "5f8ogg",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810630,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wzep10",
      "updatedAt": 1580423810630,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "82pwog",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810582,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3srb4",
      "updatedAt": 1580423810582,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "xtnstj"
      ],
      "createdAt": 1580423810760,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxxwmf",
      "updatedAt": 1580423810760,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "xah7dl"
      ],
      "createdAt": 1580423810717,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dv7hhn",
      "updatedAt": 1580423810717,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qdvdjg",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810688,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-18tgfi",
      "updatedAt": 1580423810688,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yacxf4"
      ],
      "createdAt": 1580423810662,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f51znb",
      "updatedAt": 1580423810662,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5f8ogg",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810630,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wzep10",
      "updatedAt": 1580423810630,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "adjl0h",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810606,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ymz7n",
      "updatedAt": 1580423810606,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "82pwog",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810582,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3srb4",
      "updatedAt": 1580423810582,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j89bbq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810559,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ggi12m",
      "updatedAt": 1580423810559,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2dx9qv",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810535,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-d98m7y",
      "updatedAt": 1580423810535,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "otwqc6",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810508,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o8sgh6",
      "updatedAt": 1580423810508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4bnjc3",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810478,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j3z9g9",
      "updatedAt": 1580423810478,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r1z3ys",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810451,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xdlsd5",
      "updatedAt": 1580423810451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "tf2d3r"
      ],
      "createdAt": 1580423810421,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-img122",
      "updatedAt": 1580423810421,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gfcx2o",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810398,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kw0kc",
      "updatedAt": 1580423810398,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l194b0",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810373,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2qq5z1",
      "updatedAt": 1580423810373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ppjd1i",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810348,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1cb72",
      "updatedAt": 1580423810348,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "611oix",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810324,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lr1ran",
      "updatedAt": 1580423810324,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0qy75",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810299,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9t50zv",
      "updatedAt": 1580423810299,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6s2l72",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810272,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mkqd2c",
      "updatedAt": 1580423810272,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0lg0m",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810234,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sg5ibf",
      "updatedAt": 1580423810234,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-4p68ya/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-4p68ya",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "xah7dl"
      ],
      "createdAt": 1580423810717,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dv7hhn",
      "updatedAt": 1580423810717,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yacxf4"
      ],
      "createdAt": 1580423810662,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f51znb",
      "updatedAt": 1580423810662,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "adjl0h",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810606,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ymz7n",
      "updatedAt": 1580423810606,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j89bbq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810559,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ggi12m",
      "updatedAt": 1580423810559,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "otwqc6",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810508,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o8sgh6",
      "updatedAt": 1580423810508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r1z3ys",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810451,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xdlsd5",
      "updatedAt": 1580423810451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gfcx2o",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810398,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kw0kc",
      "updatedAt": 1580423810398,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ppjd1i",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810348,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1cb72",
      "updatedAt": 1580423810348,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0qy75",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810299,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9t50zv",
      "updatedAt": 1580423810299,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0lg0m",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810234,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sg5ibf",
      "updatedAt": 1580423810234,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-kj77zn/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-kj77zn",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "xtnstj"
      ],
      "createdAt": 1580423810760,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxxwmf",
      "updatedAt": 1580423810760,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "xah7dl"
      ],
      "createdAt": 1580423810717,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dv7hhn",
      "updatedAt": 1580423810717,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qdvdjg",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810688,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-18tgfi",
      "updatedAt": 1580423810688,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "yacxf4"
      ],
      "createdAt": 1580423810662,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f51znb",
      "updatedAt": 1580423810662,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5f8ogg",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810630,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wzep10",
      "updatedAt": 1580423810630,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "adjl0h",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810606,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ymz7n",
      "updatedAt": 1580423810606,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "82pwog",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810582,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3srb4",
      "updatedAt": 1580423810582,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j89bbq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810559,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ggi12m",
      "updatedAt": 1580423810559,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2dx9qv",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810535,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-d98m7y",
      "updatedAt": 1580423810535,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "otwqc6",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810508,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o8sgh6",
      "updatedAt": 1580423810508,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4bnjc3",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810478,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j3z9g9",
      "updatedAt": 1580423810478,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r1z3ys",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810451,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xdlsd5",
      "updatedAt": 1580423810451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "tf2d3r"
      ],
      "createdAt": 1580423810421,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-img122",
      "updatedAt": 1580423810421,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gfcx2o",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810398,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kw0kc",
      "updatedAt": 1580423810398,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l194b0",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810373,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2qq5z1",
      "updatedAt": 1580423810373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ppjd1i",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810348,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v1cb72",
      "updatedAt": 1580423810348,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "611oix",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810324,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lr1ran",
      "updatedAt": 1580423810324,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0qy75",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1580423810299,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9t50zv",
      "updatedAt": 1580423810299,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6s2l72",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1580423810272,
      "author": {
        "username": "author-kj77zn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mkqd2c",
      "updatedAt": 1580423810272,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c0lg0m",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1580423810234,
      "author": {
        "username": "authoress-4p68ya",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sg5ibf",
      "updatedAt": 1580423810234,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "c0lg0m",
    "tag_0",
    "tag_mod_2_0",
    "tag_mod_3_0",
    "gfcx2o",
    "tag_6",
    "tag_a",
    "tag_b",
    "c0qy75",
    "tag_2",
    "tag_mod_3_2",
    "6s2l72",
    "tag_1",
    "tag_mod_2_1",
    "tag_mod_3_1",
    "tag_18",
    "xah7dl",
    "tag_7",
    "tf2d3r",
    "tag_19",
    "xtnstj",
    "adjl0h",
    "tag_14",
    "ppjd1i",
    "tag_4",
    "5f8ogg",
    "tag_15",
    "otwqc6",
    "tag_10",
    "4bnjc3",
    "tag_9",
    "l194b0",
    "tag_5",
    "j89bbq",
    "tag_12",
    "611oix",
    "tag_3",
    "r1z3ys",
    "tag_8",
    "qdvdjg",
    "tag_17",
    "2dx9qv",
    "tag_11",
    "tag_16",
    "yacxf4",
    "82pwog",
    "tag_13"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-7ti1w@email.com",
    "username": "author-7ti1w",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-7ti1w@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci03dGkxdyIsImlhdCI6MTU4MDQyMzgxMiwiZXhwIjoxNTgwNTk2NjEyfQ.T5ikBdb0v7rrQR1qYuXSTPQh9QHO2M1TMcCvG692HI8",
    "username": "author-7ti1w",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-ap24ed@email.com",
    "username": "commenter-ap24ed",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-ap24ed@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1hcDI0ZWQiLCJpYXQiOjE1ODA0MjM4MTIsImV4cCI6MTU4MDU5NjYxMn0.drSWdWrskmK6RLNMcUd_yIfY2fynLoDimplmGUhSsOY",
    "username": "commenter-ap24ed",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-we56tp",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1580423812122,
    "updatedAt": 1580423812122,
    "author": {
      "username": "author-7ti1w",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment 846ayz"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "0c673028-e56a-4cec-9ff4-0a9a0fcaa1f1",
    "slug": "title-we56tp",
    "body": "test comment 846ayz",
    "createdAt": 1580423812149,
    "updatedAt": 1580423812149,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment tk2mil"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "518acd5d-8d53-4b54-82d7-293c92c903dc",
    "slug": "title-we56tp",
    "body": "test comment tk2mil",
    "createdAt": 1580423812185,
    "updatedAt": 1580423812185,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment dj7zam"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "761cbbaf-57d9-4e94-9362-af3e7c9b68d4",
    "slug": "title-we56tp",
    "body": "test comment dj7zam",
    "createdAt": 1580423812217,
    "updatedAt": 1580423812217,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment xiz6cf"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "46501b6b-2626-4fb4-90bd-db1b73d2d822",
    "slug": "title-we56tp",
    "body": "test comment xiz6cf",
    "createdAt": 1580423812252,
    "updatedAt": 1580423812252,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment qrbkjv"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "61756eae-b2be-4f81-9440-8ee228adb2d8",
    "slug": "title-we56tp",
    "body": "test comment qrbkjv",
    "createdAt": 1580423812279,
    "updatedAt": 1580423812279,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment 6ecxmc"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "fb91cd44-cec7-42d6-92af-b5c27cacc433",
    "slug": "title-we56tp",
    "body": "test comment 6ecxmc",
    "createdAt": 1580423812305,
    "updatedAt": 1580423812305,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment d8u7kj"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "771b04f7-4f5d-4df7-b45d-7ce2da708952",
    "slug": "title-we56tp",
    "body": "test comment d8u7kj",
    "createdAt": 1580423812335,
    "updatedAt": 1580423812335,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment mmm0b0"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "16217248-e4bd-4da0-9509-cee4e6ef830d",
    "slug": "title-we56tp",
    "body": "test comment mmm0b0",
    "createdAt": 1580423812362,
    "updatedAt": 1580423812362,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment hnbpkq"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "ac715284-6e72-46d8-ab4f-281f09dd8fc9",
    "slug": "title-we56tp",
    "body": "test comment hnbpkq",
    "createdAt": 1580423812401,
    "updatedAt": 1580423812401,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-we56tp/comments

{
  "comment": {
    "body": "test comment -zdlhss"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "01371a78-d581-4313-98e1-62c2e36e6a92",
    "slug": "title-we56tp",
    "body": "test comment -zdlhss",
    "createdAt": 1580423812429,
    "updatedAt": 1580423812429,
    "author": {
      "username": "commenter-ap24ed",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-we56tp/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-we56tp/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment d2g58m"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-we56tp/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1580423812185,
      "id": "518acd5d-8d53-4b54-82d7-293c92c903dc",
      "body": "test comment tk2mil",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812185
    },
    {
      "createdAt": 1580423812335,
      "id": "771b04f7-4f5d-4df7-b45d-7ce2da708952",
      "body": "test comment d8u7kj",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812335
    },
    {
      "createdAt": 1580423812305,
      "id": "fb91cd44-cec7-42d6-92af-b5c27cacc433",
      "body": "test comment 6ecxmc",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812305
    },
    {
      "createdAt": 1580423812401,
      "id": "ac715284-6e72-46d8-ab4f-281f09dd8fc9",
      "body": "test comment hnbpkq",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812401
    },
    {
      "createdAt": 1580423812362,
      "id": "16217248-e4bd-4da0-9509-cee4e6ef830d",
      "body": "test comment mmm0b0",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812362
    },
    {
      "createdAt": 1580423812217,
      "id": "761cbbaf-57d9-4e94-9362-af3e7c9b68d4",
      "body": "test comment dj7zam",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812217
    },
    {
      "createdAt": 1580423812429,
      "id": "01371a78-d581-4313-98e1-62c2e36e6a92",
      "body": "test comment -zdlhss",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812429
    },
    {
      "createdAt": 1580423812252,
      "id": "46501b6b-2626-4fb4-90bd-db1b73d2d822",
      "body": "test comment xiz6cf",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812252
    },
    {
      "createdAt": 1580423812149,
      "id": "0c673028-e56a-4cec-9ff4-0a9a0fcaa1f1",
      "body": "test comment 846ayz",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812149
    },
    {
      "createdAt": 1580423812279,
      "id": "61756eae-b2be-4f81-9440-8ee228adb2d8",
      "body": "test comment qrbkjv",
      "slug": "title-we56tp",
      "author": {
        "username": "commenter-ap24ed",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1580423812279
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-we56tp/comments/0c673028-e56a-4cec-9ff4-0a9a0fcaa1f1
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-we56tp/comments/518acd5d-8d53-4b54-82d7-293c92c903dc
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-ap24ed]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-we56tp/comments/518acd5d-8d53-4b54-82d7-293c92c903dc
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-we56tp/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.we9k5bh8erj@email.com",
    "username": "user1-0.we9k5bh8erj",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.we9k5bh8erj@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAud2U5azViaDhlcmoiLCJpYXQiOjE1ODA0MjM4MTIsImV4cCI6MTU4MDU5NjYxMn0.AAUfQ_Ap8r1aPC8nwZYlxL4SKqVCq8Xo2gYZ8OOEYKU",
    "username": "user1-0.we9k5bh8erj",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.we9k5bh8erj@email.com",
    "username": "user1-0.we9k5bh8erj",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.we9k5bh8erj]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.we9k5bh8erj@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.we9k5bh8erj@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.we9k5bh8erj@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.we9k5bh8erj@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAud2U5azViaDhlcmoiLCJpYXQiOjE1ODA0MjM4MTIsImV4cCI6MTU4MDU5NjYxMn0.AAUfQ_Ap8r1aPC8nwZYlxL4SKqVCq8Xo2gYZ8OOEYKU",
    "username": "user1-0.we9k5bh8erj",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.ib2i7hzqy7j",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.ib2i7hzqy7j]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.we9k5bh8erj@email.com",
    "password": "0.yabhoabep7s"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.we9k5bh8erj@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAud2U5azViaDhlcmoiLCJpYXQiOjE1ODA0MjM4MTIsImV4cCI6MTU4MDU5NjYxMn0.AAUfQ_Ap8r1aPC8nwZYlxL4SKqVCq8Xo2gYZ8OOEYKU",
    "username": "user1-0.we9k5bh8erj",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.we9k5bh8erj
```
```
200 OK

{
  "profile": {
    "username": "user1-0.we9k5bh8erj",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.zl4j620cxsa
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.zl4j620cxsa]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1ODA0MjM4MTIsImV4cCI6MTU4MDU5NjYxMn0.zMr2yx2CS0f8yrDSxqXWxSbX1fwcvt0E5HbuQA-rRQM",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.e5lqdvfg7l5",
    "email": "user2-0.e5lqdvfg7l5@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.e5lqdvfg7l5@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuZTVscWR2Zmc3bDUiLCJpYXQiOjE1ODA0MjM4MTMsImV4cCI6MTU4MDU5NjYxM30.Ix7LEDCqnVobWkfXScSzks5HxRzHm975zMvtr8ovJVc",
    "username": "user2-0.e5lqdvfg7l5",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.we9k5bh8erj@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.we9k5bh8erj",
    "email": "updated-user1-0.we9k5bh8erj@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAud2U5azViaDhlcmoiLCJpYXQiOjE1ODA0MjM4MTIsImV4cCI6MTU4MDU5NjYxMn0.AAUfQ_Ap8r1aPC8nwZYlxL4SKqVCq8Xo2gYZ8OOEYKU"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.we9k5bh8erj",
    "email": "updated-user1-0.we9k5bh8erj@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAud2U5azViaDhlcmoiLCJpYXQiOjE1ODA0MjM4MTIsImV4cCI6MTU4MDU5NjYxMn0.AAUfQ_Ap8r1aPC8nwZYlxL4SKqVCq8Xo2gYZ8OOEYKU"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.we9k5bh8erj",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAud2U5azViaDhlcmoiLCJpYXQiOjE1ODA0MjM4MTIsImV4cCI6MTU4MDU5NjYxMn0.AAUfQ_Ap8r1aPC8nwZYlxL4SKqVCq8Xo2gYZ8OOEYKU"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.we9k5bh8erj",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAud2U5azViaDhlcmoiLCJpYXQiOjE1ODA0MjM4MTIsImV4cCI6MTU4MDU5NjYxMn0.AAUfQ_Ap8r1aPC8nwZYlxL4SKqVCq8Xo2gYZ8OOEYKU"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.2qh21tcevev@email.com",
    "username": "user2-0.2qh21tcevev",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.2qh21tcevev@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuMnFoMjF0Y2V2ZXYiLCJpYXQiOjE1ODA0MjM4MTMsImV4cCI6MTU4MDU5NjYxM30.dV2ixJSmmkfWF-yr9cKujn0YW3SPoxeCXfa7DyWOu_I",
    "username": "user2-0.2qh21tcevev",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.2qh21tcevev@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.2qh21tcevev@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2020-01-30T22:36:53.442Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
