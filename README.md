Express API Project with Pug Template

- Ensin siirtää 'express' branch (git checkout -b branch 'express')

- Asenta node --> npm init -y

- Asenta express -->  npm install express

- Asenta Pug --> npm install Pug

- Tein media.js ja yhdistänut index.js kanssa:

. import { getMediaItems, postMediaItem, getMediaItemsById, mediaItems} from './media.js';

- src/views/index.pug  näyttää mitä index.pug sisällä, kun kirjoitan index.js kautta 

. app.set('view engine', 'pug');
. app.set('views', './src/views');

- Express toimi kun kirjoitan index.js kautta 

. import express from 'express'
. app.use(express.json())

-public/index.html näyttää: 
. app.use(express.static('public'));

- media/kuva.jpg näyttää 
. app.use('/media', express.static('media'));

-http-request.http

### Hae kaikki mediaesineet

get http://localhost:3000/api/media

### Hae media esitys

get http://localhost:3000/api/media/1

### Lisää media esitys

post http://localhost:3000/api/media
Content-Type: application/json


{
  "filename": "new_image.jpg",
  "filesize": 300000,
  "title": "New Image",
  "description": "Description of the new image",
  "user_id": 1607,
  "media_type": "image/jpeg",
  "created_at": "2023-10-20T15:00:00.000Z"
}



