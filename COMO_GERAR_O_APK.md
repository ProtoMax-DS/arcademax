# ProtoMax Arcade

Console para Android que roda os jogos HTML5 da ProtoMax.Games guardados dentro do próprio app. Funciona offline.

## Gerar o APK pelo GitHub (sem instalar nada)

1. Crie um repositório novo no GitHub (pode ser privado), por exemplo `protomax-arcade`.
2. Clique em **Add file → Upload files** e arraste **todo o conteúdo** desta pasta (não a pasta em si).
   - Confira se a pasta `.github` foi junto. No Mac ela fica escondida (Cmd+Shift+. mostra).
   - Se ela não subir: **Add file → Create new file**, nome `.github/workflows/build-apk.yml`, e cole o conteúdo do arquivo de mesmo nome.
3. Clique em **Commit changes**. O GitHub começa a compilar sozinho.
4. Abra a aba **Actions**, entre na execução mais recente (leva uns 3 a 5 minutos) e baixe o **ProtoMax-Arcade** em *Artifacts*. Vem um .zip com o `ProtoMax-Arcade.apk` dentro.

Cada vez que você mudar algo no repositório, ele gera um APK novo.

## Ou pelo Android Studio

Abra esta pasta no Android Studio, espere o Gradle sincronizar e use **Build → Build APK(s)**.

## Instalar no celular

Mande o `.apk` para o celular, toque nele e permita **instalar apps desconhecidos** quando o Android pedir.
O APK é sempre assinado com a mesma chave (pasta `keystore/`), então as versões novas instalam por cima sem apagar o progresso dos jogos.

## Adicionar um jogo

1. Crie `app/src/main/assets/www/games/<nome-do-jogo>/` com o `index.html` do jogo e uma capa `cover.jpg` em 3:4 (ex.: 900×1200).
2. Acrescente um bloco em `app/src/main/assets/www/games.js` (copie o do Geo Sagris).
3. `orientation` pode ser `"portrait"`, `"landscape"` ou `"any"`. O console gira a tela sozinho ao abrir o jogo.

Dicas para o jogo funcionar offline: fontes e imagens precisam estar dentro da pasta do jogo (nada de link para Google Fonts ou CDN).
O botão voltar do celular sempre leva de volta à biblioteca.

## Recursos que os jogos podem usar

- `ProtoMaxNative.setOrientation("landscape")`: trava a orientação.
- `ProtoMaxNative.saveImage(dataUrlPng, "nome.png")`: salva na galeria, em Imagens/ProtoMax (Android 10+). Retorna `true` se deu certo.

Sempre teste `if (window.ProtoMaxNative)` antes, para o jogo continuar rodando no navegador também.
