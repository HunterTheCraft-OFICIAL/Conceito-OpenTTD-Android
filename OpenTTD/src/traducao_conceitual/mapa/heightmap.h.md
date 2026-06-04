# Tradução Conceitual: heightmap

## Descrição Original
Functions related to creating heightmaps from files. */

## Visão Geral
Este arquivo `heightmap.h` contém 4 declarações de funções, 1 definições/macros, 1 enumerações relacionados ao sistema de mapa e terreno.

## Dependências (Includes)
- `fileio_type.h`

## Funções Principais
- `GetHeightmapDimensions`: Função relacionada à gestão de mapa/terreno
- `LoadHeightmap`: Função relacionada à gestão de mapa/terreno
- `FlatEmptyWorld`: Função relacionada à gestão de mapa/terreno
- `FixSlopes`: Função relacionada à gestão de mapa/terreno

## Definições e Macros
- `HEIGHTMAP_H`: Macro de definição

## Enumerações
- `HeightmapRotation`: Tipo enumerado para opções de mapa/terreno

## Responsabilidades
- Gerenciar operações relacionadas ao mapa e terreno
- Definir tipos e constantes para tiles e landscape
- Fornecer interface para modificação do terreno

## Integração
Este arquivo se integra com sistemas de veículos, infraestrutura e viewport do OpenTTD.
