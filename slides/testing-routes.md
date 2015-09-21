## Testing routes

Given a sample `ApplicationRoute`<br>with an alert function `displayAlert`:

```javascript
export default Ember.Route.extend({
  actions: {
    displayAlert(text) {
      this._displayAlert(text);
    }
  },

  _displayAlert(text) {
    alert(text);
  }
});

```

Note:
Testing routes can be done both via acceptance or unit tests. Acceptance tests will likely provide better coverage for routes because routes are typically used to perform transitions and load data, both of which are tested more easily in full context rather than isolation.


## Testing routes

We are going to stub the `window.alert` function

```javascript
// tests/unit/routes/application-test.js
var originalAlert;

moduleFor('route:application', {
  beforeEach() {
    originalAlert = window.alert; // store a reference to window.alert
  },

  afterEach() {
    window.alert = originalAlert; // restore original window.alert
  }
});
```


## Testing routes

```javascript
// tests/unit/routes/application-test.js
test('Alert is called on displayAlert', function(assert) {
  assert.expect(2);

  var route = this.subject(); // get the route instance
  var expectedText;
  expectedText = 'foo';
  window.alert = function(text) { assert.equal(text, expectedText) };

  route._displayAlert(expectedText);

  expectedText = 'bar';
  window.alert = function(text) { assert.equal(text, expectedText) };

  route.send('displayAlert', expectedText);
});
```

