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

## Versão 1.7.0 (atual)

| Área | Comportamento |
| --- | --- |
| Mercado | Ibovespa (`^BVSP`, precisa de token) e dólar (`USD-BRL`, funciona com ou sem token); tocar no Ibovespa ou no dólar abre a tela de detalhe; lista de ações com preço e variação do dia; incluir e remover ações |
| Detalhe | Toque numa ação, no Ibovespa ou no dólar abre nome, preço, variação do dia, data e hora da última cotação (horário de Brasília) e o mesmo gráfico, com todos os recursos abaixo. Formatos: ações em R$ com 2 casas; Ibovespa em pontos, sem "R$" (ex.: 128.450 pts); dólar em R$ com 4 casas (ex.: R$ 5,4321). O formato vale também para a escala, os rótulos de máxima e mínima e o quadro da vela. O histórico do Ibovespa vem da brapi e precisa de token (sem token, a tela mostra "Requer token da brapi"); o do dólar vem da AwesomeAPI, sem token. A AwesomeAPI não informa a abertura do dia: nas velas do dólar, a abertura de cada dia é o fechamento do dia anterior, e um aviso curto embaixo do gráfico explica isso. Toque numa ação abre preço, variação, data e hora da última cotação (horário de Brasília) e gráfico com períodos 5D, 1M, 3M, 6M e 1A. Seletor "Linha \| Velas" acima do gráfico (padrão: Linha). Nas velas, cada vela é um dia em 5D, 1M e 3M, e uma semana em 6M e 1A; tocar numa vela mostra a data (ou "Semana de dd/mm"), Abertura, Máxima, Mínima e Fechamento (ou "Atual", se a vela ainda não fechou). Dias sem abertura, máxima ou mínima válidas ficam de fora; sem nenhuma vela válida, o app mostra a linha com um aviso. As velas usam a mesma consulta de histórico da linha. Os dois gráficos têm uma escala de preços à esquerda, com 4 ou 5 valores redondos no formato do ativo (por exemplo, R$ 30,00 / R$ 31,00; 126.000 pts / 128.000 pts; R$ 5,4000 / R$ 5,4500) e linhas de grade leves na altura de cada valor; o topo e a base do gráfico coincidem com o primeiro e o último valor da escala. Zoom nos dois gráficos: a pinça amplia e reduz só na horizontal (tempo), até no mínimo 5 dias (ou 5 velas) na tela e no máximo o período inteiro; com zoom, arrastar com um dedo desliza para os lados, sem passar das pontas dos dados. A escala de preços e as linhas de grade se ajustam ao trecho visível, e a faixa abaixo do gráfico mostra as datas do trecho e a variação entre o primeiro e o último fechamento visíveis, com o texto "no trecho" no lugar de "no período". A pinça dentro do gráfico não amplia a página; arrastar na vertical continua rolando a página. Nas velas, só um toque rápido seleciona a vela; arrastar ou fazer pinça não seleciona, e a vela selecionada continua mostrando as informações mesmo fora do trecho visível. Trocar o período, o tipo de gráfico ou a ação volta ao período inteiro. O zoom não é salvo |
| Sincronizar pelo link | O relatório mensal "Radar B3" traz um link que deixa a lista do Mercado igual à do relatório. Formato: `https://kreischerrb.github.io/monitor-acoes/#radar=NOME&ativos=CODIGO1,CODIGO2,...` (a lista viaja no próprio link, depois do `#`, e nunca no código do app; o token nunca entra no link). Ao abrir o app com esse link, aparece uma janela de confirmação com o título "Radar NOME" e os grupos Entram, Saem, Continuam e Ignorados. Cada código passa pela mesma limpeza do campo de incluir; inválidos, repetidos e os que passarem de 40 ficam em Ignorados. Se uma ação que sai continua na carteira ou nos alertas, a janela avisa. **Confirmar** deixa a lista exatamente igual à do link, na ordem do link, mostra "Lista sincronizada: X entraram, Y saíram" e atualiza as cotações pela fila de consultas. **Cancelar** não muda nada. Nos dois casos o trecho depois do `#` é apagado do endereço, para recarregar a página não repetir a sincronização. Link sem nenhum código válido: aviso e nada muda. Lista já igual à do link: só um aviso. Também funciona se o app já estiver aberto. Carteira, alertas, token e ajustes nunca mudam; o formato salvo em `monitorAcoes.v1` é o mesmo |
| Carteira | Posições com código, quantidade e preço médio; valor atual, resultado em R$ e %; resumo total |
| Alertas | "Sobe acima de" ou "cai abaixo de" um valor; conferidos a cada atualização; disparam aviso, vibração e notificação do navegador, se permitida; podem ser reativados |
| Ajustes | Aparência (automático, claro ou escuro; o automático segue o tema do celular, e a escolha entra no backup); a escolha Linha ou Velas da tela de detalhe também fica salva e entra no backup; token da brapi; atualização automática (desligada, 5, 15 ou 30 min); exportar e importar backup em JSON; apagar dados do aparelho; seção "Sobre o app" com o número da versão e o botão "Procurar nova versão" |
| Versão nova | Ao abrir o app e ao voltar para ele (no máximo a cada 10 min), o app lê a página publicada, sem usar a memória do navegador, e compara o número da versão. Se houver versão mais nova, mostra no topo "Nova versão disponível" com o botão "Atualizar", que recarrega a página nova. Não mexe nos dados salvos. O número fica na constante `APP_VERSION` do `index.html` e precisa mudar a cada versão |

