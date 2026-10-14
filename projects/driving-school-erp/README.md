# Multi-tenant ERP for driving schools

A management system for driving schools. It covers students and enrolment, lesson and exam scheduling, finance (plans, instalments, discounts), fleet and instructors, with separate portals for staff, instructors and students. It is used in production by driving schools and is being turned into a white-label, multi-tenant product.

**Stack:** React 19 · TypeScript · Vite · PostgreSQL (Supabase) · **Test tooling:** Playwright · Vitest · Testing Library

## What I did

- Built the application together with its test suites: end-to-end flows in Playwright, plus unit and integration checks in Vitest.
- Turned business rules into reproducible tests: scheduling conflicts, exam eligibility, instalment maths, data imports.
- Ran the end-to-end suite on a desktop profile and on four mobile profiles (current and older Android and iOS devices).
- Wrote 50+ SQL scripts that check data integrity, constraints, triggers and migration results, and tested Row Level Security policies for tenant isolation.
- Reported 13+ UI defects with evidence, expected behaviour and severity, and fixed them in the same codebase.

## Test strategy

| Level | Tool | What it covers |
|---|---|---|
| End-to-end | Playwright: HTML report, screenshots on failure, traces on retry, parallel runs, retries on CI | Login and roles, staff/instructor/student portals, scheduling, finance, exams, fleet, mobile layouts |
| Unit & integration | Vitest + Testing Library (jsdom; coverage thresholds of 70% for statements, lines and functions, 60% for branches) | Services, hooks, financial rules, scheduling conflicts, imports from a legacy system |

## Highlights

- **ERP-E2E-001**: the app boots without HTTP/2 protocol errors or failed fetches. This smoke check catches a broken deploy before anything else runs.
- **ERP-E2E-003**: modals open and close on mobile viewports without breaking the layout.
- **ERP-U-074**: scheduling refuses a double booking when the instructor already has an event at that time.
- **ERP-U-298 to ERP-U-305**: instalments always add up to the total. Discounts, quantities and cent rounding never create a mismatch.

## Catalogue

Test titles are kept in their original language (English or Portuguese). Client and product names are anonymized.

<!-- catalog:erp:start -->
**428 test cases** · 72 end-to-end · 356 unit & integration

#### End-to-end

| ID | Suite | Scenario |
|---|---|---|
| ERP-E2E-001 | App Boot & Stability | Should load the app without HTTP2 Protocol Errors or failed fetches |
| ERP-E2E-002 | Agenda & Próximos Exames Stability | Should load Próximos Exames and search without crashing |
| ERP-E2E-003 | Mobile Responsiveness & Modals | Should open and close modals on Mobile viewports without layout breaking |
| ERP-E2E-004 | Portals Stability | Should load Student Portal without HTTP2 Protocol Errors or failed fetches |
| ERP-E2E-005 | Portals Stability | Should load Instructor Portal without HTTP2 Protocol Errors or failed fetches |
| ERP-E2E-006 | Student Portal Data Visualization & Theoretical Tests - Category ${category} | deve logar e ver as informações detalhadas e corretas das suas aulas e exames |
| ERP-E2E-007 | Student Portal Data Visualization & Theoretical Tests - Category ${category} | deve aceder aos testes teóricos práticos com a categoria e imagens corretas |
| ERP-E2E-008 | Student Portal Data Visualization & Theoretical Tests - Multiple Categories | deve logar e aceder ao E-Learning e visualizar todas as categorias contratadas |
| ERP-E2E-009 | Authentication & RBAC Basics | should login successfully as Super Admin |
| ERP-E2E-010 | Authentication & RBAC Basics | should login successfully as Administrador |
| ERP-E2E-011 | Authentication & RBAC Basics | should show error for invalid credentials |
| ERP-E2E-012 | Authentication & RBAC Basics | should logout successfully |
| ERP-E2E-013 | Curriculum & Attendance Flow | should verify linear progression and enrollment |
| ERP-E2E-014 | ERP - Enrollment and Agenda Flow (UUID Migration Verification) | should enroll a new student and schedule an appointment successfully |
| ERP-E2E-015 | Financial Management (Financeiro) | should display financial page with correct title |
| ERP-E2E-016 | Financial Management (Financeiro) | should display all 4 KPI stat cards |
| ERP-E2E-017 | Financial Management (Financeiro) | should display monthly evolution chart |
| ERP-E2E-018 | Financial Management (Financeiro) | should display cash flow forecast chart |
| ERP-E2E-019 | Financial Management (Financeiro) | should display transaction table with correct headers |
| ERP-E2E-020 | Financial Management (Financeiro) | should display pagination controls |
| ERP-E2E-021 | Financial Management (Financeiro) | should filter transactions by Entradas (Income) |
| ERP-E2E-022 | Financial Management (Financeiro) | should filter transactions by Saídas (Expense) |
| ERP-E2E-023 | Financial Management (Financeiro) | should search transactions by description |
| ERP-E2E-024 | Financial Management (Financeiro) | should show empty results for non-matching search |
| ERP-E2E-025 | Financial Management (Financeiro) | should open new transaction modal |
| ERP-E2E-026 | Financial Management (Financeiro) | should have export CSV button |
| ERP-E2E-027 | Financial Management (Financeiro) | Gerente should have access to Financeiro |
| ERP-E2E-028 | Fleet Management (Frota) | should display fleet page with correct title |
| ERP-E2E-029 | Fleet Management (Frota) | should display vehicle cards in grid |
| ERP-E2E-030 | Fleet Management (Frota) | should open new vehicle modal |
| ERP-E2E-031 | Fleet Management (Frota) | should search and filter vehicles by plate |
| ERP-E2E-032 | Fleet Management (Frota) | should filter vehicles by category |
| ERP-E2E-033 | Fleet Management (Frota) | should filter vehicles by status |
| ERP-E2E-034 | Fleet Management (Frota) | should show empty state for non-matching filter |
| ERP-E2E-035 | Fleet Management (Frota) | should open vehicle detail modal on card click |
| ERP-E2E-036 | Fleet Management (Frota) | vehicle detail modal should show tabs (Info, Manutenção, Quilometragem) |
| ERP-E2E-037 | Fleet Management (Frota) | vehicle detail should display mileage and health stats |
| ERP-E2E-038 | Fleet Management (Frota) | vehicle form should have required fields |
| ERP-E2E-039 | Instructor Portal Verification | should fetch calendar events when accessing the instructor dashboard directly |
| ERP-E2E-040 | Fase 3 — Avaliação Anónima do Instrutor | T3.1: Após aula prática attended — botão de avaliação visível |
| ERP-E2E-041 | Fase 3 — Avaliação Anónima do Instrutor | T3.2: Modal de avaliação abre com 5 estrelas e campo de comentário |
| ERP-E2E-042 | Fase 3 — Avaliação Anónima do Instrutor | T3.3: Submeter avaliação com 5 estrelas — mensagem de sucesso |
| ERP-E2E-043 | Fase 3 — Avaliação Anónima do Instrutor | T3.4: Quando não há avaliação pendente — secção de avaliação não aparece |
| ERP-E2E-044 | Fase 3 — Avaliação Anónima do Instrutor | T3.5: Botão Enviar Avaliação desabilitado sem estrelas seleccionadas |
| ERP-E2E-045 | Multi-tenant Data Isolation | should cross-verify data isolation between schools |
| ERP-E2E-046 | login | a equipa entra na app e a primeira página carrega sem erros |
| ERP-E2E-047 | Navigation & Route Protection | root URL should show Landing Page with portal selection |
| ERP-E2E-048 | Navigation & Route Protection | unauthenticated access to /#/agenda should show login form |
| ERP-E2E-049 | Navigation & Route Protection | unauthenticated access to /#/financial should show login form |
| ERP-E2E-050 | Navigation & Route Protection | /#/login route should show email and password toggle |
| ERP-E2E-051 | Navigation & Route Protection | Admin can navigate to all main sections via sidebar |
| ERP-E2E-052 | Navigation & Route Protection | Instrutor cannot see admin links |
| ERP-E2E-053 | Navigation & Route Protection | direct URL access to /#/financial should be blocked for Instrutor |
| ERP-E2E-054 | Navigation & Route Protection | login page should display branding |
| ERP-E2E-055 | Verify New Features | Instructor Portal & Student Practical Tab features |
| ERP-E2E-056 | Fase 1 — Pré-requisitos Sequenciais | T1.1: M1 sempre disponível (sem pré-requisito) |
| ERP-E2E-057 | Fase 1 — Pré-requisitos Sequenciais | T1.2: M2 bloqueado quando M1 = not_started |
| ERP-E2E-058 | Fase 1 — Pré-requisitos Sequenciais | T1.3: M2 bloqueado quando M1 = enrolled (inscrito mas não attended) |
| ERP-E2E-059 | Fase 1 — Pré-requisitos Sequenciais | T1.4: M2 desbloqueado quando M1 = attended |
| ERP-E2E-060 | Fase 1 — Pré-requisitos Sequenciais | T1.5: M2 bloqueado quando M1 = missed |
| ERP-E2E-061 | Role-Based Access Control (RBAC) | Administrador should have Administrative access |
| ERP-E2E-062 | Role-Based Access Control (RBAC) | Instrutor should NOT have Administrative access |
| ERP-E2E-063 | Student Card Rendering Tests | should render student card for type: ${cardType} |
| ERP-E2E-064 | Student Portal Verification (Post-UUID Migration) | should display student portal login page correctly |
| ERP-E2E-065 | Student Portal Verification (Post-UUID Migration) | should submit NIF and show feedback message |
| ERP-E2E-066 | Student Portal Verification (Post-UUID Migration) | should show error for invalid NIF |
| ERP-E2E-067 | ui | add product and payment |
| ERP-E2E-068 | Fase 2 — Lista de Espera | T2.1: Aula disponível — slots aparecem (sem lista de espera) |
| ERP-E2E-069 | Fase 2 — Lista de Espera | T2.2: Aula cheia — botão "Entrar na Lista de Espera" aparece no modal |
| ERP-E2E-070 | Fase 2 — Lista de Espera | T2.3: Aula cheia — entra na lista e vê botão desabilitado após join |
| ERP-E2E-071 | Fase 2 — Lista de Espera | T2.4: Entrar na lista de espera — mostra mensagem de sucesso com posição |
| ERP-E2E-072 | Fase 2 — Lista de Espera | T2.5: Após entrar — indicador de posição na fila visível |

