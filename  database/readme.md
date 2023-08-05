
### PostgresSQL
* анкеты людей (имя, описание, фото, город);
* посты (описание, медиа, хэштеги,комментарии);

<img src="./pg.png">

```
// Use DBML to define your database structure
// Docs: https://dbml.dbdiagram.io/docs



Table users {
  id integer [primary key]
  username varchar
  password varchar
  file_id integer
  city_id integer
  bio text
}


Table posts {
  id integer [primary key]
  title varchar
  body text
  user_id integer
  is_active bool
}


Table comments {
  id integer [primary key]
  body text
  user_id integer
  post_id integer
  is_active bool
}

Table tags {
  id integer [primary key]
  tag varchar
}

Table files {
  id integer [primary key]
  name varchar
  size varchar
  token varchar
}

Table cities {
  id integer [primary key]
  name varchar
  code varchar
}

Table post_tag{
  post_id integer
  tag_id integer
}

Table post_file{
  post_id integer
  file_id integer
}

Ref: users.file_id > files.id
Ref: users.city_id > cities.id

Ref: posts.user_id  > users.id 
Ref: comments.user_id > users.id 
Ref: comments.post_id > users.id

Ref: post_tag.post_id > posts.id
Ref: post_tag.tag_id > tags.id

Ref: post_file.post_id > posts.id
Ref: post_file.file_id > files.id

```

### Minio
(фото, аудио, видео)
```json
{
   "buckets": [
      "posts",
      "users"
    ]
}
```


### MongoDB
Лайки и просмотры постов

```json
{
  "posts": 
  [
    {
      "post_id": 0,
      "likes": {
        "user_id": [
          1,
          3,
          6
        ]
      },
      "view": 0
    }
  ]
}
```
Личные сообщения и чаты (только текст и прочитанность сообщений)

```json

{
  "unread_messages": [
    {"_id": 123},
    {"_id": 345}
  ]
}

```
```json

{
  "messages": [
     {
       "_id": 123,
       "text": "hello",
       "discussion_id": 345
     }
   ]
}
```

```json
{
  "discussions": [
    {
        "_id": 345,
        "type": "dialog",
        "user_id": 1,
        "name": ""
    }
  ]
}
```

### Neo4j
* интересы
* друзья
* подписчики
* любовные отношения


```
[user1] - friends -> [user2]

[user1] - followers -> [user2]

[user1] - loves -> [user2]

[user1] - interests -> [user2]
```

