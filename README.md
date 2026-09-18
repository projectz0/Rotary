# Rotary Club Feira de Santana — Controle de Assiduidade

Documentação de referência do projeto. Ano Rotário 2026/27. Objetivo: controlar a presença dos sócios nas reuniões semanais (terças-feiras) para apurar, ao fim do ano, quem será bonificado por assiduidade.

- **Site publicado:** https://frequenciarotaryfsa.com.br/ (domínio próprio, ativo desde 18/08/2026; link antigo https://projectz0.github.io/Rotary/ continua funcionando como backup)
- **Repositório GitHub:** https://github.com/projectz0/Rotary (owner `projectz0`, público)
- **Pasta de trabalho local:** `C:\CONTROLADORIA\Claude - Projetos\Rotary`

---

## 1. Diretoria (exibida no cabeçalho do site)

- **Presidente:** Bruno de Nunes Silva
- **1º Secretário:** José Carlos Rodrigues

---

## 2. Regra de pontuação

| Situação | Pontos | Conta como falta? |
|---|---|---|
| Presente (assinou a lista) | 1 ponto | Não |
| Ausente com falta justificada (marcou "Sim" no campo Falta Justificada) | 1 ponto | Não |
| Ausente sem justificativa | 0 ponto | Sim |

O ranking é a soma de pontos no período. Sócios marcados com **(\*)** são "dispensados de frequência" pela regra estatutária do clube (**Idade + Tempo de Rotary ≥ 85 anos**) — mas pontuam pela mesma regra de todo mundo; a marcação é só informativa.

---

## 3. Como ler cada lista de frequência

**Mudança de processo a partir de agosto/2026 (decisão do Jefferson, 18/09/2026):** cada reunião agora gera **duas versões** da lista de frequência:

- **Lista "Checada"** (ex.: `Lista de frequência 04-08 - Checada.pdf`) — a pessoa que coleta as assinaturas pinta com **marca-texto amarelo** o nome de quem esteve presente, exatamente para tirar a ambiguidade das assinaturas pequenas/grandes/sobrepostas. **Essa é a lista que o Claude usa para ler presença/falta.** Fica arquivada só internamente, em `conferencia-interna/lista-presenca-checada/` — **nunca é publicada no site nem sobe pro GitHub**.
- **Lista pública** (ex.: `Lista de frequência 04-08.pdf`, sem marca-texto) — cópia limpa, é a que fica disponível no site em `documentos/lista-presenca/`.

Processo obrigatório ao ler uma lista Checada nova:

1. Listar **todas** as linhas da lista (não pular nenhuma, mesmo as óbvias) — presente, ausente justificado, ausente.
2. **Presença = nome pintado com marca-texto.** Não usar mais a assinatura como critério de leitura — só o marca-texto conta (decisão tomada depois de mais de um erro de leitura por assinatura/marca-texto sobrepostos nas primeiras tentativas de agosto).
3. Coluna "Falta Justificada? ( ) Sim ( ) Não" é **sempre soberana** sobre o marca-texto: se "Sim" estiver marcado, o código é AJ mesmo que o nome esteja pintado como presente (aconteceu em mais de um caso em agosto — o "Sim" reflete que a pessoa avisou falta justificada, mesmo que quem pintou tenha pintado por engano).
4. Reportar o resultado completo pro Jefferson conferir com a lista física, **data por data** (não mandar as 4-5 datas do mês de uma vez), antes de consolidar na planilha mestre. Toda correção do Jefferson é a fonte da verdade — a leitura do Claude é só um rascunho a ser validado.

---

## 4. Roster (quadro social)

Total atual: **50 sócios** (a lista original de 07/07/2026 tinha 52; Reginaldo Caribé de Araújo e Ricardo de Souza Santos foram removidos por só aparecerem nessa primeira lista e não constarem nas seguintes — decisão do Jefferson).

**Sócios dispensados (\*):** 15 no total, ligados à nota de rodapé "Idade + Tempo de Rotary = ou + 85 anos".

### Nomes canônicos (grafias diferentes entre listas — mesma pessoa)

