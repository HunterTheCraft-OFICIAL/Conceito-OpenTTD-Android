# engine_type.h - Tipos de Motores/Engines

## 📋 Visão Geral

Este arquivo define os tipos fundamentais e estruturas relacionadas a **motores (engines)** no OpenTTD. Engines são os componentes de propulsão que podem ser acoplados a veículos para fornecer tração e capacidades especiais.

---

## 🔧 Definições de Tipo

### EngineID

```cpp
DECLARE_POSTFIX_INCREMENT(EngineID)
```

**Propósito**: Identificador único para cada motor/engine.

**Características**:
- Tipo postfix increment (similar a VehicleID, StationID)
- Começa em 0 e incrementa automaticamente
- Usado para indexar arrays e tabelas de engines
- `INVALID_ENGINE` representa um ID inválido

**Exemplo de Uso**:
```cpp
EngineID main_engine = 0;      // Primeiro engine
EngineID backup_engine = 5;    // Quinto engine
EngineID invalid = INVALID_ENGINE; // ID inválido
```

---

### EngineType

```cpp
enum EngineType : uint8_t {
    ENGINE_VEH_TRAIN,    // Motor para trens
    ENGINE_VEH_ROAD,     // Motor para veículos rodoviários
    ENGINE_VEH_SHIP,     // Motor para navios
    ENGINE_VEH_AIRCRAFT, // Motor para aeronaves
    ENGINE_TYPE_END      // Marcador de fim (não é um tipo válido)
};
```

**Propósito**: Classificar engines por tipo de veículo que podem propulsionar.

**Valores**:
| Valor | Constante | Descrição |
|-------|-----------|-----------|
| 0 | `ENGINE_VEH_TRAIN` | Motor para locomotivas e vagões de trem |
| 1 | `ENGINE_VEH_ROAD` | Motor para caminhões, ônibus, carros |
| 2 | `ENGINE_VEH_SHIP` | Motor para navios e barcos |
| 3 | `ENGINE_VEH_AIRCRAFT` | Motor para aeronaves e helicópteros |
| 4 | `ENGINE_TYPE_END` | Marcador de limite (count) |

**Uso em Código**:
```cpp
EngineType train_engine = ENGINE_VEH_TRAIN;
EngineType road_engine = ENGINE_VEH_ROAD;

// Iterar sobre todos os tipos
for (EngineType et = ENGINE_VEH_TRAIN; et < ENGINE_TYPE_END; et++) {
    // Processar cada tipo de engine
}
```

---

### EngineImageType

```cpp
enum EngineImageType : uint8_t {
    ENGINE_IMAGE_PREVIEW,    // Imagem de preview (vista prévia)
    ENGINE_IMAGE_INFO,       // Imagem informativa (detalhes)
    ENGINE_IMAGE_PURCHASE,   // Imagem de compra (loja)
    ENGINE_IMAGE_SELL,       // Imagem de venda
    ENGINE_IMAGE_BUILD,      // Imagem de construção
    ENGINE_IMAGE_RENAME,     // Imagem de renomeação
    ENGINE_IMAGE_COUNT       // Total de tipos de imagem
};
```

**Propósito**: Definir contextos diferentes para renderização de sprites de engines.

**Contextos**:
- **Preview**: Mostra o engine em tamanho reduzido antes da compra
- **Info**: Display detalhado com especificações técnicas
- **Purchase**: Interface da loja de compra de engines
- **Sell**: Interface de venda de engines usados
- **Build**: Visualização durante construção de veículos
- **Rename**: Display ao renomear o engine

---

## 🏗️ Estruturas Principais

### EngineStruct (Conceitual)

```cpp
struct EngineStruct {
    // Identificação
    EngineID id;              // ID único deste engine
    EngineType type;          // Tipo de veículo compatível
    string name;              // Nome do engine
    
    // Propriedades Técnicas
    uint16 power;             // Potência (kW ou HP)
    uint16 weight;            // Peso (toneladas)
    byte max_speed;           // Velocidade máxima (km/h dividido por 8)
    byte reliability;         // Confiabilidade (0-255)
    
    // Economia
    Money cost;               // Custo de compra
    Money running_cost;       // Custo de operação anual
    byte fuel_consumption;    // Consumo de combustível
    
    // Ciclo de Vida
    Date intro_date;          // Data de introdução no jogo
    Date expiry_date;         // Data de expiração (obsoleto)
    bool is_available;        // Disponível para compra
    
    // Capacidades Especiais
    CargoID cargo_capacity;   // Capacidade de carga (se aplicável)
    bitset features;          // Features especiais (bitset)
    
    // NewGRF
    GRFFile *grf;             // Arquivo NewGRF associado
    uint32 grf_id;            // ID do NewGRF
    uint16 grf_local_id;      // ID local dentro do NewGRF
};
```

