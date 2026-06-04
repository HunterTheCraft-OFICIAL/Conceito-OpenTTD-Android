# Tradução Conceitual: vehicle_gui

## Descrição Original
Functions related to the vehicle's GUIs. */

## Visão Geral
Este arquivo `vehicle_gui.h` contém 21 declarações de funções, 3 estruturas, 1 definições/macros, 2 enumerações relacionados ao sistema de veículos.

## Dependências (Includes)
- `window_type.h`
- `vehicle_type.h`
- `vehicle_gui_base.h`
- `vehiclelist.h`
- `order_type.h`
- `station_type.h`
- `engine_type.h`
- `company_type.h`

## Funções Principais
- `ShowVehicleRefitWindow`: Função relacionada à gestão de veículos
- `DrawVehiclePurchaseInfo`: Função relacionada à gestão de veículos
- `DrawTrainImage`: Função relacionada à gestão de veículos
- `DrawRoadVehImage`: Função relacionada à gestão de veículos
- `DrawShipImage`: Função relacionada à gestão de veículos
- `DrawAircraftImage`: Função relacionada à gestão de veículos
- `ShowBuildVehicleWindow`: Função relacionada à gestão de veículos
- `ShowRefitOptionsList`: Função relacionada à gestão de veículos
- `ShowVehicleListWindow`: Função relacionada à gestão de veículos
- `ShowVehicleListWindow`: Função relacionada à gestão de veículos
- `ShowVehicleListWindow`: Função relacionada à gestão de veículos
- `ShowVehicleListWindow`: Função relacionada à gestão de veículos
- `GetSingleVehicleWidth`: Função relacionada à gestão de veículos
- `GetVehicleWidth`: Função relacionada à gestão de veículos
- `ShowVehicleViewWindow`: Função relacionada à gestão de veículos
- ... e mais 6 funções

## Estruturas de Dados
- `TestedEngineDetails`: Estrutura para dados de veículos
- `VehicleCellSize`: Estrutura para dados de veículos
- `Viewport`: Estrutura para dados de veículos

## Definições e Macros
- `VEHICLE_GUI_H`: Macro de definição

## Enumerações
- `TrainDetailsWindowTabs`: Tipo enumerado para opções de veículos
- `VehicleInvalidateWindowData`: Tipo enumerado para opções de veículos

## Responsabilidades
- Gerenciar operações relacionadas a veículos
- Definir tipos e constantes para veículos
- Fornecer interface para movimentação e controle de veículos

## Integração
Este arquivo se integra com sistemas de pathfinding, ordens, economia e infraestrutura do OpenTTD.
