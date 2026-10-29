# Compatibilidade e pesquisa de dispositivos

Pesquisa de 29/10/2026: o [catálogo público oficial do Google](https://storage.googleapis.com/play_public/supported_devices.html) contém 54.303 registros, 3.873 marcas informadas e 47.914 pares distintos de marca/modelo. Registros incluem variantes; esses números não representam aparelhos testados nem um censo mundial. Há dispositivos sem Google Play, ROMs modificadas e equipamentos antigos fora dessa fonte.

O [catálogo do Play Console](https://support.google.com/googleplay/android-developer/answer/9859371?hl=en) permite consultar os dispositivos publicamente lançados compatíveis com Google Play e exportar a cobertura de um aplicativo. A disponibilidade depende de versão do sistema, recursos exigidos, políticas e configuração de distribuição, não apenas da marca.

`scripts/research-devices.py` consulta o CSV oficial e gera contagens de **todas as marcas presentes nessa fonte**, em [contagens de marcas](brands.csv), e resumo com data e SHA-256 da origem. O catálogo completo de modelos permanece acessível na fonte oficial. A pesquisa não instala nem testa o APK nesses modelos.

## Cobertura da versão 1.1.1

| Sistema ou categoria | Situação |
| --- | --- |
| Android 1–4.4 / API abaixo de 21 | Não suportado; o instalador deve recusar o APK. |
| Android 5.0–5.1 / API 21–22 | Mínimo declarado; chamadas mais recentes protegidas e verificadas por Lint. Sem teste físico nesta versão. |
| Android 6–11 | Compatibilidade estática; testes físicos pendentes. |
| Android 12, Samsung SM-A025M | Aparelho físico disponível para instalação e validação. |
| Android 13 e posteriores | APIs recentes protegidas; validação de cada versão/modelo pendente. `targetSdk 35` não limita a versão máxima. |
| Celulares e tablets | Interface de toque; sem restrição por marca e sem bibliotecas nativas que exijam determinada ABI. |
| Dispositivos sem serviços Google, AOSP e Fire OS | Motor local sem dependência de Google Play Services; validação pendente. Atalhos de outros serviços podem não estar disponíveis. |
| TV, Wear OS, Android Automotive, Android Auto, XR | Sem interface dedicada nem certificação; não declarar suporte integral. |
| ROM modificada, root, gerenciamento corporativo | Comportamento depende das alterações e políticas; não há garantia. |

As marcas da fonte incluem Samsung, Motorola, Huawei, Xiaomi, Redmi, Oppo, Vivo, Realme, Nokia, HMD, Sony, Asus, Lenovo, LG, ZTE, TCL, Tecno e milhares de outras. O código não usa uma lista de marcas permitidas. Um nome aparecer no catálogo não comprova compatibilidade com este aplicativo.

## Adaptações realizadas

- `minSdk 21` amplia instalação para Android 5.0 sem exigir recursos mais novos no início do aplicativo.
- A informação de patch de segurança só é consultada na API 23 ou superior.
- Na API 21–22, o indicador usa `isKeyguardSecure`, com texto que distingue bloqueio de tela/SIM; isso não comprova configuração de senha de tela.
- Linhas de aplicativos também podem receber foco de teclado. Isso não equivale a uma interface certificada para controle remoto de TV.
- Não há `maxSdkVersion`, bloqueio de fabricante nem biblioteca nativa por arquitetura.

Conforme a [documentação de compatibilidade Android](https://developer.android.com/guide/practices/compatibility), chamadas de APIs recentes precisam de verificação de versão. Declarar um SDK mínimo não substitui testes reais. Recursos de hardware opcionais só devem ser liberados no manifesto depois de validar os respectivos fluxos de entrada e interface.

## Limites de segurança

Compatibilidade com Android antigo não corrige vulnerabilidades do próprio sistema. O aplicativo não pode ultrapassar o isolamento entre aplicativos, acessar todos os dados privados de outros apps ou garantir remover todo malware. Atualizar o sistema e manter cópias de segurança continuam sendo medidas separadas.
