# Tradução Conceitual: aircraft

## Descrição Original
Base for aircraft. */

## Visão Geral
Este arquivo `aircraft.h` contém 10 declarações de funções, 3 estruturas, 1 classes, 1 definições/macros, 3 enumerações relacionados ao sistema de veículos.

## Dependências (Includes)
- `station_map.h`
- `vehicle_base.h`

## Funções Principais
- `HandleAircraftEnterHangar`: Função relacionada à gestão de veículos
- `GetAircraftSpriteSize`: Função relacionada à gestão de veículos
- `UpdateAirplanesOnNewStation`: Função relacionada à gestão de veículos
- `UpdateAircraftCache`: Função relacionada à gestão de veículos
- `AircraftLeaveHangar`: Função relacionada à gestão de veículos
- `AircraftNextAirportPos_and_Order`: Função relacionada à gestão de veículos
- `SetAircraftPosition`: Função relacionada à gestão de veículos
- `GetAircraftFlightLevelBounds`: Função relacionada à gestão de veículos
- `GetAircraftFlightLevel`: Função relacionada à gestão de veículos
- `GetRotorImage`: Função relacionada à gestão de veículos

## Estruturas de Dados
- `Aircraft`: Estrutura para dados de veículos
- `AircraftCache`: Estrutura para dados de veículos
- `Aircraft`: Estrutura para dados de veículos

## Classes
- `T`: Classe para implementação de funcionalidades de veículos

## Definições e Macros
- `AIRCRAFT_H`: Macro de definição

## Enumerações
- `AircraftFlyingAltitude`: Tipo enumerado para opções de veículos
- `AircraftSubType`: Tipo enumerado para opções de veículos
- `AirVehicleFlags`: Tipo enumerado para opções de veículos

## Responsabilidades
- Gerenciar operações relacionadas a veículos
- Definir tipos e constantes para veículos
- Fornecer interface para movimentação e controle de veículos

## Integração
Este arquivo se integra com sistemas de pathfinding, ordens, economia e infraestrutura do OpenTTD.
