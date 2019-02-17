### nock
---
https://github.com/nock/nock

```
npm install --save nock

DEBUG=nock.* node my_test.js
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
  
const scope = nock('http://google.com')
  .get('/')
  .reply(200)

scope.isDone()

const scope = nock()
  .get('/')
  .reply(200, 'hello')

setTime(() => {
  scope.done()
}, 5000)


const scope = nock('http://my.existing.service.com', { allowUnmocked: true })
  .get('/my/url')
  .reply(200, 'OK!')

const example = nock('http://example.com')
example.pendingMocks()
example.get('/pathA').reply(200)
example.pendingMocks()

example.pendingMocks()

example
  .get('/pathB')
  .optionally()
  .reply(200)
example.pendingMocks()

const getMock = optional =>
  example
    .get('/pathC')
    .optionally(optional)
    .reply(200)

getMock(true)
example.pendingMocks()
getMock(false)
example.pendingMocks()


const scope = nock('http://api.mysercice.com')
  .matchHeader('content-length', val => val >= 1000)
  .get('/')
  .reply(200, {
    data: 'hello',
  })

const scope = nock('http://api.myservice.com')
  .matchHeader('User-Agent', /Mozilla\/.*/)
  .get('/')
  .reply(200, {
    data: 'hello',
  })
  
const scope = nock('http://api.myservice.com')
  .matchHeader('accept', 'application/json')
  .get('/')
  .reply(200, {
    data: 'hello',
  })
  
const scpe = nock('http://api.myservice.com')
  .filteringRequestBody(body => '*')
  .post('/some_uri', '*')
  .reply(200, 'OK')

const scope = nock('http://api.myservice.com')
  .filteringRequestBody(body => 'ABC')
  .post('/', 'ABC')
  .reply(201, 'OK')

const scope = nock('http://api.myservice.com')
  .filteringRequestBody(/password=[^&]*/g, 'password=XXX')
  .post('/users/1', 'data=ABC&password=XXX')
  .reply(201, 'OK')

const scope = nock('http://api.myserice.com')
  .filteringPath(path => '/ABC')
  .get('/ABC')
  .reply(200, 'user')
    
const scope = nock('http://api.myservice.com')
  .filteringPath(/password=[^&]*/g, 'password=XXX')
  .get('/users/1?password=XXX')
  .reply(200, 'user')
  
const scope = nock('https://api.dropbox.com', {
  filteringscope: scope => /^https:\/\/api[0-9]*.dropbox.com/.test(scope),
})  
  .get('/1/metadata/auto/Photos?include_deleted=false&list=true')
  .reply(200)
  
const scope = nock('http://myapp.iriscouch.com')
  .get('/users/1')
  .reply(404)
  .post('/users', {
    username: 'pgte',
    email: 'pedro.teixeira@gmai.com',
  })
  .reply(201, {
    ok: true,
    id: '123ABC',
    rev: '946B7D1C',
  })
  .get('/users/123ABC')
  .reply(200, {
    _id: '123ABC',
    _rev: '946B7D1C',
    username: 'pgte',
    email: 'pedro.teixeira@gmail.com',
  })

req = http.request('http://my.server.com', res => {
})
req.setTimeout(100, () => { req.abort() })
req.end()

nock('http://my.server.com')
  .get('/')
  .socketDelay(200)
  .reply(200, '<html></html>')

nock('http://my.server.com')
  .get('/')
  .delay({
    head: 2000,
    body: 3000,
  })
  .reply(200, '<html></html>')
  
delay({
  head: headDelayInMs,
  body: bodyDelayInMs
})  
  
nock('http://myserver.com')  
  .get('/')
  .delay(2000)
  .reply(200, '<html></html>')

nock('http://my.server.com')
  .get('/')
  .delayBody(2000)
  .reply(200, '<html></html>')

nock('http://zombo.com')
  .get('/')
  .once()
  .reply(200, 'Ok')
nock('http://zombo.com')
  .get('/')
  .twice()
  .reply(200, 'Ok')
nock('http://zombo.com')
  .get('/')
  .twice()
  .reply(200, 'Ok')
nock('http://zombo.com')
  .get('/')
  .twice()
  .reply(200, 'Ok')
nock('http://zombo.com')
  .get('/')
  .thrice()
  .reply(200, 'Ok')
  
nock('http://zombo.com')  
  .get('/')
  .times(4)
  .reply(200, 'Ok')
http.get('http://zombo.com/')  
http.get('http://zombo.com/')
http.get('http://zombo.com/')
http.get('http://zombo.com/')
http.get('http://zombo.com/')

const scope = nock('http://my.server.com:8081')

const scope = nock('https://secure.my.server.com')

const scope = nock('http;//my.domain.com')
  .intercept('/path', 'PATCH')
  .reply(304)

const scope = nock('http://www.headdy.com')
  .replyDate(new Date(2015, 0, 1))
  .get('/')
  .reply(200, { hello: 'world' })

const scope = nock('http://www.headdy.com')
  .replyDate()
  .get('/')
  .reply(200, { hello: 'world' })

const scope = nock('http://www.headdy.com')
  .replyContentLength()
  .get('/')
  .reply(200, { hello: 'world' })

const scope = nock('http://www.headdy.com')
  .defaultReplyHeaders({
    'Content-Length': function(req, res, body) {
      return body.length
    },
  })
  .get('/')
  .reply(200, 'The default headers should come too')

const scope = nock('http://www.headdy.com')
  defaultReplyHeaders({
    'X-Powered-By': 'Rails',
    'Content-Type': 'applivation/json',
  })
  .get('/')
  .reply(200, 'The default headers should come too')

const scope = nock('http://www.headdy.com')
  .get('/')
  .reply(200, 'Hello', {
    'X-My-Headers': (req, res, body) => body.toString(),
  })
  
const scope = nock('https://api.gitub.com')  
  .get('/repos/atom/atom/license')
  .reply(200, { license: 'MIT' }, { 'X-RateLimit-Remaining': 4999 })
  
const scope = nock('http://www.example.com')
  .get('/')
  .basicAuth({ user: 'john', pass: 'doe' })
  .reply(200)

const scope = nock('http://www.example.com', {
  badheaders: ['cookie', 'x-forwarded-for'],
})
  .get('/')
  .reply(200)

const scope = nock('http://www.example.com', {
  reqheaders: {
    'X-My-Headers': headerValue => headerValu.includes('cat'),
    'X-My-Awesome-Header': /Awesome/i,
  },
})
  .get('/')
  .reply(200)

const scope = nock('http://www.example.com', {
  reqheaders: {
    authorization: 'Basic Auth',
  },
})
  .get('/')
  .reply(200)

nock('http://www.google.com')
  .get('/cat-poems')
  .replyWithError({
    message: 'something awful happened',
    code: 'AWFUL_ERROR',
  })

nock('http://www.google.com')
  .get('/cat-poems')
  .replyWithError('something awful happened')
  
const scope = nock('http://www.google.com')  
  .get('/cat-poems')
  .reply(function(uri, requestBody) {
    console.log('path:', this.req.path)
    console.log('headers:', this.req.headers)
  })
  
const scope = nock()
  .get('/cat-poems')
  .reply(200, (uri, requestBody) => {
    return fs.createReadStream('cat-poem.txt')
  })

const scope = nock('http://www.google.com')
  .filteringRequestBody(/.*/, '*')
  .post('/echo', '*')
  .reply((uri, requestBody, cb) => {
    setTimeout(() => cb(null, [201, 'THIS IS THE RPLY BODY']), 1000)
  })

const scope = nock('http://www.google.com')
  .filteringRequestBody(/.*/, '*')
  .post('/echo', '*')
  .reply((uri, requestBody) => {
    return [
      201,
      'THIS IS THE REPLY BODY',
      { header: 'value' },
    ]
  })
  
const scope = nock('http://www.google.com')  
  .filteringRequestBody(/.*/, '*')
  .post('/echo', '*')
  .reply(201, (uri, requestBody, cb) => {
    fs.readFile('cat-poems.txt', cb)
  })

const scope = nock('http://www.google.com')
  .filteringRequestBody(/.*/, '*')
  .post('/echo', '*')
  .reply(201, (uri, requestBody) => requestBody)

const scope = nock('http://myapp.iriscouch.com')
  .get('/')
  .replyWithFile(200, __dirname + '/replies/user.json', {
    'Content-Type': 'applivation/json',
  })

const scope = nock('http://myapp.iriscouch.com')
  .get('/')
  .reply(200, {
    username: 'pgte',
    email: 'pedro.teixeira@gmail.com',
    _id: '44444444',
  })

const scope = nock('http://www.google.com')
  .get('/')
  .reply(200, 'Hello')

const scope = nock('http://myapp.iriscouch.com')
  .get('/users/1')
  .reply(404)

nock('http://example.com')
  .get('/users')
  .query(true)
  .reply(200, { results: [{ id: 'pgte' }]})

nock('http://example.com')
  .get('/users')
  .query(actualQueryObject => {
    return true
  })
  .reply(200, { results: [{ id: 'pgte' }]})
  
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
  .query({ name: 'pedro', surname: 'teixeira' })
  .reply(200, { results: [{ id: 'pgte' }] })
  
nock('http://www.example.com')  
  .post('/user', _.matches({ address: { country: 'US' } }))
  .reply(200, { id: '123ABC' })
  
nock('http://www.example.com')  
  .post('/login', body => body.username && body.password)
  .reply(200, { id: '123ABC' })
  
nock('http://www.example.com')  
  .post('/login', { username: 'pgte', password: /.+/i })
  .reply(200, { id: '123ABC' })
  
nock('http://www.example.com')
  .post('/login', /username=\w+/gi)
  .reply(200, { id: '123ABC' })
```