### Limitações conhecidas

- Os alertas só funcionam com o app aberto.
- Sem token, o Ibovespa e as outras ações aparecem como "Disponível com token" ou "Requer token da brapi". O dólar funciona sem token.
- Com token salvo, se a brapi recusar uma consulta (erro 401 ou 403), o app mostra a mensagem que a própria brapi devolveu.
- O plano gratuito da brapi limita o histórico; períodos longos podem mostrar "Fora do plano gratuito".
- As velas do dólar usam o fechamento do dia anterior como abertura, porque a AwesomeAPI não informa a abertura do dia.
- Cada aparelho guarda os próprios dados.
- No gráfico, um arrasto que começa na diagonal pode ser entendido pelo celular como rolagem da página; nesse caso o gráfico não desliza naquele gesto.
- No app instalado no Android, a tela de abertura usa sempre a cor clara do `manifest.json`, mesmo no tema escuro, porque o manifesto aceita uma cor só.

## Fonte de dados

- Cotação e histórico: `https://brapi.dev/api/quote/{TICKER}` com `range` e `interval=1d`.
- Câmbio: AwesomeAPI, `https://economia.awesomeapi.com.br/json/last/USD-BRL` (gratuita, sem token). Preço = campo `bid`; variação = campo `pctChange`. O endpoint `/v2/currency` da brapi não responde no plano gratuito, por isso não é usado.
- Histórico do dólar: AwesomeAPI, `https://economia.awesomeapi.com.br/json/daily/USD-BRL/{dias}` (gratuita, sem token). Devolve um item por dia útil, o mais recente primeiro. O app usa `bid` como fechamento, `high` e `low` como máxima e mínima e `timestamp` como data. Não há campo de abertura. Pedidos por período (dias úteis, mais 1 para a abertura do primeiro dia): 5D = 6, 1M = 23, 3M = 67, 6M = 131 e 1A = 261. Se o mesmo dia vier repetido, fica a cotação mais recente. O limite de dias aceito pela API ainda não foi confirmado; se ela devolver menos dias, o gráfico mostra o que veio.
- Token enviado como parâmetro `token=` na consulta à brapi, só quando o usuário o cadastrou. Ele nunca é enviado à AwesomeAPI.
- Sem token: as ações de teste vão juntas numa consulta só, o dólar é consultado na AwesomeAPI, e nada é consultado para índices ou outras ações.
- Com token: uma consulta por ativo, compatível com o plano gratuito.
- As consultas à brapi saem em fila, uma de cada vez. Se a brapi responder "limite de consultas", o app espera e tenta de novo até 2 vezes.

## Próximas evoluções

A primeira evolução será escolhida depois de usar a versão 1.0 e servirá de exercício no tour guiado de Claude Code.

## Histórico

| Versão | Data | Mudança |
| --- | --- | --- |
| 1.7.0 | 06/11/2026 | Sincronizar a lista do Mercado por um link do relatório "Radar B3" (`#radar=…&ativos=…`), com janela de confirmação (Entram, Saem, Continuam e Ignorados), no máximo 40 códigos e endereço limpo depois de confirmar ou cancelar |
| 1.6.0 | 05/11/2026 | Número da versão em Ajustes (o rodapé mostrava "v1.2.1" fixo) e aviso automático de versão nova, para o app instalado não ficar preso numa versão antiga |
| 1.5.0 | 05/11/2026 | Ibovespa e dólar ganham tela de detalhe com gráfico de linha e velas, zoom e todos os períodos; Ibovespa em pontos, dólar em R$ com 4 casas; histórico do dólar pela AwesomeAPI, sem token, com abertura igual ao fechamento do dia anterior |
| 1.4.0 | 05/11/2026 | Zoom no gráfico da tela de detalhe: pinça amplia e reduz na horizontal, arrastar com um dedo desliza; escala, grade e faixa de datas seguem o trecho visível |
| 1.3.0 | 05/11/2026 | Escala de preços à esquerda nos gráficos de linha e de velas, com valores redondos em R$ e linhas de grade leves |
| 1.2.1 | 05/11/2026 | Dólar passa a vir da AwesomeAPI e funciona com ou sem token; com token salvo, recusas da brapi (401/403) mostram a mensagem da própria brapi |
| 1.2.0 | 04/11/2026 | Gráfico de velas na tela de detalhe, com seletor "Linha \| Velas"; velas semanais em 6M e 1A; toque na vela mostra abertura, máxima, mínima e fechamento |
| 1.1.0 | 03/11/2026 | Modo escuro: nova seção Aparência em Ajustes (automático, claro ou escuro); o padrão segue o tema do celular |
| 1.0.2 | 02/11/2026 | Tela de detalhe mostra a data e a hora da última cotação |
| 1.0.1 | 01/11/2026 | Corrige "limite de consultas atingido": menos consultas sem token, fila entre consultas e nova tentativa automática |
| 1.0 | 01/11/2026 | Primeira versão: mercado, detalhe com gráfico, carteira, alertas, ajustes e backup |
