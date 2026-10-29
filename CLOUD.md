# Supabase — implantação e limites

Criador e marca dona: **lzworldstech**. Projeto `wduormqfxmjmkbfauzzj`, região `us-east-1`, ativo e verificado em 29/10/2026. As três tabelas iniciais já existiam: estrutura, RLS, políticas e função foram inspecionadas e preservadas. Foram carregados 31 indicadores públicos revisados. O acesso dos clientes à função auxiliar `rls_auto_enable` foi revogado.

## Aplicativo 1.3.0

Cuidados → Atualizações e memória local → Banco online Supabase:

- Consulta pública sem login, limitada a 1.000 indicadores revisados por consulta.
- Login opcional por email e código; envio de email confirmado pelo usuário.
- Envio individual confirmado de um dos seis códigos permitidos. O app não envia hash, arquivo, inventário ou conversa. O servidor associa dono, horário e status não revisado.
- Consulta dos próprios relatos (últimos até 100), exclusão dos próprios relatos, encerramento de sessão e exclusão da própria conta.

Android 6 ou superior protege a sessão com AES-256/GCM e chave do Android Keystore, com gravação atômica. Não se promete armazenamento em hardware em todos os modelos. Android 5 mantém consulta pública e recursos locais, sem alternativa com token em texto aberto. O APK contém somente URL e chave publishable pública; nenhuma chave administrativa.

O scanner continua usando o catálogo assinado. Relatos, votos ou linhas arbitrárias do banco não são promovidos automaticamente a detecções. O snapshot GitHub é público e não contém relatos privados.

## Proteção do banco

RLS nas três tabelas. Clientes não têm INSERT/UPDATE direto em relatos nem escrita em indicadores. A RPC deriva o dono de `auth.uid()`, valida códigos/hash opcional e limita a 20 envios por conta/dia UTC. Um contador separado impede reiniciar o limite ao apagar relatos. Uma conta não lê/apaga relatos de outra nem aprova indicadores.

A Edge Function `lua-delete-account` valida a sessão em `/auth/v1/user`, obtém o ID verificado e exclui somente essa conta usando chave administrativa apenas no servidor. IDs enviados no corpo são ignorados. A validação genérica de JWT do gateway está desativada nessa função porque a validação explícita no Auth aceita as chaves de assinatura atuais. Chamadas sem sessão ou com token inválido foram rejeitadas nos testes.

O aviso do advisor sobre a RPC `lua_submit_event` ser SECURITY DEFINER e acessível a usuários autenticados é esperado para esse fluxo mediado. As restrições foram testadas; isso não é uma certificação. Não habilitamos login anônimo nem desativamos confirmação de email.

O advisor também reportou proteção contra senhas vazadas desativada no projeto. O aplicativo usa código por email e não oferece login por senha; o aviso sobre a configuração global do Auth permanece registrado e deve ser avaliado antes de operação em produção. Não houve contratação ou alteração para plano pago.

## Entrega de email

Os testes geram códigos para contas sintéticas pelo endpoint administrativo, **sem enviar email**. Validam autenticação e acesso, mas não comprovam entrega em caixas de entrada.

Nenhum SMTP externo foi configurado nesta sessão. Antes de abrir o login ao público, é necessário verificar/configurar a entrega: o [SMTP padrão do Supabase](https://supabase.com/docs/guides/auth/auth-smtp) é voltado a testes, restringe destinatários à equipe e tem limites baixos. A consulta pública e os recursos locais não dependem dessa entrega.

## Testes executados

- 40 verificações reais do backend: leitura pública, submissão autenticada, isolamento entre contas, validação, impossibilidade de aprovar relatos/publicar indicadores e limite diário mesmo após apagar um relato.
- 6 verificações reais da função de exclusão: falta de sessão, token inválido, exclusão do próprio usuário e preservação de outra conta quando seu ID é injetado.
- Contas desses testes foram removidas. Um fixture separado permite testar no aparelho e é excluído ao concluir esse teste.
- No Samsung SM-A025M/Android 12: consulta pública HTTPS, login por código de teste, sessão criptografada persistente após reinício, envio confirmado, leitura privada, exclusão de relatos e exclusão da conta passaram. Alterar um byte da sessão criptografada causou rejeição antes da consulta remota; o ciphertext original foi restaurado somente para concluir a exclusão do fixture.
- As 66 verificações Java e build/Lint continuam sendo validações técnicas. Não substituem auditoria externa, testes em todos os modelos ou certificação de eficácia antivírus.

Referências: [RLS](https://supabase.com/docs/guides/database/postgres/row-level-security), [funções do banco](https://supabase.com/docs/guides/database/functions), [Auth](https://supabase.com/docs/guides/auth), [SMTP](https://supabase.com/docs/guides/auth/auth-smtp).
