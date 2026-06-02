<!--
================================================================================
ARQUIVO: vehicle_base.h.md
PRIORIDADE: Nível 1 - Crítico
CATEGORIA: Veículos (Base)
DESCRICAO: Define a classe base Vehicle e todos os componentes fundamentais 
           para qualquer veículo no jogo (trens, caminhões, aviões, navios).
           Estabelece a estrutura de dados principal, enums de status, cache,
           e métodos comuns para todo o sistema de veículos.
INTERACOES: vehicle.h, aircraft.h, roadveh.h, train.h, ship.h, order_base.h, 
            cargopacket.h, engine_type.h, group_type.h
AUTOR: OpenTTD Team
TRADUCAO_CONCEITUAL: Assistente IA
DATA: 2024
================================================================================
-->

# vehicle_base.h - Base para Todos os Veículos

## 📋 Visão Geral

Este é o arquivo **mais fundamental** do sistema de veículos do OpenTTD. Ele define:
- A classe `Vehicle` que serve como base para TODOS os veículos do jogo
- Enums de status e flags que controlam o comportamento dos veículos
- Estruturas de cache para otimização de performance
- Métodos virtuais que serão implementados por tipos específicos (trens, aviões, etc.)

**Importância**: Sem este arquivo, nenhum veículo poderia existir no jogo. Ele estabelece o contrato básico que todos os veículos devem seguir.

---

## 🔢 Constantes Fundamentais

### Distâncias de Movimento

```cpp
const uint TILE_AXIAL_DISTANCE = 192;   // Distância lógica em direções diagonais
const uint TILE_CORNER_DISTANCE = 128;  // Distância lógica ao cruzar cantos
```

**Explicação da Lógica**:
- O OpenTTD usa um sistema de coordenadas onde cada tile tem medidas lógicas específicas
- `TILE_AXIAL_DISTANCE` (192): Usado quando veículo se move nas direções diagonais (NE, SE, SO, NO)
- `TILE_CORNER_DISTANCE` (128): Usado quando veículo cruza os cantos do tile
- Estes valores são cruciais para o sistema de movimento suave e progressivo dos veículos
- O progresso do veículo é medido em unidades de 1/256 destas distâncias

---

## 🎯 Enums de Status e Flags

### VehStatus - Bits de Status do Veículo

```cpp
enum VehStatus {
    VS_HIDDEN          = 0x01,  // Veículo não está visível
    VS_STOPPED         = 0x02,  // Veículo parado pelo jogador
    VS_UNCLICKABLE     = 0x04,  // Veículo não clicável (sombras)
    VS_DEFPAL          = 0x08,  // Usa paleta padrão do veículo
    VS_TRAIN_SLOWING   = 0x10,  // Trem está desacelerando
    VS_SHADOW          = 0x20,  // Veículo é uma sombra
    VS_AIRCRAFT_BROKEN = 0x40,  // Avião está quebrado
    VS_CRASHED         = 0x80   // Veículo está destruído
};
```

**Lógica de Uso**:
- Cada bit representa um estado independente (bitmask)
- Múltiplos status podem estar ativos simultaneamente
- Exemplo: Um avião pode estar `VS_STOPPED | VS_AIRCRAFT_BROKEN` (parado e quebrado)
- `VS_HIDDEN` e `VS_SHADOW`: Usados para veículos "fantasmas" que não interagem com o jogador
- `VS_TRAIN_SLOWING`: Sinaliza que o trem está em processo de frenagem

### VehicleFlags - Flags de Controle Comportamental

```cpp
enum VehicleFlags {
    VF_LOADING_FINISHED,        // Terminou de carregar carga
    VF_CARGO_UNLOADING,         // Está descarregando carga
    VF_BUILT_AS_PROTOTYPE,      // É um protótipo (preview exclusiva)
    VF_TIMETABLE_STARTED,       // Já começou a operar no horário
    VF_AUTOFILL_TIMETABLE,      // Deve preencher horário automaticamente
    VF_AUTOFILL_PRES_WAIT_TIME, // Preservar tempos de espera no auto-fill
    VF_STOP_LOADING,            // Não carregar mais no próximo ciclo
    VF_PATHFINDER_LOST,         // Pathfinder está perdido (sem rota)
    VF_SERVINT_IS_CUSTOM,       // Intervalo de serviço é personalizado
    VF_SERVINT_IS_PERCENT       // Intervalo de serviço é em porcentagem
};
```

**Aplicações Práticas**:
- `VF_LOADING_FINISHED` + `VF_CARGO_UNLOADING`: Controlam o ciclo de carga/descarga
- `VF_BUILT_AS_PROTOTYPE`: Permite testar veículos antes do lançamento oficial
- `VF_TIMETABLE_*`: Gerenciam o sistema de horários (timetable)
- `VF_PATHFINDER_LOST`: Aciona recálculo de rota quando o veículo se perde
- `VF_SERVINT_*`: Determinam como o intervalo de manutenção é calculado

