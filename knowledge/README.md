# Base pública Luasegurity — lzworldstech

`catalog.json` distribui indicadores SHA-256 revisados, com assinatura RSA-3072/SHA-256. O aplicativo fixa a chave pública e verifica assinatura, limites, formato e revisão antes de ativar os dados. A chave privada não é publicada.

`knowledge.db` é um snapshot SQLite público para consulta e auditoria, com indicadores e metadados. O aplicativo usa a exportação JSON assinada, não executa SQL remoto e não envia arquivos, inventários ou ocorrências para este endereço. O snapshot não é um servidor gravável nem uma integração Supabase.

A revisão inicial contém 31 indicadores públicos das pesquisas ESET AridSpy, Android GravityRAT e VajraSpy. Estudos de 2023–2024, importados em 29/10/2026. A publicação do mecanismo de atualização não aumenta automaticamente essa cobertura. Novas revisões precisam de revisão humana e assinatura pelo mantenedor.

Indicadores sob BSD-2-Clause: [licença ESET](../downloads/ESET-LICENSE.txt). Sem afiliação à ESET e sem seu motor comercial. O hash de um arquivo modificado pode escapar da base. Ausência de correspondência não comprova segurança.
