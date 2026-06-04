# Tradução Conceitual: station_func

## Descrição Original
Functions related to stations. */

## Visão Geral
Este arquivo `station_func.h` contém 20 declarações de funções, 1 definições/macros relacionados ao sistema de infraestrutura.

## Dependências (Includes)
- `sprite.h`
- `rail_type.h`
- `road_type.h`
- `vehicle_type.h`
- `economy_func.h`
- `rail.h`
- `road.h`
- `linkgraph/linkgraph_type.h`
- `industry_type.h`

## Funções Principais
- `ModifyStationRatingAround`: Função relacionada à gestão de infraestrutura
- `ShowStationViewWindow`: Função relacionada à gestão de infraestrutura
- `UpdateAllStationVirtCoords`: Função relacionada à gestão de infraestrutura
- `ClearAllStationCachedNames`: Função relacionada à gestão de infraestrutura
- `UpdateStationAcceptance`: Função relacionada à gestão de infraestrutura
- `StationPickerDrawSprite`: Função relacionada à gestão de infraestrutura
- `HasStationInUse`: Função relacionada à gestão de infraestrutura
- `DeleteOilRig`: Função relacionada à gestão de infraestrutura
- `UpdateStationDockingTiles`: Função relacionada à gestão de infraestrutura
- `RemoveDockingTile`: Função relacionada à gestão de infraestrutura
- `ClearDockingTilesCheckingNeighbours`: Função relacionada à gestão de infraestrutura
- `IsValidDockingDirectionForDock`: Função relacionada à gestão de infraestrutura
- `IsStationTileBlocked`: Função relacionada à gestão de infraestrutura
- `CanStationTileHavePylons`: Função relacionada à gestão de infraestrutura
- `CanStationTileHaveWires`: Função relacionada à gestão de infraestrutura
- ... e mais 5 funções

## Definições e Macros
- `STATION_FUNC_H`: Macro de definição

## Responsabilidades
- Gerenciar operações relacionadas à infraestrutura
- Definir tipos e constantes para trilhos/estradas/estações
- Fornecer interface para construção e manutenção

## Integração
Este arquivo se integra com sistemas de veículos, economia e pathfinding do OpenTTD.
