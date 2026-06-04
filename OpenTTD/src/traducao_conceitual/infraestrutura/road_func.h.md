# Tradução Conceitual: road_func

## Descrição Original
Functions related to roads. */

## Visão Geral
Este arquivo `road_func.h` contém 6 declarações de funções, 1 estruturas, 1 definições/macros relacionados ao sistema de infraestrutura.

## Dependências (Includes)
- `core/bitmath_func.hpp`
- `road.h`
- `economy_func.h`
- `transparency.h`

## Funções Principais
- `HasRoadTypeAvail`: Função relacionada à gestão de infraestrutura
- `ValParamRoadType`: Função relacionada à gestão de infraestrutura
- `UpdateLevelCrossing`: Função relacionada à gestão de infraestrutura
- `MarkDirtyAdjacentLevelCrossingTiles`: Função relacionada à gestão de infraestrutura
- `UpdateCompanyRoadInfrastructure`: Função relacionada à gestão de infraestrutura
- `DrawRoadOverlays`: Função relacionada à gestão de infraestrutura

## Estruturas de Dados
- `TileInfo`: Estrutura para dados de infraestrutura

## Definições e Macros
- `ROAD_FUNC_H`: Macro de definição

## Responsabilidades
- Gerenciar operações relacionadas à infraestrutura
- Definir tipos e constantes para trilhos/estradas/estações
- Fornecer interface para construção e manutenção

## Integração
Este arquivo se integra com sistemas de veículos, economia e pathfinding do OpenTTD.
