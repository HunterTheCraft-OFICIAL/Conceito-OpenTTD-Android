# Interface Gráfica de Grupos (Group GUI)

## Visão Geral
Este arquivo define as funções relacionadas à interface gráfica de gerenciamento de grupos de veículos no OpenTTD. Grupos permitem que os jogadores organizem e gerenciem frota de veículos de forma eficiente.

## Funções Principais

### ShowCompanyGroup
**Propósito:** Exibe a janela de gerenciamento de grupos para uma empresa específica.

**Parâmetros:**
- `company` (CompanyID): Identificador da empresa dona dos grupos
- `veh` (VehicleType): Tipo de veículo (trem, caminhão, ônibus, navio, aeronave)
- `group` (GroupID): ID do grupo específico a ser exibido (padrão: INVALID_GROUP para mostrar lista geral)
- `need_existing_window` (bool): Se true, apenas foca na janela se já existir; se false, cria nova janela se necessário

**Comportamento:**
- Abre ou foca na janela de grupos da empresa especificada
- Filtra pelo tipo de veículo indicado
- Opcionalmente seleciona um grupo específico
- Controla se deve criar nova janela ou reutilizar existente

### ShowCompanyGroupForVehicle
**Propósito:** Exibe a janela de grupos destacando o grupo ao qual um veículo específico pertence.

**Parâmetros:**
- `v` (const Vehicle*): Ponteiro para o veículo cujo grupo será mostrado

**Comportamento:**
- Identifica o grupo ao qual o veículo pertence
- Abre a janela de grupos apropriada
- Destaca/seleciona automaticamente o grupo relevante
- Útil para gerenciamento rápido a partir da visualização de veículos individuais

### DeleteGroupHighlightOfVehicle
**Propósito:** Remove destaque de grupo associado a um veículo quando ele é deletado ou muda de grupo.

**Parâmetros:**
- `v` (const Vehicle*): Ponteiro para o veículo cujo destaque será removido

**Comportamento:**
- Limpa referências de destaque em janelas de grupo abertas
- Previne referências inválidas após deleção de veículos
- Mantém consistência da interface quando veículos são removidos

## Integração com Sistema de Grupos
- Trabalha em conjunto com `group.h` e `group_type.h`
- Usa sistema de janelas definido em `window.h`
- Integra-se com UI de veículos para seleção rápida de grupos
- Suporta todos os tipos de veículos do jogo

## Casos de Uso Típicos
1. Jogador clica em botão "Grupos" na barra de ferramentas da empresa
2. Jogador clica com botão direito em um veículo para ver/gerenciar seu grupo
3. Veículo é vendido/destruído e precisa limpar destaques na UI
4. Troca rápida entre visualização de diferentes tipos de grupos (trens, caminhões, etc.)