#### Unit & integration

<details><summary><b>auditService</b> · 13 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-001 | logAction | should insert audit log with correct data |
| ERP-U-002 | logAction | should include environment details (_env) in audit log |
| ERP-U-003 | logAction | should detect Chrome browser from user agent |
| ERP-U-004 | logAction | should detect MacOS from user agent |
| ERP-U-005 | logAction | should handle null entity_id and entity_name gracefully |
| ERP-U-006 | logAction | should merge custom details with environment info |
| ERP-U-007 | logAction | should NOT throw when Supabase insert fails (silent fail) |
| ERP-U-008 | logAction | should warn in console when insert fails |
| ERP-U-009 | fetchAuditLogs | should query audit_logs table with default pagination |
| ERP-U-010 | fetchAuditLogs | should apply userId filter when provided |
| ERP-U-011 | fetchAuditLogs | should apply date range filters |
| ERP-U-012 | fetchAuditLogs | should throw when Supabase returns an error |
| ERP-U-013 | fetchAuditLogs | should return empty array when no data matches |

</details>

<details><summary><b>avulsaLessonCount</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-014 | avulsaLessonCount | uses contract quantity as the avulsa lesson count |
| ERP-U-015 | avulsaLessonCount | ignores a polluted 32h base for avulsa (no 32\*qty overcount) |
| ERP-U-016 | avulsaLessonCount | treats missing/1 quantity as a single avulsa lesson |
| ERP-U-017 | avulsaLessonCount | leaves every non-avulsa product untouched (no regression) |
| ERP-U-018 | avulsaLessonCount | isAvulsaLesson only matches the canonical avulsa products |

</details>

<details><summary><b>avulsaOnAbsenceRpc</b> · 10 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-019 | create_avulsa_for_absence | o cliente chama a função que a migração cria |
| ERP-U-020 | create_avulsa_for_absence | os parâmetros do cliente batem certo com os do SQL |
| ERP-U-021 | create_avulsa_for_absence | o cliente já não insere em student_products no caminho da falta |
| ERP-U-022 | create_avulsa_for_absence | só aceita produtos de aula avulsa ativos |
| ERP-U-023 | create_avulsa_for_absence | mantém o aluno dentro das escolas de quem marca a falta |
| ERP-U-024 | create_avulsa_for_absence | o preço vem do catálogo, nunca do cliente |
| ERP-U-025 | create_avulsa_for_absence | aula dupla: desduplica pelo número de faltas do dia, não por uma janela de tempo |
| ERP-U-026 | a avulsa criada pela falta sobrevive | o updateStudent não apaga contratos que a ficha aberta não conhece |
| ERP-U-027 | a avulsa criada pela falta sobrevive | remover um contrato na ficha é um DELETE dessa linha |
| ERP-U-028 | a avulsa criada pela falta sobrevive | a falta não depende de a lista de alunos já ter carregado |

