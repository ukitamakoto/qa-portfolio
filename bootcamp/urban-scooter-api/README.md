# Urban Scooter: REST API

A TripleTen QA Engineer Bootcamp project. It covers the back end of the scooter service: a REST API in Node.js with PostgreSQL that registers couriers and logs them in, creates, lists, tracks and accepts orders, and deletes couriers together with their orders.

## What I tested

A checklist for the courier endpoints:
- the required fields, and the length and character rules for login, password and first name;
- duplicate logins;
- the error codes and messages;
- whether deleting a courier also deletes their orders.

- **Techniques:** boundary values on every field rule, negative cases, checking the response codes and bodies against the specification.

**22 test cases** · 12 passed · 10 failed

Most of the failures are missing validations: the API accepts logins, passwords and names outside the specified limits, and deleting a courier does not remove their orders.

- [Test cases](test-cases.md)

Cases are in Portuguese, as written during the bootcamp.

[← Back to the portfolio](../../README.md)
