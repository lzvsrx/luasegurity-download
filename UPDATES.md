# Atualizações, memória e base online — 1.2.0

Criador e marca dona: **lzworldstech**.

## O que está integrado

- O scanner de aplicativos e o de arquivos consultam o catálogo ativo assinado. Sem catálogo baixado, usam a base incorporada no APK.
- `JobScheduler` agenda consulta diária em rede não tarifada, habilitada por padrão e desativável em Cuidados → Atualizações e memória local. O Android pode adiar a execução por rede, bateria, suspensão ou políticas do fabricante; não há garantia de horário. O agendamento persiste após reinício, salvo restrições do sistema ou encerramento forçado pelo usuário.
- “Buscar agora” consulta o mesmo endereço usando a conexão disponível. A consulta é executada fora da thread da interface.
- A memória SQLite `experiences.db` registra somente seis códigos de ocorrência e contagens limitadas. Avaliações “ajudou/não ajudou” adaptam as orientações locais. Não há treinamento de modelo, geração de assinaturas a partir de suspeitas ou execução de comandos.
- Listagem em lotes de 25 aplicativos e busca com espera de 180 ms reduzem reconstruções da interface. As análises e downloads usam executores separados.

## Endereços publicados

- [Catálogo JSON assinado](https://lzvsrx.github.io/luasegurity-download/knowledge/catalog.json)
- [Snapshot SQLite público](https://lzvsrx.github.io/luasegurity-download/knowledge/knowledge.db)
- [Descrição da base](https://lzvsrx.github.io/luasegurity-download/knowledge/README.md)

O snapshot contém indicadores públicos e metadados. Ele não é um banco gravável de usuários. O aplicativo consome o JSON assinado, não executa SQL baixado. A revisão inicial possui os mesmos 31 hashes já documentados: implementar atualização não cria cobertura nova por si só.

## Verificação e publicação

RSA-3072/SHA-256, chave pública fixa no APK, manifesto canônico com revisão, SHA-256 e tamanho do CSV. Limites de download e tempo, HTTPS sem redirecionamento, parser restrito, rejeição de regressão de revisão e gravação atômica. A assinatura também é verificada em consultas que retornam revisão já instalada. Falha mantém a base anterior.

Não existe confiança em certificados TLS arbitrários ou verificador de hostname permissivo. Em aparelhos antigos, certificados raiz ou rede desatualizados podem impedir o download; a base local continua disponível. A limpeza dos dados ou acesso privilegiado ao armazenamento pode remover o estado de revisão; não se promete proteção contra rollback após reset/root.

Para publicar uma nova revisão, o mantenedor revisa a origem e licença dos indicadores, atualiza o CSV e executa `SignKnowledge.java sign`. A chave privada fica fora do Git e do APK. `scripts/build-knowledge-db.py` produz o snapshot a partir da mesma exportação. Não assinar automaticamente denúncias ou conteúdos não revisados.

## Atualização do aplicativo e certificação

O mecanismo automático atualiza **dados de indicadores**, não o APK, as regras da Lua IA ou código executável. Novas versões do aplicativo são distribuídas pelo site e exigem confirmação de instalação. Não há instalação ou desinstalação silenciosa, antivírus universal ou certificação independente de eficácia.

Referências: [JobInfo.Builder e permissões de rede](https://developer.android.com/reference/android/app/job/JobInfo.Builder), [JobScheduler](https://developer.android.com/reference/android/app/job/JobScheduler), [PackageInstaller](https://developer.android.com/reference/android/content/pm/PackageInstaller).

## Supabase

A integração com banco remoto gravável continua separada. A migração em `supabase/migrations` está preparada; não comprova implantação. É preciso autenticar a conta, selecionar um projeto e testar permissões de acesso. Esta versão não envia ocorrências a Supabase. Não há chave administrativa embutida, banco privado exposto no GitHub nem alegação de conexão remota antes da validação.