| Nome canônico adotado | Grafia alternativa vista |
|---|---|
| Albertony Santos Assis | "Albertony Santos SSSIS - Tony" (1ª lista) |
| Antônio José de Carvalho Monteiro | "...- Toni" (1ª lista) |
| Roseli Rodrigues da Silva | "...de Jesus - Rose" (1ª lista) |
| Maria Clécia Vasconcelos | "Maria Clécia V. de M. F. Costa" (1ª lista) — confirmado com o Jefferson que é a mesma pessoa |

---

## 5. Estrutura de arquivos na pasta do projeto

```
Rotary/
├── index.html                          → site (dashboard de ranking)
├── assets/
│   └── rotary-wheel.png                → logo do Rotary (recortada de imagem enviada pelo Jefferson, fundo transparente)
├── documentos/                         → só o que é público / sobe pro site
│   ├── lista-presenca/                 → lista de frequência limpa (sem marca-texto) de cada reunião
│   │   ├── 2026-07-07.pdf ... 2026-07-28.pdf
│   │   └── 2026-08-04.pdf ... 2026-08-25.pdf
│   └── ata-reuniao/                    → ata oficial (registro/minuta) de cada reunião
│       ├── 2026-07-07.pdf ... 2026-07-28.pdf
│       └── 2026-08-04.pdf ... 2026-08-25.pdf   (todas as 4 datas recebidas)
├── conferencia-interna/
│   └── lista-presenca-checada/         → listas COM marca-texto, uso interno do Claude só pra ler presença.
│                                          NUNCA sobe pro GitHub/site (ver seção 3).
└── Rotary_Frequencia_Mestre.xlsx       → planilha mestre (histórico completo + fórmulas)
```

Estrutura **flat** (sem subpasta por mês) — decisão confirmada com o Jefferson em 18/09/2026 ("Opção A"): todo mês novo, os PDFs entram direto em `documentos/lista-presenca/` e `documentos/ata-reuniao/` no padrão `AAAA-MM-DD.pdf`, sem criar pasta `Agosto - 26/` etc. Isso mantém o mesmo padrão que já estava valendo pro site desde julho.

Cada reunião tem **dois documentos-fonte públicos**, guardados com o mesmo nome de arquivo em pastas separadas: a lista de presença (a versão limpa, sem marca-texto — usada só pra visualização, não pra apurar presença) e a ata oficial da reunião (registro do que foi discutido). No site, os dois ficam disponíveis numa aba própria "Atas e Listas de Presença" (acima do ranking, expande igual a um card de sócio) — uma linha por data, com os dois documentos lado a lado. Isso evita repetir os mesmos links em todos os 50 cards de sócio quando "Expandir tudo" é usado; o card de cada sócio mostra só o status visual (presente/falta/justificada) por data.

> Pasta antiga `atas/` (usada até 17/08/2026) e os PDFs duplicados soltos na raiz do projeto (cópias antigas de antes da correção do nome do Presidente/Ruy Sandes) foram apagados em 18/09/2026, depois de confirmar que o site não referenciava nenhum deles (só lê de `documentos/lista-presenca/` e `documentos/ata-reuniao/`). A foto `WhatsApp Image 2026-08-14 at 13.07.09.jpeg` foi mantida a pedido do Jefferson.

A planilha mestre é o **arquivo único e cumulativo do ano** — não se cria um arquivo novo por mês. A cada mês novo, adicionam-se colunas de data novas nela (aba "Frequência"), preservando o histórico e o total de pontos acumulado. A aba "Legenda" documenta os códigos (P / AJ / A / -) e as decisões já tomadas com o Jefferson.

**Atenção — dado sensível:** a ata de 07/07 (eleição e posse do conselho) contém CPF, RG e endereço residencial completo de vários diretores. Por decisão explícita do Jefferson (17/08/2026), o arquivo foi publicado como está, mesmo sabendo que o site/repositório é público. Se algum diretor pedir remoção, o arquivo precisa ser substituído por uma versão com esses campos tarjados antes.

---

## 6. Site (index.html)