### NewGRFCacheValidValues - Validação de Cache NewGRF

```cpp
enum NewGRFCacheValidValues {
    NCVV_POSITION_CONSIST_LENGTH   = 0,  // Var 40 do NewGRF válida
    NCVV_POSITION_SAME_ID_LENGTH   = 1,  // Var 41 do NewGRF válida
    NCVV_CONSIST_CARGO_INFORMATION = 2,  // Var 42 do NewGRF válida
    NCVV_COMPANY_INFORMATION       = 3,  // Var 43 do NewGRF válida
    NCVV_POSITION_IN_VEHICLE       = 4,  // Var 4D do NewGRF válida
    NCVV_END                       = 5   // Fim dos bits
};
```

**Propósito**:
- NewGRFs são modificações criadas pela comunidade que adicionam funcionalidades
- Este enum controla quais valores calculados do NewGRF ainda são válidos no cache
- Quando algo muda (ex: composição do trem), bits específicos são invalidados
- Evita recálculos desnecessários, melhorando performance

### VisualEffect - Efeitos Visuais de Veículos

```cpp
enum VisualEffect {
    VE_OFFSET_START        = 0,   // Primeiro bit do offset (posição)
    VE_OFFSET_COUNT        = 4,   // Número de bits para offset
    VE_OFFSET_CENTRE       = 8,   // Offset = centro do veículo
    
    VE_TYPE_START          = 4,   // Primeiro bit do tipo de efeito
    VE_TYPE_COUNT          = 2,   // Número de bits para tipo
    VE_TYPE_DEFAULT        = 0,   // Padrão da classe do motor
    VE_TYPE_STEAM          = 1,   // Fumaça de vapor
    VE_TYPE_DIESEL         = 2,   // Fumaça diesel
    VE_TYPE_ELECTRIC       = 3,   // Faíscas elétricas
    
    VE_DISABLE_EFFECT      = 6,   // Flag para desativar efeito
    VE_ADVANCED_EFFECT     = 6,   // Flag para efeitos avançados
    VE_DISABLE_WAGON_POWER = 7,   // Desativar potência do vagão
    
    VE_DEFAULT = 0xFF             // Valor padrão
};
```

**Como Funciona**:
- Combina **posição** (onde aparece o efeito) com **tipo** (qual efeito)
- Offsets: 0 = frente, 8 = centro, 15 = traseira do veículo
- Tipos definem o estilo visual baseado no motor (vapor, diesel, elétrico)
- Flags permitem desativar efeitos ou usar configurações avançadas

### VisualEffectSpawnModel - Modelos de Efeitos

```cpp
enum VisualEffectSpawnModel {
    VESM_NONE       = 0,  // Sem efeito visual
    VESM_STEAM,           // Modelo de vapor
    VESM_DIESEL,          // Modelo diesel
    VESM_ELECTRIC,        // Modelo elétrico
    VESM_END              // Fim da enumeração
};
```

**Uso**: Define qual modelo de partícula/spawn será usado para cada tipo de motor.

### GroundVehicleSubtypeFlags - Subtipos de Veículos Terrestres

```cpp
enum GroundVehicleSubtypeFlags {
    GVSF_FRONT            = 0,  // Locomotiva líder do consist
    GVSF_ARTICULATED_PART = 1,  // Parte articulada de um motor
    GVSF_WAGON            = 2,  // Vagão (não usado para veículos rodoviários)
    GVSF_ENGINE           = 3,  // Motor que pode estar atrás de outro
    GVSF_FREE_WAGON       = 4,  // Primeiro vagão em cadeia (no depósito)
    GVSF_MULTIHEADED      = 5   // Motor com múltiplas cabeças
};
```

**Conceito de "Consist"**:
- **Consist**: Composição completa de um trem (locomotiva + vagões)
- `GVSF_FRONT`: Identifica a locomotiva principal que controla o trem
- `GVSF_ARTICULATED_PART`: Partes conectadas permanentemente (ex: locomotiva dupla)
- `GVSF_WAGON`: Vagões independentes que podem ser rearranjados
- `GVSF_MULTIHEADED`: Trens com locomotivas em ambas as extremidades

---

## 🗂️ Estruturas de Dados

### NewGRFCache - Cache de Valores NewGRF

```cpp
struct NewGRFCache {
    uint32 position_consist_length;   // Cache para NewGRF var 40
    uint32 position_same_id_length;   // Cache para NewGRF var 41
    uint32 consist_cargo_information; // Cache para NewGRF var 42
    uint32 company_information;       // Cache para NewGRF var 43
    uint32 position_in_vehicle;       // Cache para NewGRF var 4D
    uint8  cache_valid;               // Bitset de validade dos caches
};
```

