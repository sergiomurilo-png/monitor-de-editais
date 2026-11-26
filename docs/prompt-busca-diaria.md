# Instruções da busca diária

Este é o texto usado na tarefa agendada do Claude que atualiza a lista todo dia às 6h31 (horário de Cuiabá). Para usar no seu próprio monitor:

1. Publique o `index.html` como página (artifact) no Claude, com a base de dados ativada, e copie o endereço dela.
2. Troque `<ENDERECO_DA_PAGINA>` abaixo por esse endereço e ajuste o bloco **Perfil** para a sua pesquisa.
3. Peça ao Claude para criar uma tarefa agendada diária com este texto.

---

Atualize o Monitor de Editais. Trabalhe sozinho, sem fazer perguntas: ninguém está acompanhando esta execução.

## Perfil (edite para a sua pesquisa)

Doutorando em Ciências Ambientais (PPGCA/UNEMAT, Cáceres, Mato Grosso). Interesses principais: doutorado sanduíche no exterior, bolsas e auxílios para doutorando, editais de pesquisa em ciências ambientais, sustentabilidade, Amazônia, Cerrado e Pantanal, gestão ambiental em universidades (A3P), divulgação e apropriação social da ciência. Registrar também oportunidades para depois do doutorado (pós-doc, fixação de doutores) com prioridade baixa ou média.

## Onde os dados ficam

Página: `<ENDERECO_DA_PAGINA>`. Use a ferramenta ArtifactData com esse endereço. Não republique a página; só altere a base.

- Coleção `editais`: um documento por chamada, com id curto e estável em minúsculas com hífens (ex.: `cnpq-37-2026-brasil-suecia`). Campos descritos no README deste repositório.
- Documento `meta/status`: `ultimaAtualizacao` (data e hora ISO 8601 com fuso -04:00), `resumo` (1 a 2 frases do que mudou), `fontesConsultadas` (lista).

## Passos

1. Pegue a data de hoje no fuso America/Cuiaba. Leia toda a coleção `editais` (action "list", limit 1000) e o documento `meta/status`.
2. Pesquise chamadas novas e atualizações. Consulte no mínimo: chamadas abertas do CNPq (https://www.gov.br/cnpq/pt-br/chamadas/abertas-para-submissao), editais da CAPES (PDSE, CAPES Global, Print, cooperação internacional), FAPEMAT, FINEP, PRPPG da UNEMAT, DAAD, Fulbright Brasil, Comissão Europeia e Marie Curie, e fundações com foco ambiental (Serrapilheira, Fundação Grupo Boticário, Instituto Clima e Sociedade, Fundo Amazônia). Prefira sempre a fonte oficial. Se uma página não abrir, siga com as outras.
3. Para cada chamada relevante e aberta que ainda não está na base, crie um documento com todos os campos e `adicionadoEm` = hoje. Não invente dados: deixe de fora o campo que não conseguir confirmar e diga em `relevancia` o que falta conferir.
4. Nos documentos existentes, atualize prazos, `situacao` e `verificadoEm` quando algo mudou. Marque `encerrado` quando o prazo passou. Mantenha os encerrados como referência de ciclo anual; apague só os encerrados há mais de 12 meses. Ao escrever, passe `if_version` com a versão lida.
5. Grave tudo numa única escrita em lote, incluindo `meta/status` com `ultimaAtualizacao` = agora. Grave `meta/status` mesmo sem mudanças ("Nenhuma chamada nova hoje.").
6. Termine com uma mensagem curta: quantas chamadas novas, quais prazos vencem nos próximos 14 dias e qualquer chamada de prioridade alta que apareceu.

Regras de escrita: textos em português, sem travessões; use dois-pontos, vírgulas ou parênteses.
