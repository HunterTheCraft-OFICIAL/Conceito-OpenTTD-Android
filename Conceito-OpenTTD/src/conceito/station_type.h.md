<!--
================================================================================
ARQUIVO: station_type.h
NÍVEL: 1
SUBCATEGORIA: Tipos Fundamentais de Estações
LINGUAGEM ORIGINAL: C++
PROPÓSITO: Definir os tipos básicos, enums e estruturas relacionadas a estações.
           Este arquivo estabelece o vocabulário para estações de trem, aeroporto,
           rodoviárias, portos e waypoints.
INTERAÇÕES: station.h, station_base.h, tilearea_type.h, waypoint.h
VARIÁVEIS_PRINCIPAIS: StationID, INVALID_STATION, StationType, StationFacility
ESTRUTURAS: StationFinder, StationCompare
FUNÇÕES_CHAVE: GetStations()
================================================================================
-->

# station_type.h - Tipos de Estações

## Visão Geral

Este arquivo define **o vocabulário fundamental** para o sistema de estações do OpenTTD. Ele estabelece:
- Como identificar estações unicamente (StationID)
- Que tipos de estações existem (trem, aeroporto, porto, etc.)
- Quais facilidades cada estação pode ter
- Como encontrar estações próximas em uma área

**Importância**: Sem este arquivo, o jogo não poderia diferenciar entre tipos de estações nem gerenciar a infraestrutura de transporte.

---

## Tipos e Identificadores Básicos

### StationID - Identificador de Estação

```cpp
typedef uint16 StationID;
typedef uint16 RoadStopID;
```

**O que é**: Um número de 16 bits que identifica unicamente cada estação.

**Por que 16 bits**:
- Permite até 65.536 estações simultâneas
- Equilíbrio entre capacidade e uso de memória
- Suficiente para qualquer partida realista

**RoadStopID**:
- Tipo separado para pontos de parada de estrada (ônibus/caminhões)
- Mesma estrutura, mas semanticamente diferente
- Permite tratamento especializado

---

### Constantes de Validade

```cpp
static const StationID NEW_STATION = 0xFFFE;      // 65534
static const StationID INVALID_STATION = 0xFFFF;  // 65535
```

**NEW_STATION (0xFFFE)**:
- Usado quando criando uma NOVA estação
- Marca temporária antes de atribuir ID real
- Similar a "auto_increment" em bancos de dados

**INVALID_STATION (0xFFFF)**:
- Representa "nenhuma estação" ou "estação inexistente"
- Usado como valor nulo/error
- Escolhido por ser o máximo valor de uint16 (nunca será um ID válido)

---

### StationIDStack - Pilha de IDs

```cpp
typedef SmallStack<StationID, StationID, INVALID_STATION, 8, 0xFFFD> StationIDStack;
```

**O que é**: Uma pilha especializada para armazenar temporariamente IDs de estação.

**Parâmetros do SmallStack**:
- `StationID`: Tipo dos elementos
- `StationID`: Tipo do índice/contador
- `INVALID_STATION`: Valor usado para marcar posição vazia
- `8`: Capacidade inicial padrão
- `0xFFFD`: Valor sentinela adicional

**Casos de uso**:
- Durante construção de estações (tiles sendo adicionados)
- Processamento em lote de múltiplas estações
- Backtracking em algoritmos de busca

---

## Enums de Classificação

### StationType - Tipos de Estação

```cpp
enum StationType {
    STATION_RAIL,      // Estação ferroviária
    STATION_AIRPORT,   // Aeroporto
    STATION_TRUCK,     // Terminal de caminhões
    STATION_BUS,       // Rodoviária de ônibus
    STATION_OILRIG,    // Plataforma petrolífera
    STATION_DOCK,      // Porto/Doca
    STATION_BUOY,      // Boia (navegação)
    STATION_WAYPOINT,  // Waypoint (ponto de passagem)
};
```

**Classificação por Categoria**:

1. **Terrestre**:
   - `STATION_RAIL`: Trens - requer trilhos
   - `STATION_TRUCK`: Caminhões - requer estradas para carga
   - `STATION_BUS`: Ônibus - requer estradas para passageiros

2. **Aérea**:
   - `STATION_AIRPORT`: Aeronaves - requer grande área plana

3. **Aquática**:
   - `STATION_DOCK`: Navios de carga - requer água profunda
   - `STATION_BUOY`: Navios (waypoint) - marca rota aquática
   - `STATION_OILRIG`: Indústria offshore - extrai petróleo

4. **Navegação**:
   - `STATION_WAYPOINT`: Ponto de passagem genérico - não carrega/descarrega

**Por que diferenciar**:
- Cada tipo aceita veículos diferentes
- Regras de construção específicas
- Interações diferentes com indústria/cidades

