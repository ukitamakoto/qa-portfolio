# Urban Scooter: courier Android app

A TripleTen QA Engineer Bootcamp project. In the courier app, couriers log in and see two tabs: "All orders" (not yet accepted) and "My orders". From there they can pull to refresh, sort by delivery date with overdue orders on top, filter by metro station, and accept and complete orders.

## What I tested

The order list, the order cards (short and full versions), the station filter, accepting and completing orders, login and logout, and persistence after the app is killed. Everything ran on the Android Studio emulator, with test data created through the app's API.

- **Techniques:** requirement-based test design, state checks across tabs, negative cases (invalid login, empty states).
- **Evidence:** screenshots of the key screens and of the defects (gallery below).

**35 test cases** · 20 passed · 7 failed · 8 inconclusive

- [Test cases](test-cases.md)

### Evidence gallery

Screenshots reviewed one by one. They are shown by what they prove, not linked to case IDs.

| | | |
|---|---|---|
| ![My orders: empty state](screenshots/TC-01_meus_pedidos.png)<br>My orders: empty state | ![All orders: the overdue order is on top, with a red border](screenshots/TC-02_refresh.png)<br>All orders: the overdue order is on top, with a red border | ![Full card: name, surname, phone and scooter colour](screenshots/TC-05_detalhes_pedido.png)<br>Full card: name, surname, phone and scooter colour |
| ![Metro-station filter](screenshots/TC-07_filtro_estacao.png)<br>Metro-station filter | ![Accepting an order: confirmation dialog](screenshots/TC-10_aceitar_pedido.png)<br>Accepting an order: confirmation dialog | ![Logging out: confirmation dialog](screenshots/TC-14_logout.png)<br>Logging out: confirmation dialog |
| ![Defect: crash (KotlinNullPointerException) when the My orders tab renders](screenshots/TC-18_botao_concluir.png)<br>Defect: crash (KotlinNullPointerException) when the My orders tab renders | ![Defect: rotating to landscape leaves a blank screen](screenshots/TC-25_landscape.png)<br>Defect: rotating to landscape leaves a blank screen | ![Invalid login: error message](screenshots/TC-26_login_invalido.png)<br>Invalid login: error message |
| ![Forgot password: "Contact the manager: 0101"](screenshots/TC-27_esqueci_senha.png)<br>Forgot password: "Contact the manager: 0101" | ![Backend URL setting for the test environment](screenshots/TC-29_popup_api.png)<br>Backend URL setting for the test environment | ![Defect: after the app is killed, stations show "Unknown" and an HTTP 404 appears](screenshots/TC-32_persistencia_killed.png)<br>Defect: after the app is killed, stations show "Unknown" and an HTTP 404 appears |

Cases are in Portuguese, as written during the bootcamp.

[← Back to the portfolio](../../README.md)
