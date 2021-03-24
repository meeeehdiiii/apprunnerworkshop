---
title: "Deploying an application using a Dockerfile"
chapter: true
weight: 25
pre: '<i class="fa fa-film" aria-hidden="true"></i> '
---

## Deploying to AWS App Runner with Docker

*Pre-requisites:*

This section of the workshop assumes you have docker installed. Follow the instructions at https://docs.docker.com/get-docker/

Create a new directory “apprunner-example”, and in this directly, create the following files:

index.js

```
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
    res.send('Hello World!')
})

app.listen(port, () => {
    console.log(`Example app listening at http://localhost:${port}`)
})
```

package.json
```
{
  "name": "fusion_example",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {},
  "author": "",
  "license": "ISC"
}
```

Dockerfile
```
FROM node:14

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./

RUN npm install

# Bundle app source
COPY . .

EXPOSE 3000
CMD [ "node", "index.js" ]
```

This means you should have the following files in your directory:

```
iamtim@mypc:~/apprunner-example$ ls
Dockerfile  index.js  package.json
```