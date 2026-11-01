# Trading Desk — Android + PWA

Projeto mobile do Trading Desk, com os seis agentes e operação exclusivamente simulada.

## Android (aplicativo instalável)

A pasta `android/` contém um aplicativo Android nativo mínimo (WebView) que empacota os arquivos do Trading Desk dentro do APK. O app abre offline e permite importar CSV pelo seletor de arquivos do Android.

### Gerar APK automaticamente pelo GitHub Actions

1. Crie um repositório GitHub vazio e envie o conteúdo desta pasta.
2. Abra a aba **Actions** do repositório.
3. Execute **Build Android APK** em **Run workflow** (ou aguarde o build após enviar alterações).
4. Ao terminar, abra a execução e baixe o artefato `TradingDesk-Android-debug`.
5. Extraia `app-debug.apk`, envie-o ao Android e toque no arquivo para instalar. O Android pode pedir autorização para instalar apps dessa fonte.

O APK gerado pelo fluxo é de depuração, não assinado para publicação na Play Store. Para distribuição pública, é necessário gerar uma versão release e assinar com uma chave própria.

### Compilar localmente

Requisitos: Android Studio/Android SDK 35, JDK 17 e Gradle 8.9.

```bash
cd android
gradle assembleDebug
```

Saída: `android/app/build/outputs/apk/debug/app-debug.apk`.

## PWA (instalação pelo navegador)

A raiz também mantém a versão PWA. Publique a pasta em hospedagem HTTPS e abra o endereço no Android Chrome ou iPhone Safari. No Android, use **Instalar app**; no iPhone, **Compartilhar → Adicionar à Tela de Início**.

## Funcionalidades presentes

- Seis agentes simulados, com decisão final do Chief.
- WIN, WDO, IND e DOL com mercado sintético.
- Consenso configurável, parâmetros de risco, entradas virtuais e saídas por stop/alvo.
- Diário local e exportação CSV.
- Importação de CSV com coluna `close` para atualizar a série visual.
- Interface responsiva e funcionamento local/offline no pacote Android.

## Limites da versão

- Não há conexão com Profit, corretora, Nelogica, B3, notícias, book, Times & Trades, opções ou redes sociais.
- Scout, Sentiment, News e Charts usam dados demonstrativos/sintéticos; News informa que não há feed conectado.
- Importar CSV atualiza a série visual, mas não executa backtest histórico completo.
- Custos e valores por ponto são estimativas simplificadas; valide especificações antes de qualquer avaliação financeira.
- Nenhuma ordem real é enviada. Não insira credenciais de corretora.

## Estrutura

- `index.html`, `styles.css`, `app.js`: aplicação.
- `android/`: projeto Android nativo que empacota a aplicação.
- `.github/workflows/android-apk.yml`: pipeline para gerar APK debug.
