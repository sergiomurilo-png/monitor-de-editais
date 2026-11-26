# Monitor de Editais

Página para celular que reúne editais de bolsas e financiamento à pesquisa (CNPq, CAPES, FAPEMAT, FINEP, DAAD, Fulbright e outros), com foco em quem faz doutorado em ciências ambientais em Mato Grosso.

Criado por Sergio, doutorando do Programa de Pós-Graduação em Ciências Ambientais (PPGCA) da UNEMAT, Campus Cáceres. Contribuições de colegas são muito bem-vindas.

## O que a página faz

- Lista os editais com prazo, valor, público-alvo e link oficial.
- Mostra quantos dias faltam para cada prazo e destaca os urgentes.
- Separa abertos, encerrados e novos (adicionados nos últimos 7 dias).
- Filtra por tipo (bolsa, projeto, evento, infraestrutura) e por destino ou origem.
- Busca por palavra, sem diferenciar acentos.
- Explica, em cada edital, por que ele interessa (campo "Por que interessa").

## Como funciona

O projeto tem três partes:

| Parte | O que é | Onde fica |
|---|---|---|
| Página | Um único arquivo HTML, sem dependências | `index.html` |
| Dados | A lista de editais, um registro por chamada | Na versão original, numa base de dados do Claude; aqui, em `dados/editais.json` |
| Atualização | Uma tarefa agendada do Claude que pesquisa os editais todo dia às 6h31 (Cuiabá) e grava as mudanças na base | Instruções em `docs/prompt-busca-diaria.md` |

A página tenta ler primeiro a base de dados do Claude. Fora do Claude (por exemplo, aqui no GitHub Pages), ela lê o arquivo `dados/editais.json`. Esse arquivo é uma **cópia estática**: só muda quando alguém o atualiza no repositório.

## Ver a página publicada

Se o GitHub Pages estiver ativado neste repositório (Settings > Pages > Branch `main`, pasta `/root`), a página fica em:

`https://<usuario>.github.io/<nome-do-repositorio>/`

## Formato de cada edital (`dados/editais.json`)

```json
{
  "_id": "cnpq-37-2026-brasil-suecia",
  "titulo": "Cooperação Brasil-Suécia: doutorado sanduíche e pós-doc (Chamada 37/2026)",
  "agencia": "MCTI/CNPq/CISB/SAAB · Suécia",
  "tipo": ["bolsa"],
  "pais": "suecia",
  "prioridade": "alta",
  "situacao": "aberto",
  "objetivo": "…",
  "publicoAlvo": "…",
  "relevancia": "Por que interessa e o que precisa ser feito.",
  "financiavel": ["…"],
  "cronograma": [{ "label": "Inscrições até", "data": "12 mar 2027" }],
  "prazoISO": "2027-03-12",
  "valor": "…",
  "link": "https://…",
  "fonte": "CNPq: chamadas abertas",
  "adicionadoEm": "2026-11-26",
  "verificadoEm": "2026-11-26"
}
```

Valores aceitos:

- `tipo`: `bolsa`, `projeto`, `infra`, `equipamento`, `evento`
- `pais`: `brasil`, `europa`, `eua`, `alemanha`, `franca`, `suecia`, `canada`, `america-do-sul`, `internacional`
- `prioridade`: `alta`, `media`, `baixa`
- `situacao`: `aberto`, `continuo`, `encerrado`
- Datas em `prazoISO`, `adicionadoEm` e `verificadoEm`: `AAAA-MM-DD`. Sem prazo fixo, omita `prazoISO` e use `prazoTexto` (ex.: "Fluxo contínuo").

## Ideias para quem quiser ajudar

- **Atualizar o `dados/editais.json` automaticamente**, por exemplo com uma GitHub Action que roda todo dia, para a versão do GitHub não depender da cópia manual.
- **Adaptar o perfil de busca** em `docs/prompt-busca-diaria.md` para outras áreas ou programas de pós-graduação.
- **Adicionar fontes**: editais internos de outras universidades, fundações estaduais (FAPs) de outros estados, fundações privadas da área ambiental.
- **Alertas**: aviso por e-mail ou Telegram quando aparecer um edital de prioridade alta ou um prazo estiver a menos de 7 dias.

## Aviso

A lista é um apoio para consulta rápida. Confirme sempre prazos e requisitos no edital oficial antes de submeter uma proposta.
