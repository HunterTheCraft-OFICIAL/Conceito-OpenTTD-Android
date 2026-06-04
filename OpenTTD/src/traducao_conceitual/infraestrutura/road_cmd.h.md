# Tradução Conceitual: road_cmd

## Descrição Original
Road related functions. */

## Visão Geral
Este arquivo `road_cmd.h` contém 4 declarações de funções, 1 definições/macros relacionados ao sistema de infraestrutura.

## Dependências (Includes)
- `direction_type.h`
- `road_type.h`
- `command_type.h`

## Funções Principais
- `DrawRoadDepotSprite`: Função relacionada à gestão de infraestrutura
- `UpdateNearestTownForRoadTiles`: Função relacionada à gestão de infraestrutura
- `CcRoadDepot`: Função relacionada à gestão de infraestrutura
- `CcRoadStop`: Função relacionada à gestão de infraestrutura

## Definições e Macros
- `ROAD_CMD_H`: Macro de definição

## Responsabilidades
- Gerenciar operações relacionadas à infraestrutura
- Definir tipos e constantes para trilhos/estradas/estações
- Fornecer interface para construção e manutenção

## Integração
Este arquivo se integra com sistemas de veículos, economia e pathfinding do OpenTTD.
