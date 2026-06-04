# Tradução Conceitual: company_func

## Descrição Original
Functions related to companies. */

## Visão Geral
Este arquivo `company_func.h` contém 13 declarações de funções, 1 definições/macros relacionados ao sistema de economia e gestão.

## Dependências (Includes)
- `command_type.h`
- `company_type.h`
- `gfx_type.h`
- `vehicle_type.h`

## Funções Principais
- `MayCompanyTakeOver`: Função relacionada à gestão econômica
- `ChangeOwnershipOfCompanyItems`: Função relacionada à gestão econômica
- `GetNameOfOwner`: Função relacionada à gestão econômica
- `SetLocalCompany`: Função relacionada à gestão econômica
- `ShowBuyCompanyDialog`: Função relacionada à gestão econômica
- `CompanyAdminUpdate`: Função relacionada à gestão econômica
- `CompanyAdminBankrupt`: Função relacionada à gestão econômica
- `UpdateLandscapingLimits`: Função relacionada à gestão econômica
- `CheckCompanyHasMoney`: Função relacionada à gestão econômica
- `SubtractMoneyFromCompany`: Função relacionada à gestão econômica
- `SubtractMoneyFromCompanyFract`: Função relacionada à gestão econômica
- `CompanyServiceInterval`: Função relacionada à gestão econômica
- `GetFirstPlayableCompanyID`: Função relacionada à gestão econômica

## Definições e Macros
- `COMPANY_FUNC_H`: Macro de definição

## Responsabilidades
- Gerenciar operações econômicas e financeiras
- Definir tipos e constantes para empresas/indústrias/cidades
- Controlar sistemas de carga e ordens

## Integração
Este arquivo se integra com sistemas de veículos, infraestrutura e interface do OpenTTD.
