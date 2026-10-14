# Websites: rural guesthouse, scenography studio, sports club

Three client websites. Each one ships its own automated checks, aimed at the parts that break quietly: data, content rules, exports and accessibility.

Test titles are kept in their original language (English or Portuguese). Client and product names are anonymized.

## Rural guesthouse website

A multilingual site (5 languages) with every piece of content editable in an admin area, including an events agenda and a guest-data export.
**Stack:** React 19 · Vite · Tailwind · PHP admin · **Test tooling:** `node:test`, PHP test runner

- **WEB-GH-U-005**: the CSV export quotes cells, separates them with `;` and neutralizes spreadsheet formulas (CSV injection).
- **WEB-GH-U-002**: a departure date earlier than the arrival date is swapped instead of producing a negative stay.

<!-- catalog:guesthouse:start -->
**38 test cases** · 0 end-to-end · 38 unit & integration

#### Unit & integration

<details><summary><b>agenda</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-GH-U-001 | agenda | events overlapping the stay, sorted by start |
| WEB-GH-U-002 | agenda | a departure before the arrival is swapped |
| WEB-GH-U-003 | agenda | an end date before the start date counts as a one-day event |
| WEB-GH-U-004 | agenda | empty dates show nothing; dates cross months and years |

</details>

<details><summary><b>csv</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-GH-U-005 | csv | quotes cells, separates with ; and neutralizes formulas |

</details>

<details><summary><b>format</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-GH-U-006 | format | fill replaces known placeholders only |
| WEB-GH-U-007 | format | formatDate is a calendar day in every language |
| WEB-GH-U-008 | format | tel and mail links |
| WEB-GH-U-009 | format | long titles may wrap after a slash |

</details>

<details><summary><b>load</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-GH-U-010 | load | seed only when there is no live file |
| WEB-GH-U-011 | load | live over seed |
| WEB-GH-U-012 | load | fields added by a newer seed survive an older live file |
| WEB-GH-U-013 | load | an HTML fallback page counts as a missing file |
| WEB-GH-U-014 | load | server errors and a missing seed fail loudly |

</details>

<details><summary><b>merge</b> · 2 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-GH-U-015 | merge | live objects override key by key; lists and scalars replace |
| WEB-GH-U-016 | merge | null or missing live keeps the seed |

</details>

<details><summary><b>model</b> · 12 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-GH-U-017 | model | Pedidos de estadias canceladas deixam de estar ativos |
| WEB-GH-U-018 | model | Noites e valores em mudanças de mês, ano e horário de verão |
| WEB-GH-U-019 | model | Reserva recusa datas impossíveis, passadas, invertidas, excessivas e ocupação inválida |
| WEB-GH-U-020 | model | Perfil reutilizável exige cinco campos válidos |
| WEB-GH-U-021 | model | Estado corrompido ou parcialmente incompatível não é aceite |
| WEB-GH-U-022 | model | Primeiros domingos dentro da estadia, na virada do mês e sem nenhum |
| WEB-GH-U-023 | model | Sugestões seguem os interesses e as datas da estadia |
| WEB-GH-U-024 | model | Capacidade real por unidade |
| WEB-GH-U-025 | model | Estado v1 migra para v2 sem perder dados; lixo é recusado |
| WEB-GH-U-026 | model | Interesses, ocasião e pedidos inválidos são recusados |
| WEB-GH-U-027 | model | Pedido de experiência só dentro de uma estadia ativa |
| WEB-GH-U-028 | model | Cenário inicial: a próxima estadia inclui um 1.º domingo e o mercado vem primeiro |

</details>

<details><summary><b>site</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-GH-U-029 | site | Cada imagem referida no conteúdo existe |
| WEB-GH-U-030 | site | Cores da marca com contraste AA para texto e botões |
| WEB-GH-U-031 | site | Logo, fontes e fotos existem; fotos somam no máximo 3 MB |

</details>

<details><summary><b>slugify</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-GH-U-032 | slugify | titles become journal addresses |

</details>

<details><summary><b>structure</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-GH-U-033 | structure | every unit slug is its id without the room- prefix (the sitemap relies on it) |
| WEB-GH-U-034 | structure | the booking URL filters the unit; without a unit it opens the engine |
| WEB-GH-U-035 | structure | 8 units, every group has units |
| WEB-GH-U-036 | structure | isGroupSlug accepts only known groups |
| WEB-GH-U-037 | structure | [venue] is /[venue] and what is under it, nothing else |
| WEB-GH-U-038 | structure | the next unit follows the site order and wraps round to the first |

