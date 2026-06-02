<!--
================================================================================
ARQUIVO: aircraft.h
NÍVEL: 2 (Essencial - Sistemas Principais)
SUBCATEGORIA: Veículos Aéreos
LINGUAGEM ORIGINAL: C++
PROPÓSITO: Define a estrutura base para aeronaves, helicópteros, rotores e sombras no jogo.
           Este arquivo estabelece os tipos de aeronaves, seus estados de voo, altitude,
           flags de comportamento e a classe principal Aircraft que gerencia todo o 
           comportamento de veículos aéreos.

INTERAÇÕES: 
   - station_map.h (para StationID e tiles de aeroporto)
   - vehicle_base.h (herda de SpecializedVehicle)
   - airport.h / airport_cmd.h (estados de movimento do aeroporto)
   - vehicle.h (classe base Vehicle)

VARIÁVEIS_PRINCIPAIS:
   - crashed_counter: Timer para animações de colisão
   - pos/previous_pos: Posição atual e anterior na pista de aeroporto
   - targetairport: ID do aeroporto de destino
   - state: Estado atual do movimento no aeroporto
   - flags: Flags de comportamento (AirVehicleFlags)
   - acache: Cache de performance para alcance máximo

ESTRUTURAS:
   - enum AircraftFlyingAltitude: Constantes de altitude mínima/máxima de voo
   - enum AircraftSubType: Tipos (helicóptero=0, avião=2, sombra=4, rotor=6)
   - enum AirVehicleFlags: Flags de estado (destino longe, correção de altura, etc.)
   - struct AircraftCache: Variáveis em cache para performance
   - struct Aircraft: Classe principal herdando de SpecializedVehicle

FUNÇÕES_CHAVE:
   - HandleAircraftEnterHangar(): Processa entrada da aeronave no hangar
   - UpdateAircraftCache(): Atualiza cache de performance
   - AircraftLeaveHangar(): Faz aeronave sair do hangar
   - SetAircraftPosition(): Define posição X, Y, Z da aeronave
   - GetAircraftFlightLevel(): Calcula nível de voo atual
   - IsNormalAircraft(): Verifica se é aeronave "real" (não sombra/rotor)
   - GetRange(): Retorna alcance máximo em tiles
   - Tick()/OnNewDay(): Atualizações por tick e por dia
   - Crash(): Processa colisão da aeronave
================================================================================
-->

# aircraft.h - Base para Aeronaves

## Licença e Informações do Arquivo
Este arquivo faz parte do OpenTTD, software livre sob licença GNU GPL versão 2.

## Propósito Principal
Define todas as estruturas, enums e funções necessárias para representar e gerenciar 
aeronaves (aviões e helicópteros) no jogo, incluindo seus componentes visuais (sombras 
e rotores) e lógica de voo.

---

## Constantes de Altitude de Voo

### Enum: AircraftFlyingAltitude
Define os níveis de voo básicos acima do terreno para voo normal e padrões de espera.

**Valores:**
- `AIRCRAFT_MIN_FLYING_ALTITUDE = 120`: Altitude mínima absoluta acima do tile
- `AIRCRAFT_MAX_FLYING_ALTITUDE = 360`: Altitude máxima absoluta acima do tile  
- `PLANE_HOLD_MAX_FLYING_ALTITUDE = 150`: Altitude máxima para aviões em padrão de espera
- `HELICOPTER_HOLD_MAX_FLYING_ALTITUDE = 184`: Altitude máxima para helicópteros em espera

**Lógica Explicada:**
As aeronaves voam entre 120 e 360 unidades de altura acima do terreno. Durante padrões 
de espera (quando aguardam permissão para pousar), aviões voam mais baixo (150) que 
helicópteros (184). Devido à velocidade e direção, a altitude real pode ser maior que 
esses valores base.

---

## Tipos de Aeronaves

### Enum: AircraftSubType
Classifica os diferentes tipos de objetos aéreos no jogo.

**Valores:**
- `AIR_HELICOPTER = 0`: Um helicóptero
- `AIR_AIRCRAFT = 2`: Um avião
- `AIR_SHADOW = 4`: Sombra projetada pela aeronave (objeto visual separado)
- `AIR_ROTOR = 6`: Rotor de um helicóptero (objeto visual separado)

**Lógica Explicada:**
O sistema trata sombras e rotores como entidades separadas da aeronave principal para 
facilitar a renderização e animação. Os valores pares (0, 2, 4, 6) permitem verificações 
bitwise eficientes.

---

## Flags de Comportamento

