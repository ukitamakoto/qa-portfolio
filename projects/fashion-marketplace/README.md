# Local fashion marketplace with a live virtual fitting room

A marketplace where local shops publish their catalogue and customers browse by proximity. A live virtual fitting room shows the clothes on the customer through a real-time video-generation API, paid with credits.

**Stack:** Next.js 16 (App Router) · React 19 · TypeScript · Supabase · **Test tooling:** Playwright (mobile and desktop projects) · Vitest (unit and integration)

## What I did

- Built the product together with its test suites.
- Covered the three roles end to end (customer, shop owner, administrator): what each one can see and do, and what each one must not reach.
- Tested the money paths: credits, refunds when the video API fails, the shop ledger and the commission limits.
- Wrote integration tests against the API routes, as well as browser tests on a phone-sized and a desktop viewport.

## Test strategy

| Level | Tool | What it covers |
|---|---|---|
| End-to-end | Playwright: a setup project plus mobile and desktop projects, traces kept on failure | Search, filters, shop and product pages, roles, the fitting-room flow |
| Unit & integration | Vitest | Business rules in `lib`, API routes (fitting room start/finish/refund, scheduled jobs), admin actions |

## Highlights

- **MKT-E2E-003**: search ignores accents ("calca" finds "calça").
- **MKT-E2E-044**: when the video API fails before generating, the credit is refunded and the customer is told.
- **MKT-E2E-001**: a regular customer cannot reach the admin area.
- **MKT-U-008**: the admin can grant fitting-room credits with a ledger, and the balance never goes negative.

## Catalogue

Test titles are kept in their original language (English or Portuguese). Client and product names are anonymized.

<!-- catalog:marketplace:start -->
**221 test cases** · 54 end-to-end · 167 unit & integration

#### End-to-end