**Otimização de Performance**:
- Armazena resultados de cálculos complexos do NewGRF
- `cache_valid` indica quais campos são válidos (usando enum anterior)
- Quando a composição muda, apenas bits relevantes são invalidados
- Evita recalcular informações caras a cada frame/tick

### VehicleCache - Cache Comum a Todos os Veículos

```cpp
struct VehicleCache {
    uint16 cached_max_speed;        // Velocidade máxima do consist
    uint16 cached_cargo_age_period; // Período de envelhecimento da carga
    byte cached_vis_effect;         // Efeito visual ativo
};
```

**Propósito**:
- `cached_max_speed`: Menor velocidade entre todos os veículos do consist
- `cached_cargo_age_period`: Quantos ticks até a carga envelhecer
- `cached_vis_effect`: Efeito visual atualmente aplicado

### VehicleSpriteSeq - Sequência de Sprites

```cpp
struct VehicleSpriteSeq {
    PalSpriteID seq[8];  // Sequência de sprites com paleta
    uint count;          // Quantidade de sprites na sequência
    
    // Métodos utilitários:
    bool IsValid() const;           // Tem sprites?
    void Clear();                   // Limpa sequência
    void Set(SpriteID sprite);      // Define sprite único
    void Draw(...);                 // Desenha no screen
};
```

**Funcionalidade**:
- Permite veículos compostos por múltiplos sprites
- Suporta recolouring (mudança de paleta de cores)
- Usado para animações e diferentes ângulos de visão

### MutableSpriteCache - Cache de Sprites Mutáveis

```cpp
struct MutableSpriteCache {
    Direction last_direction;          // Última direção usada
    bool revalidate_before_draw;       // Precisa validar antes de desenhar
    Rect old_coord;                    // Coordenadas da última bounding box
    bool is_viewport_candidate;        // Pode ser desenhado na viewport
    VehicleSpriteSeq sprite_seq;       // Aparência atual do veículo
};
```

**Lógica de Renderização**:
- Controla quando sprites precisam ser recalculados
- `revalidate_before_draw`: Bandeira para validação preguiçosa
- `is_viewport_candidate`: Otimização para determinar visibilidade
- Minimiza chamadas caras de `GetImage()` apenas quando necessário

---

## 🚗 Classe Vehicle - O Coração do Sistema

### Declaração e Herança

```cpp
struct Vehicle : VehiclePool::PoolItem<&_vehicle_pool>, BaseVehicle, BaseConsist {
    // ... membros e métodos ...
};
```

**Arquitetura**:
- Herda de `VehiclePool::PoolItem`: Gerenciamento por pool de memória
- Herda de `BaseVehicle`: Propriedades básicas de veículo
- Herda de `BaseConsist`: Propriedades de composição (para trens)
- Usa padrão **CRTP** (Curiously Recurring Template Pattern) via `SpecializedVehicle`

### Membros Privados - Encadeamento de Veículos

```cpp
private:
    Vehicle *next;                      // Próximo veículo na cadeia
    Vehicle *previous;                  // Veículo anterior (NOSAVE)
    Vehicle *first;                     // Primeiro veículo (NOSAVE)
    
    Vehicle *next_shared;               // Próximo com ordens compartilhadas
    Vehicle *previous_shared;           // Anterior com ordens compartilhadas (NOSAVE)
```

**Sistema de Cadeia**:
- **next/previous**: Formam lista duplamente encadeada de veículos articulados
- **first**: Ponteiro rápido para a locomotiva líder
- **NOSAVE**: Não salvos no savegame (reconstruídos ao carregar)
- **shared**: Cadeia separada para veículos que compartilham ordens

### Membros Públicos - Estado Fundamental

#### Posicionamento e Movimento

```cpp
TileIndex tile;              // Tile atual do veículo
TileIndex dest_tile;         // Tile de destino (próxima estação)

int32 x_pos, y_pos, z_pos;   // Coordenadas precisas (sub-tile)
Direction direction;         // Direção para onde está facing

uint16 cur_speed;            // Velocidade atual
byte subspeed;               // Velocidade fracionária
byte acceleration;           // Aceleração atual
uint32 motion_counter;       // Contador para sons de movimento
byte progress;               // Progresso no tile atual (0-255)
```

**Sistema de Coordenadas Híbrido**:
- `tile`: Posição grossa (qual tile está ocupando)
- `x_pos, y_pos, z_pos`: Posição precisa dentro do tile (para animação suave)
- `progress`: Quanto do tile já foi percorrido (usado para movimento)
- `direction`: Para onde o veículo está apontado (8 direções possíveis)

#### Economia e Lucro

```cpp
Money profit_this_year;      // Lucro este ano (<< 8, parte fracionária)
Money profit_last_year;      // Lucro ano passado
Money value;                 // Valor do veículo

CargoPayment *cargo_payment; // Pagamento de carga em andamento
```

