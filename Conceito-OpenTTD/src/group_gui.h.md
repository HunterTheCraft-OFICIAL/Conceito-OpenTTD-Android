# 📊 Interface Gráfica de Grupos de Veículos

## Visão Geral
Sistema de interface para gerenciamento de grupos de veículos no OpenTTD.

## Estrutura Principal

### Classes e Funções

#### BuildVehicleGroupList
- Lista de construção de grupos de veículos
- Gerencia a exibição de veículos disponíveis para agrupamento

#### BuildCompanyGroupList
- Lista de construção de grupos por empresa
- Organiza veículos por companhia

#### GroupGUIFunctions
- Funções principais da interface de grupos
- Manipulação de criação, edição e exclusão de grupos

### Funcionalidades

- **Criação de Grupos**: Interface para criar novos grupos de veículos
- **Edição de Grupos**: Modificar propriedades de grupos existentes
- **Filtragem**: Filtrar veículos por tipo, status ou outras propriedades
- **Atribuição**: Atribuir veículos a grupos específicos
- **Estatísticas**: Exibir informações sobre desempenho do grupo

### Integração

- Conecta-se ao sistema de veículos (`vehicle.h`)
- Utiliza sistema de janelas (`window.h`)
- Integra com sistema de orders (`order.h`)
- Usa widgets padrão (`widget_type.h`)

## Notas de Implementação

- Mantém consistência com outras interfaces do jogo
- Suporta múltiplos tipos de veículos (trens, caminhões, aviões, navios)
- Permite organização hierárquica de grupos
