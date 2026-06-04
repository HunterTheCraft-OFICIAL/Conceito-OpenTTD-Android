# Sistema de Janelas e Interface Gráfica (Window GUI)

## Visão Geral
Este arquivo define as estruturas e funções fundamentais para o sistema de janelas do OpenTTD, incluindo a classe base `Window`, descrições de janelas, viewport, e gerenciamento de widgets aninhados.

## Estruturas Principais

### WindowDesc (Descrição da Janela)
Define as propriedades padrão de uma janela:
- **default_pos**: Posição preferencial da janela (manual, automático, centralizado, alinhado à toolbar)
- **cls**: Classe da janela (identificador único)
- **parent_cls**: Classe da janela pai
- **ini_key**: Chave para armazenar configurações no openttd.cfg
- **flags**: Flags padrão da janela (construção, modal, sem foco)
- **nwid_parts**: Partes do widget aninhado que descrevem o layout da janela
- **hotkeys**: Lista de teclas de atalho associadas
- **pref_width/height**: Largura/altura preferidas pelo usuário

**Métodos:**
- `GetDefaultWidth()/GetDefaultHeight()`: Obtém dimensões padrão
- `LoadFromConfig()/SaveToConfig()`: Carrega/salva configurações do arquivo

### WindowFlags (Flags de Janela)
Flags que controlam o estado da janela:
- **WF_TIMEOUT**: Contador de timeout da janela
- **WF_DRAGGING**: Janela está sendo arrastada
- **WF_SIZING_RIGHT/LEFT**: Redimensionamento para direita/esquerda
- **WF_STICKY**: Janela fixa (não fecha ao clicar fora)
- **WF_DISABLE_VP_SCROLL**: Janela não faz autoscroll
- **WF_WHITE_BORDER**: Contador de borda branca
- **WF_HIGHLIGHTED**: Widget com destaque
- **WF_CENTERED**: Janela centralizada

### ResizeInfo
Informações de redimensionamento:
- **step_width**: Passo de mudança de largura
- **step_height**: Passo de mudança de altura

### ViewportData
Dados de viewport da janela:
- **follow_vehicle**: ID do veículo sendo seguido (ou INVALID_VEHICLE)
- **scrollpos_x/y**: Coordenadas atualmente mostradas
- **dest_scrollpos_x/y**: Coordenadas de destino para mostrar

### WidgetDimensions
Dimensões e espaçamentos de widgets:
- Padding para diversos tipos de widgets (botões, scrollbars, bevels, etc.)
- Espaçamentos verticais/horizontais (normal, wide, indent)
- Versões escaladas e não-escaladas para zoom

## Classe Window (Janela)

### Propriedades Principais
- **window_desc**: Descrição da janela
- **flags**: Flags atuais da janela
- **window_class/number**: Identificadores únicos da janela
- **left/top/width/height**: Posição e dimensões em pixels
- **resize**: Informações de redimensionamento
- **owner**: Dono do conteúdo (empresa para cores)
- **viewport**: Dados de viewport (se presente)
- **nested_root/array**: Árvore de widgets aninhados
- **parent**: Janela pai
- **mouse_capture_widget**: Widget com captura do mouse

### Métodos de Inicialização
- `InitializeData()`: Inicializa dados básicos
- `InitNested()`: Inicializa árvore de widgets aninhados
- `CreateNestedTree()`: Cria a árvore de widgets
- `FinishInitNested()`: Finaliza inicialização

### Gerenciamento de Widgets
- `GetWidget<NWID>(widget_index)`: Obtém widget específico
- `GetScrollbar(widget_index)`: Obtém scrollbar
- `GetQueryString(widget_index)`: Obtém string de query
- `SetWidgetDisabledState()`: Habilita/desabilita widget
- `SetWidgetLoweredState()`: Alterna estado pressionado/não-pressionado
- `IsWidgetDisabled/Lowered/Focused()`: Verifica estados do widget
- `SetWidgetHighlight()`: Define destaque no widget
- `SetWidgetDirty()`: Marca widget para redesenho

### Eventos e Callbacks

#### Inicialização e Layout
- `OnInit()`: Notificação de inicialização da árvore de widgets
- `OnInitialPosition()`: Computa posição inicial
- `UpdateWidgetSize()`: Atualiza tamanho e passo de resize de widget
- `SetStringParameters()`: Inicializa parâmetros de string para widgets
- `OnResize()`: Chamado após redimensionamento

