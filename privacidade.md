# Privacidade

Na versão 1.3.1, a opção “Conectar sem email” cria uma conta no Supabase sem fornecer email, após confirmação. O servidor ainda recebe IP e identificador da conta. A sessão fica criptografada no aparelho; perdê-la, limpar dados ou encerrar a sessão impede recuperar essa conta sem email. É possível excluir conta e relatos antes de sair. Nenhuma ocorrência é enviada ao conectar. A opção por email permanece experimental até configurar o envio e o template no provedor.

O Luasegurity 1.3.0 usa internet para consultar a base pública assinada do GitHub e, quando solicitado, acessar o Supabase. Não envia conteúdo de arquivos, inventário ou conversas. Conta e relatos são opcionais; as análises locais funcionam sem login. Não usa anúncios, identificadores publicitários ou telemetria adicionada. Os serviços recebem dados normais de conexão, como IP e User-Agent.

Atualizações da base são agendadas diariamente em rede não tarifada pelo Android e podem ser desligadas em Cuidados → Atualizações e memória local. A consulta manual usa a conexão disponível. INTERNET e ACCESS_NETWORK_STATE permitem o download e agendamento; RECEIVE_BOOT_COMPLETED permite persistir o agendamento após reinício. A base é assinada e somente dados são atualizados. Veja [UPDATES.md](UPDATES.md).

A memória SQLite privada guarda códigos fixos de ocorrência, contagens e avaliações. Não guarda nomes ou caminhos de arquivos, conversas ou inventário nessa tabela. Pode ser apagada separadamente e não é enviada automaticamente ao Supabase.

O login opcional envia seu email ao Supabase Auth para criar/acessar a conta. Um relato exige confirmação individual: o app envia somente o código escolhido, sem hash ou arquivo; o servidor associa dono, horário e status não revisado. Uma conta não pode consultar relatos de outra ou aprovar indicadores. Há limite de 20 envios por conta/dia UTC, inclusive após apagar relatos.

Android 6 ou superior guarda a sessão criptografada com AES-GCM e chave do Android Keystore, fora dos relatórios. Android 5 mantém consulta pública e funções locais. Email e código não são gravados no histórico; o email pode permanecer em memória no formulário durante o uso. A tela de nuvem restringe capturas conforme os recursos do sistema.

É possível apagar relatos, encerrar sessão ou excluir a própria conta e dados associados com confirmação. Encerrar sessão, limpar dados ou desinstalar o app não exclui a conta no servidor. Os indicadores públicos permanecem. Veja [CLOUD.md](CLOUD.md), incluindo os limites de entrega de email.

Uma análise lê nomes de pacotes, rótulos, permissões solicitadas e origem de instalação dos aplicativos visíveis. Salva o resultado e um histórico limitado no armazenamento privado do próprio app. Arquivos são lidos somente após seleção pelo seletor do Android; seu conteúdo não é copiado para armazenamento do app.

O usuário pode apagar o histórico em Cuidados ou limpar os dados/desinstalar o aplicativo. Relatórios exportados ficam no destino escolhido, fora do controle do app, e devem ser removidos pelo usuário se desejar.

A exclusão de um arquivo é opcional, confirmada individualmente e depende da permissão do provedor de documentos. É permanente; não há quarentena. Desinstalação de outros apps depende da confirmação do sistema.

O link de ajuda abre o navegador externo; a política do site acessado passa a valer nesse navegador.

Lua IA não grava perguntas ou respostas no histórico, em arquivos ou em relatórios. Seu motor é local e simbólico, sem chamadas de rede. Dados recebidos pelo menu Compartilhar só são analisados após ação do usuário. Arquivos compartilhados precisam de permissão temporária real e não podem ser excluídos nesse fluxo. Compartilhar resumo abre o seletor do Android e não envia mensagens automaticamente. Nenhuma integração concede acesso livre aos dados privados de outros aplicativos.