| ID | Suite | Scenario |
|---|---|---|
| MKT-E2E-001 | cliente comum | não encontra a área de admin |
| MKT-E2E-002 | cliente comum | admin aprova a loja, lança provas e suspende |
| MKT-E2E-003 | busca | busca sem acento acha a calça |
| MKT-E2E-004 | busca | buscar pelo cabeçalho |
| MKT-E2E-005 | busca | filtro de tamanho esconde quem está esgotado nele |
| MKT-E2E-006 | busca | parâmetros inválidos são ignorados sem erro |
| MKT-E2E-007 | busca | busca sem resultado mostra mensagem |
| MKT-E2E-008 | busca | "Ver mais" traz as próximas peças sem perder o filtro |
| MKT-E2E-009 | busca | busca sozinha 3 segundos depois da última tecla |
| MKT-E2E-010 | busca | buscar pelo cabeçalho mantém os filtros já escolhidos |
| MKT-E2E-011 | compra | peça de outra loja pergunta antes de trocar a sacola |
| MKT-E2E-012 | compra | fechar pedido pede login |
| MKT-E2E-013 | logado | compra completa: sacola, pagamento, a loja entrega, o cliente devolve |
| MKT-E2E-014 | entrar | senha errada mostra aviso |
| MKT-E2E-015 | entrar | voltar para outro site é ignorado depois do login |
| MKT-E2E-016 | logado | mostra a conta e permite sair |
| MKT-E2E-017 | favoritos | sem login, favoritar leva para /entrar e guarda o caminho de volta |
| MKT-E2E-018 | logado | favorita na página da peça, vê em Favoritos e desfavorita |
| MKT-E2E-019 | logado | Favoritos pede login |
| MKT-E2E-020 | inicio | apresenta o provador com transparência sobre câmera e gravação |
| MKT-E2E-021 | inicio | mostra lojas próximas, marca só retirada e lista produtos |
| MKT-E2E-022 | inicio | sem localização vai para /localizacao |
| MKT-E2E-023 | inicio | cookie corrompido vai para /localizacao |
| MKT-E2E-024 | com permissão de localização | salva a localização e volta ao início |
| MKT-E2E-025 | com permissão de localização | permissão negada mostra aviso e mantém o CEP |
| MKT-E2E-026 | com permissão de localização | CEP inválido mostra erro |
| MKT-E2E-027 | loja-produto | página da loja lista só os produtos dela |
| MKT-E2E-028 | loja-produto | produto mostra preço, tamanhos e esgotado |
| MKT-E2E-029 | loja-produto | produto com duas cores troca os tamanhos |
| MKT-E2E-030 | loja-produto | loja pendente, loja inexistente e produto inválido dão 404 |
| MKT-E2E-031 | loja-produto | loja e produto têm cabeçalho com busca, mesmo sem endereço definido |
| MKT-E2E-032 | lojista | cadastra a loja e ela fica em análise |
| MKT-E2E-033 | lojista | cadastro com dado errado aponta o campo e mantém o que foi digitado |
| MKT-E2E-034 | lojista | cria uma peça com foto e duas variações |
| MKT-E2E-035 | lojista | ativa o provador da peça com a imagem enviada, e recusa imagem pequena |
| MKT-E2E-036 | lojista | arquivo com erro mostra a linha e não importa nada |
| MKT-E2E-037 | lojista | importa um arquivo válido e as peças entram na lista |
| MKT-E2E-038 | lojista | a vitrine só mostra a loja depois de aprovada |
| MKT-E2E-039 | medidas | cliente novo passa pela tela de medidas ao entrar e pode deixar para depois |
| MKT-E2E-040 | logado | medidas viram tamanho e a busca passa a mostrar só o que serve |
| MKT-E2E-041 | logado | apagar as medidas desliga o filtro |
| MKT-E2E-042 | provador | loja sem crédito: avisa, solta a câmera e permite tentar de novo |
| MKT-E2E-043 | provador | toque duplo em Abrir câmera inicia uma vez só |
| MKT-E2E-044 | provador | [video API] falha antes de gerar: pede o estorno e avisa |
| MKT-E2E-045 | provador | voltar enquanto a câmera abre: não chama o servidor e desliga a câmera |
| MKT-E2E-046 | provador-api | sem login responde 401 |
| MKT-E2E-047 | logado | entrega token [video API], prompt e marca, e debita 1 crédito |
| MKT-E2E-048 | logado | peça sem provador e id inválido respondem 404 |
| MKT-E2E-049 | provador-botao | peça com foto de provador mostra o botão; sem foto, não |
| MKT-E2E-050 | provador-botao | sem login, provar leva para /entrar e guarda o caminho de volta |
| MKT-E2E-051 | logado | abre a orientação da prova |
| MKT-E2E-052 | logado | peça sem provador ou id inválido dá 404 |
| MKT-E2E-053 | provador-camera-negada | câmera negada avisa e não chama o servidor (nenhum crédito debitado) |
| MKT-E2E-054 | pwa | manifesto instalável com ícones PNG |

#### Unit & integration

<details><summary><b>admin</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-001 | lerLancamento | pacote vendido e ajuste somam; retirada subtrai |
| MKT-U-002 | lerLancamento | recusa quantidade que não é inteiro de 1 a 10000, tipo desconhecido e loja inválida |
| MKT-U-003 | lerComissao | aceita de 0 a 50, com vírgula ou ponto |
| MKT-U-004 | lerComissao | recusa fora da faixa ou texto |

</details>

<details><summary><b>admin.int</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-005 | quem não é admin | não lista lojas, não aprova, não lança provas, não mexe na comissão e não vê o resumo |
| MKT-U-006 | admin | vê as lojas com o contato do dono, pendentes primeiro |
| MKT-U-007 | admin | aprova, suspende e reativa; a vitrine acompanha |
| MKT-U-008 | admin | lança provas com extrato e nunca deixa o saldo negativo |
| MKT-U-009 | admin | o dono vê o extrato da própria loja; outra conta não |
| MKT-U-010 | admin | resumo traz os números e a comissão só aceita de 0 a 50 |

</details>

<details><summary><b>auth</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-011 | destinoSeguro | aceita caminhos do próprio site |
| MKT-U-012 | destinoSeguro | recusa outros sites e valores vazios |
| MKT-U-013 | mensagemErroAuth | traduz os erros conhecidos do Supabase |
| MKT-U-014 | mensagemErroAuth | tem mensagem genérica para o resto |

