<!--
================================================================================
ARQUIVO: vehicle_type.h.md
NÍVEL: 1 - Crítico
CATEGORIA: Tipos Fundamentais de Veículos
LINHAS ORIGINAIS: 95
PROPÓSITO: Define tipos, enums e constantes fundamentais para todos os veículos
INTERAÇÕES: 
  - vehicle_base.h (usa VehicleType)
  - aircraft.h (usa VehicleType)
  - train.h, roadveh.h, ship.h (usam VehicleType)
  - core/enum_type.hpp (macros de enum)
================================================================================
-->

# vehicle_type.h - Tipos de Veículos

## 📋 Visão Geral

Este arquivo define os **tipos fundamentais** e **constantes universais** usados por todo o sistema de veículos do OpenTTD. É um arquivo de cabeçalho essencial que estabelece a base tipológica para trens, veículos rodoviários, navios e aeronaves.

---

## 🔢 Constantes Fundamentais

### `GROUND_ACCELERATION = 9800`
```cpp
static const int GROUND_ACCELERATION = 9800;
```
**Significado**: Aceleração gravitacional na superfície terrestre (9.8 m/s²)
- Usado em cálculos de física para veículos terrestres
- Valor multiplicado por 1000 para precisão em ponto fixo
- Fundamental para modelos de aceleração realística

### `INVALID_VEHICLE = 0xFFFFF`
```cpp
static const VehicleID INVALID_VEHICLE = 0xFFFFF;
```
**Significado**: ID especial que representa um veículo inexistente ou inválido
- Usado como valor sentinel em validações
- Equivalente a `nullptr` para IDs de veículos
- Previne acesso a memória inválida

### `MAX_LENGTH_VEHICLE_NAME_CHARS = 32`
```cpp
static const uint MAX_LENGTH_VEHICLE_NAME_CHARS = 32;
```
**Significado**: Comprimento máximo de nomes de veículos (incluindo null terminator)
- Limita buffer de strings de nomes
- Garante consistência em UI e salvamento
- 31 caracteres úteis + 1 caractere nulo

### `VEHICLE_LENGTH = 8`
```cpp
static const uint VEHICLE_LENGTH = 8;
```
**Significado**: Comprimento padrão de um veículo em unidades de tile
- Cada tile = 16 unidades no OpenTTD
- Veículo padrão ocupa meio tile (8/16)
- Usado para cálculo de ocupação de espaço em depots e trilhos

---

## 🏷️ Enumerações Principais

### `VehicleType` - Tipos de Veículos (8-bit)

```cpp
enum VehicleType : byte {
    VEH_BEGIN,              // = 0, início da enumeração
    
    VEH_TRAIN = VEH_BEGIN,  // = 0, Trens
    VEH_ROAD,               // = 1, Veículos Rodoviários
    VEH_SHIP,               // = 2, Navios
    VEH_AIRCRAFT,           // = 3, Aeronaves
    
    VEH_COMPANY_END,        // = 4, Último tipo pertencente a empresas
    
    VEH_EFFECT = VEH_COMPANY_END,  // = 4, Efeitos (fumaça, explosões)
    VEH_DISASTER,                    // = 5, Veículos de desastre
    
    VEH_END,                // = 6, Fim da enumeração
    VEH_INVALID = 0xFF      // = 255, Tipo inválido
};
```

#### Lógica e Categorias:

**🚂 Veículos Controláveis por Empresas (0-3):**
- `VEH_TRAIN`: Locomotivas e vagões em trilhos
- `VEH_ROAD`: Ônibus, caminhões, táxis em estradas
- `VEH_SHIP`: Barcos e navios em água
- `VEH_AIRCRAFT`: Aviões e helicópteros no ar

**✨ Veículos Especiais (4-5):**
- `VEH_EFFECT`: Partículas visuais (fumaça de trem, faíscas, bolhas)
  - Não pertence a nenhuma empresa
  - Destruído automaticamente após animação
- `VEH_DISASTER`: Eventos catastróficos (acidentes, objetos caindo)
  - Controlado pelo jogo, não por jogadores
  - Usado para efeitos dramáticos

**⚠️ Valores Especiais:**
- `VEH_BEGIN`: Marcador inicial (sempre 0)
- `VEH_COMPANY_END`: Limite entre veículos de empresas e especiais
- `VEH_END`: Total de tipos válidos (usado em iterações)
- `VEH_INVALID`: Valor sentinel para erros ou dados não inicializados

#### Por que 8-bit?
```cpp
/** It needs to be 8bits, because we save and load it as such */
```
- Compatibilidade com arquivos de salvamento
- Economiza memória em grandes frotas
- Permite até 256 tipos (atualmente usa apenas 6)

