# Sistema de Tipos de Widgets (Widget Type)

## Visão Geral
Este arquivo define os tipos fundamentais de widgets usados no sistema de interface do OpenTTD, incluindo widgets de janela, widgets aninhados, containers, scrollbars e partes de especificação de widgets hierárquicos.

## Constantes e Enums Principais

### MatrixWidgetValues
Bits para dados do widget WWT_MATRIX:
- **MAT_COL_START/BITS**: Bits para número de colunas (8 bits a partir de 0)
- **MAT_ROW_START/BITS**: Bits para número de linhas (8 bits a partir de 8)

### ArrowWidgetValues
Valores para widgets de seta:
- **AWV_DECREASE**: Seta para esquerda (ou direita em RTL)
- **AWV_INCREASE**: Seta para direita (ou esquerda em RTL)
- **AWV_LEFT**: Força seta para esquerda
- **AWV_RIGHT**: Força seta para direita

### NWidSizingType
Tipos de dimensionamento mínimo:
- **NWST_NONE**: Sem dimensionamento automático
- **NWST_BUTTON**: Tamanho mínimo baseado em min_button das configurações
- **NWST_VIEWPORT**: Tipo de dimensionamento para viewports
- **NWST_END**: Marcador de fim

### WidgetType (Tipos de Widgets)

#### Widgets de Janela
- **WWT_EMPTY**: Widget vazio, placeholder para reservar espaço
- **WWT_PANEL**: Painel depressivo simples
- **WWT_INSET**: Painel pressionado (inserido), usado como área de texto de combo box
- **WWT_IMGBTN**: Botão (toggle) com imagem
- **WWT_IMGBTN_2**: Botão (toggle) com imagem diferente quando clicado
- **WWT_ARROWBTN**: Botão (toggle) com seta
- **WWT_TEXTBTN**: Botão (toggle) com texto
- **WWT_TEXTBTN_2**: Botão (toggle) com texto diferente quando clicado
- **WWT_LABEL**: Label centralizado
- **WWT_TEXT**: Texto puro simples
- **WWT_MATRIX**: Grid de linhas e colunas
- **WWT_FRAME**: Moldura/frame
- **WWT_CAPTION**: Legenda da janela (título entre closebox e stickybox)
- **WWT_DEBUGBOX**: Debug box NewGRF (canto superior direito)
- **WWT_SHADEBOX**: Shade box (recolher janela)
- **WWT_DEFSIZEBOX**: Default size box (tamanho padrão da janela)
- **WWT_STICKYBOX**: Sticky box (fixar janela)
- **WWT_RESIZEBOX**: Resize box (canto inferior direito para redimensionar)
- **WWT_CLOSEBOX**: Close box (canto superior esquerdo para fechar)
- **WWT_DROPDOWN**: Lista dropdown
- **WWT_EDITBOX**: Caixa de texto para digitação
- **WWT_LAST**: Último item (usar WIDGETS_END para padding)

#### Widgets Aninhados
- **NWID_HORIZONTAL**: Container horizontal
- **NWID_HORIZONTAL_LTR**: Container horizontal que não inverte ordem para RTL
- **NWID_VERTICAL**: Container vertical
- **NWID_MATRIX**: Container matrix
- **NWID_SPACER**: Widget invisível que ocupa espaço
- **NWID_SELECTION**: Widgets empilhados, apenas um visível por vez (ex: abas)
- **NWID_VIEWPORT**: Widget contendo viewport
- **NWID_BUTTON_DROPDOWN**: Botão com dropdown
- **NWID_HSCROLLBAR**: Scrollbar horizontal
- **NWID_VSCROLLBAR**: Scrollbar vertical