---

### RoadStopType - Tipos de Parada de Estrada

```cpp
enum RoadStopType : byte {
    ROADSTOP_BUS,    // Parada de ônibus
    ROADSTOP_TRUCK,  // Parada de caminhão
    ROADSTOP_END,    // Fim dos tipos válidos
};
```

**Contexto**: Diferente de estações completas, road stops são paradas simples na estrada.

**Diferenças**:
- **Bus**: Aceita apenas ônibus (passageiros)
- **Truck**: Aceita apenas caminhões (carga)
- Não podem ser misturados na mesma parada

**ROADSTOP_END**:
- Marcador para iteração sobre enums
- Útil em loops: `for (type = 0; type < ROADSTOP_END; type++)`

---

### StationFacility - Facilidades da Estação (Bitmask)

```cpp
enum StationFacility : byte {
    FACIL_NONE       = 0,        // Sem facilidades
    FACIL_TRAIN      = 1 << 0,   // Plataforma de trem
    FACIL_TRUCK_STOP = 1 << 1,   // Área de caminhões
    FACIL_BUS_STOP   = 1 << 2,   // Área de ônibus
    FACIL_AIRPORT    = 1 << 3,   // Aeroporto
    FACIL_DOCK       = 1 << 4,   // Doca/porto
    FACIL_WAYPOINT   = 1 << 7,   // É um waypoint
};
DECLARE_ENUM_AS_BIT_SET(StationFacility)
```

**Lógica de Bitmask**:

Cada facilidade é um BIT diferente, permitindo combinações:

```
Byte: [7] [6] [5] [4] [3] [2] [1] [0]
      |   |   |   |   |   |   |   |   |
      |   |   |   |   |   |   |   +---+---+ FACIL_TRAIN
      |   |   |   |   |   +---+---+---+---+ FACIL_TRUCK_STOP
      |   |   |   +---+---+---+---+---+---+ FACIL_BUS_STOP
      |   |   +---+---+---+---+---+---+---+---+ FACIL_AIRPORT
      |   +---+---+---+---+---+---+---+---+---+ FACIL_DOCK
      +---+---+---+---+---+---+---+---+---+---+ (reservado)
      WAYPOINT (bit 7)
```

**Exemplos de Combinações**:

1. **Estação multimodal pequena**:
   ```
   FACIL_TRAIN | FACIL_BUS_STOP = 0b00000101 = 5
   ```
   → Tem plataforma de trem E ponto de ônibus

2. **Aeroporto com acesso terrestre**:
   ```
   FACIL_AIRPORT | FACIL_TRUCK_STOP | FACIL_BUS_STOP = 0b00001110 = 14
   ```
   → Aceita aviões, caminhões de carga E ônibus

3. **Waypoint puro**:
   ```
   FACIL_WAYPOINT = 0b10000000 = 128
   ```
   → Apenas ponto de passagem, sem carregamento

**FACIL_NONE**:
- Estação existe mas não tem facilidades ativas
- Estado temporário durante construção/destruição

**FACIL_WAYPOINT no bit 7**:
- Posicionado alto para não conflitar com facilidades reais
- Waypoints NÃO são estações verdadeiras (não carregam carga)

---

### StationHadVehicleOfType - Histórico de Veículos

```cpp
enum StationHadVehicleOfType : byte {
    HVOT_NONE     = 0,        // Nenhum veículo visitou
    HVOT_TRAIN    = 1 << 1,   // Trem já visitou
    HVOT_BUS      = 1 << 2,   // Ônibus já visitou
    HVOT_TRUCK    = 1 << 3,   // Caminhão já visitou
    HVOT_AIRCRAFT = 1 << 4,   // Aeronave já visitou
    HVOT_SHIP     = 1 << 5,   // Navio já visitou
    
    HVOT_WAYPOINT = 1 << 6,   // É waypoint (NewGRF apenas)
};
DECLARE_ENUM_AS_BIT_SET(StationHadVehicleOfType)
```

**Propósito**: Rastrear QUAIS TIPOS de veículos já visitaram esta estação.

**Por que importa**:

1. **Rating da estação**:
   - Estações que recebem múltiplos tipos têm melhor rating
   - Afeta quantidade de carga gerada

2. **Desbloqueio de conquistas**:
   - "Conecte todos os tipos de transporte"
   - Tracking estatístico

3. **NewGRF callbacks**:
   - Scripts podem reagir a histórico de visitas
   - Ex: Bônus se estação recebe navios E trens

**Diferença para StationFacility**:
- `StationFacility`: O que a estação TEM (infraestrutura)
- `StationHadVehicleOfType`: O que já VISITOU a estação (histórico)