**Detalhe Importante**:
- Lucros são armazenados com 8 bits fracionários (`<< 8`)
- Isso permite precisão de centavos sem usar floating point
- Exemplo: 1000 na verdade significa 1000/256 = ~3.9 unidades monetárias

#### Idade e Confiabilidade

```cpp
Year build_year;                        // Ano de construção
Date age;                               // Idade em dias
Date max_age;                           // Idade máxima (aposentadoria)
Date date_of_last_service;              // Último serviço em depósito

uint16 reliability;                     // Confiabilidade atual (%)
uint16 reliability_spd_dec;             // Velocidade de queda da confiabilidade

byte breakdown_ctr;                     // Contador de falhas
byte breakdown_delay;                   // Duração da falha
byte breakdowns_since_last_service;     // Falhas desde último serviço
byte breakdown_chance;                  // Chance atual de falha
```

**Sistema de Envelhecimento**:
- Veículos perdem confiabilidade com o tempo
- `breakdown_ctr`: Conta ticks até próxima falha potencial
- `breakdown_chance`: Aumenta com idade e diminui após serviço
- Serviço em depósitos restaura confiabilidade e reseta contadores

#### Aparência e Identificação

```cpp
SpriteID colourmap;                 // Mapeamento de cores cacheado
byte spritenum;                     // Índice do sprite (0xfd = custom)
UnitID unitnumber;                  // Número da unidade (ex: "Truck #42")

byte x_extent, y_extent, z_extent;  // Dimensões da bounding box
int8 x_bb_offs, y_bb_offs;          // Offsets da bounding box
int8 x_offs, y_offs;                // Offsets do sprite
```

**Customização Visual**:
- `spritenum`: Permite sprites customizados via NewGRF
- `colourmap`: Define esquema de cores da empresa
- Bounding boxes: Controlam área de redraw e colisão

#### Carga e Capacidade

```cpp
CargoID cargo_type;                 // Tipo de carga transportada
byte cargo_subtype;                 // Subtipo (para refits de livery)
uint16 cargo_cap;                   // Capacidade total
uint16 refit_cap;                   // Capacidade remanescente de refit anterior

VehicleCargoList cargo;             // Lista detalhada da carga atual
uint16 cargo_age_counter;           // Ticks até envelhecer carga
int8 trip_occupancy;                // Ocupação da viagem atual (NOSAVE)
```

**Sistema de Carga Complexo**:
- `VehicleCargoList`: Contém detalhes de cada pacote de carga (origem, destino, valor)
- `refit_cap`: Rastreia capacidade não utilizada após mudança de tipo de carga
- `trip_occupancy`: Estatística para avaliação de desempenho da rota

#### Contadores e Timing

```cpp
byte day_counter;       // Incrementado diariamente
byte tick_counter;      // Incrementado a cada tick
byte running_ticks;     // Ticks em movimento hoje
```

**Uso**:
- `day_counter`: Para eventos diários (ex: envelhecimento)
- `tick_counter`: Para timing preciso de ações
- `running_ticks`: Calcula quanto o veículo operou hoje

#### Status e Ordens

```cpp
byte vehstatus;                     // Status atual (VehStatus bitmask)
Order current_order;                // Ordem atual sendo executada

OrderList *orders;                  // Lista de ordens do veículo
// ou
Order *old_orders;                  // Apenas para savegames antigos

uint16 load_unload_ticks;           // Ticks para próximo ciclo de carga/descarga
GroupID group_id;                   // Grupo ao qual pertence
byte subtype;                       // Subtipo específico (avião, desastre, etc.)
```

**Sistema de Ordens**:
- `current_order`: Ordem ativa no momento (ex: "indo para Estação X")
- `orders`: Ponteiro para lista compartilhada (múltiplos veículos podem compartilhar)
- `load_unload_ticks`: Controla tempo gasto carregando/descarregando

#### Caches e Otimizações

```cpp
NewGRFCache grf_cache;              // Cache de valores NewGRF
VehicleCache vcache;                // Cache de valores do veículo
MutableSpriteCache sprite_cache;    // Cache de sprites e renderização
```

**Performance First**:
- Três camadas de cache para evitar recálculos
- Invalidados seletivamente quando dados mudam
- Crítico para performance com milhares de veículos

### Métodos Principais - Ciclo de Vida

#### Construtor e Destruidor

```cpp
Vehicle(VehicleType type = VEH_INVALID);
void PreDestructor();
virtual ~Vehicle();
```

**Fluxo**:
1. Construtor inicializa todos os membros com valores padrão
2. `PreDestructor()`: Limpeza especial antes da destruição
3. Destruidor remove de hashes, libera memória, notifica sistemas

#### Métodos de Carregamento/Descarregamento

```cpp
void BeginLoading();                              // Inicia processo de carga
void CancelReservation(StationID next, Station *st); // Cancela reserva de plataforma
void LeaveStation();                              // Sai da estação
void HandleLoading(bool mode = false);            // Processa ciclo de carga/descarga
```