</details>

<details><summary><b>catalogo</b> · 13 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-015 | lerFiltros | aceita filtros válidos |
| MKT-U-016 | lerFiltros | descarta valores inválidos ou vazios |
| MKT-U-017 | lerFiltros | usa o primeiro valor quando o parâmetro vem repetido |
| MKT-U-018 | lerFiltros | ignora preço fora das opções e caractere nulo na busca |
| MKT-U-019 | lerFiltros | "meu tamanho" vale por padrão e só a URL com meu=0 desliga |
| MKT-U-020 | lerFiltros | limita o texto da busca a 100 caracteres |
| MKT-U-021 | lerQuantidade | mostra 40 peças quando ninguém pediu mais |
| MKT-U-022 | lerQuantidade | aceita o pedido de mais peças até o teto de 200 |
| MKT-U-023 | camposDosFiltros | devolve os filtros com o nome que a URL usa, sem os vazios |
| MKT-U-024 | camposDosFiltros | volta ao mesmo filtro quando a URL gerada é lida de novo |
| MKT-U-025 | ordemTamanho | ordena do menor para o maior e deixa desconhecidos no fim |
| MKT-U-026 | corInicial | começa pela primeira cor que ainda tem estoque |
| MKT-U-027 | corInicial | sem estoque nenhum, fica com a primeira cor |

</details>

<details><summary><b>catalogo.int</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-028 | lojas_proximas | lista quem entrega, marca só retirada e esconde distantes e pendentes |
| MKT-U-029 | buscar_produtos | acha "calca" sem acento |
| MKT-U-030 | buscar_produtos | gênero inclui peças unissex |
| MKT-U-031 | buscar_produtos | infantil não recebe unissex adulto |
| MKT-U-032 | buscar_produtos | filtro de tamanho só considera variações com estoque |
| MKT-U-033 | buscar_produtos | filtro de preço máximo |
| MKT-U-034 | buscar_produtos | nunca mostra produto de loja distante ou pendente |
| MKT-U-035 | RLS | visitante não enxerga loja pendente nem por consulta direta |
| MKT-U-036 | RLS | visitante não consegue criar loja |

</details>

<details><summary><b>cep</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-037 | normalizarCep | aceita hífen, pontos e espaços |
| MKT-U-038 | normalizarCep | rejeita tamanho errado |
| MKT-U-039 | buscarCep | usa as coordenadas da BrasilAPI quando existem |
| MKT-U-040 | buscarCep | cai no Nominatim quando a BrasilAPI vem sem coordenadas |
| MKT-U-041 | buscarCep | retorna null para CEP inexistente, inválido ou sem rede |
| MKT-U-042 | buscarCep | retorna null quando o Nominatim também não acha |

</details>

<details><summary><b>compra.int</b> · 13 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-043 | criar_pedido | calcula tudo pelo banco e soma a variação repetida |
| MKT-U-044 | criar_pedido | entrega cobra a taxa dentro do raio e recusa fora dele |
| MKT-U-045 | criar_pedido | recusa estoque insuficiente, quantidade inválida, peça inexistente, contato ruim e visitante |
| MKT-U-046 | criar_pedido | peça de loja fora do ar não é vendida |
| MKT-U-047 | pagamento | confirmar baixa o estoque uma vez só, mesmo chamado de novo |
| MKT-U-048 | pagamento | se o estoque acabou antes de pagar, o pedido é recusado, estornado e nada é baixado |
| MKT-U-049 | pagamento | só o dono do pedido paga ou cancela, e cancelar só vale antes de pagar |
| MKT-U-050 | loja | avança na ordem certa; fora de ordem ou por outra conta é recusado |
| MKT-U-051 | loja | recusar devolve o estoque e estorna |
| MKT-U-052 | loja | cliente e loja veem o pedido com os itens; outra conta e visitante não; ninguém grava direto |
| MKT-U-053 | devolução e prazos | cliente pede até 7 dias depois da entrega; a loja aprova, o estoque volta e o valor é estornado |
| MKT-U-054 | devolução e prazos | depois de 7 dias da entrega não dá mais para devolver |
| MKT-U-055 | devolução e prazos | a rotina cancela quem não pagou em 30 min e recusa, com estorno, o que a loja não aceitou em 15 |