</details>

<details><summary><b>avulsaProductMatch</b> · 8 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-029 | findAvulsaProduct | devolve o produto da categoria, ao preço da categoria |
| ERP-U-030 | findAvulsaProduct | C não apanha o C+E — era o bug dos 60€ contra 65€ |
| ERP-U-031 | findAvulsaProduct | C+E encontra o seu produto — o "+" já não é quantificador |
| ERP-U-032 | findAvulsaProduct | categoria sem produto no catálogo não devolve nada |
| ERP-U-033 | findAvulsaProduct | ignora produtos que não sejam aula avulsa |
| ERP-U-034 | findAvulsaProduct | tolera maiúsculas e espaços à volta da categoria |
| ERP-U-035 | findAvulsaProduct | não rebenta com categorias que tenham caracteres de regex |
| ERP-U-036 | findAvulsaProduct | lê a categoria do nome do produto |

</details>

<details><summary><b>chunkRecovery</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-037 | recoverFromStaleChunk | recarrega uma vez e marca a tentativa no URL |
| ERP-U-038 | recoverFromStaleChunk | não recarrega uma segunda vez — o marcador já está no URL |
| ERP-U-039 | recoverFromStaleChunk | preserva a rota do HashRouter ao recarregar |
| ERP-U-040 | recoverFromStaleChunk | recarrega mesmo quando o service worker não existe |
| ERP-U-041 | clearRecoveryMarker | limpa o marcador depois de o arranque correr bem |

</details>

<details><summary><b>ClassesView</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-042 | ClassesView | displays the instructor name correctly for scheduled classes |

</details>

<details><summary><b>clausulaSextaVehicles</b> · 12 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-043 | Bug 1: StudentProfilePage — schoolVehicles filter | ACTUAL CODE: misses vehicle v2 (no legacy schoolId, only schoolIds) |
| ERP-U-044 | Bug 1: StudentProfilePage — schoolVehicles filter | ACTUAL CODE: only returns vehicles with legacy schoolId |
| ERP-U-045 | Bug 1: StudentProfilePage — schoolVehicles filter | FIXED CODE: includes vehicles associated via vehicle_schools |
| ERP-U-046 | Bug 2: ContractEditorModal — category filter | ACTUAL CODE: excludes v4 (no category) from Cat B contract |
| ERP-U-047 | Bug 2: ContractEditorModal — category filter | ACTUAL CODE: returns only Cat B vehicles with category set |
| ERP-U-048 | Bug 2: ContractEditorModal — category filter | FIXED CODE: includes v4 (no category = universal) in Cat B contract |
| ERP-U-049 | Bug 2: ContractEditorModal — category filter | ACTUAL CODE: Cat A contract returns ONLY Cat A vehicles |
| ERP-U-050 | Bug 3 & 4: PDF generator — double filtering + missing category | BUG 4 CONFIRMED: vehicles passed to PDF have no category field |
| ERP-U-051 | Bug 3 & 4: PDF generator — double filtering + missing category | BUG 3 CONFIRMED: PDF filter is redundant — all vehicles pass through |
| ERP-U-052 | Bug 3 & 4: PDF generator — double filtering + missing category | PDF filter with a Cat A contract still shows Cat B vehicles (no category to filter) |
| ERP-U-053 | Combined: Full chain — What actually happens for a [city] Cat B student | ACTUAL chain: counts vehicles that reach Cláusula Sexta |
| ERP-U-054 | Combined: Full chain — What actually happens for a [city] Cat B student | FIXED chain: all valid vehicles reach Cláusula Sexta |

</details>

<details><summary><b>composicaoPrecoContrato</b> · 11 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-055 | composição de preço ↔ valor contratado ↔ contrato | a soma da composição é o valor total do produto |
| ERP-U-056 | composição de preço ↔ valor contratado ↔ contrato | editar uma parcela muda o valor total (era o bug: total ficava congelado) |
| ERP-U-057 | composição de preço ↔ valor contratado ↔ contrato | remover e adicionar linhas recalcula o total |
| ERP-U-058 | composição de preço ↔ valor contratado ↔ contrato | soma com cêntimos não acumula erro de ponto flutuante |
| ERP-U-059 | composição de preço ↔ valor contratado ↔ contrato | o contrato usa a composição guardada, não a distribuição por rácios |
| ERP-U-060 | composição de preço ↔ valor contratado ↔ contrato | carta sem composição gravada leva o template IMT, não os rácios |
| ERP-U-061 | composição de preço ↔ valor contratado ↔ contrato | C+E sem composição: a inscrição no contrato é 300€, não 90,31€ dos rácios |
| ERP-U-062 | composição de preço ↔ valor contratado ↔ contrato | categoria A sem composição: o contrato tem a linha do módulo teórico específico |
| ERP-U-063 | composição de preço ↔ valor contratado ↔ contrato | produto que não é carta (template vazio) mantém o fallback por rácios |
| ERP-U-064 | composição de preço ↔ valor contratado ↔ contrato | hours null vira 0 no contrato (PriceComponent.hours não é nullable) |
| ERP-U-065 | composição de preço ↔ valor contratado ↔ contrato | produto sem composição mantém o fallback por rácios |

</details>

<details><summary><b>contratoLayoutPdf</b> · 2 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-066 | layout do contrato em PDF | não desenha nada fora da coluna nem invade a coluna da direita |
| ERP-U-067 | layout do contrato em PDF | não duplica a morada do aluno nem deixa \\n ou espaços duplos |

</details>

<details><summary><b>dbGuard</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-068 | validarProjeto | aceita quando o DATABASE_URL pertence ao projeto configurado |
| ERP-U-069 | validarProjeto | recusa quando o DATABASE_URL é de outro projeto |
| ERP-U-070 | validarProjeto | recusa quando falta o SUPABASE_PROJECT_REF |
| ERP-U-071 | validarProjeto | recusa quando falta o DATABASE_URL |