**Lógica de Operação em Estações**:
1. `BeginLoading()`: Reserva plataforma, prepara para carga
2. `HandleLoading()`: Executa carga/descarga baseada em ordens
3. `LeaveStation()`: Libera plataforma, retoma viagem
4. `CancelReservation()`: Emergência - libera plataforma se necessário

#### Métodos de Atualização e Renderização

```cpp
virtual void MarkDirty();                         // Marca para redesenho
virtual void UpdateDeltaXY();                     // Atualiza offsets do sprite
inline void UpdateViewport(bool dirty);           // Atualiza viewport
void UpdatePosition();                            // Atualiza posição no mapa
void UpdateBoundingBoxCoordinates(bool update_cache); // Atualiza bounding box
void UpdatePositionAndViewport();                 // Atualiza ambos
```

**Pipeline de Renderização**:
1. `UpdatePosition()`: Calcula nova posição baseada em velocidade
2. `UpdateDeltaXY()`: Determina offsets do sprite para nova posição
3. `UpdateBoundingBoxCoordinates()`: Calcula área ocupada na tela
4. `MarkDirty()`: Notifica sistema que área precisa ser redesenhada
5. `UpdateViewport()`: Efetivamente redesenha se visível

#### Métodos de Movimento - Sistema Antigo vs Novo

```cpp
// Sistema ANTIGO (ainda usado em alguns casos)
inline uint GetOldAdvanceSpeed(uint speed) {
    return (this->direction & 1) ? speed : speed * 3 / 4;
}

// Sistema NOVO (recomendado)
static inline uint GetAdvanceSpeed(uint speed) {
    return speed * 3 / 4;
}

inline uint GetAdvanceDistance() {
    return (this->direction & 1) ? TILE_AXIAL_DISTANCE : TILE_CORNER_DISTANCE * 2;
}
```

**Evolução do Sistema de Movimento**:
- **Antigo**: Velocidade era escalada por direção, causava problemas em curvas
- **Novo**: Separa velocidade (`GetAdvanceSpeed`) de distância necessária (`GetAdvanceDistance`)
- **Vantagem**: Progresso residual não precisa adaptação ao mudar direção
- **Direções**: `(direction & 1)` verifica se é diagonal (ímpar) ou cardinal (par)

#### Métodos Virtuais - Sobrescritos por Tipos Específicos

```cpp
virtual uint16 GetMaxWeight() const { return 0; }
virtual ExpensesType GetExpenseType(bool income) const { return EXPENSES_OTHER; }
virtual void PlayLeaveStationSound(bool force = false) const {}
virtual bool IsPrimaryVehicle() const { return false; }
virtual void GetImage(Direction direction, ...) const { result->Clear(); }
virtual int GetDisplaySpeed() const { return 0; }
virtual int GetDisplayMaxSpeed() const { return 0; }
virtual int GetCurrentMaxSpeed() const { return 0; }
virtual Money GetRunningCost() const { return 0; }
virtual bool IsInDepot() const { return false; }
virtual bool Tick() { return true; }
virtual void OnNewDay() {}
virtual uint Crash(bool flooded = false);
virtual Trackdir GetVehicleTrackdir() const { return INVALID_TRACKDIR; }
virtual TileIndex GetOrderStationLocation(StationID station) { return INVALID_TILE; }
virtual bool FindClosestDepot(...) { return false; }
```

**Padrão Template Method**:
- Classe base fornece implementação padrão (muitas vezes vazia ou retornando 0)
- Classes derivadas (Train, Aircraft, etc.) sobrescrevem conforme necessário
- Exemplo: `IsPrimaryVehicle()` retorna `true` apenas para locomotivas líderes
- `GetImage()`: Cada tipo implementa sua própria lógica de sprite

#### Métodos de Navegação na Cadeia

```cpp
inline Vehicle *Next() const { return this->next; }
inline Vehicle *Previous() const { return this->previous; }
inline Vehicle *First() const { return this->first; }
inline Vehicle *Last();
inline Vehicle *Move(int n);  // Move n posições na cadeia
```

**Utilitários de Iteração**:
- Permitem navegar facilmente por trens compostos de múltiplos veículos
- `Move(n)`: Avança ou retrocede n posições (negativo = retrocede)
- Essencial para operações em consists completos

#### Métodos de Ordens Compartilhadas

```cpp
void AddToShared(Vehicle *shared_chain);
void RemoveFromShared();

inline Vehicle *NextShared() const { return this->next_shared; }
inline Vehicle *FirstShared() const;
inline bool IsOrderListShared() const;
inline VehicleOrderID GetNumOrders() const;
inline StationIDStack GetNextStoppingStation() const;
```

