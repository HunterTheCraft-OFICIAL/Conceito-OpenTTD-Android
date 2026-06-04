# Tradução Conceitual: roadveh

## Descrição Original
Road vehicle states */

## Visão Geral
Este arquivo `roadveh.h` contém 2 declarações de funções, 4 estruturas, 1 definições/macros, 1 enumerações relacionados ao sistema de veículos.

## Dependências (Includes)
- `ground_vehicle.hpp`
- `engine_base.h`
- `cargotype.h`
- `track_func.h`
- `road.h`
- `road_map.h`
- `newgrf_engine.h`

## Funções Principais
- `RoadVehUpdateCache`: Função relacionada à gestão de veículos
- `GetRoadVehSpriteSize`: Função relacionada à gestão de veículos

## Estruturas de Dados
- `RoadVehicle`: Estrutura para dados de veículos
- `RoadVehPathCache`: Estrutura para dados de veículos
- `RoadVehicle`: Estrutura para dados de veículos
- `GroundVehicle`: Estrutura para dados de veículos

## Definições e Macros
- `ROADVEH_H`: Macro de definição

## Enumerações
- `RoadVehicleStates`: Tipo enumerado para opções de veículos

## Responsabilidades
- Gerenciar operações relacionadas a veículos
- Definir tipos e constantes para veículos
- Fornecer interface para movimentação e controle de veículos

## Integração
Este arquivo se integra com sistemas de pathfinding, ordens, economia e infraestrutura do OpenTTD.
