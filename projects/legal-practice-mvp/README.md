# Legal practice management MVP

An MVP for a law office: clients and entities, cases with conflict-of-interest checks, deadlines, an agenda and internal notes per case.

**Stack:** React 19 · Vite · Supabase · **Test tooling:** Vitest (happy-dom; coverage thresholds of 70% for statements, lines and functions, 60% for branches) · Testing Library

## What I did

- Built the MVP and unit-tested the parts where small mistakes become legal risk: deadline dates and form validation.

## Highlights

- **LEG-U-004**: a date reads back as the date that was written, with no off-by-one day caused by time zones.
- **LEG-U-003**: an end time earlier than the start time is refused.
- **LEG-U-002**: the tax ID is either empty or exactly nine digits.

## Catalogue

Test titles are kept in their original language (Portuguese). Client and product names are anonymized.

<!-- catalog:legal:start -->
**8 test cases** · 0 end-to-end · 8 unit & integration

#### Unit & integration

<details><summary><b>form</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| LEG-U-001 | helpers de formulário do MVP | normaliza campos opcionais vazios |
| LEG-U-002 | helpers de formulário do MVP | aceita NIF vazio ou com nove dígitos |
| LEG-U-003 | helpers de formulário do MVP | impede uma hora final anterior à inicial |

</details>

<details><summary><b>formatters</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| LEG-U-004 | datas ancoradas ao meio-dia local | não recua um dia — o dia lido é o dia escrito |
| LEG-U-005 | datas ancoradas ao meio-dia local | aceita também o formato timestamptz |
| LEG-U-006 | datas ancoradas ao meio-dia local | conta dias de calendário a partir do dia local |
| LEG-U-007 | datas ancoradas ao meio-dia local | a hora do dia não altera a contagem |
| LEG-U-008 | datas ancoradas ao meio-dia local | descreve o prazo em português |

</details>
<!-- catalog:legal:end -->

[← Back to the portfolio](../../README.md)