**Sistema de Shared Orders**:
- Múltiplos veículos podem compartilhar mesma lista de ordens
- Útil para linhas com vários veículos operando em sequência
- `FirstShared()`: Retorna primeiro veículo na cadeia compartilhada
- Economia de memória: uma lista de ordens para múltiplos veículos

#### Métodos de Gerenciamento de Ordens

```cpp
void SkipToNextRealOrderIndex();  // Pula ordens implícitas
void IncrementImplicitOrderIndex(); // Avança ordem implícita
void IncrementRealOrderIndex();     // Avança ordem real
void UpdateRealOrderIndex();        // Garante índice válido

inline Order *GetOrder(int index) const;
inline Order *GetLastOrder() const;
IterateWrapper Orders() const;  // Iterator para loop for-each
```

**Ordens Implícitas vs Manuais**:
- **Manuais**: Adicionadas pelo jogador
- **Implícitas**: Geradas automaticamente (ex: "ir para depot" quando necessário)
- `cur_real_order_index`: Índice da próxima ordem manual
- `cur_implicit_order_index`: Índice da ordem atual (pode ser implícita)

#### Métodos de Subtipo de Veículo Terrestre

```cpp
inline bool IsFrontEngine() const;           // É locomotiva líder?
inline bool IsArticulatedPart() const;       // É parte articulada?
inline bool HasArticulatedPart() const;      // Tem parte articulada?
inline Vehicle *GetNextArticulatedPart() const;
inline Vehicle *GetFirstEnginePart();
inline Vehicle *GetLastEnginePart();
inline Vehicle *GetNextVehicle() const;      // Próximo veículo real
inline Vehicle *GetPrevVehicle() const;      // Veículo real anterior
```

**Hierarquia de Trens**:
```
Locomotiva (Front) → Parte Articulada → Vagão → Vagão
     ↓                    ↓                ↓         ↓
  GVSF_FRONT      GVSF_ARTICULATED    GVSF_WAGON  GVSF_WAGON
```

- `GetNextVehicle()`: Pula partes articuladas, vai para próximo veículo independente
- Essencial para lógica de consist e distribuição de peso/potência

#### Métodos de Utilidade e Informação

```cpp
const Engine *GetEngine() const;              // Obtém dados do motor
const GRFFile *GetGRF() const;                // Obtém arquivo NewGRF
uint32 GetGRFID() const;                      // Obtém ID do NewGRF

inline void InvalidateNewGRFCache();          // Invalida cache local
inline void InvalidateNewGRFCacheOfChain();   // Invalida cache de toda cadeia

inline bool IsGroundVehicle() const;          // É trem ou veículo rodoviário?

Money GetDisplayRunningCost() const;          // Custo para display
Money GetDisplayProfitThisYear() const;       // Lucro este ano para display
Money GetDisplayProfitLastYear() const;       // Lucro ano passado para display

void SetNext(Vehicle *next);                  // Define próximo veículo
```

#### Métodos de Manutenção e Serviço

```cpp
bool NeedsAutorenewing(const Company *c, ...) const;  // Precisa renovar?
bool NeedsServicing() const;                          // Precisa de serviço?
bool NeedsAutomaticServicing() const;                 // Precisa serviço automático?

CommandCost SendToDepot(DoCommandFlag flags, DepotCommand command); // Enviar para depot

void UpdateVisualEffect(bool allow_power_change = true); // Atualiza efeitos visuais
void ShowVisualEffect() const;                           // Mostra efeito atual
```

**Lógica de Manutenção**:
- `NeedsServicing()`: Verifica se intervalo de serviço foi atingido
- `NeedsAutorenewing()`: Verifica se veículo está obsoleto/velho
- `SendToDepot()`: Comando para enviar veículo para manutenção
- Efeitos visuais atualizados baseado no tipo de motor e estado

#### Métodos de Colisão e Acidentes

```cpp
virtual uint Crash(bool flooded = false);  // Destroi veículo (retorna almas perdidas)
bool HandleBreakdown();                    // Processa falha mecânica
```

**Sistema de Acidentes**:
- `Crash()`: Destrói veículo, calcula casualties, spawn veículos de emergência
- `HandleBreakdown()`: Aplica penalidades de quebra, agenda reparos
- `flooded`: Se verdadeiro, causa foi inundação (sem casualties)

#### Métodos de Predição de Refit

```cpp
void ResetRefitCaps();  // Reseta capacidades de refit

// Estrutura auxiliar para predição
struct RefitDesc {
    CargoID cargo;    // Tipo de carga após refit
    uint16 capacity;  // Capacidade após refit
    uint16 remaining; // Capacidade sobrando do refit anterior
    
    RefitDesc(CargoID cargo, uint16 capacity, uint16 remaining);
};
```

**Refit (Reconfiguração de Carga)**:
- Permite mudar tipo de carga que veículo pode transportar
- `RefitDesc`: Usado para prever resultado de refits futuros
- Importante para planejamento de rotas e logística