**Campos Explicados**:

#### Seção: Identificação
- `id`: Identificador único global
- `type`: Categoria do engine (trem, road, ship, aircraft)
- `name`: Nome exibido na interface

#### Seção: Propriedades Técnicas
- `power`: Força de tração do motor
- `weight`: Massa do engine (afeta aceleração e consumo)
- `max_speed`: Velocidade máxima permitida
- `reliability`: Chance de não quebrar (255 = 100%)

#### Seção: Economia
- `cost`: Preço de compra inicial
- `running_cost`: Manutenção anual
- `fuel_consumption`: Quanto combustível consome

#### Seção: Ciclo de Vida
- `intro_date`: Quando fica disponível no mercado
- `expiry_date`: Quando sai de linha
- `is_available`: Pode ser comprado agora?

#### Seção: Capacidades Especiais
- `cargo_capacity`: Se transporta carga passageira
- `features`: Bits de capacidades extras (ex: múltiplos units)

#### Seção: NewGRF
- `grf`: Ponteiro para arquivo de mod
- `grf_id`: Identificador do mod
- `grf_local_id`: ID dentro do mod

---

## 📊 Constants Importantes

### INVALID_ENGINE

```cpp
const EngineID INVALID_ENGINE = UINT_MAX; // ou valor máximo de EngineID
```

**Propósito**: Representar um ID de engine inválido ou inexistente.

**Uso**:
```cpp
EngineID FindAvailableEngine(VehicleType type) {
    for (auto engine : engines) {
        if (engine.IsAvailable(type)) {
            return engine.id;
        }
    }
    return INVALID_ENGINE; // Nenhum encontrado
}
```

---

### MAX_ENGINGES

```cpp
const int MAX_ENGINES = 65536; // 2^16, limite máximo de engines
```

**Propósito**: Limite superior do número de engines no jogo.

**Motivação**:
- Baseado no tamanho do tipo `EngineID` (16 bits)
- Previne overflow de arrays
- Otimiza alocação de memória

---

## 🎯 Funções Conceituais

### IsValidEngine()

```cpp
bool IsValidEngine(EngineID eid) {
    return (eid >= 0 && eid < MAX_ENGINES && engines[eid].exists);
}
```

**Propósito**: Validar se um EngineID é válido e existe.

**Retorno**:
- `true`: Engine existe e é acessível
- `false`: ID inválido ou engine não existe

---

### IsEngineAvailable()

```cpp
bool IsEngineAvailable(EngineID eid, CompanyID company) {
    if (!IsValidEngine(eid)) return false;
    
    Engine &e = engines[eid];
    
    // Verifica disponibilidade temporal
    if (_date < e.intro_date) return false;
    if (_date > e.expiry_date && !e.is_experimental) return false;
    
    // Verifica disponibilidade para a empresa
    if (company != OWNER_NONE && !HasBit(e.companies_avail, company)) {
        return false;
    }
    
    return true;
}
```

**Propósito**: Determinar se um engine pode ser comprado por uma empresa específica.

**Critérios**:
1. Engine deve ser válido
2. Data atual deve estar dentro do período de disponibilidade
3. Empresa deve ter permissão (para engines exclusivos)

---

### GetEnginePower()

```cpp
uint16 GetEnginePower(EngineID eid) {
    if (!IsValidEngine(eid)) return 0;
    return engines[eid].power;
}
```

**Propósito**: Obter a potência de um engine específico.

**Retorno**: Potência em kW ou HP (dependendo da configuração).

---

### GetEngineWeight()

```cpp
uint16 GetEngineWeight(EngineID eid) {
    if (!IsValidEngine(eid)) return 0;
    return engines[eid].weight;
}
```

**Propósito**: Obter o peso de um engine específico.

**Importância**: Afeta:
- Aceleração do veículo
- Consumo de combustível
- Desgaste de trilhos/estradas

---

### GetEngineReliability()

