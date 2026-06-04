# Tradução Conceitual: vehicle_func

## Descrição Original
Functions related to vehicles. */

## Visão Geral
Este arquivo `vehicle_func.h` contém 28 declarações de funções, 4 estruturas, 4 definições/macros relacionados ao sistema de veículos.

## Dependências (Includes)
- `gfx_type.h`
- `direction_type.h`
- `command_type.h`
- `vehicle_type.h`
- `engine_type.h`
- `transport_type.h`
- `newgrf_config.h`
- `track_type.h`
- `livery.h`

## Funções Principais
- `IsValidImageIndex`: Função relacionada à gestão de veículos
- `VehicleServiceInDepot`: Função relacionada à gestão de veículos
- `CountVehiclesInChain`: Função relacionada à gestão de veículos
- `FindVehicleOnPos`: Função relacionada à gestão de veículos
- `FindVehicleOnPosXY`: Função relacionada à gestão de veículos
- `HasVehicleOnPos`: Função relacionada à gestão de veículos
- `HasVehicleOnPosXY`: Função relacionada à gestão de veículos
- `CallVehicleTicks`: Função relacionada à gestão de veículos
- `VehicleLengthChanged`: Função relacionada à gestão de veículos
- `VehicleRandomBits`: Função relacionada à gestão de veículos
- `ResetVehicleHash`: Função relacionada à gestão de veículos
- `ResetVehicleColourMap`: Função relacionada à gestão de veículos
- `GetBestFittingSubType`: Função relacionada à gestão de veículos
- `ViewportAddVehicles`: Função relacionada à gestão de veículos
- `ShowNewGrfVehicleError`: Função relacionada à gestão de veículos
- ... e mais 13 funções

## Estruturas de Dados
- `GetNewVehiclePosResult`: Estrutura para dados de veículos
- `Livery`: Estrutura para dados de veículos
- `Station`: Estrutura para dados de veículos
- `Station`: Estrutura para dados de veículos

## Definições e Macros
- `VEHICLE_FUNC_H`: Macro de definição
- `is_custom_sprite`: Macro de definição
- `IS_CUSTOM_FIRSTHEAD_SPRITE`: Macro de definição
- `IS_CUSTOM_SECONDHEAD_SPRITE`: Macro de definição

## Responsabilidades
- Gerenciar operações relacionadas a veículos
- Definir tipos e constantes para veículos
- Fornecer interface para movimentação e controle de veículos

## Integração
Este arquivo se integra com sistemas de pathfinding, ordens, economia e infraestrutura do OpenTTD.
