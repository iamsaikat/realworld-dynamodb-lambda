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
    "email": "author-2r70bl@email.com",
    "username": "author-2r70bl",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-2r70bl@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci0ycjcwYmwiLCJpYXQiOjE1ODU2MDk4MjMsImV4cCI6MTU4NTc4MjYyM30.k2kV1fMwA4s6NpvWDRrrtYUvzv8j-kYXyE-6KUG1aB0",
    "username": "author-2r70bl",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-uq2f28@email.com",
    "username": "authoress-uq2f28",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-uq2f28@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy11cTJmMjgiLCJpYXQiOjE1ODU2MDk4MjMsImV4cCI6MTU4NTc4MjYyM30.jJfOf6RS6NMA6zCU81udbdbCx_ujuBX_FpeW6qcsqwI",
    "username": "authoress-uq2f28",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-u4zbde@email.com",
    "username": "non-author-u4zbde",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-u4zbde@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItdTR6YmRlIiwiaWF0IjoxNTg1NjA5ODIzLCJleHAiOjE1ODU3ODI2MjN9.YSySzyRe44h0UIDNOoIB0aTnahgGbSr4ccCjOxFL4lU",
    "username": "non-author-u4zbde",
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
    "slug": "title-9ysfnt",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609823619,
    "updatedAt": 1585609823619,
    "author": {
      "username": "author-2r70bl",
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
    "slug": "title-6yoy9k",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609823661,
    "updatedAt": 1585609823661,
    "author": {
      "username": "author-2r70bl",
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
GET /articles/title-9ysfnt
```
```
200 OK

{
  "article": {
    "createdAt": 1585609823619,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-9ysfnt",
    "updatedAt": 1585609823619,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-6yoy9k
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1585609823661,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-6yoy9k",
    "updatedAt": 1585609823661,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/ylernv
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [ylernv]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-6yoy9k

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
    "createdAt": 1585609823661,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-6yoy9k",
    "updatedAt": 1585609823661,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-6yoy9k

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
    "createdAt": 1585609823661,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-6yoy9k",
    "updatedAt": 1585609823661,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-6yoy9k

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
    "createdAt": 1585609823661,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-6yoy9k",
    "updatedAt": 1585609823661,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-6yoy9k

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
PUT /articles/title-6yoy9k

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
PUT /articles/title-6yoy9k

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
PUT /articles/foo-title-6yoy9k

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
      "Article not found: [foo-title-6yoy9k]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-6yoy9k

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
      "Article can only be updated by author: [author-2r70bl]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-9ysfnt/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1585609823619,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-9ysfnt",
    "updatedAt": 1585609823619,
    "favoritedBy": [
      "non-author-u4zbde"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-9ysfnt
```
```
200 OK

{
  "article": {
    "createdAt": 1585609823619,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-9ysfnt",
    "updatedAt": 1585609823619,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-9ysfnt/favorite

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
POST /articles/title-9ysfnt_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-9ysfnt_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-9ysfnt/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1585609823619,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-9ysfnt",
    "updatedAt": 1585609823619,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-9ysfnt
```
```
200 OK

{}
```
```
GET /articles/title-9ysfnt
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-9ysfnt]"
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
DELETE /articles/title-6yoy9k
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-2r70bl]"
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
      "dz2sny",
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
    "slug": "title-6bvtip",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609824792,
    "updatedAt": 1585609824792,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dz2sny",
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
      "dlg02r",
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
    "slug": "title-af2xmc",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609824834,
    "updatedAt": 1585609824834,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dlg02r",
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
      "dr1fhn",
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
    "slug": "title-x2g8vd",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609824859,
    "updatedAt": 1585609824859,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dr1fhn",
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
      "kt0qdm",
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
    "slug": "title-q60p0q",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609824886,
    "updatedAt": 1585609824886,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "kt0qdm",
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
      "hj17b6",
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
    "slug": "title-f5286h",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609824911,
    "updatedAt": 1585609824911,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "hj17b6",
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
      "1rraz4",
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
    "slug": "title-6a3uv9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609824939,
    "updatedAt": 1585609824939,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "1rraz4",
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
      "3kfrf8",
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
    "slug": "title-quvjqg",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609824967,
    "updatedAt": 1585609824967,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "3kfrf8",
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
      "i8027n",
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
    "slug": "title-3soeju",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609824993,
    "updatedAt": 1585609824993,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "i8027n",
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
      "t9k02h",
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
    "slug": "title-b4i65g",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825021,
    "updatedAt": 1585609825021,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "t9k02h",
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
      "oqnpwe",
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
    "slug": "title-uq3ubd",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825048,
    "updatedAt": 1585609825048,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "oqnpwe",
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
      "wq3cdb",
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
    "slug": "title-cx9fiy",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825079,
    "updatedAt": 1585609825079,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wq3cdb",
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
      "8fpz20",
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
    "slug": "title-j0mu5",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825112,
    "updatedAt": 1585609825112,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8fpz20",
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
      "j2zknm",
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
    "slug": "title-s1tldr",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825140,
    "updatedAt": 1585609825140,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "j2zknm",
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
      "376dag",
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
    "slug": "title-dswkih",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825164,
    "updatedAt": 1585609825164,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "376dag",
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
      "v0g0ee",
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
    "slug": "title-6dx3yl",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825188,
    "updatedAt": 1585609825188,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "v0g0ee",
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
      "8qy4rc",
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
    "slug": "title-935fe",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825219,
    "updatedAt": 1585609825219,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8qy4rc",
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
      "sw1r3t",
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
    "slug": "title-fweqf4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825246,
    "updatedAt": 1585609825246,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "sw1r3t",
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
      "yf21yy",
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
    "slug": "title-63l5w",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825280,
    "updatedAt": 1585609825280,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "yf21yy",
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
      "n8uek8",
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
    "slug": "title-8fekdt",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825325,
    "updatedAt": 1585609825325,
    "author": {
      "username": "authoress-uq2f28",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "n8uek8",
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
      "tzqk6q",
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
    "slug": "title-kgdtmz",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609825387,
    "updatedAt": 1585609825387,
    "author": {
      "username": "author-2r70bl",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tzqk6q",
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
        "tzqk6q"
      ],
      "createdAt": 1585609825387,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kgdtmz",
      "updatedAt": 1585609825387,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n8uek8",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825325,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8fekdt",
      "updatedAt": 1585609825325,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "yf21yy"
      ],
      "createdAt": 1585609825280,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-63l5w",
      "updatedAt": 1585609825280,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "sw1r3t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609825246,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fweqf4",
      "updatedAt": 1585609825246,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8qy4rc",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825219,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-935fe",
      "updatedAt": 1585609825219,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "v0g0ee"
      ],
      "createdAt": 1585609825188,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6dx3yl",
      "updatedAt": 1585609825188,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "376dag",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609825164,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dswkih",
      "updatedAt": 1585609825164,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j2zknm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825140,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s1tldr",
      "updatedAt": 1585609825140,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8fpz20",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825112,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j0mu5",
      "updatedAt": 1585609825112,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wq3cdb"
      ],
      "createdAt": 1585609825079,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cx9fiy",
      "updatedAt": 1585609825079,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oqnpwe",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825048,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uq3ubd",
      "updatedAt": 1585609825048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t9k02h",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825021,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b4i65g",
      "updatedAt": 1585609825021,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i8027n",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824993,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3soeju",
      "updatedAt": 1585609824993,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3kfrf8",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824967,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-quvjqg",
      "updatedAt": 1585609824967,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1rraz4",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824939,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6a3uv9",
      "updatedAt": 1585609824939,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hj17b6",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824911,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f5286h",
      "updatedAt": 1585609824911,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kt0qdm",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824886,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q60p0q",
      "updatedAt": 1585609824886,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dr1fhn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824859,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x2g8vd",
      "updatedAt": 1585609824859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dlg02r",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824834,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-af2xmc",
      "updatedAt": 1585609824834,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz2sny",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824792,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6bvtip",
      "updatedAt": 1585609824792,
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
        "i8027n",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824993,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3soeju",
      "updatedAt": 1585609824993,
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
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "yf21yy"
      ],
      "createdAt": 1585609825280,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-63l5w",
      "updatedAt": 1585609825280,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "v0g0ee"
      ],
      "createdAt": 1585609825188,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6dx3yl",
      "updatedAt": 1585609825188,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8fpz20",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825112,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j0mu5",
      "updatedAt": 1585609825112,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t9k02h",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825021,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b4i65g",
      "updatedAt": 1585609825021,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1rraz4",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824939,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6a3uv9",
      "updatedAt": 1585609824939,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dr1fhn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824859,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x2g8vd",
      "updatedAt": 1585609824859,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-uq2f28
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "n8uek8",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825325,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8fekdt",
      "updatedAt": 1585609825325,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "sw1r3t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609825246,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fweqf4",
      "updatedAt": 1585609825246,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "v0g0ee"
      ],
      "createdAt": 1585609825188,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6dx3yl",
      "updatedAt": 1585609825188,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j2zknm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825140,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s1tldr",
      "updatedAt": 1585609825140,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wq3cdb"
      ],
      "createdAt": 1585609825079,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cx9fiy",
      "updatedAt": 1585609825079,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t9k02h",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825021,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b4i65g",
      "updatedAt": 1585609825021,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3kfrf8",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824967,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-quvjqg",
      "updatedAt": 1585609824967,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hj17b6",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824911,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f5286h",
      "updatedAt": 1585609824911,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dr1fhn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824859,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x2g8vd",
      "updatedAt": 1585609824859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz2sny",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824792,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6bvtip",
      "updatedAt": 1585609824792,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-u4zbde
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-2r70bl&limit=2
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
        "tzqk6q"
      ],
      "createdAt": 1585609825387,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kgdtmz",
      "updatedAt": 1585609825387,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "yf21yy"
      ],
      "createdAt": 1585609825280,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-63l5w",
      "updatedAt": 1585609825280,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-2r70bl&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8qy4rc",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825219,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-935fe",
      "updatedAt": 1585609825219,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "376dag",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609825164,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dswkih",
      "updatedAt": 1585609825164,
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
        "tzqk6q"
      ],
      "createdAt": 1585609825387,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kgdtmz",
      "updatedAt": 1585609825387,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n8uek8",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825325,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8fekdt",
      "updatedAt": 1585609825325,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "yf21yy"
      ],
      "createdAt": 1585609825280,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-63l5w",
      "updatedAt": 1585609825280,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "sw1r3t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609825246,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fweqf4",
      "updatedAt": 1585609825246,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8qy4rc",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825219,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-935fe",
      "updatedAt": 1585609825219,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "v0g0ee"
      ],
      "createdAt": 1585609825188,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6dx3yl",
      "updatedAt": 1585609825188,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "376dag",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609825164,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dswkih",
      "updatedAt": 1585609825164,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j2zknm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825140,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s1tldr",
      "updatedAt": 1585609825140,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8fpz20",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825112,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j0mu5",
      "updatedAt": 1585609825112,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wq3cdb"
      ],
      "createdAt": 1585609825079,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cx9fiy",
      "updatedAt": 1585609825079,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oqnpwe",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825048,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uq3ubd",
      "updatedAt": 1585609825048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t9k02h",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825021,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b4i65g",
      "updatedAt": 1585609825021,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i8027n",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824993,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3soeju",
      "updatedAt": 1585609824993,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3kfrf8",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824967,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-quvjqg",
      "updatedAt": 1585609824967,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1rraz4",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824939,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6a3uv9",
      "updatedAt": 1585609824939,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hj17b6",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824911,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f5286h",
      "updatedAt": 1585609824911,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kt0qdm",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824886,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q60p0q",
      "updatedAt": 1585609824886,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dr1fhn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824859,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x2g8vd",
      "updatedAt": 1585609824859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dlg02r",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824834,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-af2xmc",
      "updatedAt": 1585609824834,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz2sny",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824792,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6bvtip",
      "updatedAt": 1585609824792,
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
POST /profiles/authoress-uq2f28/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-uq2f28",
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
        "n8uek8",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825325,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8fekdt",
      "updatedAt": 1585609825325,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "sw1r3t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609825246,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fweqf4",
      "updatedAt": 1585609825246,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "v0g0ee"
      ],
      "createdAt": 1585609825188,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6dx3yl",
      "updatedAt": 1585609825188,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j2zknm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825140,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s1tldr",
      "updatedAt": 1585609825140,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wq3cdb"
      ],
      "createdAt": 1585609825079,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cx9fiy",
      "updatedAt": 1585609825079,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t9k02h",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825021,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b4i65g",
      "updatedAt": 1585609825021,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3kfrf8",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824967,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-quvjqg",
      "updatedAt": 1585609824967,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hj17b6",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824911,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f5286h",
      "updatedAt": 1585609824911,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dr1fhn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824859,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x2g8vd",
      "updatedAt": 1585609824859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz2sny",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824792,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6bvtip",
      "updatedAt": 1585609824792,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-2r70bl/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-2r70bl",
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
        "tzqk6q"
      ],
      "createdAt": 1585609825387,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kgdtmz",
      "updatedAt": 1585609825387,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n8uek8",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825325,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8fekdt",
      "updatedAt": 1585609825325,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "yf21yy"
      ],
      "createdAt": 1585609825280,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-63l5w",
      "updatedAt": 1585609825280,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "sw1r3t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609825246,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fweqf4",
      "updatedAt": 1585609825246,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8qy4rc",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825219,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-935fe",
      "updatedAt": 1585609825219,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "v0g0ee"
      ],
      "createdAt": 1585609825188,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6dx3yl",
      "updatedAt": 1585609825188,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "376dag",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609825164,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dswkih",
      "updatedAt": 1585609825164,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j2zknm",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825140,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s1tldr",
      "updatedAt": 1585609825140,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8fpz20",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825112,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-j0mu5",
      "updatedAt": 1585609825112,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wq3cdb"
      ],
      "createdAt": 1585609825079,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-cx9fiy",
      "updatedAt": 1585609825079,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "oqnpwe",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609825048,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uq3ubd",
      "updatedAt": 1585609825048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t9k02h",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609825021,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b4i65g",
      "updatedAt": 1585609825021,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i8027n",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824993,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3soeju",
      "updatedAt": 1585609824993,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3kfrf8",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824967,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-quvjqg",
      "updatedAt": 1585609824967,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1rraz4",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824939,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6a3uv9",
      "updatedAt": 1585609824939,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hj17b6",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824911,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-f5286h",
      "updatedAt": 1585609824911,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kt0qdm",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824886,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q60p0q",
      "updatedAt": 1585609824886,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dr1fhn",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585609824859,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-x2g8vd",
      "updatedAt": 1585609824859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dlg02r",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585609824834,
      "author": {
        "username": "author-2r70bl",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-af2xmc",
      "updatedAt": 1585609824834,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz2sny",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585609824792,
      "author": {
        "username": "authoress-uq2f28",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-6bvtip",
      "updatedAt": 1585609824792,
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
    "j2zknm",
    "tag_12",
    "tag_mod_2_0",
    "tag_mod_3_0",
    "n8uek8",
    "tag_18",
    "dz2sny",
    "tag_0",
    "tag_14",
    "tag_mod_3_2",
    "v0g0ee",
    "3kfrf8",
    "tag_6",
    "8qy4rc",
    "tag_15",
    "tag_mod_2_1",
    "i8027n",
    "tag_7",
    "tag_mod_3_1",
    "tag_10",
    "wq3cdb",
    "tag_a",
    "tag_b",
    "376dag",
    "tag_13",
    "tag_17",
    "yf21yy",
    "sw1r3t",
    "tag_16",
    "t9k02h",
    "tag_8",
    "kt0qdm",
    "tag_3",
    "dr1fhn",
    "tag_2",
    "1rraz4",
    "tag_5",
    "hj17b6",
    "tag_4",
    "oqnpwe",
    "tag_9",
    "8fpz20",
    "tag_11",
    "dlg02r",
    "tag_1",
    "tag_19",
    "tzqk6q"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-3zhqty@email.com",
    "username": "author-3zhqty",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-3zhqty@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci0zemhxdHkiLCJpYXQiOjE1ODU2MDk4MjYsImV4cCI6MTU4NTc4MjYyNn0.TGdU3b8mmdOAQVCk1toO-ZwqSGKE5gWLIfyE01Iu8eU",
    "username": "author-3zhqty",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-jy8obr@email.com",
    "username": "commenter-jy8obr",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-jy8obr@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1qeThvYnIiLCJpYXQiOjE1ODU2MDk4MjYsImV4cCI6MTU4NTc4MjYyNn0.mSPHvIlwf0qiwW4wDvCMt44XR5W-wDRuFxVjBeLiMdg",
    "username": "commenter-jy8obr",
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
    "slug": "title-vpf1zf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585609826951,
    "updatedAt": 1585609826951,
    "author": {
      "username": "author-3zhqty",
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
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment gnaa69"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "c59c365f-aa3c-41dc-b1fe-414418af05c3",
    "slug": "title-vpf1zf",
    "body": "test comment gnaa69",
    "createdAt": 1585609827001,
    "updatedAt": 1585609827001,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment q3us9i"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "bf000b22-2be2-4cfe-870b-d0d0b20c6608",
    "slug": "title-vpf1zf",
    "body": "test comment q3us9i",
    "createdAt": 1585609827058,
    "updatedAt": 1585609827058,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment xlt78o"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e429a54f-c2b8-4467-9774-48e18527af19",
    "slug": "title-vpf1zf",
    "body": "test comment xlt78o",
    "createdAt": 1585609827098,
    "updatedAt": 1585609827098,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment 2zgnbz"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "b716a5ec-f450-4fb3-bfd1-e6478315376b",
    "slug": "title-vpf1zf",
    "body": "test comment 2zgnbz",
    "createdAt": 1585609827128,
    "updatedAt": 1585609827128,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment s7t8hc"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "565153eb-e27d-40d3-861e-287fdf060526",
    "slug": "title-vpf1zf",
    "body": "test comment s7t8hc",
    "createdAt": 1585609827154,
    "updatedAt": 1585609827154,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment jm80z1"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "c2bd77b9-dbfc-4014-a88d-fa58c6dbcdf6",
    "slug": "title-vpf1zf",
    "body": "test comment jm80z1",
    "createdAt": 1585609827183,
    "updatedAt": 1585609827183,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment 3wj2hh"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "3a2bfce4-fdb8-45a1-a8b7-923dc8d23a42",
    "slug": "title-vpf1zf",
    "body": "test comment 3wj2hh",
    "createdAt": 1585609827209,
    "updatedAt": 1585609827209,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment ukyyz8"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "6a8c3662-693c-4185-9652-d90714026685",
    "slug": "title-vpf1zf",
    "body": "test comment ukyyz8",
    "createdAt": 1585609827241,
    "updatedAt": 1585609827241,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment v4jykk"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "6ef97786-e905-418e-b065-05787bb26d08",
    "slug": "title-vpf1zf",
    "body": "test comment v4jykk",
    "createdAt": 1585609827279,
    "updatedAt": 1585609827279,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-vpf1zf/comments

{
  "comment": {
    "body": "test comment jwnj9d"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "fc4ed340-bbe0-45c9-9d11-35970330f9c6",
    "slug": "title-vpf1zf",
    "body": "test comment jwnj9d",
    "createdAt": 1585609827306,
    "updatedAt": 1585609827306,
    "author": {
      "username": "commenter-jy8obr",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-vpf1zf/comments

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
POST /articles/title-vpf1zf/comments

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
    "body": "test comment rczcw2"
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
GET /articles/title-vpf1zf/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1585609827241,
      "id": "6a8c3662-693c-4185-9652-d90714026685",
      "body": "test comment ukyyz8",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827241
    },
    {
      "createdAt": 1585609827001,
      "id": "c59c365f-aa3c-41dc-b1fe-414418af05c3",
      "body": "test comment gnaa69",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827001
    },
    {
      "createdAt": 1585609827183,
      "id": "c2bd77b9-dbfc-4014-a88d-fa58c6dbcdf6",
      "body": "test comment jm80z1",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827183
    },
    {
      "createdAt": 1585609827128,
      "id": "b716a5ec-f450-4fb3-bfd1-e6478315376b",
      "body": "test comment 2zgnbz",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827128
    },
    {
      "createdAt": 1585609827306,
      "id": "fc4ed340-bbe0-45c9-9d11-35970330f9c6",
      "body": "test comment jwnj9d",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827306
    },
    {
      "createdAt": 1585609827154,
      "id": "565153eb-e27d-40d3-861e-287fdf060526",
      "body": "test comment s7t8hc",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827154
    },
    {
      "createdAt": 1585609827098,
      "id": "e429a54f-c2b8-4467-9774-48e18527af19",
      "body": "test comment xlt78o",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827098
    },
    {
      "createdAt": 1585609827209,
      "id": "3a2bfce4-fdb8-45a1-a8b7-923dc8d23a42",
      "body": "test comment 3wj2hh",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827209
    },
    {
      "createdAt": 1585609827058,
      "id": "bf000b22-2be2-4cfe-870b-d0d0b20c6608",
      "body": "test comment q3us9i",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827058
    },
    {
      "createdAt": 1585609827279,
      "id": "6ef97786-e905-418e-b065-05787bb26d08",
      "body": "test comment v4jykk",
      "slug": "title-vpf1zf",
      "author": {
        "username": "commenter-jy8obr",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585609827279
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-vpf1zf/comments/c59c365f-aa3c-41dc-b1fe-414418af05c3
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-vpf1zf/comments/bf000b22-2be2-4cfe-870b-d0d0b20c6608
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-jy8obr]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-vpf1zf/comments/bf000b22-2be2-4cfe-870b-d0d0b20c6608
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
DELETE /articles/title-vpf1zf/comments/foobar_id
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
    "email": "user1-0.qx5pw5067p@email.com",
    "username": "user1-0.qx5pw5067p",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.qx5pw5067p@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucXg1cHc1MDY3cCIsImlhdCI6MTU4NTYwOTgyNywiZXhwIjoxNTg1NzgyNjI3fQ.lkytNpPriECRL1GYkurVUrmYYEdY8jZdgQHBTxhkWMw",
    "username": "user1-0.qx5pw5067p",
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
    "email": "user1-0.qx5pw5067p@email.com",
    "username": "user1-0.qx5pw5067p",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.qx5pw5067p]"
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
    "email": "user1-0.qx5pw5067p@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.qx5pw5067p@email.com]"
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
    "email": "user1-0.qx5pw5067p@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.qx5pw5067p@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucXg1cHc1MDY3cCIsImlhdCI6MTU4NTYwOTgyNywiZXhwIjoxNTg1NzgyNjI3fQ.lkytNpPriECRL1GYkurVUrmYYEdY8jZdgQHBTxhkWMw",
    "username": "user1-0.qx5pw5067p",
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
    "email": "0.rkqp86mafd",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.rkqp86mafd]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.qx5pw5067p@email.com",
    "password": "0.vqu63kvuk4d"
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
    "email": "user1-0.qx5pw5067p@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucXg1cHc1MDY3cCIsImlhdCI6MTU4NTYwOTgyNywiZXhwIjoxNTg1NzgyNjI3fQ.lkytNpPriECRL1GYkurVUrmYYEdY8jZdgQHBTxhkWMw",
    "username": "user1-0.qx5pw5067p",
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
GET /profiles/user1-0.qx5pw5067p
```
```
200 OK

{
  "profile": {
    "username": "user1-0.qx5pw5067p",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.wqaeaqsbpw
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.wqaeaqsbpw]"
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
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1ODU2MDk4MjcsImV4cCI6MTU4NTc4MjYyN30.rEWfp_KlzY1NOvYfaa0QWNbm_0YzHLEmRmgESidl9uU",
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
    "username": "user2-0.ayy0yhnl3v",
    "email": "user2-0.ayy0yhnl3v@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.ayy0yhnl3v@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuYXl5MHlobmwzdiIsImlhdCI6MTU4NTYwOTgyOCwiZXhwIjoxNTg1NzgyNjI4fQ.BfL1bzTZ6rJtdeU4PkDfdz8DRWQfHT5UZEjfZrc4QDk",
    "username": "user2-0.ayy0yhnl3v",
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
    "email": "updated-user1-0.qx5pw5067p@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.qx5pw5067p",
    "email": "updated-user1-0.qx5pw5067p@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucXg1cHc1MDY3cCIsImlhdCI6MTU4NTYwOTgyNywiZXhwIjoxNTg1NzgyNjI3fQ.lkytNpPriECRL1GYkurVUrmYYEdY8jZdgQHBTxhkWMw"
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
    "username": "user1-0.qx5pw5067p",
    "email": "updated-user1-0.qx5pw5067p@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucXg1cHc1MDY3cCIsImlhdCI6MTU4NTYwOTgyNywiZXhwIjoxNTg1NzgyNjI3fQ.lkytNpPriECRL1GYkurVUrmYYEdY8jZdgQHBTxhkWMw"
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
    "username": "user1-0.qx5pw5067p",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucXg1cHc1MDY3cCIsImlhdCI6MTU4NTYwOTgyNywiZXhwIjoxNTg1NzgyNjI3fQ.lkytNpPriECRL1GYkurVUrmYYEdY8jZdgQHBTxhkWMw"
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
    "username": "user1-0.qx5pw5067p",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAucXg1cHc1MDY3cCIsImlhdCI6MTU4NTYwOTgyNywiZXhwIjoxNTg1NzgyNjI3fQ.lkytNpPriECRL1GYkurVUrmYYEdY8jZdgQHBTxhkWMw"
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
    "email": "user2-0.ku73tocrjim@email.com",
    "username": "user2-0.ku73tocrjim",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.ku73tocrjim@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAua3U3M3RvY3JqaW0iLCJpYXQiOjE1ODU2MDk4MjgsImV4cCI6MTU4NTc4MjYyOH0.1haHRdHxJrJMrTQuwH71TyE3RclyLq_4eqdeQhMOJzA",
    "username": "user2-0.ku73tocrjim",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.ku73tocrjim@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.ku73tocrjim@email.com]"
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
  "pong": "2020-03-30T23:10:28.431Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
