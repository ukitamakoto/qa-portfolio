# Six small tools

Small products and internal tools, each with focused automated checks.

Test titles are kept in their original language (English or Portuguese). Client and product names are anonymized.

## Wedding sites with RSVP and QR check-in

A web app that generates a unique site for each wedding, collects RSVPs and checks guests in at the door with a QR code.
**Stack:** React · Vite · **Test tooling:** `node:test`

- **TL-WED-U-009**: check-in never counts a guest twice.
- **TL-WED-U-008**: the same seed always generates the same site, and different seeds generate different sites.

<!-- catalog:wedding:start -->
**9 test cases** · 0 end-to-end · 9 unit & integration

#### Unit & integration

<details><summary><b>spec</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| TL-WED-U-001 | spec | contraste bate com os valores conhecidos |
| TL-WED-U-002 | spec | todas as paletas do vocabulário são legíveis |
| TL-WED-U-003 | spec | todas as fontes têm pesos declarados |
| TL-WED-U-004 | spec | todos os ornamentos sabem desenhar-se |
| TL-WED-U-005 | spec | o endereço das fontes inclui todas as famílias do par |
| TL-WED-U-006 | spec | a validação apanha variantes e ordem inválidas |
| TL-WED-U-007 | spec | o gerador nunca sai do vocabulário |
| TL-WED-U-008 | spec | a mesma semente dá o mesmo site, sementes diferentes dão sites diferentes |
| TL-WED-U-009 | spec | o check-in não conta ninguém a dobrar |

</details>
<!-- catalog:wedding:end -->

## Balloon-decoration simulator

A web app that previews balloon decorations with AI image generation.
**Stack:** React · Express · **Test tooling:** Playwright

- **TL-BAL-E2E-002**: a slow network shows the loading skeleton instead of a blank page.

<!-- catalog:balloon:start -->
**2 test cases** · 2 end-to-end · 0 unit & integration

#### End-to-end

| ID | Suite | Scenario |
|---|---|---|
| TL-BAL-E2E-001 | P0 Smoke Test Suite | should load the homepage and display critical elements |
| TL-BAL-E2E-002 | P0 Smoke Test Suite | destructive test: slow network skeleton loading |
<!-- catalog:balloon:end -->

## Code-driven video pipeline

A shared engine that renders branded videos for several clients from manifests.
**Stack:** Remotion · FFmpeg · **Test tooling:** `node:test`

- **TL-VID-U-002**: a manifest whose timeline exceeds its declared duration is rejected.

<!-- catalog:video:start -->
**3 test cases** · 0 end-to-end · 3 unit & integration

#### Unit & integration

<details><summary><b>manifests</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| TL-VID-U-001 | manifests | example project resolves with its own brand |
| TL-VID-U-002 | manifests | manifest rejects a timeline that exceeds declared duration |
| TL-VID-U-003 | manifests | brand JSON contains complete color and typography groups |

</details>
<!-- catalog:video:end -->

## Lead-prospecting agent

A scheduled agent that researches leads through a restricted gateway. Its tests guard what the agent is allowed to do.
**Stack:** Python · **Test tooling:** `unittest`

- **TL-PRO-U-005**: an unapproved action is rejected.
- **TL-PRO-U-009**: a path that escapes the working folder is rejected.

<!-- catalog:prospecting:start -->
**10 test cases** · 0 end-to-end · 10 unit & integration

#### Unit & integration

<details><summary><b>agentctl</b> · 10 cases</summary>

| ID | Suite | Case |
|---|---|---|
| TL-PRO-U-001 | ValidationTests | Enforces safe defaults |
| TL-PRO-U-002 | ValidationTests | Rejects approval property |
| TL-PRO-U-003 | ValidationTests | Rejects weak fit |
| TL-PRO-U-004 | ValidationTests | Rejects email without valid draft |
| TL-PRO-U-005 | ValidationTests | Rejects unapproved actor |
| TL-PRO-U-006 | ValidationTests | Apify limits |
| TL-PRO-U-007 | ValidationTests | Google queries are serialized for actor |
| TL-PRO-U-008 | ValidationTests | Contact urls are serialized for actor |
| TL-PRO-U-009 | ValidationTests | Rejects path escape |
| TL-PRO-U-010 | ValidationTests | Duplicate keys cover domain email and name city |

</details>
<!-- catalog:prospecting:end -->

## Hotel-PMS guest-profile extractor

A tool that exports guest profiles from a property-management system and classifies guests as new, returning or lapsed.
**Stack:** Node.js · Playwright · **Test tooling:** `node:test`

- **TL-PMS-U-005**: cancelled bookings and no-shows do not count as stays.

<!-- catalog:pms:start -->
**7 test cases** · 0 end-to-end · 7 unit & integration

#### Unit & integration

<details><summary><b>scraper</b> · 7 cases</summary>

| ID | Suite | Case |
|---|---|---|
| TL-PMS-U-001 | scraper | classifica como novo somente quando há contador explícito igual a zero |
| TL-PMS-U-002 | scraper | classifica estadia recente como recorrente |
| TL-PMS-U-003 | scraper | classifica última estadia com mais de dois anos como antigo |
| TL-PMS-U-004 | scraper | ignora estadias futuras na contagem de histórico |
| TL-PMS-U-005 | scraper | ignora reservas canceladas e no-show |
| TL-PMS-U-006 | scraper | achata objetos e preserva listas como JSON |
| TL-PMS-U-007 | scraper | desembrulha os formatos usuais da API |

</details>
<!-- catalog:pms:end -->

## Job-application assistant

A local robot that prepares job applications on company career pages and recruiting portals.
**Stack:** Node.js · Playwright · **Test tooling:** `node:test`

- **TL-JOB-U-003**: the cover letter is written in the country's language and never invents a company or a role.

<!-- catalog:jobs:start -->
**4 test cases** · 0 end-to-end · 4 unit & integration

#### Unit & integration

<details><summary><b>prefill</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| TL-JOB-U-001 | prefill | seleciona CV por área |
| TL-JOB-U-002 | prefill | permite escolher uma variante explícita de CV |
| TL-JOB-U-003 | prefill | gera carta no idioma do país sem inventar empresa ou cargo |
| TL-JOB-U-004 | prefill | detecta portais de recrutamento |

</details>
<!-- catalog:jobs:end -->

[← Back to the portfolio](../../README.md)
