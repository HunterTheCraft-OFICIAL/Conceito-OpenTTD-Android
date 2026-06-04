# Tradução Conceitual: economy_func

## Descrição Original
Functions related to the economy. */

## Visão Geral
Este arquivo `economy_func.h` contém 12 declarações de funções, 1 estruturas, 1 definições/macros relacionados ao sistema de economia e gestão.

## Dependências (Includes)
- `economy_type.h`
- `station_type.h`
- `cargo_type.h`
- `vehicle_type.h`
- `company_type.h`

## Funções Principais
- `ResetPriceBaseMultipliers`: Função relacionada à gestão econômica
- `SetPriceBaseMultiplier`: Função relacionada à gestão econômica
- `UpdateCompanyRatingAndValue`: Função relacionada à gestão econômica
- `StartupIndustryDailyChanges`: Função relacionada à gestão econômica
- `GetTransportedGoodsIncome`: Função relacionada à gestão econômica
- `MoveGoodsToStation`: Função relacionada à gestão econômica
- `PrepareUnload`: Função relacionada à gestão econômica
- `LoadUnloadStation`: Função relacionada à gestão econômica
- `GetPrice`: Função relacionada à gestão econômica
- `InitializeEconomy`: Função relacionada à gestão econômica
- `RecomputePrices`: Função relacionada à gestão econômica
- `AddInflation`: Função relacionada à gestão econômica

## Estruturas de Dados
- `GRFFile`: Estrutura para dados econômicos

## Definições e Macros
- `ECONOMY_FUNC_H`: Macro de definição

## Responsabilidades
- Gerenciar operações econômicas e financeiras
- Definir tipos e constantes para empresas/indústrias/cidades
- Controlar sistemas de carga e ordens

## Integração
Este arquivo se integra com sistemas de veículos, infraestrutura e interface do OpenTTD.