#### Partes de Widgets Aninhados
- **WPT_RESIZE**: Parte para especificar redimensionamento
- **WPT_SIZINGTYPE**: Parte para especificar modo de dimensionamento
- **WPT_MINSIZE**: Parte para especificar tamanho mínimo
- **WPT_MINTEXTLINES**: Parte para especificar linhas mínimas de texto
- **WPT_FILL**: Parte para especificar preenchimento
- **WPT_DATATIP**: Parte para especificar dados e tooltip
- **WPT_PADDING**: Parte para especificar padding
- **WPT_PIPSPACE**: Parte para especificar espaço pré/inter/pós para containers
- **WPT_TEXTCOLOUR**: Parte para especificar cor do texto
- **WPT_ALIGNMENT**: Parte para especificar alinhamento de texto/imagem
- **WPT_ENDCONTAINER**: Parte para denotar fim de container
- **WPT_FUNCTION**: Parte para chamar função do usuário
- **WPT_SCROLLBAR**: Parte para anexar scrollbar

#### Tipos Pushable
- **WWB_PUSHBUTTON**: Bit para botão push (1 << 7)
- **WWT_PUSHBTN**: Botão push normal com desenho customizado
- **WWT_PUSHTXTBTN**: Botão push normal com legenda de texto
- **WWT_PUSHIMGBTN**: Botão push normal com legenda de imagem
- **WWT_PUSHARROWBTN**: Botão push normal com legenda de seta
- **NWID_PUSHBUTTON_DROPDOWN**: Botão com dropdown pushable

### SizingType
Formas de dimensionar widgets aninhados:
- **ST_SMALLEST**: Inicializa árvore ao menor tamanho, atualiza current_x/y
- **ST_RESIZE**: Redimensiona a árvore de widgets

### NWidgetDisplay (Flags de Display)
Flags que afetam display e interação:
- **NDB_LOWERED**: Widget está pressionado/baixado
- **NDB_DISABLED**: Widget está desabilitado (cinza)
- **NDB_NO_TRANSPARENCY**: Viewport nunca transparente
- **NDB_SHADE_GREY**: Viewport em escala de cinza
- **NDB_SHADE_DIMMED**: Cores dimmed na viewport
- **NDB_DROPDOWN_ACTIVE**: Dropdown do botão está ativo
- **NDB_SCROLLBAR_UP**: Botão up da scrollbar pressionado
- **NDB_SCROLLBAR_DOWN**: Botão down da scrollbar pressionado
- **NDB_HIGHLIGHT**: Highlight do widget ligado

**Macros derivadas:**
- **ND_LOWERED/DISABLED/HIGHLIGHT**: Valores de bit correspondentes
- **ND_NO_TRANSPARENCY/SHADE_GREY/SHADE_DIMMED**: Flags de viewport
- **ND_DROPDOWN_ACTIVE**: Flag de dropdown
- **ND_SCROLLBAR_UP/DOWN/BTN**: Flags de scrollbar

### NWidContainerFlags (Flags de Container)
- **NCB_EQUALSIZE**: Containers mantêm filhos igualmente grandes
- **NCB_BIGFIRST**: Aloca espaço para maior resize primeiro
- **NC_NONE/NW_EQUALSIZE/NC_BIGFIRST**: Macros correspondentes

### StackedZeroSizePlanes
Planos de display com tamanho zero para NWidgetStacked:
- **SZSP_VERTICAL**: Plano com tamanho zero horizontalmente, preenchendo verticalmente
- **SZSP_HORIZONTAL**: Plano com tamanho zero verticalmente, preenchendo horizontalmente
- **SZSP_NONE**: Plano com tamanho zero em ambas direções
- **SZSP_BEGIN**: Primeiro plano de tamanho zero

## Classes Principais

### NWidgetBase (Classe Base)
Classe base para todos os widgets aninhados:

**Propriedades:**
- **type**: Tipo do widget
- **sizing_type**: Tipo de decisão de tamanhos mínimos
- **fill_x/y**: Passo de preenchimento horizontal/vertical
- **resize_x/y**: Passo de redimensionamento horizontal/vertical
- **smallest_x/y**: Menor tamanho possível do widget
- **current_x/y**: Tamanho atual após redimensionamento
- **pos_x/y**: Posição do canto superior esquerdo
- **next/prev**: Ponteiros para próximo/anterior no container
- **padding/uz_padding**: Padding (escalado e não-escalado)

