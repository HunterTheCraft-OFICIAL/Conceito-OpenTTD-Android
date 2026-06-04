# 📄 widget_type.h - Definições de Widgets da Interface

## Visão Geral
Arquivo de cabeçalho que define **todos os tipos de widgets** usados no sistema de interface aninhada (nested widgets) do OpenTTD. Este é o arquivo fundamental que estabelece a base para construção de interfaces gráficas complexas através de composição hierárquica de elementos visuais.

---

## Constantes Fundamentais

### WIDGET_LIST_END
```cpp
static const int WIDGET_LIST_END = -1;
```
Marcador especial que indica o **fim da lista de widgets** em funções variádicas. Usado para terminação segura de arrays de definição de widgets.

---

## Enums de Configuração de Widgets

### MatrixWidgetValues
Configurações para o widget `WWT_MATRIX` (grade/matriz).

**Bits de Coluna:**
- `MAT_COL_START = 0` → Bit inicial do número de colunas
- `MAT_COL_BITS = 8` → Número de bits reservados para colunas

**Bits de Linha:**
- `MAT_ROW_START = 8` → Bit inicial do número de linhas
- `MAT_ROW_BITS = 8` → Número de bits reservados para linhas

**Uso**: Permite armazenar dimensões de matriz (até 256x256) em um único valor de 16 bits.

---

### ArrowWidgetValues
Valores para widgets de seta (`WWT_ARROWBTN`).

| Valor | Descrição | Comportamento |
|-------|-----------|---------------|
| `AWV_DECREASE` | Seta de diminuição | Esquerda (ou direita em RTL*) |
| `AWV_INCREASE` | Seta de aumento | Direita (ou esquerda em RTL*) |
| `AWV_LEFT` | Seta forçada à esquerda | Sempre aponta para esquerda |
| `AWV_RIGHT` | Seta forçada à direita | Sempre aponta para direita |

*RTL = Right-to-Left (idiomas como árabe/hebraico)

---

### NWidSizingType
Tipos de dimensionamento mínimo automático para widgets.

| Tipo | Descrição |
|------|-----------|
| `NWST_NONE` | Sem dimensionamento automático |
| `NWST_BUTTON` | Usa `_settings_client.gui.min_button` como mínimo |
| `NWST_VIEWPORT` | Tipo especial para viewports |
| `NWST_END` | Marcador de fim |

---

## WidgetType - Tipos de Widgets

### Widgets de Janela (Window Widget Types)

#### Widgets Básicos de Conteúdo

| Tipo | Descrição | Uso Típico |
|------|-----------|------------|
| `WWT_EMPTY` | Widget vazio | Reservar espaço no array |
| `WWT_PANEL` | Painel rebaixado simples | Fundos, containers |
| `WWT_INSET` | Painel pressionado (inserido) | Áreas de texto de combo boxes |
| `WWT_LABEL` | Rótulo centralizado | Textos informativos |
| `WWT_TEXT` | Texto puro simples | Exibição de texto |
| `WWT_FRAME` | Moldura | Agrupamento visual |
| `WWT_CAPTION` | Legenda da janela | Título entre botões de fechar e fixar |

#### Botões

| Tipo | Descrição | Comportamento |
|------|-----------|---------------|
| `WWT_IMGBTN` | Botão com imagem | Toggle opcional |
| `WWT_IMGBTN_2` | Botão com imagem alternativa | Imagem diferente quando clicado |
| `WWT_ARROWBTN` | Botão com seta | Navegação, incremento/decremento |
| `WWT_TEXTBTN` | Botão com texto | Toggle opcional |
| `WWT_TEXTBTN_2` | Botão com texto alternativo | Texto diferente quando clicado |
| `WWT_MATRIX` | Grade de linhas e colunas | Listas em grade, inventários |

#### Controles de Janela (Canto Superior Direito)

| Tipo | Posição | Função |
|------|---------|--------|
| `WWT_DEBUGBOX` | Entre caption e shadebox | Debug de NewGRF |
| `WWT_SHADEBOX` | Entre debugbox e defsizebox | Minimizar janela (sombr ear) |
| `WWT_DEFSIZEBOX` | Entre shadebox e stickybox | Restaurar tamanho padrão |
| `WWT_STICKYBOX` | Após defsizebox | Fixar janela (sticky) |