</details>

<details><summary><b>exam-cascade-sync</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-072 | 1. Finding Adjacent Events | should find the preceding lesson_exam when moving an exam_practical |
| ERP-U-073 | 1. Finding Adjacent Events | should return undefined if no lesson_exam exists for the student on that day |
| ERP-U-074 | 2. Conflict Prevention (Double Booking) | should detect conflict if target instructor has an event during the combined time |
| ERP-U-075 | 2. Conflict Prevention (Double Booking) | should allow move if target instructor is free |

</details>

<details><summary><b>exam-dossier-sync</b> · 34 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-076 | 1. Event Type Qualification (isExamType) | should recognize exam_theory as exam type |
| ERP-U-077 | 1. Event Type Qualification (isExamType) | should recognize exam_practical as exam type |
| ERP-U-078 | 1. Event Type Qualification (isExamType) | should recognize exam_imt as exam type |
| ERP-U-079 | 1. Event Type Qualification (isExamType) | should recognize exam as exam type |
| ERP-U-080 | 1. Event Type Qualification (isExamType) | should NOT recognize lesson as exam type |
| ERP-U-081 | 1. Event Type Qualification (isExamType) | should recognize lesson_exam as an exam type |
| ERP-U-082 | 1. Event Type Qualification (isExamType) | should NOT qualify empty/null type |
| ERP-U-083 | 2. ID-Based Matching (Same UUID) | HAPPY PATH: should match when exam dossier ID === calendar event ID |
| ERP-U-084 | 2. ID-Based Matching (Same UUID) | BUG SCENARIO: IDs MISMATCH when exam is created from Agenda (not from Dossiê) |
| ERP-U-085 | 2. ID-Based Matching (Same UUID) | CRITICAL BUG: IDs differ because Dossiê exam was created BEFORE calendar sync |
| ERP-U-086 | 3. Type + Date Fallback Matching | should match theory exam: dossiê type="theory" ↔ calendar type="exam_theory" |
| ERP-U-087 | 3. Type + Date Fallback Matching | should match practical exam: dossiê type="practical" ↔ calendar type="exam_practical" |
| ERP-U-088 | 3. Type + Date Fallback Matching | should match practical exam: dossiê type="practical" ↔ calendar type="exam_imt" |
| ERP-U-089 | 3. Type + Date Fallback Matching | should match practical exam: dossiê type="practical" ↔ calendar type="exam" |
| ERP-U-090 | 3. Type + Date Fallback Matching | ★ BUG: should NOT match when dates are different |
| ERP-U-091 | 3. Type + Date Fallback Matching | ★ BUG: should handle Portuguese type names in dossiê |
| ERP-U-092 | 3. Type + Date Fallback Matching | ★ BUG: should handle "prática" type name in dossiê |
| ERP-U-093 | 3. Type + Date Fallback Matching | ★ POSSIBLE BUG: dossiê has datetime string with time, calendar has date-only |
| ERP-U-094 | 3. Type + Date Fallback Matching | ★ AMBIGUITY: two exams of same type on same date → removes first one found |
| ERP-U-095 | 4. Student Matching | should match student by ID |
| ERP-U-096 | 4. Student Matching | should match student by NIF |
| ERP-U-097 | 4. Student Matching | ★ BUG: should NOT find student when studentId is missing on the calendar event |
| ERP-U-098 | 4. Student Matching | ★ BUG: calendar event has NIF as studentId but student has no NIF |
| ERP-U-099 | 5. Full Integration: removeExamFromStudent simulation | SCENARIO A: Exam created in Dossiê, synced to Calendar, deleted from Calendar |
| ERP-U-100 | 5. Full Integration: removeExamFromStudent simulation | SCENARIO B: Exam created in Calendar, synced to Dossiê, deleted from Calendar |
| ERP-U-101 | 5. Full Integration: removeExamFromStudent simulation | ★ SCENARIO C (LIKELY BUG): Exam created in Calendar, NOT synced to Dossiê, deleted from Calendar |
| ERP-U-102 | 5. Full Integration: removeExamFromStudent simulation | ★ SCENARIO D (ROOT CAUSE): Event has no studentId → entire sync is skipped |
| ERP-U-103 | 5. Full Integration: removeExamFromStudent simulation | ★ SCENARIO E: Student loaded lazily — exams array is empty at deletion time |
| ERP-U-104 | 5. Full Integration: removeExamFromStudent simulation | ★ SCENARIO F: Student found by NIF but exams state is stale |
| ERP-U-105 | 5. Full Integration: removeExamFromStudent simulation | SCENARIO G: Multiple exams, deleting the correct one by ID |
| ERP-U-106 | 6. ExamDossier handleRemove (profile-side deletion) | handleRemove calls deleteEvent with the exam ID (line 1992) |
| ERP-U-107 | 6. ExamDossier handleRemove (profile-side deletion) | ★ BUG: Legacy exam ID is NOT a valid UUID → deleteEvent skips DB delete |
| ERP-U-108 | 7. Timing Issues | ★ CRITICAL: deleteEvent uses setTimeout(UNDO_TIMEOUT_MS) before actual DB delete |
| ERP-U-109 | 7. Timing Issues | ★ updateStudent could fail if matchedStudent has stale/incomplete data |

</details>

<details><summary><b>exam-instructor-change</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-110 | Theory Exams (exam_theory) | should NOT allow changing the instructor (forces null) |
| ERP-U-111 | Practical Exams (exam_practical, exam_imt, exam) | should allow changing the instructor for exam_practical |
| ERP-U-112 | Practical Exams (exam_practical, exam_imt, exam) | should allow changing the instructor for exam_imt |

</details>

<details><summary><b>examConflicts</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-113 | findExamConflict | deteta o instrutor ocupado com uma aula normal |
| ERP-U-114 | findExamConflict | deteta o instrutor ocupado com outro exame ou aula de exame (o caso mais comum) |
| ERP-U-115 | findExamConflict | permite 2 exames práticos no mesmo instrutor e veículo, bloqueia o 3.º |
| ERP-U-116 | findExamConflict | trata bloqueios de agenda como erro |
| ERP-U-117 | findExamConflict | deteta o aluno já agendado (direto ou como presença em teórica) |
| ERP-U-118 | findExamConflict | deteta o veículo ocupado por outro instrutor |
| ERP-U-119 | findExamConflict | sobreposição parcial conta; horário seguinte não |
| ERP-U-120 | findExamConflict | ignora cancelados/faltas, outros dias e o próprio evento em edição |
| ERP-U-121 | findExamConflict | sem data ou hora não bloqueia nada |