**Métodos Virtuais:**
- `AdjustPaddingForZoom()`: Ajusta padding para zoom
- `SetupSmallestSize()`: Configura menor tamanho
- `AssignSizePosition()`: Atribui tamanho e posição
- `FillNestedArray()`: Preenche array de widgets aninhados
- `GetWidgetFromPos()`: Obtém widget de posição x,y
- `GetWidgetOfType()`: Obtém widget de tipo específico
- `IsHighlighted()/GetHighlightColour()/SetHighlighted()`: Gerencia highlight
- `Draw()`: Desenha o widget
- `SetDirty()`: Marca widget como sujo para redesenho

**Métodos Inline:**
- `SetPadding()`: Define padding adicional
- `GetHorizontal/VerticalStepSize()`: Obtém passo de dimensionamento
- `GetCurrentRect()`: Obtém retângulo atual do widget

### NWidgetResizeBase
Classe base para widgets redimensionáveis:

**Propriedades Adicionais:**
- **min_x/y**: Tamanho mínimo apenas deste widget
- **absolute**: Se tamanho mínimo é fixo
- **uz_min_x/y**: Tamanhos mínimos não-escalados
- **uz_text_lines/spacing/size**: Dados de texto não-escalados

**Métodos:**
- `SetMinimalSize()`: Define tamanho mínimo
- `SetMinimalSizeAbsolute()`: Define tamanho mínimo absoluto
- `SetMinimalTextLines()`: Define linhas mínimas de texto
- `SetMinimalSizeForSizingType()`: Define tamanho baseado no tipo
- `SetFill()`: Define preenchimento
- `SetResize()`: Define redimensionamento

### NWidgetCore (Widget "Real")
Classe base para widgets reais (não-containers):

**Propriedades:**
- **disp_flags**: Flags de display e interação
- **colour**: Cor do widget
- **index**: Índice no array de widgets da janela (-1 se não usado)
- **widget_data**: Dados do widget
- **tool_tip**: Tooltip do widget
- **scrollbar_index**: Índice de scrollbar anexada
- **highlight_colour**: Cor do highlight
- **text_colour**: Cor do texto
- **align**: Alinhamento de texto/imagem

**Métodos:**
- `SetIndex()`: Define índice
- `SetDataTip()`: Define dados e tooltip
- `SetToolTip()`: Define apenas tooltip
- `SetTextColour()`: Define cor do texto
- `SetAlignment()`: Define alinhamento
- `SetLowered()/IsLowered()`: Controla estado pressionado
- `SetDisabled()/IsDisabled()`: Controla estado desabilitado
- `DrawEdgeOrnament*()`: Desenha ornamentos de borda

### NWidgetContainer
Classe base para containers:

**Propriedades:**
- **head/tail**: Ponteiros para primeiro/último widget no container

**Métodos:**
- `Add()`: Adiciona widget ao container
- `IsEmpty()`: Verifica se container está vazio
- `GetWidgetOfType()`: Override para buscar em filhos

### NWidgetStacked
Widgets empilhados ocupando mesmo espaço:

**Propriedades:**
- **shown_plane**: Plano sendo exibido (para NWID_SELECTION)
- **index**: Índice no nested_array da janela

**Métodos:**
- `SetDisplayedPlane()`: Define qual plano mostrar
- `SetIndex()`: Define índice

**Comportamento Especial:**
- Planos SZSP_* têm tamanho zero em uma ou ambas direções
- Trocar para/de planos zero-size requer ReInit() da janela
- Todos os planos são inicializados, permitindo troca dinâmica

### NWidgetPIPContainer
Container com espaço pré/inter/pós:

**Propriedades:**
- **flags**: Flags do container
- **pip_pre/inter/post**: Espaço antes/entre/depois dos widgets
- **uz_pip_pre/inter/post**: Versões não-escaladas

**Métodos:**
- `SetPIP()`: Define espaços PIP

### NWidgetHorizontal / NWidgetHorizontalLTR / NWidgetVertical
Containers de layout específicos:
- **Horizontal**: Layout da esquerda para direita (inverte para RTL)
- **HorizontalLTR**: Layout sempre da esquerda para direita
- **Vertical**: Layout de cima para baixo

### NWidgetMatrix
Container matrix com sub-widgets virtualmente iguais:

**Propriedades:**
- **index**: Índice no nested_array
- **colour**: Cor do widget
- **clicked**: Widget atualmente clicado
- **count**: Quantidade de widgets válidos
- **sb/scrollbar_index**: Scrollbar associada
- **widget_w/h**: Largura/altura do widget filho com espaçamento
- **widgets_x/y**: Número de widgets visíveis em cada direção

**Métodos:**
- `SetClicked()`: Define widget clicado
- `SetCount()`: Define quantidade de widgets
- `SetScrollbar()`: Associa scrollbar
- `GetScrollbar()`: Obtém scrollbar associada
- `GetScrollOffsets()`: Obtém offsets de scroll

### NWidgetSpacer
Widget espaçador invisível:
- Ocupa espaço definido por min_size
- Não desenha nada
- Usado para criar gaps no layout

### NWidgetBackground
Widget de fundo com filho opcional:
- Pode ser usado como leaf widget (espaço simples)
- Pode ser usado como container (fundo para outros widgets)
- **child**: Widget filho (se container)

### NWidgetViewport
Widget para exibir viewport:

**Métodos Especiais:**
- `InitializeViewport()`: Inicializa viewport após criação da árvore
- `UpdateViewportCoordinates()`: Atualiza coordenadas após resize da janela

**Flags Especiais:**
- ND_NO_TRANSPARENCY: Desabilita transparência
- ND_SHADE_GREY: Escala de cinza (jornal B&W)
- ND_SHADE_DIMMED: Cores dimmed (jornal colorido)

### Scrollbar
Estrutura de dados para scrollbar:

**Propriedades:**
- **is_vertical**: Scrollbar é vertical?
- **count**: Número de elementos na lista
- **cap**: Número de elementos visíveis
- **pos**: Índice do primeiro item visível
- **stepsize**: Distância para scroll com botões/wheel

**Enum ScrollbarStepping:**
- **SS_RAW**: Passo em unidades simples
- **SS_SMALL**: Passo em unidades stepsize
- **SS_BIG**: Passo em unidades cap

**Métodos:**
- `GetCount()/GetCapacity()/GetPosition()`: Getters básicos
- `IsVisible()`: Verifica se item está visível
- `IsVertical()`: Verifica orientação
- `SetStepSize()`: Define distância de scroll
- `SetCount()`: Define número de elementos
- `SetCapacity()`: Define capacidade visível
- `SetCapacityFromWidget()`: Define capacidade baseada em widget
- `SetPosition()`: Define posição do primeiro elemento
- `UpdatePosition()`: Atualiza posição por diferença
- `ScrollTowards()`: Scroll para tornar item visível
- `GetScrolledRowFromWidget()`: Obtém linha de clique
- `UpdateListPositionOnKeyPress()`: Atualiza posição com teclado

### NWidgetScrollbar
Scrollbar como widget aninhado:
- Combina NWidgetCore e Scrollbar
- Métodos estáticos para cache de dimensões
- `GetVertical/HorizontalDimension()`: Dimensões cached

### NWidgetLeaf
Widget folha (terminal):
- Widgets básicos como botões, labels, etc.
- `ButtonHit()`: Verifica clique no botão
- Dimensões cached para vários tipos de widgets

## Partes de Especificação de Widgets (NestedWidgetParts)

### Estruturas de Partes
- **NWidgetPartDataTip**: data + tooltip
- **NWidgetPartWidget**: colour + index
- **NWidgetPartPaddings**: RectPadding completo
- **NWidgetPartPIP**: pre/inter/post spaces
- **NWidgetPartTextLines**: lines/spacing/size
- **NWidgetPartTextColour**: TextColour
- **NWidgetPartAlignment**: StringAlignment

### Funções de Partes (Macros Inline)

#### Dimensionamento
- `SetResize(dx, dy)`: Define passo de resize
- `SetSizingType(type)`: Define tipo de sizing automático
- `SetMinimalSize(x, y)`: Define tamanho mínimo
- `SetMinimalTextLines(lines, spacing, size)`: Define linhas mínimas de texto
- `SetFill(fill_x, fill_y)`: Define passo de fill