**Exemplo**:
```
Uma estação pode ter:
- FACIL_TRAIN (tem plataforma)
- HVOT_TRAIN | HVOT_TRUCK (trens e caminhões já vieram)
```

---

### CatchmentArea - Áreas de Influência

```cpp
enum CatchmentArea {
    CA_NONE       =  0,  // Sem área de influência
    CA_BUS        =  3,  // Parada de ônibus
    CA_TRUCK      =  3,  // Parada de caminhão
    CA_TRAIN      =  4,  // Estação de trem
    CA_DOCK       =  5,  // Doca/porto
    
    CA_UNMODIFIED =  4,  // Área padrão (quando modificado está desligado)
    
    MAX_CATCHMENT = 10,  // Máximo (aeroportos grandes)
};
```

**O que é Catchment Area**:

A "área de influência" de uma estação é a região ao redor dela onde:
- Edifícios geram carga/passageiros para ESTA estação
- A estação "coleta" produção de indústrias próximas
- Compete com outras estações por recursos

**Tamanhos Relativos**:

```
CA_BUS/TRUCK (3):    [███] Pequena - só quarteirão imediato
CA_TRAIN (4):        [████] Média - vários quarteirões
CA_DOCK (5):         [█████] Grande - área portuária
CA_AIRPORT (10):     [██████████] Enorme - cidade inteira
```

**CA_UNMODIFIED**:
- Usado quando configuração "modified catchment" está DESLIGADA
- Todas as estações têm tamanho padrão (4)
- Mais simples, menos realista

**Modified Catchment**:
- Quando LIGADO: cada tipo tem tamanho específico
- Mais realista: aeroportos influenciam mais que paradas de ônibus
- Configuração do jogo

---

### Constantes de Nome

```cpp
static const uint MAX_LENGTH_STATION_NAME_CHARS = 32;
```

**Propósito**: Limitar tamanho do nome da estação.

**Inclui**: Caractere nulo (`\0`) final.

**Na prática**: Jogador pode usar até 31 caracteres.

**Exemplos**:
- "Central Station" ✓ (15 chars)
- "London King's Cross Railway Station" ✗ (36 chars - truncado)

---

## Estruturas Especializadas

### StationCompare - Comparador para Ordenação

```cpp
struct StationCompare {
    bool operator() (const Station *lhs, const Station *rhs) const;
};
```

**Propósito**: Permitir ordenação de ponteiros de Station em containers.

**Por que necessário**:
- `std::set` e `std::map` precisam de critério de ordenação
- Ponteiros brutos comparam endereços de memória (não útil)
- Queremos ordenar por ID, nome, ou outro critério lógico

**Uso típico**:
```cpp
std::set<Station*, StationCompare> stations;
// Agora o set ordena estações logicamente, não por endereço
```

**Critério de comparação** (implementação em station.cpp):
- Primário: StationID (ordenamento numérico)
- Secundário: Nome (alfabético)

---

### StationList - Lista de Estações

```cpp
typedef std::set<Station *, StationCompare> StationList;
```

**O que é**: Container padronizado para coleções de estações.

**Por que `std::set`**:
- Garante unicidade (sem estações duplicadas)
- Mantém ordenado automaticamente
- Busca rápida O(log n)

**Casos de uso**:
- Lista de estações de uma empresa
- Estações conectadas a uma indústria
- Estações dentro de uma cidade

---

### StationFinder - Buscador de Estações Próximas

```cpp
class StationFinder : TileArea {
    StationList stations;  // Lista de estações próximas
public:
    StationFinder(const TileArea &area);
    const StationList *GetStations();
};
```

**Herança de TileArea**:
- `TileArea` define uma região retangular no mapa
- StationFinder "é um" TileArea com funcionalidade extra

**Funcionamento**:

1. **Construção**:
   ```cpp
   TileArea area(center_tile, radius);
   StationFinder finder(area);
   ```
   - Define área de busca
   - Internamente prepara para varredura

2. **Busca**:
   ```cpp
   const StationList *results = finder.GetStations();
   ```
   - Varre todos os tiles na área
   - Identifica quais pertencem a estações
   - Cacheia resultado em `stations`

3. **Lazy Evaluation**:
   - `stations` começa vazio
   - Preenchido apenas na primeira chamada a `GetStations()`
   - Evita trabalho desnecessário se nunca usado

**Casos de uso**:

1. **Construção de estação**:
   - Verificar estações próximas para mesclar
   - Checar distância mínima de outras estações

2. **Indústria gerando carga**:
   - Encontrar estações aceitantes próximas
   - Distribuir carga entre múltiplas estações

3. **Avaliação de cobertura**:
   - Quantas estações servem esta área?
   - Há "desertos" de transporte?