---

### `VehiclePathFinders` - Sistemas de Pathfinding

```cpp
enum VehiclePathFinders {
    VPF_NPF  = 1,  ///< New PathFinder
    VPF_YAPF = 2,  ///< Yet Another PathFinder
};
```

**Contexto Histórico:**
- Originalmente existia `OPF` (Original PathFinder) = 0
- Obsoleto e removido, mas valores mantidos para compatibilidade

**Sistemas Atuais:**
- **NPF (1)**: Pathfinding baseado em A* clássico
  - Mais preciso, porém mais lento
  - Usado em situações específicas
- **YAPF (2)**: Otimização do NPF com heurísticas avançadas
  - Balanceia performance e precisão
  - Padrão para maioria dos veículos

---

### `DepotCommand` - Comandos de Ir para Depot

```cpp
enum class DepotCommand : byte {
    None         = 0,         ///< Sem flags especiais
    Service      = (1U << 0), ///< Apenas serviço, sai logo após chegada
    MassSend     = (1U << 1), ///< Comando em massa (tipo em VLW flag)
    DontCancel   = (1U << 2), ///< Não cancelar comando atual se existir
    LocateHangar = (1U << 3), ///< Buscar outro aeroporto se alvo não tem hangar
};
```

**Flags Bitwise (podem ser combinadas):**

| Flag | Valor | Descrição | Caso de Uso |
|------|-------|-----------|-------------|
| `None` | 0b0000 | Nenhum comportamento especial | Operação normal |
| `Service` | 0b0001 | Entra e sai imediatamente | Reabastecimento rápido |
| `MassSend` | 0b0010 | Parte de envio em lote | Ctrl+click em múltiplos veículos |
| `DontCancel` | 0b0100 | Mantém comando anterior | Proteção contra sobrescrita |
| `LocateHangar` | 0b1000 | Procura hangar alternativo | Aeroporto sem manutenção |

**Exemplo de Combinação:**
```cpp
DepotCommand cmd = DepotCommand::Service | DepotCommand::LocateHangar;
// Veículo vai para serviço e busca hangar alternativo se necessário
```

---

### `AccelerationModel` - Modelos de Aceleração

```cpp
enum AccelerationModel {
    AM_ORIGINAL,    ///< Modelo arcade original do Transport Tycoon
    AM_REALISTIC,   ///< Modelo físico realístico
};
```

**Diferenças:**
- **AM_ORIGINAL**: 
  - Aceleração constante independente da velocidade
  - Mais simples, menos preciso
  - Estilo "arcade" do jogo original
  
- **AM_REALISTIC**:
  - Considera resistência do ar, atrito, peso
  - Aceleração diminui com aumento da velocidade
  - Usa `GROUND_ACCELERATION` como base física

---

### `EngineImageType` - Contextos de Visualização

```cpp
enum EngineImageType {
    EIT_ON_MAP     = 0x00,  ///< Veículo desenhado no viewport (mapa)
    EIT_IN_DEPOT   = 0x10,  ///< Veículo desenhado dentro do depot
    EIT_IN_DETAILS = 0x11,  ///< Detalhes do veículo, janela de refit
    EIT_IN_LIST    = 0x12,  ///< Listas de veículos, grupos
    EIT_PURCHASE   = 0x20,  ///< Lista de compra, substituição automática
    EIT_PREVIEW    = 0x21,  ///< Janela de preview, notícias
};
```

**Padrão de Codificação:**
- `0x00-0x0F`: Contextos de jogo ativo (mapa, depot)
- `0x10-0x1F`: Contextos de gerenciamento detalhado
- `0x20-0x2F`: Contextos de compra/preview

**Por que isso importa?**
- Diferentes níveis de detalhe gráfico para cada contexto
- Otimização de performance (menos detalhes em listas)
- Sprites diferentes podem ser usados em cada situação

---

## 🏗️ Estruturas e Tipos

### `VehicleID`
```cpp
typedef uint32 VehicleID;
```
- Identificador único de 32 bits para cada veículo
- Permite até ~4 bilhões de veículos teóricos
- Usado em todas as referências cruzadas entre sistemas

### `BaseVehicle`
```cpp
struct BaseVehicle {
    VehicleType type;  ///< Tipo de veículo
};
```
**Propósito**: Classe base mínima contendo apenas o tipo
- Usada em contextos onde apenas o tipo importa
- Evita necessidade de polimorfismo completo em operações simples
- Economia de memória em arrays grandes

