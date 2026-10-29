# Pendências para lançamento público

Revisão de 29/10/2026. O APK publicado é experimental.

## Concluído

- Memória SQLite integrada e catálogo de indicadores com atualização assinada.
- Banco Supabase ativo, políticas de isolamento e submissão mediada com limite de 20 relatos por conta/dia.
- Conta opcional sem email, sessão criptografada e exclusão da própria conta.
- Site e download no GitHub Pages; código Android no repositório privado.
- Versão 1.3.2: falhas ao encerrar sessão preservam a credencial local; renovação de token antes de sair; recuperação do backup de sessão após gravação interrompida.

## Ainda necessário

- **Email:** configurar um provedor SMTP autorizado e validar entrega e templates. O provedor gratuito atual recusou a personalização. A conta sem email funciona independentemente.
- **Antiabuso público:** adicionar proteção contra criação distribuída de contas, limite global e política de retenção. O limite atual por conta não impede abuso por múltiplas contas.
- **Distribuição de produção:** definir e proteger uma chave de assinatura de lançamento e sua continuidade. Os APKs atuais usam assinatura de desenvolvimento; mudar a chave exige planejar a migração das instalações existentes.
- **Compatibilidade:** executar uma matriz de testes com Android 5, 6 e versões recentes, fabricantes e formatos adicionais. O aparelho validado é um Samsung SM-A025M com Android 12; SDK mínimo não certifica todos os modelos.
- **Eficácia:** ampliar e revisar os indicadores, avaliar falsos positivos e cobertura em laboratório e contratar auditoria/certificação quando houver essa decisão. Os 31 hashes e as heurísticas atuais têm alcance limitado.
- **Atualização do APK:** existe distribuição pelo site; a atualização automática assinada corresponde ao catálogo. Instalações de APK dependem das regras e da confirmação do Android.

O assistente usa regras locais revisadas. Relatos não viram regras de detecção automaticamente. Exclusões de aplicativos dependem de confirmação do Android. Estas restrições são deliberadas e não significam certificação de segurança absoluta.
