# Tradução Conceitual: road

## Descrição Original
Road specific functions. */

## Visão Geral
Este arquivo `road.h` contém 3 declarações de funções, 2 estruturas, 1 classes, 1 definições/macros, 4 enumerações relacionados ao sistema de infraestrutura.

## Dependências (Includes)
- `road_type.h`
- `gfx_type.h`
- `core/bitmath_func.hpp`
- `strings_type.h`
- `date_type.h`
- `core/enum_type.hpp`
- `newgrf.h`
- `economy_func.h`

## Funções Principais
- `ResetRoadTypes`: Função relacionada à gestão de infraestrutura
- `InitRoadTypes`: Função relacionada à gestão de infraestrutura
- `HasAnyRoadTypesAvail`: Função relacionada à gestão de infraestrutura

## Estruturas de Dados
- `SpriteGroup`: Estrutura para dados de infraestrutura
- `containing`: Estrutura para dados de infraestrutura

## Classes
- `RoadTypeInfo`: Classe para implementação de funcionalidades de infraestrutura

## Definições e Macros
- `ROAD_H`: Macro de definição

## Enumerações
- `RoadTramType`: Tipo enumerado para opções de infraestrutura
- `RoadTramTypes`: Tipo enumerado para opções de infraestrutura
- `RoadTypeFlags`: Tipo enumerado para opções de infraestrutura
- `RoadTypeSpriteGroup`: Tipo enumerado para opções de infraestrutura

## Responsabilidades
- Gerenciar operações relacionadas à infraestrutura
- Definir tipos e constantes para trilhos/estradas/estações
- Fornecer interface para construção e manutenção

## Integração
Este arquivo se integra com sistemas de veículos, economia e pathfinding do OpenTTD.
