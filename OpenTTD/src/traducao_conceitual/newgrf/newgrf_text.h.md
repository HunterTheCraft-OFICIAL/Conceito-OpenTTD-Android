# Tradução Conceitual: newgrf_text

## Descrição Original
Header of Action 04 "universal holder" structure and functions */

## Visão Geral
Este arquivo `newgrf_text.h` contém 12 declarações de funções, 6 estruturas, 1 definições/macros relacionados ao sistema NewGRF.

## Dependências (Includes)
- `string_type.h`
- `strings_type.h`
- `core/smallvec_type.hpp`
- `table/control_codes.h`

## Funções Principais
- `CleanUpStrings`: Função relacionada ao sistema NewGRF
- `SetCurrentGrfLangID`: Função relacionada ao sistema NewGRF
- `AddGRFTextToList`: Função relacionada ao sistema NewGRF
- `AddGRFTextToList`: Função relacionada ao sistema NewGRF
- `AddGRFTextToList`: Função relacionada ao sistema NewGRF
- `CheckGrfLangID`: Função relacionada ao sistema NewGRF
- `StartTextRefStackUsage`: Função relacionada ao sistema NewGRF
- `StopTextRefStackUsage`: Função relacionada ao sistema NewGRF
- `RewindTextRefStack`: Função relacionada ao sistema NewGRF
- `UsingNewGRFTextStack`: Função relacionada ao sistema NewGRF
- `RestoreTextRefStackBackup`: Função relacionada ao sistema NewGRF
- `RemapNewGRFStringControlCode`: Função relacionada ao sistema NewGRF

## Estruturas de Dados
- `GRFText`: Estrutura para dados NewGRF
- `GRFFile`: Estrutura para dados NewGRF
- `TextRefStack`: Estrutura para dados NewGRF
- `TextRefStack`: Estrutura para dados NewGRF
- `LanguageMap`: Estrutura para dados NewGRF
- `Mapping`: Estrutura para dados NewGRF

## Definições e Macros
- `NEWGRF_TEXT_H`: Macro de definição NewGRF

## Responsabilidades
- Gerenciar operações relacionadas ao sistema NewGRF
- Definir tipos e constantes para NewGRF
- Fornecer interface para carregamento e processamento de GRFs

## Integração
Este arquivo se integra com sistemas de veículos, infraestrutura, economia e interface do OpenTTD.