#### Aparência
- `SetTextColour(colour)`: Define cor do texto
- `SetAlignment(align)`: Define alinhamento
- `SetDataTip(data, tip)`: Define dados e tooltip
- `SetMatrixDataTip(cols, rows, tip)`: Define dados para matrix

#### Espaçamento
- `SetPadding(top, right, bottom, left)`: Padding direcional
- `SetPadding(RectPadding)`: Padding via struct
- `SetPadding(padding)`: Padding uniforme
- `SetPIP(pre, inter, post)`: Espaços entre widgets

#### Containers e Estrutura
- `EndContainer()`: Fim de container
- `SetScrollbar(index)`: Anexa scrollbar
- `NWidget(tp, col, idx)`: Inicia widget real
- `NWidget(tp, cont_flags)`: Inicia container/spacer
- `NWidgetFunction(func_ptr)`: Obtém árvore de função externa

#### Utilitários
- `MakeNWidgets()`: Cria widgets de array de partes
- `MakeWindowNWidgetTree()`: Cria árvore completa de janela
- `MakeCompanyButtonRows()`: Cria botões de empresa
- `SetupWidgetDimensions()`: Inicializa dimensões de widgets
- `GetMinButtonSize()`: Obtém tamanho mínimo para touch
- `ComputeMaxSize()`: Calcula tamanho máximo possível

## Padrões de Uso

### Definição de Janelas com NestedWidgetParts
```cpp
static const NWidgetPart _nested_widgets[] = {
    NWidget(NWID_HORIZONTAL),
        NWidget(WWT_CLOSEBOX, COLOUR_GREY), SetDataTip(STR_NULL, STR_TOOLTIP_CLOSE_WINDOW),
        NWidget(WWT_CAPTION, COLOUR_GREY), SetDataTip(STR_WINDOW_TITLE, STR_TOOLTIP_WINDOW_TITLE),
        NWidget(WWT_SHADEBOX, COLOUR_GREY),
    EndContainer(),
    // ... mais widgets
};
```

### Hierarquia de Herança
```
NWidgetBase (base)
├── NWidgetResizeBase
│   ├── NWidgetCore
│   │   ├── NWidgetBackground
│   │   ├── NWidgetViewport
│   │   ├── NWidgetScrollbar
│   │   └── NWidgetLeaf
│   └── NWidgetSpacer
└── NWidgetContainer
    ├── NWidgetStacked
    ├── NWidgetPIPContainer
    │   ├── NWidgetHorizontal
    │   │   └── NWidgetHorizontalLTR
    │   ├── NWidgetVertical
    │   └── NWidgetMatrix
    └── NWidgetBackground (também herda de NWidgetCore)
```

## Fluxo de Inicialização de Widgets

1. **Definição**: Array de NWidgetPart define estrutura da janela
2. **Criação**: MakeWindowNWidgetTree() converte partes em objetos
3. **Setup Smallest Size**: SetupSmallestSize() calcula tamanhos mínimos recursivamente
4. **Assign Size Position**: AssignSizePosition() posiciona widgets na janela
5. **Fill Nested Array**: FillNestedArray() preenche array de acesso rápido da janela
6. **Draw**: Draw() renderiza widgets durante OnPaint()

## Otimizações

### Cache de Dimensões
- Scrollbars, botões, boxes mantêm dimensões cached
- InvalidateDimensionCache() força recálculo quando necessário
- Evita cálculos repetidos durante redraw

### Unscaled Values
- Valores uz_* armazenam medidas não-escaladas
- Permitem recálculo preciso durante zoom
- AdjustPaddingForZoom() aplica fator de zoom

## Notas de Implementação

- Widgets usam ZeroedMemoryAllocator para inicialização zero
- Containers gerenciam next/prev para iteração
- Index -1 indica widget não usável diretamente
- WWT_MATRIX usa bits especiais para rows/cols no widget_data
- Scrollbars podem ser compartilhadas entre múltiplos widgets
- NWidgetStacked permite switching dinâmico de "planes"
- Sistema suporta RTL (right-to-left) automaticamente
- Templates e funções inline maximizam performance
