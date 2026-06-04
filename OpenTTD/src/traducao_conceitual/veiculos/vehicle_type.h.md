# Tradução Conceitual: vehicle_type

## Descrição Original
Types related to vehicles. */

## Visão Geral
Este arquivo `vehicle_type.h` contém 9 estruturas, 1 classes, 1 definições/macros, 5 enumerações relacionados ao sistema de veículos.

## Dependências (Includes)
- `core/enum_type.hpp`

## Estruturas de Dados
- `EnumPropsT`: Estrutura para dados de veículos
- `Vehicle`: Estrutura para dados de veículos
- `Train`: Estrutura para dados de veículos
- `RoadVehicle`: Estrutura para dados de veículos
- `Ship`: Estrutura para dados de veículos
- `Aircraft`: Estrutura para dados de veículos
- `EffectVehicle`: Estrutura para dados de veículos
- `DisasterVehicle`: Estrutura para dados de veículos
- `BaseVehicle`: Estrutura para dados de veículos

## Classes
- `DepotCommand`: Classe para implementação de funcionalidades de veículos

## Definições e Macros
- `VEHICLE_TYPE_H`: Macro de definição

## Enumerações
- `VehicleType`: Tipo enumerado para opções de veículos
- `VehiclePathFinders`: Tipo enumerado para opções de veículos
- `class`: Tipo enumerado para opções de veículos
- `AccelerationModel`: Tipo enumerado para opções de veículos
- `EngineImageType`: Tipo enumerado para opções de veículos

## Responsabilidades
- Gerenciar operações relacionadas a veículos
- Definir tipos e constantes para veículos
- Fornecer interface para movimentação e controle de veículos

## Integração
Este arquivo se integra com sistemas de pathfinding, ordens, economia e infraestrutura do OpenTTD.
