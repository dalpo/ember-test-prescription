## Testing controllers

Given a sample `PostsController`

```javascript
export default Ember.Controller.extend({
  propA: 'You need to write tests',
  propB: 'And write one for me too',

  setPropB(str) {
    this.set('propB', str);
  },

  actions: {
    setProps(str) {
      this.set('propA', 'Testing is cool');
      this.setPropB(str);
    }
  }
});
```


## Testing controller actions

```javascript
import { moduleFor, test } from 'ember-qunit';

moduleFor('controller:posts-test', {
  // Specify the other units that are required for this test.
  // needs: ['controller:foo']
});
```

```javascript
test('calling the action setProps updates props', function(assert) {
  assert.expect(2);

  // get the controller instance
  var ctrl = this.subject();

  // trigger the action on the controller by using the `send` method,
  // passing in any params that our action may be expecting
  ctrl.send('setProps', 'Testing Rocks!');

  // finally we assert that our values have been updated
  // by triggering our action.
  assert.equal(ctrl.get('propA'), 'Testing is cool');
  assert.equal(ctrl.get('propB'), 'Testing Rocks!');
});
```
