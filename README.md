# Monitor de Ações

App pessoal para celular que acompanha ações da B3, índices e câmbio. Ele roda direto no navegador e pode ser adicionado à tela inicial.

**Endereço do app:** https://kreischerrb.github.io/monitor-acoes/

## O que o app faz

| Aba | Função |
| --- | --- |
| Mercado | Ibovespa e dólar, lista de ações acompanhadas e gráfico de cada ação (5 dias a 1 ano) |
| Carteira | Posições com quantidade e preço médio, valor atual e resultado em R$ e % |
| Alertas | Aviso quando uma ação sobe acima ou cai abaixo de um valor (com o app aberto) |
| Ajustes | Token da brapi, atualização automática, backup e limpeza dos dados |

As cotações vêm da [brapi.dev](https://brapi.dev), com cerca de 15 minutos de atraso. Sem token, só PETR4, VALE3, ITUB4 e MGLU3 funcionam.

## Onde ficam os seus dados

O código deste repositório é público. Os seus dados nunca entram nele.

| Onde | O que guarda |
| --- | --- |
| Este repositório (público) | Só o código: telas e regras de cálculo |
| Navegador do seu celular | Lista de ações, carteira, alertas e token da brapi |

Cada aparelho tem os próprios dados. Para guardar uma cópia ou levar os dados para outro aparelho, use **Ajustes → Exportar backup**. O token não entra no backup.

## Instalar no celular

- **Android (Chrome):** abra o endereço do app, toque no menu ⋮ e escolha **Adicionar à tela inicial** (ou **Instalar app**).
- **iPhone (Safari):** abra o endereço, toque em **Compartilhar** e escolha **Adicionar à Tela de Início**.

## Arquivos

| Arquivo | Para que serve |
| --- | --- |
| `index.html` | O app inteiro: telas, estilos e lógica |
| `manifest.json` e `icons/` | Nome e ícone quando o app é instalado na tela inicial |
| `ESPECIFICACAO.md` | O que o app deve fazer e as regras que não podem ser quebradas |
| `CLAUDE.md` | Instruções para o Claude Code trabalhar neste repositório |
