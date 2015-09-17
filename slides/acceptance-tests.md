## Acceptance tests

Acceptance tests are used to test<br>user interaction and application flow.

They emulate user interaction and confirm expected results.

---

Some acceptance tests you might write are:

- A user is able to log in via the login form.
- A user is able to create a blog post.
- A visitor does not have access to the admin panel.


### Sample acceptance test

ember-cli comes with acceptance test support out of the box. For creating your first test, you just need to run:

ember generate acceptance-test &lt;name&gt;

```
$ ember generate acceptance-test user-can-login-via-form
version: 1.13.8
installing acceptance-test
  create tests/acceptance/user-can-login-via-form-test.js

```


### Give me the code!

tests/acceptance/user-can-login-via-form-test.js

```javascript
import Ember from 'ember';
import { module, test } from 'qunit';
import startApp from 'testing-ember/tests/helpers/start-app';

module('Acceptance | user can login via form', {
  beforeEach: function() {
    this.application = startApp();
  },

  afterEach: function() {
    Ember.run(this.application, 'destroy');
  }
});
```

```javascript
test('visiting /user-can-login-via-form', function(assert) {
  visit('/user-can-login-via-form');

  andThen(function() {
    assert.equal(currentURL(), '/user-can-login-via-form');
  });
});
```

Note:
This will only display in the notes window.
