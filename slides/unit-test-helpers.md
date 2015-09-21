## Unit test helpers

By including Ember-QUnit,<br>you will have access to a number of test helpers:

- __moduleFor(fullName [, description [, callbacks]])__
  <small>*fullName*: The full name of the unit, (ie. controller:application, route:index, etc.)<br>
  *description*: the description of the module<br>
  *callbacks*: normal QUnit callbacks (setup and teardown), with addition to needs.</small>
- moduleForComponent(name [, description [, callbacks]])
  <small>*name*: the short name of the component that you'd use in a template, (ie. x-foo, ic-tabs, etc.)<br>
  *description*: the description of the module<br>
  *callbacks*: normal QUnit callbacks (setup and teardown), with addition to needs.</small>
- moduleForModel(name [, description [, callbacks]])
  <small>*name*: the short name of the model you'd use in store operations (ie. user, assignmentGroup, etc.)<br>
  *description*: the description of the module<br>
  *callbacks*: normal QUnit callbacks (setup and teardown), with addition to needs.</small>
- test(description, callbacks)
- setResolver

Note:
Test: Same as QUnit test except it includes the subject function which is used to create the test subject.
setResolver: Sets the resolver which will be used to lookup objects from the application container.


### Unit testing setup

In order to unit test your Ember application,<br>you need to let Ember know it is in test mode.

```
Ember.setupForTesting()
```

This call <u>TURN OFF</u> the Ember run loop execution.
