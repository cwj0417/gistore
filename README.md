# gistore

> sync data for file-based db using gist

## preparation

`gistore` was based on [gist](gist.github.com), a github personal-access-token was **required**. and a token has only access to gist was desirable.

## installing

set gistore as dependencies:

```shell
npm i -S gistore
```

import gistore:

```js
import gistore from 'gistore'
```

## usage

basic usage:
```js
gistore.setToken('your github token')
gistore.setId('your gist id')

gistore.backUp({data: 'your app data'})
    .then(res => console.log('backup succeed'))

gistore.sync()
    .then(res => {app.data = res})
```

first time:

*you have not created an gist for the first time, you should*:

```js
gistore.createBackUp('my-app-name.db', {backup1: 'data', backup2: 'data'})
    .then(id => console.log(`my backup id was: ${id}`))
```
after fetch your gist id, you should put the id in your local storage in your code.

## docs

**variables**

### `.$http`

an axios instance with defaults of base-url of gist api and headers of token.

### `.token`

boolean, whether current gistore instance have the gist token.

### `.gistId`

your backup gist id. if not exist, this value was set to `false`.

**methods**

### `.setId(string)`

set your gist id

### `.setToken(string)`

set your github token

### `.getList()`

returns a promise, resolved with gist list, rejected if token not set.

### `.getGist(id)`

fetch gist through id. rejected if token or gist id was absent.

### `.createGist(description, files)`

files was a key-value Object.

returns a promise, resolved with created gist.

### `.editGist(id, files)`

edit gist. rejected if token or gist id was absent.

### `.backUp(files)`

upload files to gist. rejected if token or gist id was absent.

### `.sync()`

get files from gist. rejected if token or gist id was absent.

### `.createBackUp(description, files)`

create a new gist, returns a promise resolving with gist id.