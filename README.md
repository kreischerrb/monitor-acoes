# Monitor de Ações

App pessoal para celular que acompanha ações da B3, índices e câmbio. Ele roda direto no navegador e pode ser adicionado à tela inicial.

**Endereço do app:** https://kreischerrb.github.io/monitor-acoes/

## O que o app faz

| Aba | Função |
| --- | --- |
| Mercado | Ibovespa e dólar, lista de ações acompanhadas e gráfico de cada ação (5 dias a 1 ano) |
| Carteira | Posições com quantidade e preço médio, valor atual e resultado em R$ e % |
| Alertas | Aviso quando uma ação sobe acima ou cai abaixo de um valor (com o app aberto) |
| Ajustes | Tema claro, escuro ou automático, token da brapi, atualização automática, backup e limpeza dos dados |

As cotações vêm da [brapi.dev](https://brapi.dev), com cerca de 15 minutos de atraso. Sem token, só PETR4, VALE3, ITUB4 e MGLU3 funcionam.

## Onde ficam os seus dados

O código deste repositório é público. Os seus dados nunca entram nele.

| Onde | O que guarda |
| --- | --- |
| Este repositório (público) | Só o código: telas e regras de cálculo |
| Navegador do seu celular | Lista de ações, carteira, alertas e token da brapi |

Cada aparelho tem os próprios dados. Para guardar uma cópia ou levar os dados para outro aparelho, use **Ajustes → Exportar backup**. O token não entra no backup.

## Sincronizar a lista com o Radar B3

O relatório mensal "Radar B3" traz um botão que abre o app com a lista de ações do mês dentro do próprio link (depois do `#`). Funciona no Chrome e no app instalado.

1. Toque no botão do relatório. O app abre e mostra uma janela com o nome do radar e quais ações **entram**, **saem** e **continuam**. Códigos inválidos, repetidos ou além de 40 aparecem como **ignorados**.
2. Toque em **Confirmar** para deixar a sua lista igual à do relatório, na mesma ordem. As cotações são atualizadas em seguida.
3. Ou toque em **Cancelar** para não mudar nada.

Só a lista do Mercado muda. Carteira, alertas e token ficam como estão. Depois de confirmar ou cancelar, o link sai do endereço, então recarregar a página não pede de novo.

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
