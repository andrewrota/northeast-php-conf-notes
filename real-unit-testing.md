# Real Unit Testing
**By Christopher Davis @chrisguitarguy**

[Joind.in](http://joind.in/11483)

Wrote demeanor

More accurate title is behavioral unit testing

## Types of Tests

### Acceptance Tests

Test the entire thing

### Integration Tests

Test the components at the seams

### Unit Tests

Test smallest units of your applications

## How to Write Tests

[github](https://github.com/crhisguitarguy/RealUnitTesting)

1. Start with a Stub
2. Write an Action
3. Write a Verification
4. Name It
5. Create the Setup

## Using Test Doubles

Read Martin Fowler's 'Mocks Aren't Stubs'

* Stubs - return canned or pre-programmed responses
* Dummie - a dependency that's not needed for the test (gets passed in as collaborator)
* Fake - a simple implementation or null object

* Spies - verify expectations after
* Mocks - set expectations before

Prophecy is a full-featured PHP test double framework

Mocking frameworks aren't required, but they are super convenient.

With mocks there is no verification step because the test framework takes care of it.  There's lots of code to set up expectations, though, which can sometimes be harder to read.  It's a trade off.  But in both cases we care that the cart sent a message.

Readable mocking is very difficult.  It's easy when you're mocking things to have a bunch of unreadable code.  You can get around this with a couple things:

* Mock Factories
* Hide expectations; use the language of your domain (extract method on your tests)

Don't mock value objects, just use them.  They're immutable and equality is not based on identity.  Almost like a form of a stub.

Only mock true collaborators.  For example, maybe your logger has no impact on the course of the test so you can just use a null or a fake object.

## Conclusion

Write tests for behavior, not just to make sure you have 100% code coverage.  An easy way to make your tests better is to **name** them better.

## Questions, etc.

* Display logic --> acceptance testing (?)
* If you're refactoring a legacy application acceptance tests are more important first
* Mockery and Prophecy are good mocking frameworks
* You don't necessarily have to write your own stubs.  Mockery, for example, will write stubs for you.