### SpecializedVehicle - Template para Tipos Específicos

```cpp
template <class T, VehicleType Type>
struct SpecializedVehicle : public Vehicle {
    static const VehicleType EXPECTED_TYPE = Type;
    
    inline SpecializedVehicle<T, Type>() : Vehicle(Type) { ... }
    
    inline T *First() const { return (T *)this->Vehicle::First(); }
    inline T *Next() const { return (T *)this->Vehicle::Next(); }
    // ... muitos outros métodos com casting automático ...
    
    static inline T *Get(size_t index);
    static inline T *GetIfValid(size_t index);
    static inline T *From(Vehicle *v);
    static inline Pool::IterateWrapper<T> Iterate(size_t from = 0);
};
```

**Padrão CRTP (Curiously Recurring Template Pattern)**:
- Permite casting seguro e automático entre Vehicle base e tipos derivados
- Exemplo de uso: `class Train : public SpecializedVehicle<Train, VEH_TRAIN>`
- Benefícios:
  - Type safety em tempo de compilação
  - Elimina necessidade de casts manuais repetitivos
  - Métodos como `Get()` retornam tipo correto automaticamente
  - Iteradores tipados para collections de veículos específicos

**Exemplo Prático**:
```cpp
// Sem SpecializedVehicle:
Vehicle *v = Vehicle::Get(id);
Train *t = (Train*)v;  // Cast manual, propenso a erros
if (t->type != VEH_TRAIN) error!

// Com SpecializedVehicle:
Train *t = Train::Get(id);  // Casting automático e seguro
// Ou:
Train *t = Train::From(v);  // Verifica tipo em runtime com assert
```

### FreeUnitIDGenerator - Gerador de Números de Unidade

```cpp
struct FreeUnitIDGenerator {
    bool *cache;   // Array de IDs ocupados
    UnitID maxid;  // ID máximo atual
    UnitID curid;  // Último ID retornado
    
    FreeUnitIDGenerator(VehicleType type, CompanyID owner);
    UnitID NextID();  // Obtém próximo ID livre
    ~FreeUnitIDGenerator();
};
```

**Propósito**:
- Gera números únicos para veículos (ex: "Bus #42", "Train #107")
- Mantém cache de IDs já utilizados para evitar duplicatas
- Por tipo de veículo e dono (empresa)
- Usado ao comprar novos veículos

---

## 🔄 Fluxos de Operação Principais

### Ciclo de Vida de um Veículo

```
1. CRIAÇÃO
   └─> ConstructorVehicle(type)
       └─> Inicializa todos os membros com valores padrão
       └─> Adiciona ao _vehicle_pool

2. OPERAÇÃO DIÁRIA
   └─> Tick() [chamado ~74 vezes por segundo]
       ├─> Move veículo baseado em velocidade
       ├─> Atualiza progress no tile
       ├─> Verifica chegada em estações/depots
       └─> HandleBreakdown() [se aplicável]
   
   └─> OnNewDay() [chamado uma vez por dia do jogo]
       ├─> Incrementa age
       ├─> Reduz reliability
       ├─> Atualiza estatísticas econômicas
       └─> Verifica necessidade de serviço

3. INTERAÇÃO COM ESTAÇÕES
   └─> BeginLoading()
       └─> Reserva plataforma
   └─> HandleLoading()
       ├─> Carrega carga disponível
       ├─> Descarrega carga destinada aqui
       └─> Calcula pagamento
   └─> LeaveStation()
       └─> Libera plataforma
       └─> Retoma viagem

4. MANUTENÇÃO
   └─> NeedsServicing() [verificado periodicamente]
       └─> Se verdadeiro: SendToDepot()
   └─> Em depot: Restaura reliability, conserta danos

5. DESTRUIÇÃO
   └─> PreDestructor()
       ├─> Remove de todas as hashes
       ├─> Cancela ordens
       └─> Notifica sistemas relacionados
   └─> ~Vehicle()
       └─> Libera memória do pool
```

### Sistema de Movimento Detalhado

```
TICK LOOP (74 Hz):
├─> 1. Calcular aceleração baseada em:
│      ├─> Potência do motor
│      ├─> Peso do consist
│      ├─> Inclinação do terreno
│      └─> Atrito/resistência
│
├─> 2. Atualizar cur_speed e subspeed
│
├─> 3. Calcular advance_distance:
│      └─> GetAdvanceSpeed(cur_speed)
│
├─> 4. Atualizar progress:
│      └─> progress += advance_distance
│
├─> 5. Se progress >= 256:
│      ├─> Mover para próximo tile/sub-position
│      ├─> progress -= 256
│      └─> Atualizar tile, x_pos, y_pos, z_pos
│
└─> 6. UpdateViewport() se mudou de posição
```

### Sistema de Carga e Pagamento