```cpp
byte GetEngineReliability(EngineID eid) {
    if (!IsValidEngine(eid)) return 0;
    
    Engine &e = engines[eid];
    byte base_reliability = e.reliability;
    
    // Modificadores de confiabilidade
    if (e.age > e.max_age / 2) {
        base_reliability -= (e.age - e.max_age / 2) / 10;
    }
    
    return Clamp(base_reliability, 0, 255);
}
```

**Propósito**: Calcular confiabilidade atual considerando idade.

**Fatores**:
- Confiabilidade base do engine
- Idade do engine (mais velho = menos confiável)
- Mods e configurações personalizadas

---

## 🔄 Relacionamento com Outros Sistemas

### Com Vehicle System

```cpp
// Veículos usam engines para propulsão
struct Vehicle {
    EngineID engine_id;       // Engine atualmente equipado
    EngineType engine_type;   // Tipo compatível
    
    void SetEngine(EngineID eid) {
        if (IsEngineAvailable(eid, this->owner)) {
            this->engine_id = eid;
            RecalculateSpeed();
            RecalculatePower();
        }
    }
};
```

### Com Company System

```cpp
// Empresas pesquisam e desbloqueiam engines
struct Company {
    bitset<MAX_ENGINES> researched_engines;  // Engines pesquisados
    bitset<MAX_ENGINES> available_engines;   // Disponíveis para compra
    
    void ResearchEngine(EngineID eid) {
        SetBit(researched_engines, eid);
        SetBit(available_engines, eid);
    }
};
```

### Com NewGRF System

```cpp
// NewGRFs podem adicionar engines customizados
struct GRFFile {
    std::vector<EngineID> added_engines;
    
    void AddCustomEngine(EngineID eid) {
        added_engines.push_back(eid);
        engines[eid].grf = this;
    }
};
```

---

## 📝 Exemplos de Uso Prático

### Exemplo 1: Iterar sobre todos os engines de um tipo

```cpp
void ListAvailableTrains(CompanyID company) {
    for (EngineID eid = 0; eid < MAX_ENGINES; eid++) {
        if (!IsValidEngine(eid)) continue;
        
        Engine &e = engines[eid];
        
        // Filtrar apenas engines de trem
        if (e.type != ENGINE_VEH_TRAIN) continue;
        
        // Filtrar apenas disponíveis para esta empresa
        if (!IsEngineAvailable(eid, company)) continue;
        
        // Mostrar informações
        printf("Engine: %s\n", e.name.c_str());
        printf("  Power: %d kW\n", e.power);
        printf("  Weight: %d tons\n", e.weight);
        printf("  Max Speed: %d km/h\n", e.max_speed * 8);
        printf("  Cost: $%d\n", e.cost);
        printf("------------------------\n");
    }
}
```

### Exemplo 2: Selecionar melhor engine para um veículo

```cpp
EngineID SelectBestEngine(VehicleType vtype, Criteria criteria) {
    EngineID best_engine = INVALID_ENGINE;
    int best_score = -1;
    
    for (EngineID eid = 0; eid < MAX_ENGINES; eid++) {
        if (!IsEngineAvailable(eid, _local_company)) continue;
        
        Engine &e = engines[eid];
        if (e.type != GetEngineTypeForVehicle(vtype)) continue;
        
        // Calcular score baseado nos critérios
        int score = 0;
        
        if (criteria & CRITERIA_POWER) {
            score += e.power * 2;
        }
        
        if (criteria & CRITERIA_SPEED) {
            score += e.max_speed * 3;
        }
        
        if (criteria & CRITERIA_RELIABILITY) {
            score += e.reliability;
        }
        
        if (criteria & CRITERIA_COST) {
            score -= e.cost / 1000; // Menor custo = mais pontos
        }
        
        if (score > best_score) {
            best_score = score;
            best_engine = eid;
        }
    }
    
    return best_engine;
}
```

### Exemplo 3: Verificar compatibilidade engine-veículo

```cpp
bool IsEngineCompatibleWithVehicle(EngineID eid, Vehicle *v) {
    if (!IsValidEngine(eid)) return false;
    if (v == nullptr) return false;
    
    Engine &e = engines[eid];
    
    // Verificar tipo básico
    if (GetEngineTypeForVehicle(v->type) != e.type) {
        return false;
    }
    
    // Verificar restrições específicas
    if (v->type == VEH_TRAIN) {
        // Trens podem ter restrições de bitola
        if (e.gauge != v->gauge) {
            return false;
        }
        
        // Locomotivas vs vagões
        if (e.is_train_rail && !v->IsLocomotive()) {
            return false;
        }
    }
    
    // Verificar limites de peso
    if (e.weight > v->max_engine_weight) {
        return false;
    }
    
    return true;
}
```

