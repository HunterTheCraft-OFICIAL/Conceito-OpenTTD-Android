# Tradução Conceitual: newgrf_commons

## Visão Geral
Este arquivo `newgrf_commons.h` contém 4 declarações de funções, 17 estruturas, 7 classes, 1 definições/macros, 2 enumerações relacionados ao sistema NewGRF.

## Dependências (Includes)
- `sprite.h`
- `core/alloc_type.hpp`
- `core/smallvec_type.hpp`
- `command_type.h`
- `direction_type.h`
- `company_type.h`

## Funções Principais
- `GetNearbyTile`: Função relacionada ao sistema NewGRF
- `ErrorUnknownCallbackResult`: Função relacionada ao sistema NewGRF
- `ConvertBooleanCallback`: Função relacionada ao sistema NewGRF
- `Convert8bitBooleanCallback`: Função relacionada ao sistema NewGRF

## Estruturas de Dados
- `TileLayoutRegisters`: Estrutura para dados NewGRF
- `is`: Estrutura para dados NewGRF
- `NewGRFSpriteLayout`: Estrutura para dados NewGRF
- `EntityIDMapping`: Estrutura para dados NewGRF
- `HouseSpec`: Estrutura para dados NewGRF
- `IndustrySpec`: Estrutura para dados NewGRF
- `IndustryTileSpec`: Estrutura para dados NewGRF
- `AirportSpec`: Estrutura para dados NewGRF
- `AirportTileSpec`: Estrutura para dados NewGRF
- `ObjectSpec`: Estrutura para dados NewGRF
- ... e mais 7 estruturas

## Classes
- `OverrideManagerBase`: Classe para implementação de funcionalidades NewGRF
- `HouseOverrideManager`: Classe para implementação de funcionalidades NewGRF
- `IndustryOverrideManager`: Classe para implementação de funcionalidades NewGRF
- `IndustryTileOverrideManager`: Classe para implementação de funcionalidades NewGRF
- `AirportOverrideManager`: Classe para implementação de funcionalidades NewGRF
- `AirportTileOverrideManager`: Classe para implementação de funcionalidades NewGRF
- `ObjectOverrideManager`: Classe para implementação de funcionalidades NewGRF

## Definições e Macros
- `NEWGRF_COMMONS_H`: Macro de definição NewGRF

## Enumerações
- `TileContext`: Tipo enumerado para opções NewGRF
- `TileLayoutFlags`: Tipo enumerado para opções NewGRF

## Responsabilidades
- Gerenciar operações relacionadas ao sistema NewGRF
- Definir tipos e constantes para NewGRF
- Fornecer interface para carregamento e processamento de GRFs

## Integração
Este arquivo se integra com sistemas de veículos, infraestrutura, economia e interface do OpenTTD.