**Exemplo prático**:
```cpp
// Jogador clica para construir estação
TileIndex click_tile = ...;
TileArea search_area(click_tile, 5);  // Raio de 5 tiles
StationFinder finder(search_area);
const StationList *nearby = finder.GetStations();

if (nearby->empty()) {
    // Pode construir nova estação
} else {
    // Mostrar estações existentes, oferecer expansão
}
```

---

## Declarações Forward

```cpp
struct BaseStation;
struct Station;
struct RoadStop;
struct StationSpec;
struct Waypoint;
```

**Propósito**: Declarar existência sem definir detalhes.

**Por que fazer isso**:
- Permite usar ponteiros (`Station*`) neste arquivo
- Evita inclusão circular (station.h precisaria deste arquivo)
- Compilação mais rápida

**Onde são definidas**:
- `BaseStation`: station_base.h
- `Station`: station.h
- `RoadStop`: station.h
- `StationSpec`: newgrf_station.h (NewGRF specs)
- `Waypoint`: waypoint.h

---

## Fluxo Lógico de Uso

### Cenário 1: Construir Nova Estação

```
1. Jogador seleciona tipo (ex: STATION_RAIL)
2. Sistema verifica:
   - Terreno adequado
   - Distância de outras estações (StationFinder)
   - Funds disponíveis
3. Cria estação com:
   - Novo StationID (incremental)
   - facilities = FACIL_TRAIN
   - had_vehicle = HVOT_NONE
4. Retorna ID para referência futura
```

### Cenário 2: Veículo Chegando na Estação

```
1. Trem entra na estação
2. Sistema atualiza:
   - station->had_vehicle |= HVOT_TRAIN
   - station->facilities já tem FACIL_TRAIN
3. Se primeira vez que trem visita:
   - Atualiza rating da estação
   - Notifica jogador ("Nova estação conectada!")
4. Inicia loading/unloading baseado em:
   - cargo_type compatível
   - catchment area da estação
```

### Cenário 3: Calcular Produção de Carga

```
1. Indústria produz 10 toneladas de aço
2. Sistema chama StationFinder(area_industria)
3. Encontra 3 estações próximas:
   - Estação A: 200m, tem FACIL_TRAIN
   - Estação B: 500m, tem FACIL_TRAIN | FACIL_TRUCK
   - Estação C: 800m, tem FACIL_TRUCK
4. Distribui carga baseada em:
   - Distância (mais perto = mais provável)
   - Rating da estação
   - Tipo compatível (aço → trem preferencial)
5. Resultado: 70% A, 25% B, 5% C
```

---

## Hierarquia de Tipos Relacionados

```
station_type.h (ESTE ARQUIVO - Tipos e Enums)
    ↓
station_base.h (BaseStation struct)
    ↓
station.h (Station completa + funções)
    ↓
    ├─ station_cmd.cpp (Comandos de construção)
    ├─ station_gui.cpp (Interface)
    └─ newgrf_station.h (Customização NewGRF)

waypoint.h (Waypoint - tipo especial de estação)
roadstop.h (RoadStop - paradas de estrada simples)
```

---

## Relação com Outros Arquivos

### Dependências Diretas:

| Arquivo | O que fornece |
|---------|---------------|
| `tilearea_type.h` | Classe TileArea (base de StationFinder) |
| `core/smallstack_type.hpp` | SmallStack template |
| `<set>` | std::set para StationList |

### Arquivos que usam estes tipos:

- **station.h**: Define struct Station completa
- **station_base.h**: Define BaseStation
- **waypoint.h**: Usa StationID, StationType
- **roadstop.h**: Usa RoadStopID, RoadStopType
- **industry.h**: Usa StationFinder para achar estações próximas
- **cargoaction.cpp**: Usa StationFacility para validar carga
- **newgrf_station.cpp**: Usa StationHadVehicleOfType para callbacks

---

## Resumo Conceitual

Este arquivo é o **vocabulário das estações**:

| Conceito | Finalidade |
|----------|------------|
| `StationID` | Identificador único (0-65534) |
| `StationType` | Classificação principal (8 tipos) |
| `StationFacility` | O que a estação TEM (bitmask) |
| `StationHadVehicleOfType` | O que já VISITOU (histórico) |
| `CatchmentArea` | Tamanho da área de influência |
| `StationFinder` | Ferramenta de busca espacial |
| `StationList` | Container padronizado |

**Principais decisões de design**:

1. **IDs de 16 bits**: Equilíbrio entre capacidade e memória
2. **Bitmasks separadas**: Facilities vs Histórico permitem lógica rica
3. **Lazy evaluation**: StationFinder só trabalha se usado
4. **Tipos especializados**: RoadStopID separado de StationID para clareza

**Próximo nível**: `station_base.h` pega estes tipos e cria a struct BaseStation com dados comuns a todas as estações.