</details>
<!-- catalog:guesthouse:end -->

## Scenography studio website

An editorial portfolio site with pre-rendered HTML on every route. The projects are data, validated before every build.
**Stack:** React 19 · Vite · GSAP · Tailwind · **Test tooling:** `node:test` on the content validators

- **WEB-SC-U-006**: an image with empty alt text is rejected.
- **WEB-SC-U-002**: duplicate project slugs are rejected.

<!-- catalog:scenography:start -->
**43 test cases** · 0 end-to-end · 43 unit & integration

#### Unit & integration

<details><summary><b>content</b> · 10 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SC-U-001 | content | projeto válido não produz erros |
| WEB-SC-U-002 | content | rejeita slug duplicado |
| WEB-SC-U-003 | content | rejeita slug fora de kebab-case |
| WEB-SC-U-004 | content | rejeita projeto sem imagens |
| WEB-SC-U-005 | content | rejeita quando a primeira imagem não é a capa |
| WEB-SC-U-006 | content | rejeita alt vazio |
| WEB-SC-U-007 | content | rejeita ratio fora do conjunto |
| WEB-SC-U-008 | content | rejeita papel fora do conjunto |
| WEB-SC-U-009 | content | rejeita texto com menos de 150 palavras |
| WEB-SC-U-010 | content | acumula vários erros do mesmo projeto |

</details>

<details><summary><b>jsonld</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SC-U-011 | jsonld | organizacao é ProfessionalService com NAP e redes |
| WEB-SC-U-012 | jsonld | listaProjetos é ItemList com uma posição por projeto |
| WEB-SC-U-013 | jsonld | obraProjeto é CreativeWork com local e data |
| WEB-SC-U-014 | jsonld | obraProjeto.about tem um Thing por entrada de escopo |
| WEB-SC-U-015 | jsonld | obraProjeto.creator aponta para o mesmo @id de organizacao |
| WEB-SC-U-016 | jsonld | obraProjeto.image ignora imagens sem src e absolutiza as demais |
| WEB-SC-U-017 | jsonld | obraProjeto omite image quando nenhuma imagem tem src |
| WEB-SC-U-018 | jsonld | breadcrumb numera a partir de 1 |
| WEB-SC-U-019 | jsonld | faqPage mapeia pergunta e resposta |

</details>

<details><summary><b>jsonld-rotas</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SC-U-020 | jsonld-rotas | home: só organização |
| WEB-SC-U-021 | jsonld-rotas | /projetos: organização + ItemList + BreadcrumbList, nessa ordem |
| WEB-SC-U-022 | jsonld-rotas | /projetos/&lt;slug&gt;: organização + CreativeWork + BreadcrumbList, nessa ordem |
| WEB-SC-U-023 | jsonld-rotas | /contato: organização + FAQPage, nessa ordem |
| WEB-SC-U-024 | jsonld-rotas | rota desconhecida: só organização |
| WEB-SC-U-025 | jsonld-rotas | slug de projeto inexistente: não produz CreativeWork nem rebenta |

</details>

<details><summary><b>llms</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SC-U-026 | llms | começa pelo título do site em h1 |
| WEB-SC-U-027 | llms | inclui o NAP completo |
| WEB-SC-U-028 | llms | lista cada rota estática com url absoluta |
| WEB-SC-U-029 | llms | lista cada projeto com url, ano, local e resumo |
| WEB-SC-U-030 | llms | nenhum projeto fica de fora |
| WEB-SC-U-031 | llms | rota /projetos/&lt;slug&gt; em "rotas" não duplica o projeto; /projetos (índice) continua em "Páginas" |

</details>

