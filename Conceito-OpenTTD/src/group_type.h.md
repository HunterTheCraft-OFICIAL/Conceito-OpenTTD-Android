# 📋 Tipos de Grupos de Veículos

## Visão Geral
Definições de tipos e constantes para sistema de grupos de veículos no OpenTTD.

## Estrutura Principal

### Enumerações

#### GroupID
- Identificador único para cada grupo
- Valores especiais para grupos padrão (todos os veículos, sem grupo, etc.)

#### GroupType
- Tipo de grupo (padrão ou personalizado)
- Define comportamento e permissões do grupo

#### VehicleGroupFlag
- Flags para propriedades de grupos
- Controle de visibilidade, proteção e outras características

### Constantes

- **INVALID_GROUP**: ID inválido de grupo
- **DEFAULT_GROUP**: Grupo padrão para novos veículos
- **ALL_VEHICLES_GROUP**: Grupo especial contendo todos os veículos

### Estruturas de Dados

#### GroupData
- Informações básicas do grupo
- Nome, cor, estatísticas e configurações

#### GroupStatistics
- Dados de desempenho do grupo
- Lucro, idade média, estado dos veículos, etc.

## Integração

- Utilizado por `group_gui.h` para interface
- Conecta-se com `vehicle_type.h` para tipos de veículos
- Integra com `company_type.h` para grupos por empresa

## Notas de Implementação

- Suporta até 256 grupos personalizados por empresa
- IDs negativos reservados para grupos do sistema
- Permite herança de propriedades entre grupos