### Forward Declarations
```cpp
struct Vehicle;
struct Train;
struct RoadVehicle;
struct Ship;
struct Aircraft;
struct EffectVehicle;
struct DisasterVehicle;
```
**Técnica**: Declarações antecipadas para evitar inclusão circular
- Permite usar ponteiros/referências sem incluir headers completos
- Reduz dependências de compilação
- Melhora tempo de build

---

## 🔄 Fluxo de Uso Típico

### 1. Criação de Veículo
```cpp
// Verifica tipo válido
if (vehicleType >= VEH_END || vehicleType == VEH_INVALID) {
    return false;  // Tipo inválido
}

// Cria veículo apropriado
switch (vehicleType) {
    case VEH_TRAIN:    new Train();    break;
    case VEH_ROAD:     new RoadVehicle(); break;
    case VEH_SHIP:     new Ship();     break;
    case VEH_AIRCRAFT: new Aircraft(); break;
    case VEH_EFFECT:   new EffectVehicle(); break;
    case VEH_DISASTER: new DisasterVehicle(); break;
}
```

### 2. Comando de Depot
```cpp
// Envia veículo para serviço
DepotCommand cmd = DepotCommand::Service;

// Se for aeronave, procura hangar alternativo
if (vehicle.type == VEH_AIRCRAFT) {
    cmd |= DepotCommand::LocateHangar;
}

vehicle.SetDepotCommand(cmd);
```

### 3. Renderização Condicional
```cpp
// Escolhe sprite baseado no contexto
SpriteID GetVehicleImage(Vehicle *v, EngineImageType eit) {
    switch (eit) {
        case EIT_ON_MAP:   return v->map_sprite;      // Detalhado
        case EIT_IN_LIST:  return v->list_icon;       // Simplificado
        case EIT_PURCHASE: return v->purchase_image;  // Com informações de preço
        // ...
    }
}
```

---

## 🎯 Conceitos-Chave Resumidos

| Conceito | Importância | Aplicação Principal |
|----------|-------------|---------------------|
| **VehicleType** | ⭐⭐⭐⭐⭐ | Classificação fundamental de todos os veículos |
| **INVALID_VEHICLE** | ⭐⭐⭐⭐ | Validação de segurança em todas as operações |
| **DepotCommand** | ⭐⭐⭐⭐ | Sistema de manutenção e reparo |
| **VEHICLE_LENGTH** | ⭐⭐⭐ | Layout de depots, estações, sinais |
| **EngineImageType** | ⭐⭐⭐ | Otimização gráfica e UX |
| **PathFinders** | ⭐⭐⭐⭐ | IA de navegação e rotas |

---

## 📁 Arquivos Relacionados

### Dependências Diretas:
- `core/enum_type.hpp` - Macros `DECLARE_POSTFIX_INCREMENT`, `EnumPropsT`
- `vehicle_base.h` - Estrutura base que usa `VehicleType`
- `vehicle.h` - Classe principal de veículo

### Arquivos que Usam Este:
- `train.h`, `roadveh.h`, `ship.h`, `aircraft.h` - Todos usam `VehicleType`
- `depot_cmd.cpp` - Implementa comandos de depot
- `vehicle_gui.cpp` - Renderização baseada em `EngineImageType`
- `pathfinder/` - Sistemas NPF e YAPF

---

## 💡 Notas de Implementação

### Compatibilidade de Save/Load
```cpp
/** Available vehicle types. It needs to be 8bits, because we save and load it as such */
```
- Mudar tamanho do enum quebraria saves antigos
- Valores numéricos são escritos diretamente no arquivo
- Manter estabilidade é crítico para jogos de longa duração

### Design de Enums Moderno
- `enum class DepotCommand` vs `enum VehiclePathFinders`
- `enum class` (scoped enum) previne poluição de namespace
- Enums antigos mantidos por compatibilidade
- Transição gradual para moderno C++11

### Performance
- `byte` para `VehicleType` economiza 3 bytes por veículo
- Em frota de 10.000 veículos = 30KB economizados
- Multiplicado por milhões de tiles e estruturas = MBs significativos

---

## 🚀 Próximos Passos Sugeridos

Após entender os tipos de veículos, prossiga para:
1. **vehicle_func.h** - Funções utilitárias que operam nestes tipos
2. **vehicle_cmd.h** - Comandos que manipulam veículos
3. **train.h / roadveh.h / ship.h** - Implementações específicas por tipo

---

**Status da Tradução**: ✅ Completa  
**Complexidade**: Baixa-Média (definições puras, pouca lógica)  
**Prioridade**: Nível 1 - Crítico (fundação do sistema de veículos)