</details>

<details><summary><b>conta.int</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-056 | favoritos | cada cliente vê só os próprios e pode desfavoritar |
| MKT-U-057 | favoritos | ninguém favorita em nome de outra conta, nem visitante |
| MKT-U-058 | medidas | ficam visíveis e editáveis só para o dono |
| MKT-U-059 | medidas | o banco recusa medida fora da faixa |
| MKT-U-060 | buscar_produtos com "meu tamanho" | esconde a peça sem estoque no tamanho do cliente e mantém as que servem |
| MKT-U-061 | buscar_produtos com "meu tamanho" | sem pedir o filtro, sem medidas ou sem login, mostra tudo |

</details>

<details><summary><b>dinheiro</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-062 | formatarBRL | converte centavos para reais no padrão brasileiro |
| MKT-U-063 | paraCentavos | entende o jeito brasileiro de escrever preço |
| MKT-U-064 | paraCentavos | entende ponto decimal e milhar sem vírgula |
| MKT-U-065 | paraCentavos | recusa o que não é preço |

</details>

<details><summary><b>gravacao</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-066 | formatoDeVideo | prefere MP4 (abre na galeria do iPhone) e cai para WebM |
| MKT-U-067 | formatoDeVideo | null quando o navegador não grava nada |
| MKT-U-068 | nomeArquivoVideo | monta o nome sem acentos nem símbolos, com a extensão do formato |
| MKT-U-069 | desenharMarca | escreve o nome da loja e "via [marketplace]" no canto inferior esquerdo |
| MKT-U-070 | desenharMarca | usa o logo quando existe |

</details>

<details><summary><b>importacao</b> · 8 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-071 | lerCsv | descobre o separador pelo cabeçalho |
| MKT-U-072 | lerCsv | respeita aspas, com separador, quebra de linha e aspas dentro do campo |
| MKT-U-073 | lerCsv | ignora BOM, linhas vazias e fim de linha do Windows |
| MKT-U-074 | decodificar | lê UTF-8 e cai para Windows-1252 no arquivo do Excel |
| MKT-U-075 | montarImportacao | junta as linhas da mesma peça e normaliza os valores |
| MKT-U-076 | montarImportacao | aponta a linha e o motivo de cada erro, e não devolve item nenhum |
| MKT-U-077 | montarImportacao | recusa arquivo sem as colunas obrigatórias, vazio ou grande demais |
| MKT-U-078 | montarImportacao | aceita cabeçalho com acento, maiúscula e colunas em outra ordem |

</details>

<details><summary><b>localizacao</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-079 | parseLocalizacao | lê um cookie válido |
| MKT-U-080 | parseLocalizacao | trata ausente, lixo e coordenadas impossíveis como sem localização |
| MKT-U-081 | parseLocalizacao | corta rótulo gigante |

</details>

<details><summary><b>loja</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-082 | slugDe | tira acento, espaço e símbolo |
| MKT-U-083 | slugDe | nunca devolve vazio nem passa de 50 letras |
| MKT-U-084 | lerLoja | lê um cadastro válido já no formato do banco |
| MKT-U-085 | lerLoja | aponta cada campo errado com uma mensagem |
| MKT-U-086 | lerLoja | aceita CPF, entrega grátis e loja sem retirada |
| MKT-U-087 | imagemDaLoja | aceita só arquivo da pasta da própria loja no Storage |

</details>

<details><summary><b>lojista.int</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-088 | loja | nasce pendente e sem créditos, e só o dono enxerga |
| MKT-U-089 | loja | o dono não se aprova, não mexe no saldo e não abre segunda loja |
| MKT-U-090 | loja | o dono edita o perfil; outra conta não |
| MKT-U-091 | peças | salvar_produto cria, edita e troca as variações |
| MKT-U-092 | peças | quem não tem loja não grava, e ninguém mexe na peça de outra loja |
| MKT-U-093 | peças | importação com uma linha ruim não grava nada; a boa grava tudo |
| MKT-U-094 | peças | peça de loja pendente não aparece para o público; aprovada, aparece |
| MKT-U-095 | provador | o dono liga o provador da peça, e o botão só vale com a loja aprovada e com provas |
| MKT-U-096 | fotos | o lojista envia e apaga só na pasta da própria loja |