---

## ⚠️ Considerações Importantes

### 1. Gerenciamento de Memória

```cpp
// Array global de engines
Engine engines[MAX_ENGINES];

// Inicialização
void InitializeEngines() {
    for (int i = 0; i < MAX_ENGINES; i++) {
        engines[i].id = INVALID_ENGINE;
        engines[i].exists = false;
    }
}
```

### 2. Thread Safety

```cpp
// Acesso a engines deve ser thread-safe
Engine* GetEngine(EngineID eid) {
    std::lock_guard<std::mutex> lock(engine_mutex);
    
    if (!IsValidEngine(eid)) {
        return nullptr;
    }
    
    return &engines[eid];
}
```

### 3. Save/Load Compatibility

```cpp
// Engines devem ser serializáveis para savegames
void SaveEngine(Savegame &sg, EngineID eid) {
    Engine &e = engines[eid];
    
    sg.Write(e.id);
    sg.Write(e.type);
    sg.Write(e.name);
    sg.Write(e.power);
    sg.Write(e.weight);
    // ... outros campos
}

void LoadEngine(Savegame &sg, EngineID eid) {
    Engine &e = engines[eid];
    
    sg.Read(e.id);
    sg.Read(e.type);
    sg.Read(e.name);
    sg.Read(e.power);
    sg.Read(e.weight);
    // ... outros campos
}
```

---

## 🎨 Integração com Interface

### Display de Engine na GUI

```cpp
void DrawEngineInfo(EngineID eid, int x, int y) {
    if (!IsValidEngine(eid)) return;
    
    Engine &e = engines[eid];
    
    // Desenhar sprite do engine
    DrawEngineSprite(eid, x, y, ENGINE_IMAGE_INFO);
    
    // Desenhar nome
    SetDParamStr(0, e.name);
    DrawString(x + 50, y, STR_ENGINE_NAME);
    
    // Desenhar estatísticas
    SetDParam(0, e.power);
    DrawString(x + 50, y + 15, STR_ENGINE_POWER);
    
    SetDParam(0, e.weight);
    DrawString(x + 50, y + 30, STR_ENGINE_WEIGHT);
    
    SetDParam(0, e.max_speed * 8);
    DrawString(x + 50, y + 45, STR_ENGINE_SPEED);
    
    // Barra de confiabilidade
    DrawReliabilityBar(e.reliability, x + 50, y + 60);
}
```

---

## 📚 Referências Cruzadas

### Arquivos Relacionados

| Arquivo | Relação |
|---------|---------|
| `vehicle_type.h` | Define VehicleType que usa EngineType |
| `vehicle_base.h` | Vehicle contém engine_id e métodos relacionados |
| `company_type.h` | Companies pesquisam e compram engines |
| `newgrf_engine.h` | Extensão de engines via NewGRF |
| `engine_cmd.h` | Comandos para gerenciar engines |
| `engine_gui.h` | Interface gráfica de engines |

### Enums Relacionados

- `VehicleType` - Tipo de veículo (usa engines)
- `CargoType` - Carga que engines podem consumir
- `CompanyID` - Dono dos engines pesquisados

---

## ✅ Resumo

Este arquivo estabelece as definições fundamentais para o sistema de **motores/engines** no OpenTTD:

**Principais Contribuições**:
1. ✅ `EngineID` - Identificador único para engines
2. ✅ `EngineType` - Classificação por tipo de veículo
3. ✅ `EngineImageType` - Contextos de renderização
4. ✅ Estrutura conceitual de Engine com todas propriedades
5. ✅ Constants de validação e limites
6. ✅ Funções utilitárias para acesso e validação
7. ✅ Integração com vehicles, companies e NewGRF

**Próximos Passos Sugeridos**:
- `engine_base.h` - Classe base completa de Engine
- `engine_cmd.h` - Comandos de gerenciamento
- `cargo_type.h` - Tipos de carga relacionados

---

*Arquivo traduzido e documentado em Português Brasileiro*
*Formato: Conceito com lógica explícita*
*Versão: 1.0 - Junho 2024*
