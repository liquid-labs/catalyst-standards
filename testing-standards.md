# Liquid Dev Testing Standards

## Purpose & scope

These standards address testing definitions and standards within the Liquid Dev context.

## Test Types

Though we use standard categorizations, our primary purpose in categorization is to define the requirements of the testing framework rather than the "nature" of the test itself. Which is just to say, the classification of a test is most simply understood as "what infrastructure do I need to have up and running to execute these tests?"

* **build check** is simply that the build process has completed without error. The build check is not itself a test type, but is a key precondition for unit testing.
* **unit test** require only single service. This may be a language interpreter or successfully compiled executable for source code or a running relational database for SQL commands. Where the test must interact with another system or library, all non-trivial behavior must be mocked.
* **integration test** coordinate two or more running services. Ideally, each combination could be tested in isolation.
* **end-to-end test** verify behavior of production-equivalent environments.
* **user testing** are tests with a limited number of users in the wild on live, pre-production environments.
* **usability testing**

## Unit Tests

### Model Packages

* Model Packages generally do not contain unit tests.

## Integration Tests