- Mobile-first, com modo claro/escuro (toggle manual + segue o sistema).
- Cabeçalho: logo, nome do clube, "Controle de Assiduidade · Ano Rotário 26/27", diretoria, tagline "Crie Impacto Duradouro".
- 3 cartões de estatística: reuniões realizadas, % de presença média do clube, sócios empatados na liderança (não mostra "um líder" sozinho, pois normalmente há empate).
- Título do ranking é dinâmico ("Ranking · até julho/2026") — calculado a partir do mês da última reunião no array `MEETINGS`. Quando agosto e os meses seguintes forem adicionados, o título se atualiza sozinho, sem precisar editar texto manualmente.
- Busca por nome, ignora acentuação (buscar "jose" encontra "José").
- Botões "Expandir tudo" / "Recolher tudo".
- Cada card de sócio, ao expandir, mostra só o status visual por data (Presente/Justificada/Falta) — sem links de documento, pra não poluir quando "Expandir tudo" é usado.
- Aba "Atas e Listas de Presença" (acima do ranking, mesmo estilo expansível dos cards): uma linha por data de reunião, com os botões "📋 Lista de Presença" e "📝 Ata da Reunião" lado a lado, cada um abrindo o PDF em nova aba.
- Dados dos sócios ficam embutidos no próprio HTML (array `MEMBERS` no `<script>`), sem backend — é um site 100% estático.
- Paleta de cores segue a skill de dataviz interna (cores validadas para acessibilidade / daltonismo).

### Pendente de decisão (falado com o Jefferson em 17/08/2026)

- **Unificar lista de presença + ata num único PDF por reunião?** Ainda em aberto — por enquanto os dois documentos continuam separados (`lista-presenca/` e `ata-reuniao/`).
- **Seletor de mês/período**: hoje só existe julho, então não há seletor. Quando agosto entrar (2º mês de dados), avaliar como fica a navegação — opções a considerar: abas por mês, dropdown de período, ou manter tudo num ranking acumulado único com filtro opcional por mês. Decisão a tomar quando chegar a hora.

---

## 7. Fluxo de atualização mensal

1. Jefferson coloca na pasta de agosto/mês corrente: a ata oficial + **as duas versões** da lista de frequência (Checada com marca-texto, e a limpa/pública) de cada reunião do mês.
2. Claude lê **uma data por vez**, a partir da lista Checada (ver seção 3 — marca-texto manda, "Falta Justificada: Sim" sempre sobrepõe o marca-texto), e reporta pro Jefferson conferir antes de passar pra próxima data.
3. Jefferson corrige o que estiver errado. Só depois de **todas** as datas do mês confirmadas, Claude consolida.
4. Claude atualiza:
   - `Rotary_Frequencia_Mestre.xlsx`: novas colunas de data na aba Frequência (`build_roster.py` recriado/reexecutado com os novos códigos, depois validado com `recalc.py` — zero erros de fórmula).
   - `index.html`: novas entradas no array `MEETINGS` (label + caminho do PDF de lista pública + ata) e novos códigos no array `MEMBERS`, um por sócio.
   - Move os PDFs recebidos pro padrão flat `AAAA-MM-DD.pdf` em `documentos/lista-presenca/` (versão pública, sem marca-texto) e `documentos/ata-reuniao/`; a versão Checada de cada data vai pra `conferencia-interna/lista-presenca-checada/` e **nunca** é enviada ao GitHub.
   - `README.md`: registra a data de fechamento do mês na seção 8.
5. Claude salva tudo na pasta local do Jefferson (`C:\CONTROLADORIA\Claude - Projetos\Rotary`) via ponte com o computador.
6. Claude sobe as mudanças direto no GitHub, usando o navegador do Jefferson já autenticado (sem precisar de token nem senha) — envia os arquivos pela tela de upload do repositório e confirma o commit. **Nunca envia arquivos da pasta `conferencia-interna/`.**
7. GitHub Pages faz o redeploy automático (leva 1-2 minutos). Claude confere o link ao vivo antes de avisar que terminou.

---

## 8. Decisões e histórico de ajustes

