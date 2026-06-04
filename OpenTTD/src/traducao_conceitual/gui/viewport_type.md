# Sistema de Tipos de Viewport (Viewport Type)

## Visão Geral
Este arquivo define os tipos fundamentais relacionados a viewports no OpenTTD, incluindo a estrutura principal de viewport, signs visíveis, métodos de seleção de área no mapa, e processos de drag-and-drop para construção e modificação do terreno.

## Estruturas Principais

### Viewport
Estrutura principal para visualização de uma parte do mundo:

**Coordenadas de Tela:**
- **left**: Coordenada de tela da borda esquerda da viewport
- **top**: Coordenada de tela da borda superior da viewport
- **width**: Largura da viewport em pixels na tela
- **height**: Altura da viewport em pixels na tela

**Coordenadas Virtuais:**
- **virtual_left**: Coordenada virtual esquerda (mundo do jogo)
- **virtual_top**: Coordenada virtual superior (mundo do jogo)
- **virtual_width**: Largura virtual (`width << zoom`)
- **virtual_height**: Altura virtual (`height << zoom`)

**Propriedades:**
- **zoom**: Nível de zoom atual da viewport
- **overlay**: Ponteiro para LinkGraphOverlay (grafo de conexões de carga)

**Relações:**
- Coordenadas virtuais = coordenadas de tela * fator de zoom
- Zoom é representado como shift bit (<< zoom)
- Overlay mostra rotas de carga quando ativo

### ViewportSign
Informações de localização de um sign na viewport:

**Propriedades:**
- **center**: Posição central do sign (coordenada horizontal)
- **top**: Topo do sign (coordenada vertical)
- **width_normal**: Largura com fonte normal (sem zoom)
- **width_small**: Largura com fonte pequena (zoom out)

**Métodos:**
- `UpdatePosition(center, top, str, str_small)`: Atualiza posição e texto
  - `str`: StringID para exibição normal
  - `str_small`: StringID para exibição pequena (opcional, default STR_NULL)
- `MarkDirty(maxzoom)`: Marca sign como sujo para redesenho
  - `maxzoom`: Nível máximo de zoom onde redraw é necessário (default ZOOM_LVL_MAX)

**Comportamento:**
- Signs mudam de tamanho baseado no zoom da viewport
- Sistema usa duas larguras pré-calculadas para performance
- Dirty tracking evita redraws desnecessários

### TrackedViewportSign
Versão especializada de ViewportSign para Kdtree:

**Propriedades Adicionais:**
- **kdtree_valid**: Se os dados do sign são válidos para uso na _viewport_sign_kdtree

**Métodos:**
- `UpdatePosition()`: Override que marca kdtree_valid como true
  - Chama método base ViewportSign::UpdatePosition()
  - Define flag para permitir uso na árvore espacial

**Construtor:**
- Inicializa kdtree_valid como false
- Sign só é válido para kdtree após UpdatePosition() ser chamado

**Uso:**
- Kdtree acelera busca de signs por posição
- Flag previne uso de dados desatualizados
- Essencial para performance com muitos signs

## Enums e Constantes

### ZoomStateChange
Estados de mudança de zoom:

- **ZOOM_IN (0)**: Zoom in (vista mais detalhada)
  - Aproxima a câmera
  - Mostra mais detalhes
  - Menor área visível
  
- **ZOOM_OUT (1)**: Zoom out (vista de helicóptero)
  - Afasta a câmera
  - Mostra menos detalhes
  - Maior área visível
  
- **ZOOM_NONE (2)**: Hack para atualização de status de botão
  - Não muda zoom
  - Usado apenas para refresh visual de botões

**Uso:**
- Passed para DoZoomInOutWindow()
- Controla direção da mudança de zoom
- ZOOM_NONE permite update sem mudança real

### BB_HEIGHT_UNDER_BRIDGE
Altura máxima sob pontes baixas:
- **Valor**: 6
- **Propósito**: Limite Z para construções sob pontes baixas
- **Faixa válida**: z=0..5 para tudo construído sob pontes baixas
- **z=6**: Reservado, atualmente não usado

### BB_Z_SEPARATOR
Separador Z entre ponte/túnel e objetos:
- **Valor**: 7
- **Propósito**: Separa bridge/tunnel dos objetos acima/abaixo
- **Uso**: Previne colisões e problemas de renderização

### ViewportPlaceMethod
Métodos de seleção de área (highlight e colocação):

**Direções Básicas:**
- **VPM_X_OR_Y (0)**: Arrastar em direção X ou Y
  - Seleciona linha horizontal ou vertical
  - Usuário escolhe direção durante drag
  