</details>

<details><summary><b>examHistory</b> · 7 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-122 | examQuestionsService — localStorage persistence | saveExamResult stores result in localStorage |
| ERP-U-123 | examQuestionsService — localStorage persistence | getExamHistory returns empty array when localStorage is empty |
| ERP-U-124 | examQuestionsService — localStorage persistence | getExamHistory returns parsed results from localStorage |
| ERP-U-125 | examQuestionsService — localStorage persistence | getExamHistory handles corrupted localStorage gracefully |
| ERP-U-126 | examQuestionsService — localStorage persistence | saveExamResult limits stored entries to 20 |
| ERP-U-127 | examQuestionsService — UUID validation | isValidUUID rejects invalid inputs |
| ERP-U-128 | examQuestionsService — ExamResult type | ExamResult supports optional supabaseId |

</details>

<details><summary><b>examQuestions</b> · 36 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-129 | ExamQuestions Data Integrity | every question has a non-empty id |
| ERP-U-130 | ExamQuestions Data Integrity | every question has non-empty question text |
| ERP-U-131 | ExamQuestions Data Integrity | no question contains placeholder text patterns |
| ERP-U-132 | ExamQuestions Data Integrity | every question has 2 to 4 options (IMT official format) |
| ERP-U-133 | ExamQuestions Data Integrity | correctAnswer index is within options bounds |
| ERP-U-134 | ExamQuestions Data Integrity | every question has a non-empty explanation |
| ERP-U-135 | ExamQuestions Data Integrity | every question has a valid theme |
| ERP-U-136 | ExamQuestions Data Integrity | every question has a valid category |
| ERP-U-137 | ExamQuestions Data Integrity | all question ids are unique within the same category pool |
| ERP-U-138 | Category C (Pesados Mercadorias) | generates exactly 20 questions for exam mode |
| ERP-U-139 | Category C (Pesados Mercadorias) | includes both common and C-specific questions |
| ERP-U-140 | Category C (Pesados Mercadorias) | C-specific questions cover pesados topics (not placeholders) |
| ERP-U-141 | Category C (Pesados Mercadorias) | respects 75/25 proportion (common/specific) |
| ERP-U-142 | Category CE (Pesados + Reboque) | CE-specific questions are real content |
| ERP-U-143 | Category D (Pesados Passageiros) | D-specific questions are real content |
| ERP-U-144 | getExamQuestions | returns shuffled questions (not always same order) |
| ERP-U-145 | getExamQuestions | never returns more questions than requested |
| ERP-U-146 | getExamQuestions | returns questions only from allowed categories |
| ERP-U-147 | getQuestionsByTheme | returns only questions of the specified theme |
| ERP-U-148 | getQuestionsByTheme | returns empty array for invalid theme |
| ERP-U-149 | getAvailableThemes | returns themes with correct counts |
| ERP-U-150 | getAvailableThemes | themes are sorted by count descending |
| ERP-U-151 | CATEGORY_INFO | all categories have valid configurations |
| ERP-U-152 | CATEGORY_INFO | Category C requires 20 questions, 2 max errors, 25min |
| ERP-U-153 | CATEGORY_INFO | Category CE requires 20 questions, 2 max errors, 25min |
| ERP-U-154 | CATEGORY_INFO | Category D requires 20 questions, 2 max errors, 25min |
| ERP-U-155 | CATEGORY_INFO | no professional categories exist (CAM, CMT, TVDE, Instrutor) |
| ERP-U-156 | ExamResult Persistence | saves and retrieves exam result |
| ERP-U-157 | ExamResult Persistence | limits history to 20 entries |
| ERP-U-158 | ExamResult Persistence | returns empty array when no history |
| ERP-U-159 | ScrollToTop Hook | useScrollToTop is exported from StudentPortalLayout |
| ERP-U-160 | ScrollToTop Hook | useScrollToTop returns a function (no-op outside provider) |
| ERP-U-161 | Supabase Question Classification | every question has a category that maps to a license_category |
| ERP-U-162 | Supabase Question Classification | every question has a theme that maps to Supabase theme column |
| ERP-U-163 | Supabase Question Classification | no professional categories exist in question data |
| ERP-U-164 | Supabase Question Classification | question data shape is compatible with exam_questions table |

</details>

<details><summary><b>ExamQuestionsManagerPage</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-165 | ExamQuestionsManagerPage | renders without crashing |

</details>

<details><summary><b>examQuestionsTranslation</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-166 | Exam Questions Translation Validation | should have english translations for all questions |

</details>

<details><summary><b>examSimulatorRepro</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-167 | H1 — tema desconhecido vindo da BD | o tema mapeado existe em THEME_INFO |
| ERP-U-168 | H1 — tema desconhecido vindo da BD | THEME_INFO[q.theme].color (ELearningView.tsx:691) não rebenta |
| ERP-U-169 | H2 — correctAnswer desalinhado das opções | (a) buraco nas chaves (A,C) + correct_option C: índice existe no array |
| ERP-U-170 | H2 — correctAnswer desalinhado das opções | (b) correct_option nulo não marca silenciosamente a opção A |
| ERP-U-171 | H2 — correctAnswer desalinhado das opções | (b) letra inválida não marca silenciosamente a opção A |
| ERP-U-172 | H2 — correctAnswer desalinhado das opções | (c) options_en mais curto: índice correto existe também em inglês |

</details>

<details><summary><b>extrairColunas</b> · 2 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-173 | extrairTabelas | lê as colunas e a nulabilidade |
| ERP-U-174 | extrairTabelas | ignora o bloco Insert |

</details>

