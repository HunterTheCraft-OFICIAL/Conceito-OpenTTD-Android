# ⏱️ Funções de Timer para Interface Gráfica

## Visão Geral
Sistema de timers para atualizações periódicas da interface gráfica no OpenTTD.

## Estrutura Principal

### Funções Principais

#### SetWindowDirty
- Marca janelas para atualização na próxima iteração
- Controla refresh de elementos específicos da UI

#### SetWidgetDirty
- Atualiza widgets individuais dentro de janelas
- Otimização para redesenho parcial

#### GUITimer_Update
- Função principal de atualização do timer
- Executada em intervalos regulares

### Intervalos de Timer

- **FAST_UPDATE**: Atualização rápida (animações, efeitos)
- **NORMAL_UPDATE**: Atualização padrão (dados dinâmicos)
- **SLOW_UPDATE**: Atualização lenta (estatísticas, informações)

### Tipos de Eventos

#### TimerEvents
- Eventos disparados por timers
- Callbacks para atualização de UI

#### UpdateFlags
- Flags para controlar quais elementos atualizar
- Otimização de performance

## Integração

- Conecta-se com `window.h` para gerenciamento de janelas
- Utiliza `guitimer_func.h` para funções utilitárias
- Integra com sistema de redraw (`viewport.h`)

## Notas de Implementação

- Timers são sincronizados com o loop principal do jogo
- Suporta múltiplos timers concurrentes
- Prioridade baseada no tipo de atualização
