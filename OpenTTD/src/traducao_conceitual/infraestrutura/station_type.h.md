# Tradução Conceitual: station_type

## Descrição Original
Types related to stations. */

## Visão Geral
Este arquivo `station_type.h` contém 6 estruturas, 1 classes, 1 definições/macros, 5 enumerações relacionados ao sistema de infraestrutura.

## Dependências (Includes)
- `core/smallstack_type.hpp`
- `tilearea_type.h`

## Estruturas de Dados
- `BaseStation`: Estrutura para dados de infraestrutura
- `Station`: Estrutura para dados de infraestrutura
- `RoadStop`: Estrutura para dados de infraestrutura
- `StationSpec`: Estrutura para dados de infraestrutura
- `Waypoint`: Estrutura para dados de infraestrutura
- `StationCompare`: Estrutura para dados de infraestrutura

## Classes
- `StationFinder`: Classe para implementação de funcionalidades de infraestrutura

## Definições e Macros
- `STATION_TYPE_H`: Macro de definição

## Enumerações
- `StationType`: Tipo enumerado para opções de infraestrutura
- `RoadStopType`: Tipo enumerado para opções de infraestrutura
- `StationFacility`: Tipo enumerado para opções de infraestrutura
- `StationHadVehicleOfType`: Tipo enumerado para opções de infraestrutura
- `CatchmentArea`: Tipo enumerado para opções de infraestrutura

## Responsabilidades
- Gerenciar operações relacionadas à infraestrutura
- Definir tipos e constantes para trilhos/estradas/estações
- Fornecer interface para construção e manutenção

## Integração
Este arquivo se integra com sistemas de veículos, economia e pathfinding do OpenTTD.