### Enum: AirVehicleFlags
Flags que controlam o comportamento de veículos aéreos (compartilhado com veículos de desastre).

**Valores:**
- `VAF_DEST_TOO_FAR = 0`: Próximo destino está muito distante
- `VAF_IN_MAX_HEIGHT_CORRECTION = 1`: Veículo está descendo porque atingiu limite superior
- `VAF_IN_MIN_HEIGHT_CORRECTION = 2`: Veículo está subindo porque atingiu limite inferior
- `VAF_HELI_DIRECT_DESCENT = 3`: Helicóptero descendo diretamente ao destino

**Lógica Explicada das Flags de Correção de Altura:**
Para evitar que aeronaves sigam exatamente o contorno do terreno (criando um efeito de 
"escada"), o sistema faz com que elas subam ou desçam múltiplos níveis de voo de uma vez. 
Isso só tem efeito quando há mais de 15 níveis de altura no jogo. As flags indicam quando 
a aeronave está em processo de correção ativa de altitude.

---

## Constantes Visuais

### ROTOR_Z_OFFSET = 5
Offset no eixo Z entre o sprite do helicóptero e o sprite do rotor. Usado para renderizar 
o rotor ligeiramente acima do corpo do helicóptero.

---

## Declarações de Funções (Protótipos)

### Funções de Gerenciamento de Hangar
- `HandleAircraftEnterHangar(Aircraft *v)`: Processa lógica quando aeronave entra no hangar
- `AircraftLeaveHangar(Aircraft *v, Direction exit_dir)`: Faz aeronave sair do hangar na direção especificada

### Funções de Renderização
- `GetAircraftSpriteSize(...)`: Obtém dimensões do sprite da aeronave
- `GetRotorImage(...)`: Obtém imagem do rotor para helicópteros

### Funções de Atualização
- `UpdateAirplanesOnNewStation(const Station *st)`: Atualiza aeronaves quando nova estação é criada
- `UpdateAircraftCache(Aircraft *v, bool update_range)`: Atualiza variáveis em cache para performance

### Funções de Movimento e Posicionamento
- `AircraftNextAirportPos_and_Order(Aircraft *v)`: Calcula próxima posição e ordem no aeroporto
- `SetAircraftPosition(Aircraft *v, int x, int y, int z)`: Define posição exata da aeronave
- `GetAircraftFlightLevelBounds(...)`: Obtém limites de nível de voo para uma aeronave
- `GetAircraftFlightLevel<T>(T *v, bool takeoff)`: Calcula nível de voo atual (template genérico)

---

## Estrutura de Cache

### Struct: AircraftCache
Variáveis armazenadas em cache para melhorar performance e evitar recálculos constantes.

**Campos:**
- `cached_max_range_sqr` (uint32): Alcance máximo ao quadrado (usado para comparações rápidas)
- `cached_max_range` (uint16): Alcance máximo em tiles

**Lógica Explicada:**
Calcular o alcance máximo requer acesso a dados do motor/jogo que podem ser custosos. 
Armazenar esse valor em cache evita recálculos desnecessários em cada frame ou tick.

---

## Classe Principal: Aircraft

### Definição
```cpp
struct Aircraft : public SpecializedVehicle<Aircraft, VEH_AIRCRAFT>
```

A classe Aircraft representa TODOS os objetos aéreos: aviões, helicópteros, suas sombras 
e rotores. Herda de `SpecializedVehicle` com tipo `VEH_AIRCRAFT`.

### Campos/Membros da Classe

#### Controle de Colisão
- `crashed_counter` (uint16): Timer para animações de colisão. Conta ticks desde a colisão.

#### Posicionamento no Aeroporto
- `pos` (byte): Próxima posição desejada na pista/aeroporto
- `previous_pos` (byte): Posição anterior (usada para detectar movimento)

#### Navegação
- `targetairport` (StationID): ID da estação/aeroporto de próximo destino
- `state` (byte): Estado atual no sistema de movimento do aeroporto (ver AirportMovementStates)
- `last_direction` (Direction): Última direção de movimento

#### Controle de Manobras
- `number_consecutive_turns` (byte): Contador de voltas consecutivas - protege contra 
  aeronaves fazendo muitas voltas para alcançar um ponto específico
- `turn_counter` (byte): Ticks entre cada volta para prevenir voltas > 45 graus

#### Estado e Flags
- `flags` (byte): Flags de comportamento (ver AirVehicleFlags)
- `acache` (AircraftCache): Dados em cache para performance

### Construtor e Destruidor