<details><summary><b>FinancialPage</b> · 19 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-175 | FinancialPage — fluxo de caixa e entradas de alunos | mostra o mês corrente no cabeçalho em vez de uma data fixa |
| ERP-U-176 | FinancialPage — fluxo de caixa e entradas de alunos | mostra o fluxo de caixa do dia e do mês, só com transações pagas |
| ERP-U-177 | FinancialPage — fluxo de caixa e entradas de alunos | conta inscrições por dia, semana e mês, pela data do 1.º pagamento |
| ERP-U-178 | FinancialPage — fluxo de caixa e entradas de alunos | não expõe os totais globais da escola |
| ERP-U-179 | FinancialPage — navegação de datas do resumo | recua um dia e recalcula fluxo de caixa e alunos |
| ERP-U-180 | FinancialPage — navegação de datas do resumo | o botão Hoje repõe o dia corrente |
| ERP-U-181 | FinancialPage — navegação de datas do resumo | avisa quando o dia escolhido é anterior aos dados carregados |
| ERP-U-182 | FinancialPage — navegação de datas do resumo | não permite navegar para o futuro |
| ERP-U-183 | FinancialPage — lista de alunos novos | abre no mês e mostra as pessoas por trás do contador |
| ERP-U-184 | FinancialPage — lista de alunos novos | o período escolhido manda na lista, e bate certo com o contador |
| ERP-U-185 | FinancialPage — lista de alunos novos | clicar num aluno abre a ficha dele |
| ERP-U-186 | FinancialPage — lista de alunos novos | sem ninguém no período, o botão não promete uma lista vazia |
| ERP-U-187 | FinancialPage — lista de alunos novos | a lista respeita os filtros da tabela, como o contador |
| ERP-U-188 | FinancialPage — a tabela é só de pagamentos | não lança a contratação como linha, mas usa-a para nomear o pagamento |
| ERP-U-189 | FinancialPage — a tabela é só de pagamentos | não oferece criar transações a partir daqui |
| ERP-U-190 | FinancialPage — a tabela é só de pagamentos | não oferece Produto/Serviço no filtro de tipo |
| ERP-U-191 | FinancialPage — os filtros da tabela também mandam nos cartões | o filtro de escola corta o fluxo de caixa e as entradas de alunos |
| ERP-U-192 | FinancialPage — os filtros da tabela também mandam nos cartões | marca os cartões como filtrados para não se lerem como totais da escola |
| ERP-U-193 | FinancialPage — os filtros da tabela também mandam nos cartões | um filtro só do movimento mexe na caixa mas deixa as inscrições em paz |

</details>

<details><summary><b>FinancialPageLoading</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-194 | FinancialPage — dados por chegar | nunca afirma 0 quando os dados ainda não chegaram |
| ERP-U-195 | FinancialPage — dados por chegar | conta as inscrições sem esperar pelo carregamento completo de alunos |
| ERP-U-196 | FinancialPage — dados por chegar | agrupa a navegação rápida entre dias num só pedido |
| ERP-U-197 | FinancialPage — dados por chegar | diz que falhou em vez de ficar a carregar para sempre |
| ERP-U-198 | FinancialPage — dados por chegar | não mostra o aviso de janela quando ainda não há dados para julgar |

</details>

<details><summary><b>financialSummary</b> · 19 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-199 | weekStart | devolve a segunda-feira da semana |
| ERP-U-200 | weekStart | atravessa a fronteira do mês |
| ERP-U-201 | addDays | anda para a frente e para trás |
| ERP-U-202 | addDays | atravessa mês e ano |
| ERP-U-203 | cashFlow | separa entradas de saídas no dia e no mês |
| ERP-U-204 | cashFlow | ignora pendente e atrasado — não é dinheiro em caixa |
| ERP-U-205 | cashFlow | não deixa o estado do contrato mexer na caixa |
| ERP-U-206 | cashFlow | conta os pagamentos dos alunos, que é o que é caixa |
| ERP-U-207 | cashFlow | aceita timestamps ISO e valores em string sem rebentar |
| ERP-U-208 | intakeWindowStart | normalmente é o início do mês |
| ERP-U-209 | intakeWindowStart | recua para o mês anterior quando a semana abre lá |
| ERP-U-210 | intakeWindowStart | nunca deixa de fora um dia que a contagem da semana precisa |
| ERP-U-211 | newStudents | conta dia, semana e mês |
| ERP-U-212 | newStudents | não conta datas futuras |
| ERP-U-213 | newStudents | ignora entradas sem data |
| ERP-U-214 | newStudents | aceita timestamp e fica-se pela parte da data |
| ERP-U-215 | newStudents | conta a semana que atravessa a fronteira do mês |
| ERP-U-216 | pendingSplit | separa a receber de a pagar em vez de somar tudo |
| ERP-U-217 | monthLabel | formata o mês em português |

</details>

<details><summary><b>htaccessStaticFallback</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-218 | .htaccess — 404 para ficheiro estático em falta | a regra ainda existe no ficheiro |
| ERP-U-219 | .htaccess — 404 para ficheiro estático em falta | apanha os chunks com hash, a origem do ecrã em branco |
| ERP-U-220 | .htaccess — 404 para ficheiro estático em falta | apanha os restos do PWA que os telemóveis antigos ainda pedem |
| ERP-U-221 | .htaccess — 404 para ficheiro estático em falta | não apanha as rotas da app — senão ninguém recebe o index.html |
| ERP-U-222 | .htaccess — 404 para ficheiro estático em falta | só apanha a extensão no fim, não no meio do caminho |

</details>

<details><summary><b>index</b> · 22 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-223 | option validation | disallow async and errback handler together |
| ERP-U-224 | option validation | disallow missing sync handler |
| ERP-U-225 | option validation | errback callback required |
| ERP-U-226 | generator function metadata | automatic naming |
| ERP-U-227 | generator function metadata | explicit naming |
| ERP-U-228 | generator function metadata | default arity |
| ERP-U-229 | generator function metadata | explicit arity |
| ERP-U-230 | 'sync' handler | success |
| ERP-U-231 | 'sync' handler | failure |
| ERP-U-232 | gensync(function\* () {}) | sync throw before body |
| ERP-U-233 | gensync(function\* () {}) | sync throw inside body |
| ERP-U-234 | gensync(function\* () {}) | async throw inside body |
| ERP-U-235 | gensync(function\* () {}) | error inside body |
| ERP-U-236 | gensync(function\* () {}) | successful return value |
| ERP-U-237 | gensync(function\* () {}) | successful final value |
| ERP-U-238 | gensync(function\* () {}) | yield unexpected object |
| ERP-U-239 | gensync(function\* () {}) | yield suspend yield |
| ERP-U-240 | gensync(function\* () {}) | yield suspend return |
| ERP-U-241 | gensync.all() | error first |
| ERP-U-242 | gensync.all() | error last |
| ERP-U-243 | gensync.all() | empty list |
| ERP-U-244 | gensync.race() | error |

</details>

