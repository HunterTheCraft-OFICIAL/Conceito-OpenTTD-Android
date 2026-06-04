# Tradução Conceitual: map_func

## Descrição Original
Functions related to maps. */

## Visão Geral
Este arquivo `map_func.h` contém 11 declarações de funções, 4 definições/macros relacionados ao sistema de mapa e terreno.

## Dependências (Includes)
- `core/math_func.hpp`
- `tile_type.h`
- `map_type.h`
- `direction_func.h`

## Funções Principais
- `AllocateMap`: Função relacionada à gestão de mapa/terreno
- `TileAddWrap`: Função relacionada à gestão de mapa/terreno
- `DistanceManhattan`: Função relacionada à gestão de mapa/terreno
- `DistanceSquare`: Função relacionada à gestão de mapa/terreno
- `DistanceMax`: Função relacionada à gestão de mapa/terreno
- `DistanceMaxPlusManhattan`: Função relacionada à gestão de mapa/terreno
- `DistanceFromEdge`: Função relacionada à gestão de mapa/terreno
- `DistanceFromEdgeDir`: Função relacionada à gestão de mapa/terreno
- `CircularTileSearch`: Função relacionada à gestão de mapa/terreno
- `CircularTileSearch`: Função relacionada à gestão de mapa/terreno
- `GetClosestWaterDistance`: Função relacionada à gestão de mapa/terreno

## Definições e Macros
- `MAP_FUNC_H`: Macro de definição
- `TILE_MASK`: Macro de definição
- `TILE_ADDXY`: Macro de definição
- `RandomTile`: Macro de definição

## Responsabilidades
- Gerenciar operações relacionadas ao mapa e terreno
- Definir tipos e constantes para tiles e landscape
- Fornecer interface para modificação do terreno

## Integração
Este arquivo se integra com sistemas de veículos, infraestrutura e viewport do OpenTTD.