<details><summary><b>montar-pagina</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SC-U-032 | montar-pagina | esc escapa &, &lt; e " mas não outros caracteres (nem "&gt;") |
| WEB-SC-U-033 | montar-pagina | substituir troca todas as ocorrências do alvo |
| WEB-SC-U-034 | montar-pagina | substituir não trata $& no valor como "insere o match" |
| WEB-SC-U-035 | montar-pagina | substituir não trata $$, $` nem $' no valor como padrões especiais |
| WEB-SC-U-036 | montar-pagina | montarPagina preenche os seis marcadores |
| WEB-SC-U-037 | montar-pagina | montarPagina: sem preload, __PRELOAD__ some sem deixar rasto; com preload, a tag aparece no &lt;head&gt; |

</details>

<details><summary><b>sitemap</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SC-U-038 | sitemap | declara xml e urlset |
| WEB-SC-U-039 | sitemap | inclui uma url por rota, sem barra final na raiz |
| WEB-SC-U-040 | sitemap | usa a data fornecida |
| WEB-SC-U-041 | sitemap | a raiz tem prioridade mais alta que as restantes |
| WEB-SC-U-042 | sitemap | rota de projeto (/projetos/&lt;slug&gt;) tem prioridade 0.8 |
| WEB-SC-U-043 | sitemap | rota /projetos (índice, não é rota de projeto) tem prioridade 0.6 |

</details>
<!-- catalog:scenography:end -->

## Sports-club class schedule

A club website whose weekly class timetable is checked like data, plus colour-contrast and link checks.
**Stack:** Astro · Tailwind · **Test tooling:** `node:test`

- **WEB-SP-U-006**: the pool never hosts two classes at the same time.
- **WEB-SP-U-004**: no class ends after the club closes (21:30).

<!-- catalog:sports-club:start -->
**31 test cases** · 0 end-to-end · 31 unit & integration

#### Unit & integration

<details><summary><b>aulas</b> · 8 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SP-U-001 | aulas | todas as horas estão em HH:MM de 24 horas |
| WEB-SP-U-002 | aulas | todos os dias e locais são válidos |
| WEB-SP-U-003 | aulas | a duração respeita a regra do mapa oficial |
| WEB-SP-U-004 | aulas | nenhuma aula acaba depois das 21:30 (fecho do clube) |
| WEB-SP-U-005 | aulas | não há duplicados exatos |
| WEB-SP-U-006 | aulas | a piscina não tem duas coisas ao mesmo tempo |
| WEB-SP-U-007 | aulas | há aulas em todos os dias de segunda a sábado |
| WEB-SP-U-008 | aulas | o mapa tem as 57 linhas transcritas |

</details>

<details><summary><b>site</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SP-U-009 | site | as chaves de rota são únicas |
| WEB-SP-U-010 | site | os caminhos PT são únicos |
| WEB-SP-U-011 | site | os caminhos EN são únicos |
| WEB-SP-U-012 | site | todo o caminho EN vive sob /en |
| WEB-SP-U-013 | site | nenhum caminho termina em barra, exceto a raiz |
| WEB-SP-U-014 | site | caminhoAlternativo é uma involução |
| WEB-SP-U-015 | site | caminhoAlternativo rejeita caminhos fora do mapa |
| WEB-SP-U-016 | site | rotaPorChave rejeita chaves desconhecidas |
| WEB-SP-U-017 | site | localeDoCaminho não confunde /english com /en/ |

</details>

<details><summary><b>textos</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SP-U-018 | textos | PT e EN têm exatamente a mesma forma |
| WEB-SP-U-019 | textos | nenhuma string está vazia |
| WEB-SP-U-020 | textos | nenhuma tradução EN ficou igual ao português por esquecimento |
| WEB-SP-U-021 | textos | as modalidades apontam para rotas que existem |
| WEB-SP-U-022 | textos | cada item da navegação tem rótulo nos dois idiomas |
| WEB-SP-U-023 | textos | a política de privacidade tem corpo nos dois idiomas |

</details>

<details><summary><b>videos</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SP-U-024 | videos | os nove vídeos locais existem e têm tamanho adequado para web |
| WEB-SP-U-025 | videos | todos os vídeos têm legenda nos dois idiomas |
| WEB-SP-U-026 | videos | identificadores de vídeo são únicos |

</details>

<details><summary><b>whatsapp</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| WEB-SP-U-027 | whatsapp | usa o domínio wa.me e o número internacional sem sinais |
| WEB-SP-U-028 | whatsapp | sem assunto, a mensagem é genérica em português |
| WEB-SP-U-029 | whatsapp | com assunto, a mensagem incorpora o assunto |
| WEB-SP-U-030 | whatsapp | em inglês muda a mensagem |
| WEB-SP-U-031 | whatsapp | caracteres acentuados e & são codificados |

</details>
<!-- catalog:sports-club:end -->

[← Back to the portfolio](../../README.md)
