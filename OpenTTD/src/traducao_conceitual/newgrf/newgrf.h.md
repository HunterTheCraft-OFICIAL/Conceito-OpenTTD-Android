# Tradução Conceitual: newgrf

## Descrição Original
Base for the NewGRF implementation. */

## Visão Geral
Este arquivo `newgrf.h` contém 7 declarações de funções, 14 estruturas, 1 definições/macros, 6 enumerações relacionados ao sistema NewGRF.

## Dependências (Includes)
- `cargotype.h`
- `rail_type.h`
- `road_type.h`
- `fileio_type.h`
- `core/bitmath_func.hpp`
- `core/alloc_type.hpp`
- `core/smallvec_type.hpp`

## Funções Principais
- `LoadNewGRFFile`: Função relacionada ao sistema NewGRF
- `LoadNewGRF`: Função relacionada ao sistema NewGRF
- `ReloadNewGRFData`: Função relacionada ao sistema NewGRF
- `ResetNewGRFData`: Função relacionada ao sistema NewGRF
- `ResetPersistentNewGRFData`: Função relacionada ao sistema NewGRF
- `GetGlobalVariable`: Função relacionada ao sistema NewGRF
- `ShowNewGRFError`: Função relacionada ao sistema NewGRF

## Estruturas de Dados
- `CanalProperties`: Estrutura para dados NewGRF
- `GRFLabel`: Estrutura para dados NewGRF
- `GRFFile`: Estrutura para dados NewGRF
- `StationSpec`: Estrutura para dados NewGRF
- `HouseSpec`: Estrutura para dados NewGRF
- `IndustrySpec`: Estrutura para dados NewGRF
- `IndustryTileSpec`: Estrutura para dados NewGRF
- `ObjectSpec`: Estrutura para dados NewGRF
- `AirportSpec`: Estrutura para dados NewGRF
- `AirportTileSpec`: Estrutura para dados NewGRF
- ... e mais 4 estruturas

## Definições e Macros
- `NEWGRF_H`: Macro de definição NewGRF

## Enumerações
- `CanalFeature`: Tipo enumerado para opções NewGRF
- `GrfLoadingStage`: Tipo enumerado para opções NewGRF
- `GrfMiscBit`: Tipo enumerado para opções NewGRF
- `GrfSpecFeature`: Tipo enumerado para opções NewGRF
- `ShoreReplacement`: Tipo enumerado para opções NewGRF
- `TramReplacement`: Tipo enumerado para opções NewGRF

## Responsabilidades
- Gerenciar operações relacionadas ao sistema NewGRF
- Definir tipos e constantes para NewGRF
- Fornecer interface para carregamento e processamento de GRFs

## Integração
Este arquivo se integra com sistemas de veículos, infraestrutura, economia e interface do OpenTTD.
