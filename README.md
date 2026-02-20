# 🚀 Radar Fitness (V2 - Multiplataforma)

Sistema avançado em Node.js para monitoramento de preços e notificações em tempo real.

## 🛠️ Escopo do Projeto
Monitoramento automatizado de **produtos** simultâneos em três plataformas:
- **Amazon**: Integração via Scraper com sistema de Backoff Exponencial.
- **Shopee**: Integração via API Oficial (HMAC-SHA256).
- **Mercado Livre**: Integração via OAuth 2.0 (Authorization Code + Refresh Token).

## ✅ Requisitos e Stack
- **Runtime**: Node.js 20+ (ES Modules)
- **Infraestrutura**: Railway.app
- **Persistência**: Railway Volumes (Ponto de montagem: `/.data`)

## 📦 Estrutura de Persistência Crítica
O bot utiliza o diretório **`/.data`** no volume persistente do Railway.
- `/.data/prices_v2.json`: Histórico de preços (Shopee/Amazon).
- `/.data/ml_tokens_v2.json`: Tokens de acesso do Mercado Livre.
**AVISO:** Não altere o caminho absoluto `/.data` nos códigos para não perder a persistência de longo prazo.

## ⚙️ Configuração (Variáveis de Ambiente)
### Essenciais
- `TELEGRAM_BOT_TOKEN`: Token do BotFather.
- `TELEGRAM_CHAT_ID`: ID do canal de ofertas.
- `CHECK_INTERVAL_MINUTES`: Tempo entre ciclos (Padrão: 60).
- `DISCOUNT_THRESHOLD_PERCENT`: % mínimo para disparar alerta (Padrão: 12).

### Mercado Livre
- `ML_CLIENT_ID` / `ML_CLIENT_SECRET`: Credenciais da aplicação.
- `ML_INITIAL_CODE`: Código TG-... (usado apenas uma vez na partida a frio).
- `RESET_ML_TOKENS`: Defina como `true` para deletar o arquivo de tokens e forçar re-autenticação.

## ⚠️ Regras de Ouro (NÃO ALTERAR)
1. **Delays de Loop**: O `index.js` gerencia o tempo entre requisições. Alterar esses valores pode causar banimento de IP por comportamento robótico.
2. **Sistema de Exportação**: Todas as funções de fetch devem ser exportadas nomeadamente para o `index.js`.
3. **Formatador de Mensagem**: O `notifier.js` já está configurado para moeda brasileira (R$) e emojis de nível de oferta.
