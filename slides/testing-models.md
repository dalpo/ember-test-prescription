## Testing models

Given a sample Ember Data model:

```javascript
// app/models/player.js
export default DS.Model.extend({
  level:     DS.attr('number', { defaultValue: 0 }),
  levelName: DS.attr('string', { defaultValue: 'Noob' }),

  levelUp() {
    var newLevel = this.incrementProperty('level');
    if (newLevel === 5) {
      this.set('levelName', 'Professional');
    }
  }
});
```


## Testing models

Ember Data Models can be tested using the `moduleForModel` helper:

```javascript
moduleForModel('player');

test('levelUp', function(assert) {
  // this.subject aliases the createRecord method on the model
  var player = this.subject({ level: 4 });

  // wrap asynchronous call in run loop
  Ember.run(function() {
    player.levelUp();
  });

  assert.equal(player.get('level'), 5);
  assert.equal(player.get('levelName'), 'Professional');
});
```


## Testing relationship

Assume that a `User` can own a `Profile`.

```javascript
// app/models/profile.js
export default DS.Model.extend({
  // code...
});
```

```javascript
// app/models/user.js
export default DS.Model.extend({
  profile: DS.belongsTo('profile')

  // code...
});
```


## Testing relationship

Then you could test that the<br>relationship is wired up correctly.

```javascript
// tests/unit/models/user-test.js
moduleForModel('user', {
  // Specify the other units that are required for this test.
  needs: ['model:profile']
});

test('profile relationship', function(assert) {
  var User = this.store().modelFor('user');
  var profile = Ember.get(User, 'relationshipsByName').get('profile');

  assert.equal(profile.key, 'profile');
  assert.equal(profile.kind, 'belongsTo');
});
```
