# V0-Optimization-Suite

Pacote com os 28 artefatos V0 + scripts de instalacao. Repositorio privado.

---

## Resumo dos 28 Modulos

| Modulo | Nome | Funcao |
|--------|------|--------|
| M01 | Exact Associative Index V8 | Indice de lookup exato em memoria. Versao V8 especializada para cargas com muitos hits (SSE4.1). Carregado sob demanda. |
| M02 | V0 Decision V8/V13 | Motor de decisao de contexto. V12 preservado como baseline; V13 e candidato aditivo para o builder gate16. |
| M03 | Temperature Decision V19 | Servico autonomo que monitora e decide temperatura de processos a cada 1s. Core V18 preservado; host V19 com indice PID exato. Roda como Windows Service. |
| M04 | Pin V15 Autonomous | Monitora processos e pina os mais relevantes. Substitui sort completo por selecao parcial exata. Roda como Scheduled Task autonoma. |
| M05 | Batch Planner V27 | Planejador de lotes. KEEP_BASELINE - nenhum candidato superou o V27 existente. Mantido como referencia. |
| M06 | Range Descriptor V18 Host V2 | Monitora ranges de memoria de processos ativos. Remove ordenacao desnecessaria do caminho critico. Roda como Scheduled Task autonoma. |
| M07 | TopK V7 Streaming | Mantem os 8 melhores processos por score em tempo real sem sort completo. K=1/2/4/8 sao prefixos do Top-8. Roda como Scheduled Task autonoma. |
| M08 | Materializer V8 Host | Materializa snapshots de estado de processos. Host V8 otimizado; core nativo V7 preservado byte-a-byte. Roda como Scheduled Task autonoma. |
| M09 | External Memory V9/V11 Lease | Memoria externa compartilhada (16GB). V11 adiciona acesso por lease (view sem copia), eliminando a copia SHM para buffer do cliente. Carregado sob demanda. |
| M10 | Dedup V7 Batch8 | Deduplicacao de blocos em lotes de 8. Adiciona hash batch nativo V0L. Roda como script autonomo continuo. |
| M11 | Dynamic Store V22 Radix8 | Armazenamento dinamico com upsert AVX2 e rebuild ERMS. V22 host com Radix8; cores V21 preservados. Roda como Scheduled Task permanente. |
| M12 | KV Window Manager V7 | Gerenciador de janela deslizante de chave-valor com pair SSE2. Gate executavel chamado no boot. |
| M13 | Contrato/Toolchain | Modulo de contrato interno. KEEP_BASELINE - serve de referencia ABI para outros modulos. |
| M14 | Contrato/Toolchain | Modulo de contrato interno. KEEP_BASELINE - biblioteca de suporte usada por consumidores compativeis. |
| M15 | Contrato/Toolchain | Modulo de contrato interno. KEEP_BASELINE - componente de toolchain sem substituto aprovado. |
| M16 | Tier Gate V7 | Classifica processos em tiers de prioridade. Gate executavel chamado no boot. |
| M17 | Remap V22 SIMD Apply4 | Remapeia blocos de memoria em grupos de 4 operacoes APPLY com SIMD. Gate executavel chamado no boot. |
| M18 | Semantic Bridge V7 Safe Pair | Ponte semantica que retorna ID seguro + chave segura em uma unica chamada. Gate executavel chamado no boot. |
| M19 | Policy Router V10 | Roteador de politicas de dispatch. KEEP_BASELINE - nenhum candidato zerou regressoes no dominio declarado. |
| M20 | Module Manager V14 Matches8 | Gerenciador de modulos com avaliacao de 8 queries em paralelo via AVX2 (bitmask). Gate executavel chamado no boot. |
| M21 | Per-Module Telemetry V7 | Telemetria por modulo com fast path para delta de chamadas ja agregadas. Gate executavel chamado no boot. |
| M22 | Trusted Lookup | Lookup confiavel. KEEP_BASELINE - candidatos rejeitados por regressao de performance. |
| M23 | Selective Transfer V7 Exact256 | Transferencia seletiva de blocos exatos de 256 bytes via AVX2. Gate executavel chamado no boot. |
| M24 | Global Memory V8.22 Small Range | FastPolicy para compilacao de ranges fisicos pequenos (2-1024 paginas). Sem alteracao de driver/EPT/hypervisor. |
| M25 | Fine-Grained Subrange V5 Exact256 | Subrange fino com candidato AVX2 exato de 256 bytes. Gate executavel chamado no boot. |
| M26 | V0L Native x86-64 Backend V7 | Backend nativo x86-64 do compilador V0L com intrinsics V7. Regressao conhecida em n=64; parity pass confirmado. |
| M27 | Memory ABI V1 | ABI de memoria. KEEP_BASELINE - V1 preservada como autoridade de layout e contrato para todos os modulos. |
| M28 | Global Adapter V3 | Adaptador global que conecta todos os modulos. Core V18 byte-identico; V3 adiciona fast hits e identity fallbacks. Roda como Windows Service. |

---

## Como Instalar

Extraia `ARTEFATOS_28_ESSENCIAL.zip` e execute como Administrador:

```powershell
.\INSTALADOR_E_AUTOSTART\V0_28_COORDINATED_INSTALLER.ps1
```

## Conteudo do ZIP

```
ARTEFATOS_28_ESSENCIAL.zip
├── ARTEFATOS/
│   └── M01 ... M28   (runtime essencial de cada modulo)
└── INSTALADOR_E_AUTOSTART/
    └── scripts de instalacao e autostart
```