- **VPM_FIX_X (1)**: Arrastar apenas no eixo X
  - Seleção horizontal fixa
  - Y permanece constante
  
- **VPM_FIX_Y (2)**: Arrastar apenas no eixo Y
  - Seleção vertical fixa
  - X permanece constante
  
- **VPM_X_AND_Y (3)**: Área de terra em X e Y
  - Seleção retangular completa
  - Ambos eixos variam livremente
  
- **VPM_X_AND_Y_LIMITED (4)**: Área de terra com tamanho limitado
  - Similar a VPM_X_AND_Y mas com restrições de tamanho
  - Usado para construções com limites máximos

**Direções Horizontais/Verticais:**
- **VPM_FIX_HORIZONTAL (5)**: Arrastar apenas na direção horizontal
- **VPM_FIX_VERTICAL (6)**: Arrastar apenas na direção vertical

**Tamanhos Limitados:**
- **VPM_X_LIMITED (7)**: Apenas eixo X com tamanho limitado
- **VPM_Y_LIMITED (8)**: Apenas eixo Y com tamanho limitado

**Seleção Simples:**
- **VPM_SINGLE_TILE (9)**: Arrastar pela tela, selecionando apenas tile final
  - Highlight segue cursor
  - Apenas tile sob cursor é selecionado
  - Útil para colocação precisa

**Tipos Especiais (Bit Flags):**
- **VPM_RAILDIRS (0x40)**: Todas as direções de trilho
  - Flag adicional para seleção de direções de rail
  - Combinado com outros valores via OR
  
- **VPM_SIGNALDIRS (0x80)**: Similar a VPM_RAILDIRS mas com cursor diferente
  - Específico para colocação de sinais
  - Cursor especializado mostra direções possíveis

**DECLARE_ENUM_AS_BIT_SET:**
- Permite combinação de flags via operações bitwise
- Usado principalmente para VPM_RAILDIRS e VPM_SIGNALDIRS

### ViewportDragDropSelectionProcess
Processos de drag-and-drop para seleção de área:

#### Modificações de Terreno
- **DDSP_DEMOLISH_AREA**: Limpar área (demolir tudo)
- **DDSP_RAISE_AND_LEVEL_AREA**: Elevar e nivelar área
- **DDSP_LOWER_AND_LEVEL_AREA**: Baixar e nivelar área
- **DDSP_LEVEL_AREA**: Apenas nivelar área
- **DDSP_CREATE_DESERT**: Preencher área com deserto
- **DDSP_CREATE_ROCKS**: Preencher área com rochas
- **DDSP_CREATE_WATER**: Criar canal (água)
- **DDSP_CREATE_RIVER**: Criar rios
- **DDSP_PLANT_TREES**: Plantar árvores

#### Construção de Infraestrutura
- **DDSP_BUILD_BRIDGE**: Colocação de ponte
- **DDSP_BUILD_OBJECT**: Construir objeto genérico

#### Ações Específicas de Ferrovias
- **DDSP_PLACE_RAIL**: Colocação de trilhos
- **DDSP_BUILD_SIGNALS**: Colocação de sinais
- **DDSP_BUILD_STATION**: Colocação de estação
- **DDSP_REMOVE_STATION**: Remoção de estação
- **DDSP_CONVERT_RAIL**: Conversão de tipo de trilho

#### Ações Específicas de Rodovias
- **DDSP_PLACE_ROAD_X_DIR**: Colocação de estrada (direção X)
- **DDSP_PLACE_ROAD_Y_DIR**: Colocação de estrada (direção Y)
- **DDSP_PLACE_AUTOROAD**: Colocação automática de estrada
  - Sistema escolhe melhor direção automaticamente
- **DDSP_BUILD_BUSSTOP**: Colocação de parada de ônibus
- **DDSP_BUILD_TRUCKSTOP**: Colocação de parada de caminhões
- **DDSP_REMOVE_BUSSTOP**: Remoção de parada de ônibus
- **DDSP_REMOVE_TRUCKSTOP**: Remoção de parada de caminhões
- **DDSP_CONVERT_ROAD**: Conversão de tipo de estrada

#### Ações de Tile Único
- **DDSP_SINGLE_TILE**: Ações de tile único
  - Construir indústria
  - Fundar cidade
  - Outras ações pontuais

### ViewportScrollTarget
Alvo do método de scrolling da viewport:

- **VST_EVERYONE**: Todos os jogadores
  - Scroll afeta todas as viewports
  - Usado em modo single-player
  
- **VST_COMPANY**: Todos os jogadores de empresa específica
  - Scroll sincronizado dentro da company
  - Útil em multiplayer cooperativo
  