#### Pintura e Desenho
- `OnPaint()`: Pintura da janela (chama DrawWidgets por padrão)
- `DrawWidget()`: Desenha conteúdo de widget específico
- `DrawViewport()`: Desenha viewport
- `DrawSortButtonState()`: Desenha estado de botão de ordenação

#### Input e Interação
- `OnKeyPress()`: Tecla pressionada
- `OnHotkey()`: Atalho ativado
- `OnCTRLStateChange()`: Mudança no estado da tecla CTRL
- `OnClick()`: Clique com botão esquerdo
- `OnRightClick()`: Clique com botão direito
- `OnHover()`: Mouse passando sobre widget
- `OnTooltip()`: Exibe tooltip customizado
- `OnMouseDrag()`: Arrastando objeto
- `OnDragDrop()`: Soltou objeto arrastado
- `OnScroll()`: Scroll solicitado
- `OnMouseOver()`: Mouse movendo sobre janela
- `OnMouseWheel()`: Scroll do mouse girado

#### Ciclo de Jogo
- `OnMouseLoop()`: Chamado a cada loop de mouse (mínimo 1x por tick)
- `OnGameTick()`: Chamado uma vez por tick do jogo
- `OnHundredthTick()`: Chamado a cada 100 ticks ou 3s
- `OnRealtimeTick()`: Chamado periodicamente com delta em ms
- `OnTimeout()`: Timeout da janela atingido

#### Dados e Invalidação
- `InvalidateData()`: Marca dados como inválidos
- `ProcessScheduledInvalidations()`: Processa invalidações agendadas
- `OnInvalidateData()`: Notificação de dados inválidos

#### Interação com Mapa
- `OnPlaceObject()`: Usuário clicou no mapa com highlight de tile
- `OnVehicleSelect()`: Usuário clicou em veículo
- `OnPlaceObjectAbort()`: Usuário cancelou highlight
- `SelectLastTool()`: Seleciona ferramenta novamente após cancelamento
- `OnPlaceDrag()`: Arrastando sobre mapa
- `OnPlaceMouseUp()`: Soltou arrasto no mapa
- `OnPlacePresize()`: Modo de pré-dimensionamento (docas, túneis)

#### Editores e Queries
- `HandleEditBoxKey()`: Processa teclas em editbox
- `InsertTextString()`: Insere texto no editbox
- `OnEditboxChanged()`: Texto do editbox modificado
- `OnQueryTextFinished()`: Janela de query fechou
- `OnDropdownSelect()`: Opção de dropdown selecionada
- `OnDropdownClose()`: Dropdown fechado

#### Foco
- `OnFocus()`: Janela ganhou foco
- `OnFocusLost()`: Janela perdeu foco
- `SetFocusedWidget()`: Define widget focado
- `UnfocusFocusedWidget()`: Remove foco do widget atual
- `IsWidgetGloballyFocused()`: Verifica se widget tem foco global

### Métodos de Utilidade
- `SetTimeout()`: Inicia timer de timeout
- `SetWhiteBorder()`: Inicia timer de borda branca
- `RaiseButtons()`: Levanta todos os botões
- `CloseChildWindows()`: Fecha janelas filhas
- `Close()`: Fecha esta janela
- `DeleteClosedWindows()`: Remove janelas fechadas da memória
- `SetDirty()`: Marca janela para redesenho
- `ReInit()`: Re-inicializa janela
- `SetShaded()/IsShaded()`: Controla estado "recolhido" da janela
- `HandleButtonClick()`: Processa clique de botão
- `GetRowFromWidget()`: Obtém linha de posição em widget

### Iteradores de Janela
- `WindowIterator`: Itera sobre janelas válidas
- `AllWindows`: Conjunto iterável de todas as janelas
- Suporta iteração para frente/trás na ordem Z

## Funções Globais

### Gerenciamento de Janelas
- `BringWindowToFrontById()`: Traz janela específica para frente
- `FindWindowFromPt()`: Encontra janela em coordenadas x,y
- `AllocateWindowDescFront()`: Aloca nova janela ou retorna existente
- `RelocateAllWindows()`: Realoca todas as janelas para novas dimensões
- `MoveAllWindowsOffScreen()`: Move janelas para fora da tela
- `MoveAllHiddenWindowsBackToScreen()`: Traz janelas ocultas de volta
- `SetFocusedWindow()`: Define janela focada
- `DeleteClosedWindows()`: Limpa janelas fechadas

### Tooltips
- `GuiShowTooltips()`: Exibe tooltips com parâmetros