#### Outros Controles

| Tipo | Descrição |
|------|-----------|
| `WWT_RESIZEBOX` | Alça de redimensionamento (canto inferior direito) |
| `WWT_CLOSEBOX` | Botão de fechar (canto superior esquerdo) |
| `WWT_DROPDOWN` | Lista suspensa (dropdown) |
| `WWT_EDITBOX` | Caixa de texto editável |
| `WWT_LAST` | Último item (usar WIDGETS_END para padding) |

---

### Tipos de Widgets Aninhados (Nested Widget Types)

Containers e elementos estruturais para layout.

| Tipo | Descrição | Layout |
|------|-----------|--------|
| `NWID_HORIZONTAL` | Container horizontal | Widgets em linha (L→R ou R→L em RTL) |
| `NWID_HORIZONTAL_LTR` | Container horizontal LTR | Sempre da esquerda para direita |
| `NWID_VERTICAL` | Container vertical | Widgets em coluna (cima→baixo) |
| `NWID_MATRIX` | Container matricial | Grade de widgets |
| `NWID_SPACER` | Espaçador invisível | Reserva espaço vazio |
| `NWID_SELECTION` | Pilha de widgets | Apenas um visível por vez (tabs) |
| `NWID_VIEWPORT` | Widget de viewport | Exibe área do mapa |
| `NWID_BUTTON_DROPDOWN` | Botão com dropdown | Combinação botão+lista |
| `NWID_HSCROLLBAR` | Barra de rolagem horizontal | Scroll horizontal |
| `NWID_VSCROLLBAR` | Barra de rolagem vertical | Scroll vertical |

---

### Tipos de Partes de Widgets (Nested Widget Part Types)

Componentes para configuração detalhada de widgets.

| Tipo | Finalidade |
|------|-----------|
| `WPT_RESIZE` | Especificar redimensionamento |
| `WPT_SIZINGTYPE` | Especificar modo de dimensionamento |
| `WPT_MINSIZE` | Especificar tamanho mínimo |
| `WPT_MINTEXTLINES` | Especificar número mínimo de linhas de texto |
| `WPT_FILL` | Especificar preenchimento (fill) |
| `WPT_DATATIP` | Especificar dados e tooltip |
| `WPT_PADDING` | Especificar espaçamento interno (padding) |
| `WPT_PIPSPACE` | Especificar espaços pré/inter/pós para containers |
| `WPT_TEXTCOLOUR` | Especificar cor do texto |
| `WPT_ALIGNMENT` | Especificar alinhamento de texto/imagem |
| `WPT_ENDCONTAINER` | Marcar fim de container |
| `WPT_FUNCTION` | Chamar função definida pelo usuário |
| `WPT_SCROLLBAR` | Anexar barra de rolagem |

---

### Tipos de Botões Pressionáveis (Pushable Window Widget Types)

#### Máscara e Bit Flag
```cpp
WWT_MASK = 0x7F           // Máscara para tipo base
WWB_PUSHBUTTON = 1 << 7   // Bit flag para botão pressionável
```

#### Combinações Pré-definidas

| Tipo | Base + Flag | Descrição |
|------|-------------|-----------|
| `WWT_PUSHBTN` | WWT_PANEL + PUSHBUTTON | Botão push normal com desenho customizado |
| `WWT_PUSHTXTBTN` | WWT_TEXTBTN + PUSHBUTTON | Botão push com legenda de texto |
| `WWT_PUSHIMGBTN` | WWT_IMGBTN + PUSHBUTTON | Botão push com legenda de imagem |
| `WWT_PUSHARROWBTN` | WWT_ARROWBTN + PUSHBUTTON | Botão push com seta |
| `NWID_PUSHBUTTON_DROPDOWN` | NWID_BUTTON_DROPDOWN + PUSHBUTTON | Botão container com dropdown |

---

## SizingType - Tipos de Dimensionamento

Enum usado em `NWidgetBase::AssignSizePosition()` para controle de layout.

