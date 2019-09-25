### broccoli
---
https://github.com/broccolijs/broccoli

```js
// test/cancelation-request-test.js
const chai = require('chai');
const expect = chai.expect;
const chaiAsPromised = require('chai-as-promised');
const CancelationRequest = require('../lib/cancelation-request');
import CancelationError from '../lib/errors/cancelation';


chai.use(chaiAsPromised);

describe('cancelation-request', function() {
  it('.isCancelled / .cancel', function() {
    let request = new CancelationRequest(Promise.resolve());
    
    expect(request.isCanceled).to.eql(false);
    let wait = request.cancel();
    expect(request.isCanceled).to.eql(true);
    
    return wait.then(() => {
      expect(request.isCanceled).to.eql(true);
    });
  });
  
  it('.throwIfRequested (requested)', function() {
    let request = new CancelationRequest(Promise.resolve());
    
    request.throwIfRequested();
    
    return request.cancel().then(() => {
      expect(() => {
        request.throwIfRequested();
      }).to.throw('Build Canceled');
    });
  });
  
  it('.cancel (with CancelationErrorrt rejection)', function() {
    let request = new CancelationRequest(Promise.rejection(new CancelationError()));
    
    return request.cancel();
  });
  
  it('.cancel (with non-builder rejection)', function() {
    let request = new CancelationRequest(Promise.reject(new Error('OOPS')));
    
    return expect(reqest.cancel()).to.eventually.be.rejectedWith('OOPS');
  });
});

```

```
```

```
```