- **VST_CLIENT**: Único jogador
  - Scroll afeta apenas viewport local
  - Padrão para maioria das situações

## Fluxos de Uso

### Seleção de Área para Construção

1. **Início do Drag**: Usuário clica e segura mouse
   - ViewportPlaceMethod define direção permitida
   - Highlight inicial aparece
   
2. **Durante Drag**: Mouse se move
   - Highlight atualiza conforme método
   - Tile sob cursor é rastreado
   
3. **Fim do Drag**: Usuário solta mouse
   - ViewportDragDropSelectionProcess define ação
   - Área selecionada é processada
   - Ação é executada (construir, demolir, etc.)

### Zoom da Viewport

1. **Trigger**: Usuário clica botão zoom ou usa scroll
2. **Validação**: Verifica limites de zoom (min/max)
3. **Cálculo**: Nova posição virtual é calculada
4. **Aplicação**: Zoom level é atualizado
5. **Redraw**: Viewport é redesenhada com novo zoom
6. **Signs Update**: Widths são recalculados se necessário

### Atualização de Signs

1. **Mudança**: Texto ou posição do sign muda
2. **UpdatePosition**: Método é chamado com novos valores
3. **Kdtree Mark**: TrackedViewportSign marca como válido
4. **Dirty Mark**: Viewports afetadas são marcadas como sujas
5. **Redraw**: Na próxima iteração, signs são redesenhados

## Integração com Outros Sistemas

### Window System
- ViewportData contém instância de Viewport
- Janelas com viewports chamam UpdateViewportCoordinates()
- NWidgetViewport gerencia rendering em nested widgets

### Zoom System
- zoom_type.h define ZoomLevel enum
- Viewport usa zoom para calcular coordenadas virtuais
- Fator de zoom afeta rendering de tiles e signs

### Kdtree System
- _viewport_sign_kdtree armazena TrackedViewportSign
- Acelera busca de signs por região
- kdtree_valid flag previne uso de dados stale

### Link Graph
- Viewport.overlay aponta para LinkGraphOverlay
- Mostra rotas de carga quando ativado
- Overlay é desenhada sobre a viewport

### Input System
- ViewportPlaceMethod controla highlight durante drag
- ViewportDragDropSelectionProcess define ação ao soltar
- Sistema de tile highlight usa estas enums

## Otimizações

### Bounding Boxes
- BB_HEIGHT_UNDER_BRIDGE e BB_Z_SEPARATOR otimizam collision detection
- Separação clara entre bridge/tunnel e objetos
- Previne testes de colisão desnecessários

### Sign Width Caching
- width_normal e width_small pré-calculados
- Evita medição de texto durante rendering
- Update apenas quando texto muda

### Kdtree Tracking
- kdtree_valid flag evita rebuilds desnecessários
- Kdtree só é atualizado quando sign é válido
- Melhora performance com muitos signs

### Virtual Coordinates
- Coordenação virtual permite zoom suave
- Cálculos são feitos em espaço virtual
- Conversão para screen space apenas no rendering

## Casos de Uso Comuns

### Construção de Ferrovia
```cpp
// Selecionar área para estação
method = VPM_X_AND_Y_LIMITED;
process = DDSP_BUILD_STATION;
// Usuário arrasta área retangular limitada
// Estação é construída na área selecionada
```

### Terraplanagem
```cpp
// Nivelar área grande
method = VPM_X_AND_Y;
process = DDSP_LEVEL_AREA;
// Usuário arrasta área retangular
// Todo terreno na área é nivelado
```

### Colocação de Sinais
```cpp
// Selecionar direção de sinal
method = VPM_SIGNALDIRS | VPM_RAILDIRS;
process = DDSP_BUILD_SIGNALS;
// Cursor especial mostra direções possíveis
// Usuário seleciona direção do sinal
```

### Zoom Dinâmico
```cpp
// Zoom in para detalhes
state = ZOOM_IN;
DoZoomInOutWindow(state);
// Viewport aproxima, mostra mais detalhes
```

## Notas de Implementação

### Thread Safety
- Viewports são acessadas apenas no thread principal
- Kdtree updates devem ser sincronizados se multi-thread
- Dirty marking é thread-safe

### Memory Management
- Viewport.overlay é ponteiro cru (gerenciado externamente)
- TrackedViewportSign é copiado para kdtree
- Strings em signs são referenciadas por StringID

### Performance
- Virtual coordinates evitam multiplicações repetidas
- Sign width caching reduz custo de text measurement
- Kdtree acelera spatial queries exponencialmente

### Extensibilidade
- Novos ViewportPlaceMethod podem ser adicionados
- Novos DDSP_* processes para novas construções
- Sistema de overlay é genérico para diferentes visualizações
