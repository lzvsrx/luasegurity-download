# Privacidade

O Luasegurity 1.2.0 usa internet para consultar a base pública assinada hospedada no GitHub. Não envia conteúdo de arquivos, inventário de aplicativos, conversas ou ocorrências. Não usa anúncios, contas, identificadores publicitários ou telemetria adicionada. O serviço de hospedagem recebe dados normais de conexão, como IP e User-Agent.

Atualizações da base são agendadas diariamente em rede não tarifada pelo Android e podem ser desligadas em Cuidados → Atualizações e memória local. A consulta manual usa a conexão disponível. INTERNET e ACCESS_NETWORK_STATE permitem o download e agendamento; RECEIVE_BOOT_COMPLETED permite persistir o agendamento após reinício. A base é assinada e somente dados são atualizados. Veja [UPDATES.md](UPDATES.md).

A memória SQLite privada guarda códigos fixos de falha ou correspondência conhecida, quantidade de ocorrências e avaliações de utilidade das orientações. Não guarda nomes ou caminhos de arquivos, textos de conversa ou lista de aplicativos nessa tabela. Pode ser apagada separadamente pelo painel de atualizações. Não há sincronização de ocorrências com Supabase nesta versão.

Uma análise lê nomes de pacotes, rótulos, permissões solicitadas e origem de instalação dos aplicativos visíveis. Salva o resultado e um histórico limitado no armazenamento privado do próprio app. Arquivos são lidos somente após seleção pelo seletor do Android; seu conteúdo não é copiado para armazenamento do app.

O usuário pode apagar o histórico em Cuidados ou limpar os dados/desinstalar o aplicativo. Relatórios exportados ficam no destino escolhido, fora do controle do app, e devem ser removidos pelo usuário se desejar.

A exclusão de um arquivo é opcional, confirmada individualmente e depende da permissão do provedor de documentos. É permanente; não há quarentena. Desinstalação de outros apps depende da confirmação do sistema.

O link de ajuda abre o navegador externo; a política do site acessado passa a valer nesse navegador.

Lua IA não grava perguntas ou respostas no histórico, em arquivos ou em relatórios. Seu motor é local e simbólico, sem chamadas de rede. Dados recebidos pelo menu Compartilhar só são analisados após ação do usuário. Arquivos compartilhados precisam de permissão temporária real e não podem ser excluídos nesse fluxo. Compartilhar resumo abre o seletor do Android e não envia mensagens automaticamente. Nenhuma integração concede acesso livre aos dados privados de outros aplicativos.