<details><summary><b>lessonNumbering</b> · 13 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-245 | findMainContract | prefere o contrato com pack/inicial no nome |
| ERP-U-246 | findMainContract | sem pack/inicial, cai no mais caro |
| ERP-U-247 | findMainContract | devolve null sem contratos |
| ERP-U-248 | isEventForContract | a aula fica na contratação guardada, não no contrato principal |
| ERP-U-249 | isEventForContract | aula sem contratação vai para o contrato principal |
| ERP-U-250 | isEventForContract | reconhece o formato legado [Contratação: N] |
| ERP-U-251 | isEventForContract | reconhece o formato legado JSON cobalt_contract_id |
| ERP-U-252 | isEventForContract | não rebenta com JSON inválido na descrição |
| ERP-U-253 | eventsForContract | numera 1..N dentro de cada contratação, por ordem cronológica |
| ERP-U-254 | eventsForContract | a numeração de uma contratação não conta as aulas da outra |
| ERP-U-255 | resolveContractForEvent | devolve a contratação guardada na aula |
| ERP-U-256 | resolveContractForEvent | devolve o contrato principal quando a aula não tem contratação |
| ERP-U-257 | resolveContractForEvent | devolve null quando o aluno não tem contratos |

</details>

<details><summary><b>mod13Generator</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-258 | generateMod13 | compacta telefone, NIF e código postal para caberem nos campos do IMT |
| ERP-U-259 | generateMod13 | tira o acento às letras que a fonte não tem, mantém o português |
| ERP-U-260 | generateMod13 | o que não há forma de escrever ou de caber fica visível ou em branco, sem partir o PDF |

</details>

<details><summary><b>paymentSync</b> · 8 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-261 | buildPaymentUpsertRow | NEVER writes student_product_id (bulk save must not clobber associations) |
| ERP-U-262 | buildPaymentUpsertRow | preserves the core payment fields and keeps a valid id |
| ERP-U-263 | buildPaymentUpsertRow | generates an id when the payment has a non-uuid id |
| ERP-U-264 | mapDbPaymentToRecord | PRESERVES student_product_id (the list view dropped it → payments showed unassociated) |
| ERP-U-265 | mapDbPaymentToRecord | maps a null association to undefined, not a falsy string |
| ERP-U-266 | mapDbPaymentToRecord | carries the core fields through |
| ERP-U-267 | withAssociation | overrides the stale association the DB read brings back |
| ERP-U-268 | withAssociation | clears the association when set to null |

</details>

<details><summary><b>pdfContractGenerator.retake</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-269 | getCorrectPracticalHours — practical exam-retake ("Repetição de Exame Prático") lesson counts | detects ONLY practical retake products by name (theory excluded) |
| ERP-U-270 | getCorrectPracticalHours — practical exam-retake ("Repetição de Exame Prático") lesson counts | Categoria B practical retake → 8 lessons (not the full-course 32) |
| ERP-U-271 | getCorrectPracticalHours — practical exam-retake ("Repetição de Exame Prático") lesson counts | Motos (Categoria A) practical retake → 3 lessons |
| ERP-U-272 | getCorrectPracticalHours — practical exam-retake ("Repetição de Exame Prático") lesson counts | CE/C/D practical retakes → 4 lessons |
| ERP-U-273 | getCorrectPracticalHours — practical exam-retake ("Repetição de Exame Prático") lesson counts | exam-THEORY retakes are NOT given the practical-retake count (fall through to normal logic) |
| ERP-U-274 | getCorrectPracticalHours — practical exam-retake ("Repetição de Exame Prático") lesson counts | KNOWN LIMITATION: a practical-retake name with no category token falls to 4 (would be wrong for a B product) |
| ERP-U-275 | getCorrectPracticalHours — practical exam-retake ("Repetição de Exame Prático") lesson counts | resolves every real practical-retake product to the correct count |
| ERP-U-276 | getCorrectPracticalHours — practical exam-retake ("Repetição de Exame Prático") lesson counts | every real exam-THEORY retake product is excluded |
| ERP-U-277 | getCorrectPracticalHours — practical exam-retake ("Repetição de Exame Prático") lesson counts | full-course products are unchanged |

</details>

<details><summary><b>precoContratado</b> · 7 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-278 | contractedPrice | devolve o valor gravado na contratacao |
| ERP-U-279 | contractedPrice | um zero gravado e zero, nao um vazio que cai noutro preco |
| ERP-U-280 | contractedPrice | sem valor gravado vale zero -- nunca o preco do catalogo |
| ERP-U-281 | contractedPrice | aceita o numeric do Postgres, que chega como string |
| ERP-U-282 | contractedPrice | lixo na coluna nao vira NaN a somar num total |
| ERP-U-283 | contractedPrice | regressao 04/08/2026: o catalogo subir nao mexe no contrato de Junho |
| ERP-U-284 | contractedPrice | o total a pagar soma os valores contratados, nao os do catalogo |

</details>

