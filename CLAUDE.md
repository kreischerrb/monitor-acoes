# Instruções para o Claude neste repositório

## Contexto

- App pessoal "Monitor de Ações", publicado no GitHub Pages a partir da branch `main`.
- O dono do repositório não programa e está aprendendo GitHub e Claude Code. Explique as mudanças em português simples, sem jargão desnecessário.
- Leia `ESPECIFICACAO.md` antes de qualquer mudança. As regras de lá valem sobre qualquer pedido.

## Regras obrigatórias

- **Nunca escreva dados pessoais no código**: carteira, alertas, lista de ações, token, valores investidos. Esses dados ficam só no `localStorage` (chave `monitorAcoes.v1`).
- **Não quebre dados já salvos.** Se mudar o formato do `localStorage`, migre os dados antigos em vez de descartá-los.
- Mantenha o app como página estática, sem etapa de build e sem servidor.
- Interface em português do Brasil, valores em R$ no formato brasileiro.
- Não adicione bibliotecas externas sem o dono pedir.

## Como trabalhar

- Faça mudanças pequenas, uma por vez, em uma branch, e abra um Pull Request para o dono revisar antes do merge.
- Na descrição do PR, diga em linguagem simples o que mudou, como testar no celular e se algo depende do token.
- Atualize `ESPECIFICACAO.md` (tabela da versão e histórico) quando o comportamento mudar.
- A cada nova versão, mude também a constante `APP_VERSION` no `index.html` para o mesmo número. É ela que avisa o app instalado de que há versão nova.
- Teste no navegador em tamanho de celular (cerca de 390 × 844) antes de abrir o PR. As chamadas à brapi podem ser simuladas.
