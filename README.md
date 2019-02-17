### nock
---
https://github.com/nock/nock

```
npm install --save nock
```

```js
const nock = require('nock')

const scope = nock('https://api.github.com')
  .get('/repos/atom/atom/license')
  .reply(200, {
    license: {
      key: 'mit',
      name: 'MIT License',
      spdx_id: 'MIT',
      url: 'https://api.github.com/licenses/mit',
      node_id: '',
    },
  })
  
const scope = nock('http://www.example.com')
  .get('/resource')
  .reply(200, 'domain matched')
  
const scope = nock(/example\.com/)
  .get('/resource')
  .reply(200, 'domain regex matched')

const scope = nock('http://www.example.com')
  .get('/resource')
  .reply(200, 'path matched')

const scope = nock('http://www.example.com')
  .get(/source$/)
  .reply(200, 'path using regex matched')

const scope = nock('http://www.example.com')
  .get(uri => uri.includes('cats'))
  .reply(200, 'path using function matched')

nock('http://www.example.com')
  .post('/login', 'username=pgte&password=123456')
  .reply(200, { id: '123ABC' })

nock('http://www.example.com')
  .post('/login', Buffer.from([0xff, 0x11]))
  .reply(200, { id: '123ABC' })

nock('http://www.example.com')
  .post('/login', /username=\w+/gi)
  .reply(200, { id: '123ABC' })

nock('http://www.example.com')
  .post('/login', { username: 'pgte', password: //+/i })
  .reply(200, { id: '123ABC' })
  
nock('http://www.example.com')
  .post('/login', body => body.username && body.password)
  .reply(200, { id: '123ABC' })
  
nock('http://www.example.com')
  .post('/user', _.matches({ address: { country: 'US' } }))
  .reply(200, { id: '123ABC' })
  
nock('http://example.com')
  .get('/users')
  .query({ name: 'pedro', surname: 'teixeira' })
  .reply(200, { results: [{ id: 'pgte' }] })

nock('http://example.com')
  .get('/users')
  .query({
    names: ['alice', 'bob'],
    tags: {
      alice: ['admin', 'tester'],
      bob: ['tester'],
    },
  })
  .reply(200, { results: [{ id: 'pgte' }] })
  
nock('http://example.com')
  .get('/users')
  .query(actualQueryObject => {
    return true
  })
  .reply(200, { results: [{ id: 'pgte' }] })
  
nock('http://example.com')
  .get('/users')
  .query(true)
  .reply(200, { results: [{ id: 'pgte' }] })

const scope = nock()
  .get()
  .reply
  































```

```
```


