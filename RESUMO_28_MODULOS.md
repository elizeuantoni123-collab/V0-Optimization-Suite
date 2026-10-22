# Resumo dos 28 Módulos — V0 Optimization Suite

| Módulo | Nome | O que faz |
|--------|------|-----------|
| **M01** | Exact Associative Index V8 | Índice de lookup exato em memória. Versão V8 especializada para cargas com muitos hits (SSE4.1). Carregado sob demanda por quem precisar de busca exata rápida. |
| **M02** | V0 Decision V8/V13 | Motor de decisão de contexto. V12 preservado como baseline; V13 é candidato aditivo para o builder gate16. |
| **M03** | Temperature Decision V19 | Serviço autônomo que monitora e decide "temperatura" de processos a cada 1s. Core V18 preservado; host V19 com índice PID exato. Roda como Windows Service. |
| **M04** | Pin V15 Autonomous | Monitora processos e "pina" os mais relevantes (seleciona os N melhores). Substitui sort completo por seleção parcial exata. Roda como Scheduled Task autônoma. |
| **M05** | Batch Planner V27 | Planejador de lotes. Resultado: KEEP_BASELINE — nenhum candidato superou o V27 existente. Mantido como referência. |
| **M06** | Range Descriptor V18 Host V2 | Monitora ranges de memória de processos ativos. Remove ordenação desnecessária (`Array.Sort`) do caminho crítico. Roda como Scheduled Task autônoma. |
| **M07** | TopK V7 Streaming | Mantém os 8 melhores processos por score em tempo real sem sort completo. K=1/2/4/8 são prefixos do Top-8. Roda como Scheduled Task autônoma. |
| **M08** | Materializer V8 Host | Materializa snapshots de estado de processos. Host V8 otimizado; core nativo V7 preservado byte-a-byte. Roda como Scheduled Task autônoma. |
| **M09** | External Memory V9/V11 Lease | Memória externa compartilhada (16GB). V11 adiciona acesso por "lease" (view sem cópia), eliminando a cópia SHM→buffer do cliente. Carregado sob demanda. |
| **M10** | Dedup V7 Batch8 | Deduplicação de blocos em lotes de 8. Adiciona hash batch nativo V0L. Roda como script autônomo contínuo. |
| **M11** | Dynamic Store V22 Radix8 | Armazenamento dinâmico com upsert AVX2 e rebuild ERMS. V22 host com Radix8; cores V21 preservados. Roda como Scheduled Task permanente. |
| **M12** | KV Window Manager V7 | Gerenciador de janela deslizante de chave-valor com pair SSE2. Gate executável chamado no boot para validar contratos. |
| **M13** | (Contrato/Toolchain) | Módulo de contrato interno. KEEP_BASELINE — serve de referência ABI para outros módulos. |
| **M14** | (Contrato/Toolchain) | Módulo de contrato interno. KEEP_BASELINE — biblioteca de suporte usada por consumidores compatíveis. |
| **M15** | (Contrato/Toolchain) | Módulo de contrato interno. KEEP_BASELINE — componente de toolchain sem substituto aprovado. |
| **M16** | Tier Gate V7 | Classifica processos em tiers de prioridade. Gate executável chamado no boot; candidato regrediu em n=64 (integrado no M26). |
| **M17** | Remap V22 SIMD Apply4 | Remapeia blocos de memória em grupos de 4 operações APPLY com SIMD. Gate executável chamado no boot. |
| **M18** | Semantic Bridge V7 Safe Pair | Ponte semântica que retorna ID seguro + chave segura em uma única chamada. Gate executável chamado no boot. |
| **M19** | Policy Router V10 | Roteador de políticas de dispatch. KEEP_BASELINE — nenhum candidato zerou regressões no domínio declarado. |
| **M20** | Module Manager V14 Matches8 | Gerenciador de módulos com avaliação de 8 queries em paralelo via AVX2 (bitmask). Gate executável chamado no boot. |
| **M21** | Per-Module Telemetry V7 | Telemetria por módulo com fast path para delta de chamadas já agregadas. Gate executável chamado no boot. |
| **M22** | Trusted Lookup | Lookup confiável. KEEP_BASELINE — candidatos (perfect hash e AVX2 batch) rejeitados por regressão de performance. |
| **M23** | Selective Transfer V7 Exact256 | Transferência seletiva de blocos exatos de 256 bytes via AVX2. Gate executável chamado no boot. |
| **M24** | Global Memory V8.22 Small Range | FastPolicy para compilação de ranges físicos pequenos (2–1024 páginas). Sem alteração de driver/EPT/hypervisor. |
| **M25** | Fine-Grained Subrange V5 Exact256 | Subrange fino com candidato AVX2 exato de 256 bytes. Gate executável chamado no boot. |
| **M26** | V0L Native x86-64 Backend V7 | Backend nativo x86-64 do compilador V0L com intrinsics V7. Regressão conhecida em n=64; parity pass confirmado. |
| **M27** | Memory ABI V1 | ABI de memória. KEEP_BASELINE — V1 preservada como autoridade de layout/contrato para todos os módulos. |
| **M28** | Global Adapter V3 | Adaptador global que conecta todos os módulos. Core V18 byte-idêntico; V3 adiciona fast hits e identity fallbacks. Roda como Windows Service. |