| Tipo | Descrição | Efeitos |
|------|-----------|---------|
| `ST_SMALLEST` | Inicializar ao menor tamanho | Atualiza `current_x` e `current_y` |
| `ST_RESIZE` | Redimensionar árvore de widgets | Ajusta tamanhos conforme espaço disponível |

---

## Classe NWidgetBase - Base para Widgets Aninhados

Classe base abstrata para todos os widgets aninhados. Define a interface comum.

### Invariantes de Design
Após inicialização:
- `current_x = smallest_x + n * resize_x`, onde `n ≥ 0`
- `current_y = smallest_y + m * resize_y`, onde `m ≥ 0`

### Métodos Virtuais Puros (Obrigatórios)

| Método | Responsabilidade |
|--------|-----------------|
| `SetupSmallestSize(w, init_array)` | Calcular tamanho mínimo do widget |
| `AssignSizePosition(sizing, x, y, width, height, rtl)` | Atribuir tamanho e posição final |
| `FillNestedArray(array, length)` | Preencher array de widgets aninhados |
| `GetWidgetFromPos(x, y)` | Encontrar widget na posição (x,y) |
| `Draw(w)` | Renderizar o widget |

### Métodos Virtuais com Implementação Padrão

| Método | Padrão | Sobrescrita |
|--------|--------|-------------|
| `AdjustPaddingForZoom()` | Ajusta padding para zoom | Personalizado por tipo |
| `GetWidgetOfType(tp)` | Busca widget por tipo | Recursivo em containers |
| `IsHighlighted()` | Retorna `false` | Widgets interativos |
| `GetHighlightColour()` | Retorna `TC_INVALID` | Widgets com highlight |
| `SetHighlighted(colour)` | Não faz nada | Widgets destacáveis |
| `SetDirty(w)` | Marca janela como suja | Para redesenho |

### Métodos de Padding (Inline)

```cpp
// Versão com 4 parâmetros
SetPadding(top, right, bottom, left)

// Versão com RectPadding
SetPadding(padding)
```

### Métodos de Step Size

```cpp
GetHorizontalStepSize(sizing)  // Passo horizontal de redimensionamento
GetVerticalStepSize(sizing)    // Passo vertical de redimensionamento
```

### Atributos Públicos

| Atributo | Tipo | Descrição |
|----------|------|-----------|
| `type` | WidgetType | Tipo do widget |
| `sizing_type` | NWidSizingType | Tipo de dimensionamento mínimo |
| `fill_x` | uint | Passo de preenchimento horizontal (0 = não redimensionável) |
| `fill_y` | uint | Passo de preenchimento vertical (0 = não redimensionável) |
| `resize_x` | uint | Passo de redimensionamento horizontal |
| `resize_y` | uint | Passo de redimensionamento vertical |
| `smallest_x` | uint | Largura mínima |
| `smallest_y` | uint | Altura mínima |
| `current_x` | uint | Largura atual |
| `current_y` | uint | Altura atual |
| `pos_x` | uint | Posição X do canto superior esquerdo |
| `pos_y` | uint | Posição Y do canto superior esquerdo |
| `uz_padding` | RectPadding | Espaçamento interno (upscaled para zoom) |

### Método Utilitário

```cpp
GetCurrentRect()
```
Retorna `Rect` representando a área atual ocupada pelo widget.

---

## Forward Declarations

Declarações antecipadas para evitar inclusões circulares:
- `class NWidgetCore`
- `class Scrollbar`

---

## Funções Auxiliares (Widget Parts)

### Funções de Configuração de Data/Tooltip

#### SetDataTip(data, tip)
Define dados e tooltip para um widget.

#### SetStringTip(string, tip)
Converte StringID para dados e define tooltip.

#### SetMatrixDataTip(cols, rows, tip)
Configura matriz com colunas, linhas e tooltip.
```cpp
// Combina cols e rows em um único valor
(rows << MAT_ROW_START) | (cols << MAT_COL_START)
```

---

### Funções de Padding

#### SetPadding(top, right, bottom, left)
Define espaçamento interno com 4 valores individuais.

#### SetPadding(RectPadding)
Define padding usando estrutura RectPadding.

#### SetPadding(padding)
Define padding uniforme para todos os lados.

