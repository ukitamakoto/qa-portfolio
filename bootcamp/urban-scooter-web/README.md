# Urban Scooter: web order form

A TripleTen QA Engineer Bootcamp project. Urban Scooter is a scooter-rental web app: the customer orders a scooter, chooses when and where it is delivered, and tracks the order. The supported environment is Chrome and Opera at 1280×720.

## What I tested

The order form ("who is the scooter for" and "rental"): name, surname, delivery address, metro station and phone number. Every field went through equivalence classes and boundary values, and every case was run in both browsers.

- **Techniques:** equivalence partitioning, boundary-value analysis, cross-browser runs.
- **Defects:** filed as Jira-style reports with steps, expected and actual results, priority and evidence.

**44 test cases** · 8 failed in at least one browser · 7 bug reports

- [Test cases](test-cases.md)
- [Bug reports](bug-reports.md)

| The phone field accepts a number without "+" | The phone field accepts letters |
|---|---|
| ![Bug 1](screenshots/Bug1_Telefone_Sem_Sinal_Mais.png) | ![Bug 2](screenshots/Bug2_Telefone_Com_Letras.png) |

Cases are in Portuguese, as written during the bootcamp.

[← Back to the portfolio](../../README.md)