<details><summary><b>priceComposition</b> · 35 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-285 | sumComposition | soma e arredonda a dois decimais |
| ERP-U-286 | sumComposition | trata valores em falta como zero em vez de NaN |
| ERP-U-287 | getCompositionTemplate — estrutura | Categoria B inicial abre com inscrição de 125€ e fecha com exame prático de 80€ |
| ERP-U-288 | getCompositionTemplate — estrutura | cursos em inglês usam inscrição de 300€ |
| ERP-U-289 | getCompositionTemplate — estrutura | nome só em inglês não é reconhecido como carta — a inscrição de 300€ nunca chega a aplicar-se |
| ERP-U-290 | getCompositionTemplate — estrutura | não inventa composição para produtos que não são carta |
| ERP-U-291 | getCompositionTemplate — estrutura | nunca devolve parcelas negativas mesmo com preço abaixo dos custos fixos |
| ERP-U-292 | description ↔ composição (o ciclo que apagava dados) | grava e volta a ler sem perder nada |
| ERP-U-293 | description ↔ composição (o ciclo que apagava dados) | sobrevive a um segundo guardar — era aqui que a composição desaparecia |
| ERP-U-294 | description ↔ composição (o ciclo que apagava dados) | produto sem composição não ganha lixo no texto |
| ERP-U-295 | description ↔ composição (o ciclo que apagava dados) | composição sem texto descritivo funciona à mesma |
| ERP-U-296 | description ↔ composição (o ciclo que apagava dados) | JSON corrompido não leva o texto atrás |
| ERP-U-297 | description ↔ composição (o ciclo que apagava dados) | ignora um [COMP] que não seja um array |
| ERP-U-298 | reconcileCompositionToTotal — total e parcelas nunca divergem | sem desconto nem quantidade, não mexe em nada |
| ERP-U-299 | reconcileCompositionToTotal — total e parcelas nunca divergem | NUNCA escreve "desconto" numa parcela |
| ERP-U-300 | reconcileCompositionToTotal — total e parcelas nunca divergem | o caso da aluna X: 5% sai da formação prática, taxas ficam intactas |
| ERP-U-301 | reconcileCompositionToTotal — total e parcelas nunca divergem | quantidade escala parcelas e horas |
| ERP-U-302 | reconcileCompositionToTotal — total e parcelas nunca divergem | quantidade e desconto ao mesmo tempo |
| ERP-U-303 | reconcileCompositionToTotal — total e parcelas nunca divergem | desconto maior que a maior parcela transborda para a seguinte, sem negativos |
| ERP-U-304 | reconcileCompositionToTotal — total e parcelas nunca divergem | valor acima do template acresce à maior parcela |
| ERP-U-305 | reconcileCompositionToTotal — total e parcelas nunca divergem | não cria ruído por cêntimos de arredondamento |
| ERP-U-306 | reconcileCompositionToTotal — total e parcelas nunca divergem | composição vazia continua vazia — não inventa parcelas |
| ERP-U-307 | reconcileCompositionToTotal — total e parcelas nunca divergem | não altera o array recebido |
| ERP-U-308 | contractedPrice | devolve o valor gravado na contratacao |
| ERP-U-309 | contractedPrice | zero gravado e zero, nao "em falta" |
| ERP-U-310 | contractedPrice | sem valor gravado nao inventa nenhum |
| ERP-U-311 | contractedPrice | aceita a string numerica que o Postgres devolve para numeric |
| ERP-U-312 | contractedPrice | so olha para a contratacao — o catalogo nao entra na conta |
| ERP-U-313 | resolveComposition | a composicao gravada manda |
| ERP-U-314 | resolveComposition | sem composicao gravada cai no template IMT, nao nos racios do contrato |
| ERP-U-315 | resolveComposition | categoria A leva a rubrica do modulo teorico especifico |
| ERP-U-316 | resolveComposition | composicao vazia conta como nao gravada |
| ERP-U-317 | resolveComposition | C+E conta como CE, nao como C |
| ERP-U-318 | resolveComposition | categoria C pura continua no template de pesados C |
| ERP-U-319 | resolveComposition | produto que nao e carta fica sem composicao |

</details>

<details><summary><b>safeStorage</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-320 | SafeStorage | should store and retrieve values normally when storage works |
| ERP-U-321 | SafeStorage | should fallback to in-memory storage if localStorage throws |
| ERP-U-322 | SafeStorage | should handle removeItem gracefully when storage throws |

</details>

<details><summary><b>storageUrl</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-323 | storagePath | extrai o path de um URL público |
| ERP-U-324 | storagePath | extrai o path de um URL assinado, sem a query |
| ERP-U-325 | storagePath | descodifica o path |
| ERP-U-326 | storagePath | devolve null para outro bucket ou URL externo |

</details>

<details><summary><b>studentCard</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-327 | findContentBounds | encontra o cartão no canto de uma folha em branco |
| ERP-U-328 | findContentBounds | devolve null numa página totalmente branca |
| ERP-U-329 | findContentBounds | ignora cinzento muito claro (ruído de digitalização), não o conteúdo real |
| ERP-U-330 | findContentBounds | abrange todo o conteúdo quando este toca as bordas |
| ERP-U-331 | isImageCard | aceita imagens (upload manual, auto-sync e cobalt legacy) |
| ERP-U-332 | isImageCard | rejeita PDFs por mime-type ou extensão, em qualquer um dos campos |
| ERP-U-333 | isImageCard | não confunde "pdf" no meio do nome com a extensão |
| ERP-U-334 | isImageCard | rejeita cartões vazios |
| ERP-U-335 | isImageCard | deixa o portal escolher o JPG mesmo quando o PDF vem primeiro |

</details>

<details><summary><b>studentCardView</b> · 12 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-336 | extractPath | usa o path guardado quando existe |
| ERP-U-337 | extractPath | extrai o path de um URL público do bucket |
| ERP-U-338 | extractPath | extrai o path de um URL assinado, sem a query |
| ERP-U-339 | extractPath | devolve null para um URL externo |
| ERP-U-340 | extractDirectUrl | aceita um URL externo (cartões legacy do [legacy system]) |
| ERP-U-341 | extractDirectUrl | rejeita blob: — gravações falhadas antigas que dariam imagem partida |
| ERP-U-342 | extractDirectUrl | rejeita URLs do bucket, que têm de ir por signed URL |
| ERP-U-343 | extractDirectUrl | ignora o blob: e fica com o URL externo quando ambos existem |
| ERP-U-344 | legendaDoCartao | tira a extensão e o NIF do início, deixando o que distingue |
| ERP-U-345 | legendaDoCartao | não mexe num nome que já não tem NIF |
| ERP-U-346 | legendaDoCartao | devolve vazio quando não há nome |
| ERP-U-347 | legendaDoCartao | não come um número curto que faça parte do nome |

</details>

<details><summary><b>studentPortalTranslations</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-348 | Portal do aluno — traduções | encontra as chaves nos ficheiros (senão o teste não prova nada) |
| ERP-U-349 | Portal do aluno — traduções | en, fr e es têm exatamente as mesmas chaves, e todas as de pt |
| ERP-U-350 | Portal do aluno — traduções | as {variáveis} de cada texto são as mesmas em todas as línguas |

</details>

<details><summary><b>studentProductSync</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| ERP-U-351 | mapDbProductToStudentProduct | keeps quantity, theory_hours and practical_hours |
| ERP-U-352 | mapDbProductToStudentProduct | defaults quantity to 1 when the column is null |
| ERP-U-353 | mapDbProductToStudentProduct | maps the remaining persisted columns |
| ERP-U-354 | mapDbProductToStudentProduct | resolves the instructor name from the caller |
| ERP-U-355 | parseProductNotes | splits composition out of notes |
| ERP-U-356 | parseProductNotes | leaves plain notes untouched and tolerates broken json |

</details>
<!-- catalog:erp:end -->

[← Back to the portfolio](../../README.md)