---

### Funções de Espaçamento de Container

#### SetPIP(pre, inter, post)
Configura espaços em containers:
- `pre` → Espaço antes do primeiro widget
- `inter` → Espaço entre widgets
- `post` → Espaço após o último widget

---

### Funções de Scrollbar

#### SetScrollbar(index)
Anexa barra de rolagem a um widget.
- Permite controle via mouse wheel
- Múltiplos widgets podem referenciar mesma scrollbar

---

### Funções de Criação de Widgets

#### NWidget(tp, col, idx)
Cria novo widget "real":
- `tp` → Tipo do widget
- `col` → Cor (Colours)
- `idx` → Índice no array de widgets (-1 = não especificado)

**Nota**: `WWT_PANEL`, `WWT_FRAME`, `WWT_INSET` iniciam novos containers. Widgets filhos devem ter índices maiores que o pai.

#### NWidget(tp, cont_flags)
Cria containers especiais:
- `NWID_HORIZONTAL`, `NWID_VERTICAL`, `NWID_SPACER`, `NWID_SELECTION`, `NWID_MATRIX`
- `cont_flags` → Flags adicionais para containers

#### NWidgetFunction(func_ptr)
Obtém subárvore de widgets de fonte externa.
- `func_ptr` → Ponteiro para função que retorna a árvore

---

## Funções de Construção de Alto Nível

### MakeNWidgets(parts, count, biggest_index, container)
Constrói widgets aninhados a partir de array de partes.

### MakeWindowNWidgetTree(parts, count, biggest_index, shade_select)
Cria árvore completa de widgets para uma janela.

### MakeCompanyButtonRows(biggest_index, widget_first, widget_last, button_colour, max_length, button_tooltip)
Gera fileiras de botões de empresa automaticamente.

### SetupWidgetDimensions()
Inicializa dimensões padrão de widgets (chamada na inicialização).

---

## Padrões de Nomenclatura

### Em Português (Conceitual)

| Inglês | Português |
|--------|-----------|
| Widget | Componente / Elemento Visual |
| Nested Widget | Widget Aninhado |
| Container | Container / Agrupador |
| Padding | Espaçamento Interno |
| Tooltip | Dica / Tooltip |
| Scrollbar | Barra de Rolagem |
| Viewport | Área de Visualização / Viewport |
| Caption | Legenda / Título |
| Label | Rótulo / Etiqueta |
| Button | Botão |
| Panel | Painel |
| Frame | Moldura |
| Matrix | Matriz / Grade |
| Dropdown | Lista Suspensa |
| Edit Box | Caixa de Edição |
| Resize | Redimensionar |
| Sticky | Fixo / Permanente |
| Shade | Minimizar / Sombrear |
| Debug | Depuração |

---

## Fluxo de Construção de Interface

### 1. Definição de Partes de Widget
```cpp
NWidgetPart widget_parts[] = {
    NWidget(WWT_CAPTION, COLOUR_BLUE), SetDataTip(STR_WINDOW_TITLE, STR_TOOLTIP),
    NWidget(WWT_CLOSEBOX, COLOUR_BLUE),
    NWidget(NWID_HORIZONTAL),
        NWidget(WWT_PANEL, COLOUR_BLUE), SetPadding(2, 2, 2, 2),
            // Widgets filhos aqui
        EndContainer,
    EndContainer,
};
```

### 2. Construção da Árvore
```cpp
int biggest_index = 0;
NWidgetContainer *tree = MakeWindowNWidgetTree(
    widget_parts, 
    num_parts, 
    &biggest_index, 
    &shade_select
);
```

### 3. Inicialização de Tamanhos
```cpp
tree->SetupSmallestSize(window, true);
```

### 4. Posicionamento e Redimensionamento
```cpp
tree->AssignSizePosition(ST_SMALLEST, 0, 0, min_width, min_height, rtl);
// ou
tree->AssignSizePosition(ST_RESIZE, 0, 0, available_width, available_height, rtl);
```

### 5. Renderização
```cpp
tree->Draw(window);
```

---

## Hierarquia de Classes (Resumo)