</details>

<details><summary><b>medidas</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-097 | tamanhosDasMedidas | modelagem feminina: letra pelo busto e número pelo maior entre cintura e quadril |
| MKT-U-098 | tamanhosDasMedidas | modelagem masculina: letra pelo tórax e número pela cintura |
| MKT-U-099 | tamanhosDasMedidas | os limites de cada faixa pertencem ao tamanho menor |
| MKT-U-100 | tamanhosDasMedidas | acima da tabela fica no maior tamanho vendido |
| MKT-U-101 | tamanhosDasMedidas | sem modelagem ou sem a medida, não chuta tamanho |
| MKT-U-102 | lerMedidas | lê o formulário e ignora campos vazios |
| MKT-U-103 | lerMedidas | descarta valores fora da faixa ou que não estão nas opções |
| MKT-U-104 | lerMedidas | arredonda centímetros quebrados |
| MKT-U-105 | rotuloTamanhos | junta só os tamanhos conhecidos |

</details>

<details><summary><b>pagamento</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-106 | provedor simulado | Pix devolve um código para copiar; cartão devolve o link de pagamento |

</details>

<details><summary><b>pedido</b> · 7 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-107 | etapasDoPedido | mostra o caminho de entrega ou de retirada |
| MKT-U-108 | ACOES_DA_LOJA | só oferece o que o banco aceita em cada status |
| MKT-U-109 | podeDevolver | só pedido entregue há menos de 7 dias |
| MKT-U-110 | lerCheckout | lê uma retirada válida no formato de criar_pedido |
| MKT-U-111 | lerCheckout | entrega exige CEP e endereço |
| MKT-U-112 | lerCheckout | recusa sacola vazia ou adulterada, contato curto e opção inexistente |
| MKT-U-113 | mensagemDoPedido | traduz os erros do banco e tem uma genérica |

</details>

<details><summary><b>produto</b> · 7 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-114 | normalizadores | aceitam o jeito que o lojista escreve |
| MKT-U-115 | normalizadores | devolvem null para o que não existe no catálogo |
| MKT-U-116 | lerProduto | lê uma peça válida já no formato de salvar_produto |
| MKT-U-117 | lerProduto | exige ao menos uma variação e recusa repetida |
| MKT-U-118 | lerProduto | recusa preço zerado, foto que não é https e mais de 5 fotos |
| MKT-U-119 | lerProduto | recusa estoque negativo ou quebrado |
| MKT-U-120 | lerProduto | peça desmarcada como ativa fica fora da vitrine |

</details>

<details><summary><b>provador</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-121 | promptDaPeca | usa o termo certo para cada tipo de peça |
| MKT-U-122 | códigos de erro | reconhece os erros do banco e trata o resto como falha de conexão |
| MKT-U-123 | códigos de erro | mapeia status HTTP |
| MKT-U-124 | códigos de erro | tem mensagem em português para cada código e uma genérica |

</details>

<details><summary><b>provador.int</b> · 12 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-125 | visitante | vê só sim/não do provador, nunca o saldo |
| MKT-U-126 | visitante | não consegue iniciar prova |
| MKT-U-127 | saldo só muda pelas funções do banco | cliente logado não consegue alterar créditos nem criar loja |
| MKT-U-128 | iniciar_prova | debita 1 crédito, registra a sessão e o extrato, devolve a peça |
| MKT-U-129 | iniciar_prova | sem crédito: erro sem_credito e o botão some |
| MKT-U-130 | iniciar_prova | duas provas simultâneas com 1 crédito: exatamente uma passa |
| MKT-U-131 | iniciar_prova | duas abas do mesmo cliente não debitam duas vezes e a conclusão libera uma nova prova |
| MKT-U-132 | iniciar_prova | peça sem foto de provador: indisponivel, nada debitado |
| MKT-U-133 | iniciar_prova | limite de 10 provas por dia; estornadas não contam |
| MKT-U-134 | estornar_prova | devolve o crédito uma vez só |
| MKT-U-135 | estornar_prova | não estorna depois de gerar, depois de 2 minutos, nem sessão de outro cliente |
| MKT-U-136 | estornar_prova | no máximo 3 estornos por dia |