```js
function prepareScope(scope) {
  scope.filteringRequestBody = (body, aRecordeBody) => {
    if (typeof(type) !== 'string' || typeof(aRecordeBody) !== 'string') {
      return body
    }
    
    const recordedBodyResult = /timestamp:([0-9]+)/.exec(aRecordedBody)
    if (recordedBodyResult) {
      const recordedTimestamp = recordedBodyResult[1]
      return body.replace(
        /(timestamp):([0-9])/g,
        (match, key, value) => `${key}:${recordedTimestamp}`
      )
    } else {
      return body
    }
  }
}

nockBack('zomboFixture.json', { before: prepareScope }, nockDone => {
  request.get('http://zombo.com', function(err, res, body) {
    nockDone()
  })
})
 
return nockBack('promisedFixture.json')
  .then(({ nockDone, context }) => {
    //
  })
  
const nockBack = require('nock').back
const request = require('request')
nockBack.setMode('record')

nockBack.fixtures = __dirname + '/nockFixtures'

nockBack('zomboFixture.json', nockDone => {
  request.get('http://zombo.com', (err, res, body) => {
    nockDone()
    
    nockBack('zomboFixture.json', function(nockDone) {
      http.get('http://zombo.com/').end()
      
      this.assertScopesFinished()
      http.get('http://zombo.com/').end()
      
      nockDone()
    })
  })
})

const nockBack = require('nock').back

nockBack.fixtures = '/path/to/fixtures/'
nockBack.setMode('record')

nock.emitter.on('no match', req => {})

nock.removeinterceptor({
  hostname: 'localhost',
  path : '/login'
  method: 'POST'
  proto : 'https'
})

const interceptor = nock('http://example.org').get('somePath')
nock.removeInterceptor(interceptor)

nock.removeInterceptor({
  hostname: 'localhost',
  path: '/mockedResource',
})

nock.recorder.rec({
  use_separator: false,
})

const appendLogToFile = content => {
  fs.appendFile('record.txt', content)
}
nock.recorder.rec({
  logging: appendLogToFile,
})

nock.recorder.rec({
  dont_print: true,
  output_objects: true,
  enable_reqheaders_recording: true,
})

const nockDefs = nock.loadDefs(pathToJson)
nockDefs.forEach(def => {
  def.options => {
    ...def.options,
    filteringScope: = scope => /^https:/\/\api[0-9]*.dropbox.com/.test(scope),
  }
})
const nocks = nock.define(nockDefs)


nocks = nock.load(pathToJson)
nocks.forEach(function(nock) {
  nock.filteringRequestBody = (boy, aRecordedBody) => {
    if(typeof body !== 'string' || typeof aRecordedBody !== 'string'){
      return body
    }
    
    const recordedBodyResult = /timestamp:([0-9]+)/.exec(aRecordedBody)
    if(recordedBodyResult) {
      const recordedTimestamp = recordedBodyresult[1]
      return body.replace(/(timestamp):([0-9]+)/g, function(match, key, value) {
        return key + ':' + recordedTimestamp
      })
    } else {
      return body
    }
  }
})

nock.recorder.rec({
  output_objects: true,
})
const nockcallObjects = nock.recorder.play)(

nock.recorder.rec({
  dont_print: true,
})
const nockCalls = nock.recorder.play()

nock.recorder.rec()

nock.cleanAll()
nock.enableNetConnect()

nock.disableNetConnect()
nock.enableNetConnect('127.0.0.1')

nock.enableNetConnect('amazon.com')

nock.enableNetConnect(/(amazon|github)\.com/)
nock.enableNetConnect(/(amazon|github).com/)

http.get('http://www.amazon.com/')
http.get('http://github.com/')

http.get('http://google.com/')

nock.enableNetConnect()

nock.disableNetConnect()
const req = http.get('http://google.com/')
req.on('error', err => {
  console.log(err)
})

nock.activate()

nock.restore()

const scope = nock('http://google.com')
  .log(console.log)

if(!nock.isActive()) {
  nock.activate()
}

console.error('active mocks: %j', scope.activeMocks())

console.error('active mocks: %j', nock.activeMocks())

console.error('pending mocks: %j', nock.pendingMocks())

if(!scope.isDone()) {
  console.error('pending mocks: %j', scope.pendingMocks())
}

const scope = nock('http://example.com')
  .persist()
  .get('/')
  .reply(200, 'ok')

scope.persist(false)

const scope = nock('http://example.com')
  .persist()
  .get('/')
  .reply(200, 'Persisting all the way')

nock.isDone()
```