- 07/07/2026: primeira lista veio sem a coluna "Falta Justificada" preenchida em 5 linhas (irregularidade pontual daquela lista, não um padrão).
- Regra de falta justificada ajustada: conta como presença (1 ponto), não como neutro.
- Reginaldo Caribé de Araújo e Ricardo de Souza Santos: removidos do quadro e do ranking (só apareciam na lista de 07/07).
- Avisos de "assinatura fraca/marca pequena" (usados só como conferência interna durante a leitura) foram removidos do site e da planilha depois de validados com o Jefferson — não aparecem mais pro público.
- 17/08/2026: Eliana Mattos de Amorim Bueno (falta justificada, doença) — listas de 14/07 e 21/07 substituídas pelas versões corretas enviadas pelo Jefferson; código dela mudou de A (falta) para AJ (falta justificada) nas duas datas na planilha e no site (2 pts → 4 pts, 100% presença).
- 17/08/2026: adicionadas as 4 atas oficiais das reuniões (documento distinto da lista de presença) — site passou a mostrar os dois documentos por data lado a lado, cada um com seu ícone.
- 18/08/2026: cabeçalho ajustado (Presidente/Secretário em negrito com quebra de linha, tagline do tamanho do título, cores pretas nos nomes) e círculos de posição 1º/2º/3º (dourado/prata/bronze) removidos do ranking, já que empates são comuns e não há critério de desempate — não faz sentido sugerir "pódio".
- 18/08/2026: os links de documento (Lista de Presença / Ata da Reunião) saíram de dentro de cada card de sócio — como se repetiam nos 50 cards, ficava poluído ao clicar "Expandir tudo". Agora moram numa aba própria "Atas e Listas de Presença", acima do ranking, que expande igual a um card e lista as 4 datas com os dois documentos cada uma. O card de sócio voltou a mostrar só o status visual por data.
- 18/08/2026: domínio próprio `frequenciarotaryfsa.com.br` configurado (comprado pelo Jefferson no Registro.br). DNS: 4 registros A apontando pro GitHub Pages (185.199.108/109/110/111.153) + CNAME `www` → `projectz0.github.io.`, cadastrados no painel do Registro.br. GitHub Pages: domínio customizado ativado em Settings → Pages, "DNS check successful" e "Enforce HTTPS" habilitado. Propagação levou algumas horas (normal para domínio recém-registrado) — durante a espera, o domínio customizado precisou ser removido e reconfigurado uma vez no GitHub, porque configurá-lo antes do DNS propagar fazia o GitHub redirecionar até o link antigo (`projectz0.github.io/Rotary/`) para o domínio novo, quebrando os dois links ao mesmo tempo. Site testado e confirmado funcionando no domínio próprio.
- 18/08/2026: nome do Presidente corrigido de "Bruno Nunes Silva" para "Bruno de Nunes Silva" (grafia correta) — atualizado no cabeçalho do site, no card dele no ranking e neste README.
- 18/08/2026: Ruy Sandes Leal Junior corrigido de falta (A) para presente (P) em 28/07 — confirmado pelo Jefferson que ele esteve na última reunião (a 07/07 dele já estava correta como presente).
- 18/09/2026: **Importação de agosto (04/08, 11/08, 18/08, 25/08) fechada.** Pontos principais:
  - Limpeza de arquivos: apagados 8 PDFs duplicados soltos na raiz e a pasta `atas/` obsoleta inteira (16 arquivos no total), depois de confirmar via GitHub que o site não referenciava nenhum deles. Pastas `Julho - 26/` dentro de `documentos/` foram achatadas (removida a subpasta, arquivos foram pro nível de `documentos/lista-presenca/` e `documentos/ata-reuniao/` direto) para manter o padrão flat que já valia desde julho — confirmado com o Jefferson como "Opção A".
  - **Novo processo de leitura com marca-texto** instituído a partir de agosto (detalhado na seção 3): a pessoa que coleta assinaturas agora pinta o nome de quem esteve presente na lista "Checada", que fica só de uso interno em `conferencia-interna/lista-presenca-checada/` — nunca sobe pro site. A lista pública (sem marca-texto) é a que fica em `documentos/lista-presenca/`.
  - A leitura de agosto passou por 3 rodadas de correção do Jefferson (erros do Claude leram marca-texto errado em Alpiniano Reis Oliveira Filho em 04/08, em Jolival Alves Soares e José Rosa Figueiredo Filho em 18/08, e o caso de Paulo Barreto dos Santos em 18/08 onde o marca-texto estava errado por engano de quem pintou) — todas as 4 datas foram fechadas linha a linha com confirmação explícita do Jefferson antes de consolidar na planilha e no site.
  - Regra confirmada: quando "Falta Justificada: Sim" está marcado, o sócio é AJ (não conta falta, soma ponto) independentemente do marca-texto estar pintado ou não — o "Sim" é sempre soberano.
  - Ata da reunião de 11/08 estava pendente (aguardando terceiros) e foi recebida e publicada em 18/09/2026 — as 4 atas de agosto estão completas no site.