```
EM ESTAÇÃO:
├─> BeginLoading()
│   └─> Reservar slot na plataforma
│
├─> HandleLoading() [repetido até completar]
│   ├─> Se modo = CARREGAR:
│   │   ├─> Pegar carga da estação
│   │   ├─> Adicionar a VehicleCargoList
│   │   └─> Atualizar cargo_cap utilizada
│   │
│   ├─> Se modo = DESCARREGAR:
│   │   ├─> Remover carga com destino = esta estação
│   │   ├─> Calcular pagamento baseado em:
│   │   │   ├─> Tipo de carga
│   │   │   ├─> Distância percorrida
│   │   │   ├─> Tempo de entrega
│   │   │   └─> Demanda da cidade/indústria
│   │   └─> Adicionar profit_this_year
│   │
│   └─> Incrementar load_unload_ticks
│
└─> LeaveStation()
    └─> Liberar plataforma
```

---

## 📊 Resumo dos Conceitos-Chave

### 1. **Sistema de Pool de Veículos**
- Todos os veículos gerenciados em `_vehicle_pool`
- Alocação eficiente de memória para ~1 milhão de veículos
- IDs únicos (VehicleID) para acesso rápido

### 2. **Encadeamento de Veículos**
- Lista duplamente encadeada para veículos articulados
- Suporte a cadeias de ordens compartilhadas
- Ponteiros inteligentes para primeiro/último veículo

### 3. **Movimento Baseado em Progresso**
- Sistema híbrido tile + coordenadas precisas
- Progresso medido em unidades de 1/256
- Separação moderna entre velocidade e distância

### 4. **Cache Multi-Camada**
- NewGRFCache: Valores de scripts NewGRF
- VehicleCache: Propriedades computadas frequentemente
- SpriteCache: Dados de renderização
- Invalidação seletiva para performance

### 5. **Ordens Flexíveis**
- Sistema de ordens manuais e implícitas
- Compartilhamento de ordens entre veículos
- Iteradores para fácil navegação

### 6. **Economia Detalhada**
- Rastreamento de lucro por veículo
- Sistema de envelhecimento e confiabilidade
- Custos operacionais e de manutenção

### 7. **Renderização Otimizada**
- Bounding boxes para redraw mínimo
- Sprites compostos e recolouring
- Viewport candidates para culling

---

## 🔗 Arquivos Relacionados

### Dependências Diretas
- **vehicle.h**: Declarações forward e tipos específicos
- **order_base.h**: Sistema de ordens
- **cargopacket.h**: Gestão de pacotes de carga
- **engine_type.h**: Definições de motores
- **group_type.h**: Sistema de grupos de veículos

### Implementações Específicas
- **train.h/.cpp**: Trens e ferrovias
- **roadveh.h/.cpp**: Veículos rodoviários
- **aircraft.h/.cpp**: Aviões e aeroportos
- **ship.h/.cpp**: Navios e docas

### Sistemas Integrados
- **station.h**: Estações e plataformas
- **depot.h**: Depósitos e manutenção
- **newgrf.h**: Extensões NewGRF
- **pathfinder.h**: Sistema de pathfinding

---

## 💡 Notas de Implementação

### Thread Safety
- ⚠️ **Não é thread-safe**
- Assume execução single-threaded (típico do OpenTTD)
- Modificações externas requerem travamento manual

### Savegame Compatibility
- Ponteiros `NOSAVE` são reconstruídos no carregamento
- Estrutura persistida via sistema SlVehicle*
- Versões antigas suportadas via `old_orders`

### Performance Considerations
- Método `Tick()` chamado ~74× por segundo por veículo
- Otimizações críticas em caches e bounding boxes
- Evitar alocações dinâmicas durante operação normal

### Extensibilidade
- Virtual methods permitem extensão via NewGRF
- SpecializedVehicle facilita adição de novos tipos
- RefitDesc suporta sistemas complexos de carga

---

## 🎓 Glossário

| Termo | Definição |
|-------|-----------|
| **Consist** | Composição completa de um trem (locomotiva + vagões) |
| **Tile** | Unidade básica do mapa (74×74 pixels) |
| **Tick** | Unidade de tempo do jogo (~74 ticks = 1 segundo real) |
| **NewGRF** | Sistema de modificações/extensões criado pela comunidade |
| **Refit** | Reconfigurar veículo para transportar diferente tipo de carga |
| **Pathfinder** | Algoritmo que calcula rotas ótimas para veículos |
| **Viewport** | Área visível da tela onde o jogo é renderizado |
| **Bounding Box** | Retângulo que delimita área ocupada por sprite |
| **Palette/Pal** | Tabela de cores aplicada a sprites |
| **Service Interval** | Período entre manutenções em depósitos |

---

**Fim da documentação conceitual de `vehicle_base.h`**

*Próximos arquivos sugeridos: `vehicle.h`, `train.h`, `roadveh.h`*