</details>

<details><summary><b>requisicao</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-137 | protecoes das rotas JSON | aceita a origem configurada e rejeita outra origem, inclusive same-site |
| MKT-U-138 | protecoes das rotas JSON | aceita cliente HTTP sem metadados de navegador, mas rejeita contexto cross-site |
| MKT-U-139 | protecoes das rotas JSON | exige application/json e limita o corpo |

</details>

<details><summary><b>route</b> · 14 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-140 | GET /api/cron/tick | aplica os prazos dos pedidos e não deixa a resposta em cache |
| MKT-U-141 | GET /api/cron/tick | com CRON_SECRET configurado, só aceita quem manda o segredo |
| MKT-U-142 | GET /api/cron/tick | responde 502 quando o banco falha, para o cron registrar o erro |
| MKT-U-143 | POST /api/provador/estornar | pede o estorno ao banco com a sessão do cliente |
| MKT-U-144 | POST /api/provador/estornar | sem login ou com id inválido não chama o banco |
| MKT-U-145 | POST /api/provador/estornar | rejeita origem externa antes de chamar o banco |
| MKT-U-146 | POST /api/provador/estornar | diferencia falha tecnica de estorno recusado pela regra |
| MKT-U-147 | POST /api/provador/finalizar | finaliza a sessao do cliente sem permitir cache |
| MKT-U-148 | POST /api/provador/finalizar | rejeita origem externa antes de consultar a sessao |
| MKT-U-149 | POST /api/provador/finalizar | responde 502 quando o banco nao confirma a finalizacao |
| MKT-U-150 | POST /api/provador/iniciar | [video API] fora do ar: falha_conexao sem debitar crédito |
| MKT-U-151 | POST /api/provador/iniciar | com token, debita e devolve a prova |
| MKT-U-152 | POST /api/provador/iniciar | erro do banco depois do token: repassa o código |
| MKT-U-153 | POST /api/provador/iniciar | rejeita origem externa antes de criar token ou consultar o banco |

</details>

<details><summary><b>sacola</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-154 | sacola | soma a quantidade quando a mesma variação entra de novo |
| MKT-U-155 | sacola | peça de outra loja começa uma sacola nova |
| MKT-U-156 | sacola | quantidade vai de 1 a 20; zero tira a peça e a última esvazia a sacola |
| MKT-U-157 | sacola | lê do armazenamento do navegador sem confiar no que está lá |

</details>

<details><summary><b>sessao-provador</b> · 10 cases</summary>

| ID | Suite | Case |
|---|---|---|
| MKT-U-158 | antes do servidor | abrir vai para preparando; abrir de novo é ignorado (toque duplo) |
| MKT-U-159 | antes do servidor | câmera negada: erro, solta a câmera, sem estorno (nada foi debitado) |
| MKT-U-160 | antes do servidor | servidor recusou: erro com o código, sem estorno |
| MKT-U-161 | antes do servidor | servidor aprovou: conectando e começa a esperar a geração |
| MKT-U-162 | antes do servidor | fechar enquanto prepara: cancela; se o servidor responder depois, estorna |
| MKT-U-163 | conectando | primeira geração: ao vivo, marca, conta o tempo e grava |
| MKT-U-164 | ao vivo | gerando de novo (reconexão) não reinicia nada |
| MKT-U-165 | ao vivo | espera de geração vencida depois de gerar é ignorada |
| MKT-U-166 | estados finais | fim e erro ignoram eventos atrasados e reiniciam com reiniciar |
| MKT-U-167 | estados finais | fechar na orientação não faz nada (desmontagem do React em dev) |

</details>
<!-- catalog:marketplace:end -->

[← Back to the portfolio](../../README.md)
