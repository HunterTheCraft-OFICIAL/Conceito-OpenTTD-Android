# Tradução Conceitual: company_gui

## Descrição Original
GUI Functions related to companies. */

## Visão Geral
Este arquivo `company_gui.h` contém 8 declarações de funções, 1 definições/macros relacionados ao sistema de economia e gestão.

## Dependências (Includes)
- `company_type.h`
- `group.h`
- `gfx_type.h`

## Funções Principais
- `DrawCompanyIcon`: Função relacionada à gestão econômica
- `ShowCompanyLiveryWindow`: Função relacionada à gestão econômica
- `ShowCompanyStations`: Função relacionada à gestão econômica
- `ShowCompanyFinances`: Função relacionada à gestão econômica
- `ShowCompany`: Função relacionada à gestão econômica
- `InvalidateCompanyWindows`: Função relacionada à gestão econômica
- `CloseCompanyWindows`: Função relacionada à gestão econômica
- `DirtyCompanyInfrastructureWindows`: Função relacionada à gestão econômica

## Definições e Macros
- `COMPANY_GUI_H`: Macro de definição

## Responsabilidades
- Gerenciar operações econômicas e financeiras
- Definir tipos e constantes para empresas/indústrias/cidades
- Controlar sistemas de carga e ordens

## Integração
Este arquivo se integra com sistemas de veículos, infraestrutura e interface do OpenTTD.
