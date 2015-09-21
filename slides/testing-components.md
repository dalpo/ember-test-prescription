## Testing components


### Component Unit Tests

An `Ember.Component` extends `Ember.Object` too

```javascript
import { test, moduleForComponent } from 'ember-qunit';

moduleForComponent('x-foo', {
  unit: true,
  needs: []
});
```

```javascript
// run a test
test('it renders', function(assert) {
  assert.expect(1);

  // creates the component instance
  var subject = this.subject();

  // render the component on the page
  this.render();
  assert.equal(this.$('.foo').text(), 'bar');
});
```


### But...

Unit tests require you to instantiate your<br>Ember components in JavaScript.

And you will never use an Ember component in this way on your production code.

Components are integrated into your app with templates, and you don't set attributes on them directly either.


### Component Integration Tests

```javascript
import hbs from 'htmlbars-inline-precompile';
import { test, moduleForComponent } from 'ember-qunit';

moduleForComponent('x-foo', {
  integration: true
});

```

```javascript
test('it renders', function(assert) {
  assert.expect(2);
  // setup the outer context
  this.set('value', 'cat');
  this.on('action', function(result) {
    assert.equal(result, 'bar');
  });

  // render the component
  this.render(hbs`
    {{ x-foo value=value action="result" }}
  `);

  assert.equal(this.$('div>.value').text(), 'cat');
  this.$('button').click();
});
```