```
NWidgetBase (classe base abstrata)
├── NWidgetCore (implementação base para widgets com cor/índice)
│   ├── NWidgetLeaf (widgets folha - botões, textos, etc.)
│   └── NWidgetContainer (containers)
│       ├── NWidgetHorizontal
│       ├── NWidgetVertical
│       ├── NWidgetMatrix
│       ├── NWidgetSelection
│       ├── NWidgetViewport
│       └── NWidgetSpacer
└── NWidgetBackground (widgets com background)
```

---

## Considerações de Design

### Sistema de Composição
- Widgets são construídos através de **composição**, não herança profunda
- Partes de widget (`NWidgetPart`) permitem configuração flexível
- Containers podem ser aninhados arbitrariamente

### Separação de Definição e Instanciação
- Definição: Array estático de `NWidgetPart`
- Instanciação: Funções `MakeNWidgets*` convertem partes em objetos
- Vantagem: Definições podem ser compiladas estaticamente

### Suporte a Internacionalização
- `NWID_HORIZONTAL_LTR` preserva ordem em idiomas RTL
- Textos são referenciados por `StringID`, não hardcoded
- Layouts se adaptam a diferentes tamanhos de texto

### Sistema de Cores
- Widgets usam enum `Colours` para padronização
- Permite temas e skins consistentes
- Separação entre lógica e aparência

### Redimensionamento Inteligente
- Step sizes permitem controle fino de comportamento
- Fill vs Resize: fill expande proporcionalmente, resize usa passos fixos
- Minimum sizes garantem usabilidade

---

## Relacionamentos

### Dependências Internas
- `core/alloc_type.hpp` → ZeroedMemoryAllocator
- `core/bitmath_func.hpp` → Funções bit math
- `core/math_func.hpp` → Funções matemáticas
- `strings_type.h` → StringID para textos
- `gfx_type.h` → Tipos gráficos (cores, rects)
- `window_type.h` → Classe Window

### Integração com Sistema de Janelas
- Toda janela tem uma árvore de widgets raiz
- Eventos de mouse/teclado são dispatchados pela árvore
- Desenho é feito recursivamente de cima para baixo

### Conexão com Sistema de Strings
- Tooltips e textos usam `StringID`
- Permite tradução dinâmica
- Separação entre código e conteúdo textual

---

## Casos de Uso Avançados

### Tabs com NWID_SELECTION
```cpp
NWidget(NWID_SELECTION, INVALID_COLOUR),
    // Página 1
    NWidget(NWID_VERTICAL),
        // Widgets da página 1
    EndContainer,
    // Página 2
    NWidget(NWID_VERTICAL),
        // Widgets da página 2
    EndContainer,
EndContainer,
```

### Scroll em Lista Longa
```cpp
NWidget(NWID_VERTICAL),
    NWidget(WWT_MATRIX, COLOUR_GREY, 1), SetScrollbar(2),
    // Itens da matriz
EndContainer,
NWidget(NWID_VSCROLLBAR, COLOUR_GREY, 2),
```

### Botões de Empresa Dinâmicos
```cpp
MakeCompanyButtonRows(
    &biggest_index,
    WIDGET_COMPANY_FIRST,
    WIDGET_COMPANY_LAST,
    COLOUR_ORANGE,
    3,  // 3 botões por linha
    STR_COMPANY_BUTTON_TOOLTIP
);
```

---

## Notas de Implementação

⚠️ **Atenção**: Este é um arquivo conceitual traduzido para documentação em português. A implementação real mantém os nomes originais em inglês no código fonte.

📝 **Observação**: O sistema de nested widgets é uma das partes mais complexas da GUI do OpenTTD, permitindo interfaces altamente customizáveis e responsivas.

🔧 **Performance**: Invariantes matemáticos garantem que cálculos de posicionamento sejam eficientes e previsíveis.

🎨 **Extensibilidade**: Novos tipos de widgets podem ser adicionados estendendo `WidgetType` e criando subclasses de `NWidgetBase`.

---

**Status**: ✅ Traduzido Conceitualmente  
**Nível**: 02 - Sistemas Centrais de Interface  
**Categoria**: GUI / Widgets  
**Última Atualização**: Dezembro 2024
