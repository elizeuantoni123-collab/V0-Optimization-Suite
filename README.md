# Resumo dos 28 MÃ³dulos â€” V0 Optimization Suite

| MÃ³dulo | Nome | O que faz |
|--------|------|-----------|
| **M01** | Exact Associative Index V8 | Ãndice de lookup exato em memÃ³ria. VersÃ£o V8 especializada para cargas com muitos hits (SSE4.1). Carregado sob demanda por quem precisar de busca exata rÃ¡pida. |
| **M02** | V0 Decision V8/V13 | Motor de decisÃ£o de contexto. V12 preservado como baseline; V13 Ã© candidato aditivo para o builder gate16. |
| **M03** | Temperature Decision V19 | ServiÃ§o autÃ´nomo que monitora e decide "temperatura" de processos a cada 1s. Core V18 preservado; host V19 com Ã­ndice PID exato. Roda como Windows Service. |
| **M04** | Pin V15 Autonomous | Monitora processos e "pina" os mais relevantes (seleciona os N melhores). Substitui sort completo por seleÃ§Ã£o parcial exata. Roda como Scheduled Task autÃ´noma. |
| **M05** | Batch Planner V27 | Planejador de lotes. Resultado: KEEP_BASELINE â€” nenhum candidato superou o V27 existente. Mantido como referÃªncia. |
| **M06** | Range Descriptor V18 Host V2 | Monitora ranges de memÃ³ria de processos ativos. Remove ordenaÃ§Ã£o desnecessÃ¡ria (`Array.Sort`) do caminho crÃ­tico. Roda como Scheduled Task autÃ´noma. |
| **M07** | TopK V7 Streaming | MantÃ©m os 8 melhores processos por score em tempo real sem sort completo. K=1/2/4/8 sÃ£o prefixos do Top-8. Roda como Scheduled Task autÃ´noma. |
| **M08** | Materializer V8 Host | Materializa snapshots de estado de processos. Host V8 otimizado; core nativo V7 preservado byte-a-byte. Roda como Scheduled Task autÃ´noma. |
| **M09** | External Memory V9/V11 Lease | MemÃ³ria externa compartilhada (16GB). V11 adiciona acesso por "lease" (view sem cÃ³pia), eliminando a cÃ³pia SHMâ†’buffer do cliente. Carregado sob demanda. |
| **M10** | Dedup V7 Batch8 | DeduplicaÃ§Ã£o de blocos em lotes de 8. Adiciona hash batch nativo V0L. Roda como script autÃ´nomo contÃ­nuo. |
| **M11** | Dynamic Store V22 Radix8 | Armazenamento dinÃ¢mico com upsert AVX2 e rebuild ERMS. V22 host com Radix8; cores V21 preservados. Roda como Scheduled Task permanente. |
| **M12** | KV Window Manager V7 | Gerenciador de janela deslizante de chave-valor com pair SSE2. Gate executÃ¡vel chamado no boot para validar contratos. |
| **M13** | (Contrato/Toolchain) | MÃ³dulo de contrato interno. KEEP_BASELINE â€” serve de referÃªncia ABI para outros mÃ³dulos. |
| **M14** | (Contrato/Toolchain) | MÃ³dulo de contrato interno. KEEP_BASELINE â€” biblioteca de suporte usada por consumidores compatÃ­veis. |
| **M15** | (Contrato/Toolchain) | MÃ³dulo de contrato interno. KEEP_BASELINE â€” componente de toolchain sem substituto aprovado. |
| **M16** | Tier Gate V7 | Classifica processos em tiers de prioridade. Gate executÃ¡vel chamado no boot; candidato regrediu em n=64 (integrado no M26). |
| **M17** | Remap V22 SIMD Apply4 | Remapeia blocos de memÃ³ria em grupos de 4 operaÃ§Ãµes APPLY com SIMD. Gate executÃ¡vel chamado no boot. |
| **M18** | Semantic Bridge V7 Safe Pair | Ponte semÃ¢ntica que retorna ID seguro + chave segura em uma Ãºnica chamada. Gate executÃ¡vel chamado no boot. |
| **M19** | Policy Router V10 | Roteador de polÃ­ticas de dispatch. KEEP_BASELINE â€” nenhum candidato zerou regressÃµes no domÃ­nio declarado. |
| **M20** | Module Manager V14 Matches8 | Gerenciador de mÃ³dulos com avaliaÃ§Ã£o de 8 queries em paralelo via AVX2 (bitmask). Gate executÃ¡vel chamado no boot. |
| **M21** | Per-Module Telemetry V7 | Telemetria por mÃ³dulo com fast path para delta de chamadas jÃ¡ agregadas. Gate executÃ¡vel chamado no boot. |
| **M22** | Trusted Lookup | Lookup confiÃ¡vel. KEEP_BASELINE â€” candidatos (perfect hash e AVX2 batch) rejeitados por regressÃ£o de performance. |
| **M23** | Selective Transfer V7 Exact256 | TransferÃªncia seletiva de blocos exatos de 256 bytes via AVX2. Gate executÃ¡vel chamado no boot. |
| **M24** | Global Memory V8.22 Small Range | FastPolicy para compilaÃ§Ã£o de ranges fÃ­sicos pequenos (2â€“1024 pÃ¡ginas). Sem alteraÃ§Ã£o de driver/EPT/hypervisor. |
| **M25** | Fine-Grained Subrange V5 Exact256 | Subrange fino com candidato AVX2 exato de 256 bytes. Gate executÃ¡vel chamado no boot. |
| **M26** | V0L Native x86-64 Backend V7 | Backend nativo x86-64 do compilador V0L com intrinsics V7. RegressÃ£o conhecida em n=64; parity pass confirmado. |
| **M27** | Memory ABI V1 | ABI de memÃ³ria. KEEP_BASELINE â€” V1 preservada como autoridade de layout/contrato para todos os mÃ³dulos. |
| **M28** | Global Adapter V3 | Adaptador global que conecta todos os mÃ³dulos. Core V18 byte-idÃªntico; V3 adiciona fast hits e identity fallbacks. Roda como Windows Service. |

