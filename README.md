# BlueTech iOS — distribuição oficial

Repositório público de distribuição do BlueTech para iPhone. **Custo zero**:
GitHub Releases + GitHub Actions gratuitos, sem Apple Developer Program pago,
sem servidor e sem certificado corporativo.

O código-fonte privado continua em `bluetech-mobile`. Aqui ficam apenas:

- `version.json` — arquivo público lido pelo app para detectar versão nova.
- Releases com o arquivo `Bluetech-iPhone.ipa` como anexo.
- Documentação para usuários e para quem publica.

Nenhuma senha, e-mail Apple ou segredo fica neste repositório.

## Para o usuário

1. Abra o app. Se houver versão nova, toque em **Atualizar agora**.
2. O app abre a página oficial da Release neste repositório.
3. Baixe o arquivo `Bluetech-iPhone.ipa` na página da Release.
4. No computador, abra o Sideloadly, escolha esse IPA e reinstale usando a
   mesma conta Apple gratuita de sempre.
5. No iPhone: Ajustes > Geral > Gestão de dispositivos > confiar na conta.

**Baixar o IPA não instala o app.** A instalação é feita pelo Sideloadly.
A assinatura gratuita da Apple continua válida por **7 dias** e precisa ser
renovada; publicar uma versão nova **não** renova a assinatura.

Mais detalhes: [INSTALL.md](INSTALL.md).

## Para publicar uma versão nova

1. No projeto privado, atualize `pubspec.yaml` (`version: nome+build`) e
   `lib/core/constants/app_constants.dart` com o mesmo número/build.
2. Rode `flutter analyze` e `flutter test`. Faça commit e push.
3. No repositório privado, dispare a Action `iOS unsigned build` e baixe o
   artefato `Bluetech-unsigned-ipa`.
4. Renomeie o arquivo para `Bluetech-iPhone.ipa`.
5. Publicação manual: crie uma Release aqui com tag `vX.Y.Z`, anexe o IPA e
   escreva as novidades. **Não use automação de publicação**: toda Release é
   revisada e publicada manualmente.
6. Atualize `version.json` neste repositório com a nova versão, build, data,
   notas, link da Release e o SHA-256 real do IPA.
7. Faça commit de `version.json`. O app passa a avisar na próxima abertura.

O hash SHA-256 é publicado para conferência externa (por exemplo, no
Sideloadly ou em outra ferramenta de sua escolha). O app **não afirma** ter
verificado o IPA: ele apenas abre a página oficial.

## Histórico de versões

O app lê o histórico diretamente da API pública de Releases:

`https://api.github.com/repos/natanmuller585-netizen/BlueTech-iOS/releases`

Não é preciso duplicar notas manualmente em cada versão: a Release é a fonte
oficial.

## Verificação automática (sem publicar)

O workflow `.github/workflows/validate-version.yml` valida o `version.json`,
confere se a versão bate com a tag da Release e, quando há anexo, confere o
SHA-256 publicado. Ele **não publica nem altera nada** automaticamente.
