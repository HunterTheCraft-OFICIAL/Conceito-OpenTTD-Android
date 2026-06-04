# Tradução Conceitual: order_func

## Descrição Original
Functions related to orders. */

## Visão Geral
Este arquivo `order_func.h` contém 8 declarações de funções, 5 definições/macros relacionados ao sistema de economia e gestão.

## Dependências (Includes)
- `order_type.h`
- `vehicle_type.h`
- `company_type.h`

## Funções Principais
- `RemoveOrderFromAllVehicles`: Função relacionada à gestão econômica
- `InvalidateVehicleOrder`: Função relacionada à gestão econômica
- `CheckOrders`: Função relacionada à gestão econômica
- `DeleteVehicleOrders`: Função relacionada à gestão econômica
- `ProcessOrders`: Função relacionada à gestão econômica
- `UpdateOrderDest`: Função relacionada à gestão econômica
- `GetOrderDistance`: Função relacionada à gestão econômica
- `DrawOrderString`: Função relacionada à gestão econômica

## Definições e Macros
- `ORDER_FUNC_H`: Macro de definição
- `MIN_SERVINT_PERCENT`: Macro de definição
- `MAX_SERVINT_PERCENT`: Macro de definição
- `MIN_SERVINT_DAYS`: Macro de definição
- `MAX_SERVINT_DAYS`: Macro de definição

## Responsabilidades
- Gerenciar operações econômicas e financeiras
- Definir tipos e constantes para empresas/indústrias/cidades
- Controlar sistemas de carga e ordens

## Integração
Este arquivo se integra com sistemas de veículos, infraestrutura e interface do OpenTTD.
