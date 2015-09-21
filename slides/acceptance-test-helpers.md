## Acceptance test helpers

Ember includes several helpers to facilitate acceptance testing. There are two types of helpers:<br>__*asynchronous*__ and __*synchronous*__.


### ASYNCHRONOUS HELPERS

Asynchronous helpers will wait for asynchronous behavior of your application, so _each helper is only called after the previous one finishes_.

- click(selector)
- fillIn(selector, text)
- keyEvent(selector, type, keyCode)
- triggerEvent(selector, type, options)
- visit(url)

Note:
- click(selector)
  Clicks an element and triggers any actions triggered by the element's click event and returns a promise that fulfills when all resulting async behavior is complete.

- fillIn(selector, text)
  Fills in the selected input with the given text and returns a promise that fulfills when all resulting async behavior is complete. Works with <select> elements as well as <input> elements.

- keyEvent(selector, type, keyCode)
  Simulates a key event type, e.g. keypress, keydown, keyup with the desired keyCode on element found by the selector.

- triggerEvent(selector, type, options)
  Triggers the given event, e.g. blur, dblclick on the element identified by the provided selector.

- visit(url)
  Visits the given route and returns a promise that fulfills when all resulting async behavior is complete.

- currentPath()
  Returns the current path.

- currentRouteName()
  Returns the currently active route name.

- currentURL()
  Returns the current URL.

- find(selector, context)
  Finds an element within the app's root element and within the context (optional). Scoping to the root element is especially useful to avoid conflicts with the test framework's reporter, and this is done by default if the context is not specified.


### SYNCHRONOUS HELPERS

Synchronous helpers are performed immediately.

- currentPath()
- currentRouteName()
- currentURL()
- find(selector, context)

Note:
- currentPath()
  Returns the current path.

- currentRouteName()
  Returns the currently active route name.

- currentURL()
  Returns the current URL.

- find(selector, context)
  Finds an element within the app's root element and within the context (optional). Scoping to the root element is especially useful to avoid conflicts with the test framework's reporter, and this is done by default if the context is not specified.


### And Then???

The __*andThen*__ helper will wait for all preceding asynchronous helpers to complete prior to progressing forward.

```
// tests/acceptance/new-post-appears-first-test.js

test('simple test', function(assert) {
  assert.expect(1); // Ensure that we will perform one assertion

  visit('/posts/new');
  fillIn('input.title', 'My new post');
  click('button.submit');

  // Wait for asynchronous helpers above to complete
  andThen(function() {
    // Finally make our assertion
    assert.equal(find('ul.posts li:first').text(), 'My new post');
  });
});
```


### Custom helper

```
// tests/helpers/dblclick.js
import Ember from 'ember';

export default Ember.Test.registerAsyncHelper('dblclick',
  function(app, assert, selector, context) {
    var $el = findWithAssert(selector, context);

    Ember.run(function() {
      $el.dblclick();
    });
  }
);

```

Note:
Finally, don't forget to add your helpers in tests/.jshintrc and in tests/helpers/start-app.js. In tests/.jshintrc you need to add it in the predef section, otherwise you will get failing jshint tests:
