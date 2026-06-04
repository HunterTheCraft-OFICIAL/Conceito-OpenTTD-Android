# Sistema de Interface de Configurações (Settings GUI)

## Visão Geral
Este arquivo define funções utilitárias para desenho de elementos de interface relacionados a configurações no OpenTTD, incluindo botões de ajuste, dropdowns e componentes visuais específicos para edição de settings.

## Constantes de Dimensão

### SETTING_BUTTON_WIDTH
- **Valor**: `GetMinButtonSize() * 2`
- **Propósito**: Largura padrão para botões de configuração
- **Uso**: Garante consistência visual em todos os controles de setting
- **Baseado em**: Tamanho mínimo de botão para interface touch

### SETTING_BUTTON_HEIGHT
- **Valor**: `GetMinButtonSize()`
- **Propósito**: Altura padrão para botões de configuração
- **Uso**: Mantém proporção adequada com a largura
- **Baseado em**: Tamanho mínimo de botão para interface touch

## Funções de Desenho

### DrawArrowButtons
Desenha botões de seta para ajuste incremental de valores:

**Parâmetros:**
- `x, y`: Posição do topo esquerdo dos botões
- `button_colour`: Cor dos botões (tipo Colours)
- `state`: Estado visual dos botões (byte)
- `clickable_left`: Se botão da esquerda está clicável
- `clickable_right`: Se botão da direita está clicável

**Comportamento:**
- Desenha par de botões com setas esquerda/direita
- Aplica estado visual (pressionado, desabilitado, etc.)
- Respeita flags de clicabilidade para cada botão
- Usado para ajustes incrementais de valores numéricos

### DrawDropDownButton
Desenha botão de dropdown:

**Parâmetros:**
- `x, y`: Posição do topo esquerdo do botão
- `button_colour`: Cor do botão
- `state`: Estado visual (dropdown aberto/fechado)
- `clickable`: Se o botão está clicável

**Comportamento:**
- Desenha botão com indicador de dropdown (seta para baixo)
- Mostra estado aberto/fechado visualmente
- Aplica estado desabilitado se não-clicável
- Usado para seleção de opções em listas

### DrawBoolButton
Desenha botão booleano (liga/desliga):

**Parâmetros:**
- `x, y`: Posição do topo esquerdo do botão
- `state`: Estado booleano (true/false, on/off)
- `clickable`: Se o botão está clicável

**Comportamento:**
- Desenha botão toggle para valores booleanos
- Indica visualmente estado ON ou OFF
- Aplica aparência desabilitada se não-clicável
- Usado para settings do tipo checkbox/toggle

## Funções de Lista Dropdown

### BuildMusicSetDropDownList
Constrói lista dropdown para seleção de music sets:

**Parâmetros:**
- `selected_index`: Ponteiro para índice do item selecionado (output)

**Retorno:**
- DropDownList: Lista de itens para widget dropdown

**Comportamento:**
- Coleta todos os music sets disponíveis
- Constrói estrutura de dropdown compatível com sistema UI
- Define índice do item atualmente selecionado
- Usado na janela de configurações de música

### ChangeMusicSet
Muda o music set ativo:

**Parâmetros:**
- `index`: Índice do novo music set a ativar

**Implementação:**
- Declarada neste header mas implementada em `music_gui.cpp`
- Aplica mudança imediatamente
- Atualiza sistema de áudio com novo set
- Dispara invalidação de janelas relacionadas

## Padrões de Uso

### Botões de Ajuste Incremental
```cpp
// Para settings numéricos com incremento/decremento
DrawArrowButtons(x, y, colour, state, can_decrease, can_increase);
```

### Dropdowns de Seleção
```cpp
// Para settings com múltiplas opções
DropDownList list = BuildMusicSetDropDownList(&selected);
// ... associar lista ao widget dropdown
DrawDropDownButton(x, y, colour, is_open, is_clickable);
```

### Toggles Booleanos
```cpp
// Para settings sim/não, ligado/desligado
DrawBoolButton(x, y, is_enabled, is_clickable);
```

## Integração com Sistema de Settings

### Fluxo de Edição de Settings
1. **Leitura**: Valor atual do setting é lido
2. **Exibição**: Componente visual apropriado é desenhado
3. **Interação**: Usuário clica/toque para modificar
4. **Validação**: Mudança é validada (limits, dependências)
5. **Aplicação**: Novo valor é aplicado ao setting
6. **Feedback**: UI é atualizada para refletir mudança

### Tipos de Controls Suportados
- **Numérico incremental**: Setas esquerda/direita
- **Seleção múltipla**: Dropdown list
- **Booleano**: Toggle button
- **String**: Edit box (implementado em outro lugar)
- **Slider**: Não suportado diretamente por estas funções

## Considerações de Design

### Acessibilidade Touch
- `GetMinButtonSize()` garante tamanho mínimo para toque
- Botões de setting têm 2x de largura para facilitar interação
- Estados visuais claros (disabled, pressed, etc.)

### Consistência Visual
- Todas as funções usam mesmo sistema de cores (Colours)
- Estados são representados consistentemente entre controles
- Dimensões padronizadas mantêm UI coesa

### Internacionalização
- Funções não contêm texto hardcoded
- Labels e tooltips são tratados separadamente
- Suporte a RTL implícito no sistema de widgets

## Dependências

### Tipos Importados
- **gfx_type.h**: Define `Colours` e tipos gráficos básicos
- **dropdown_type.h**: Define estruturas de dropdown list

### Funções Relacionadas (Outros Arquivos)
- `GetMinButtonSize()`: widget_type.h - Obtém tamanho mínimo de botão
- Implementações de janelas de settings: settings_gui.cpp
- Sistema de settings: settings.h, settings_type.h

## Notas de Implementação

### Otimização de Desenho
- Funções de draw são chamadas durante OnPaint
- Devem ser eficientes para evitar lag visual
- Estado de clickable permite otimizar renderização

### Separação de Responsabilidades
- Este arquivo contém apenas funções de desenho
- Lógica de settings está em settings.cpp
- Gerenciamento de janelas está em settings_gui.cpp
- Música específica em music_gui.cpp

### Thread Safety
- Funções de desenho devem ser chamadas apenas no thread principal
- Settings podem ser acessados de múltiplos threads
- Sincronização é responsabilidade do caller

## Exemplos de Uso Prático

### Setting Numérico
```cpp
// Desenhar botões para ajustar número de veículos
bool can_decrease = value > min_limit;
bool can_increase = value < max_limit;
DrawArrowButtons(x, y, COLOUR_GREY, state, can_decrease, can_increase);
```

### Setting de Seleção
```cpp
// Desenhar dropdown para seleção de dificuldade
int selected = current_difficulty;
DropDownList list = BuildDifficultyDropDownList(&selected);
DrawDropDownButton(x, y, COLOUR_GREY, dropdown_open, true);
```

### Setting Booleano
```cpp
// Desenhar toggle para autosave
DrawBoolButton(x, y, _settings_client.gui.auto_save, true);
```

## Extensibilidade

### Adicionando Novos Controles
Para adicionar novo tipo de controle de setting:
1. Definir função de desenho seguindo padrão existente
2. Usar SETTING_BUTTON_WIDTH/HEIGHT para consistência
3. Implementar estados (disabled, pressed, etc.)
4. Integrar com sistema de settings existente

### Customização de Aparência
- Cores são passadas como parâmetro
- Estados permitem customização visual
- Dimensões baseadas em GetMinButtonSize() para escalabilidade
