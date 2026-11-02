# Especificação: Monitor de Ações

Documento de referência do app. Toda evolução deve seguir as regras abaixo e atualizar este arquivo quando mudar o comportamento do app.

## Objetivo

App pessoal para celular, de uso de uma só pessoa, para acompanhar ações da B3, índices e câmbio, com atraso de cerca de 15 minutos.

## Regras que não podem ser quebradas

1. **Nenhum dado pessoal no repositório.** Carteira, alertas, lista de ações, token da brapi e qualquer valor digitado pelo usuário ficam apenas no `localStorage` do navegador, na chave `monitorAcoes.v1`. Nada disso pode aparecer no código, em arquivos de exemplo ou em mensagens de commit.
2. **O token nunca sai do aparelho**, a não ser nas consultas à brapi. Ele não entra no backup exportado.
3. **Repositório público, publicado no GitHub Pages.** O app precisa funcionar como página estática, sem servidor próprio.
4. **Interface em português do Brasil**, com valores em R$ no formato brasileiro.
5. **Funcionar sem token** com as 4 ações de teste da brapi (PETR4, VALE3, ITUB4, MGLU3) e mostrar uma mensagem clara quando algo depende do token.

## Versão 1.0.2 (atual)

| Área | Comportamento |
| --- | --- |
| Mercado | Ibovespa (`^BVSP`) e dólar (`USD-BRL`); lista de ações com preço e variação do dia; incluir e remover ações |
| Detalhe | Toque numa ação abre preço, variação, data e hora da última cotação (horário de Brasília) e gráfico de linha com períodos 5D, 1M, 3M, 6M e 1A |
| Carteira | Posições com código, quantidade e preço médio; valor atual, resultado em R$ e %; resumo total |
| Alertas | "Sobe acima de" ou "cai abaixo de" um valor; conferidos a cada atualização; disparam aviso, vibração e notificação do navegador, se permitida; podem ser reativados |
| Ajustes | Token da brapi; atualização automática (desligada, 5, 15 ou 30 min); exportar e importar backup em JSON; apagar dados do aparelho |

### Limitações conhecidas

- Os alertas só funcionam com o app aberto.
- Sem token, índices, dólar e outras ações aparecem como "Disponível com token" ou "Requer token".
- O plano gratuito da brapi limita o histórico; períodos longos podem mostrar "Fora do plano gratuito".
- Cada aparelho guarda os próprios dados.

## Fonte de dados

- Cotação e histórico: `https://brapi.dev/api/quote/{TICKER}` com `range` e `interval=1d`.
- Câmbio: `https://brapi.dev/api/v2/currency?currency=USD-BRL`.
- Token enviado como parâmetro `token=` na consulta, só quando o usuário o cadastrou.
- Sem token: as ações de teste vão juntas numa consulta só, e nada é consultado para índices, dólar ou outras ações.
- Com token: uma consulta por ativo, compatível com o plano gratuito.
- As consultas saem em fila, uma de cada vez. Se a brapi responder "limite de consultas", o app espera e tenta de novo até 2 vezes.

## Próximas evoluções

A primeira evolução será escolhida depois de usar a versão 1.0 e servirá de exercício no tour guiado de Claude Code.

## Histórico

| Versão | Data | Mudança |
| --- | --- | --- |
| 1.0.2 | 02/11/2026 | Tela de detalhe mostra a data e a hora da última cotação |
| 1.0.1 | 01/11/2026 | Corrige "limite de consultas atingido": menos consultas sem token, fila entre consultas e nova tentativa automática |
| 1.0 | 01/11/2026 | Primeira versão: mercado, detalhe com gráfico, carteira, alertas, ajustes e backup |
