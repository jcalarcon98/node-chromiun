# NODE-CHROMIUN

**NODE-CHROMIUN** image is based on [markadams/chromium-xvfb](https://hub.docker.com/r/markadams/chromium-xvfb) image and provides a way to execute karma tests on Browser like Chromiun or Chrome inside a Docker container. This image also contains Node:12.16.3. 

## Installation

Download [node-chromiun](https://hub.docker.com/r/jcalarcon/node-chromiun) image from Dockerhub or directly:

```bash
docker pull jcalarcon/node-chromiun
```

## Usage

This example provides a way to execute Angular tests with karma:

**Dockerfile for tests Angular application**

``` Dockerfile
FROM jcalarcon/node-chromiun
WORKDIR /app
COPY ./package.json ./
RUN npm install
COPY . .
CMD ["npm","run","test:prod"]
```

**Karma configuration** (karma.conf.js)

Add this configuration to your karma.conf.js file:

```js
browsers: ['ChromiunHeadless'],
customLaunchers: {
  ChromiunHeadless: {
    base: 'Chrome',
    flags: [
      '--headless',
      '--disable-gpu',
      '--remote-debugging-port=9222'
    ],
    debug: true,
  }
},
```

**File package.json**

```json
"scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "test:prod": "npm test -- --watch=false",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.


## License
[MIT](https://choosealicense.com/licenses/mit/)