### Widgets
- `GetWidgetFromPos()`: Obtém widget de posição x,y
- `DrawFrameRect()`: Desenha retângulo com frame estilizado
- `DrawCaption()`: Desenha legenda de janela

### Scrollbars
- `ScrollbarClickHandler()`: Processa clique em scrollbar
- Variáveis globais: `_scrollbar_start_pos`, `_scrollbar_size`, `_scroller_click_timeout`

### Cursor e Mouse
- `_cursorpos_drag_start`: Posição inicial do arrasto
- `_scrolling_viewport`: Flag de viewport scrollando
- `_mouse_hovering`: Flag de mouse em hover
- `_special_mouse_mode`: Modo especial do mouse (drag&drop, sizing, presize, dragging)
- `GetWindowDraggedOffScreen()`: Verifica se janela foi arrastada para fora

## Classes Auxiliares

### PickerWindowBase
Classe base para janelas abertas de toolbars:
- Mantém referência à janela pai
- Override do método Close()

## Constantes Importantes

### Timeouts
- `TIMEOUT_DURATION = 7`: Valor inicial do timer WF_TIMEOUT
- `WHITE_BORDER_DURATION = 3`: Valor inicial do timer WF_WHITE_BORDER
- `SCROLLER_CLICK_DELAY = 6`: Delay entre scrolls da scrollbar

### Modos Especiais de Mouse
- **WSM_NONE**: Sem modo especial
- **WSM_DRAGDROP**: Modo de arrastar e soltar
- **WSM_SIZING**: Modo de redimensionamento
- **WSM_PRESIZE**: Modo de pré-dimensionamento
- **WSM_DRAGGING**: Modo de arrasto (árvores)

### Estados de Botão de Ordenação
- **SBS_OFF**: Não ordenar
- **SBS_DOWN**: Ordenar ascendente
- **SBS_UP**: Ordenar descendente

### Posicionamento de Janela
- **WDP_MANUAL**: Posicionamento manual
- **WDP_AUTO**: Posicionamento automático
- **WDP_CENTER**: Centralizar janela
- **WDP_ALIGN_TOOLBAR**: Alinhar à toolbar

### Condições de Fechamento de Tooltip
- **TCC_RIGHT_CLICK**: Fecha com clique direito
- **TCC_HOVER**: Fecha ao sair do hover
- **TCC_NONE**: Não fecha automaticamente
- **TCC_EXIT_VIEWPORT**: Fecha ao sair da viewport

## Fluxo de Funcionamento

1. **Criação**: WindowDesc define propriedades, AllocateWindowDescFront cria instância
2. **Inicialização**: InitNested cria árvore de widgets, OnInit permite customização
3. **Posicionamento**: OnInitialPosition calcula posição inicial baseada em preferências
4. **Renderização**: OnPaint chama DrawWidgets que desenha todos os widgets
5. **Event Loop**: 
   - Input do usuário dispara callbacks (OnClick, OnKeyPress, etc.)
   - Game ticks chamam OnGameTick, OnHundredthTick
   - Invalidações de dados disparam OnInvalidateData e redesenho
6. **Interação com Mapa**: Callbacks específicos para colocação de objetos, drag&drop
7. **Fechamento**: Close() remove janela, DeleteClosedWindows() limpa memória

## Padrões de Implementação

### Template GetWidget
- Acesso type-safe a widgets específicos via template
- Retorna nullptr se widget não existir ou tipo incompatível
- Versões const e non-const disponíveis

### Invalidação de Dados
- InvalidateData() agenda atualização com código de dados opcional
- gui_scope indica se está em escopo GUI seguro
- ProcessScheduledInvalidations() processa atualizações pendentes

### Hierarquia de Janelas
- Janelas podem ter pai (parent)
- Fechar pai pode fechar filhos (CloseChildWindows)
- Ordem Z controlada por _z_windows list

### Widgets Aninhados
- nested_root aponta para raiz da árvore
- nested_array fornece acesso rápido por índice
- NWidgetStacked permite múltiplos "planos" visíveis (ex: shading)

## Notas de Implementação

- A classe Window usa ZeroedMemoryAllocator para inicialização zero
- Copy constructor deletado para arrays de Window
- Deletion protegida: apenas DeleteClosedWindows() pode deletar
- Suporte a NewGRF inspection via IsNewGRFInspectable/ShowNewGRFInspectWindow
- QueryStrings associados a WWT_EDITBOX widgets gerenciados via SmallMap