#### Construtor: `Aircraft()`
Inicializa a aeronave chamando o construtor da classe base `SpecializedVehicleBase()`.
**Nota importante**: O comentário no código original diz "Não queremos que o GCC zerour 
nossa struct! Ela já está zerada e tem um índice!" - otimização para evitar inicialização 
redundante.

#### Destruidor: `~Aircraft()`
Chama `PreDestructor()` para garantir limpeza adequada antes da destruição.

### Métodos Públicos

#### Métodos Herdados de Vehicle (comportamento padrão de veículo)
- `MarkDirty()`: Marca a aeronave como "suja" (precisa ser redesenhada)
- `UpdateDeltaXY()`: Atualiza deltas de posição X/Y
- `GetExpenseType(bool income)`: Retorna tipo de despesa:
  - Se `income=true`: `EXPENSES_AIRCRAFT_REVENUE` (receita)
  - Se `income=false`: `EXPENSES_AIRCRAFT_RUN` (custo de operação)
- `IsPrimaryVehicle()`: Retorna verdadeiro se for aeronave principal (não sombra/rotor)
- `GetImage(...)`: Obtém sequência de sprites para renderização
- `GetDisplaySpeed()`: Retorna velocidade atual para display
- `GetDisplayMaxSpeed()`: Retorna velocidade máxima para display
- `GetSpeedOldUnits()`: Converte velocidade para unidades antigas do jogo
- `GetCurrentMaxSpeed()`: Retorna velocidade máxima atual
- `GetRunningCost()`: Calcula custo de operação

#### Método Especial: `IsInDepot()`
Verifica se a aeronave está no hangar.

**Lógica:**
1. Asserta que é uma aeronave primária (não sombra/rotor)
2. Verifica se flag `VS_HIDDEN` está definida (invisível = no hangar)
3. Verifica se o tile atual é um hangar

#### Métodos de Atualização e Eventos
- `Tick()`: Atualização por tick do jogo (movimento, lógica)
- `OnNewDay()`: Ações executadas quando um novo dia começa
- `Crash(bool flooded)`: Processa colisão da aeronave. Parâmetro `flooded` indica se 
  caiu na água. Retorna duração da animação de crash.

#### Métodos de Navegação
- `GetOrderStationLocation(StationID station)`: Obtém localização de estações de ordens
- `FindClosestDepot(...)`: Encontra hangar mais próximo
  - `location`: Output para localização do hangar
  - `destination`: Output para ID do destino
  - `reverse`: Output se precisa inverter direção

### Métodos Inline (Otimizados)

#### `IsNormalAircraft()`
Verifica se a aeronave é um objeto de voo "real" (avião ou helicóptero), não uma sombra 
ou rotor.

**Implementação:**
```cpp
return this->subtype <= AIR_AIRCRAFT;
```

**Lógica Explicada:**
O comentário explica que a verificação completa seria:
```cpp
return (this->subtype == AIR_HELICOPTER) || (this->subtype == AIR_AIRCRAFT);
```
Mas como subtype só pode ser 0 ou 2 para aeronaves reais, verificar `<= 2` é equivalente 
e mais eficiente.

#### `GetRange()`
Retorna o alcance máximo desta aeronave.

**Retorno:**
- Alcance em tiles, OU
- 0 se alcance ilimitado

**Implementação:** Simplesmente retorna `acache.cached_max_range` do cache.

---

## Funções Adicionais Fora da Classe

### `GetTargetAirportIfValid(const Aircraft *v)`
Verifica se o aeroporto alvo da aeronave ainda é válido (não foi deletado, etc.). 
Retorna ponteiro para a Station se válido, nullptr caso contrário.

---

## Resumo da Lógica Principal

1. **Tipos Múltiplos**: Uma única "aeronave" no jogo pode ser composta por até 4 objetos 
   separados: aeronave principal + sombra + rotor (se helicóptero)

2. **Controle de Altitude**: Sistema sofisticado previne seguimento excessivo do terreno, 
   fazendo aeronaves subirem/descerem em "degraus" de altitude

3. **Movimento em Aeroporto**: Sistema de estados e posições discretas controla movimento 
   preciso em pistas e áreas de aeroporto

4. **Performance**: Uso intensivo de cache para evitar recálculos de alcance e outras 
   propriedades frequentemente acessadas

5. **Otimizações**: Verificações bitwise e comparações simplificadas para performance 
   crítica em tempo real

---

## Arquivos Relacionados para Consulta
- `vehicle_base.h`: Classe base SpecializedVehicle
- `airport.h`: Estados de movimento de aeroporto
- `station.h`: Definição de StationID
- `engine.h`: Definição de EngineID
