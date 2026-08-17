# Rotary Club Feira de Santana — Controle de Assiduidade

Documentação de referência do projeto. Ano Rotário 2026/27. Objetivo: controlar a presença dos sócios nas reuniões semanais (terças-feiras) para apurar, ao fim do ano, quem será bonificado por assiduidade.

- **Site publicado:** https://projectz0.github.io/Rotary/
- **Repositório GitHub:** https://github.com/projectz0/Rotary (owner `projectz0`, público)
- **Pasta de trabalho local:** `C:\CONTROLADORIA\Claude - Projetos\Rotary`

---

## 1. Diretoria (exibida no cabeçalho do site)

- **Presidente:** Bruno Nunes Silva
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

## 3. Como ler cada ata (lista de frequência)

Cada ata tem: nome do sócio, coluna de assinatura e coluna "Falta Justificada? ( ) Sim ( ) Não".

Processo obrigatório ao ler uma ata nova:

1. Listar **todas** as linhas da lista (não pular nenhuma, mesmo as óbvias) — presente, ausente justificado, ausente.
2. Presença = tem assinatura própria naquela linha. Atenção: letra grande de um sócio pode "vazar" visualmente para a linha vizinha — sempre desconfiar de blocos de assinatura muito próximos/sobrepostos (aconteceu nas linhas 34-38 em mais de uma lista).
3. Para toda linha sem assinatura, checar explicitamente a coluna Falta Justificada **antes** de marcar como ausente simples. Um "Sim" marcado ali vira ausência justificada (pontua), não falta.
4. Reportar o resultado completo pro Jefferson conferir com a lista física antes de consolidar na planilha mestre.

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
├── documentos/
│   ├── lista-presenca/                 → lista de frequência assinada (sign-in) de cada reunião
│   │   ├── 2026-07-07.pdf
│   │   ├── 2026-07-14.pdf
│   │   ├── 2026-07-21.pdf
│   │   └── 2026-07-28.pdf
│   └── ata-reuniao/                    → ata oficial (registro/minuta) de cada reunião
│       ├── 2026-07-07.pdf
│       ├── 2026-07-14.pdf
│       ├── 2026-07-21.pdf
│       └── 2026-07-28.pdf
└── Rotary_Frequencia_Mestre.xlsx       → planilha mestre (histórico completo + fórmulas)
```

Cada reunião tem **dois documentos-fonte distintos**, guardados com o mesmo nome de arquivo em pastas separadas: a lista de presença (usada para apurar P/AJ/A) e a ata oficial da reunião (registro do que foi discutido). No site, dentro do card expandido de cada sócio, os dois ficam disponíveis lado a lado por data (ícone 📋 abre a lista, 📝 abre a ata) — a pessoa escolhe qual quer ver.

> Pasta antiga `atas/` (usada até 17/08/2026) ficou obsoleta e foi substituída por `documentos/lista-presenca/` — os arquivos antigos continuam no repositório GitHub por enquanto (não removidos), mas o site não os referencia mais.

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
- Cada card de sócio, ao expandir, mostra o histórico por data. Cada data tem 2 ícones: 📋 abre a lista de presença assinada daquele dia, 📝 abre a ata oficial da reunião — ambos em nova aba.
- Dados dos sócios ficam embutidos no próprio HTML (array `MEMBERS` no `<script>`), sem backend — é um site 100% estático.
- Paleta de cores segue a skill de dataviz interna (cores validadas para acessibilidade / daltonismo).

### Pendente de decisão (falado com o Jefferson em 17/08/2026)

- **Unificar lista de presença + ata num único PDF por reunião?** Ainda em aberto — por enquanto os dois documentos continuam separados (`lista-presenca/` e `ata-reuniao/`).
- **Seletor de mês/período**: hoje só existe julho, então não há seletor. Quando agosto entrar (2º mês de dados), avaliar como fica a navegação — opções a considerar: abas por mês, dropdown de período, ou manter tudo num ranking acumulado único com filtro opcional por mês. Decisão a tomar quando chegar a hora.

---

## 7. Fluxo de atualização mensal

1. Jefferson envia as 4-5 atas do mês (fotos/scans em PDF).
2. Claude lê cada uma, lista todas as linhas (ver seção 3) e reporta pro Jefferson conferir.
3. Jefferson corrige o que estiver errado (principalmente assinaturas sobrepostas).
4. Claude atualiza:
   - `Rotary_Frequencia_Mestre.xlsx`: novas colunas de data na aba Frequência.
   - `index.html`: novas entradas no array `MEETINGS` (label + caminho do PDF) e novos códigos no array `MEMBERS`.
   - Renomeia os PDFs recebidos para o padrão `AAAA-MM-DD.pdf` e coloca em `atas/`.
5. Claude salva tudo na pasta local do Jefferson (`C:\CONTROLADORIA\Claude - Projetos\Rotary`) via ponte com o computador.
6. Claude sobe as mudanças direto no GitHub, usando o navegador do Jefferson já autenticado (sem precisar de token nem senha) — envia os arquivos pela tela de upload do repositório e confirma o commit.
7. GitHub Pages faz o redeploy automático (leva 1-2 minutos). Claude confere o link ao vivo antes de avisar que terminou.

---

## 8. Decisões e histórico de ajustes

- 07/07/2026: primeira lista veio sem a coluna "Falta Justificada" preenchida em 5 linhas (irregularidade pontual daquela lista, não um padrão).
- Regra de falta justificada ajustada: conta como presença (1 ponto), não como neutro.
- Reginaldo Caribé de Araújo e Ricardo de Souza Santos: removidos do quadro e do ranking (só apareciam na lista de 07/07).
- Avisos de "assinatura fraca/marca pequena" (usados só como conferência interna durante a leitura) foram removidos do site e da planilha depois de validados com o Jefferson — não aparecem mais pro público.
- 17/08/2026: Eliana Mattos de Amorim Bueno (falta justificada, doença) — listas de 14/07 e 21/07 substituídas pelas versões corretas enviadas pelo Jefferson; código dela mudou de A (falta) para AJ (falta justificada) nas duas datas na planilha e no site (2 pts → 4 pts, 100% presença).
- 17/08/2026: adicionadas as 4 atas oficiais das reuniões (documento distinto da lista de presença) — site passou a mostrar os dois documentos por data lado a lado, cada um com seu ícone.
