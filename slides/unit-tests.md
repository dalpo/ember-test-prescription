## Unit tests

Unit tests are generally used to test a small piece of code and ensure that it is doing what was intended.

Testing an `Ember.Object` is as simple as creating an instance of the object, setting its state, and running assertions against the object.


### TESTING OBJECT METHODS

```javascript
// app/models/some-thing.js
export default Ember.Object.extend({
  foo: 'bar',
  testMethod() {
    this.set('foo', 'baz');
  }
});
```

```javascript
// tests/unit/models/some-thing-test.js
import { moduleForModel, test } from 'ember-qunit';

moduleForModel('some-thing', 'Unit | Model | some thing', {
  // Specify the other units that are required for this test.
  needs: []
});

test('calling testMethod updated foo', function(assert) {
  var someThing = this.subject().create({});

  someThing.testMethod();

  assert.equal(someThing.get('foo'), 'baz');
});
```


### TESTING COMPUTED PROPERTIES

```javascript
// app/models/some-thing.js
export default Ember.Object.extend({
  foo: 'bar',

  computedFoo: Ember.computed('foo', function() {
    return 'computed ' + this.get('foo');
  })
});
```

```javascript
// tests/unit/models/some-thing-test.js
import { moduleForModel, test } from 'ember-qunit';

moduleForModel('some-thing', 'Unit | Model | some thing', {
  // Specify the other units that are required for this test.
  needs: []
});

test('computedFoo correctly concats foo', function(assert) {
  var someThing = this.subject().create({});

  someThing.set('foo', 'baz');

  assert.equal(someThing.get('computedFoo'), 'computed baz');
});
```


### TESTING OBSERVERS

```javascript
// app/models/some-thing.js
export default Ember.Object.extend({
  foo: 'bar',
  other: 'no',
  doSomething: Ember.observer('foo', function(){
    this.set('other', 'yes');
  })
});
```

```javascript
// tests/unit/models/some-thing-test.js
import { moduleForModel, test } from 'ember-qunit';

moduleForModel('some-thing', 'Unit | Model | some thing', {
  // Specify the other units that are required for this test.
  needs: []
});

test('doSomething observer sets other prop', function() {
  var someThing = this.subject().create();
  someThing.set('foo', 'baz');
  equal(someThing.get('other'), 'yes');
});
```
