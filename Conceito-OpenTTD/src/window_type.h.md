# 📄 window_type.h - Tipos Relacionados a Janelas

## Visão Geral
Arquivo de cabeçalho que define **todos os tipos e enums relacionados ao sistema de janelas** do OpenTTD. Este arquivo estabelece a taxonomia completa de classes de janelas, números de janela específicos e dados de invalidação usados em todo o sistema de interface gráfica.

---

## WindowNumberEnum - Números de Janela Pré-definidos

Enums para identificar instâncias específicas de janelas comuns.

### Configurações do Jogo (Game Options)

| Valor | ID | Descrição |
|-------|----|-----------|
| `WN_GAME_OPTIONS_AI` | 0 | Configurações de IA (AI settings) |
| `WN_GAME_OPTIONS_GS` | - | Configurações de Game Script (GS settings) |
| `WN_GAME_OPTIONS_ABOUT` | - | Janela "Sobre" (About window) |
| `WN_GAME_OPTIONS_NEWGRF_STATE` | - | Configurações NewGRF |
| `WN_GAME_OPTIONS_GAME_OPTIONS` | - | Opções do jogo |
| `WN_GAME_OPTIONS_GAME_SETTINGS` | - | Configurações detalhadas do jogo |

### Strings e Consultas

| Valor | ID | Descrição |
|-------|----|-----------|
| `WN_QUERY_STRING` | 0 | Query string genérica |
| `WN_QUERY_STRING_SIGN` | - | Query string para edição de sinais/placas |

### Popups de Confirmação

| Valor | ID | Descrição |
|-------|----|-----------|
| `WN_CONFIRM_POPUP_QUERY` | 0 | Popup de confirmação de consulta |
| `WN_CONFIRM_POPUP_QUERY_BOOTSTRAP` | - | Popup de confirmação para bootstrap |

### Rede/Network

| Valor | ID | Descrição |
|-------|----|-----------|
| `WN_NETWORK_WINDOW_GAME` | 0 | Janela de jogo em rede |
| `WN_NETWORK_WINDOW_CONTENT_LIST` | - | Lista de conteúdo de rede |
| `WN_NETWORK_WINDOW_START` | - | Servidor inicial de rede |
| `WN_NETWORK_STATUS_WINDOW_JOIN` | 0 | Status de entrada em jogo |
| `WN_NETWORK_STATUS_WINDOW_CONTENT_DOWNLOAD` | - | Status de download de conteúdo |

---

## WindowClass - Classes de Janela

Enum principal que define **todas as classes de janelas** do OpenTTD. Cada classe representa um tipo funcional de janela no jogo.

### Janelas Principais do Sistema

| Classe | Descrição | Window Numbers | Widgets Associados |
|--------|-----------|----------------|-------------------|
| `WC_NONE` | Nenhuma janela (redireciona para WC_MAIN_WINDOW) | - | - |
| `WC_MAIN_WINDOW` | Janela principal do jogo | 0 | MainWidgets |
| `WC_MAIN_TOOLBAR` | Barra de ferramentas principal | 0 (Normal/Editor) | ToolbarNormal/EditorWidgets |
| `WC_MAIN_TOOLBAR_RIGHT` | Parte direita da toolbar splitada | 0 | ToolbarNormal/EditorWidgets |
| `WC_STATUS_BAR` | Barra de status (inferior) | 0 | StatusbarWidgets |

### Diálogos de Confirmação e Consulta

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_BUILD_CONFIRMATION` | Confirmação de construção | 0 | BuildConfirmationWidgets |
| `WC_QUERY_STRING` | Entrada de texto | WN_QUERY_STRING*, WN_QUERY_STRING_SIGN | QueryString/EditSignWidgets |
| `WC_CONFIRM_POPUP_QUERY` | Popup de confirmação | WN_CONFIRM_POPUP* | Query/BootstrapWidgets |
| `WC_GOAL_QUESTION` | Pergunta de objetivo (GameScript) | uniqueid | GoalQuestionWidgets |

### Barras de Ferramentas de Construção

| Classe | Descrição | Window Numbers | Transport Types |
|--------|-----------|----------------|-----------------|
| `WC_BUILD_TOOLBAR` | Toolbar de construção normal | TRANSPORT_* | Rail/Air/Water/Road |
| `WC_SCEN_BUILD_TOOLBAR` | Toolbar de construção (cenário) | TRANSPORT_WATER/ROAD | Dock/Road |
| `WC_BUILD_TREES` | Toolbar de árvores | 0 | BuildTreesWidgets |
| `WC_BUILD_SIGNAL` | Toolbar de sinais ferroviários | TRANSPORT_RAIL | BuildSignalWidgets |
| `WC_TRANSPARENCY_TOOLBAR` | Toolbar de transparência | 0 | TransparencyToolbarWidgets |

### Janelas de Informação e Utilitários

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_SMALLMAP` | Minimapa | 0 | SmallMapWidgets |
| `WC_ERRMSG` | Mensagem de erro | 0 | ErrorMessageWidgets |
| `WC_TOOLTIPS` | Tooltips | 0 | ToolTipsWidgets |
| `WC_LAND_INFO` | Informações do terreno | 0 | LandInfoWidgets |
| `WC_OSK` | Teclado na tela (On-Screen Keyboard) | 0 | OnScreenKeyboardWidgets |

### Menus e Interfaces Especiais

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_DROPDOWN_MENU` | Menu dropdown | 0 | DropdownMenuWidgets |
| `WC_SAVELOAD` | Salvar/Carregar jogo | 0 | SaveLoadWidgets |
| `WC_SET_DATE` | Definir data (editor) | VehicleID | SetDateWidgets |
| `WC_TEXTFILE` | Visualizador de arquivos de texto | 0 | TextfileWidgets |

### Configurações e Preferências

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_AI_SETTINGS` | Configurações de IA | 0 | AISettingsWidgets |
| `WC_GRF_PARAMETERS` | Parâmetros NewGRF | 0 | NewGRFParametersWidgets |
| `WC_CUSTOM_CURRENCY` | Moeda customizada | 0 | CustomCurrencyWidgets |
| `WC_GAME_OPTIONS` | Opções do jogo | WN_GAME_OPTIONS_* | Vários widgets |

### Janelas de Empresas e Finanças

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_TOWN_AUTHORITY` | Autoridade municipal | TownID | TownAuthorityWidgets |
| `WC_FINANCES` | Finanças da empresa | CompanyID | CompanyWidgets |
| `WC_COMPANY_LEAGUE` | Liga/classificação de empresas | 0 | CompanyLeagueWidgets |
| `WC_COMPANY_INFRASTRUCTURE` | Infraestrutura da empresa | CompanyID | CompanyInfrastructureWidgets |
| `WC_BUY_COMPANY` | Comprar empresa (fusão) | CompanyID | BuyCompanyWidgets |
| `WC_COMPANY_PASSWORD_WINDOW` | Senha da empresa (rede) | 0 | NetworkCompanyPasswordWidgets |

### Gráficos e Estatísticas

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_INCOME_GRAPH` | Gráfico de receitas | 0 | CompanyValueWidgets |
| `WC_OPERATING_PROFIT` | Gráfico de lucro operacional | 0 | CompanyValueWidgets |
| `WC_DELIVERED_CARGO` | Gráfico de cargas entregues | 0 | CompanyValueWidgets |
| `WC_PERFORMANCE_HISTORY` | Histórico de performance | 0 | PerformanceHistoryGraphWidgets |
| `WC_COMPANY_VALUE` | Valor da empresa | 0 | CompanyValueWidgets |
| `WC_PAYMENT_RATES` | Taxas de pagamento por carga | 0 | CargoPaymentRatesWidgets |
| `WC_PERFORMANCE_DETAIL` | Detalhes de performance | 0 | PerformanceRatingDetailsWidgets |
| `WC_GRAPH_LEGEND` | Legenda de gráficos | 0 | GraphLegendWidgets |
| `WC_FRAMETIME_GRAPH` | Gráfico de tempo de frame | 0 | FrametimeGraphWindowWidgets |

### Veículos e Frota

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_VEHICLE_VIEWER` | Visualizador de veículo | VehicleID | VehicleViewWidgets |
| `WC_VEHICLE_DETAILS` | Detalhes do veículo | VehicleID | VehicleDetailsWidgets |
| `WC_VEHICLE_ORDERS` | Ordens do veículo | VehicleID | VehicleOrdersWidgets |
| `WC_VEHICLE_REFIT` | Reequipamento do veículo | VehicleID | VehicleRefitWidgets |
| `WC_REPLACE_VEHICLE` | Substituição de veículos | VehicleID | ReplaceVehicleWidgets |
| `WC_ENGINE_PREVIEW` | Preview de motor/engine | EngineID | EnginePreviewWidgets |

### Indústrias e Cargas

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_INDUSTRY_VIEW` | Vista de indústria | IndustryID | IndustryViewWidgets |
| `WC_INDUSTRY_CARGOES` | Cadeia de cargas de indústrias | 0 | IndustryCargoesWidgets |
| `WC_BUILD_INDUSTRY` | Construir indústria | 0 | DynamicPlaceIndustriesWidgets |

### Redes e Linkgraphs

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_LINKGRAPH_LEGEND` | Legenda de linkgraph | 0 | LinkGraphWidgets |

### Janelas de Rede/Network

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_NETWORK_WINDOW` | Janelas de rede | WN_NETWORK_WINDOW_* | Network*Widgets |
| `WC_CLIENT_LIST` | Lista de clientes | 0 | ClientListWidgets |
| `WC_NETWORK_STATUS_WINDOW` | Status de rede | WN_NETWORK_STATUS_* | NetworkStatusWidgets |
| `WC_NETWORK_ASK_RELAY` | Pedido de relay | 0 | NetworkAskRelayWidgets |
| `WC_SEND_NETWORK_MSG` | Caixa de chat/mensagem | DestType | NetWorkChatWidgets |

### Entretenimento e Mídia

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_MUSIC_WINDOW` | Janela de música | 0 | MusicWidgets |
| `WC_MUSIC_TRACK_SELECTION` | Seleção de trilhas | 0 | MusicTrackSelectionWidgets |

### Editor de Cenários e Geração

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_SELECT_GAME` | Seleção de jogo | 0 | SelectGameIntroWidgets |
| `WC_SCEN_LAND_GEN` | Geração de terreno (editor) | 0 | Terraform*ToolbarWidgets |
| `WC_GENERATE_LANDSCAPE` | Gerar paisagem (newgame) | GLWM_SCENARIO, GenerateLandscapeWindowMode | CreateScenario/GenerateLandscapeWidgets |
| `WC_MODAL_PROGRESS` | Progresso de geração | 0, 1 | GenerationProgress/ScanProgressWidgets |

### Debug e Desenvolvimento

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_CONSOLE` | Console de comandos | 0 | ConsoleWidgets |
| `WC_AI_DEBUG` | Debug de IA | 0 | AIDebugWidgets |
| `WC_NEWGRF_INSPECT` | Inspetor NewGRF (debug) | Packed value | NewGRFInspectWidgets |
| `WC_SPRITE_ALIGNER` | Alinhador de sprites (debug) | 0 | SpriteAlignerWidgets |
| `WC_CHEATS` | Janela de cheats | 0 | CheatWidgets |
| `WC_EXTRA_VIEWPORT` | Viewport extra | Ascending value | ExtraViewportWidgets |

### Janelas de Fim de Jogo e Progresso

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_HIGHSCORE` | Tabela de recordes | 0 | HighscoreWidgets |
| `WC_ENDSCREEN` | Tela final do jogo | 0 | HighscoreWidgets |

### Utilitários Diversos

| Classe | Descrição | Window Numbers | Widgets |
|--------|-----------|----------------|---------|
| `WC_BOOTSTRAP` | Bootstrap (inicialização) | 0 | BootstrapBackgroundWidgets |
| `WC_SAVE_PRESET` | Salvar preset | 0 | SavePresetWidgets |
| `WC_FRAMERATE_DISPLAY` | Display de framerate | 0 | FramerateDisplayWidgets |
| `WC_SCREENSHOT` | Janela de screenshot | 0 | ScreenshotWidgets |

### Valor Especial

```cpp
WC_INVALID = 0xFFFF  ///< Janela inválida
```

---

## GameOptionsInvalidationData - Dados de Invalidação

Enum usado para `Window::OnInvalidateData()` em janelas da classe `WC_GAME_OPTIONS`.

| Valor | Descrição |
|-------|-----------|
| `GOID_DEFAULT` | 0 - Invalidação padrão |
| `GOID_NEWGRF_RESCANNED` | NewGRFs foram reescaneados |
| `GOID_NEWGRF_CURRENT_LOADED` | Lista atual de NewGRFs ativos foi carregada |
| `GOID_NEWGRF_LIST_EDITED` | Lista de NewGRFs ativos está sendo editada |
| `GOID_NEWGRF_CHANGES_MADE` | Mudanças feitas em um NewGRF (palette ou parâmetros) |
| `GOID_NEWGRF_CHANGES_APPLIED` | Mudanças na lista de NewGRFs ativos foram aplicadas |

---

## Type Definitions

### WindowNumber
```cpp
typedef int32 WindowNumber;
```
Tipo para diferenciar diferentes janelas da mesma classe. Permite múltiplas instâncias de uma mesma classe de janela (ex: múltiplas janelas de veículo abertas simultaneamente).

### Forward Declaration
```cpp
struct Window;
```
Declaração antecipada da struct Window para evitar inclusões circulares.

---

## EventState - Estado de Processamento de Eventos

Enum retornado por handlers de eventos para indicar se o evento foi processado.

| Valor | Descrição |
|-------|-----------|
| `ES_HANDLED` | O evento foi manipulado/processado |
| `ES_NOT_HANDLED` | O evento não foi manipulado (pode ser passado adiante) |

---

## Padrões de Nomenclatura

### Em Português (Conceitual)

| Inglês | Português |
|--------|-----------|
| Window | Janela |
| Toolbar | Barra de Ferramentas |
| Status Bar | Barra de Status |
| Tooltip | Dica / Tooltip |
| Dropdown | Lista Suspensa |
| Query String | Entrada de Texto / Consulta |
| Confirmation | Confirmação |
| Save/Load | Salvar/Carregar |
| Settings | Configurações |
| Options | Opções |
| Finances | Finanças |
| Infrastructure | Infraestrutura |
| Performance | Performance / Desempenho |
| Graph | Gráfico |
| Legend | Legenda |
| Debug | Depuração |
| Console | Console |
| Cheat | Trapaça / Cheat |
| Viewport | Área de Visualização / Viewport |
| Sprite | Sprite / Imagem |
| Network | Rede |
| Client | Cliente |
| Server | Servidor |
| Content | Conteúdo |
| Industry | Indústria |
| Cargo | Carga |
| Vehicle | Veículo |
| Orders | Ordens / Pedidos |
| Refit | Reequipamento |
| Company | Empresa |
| Town | Cidade |
| Authority | Autoridade |

---

## Hierarquia Organizacional das Janelas

### 1. Janelas do Sistema Core
- WC_MAIN_WINDOW
- WC_MAIN_TOOLBAR, WC_MAIN_TOOLBAR_RIGHT
- WC_STATUS_BAR

### 2. Janelas de Interface Básica
- WC_DROPDOWN_MENU, WC_TOOLTIPS, WC_OSK
- WC_QUERY_STRING, WC_CONFIRM_POPUP_QUERY

### 3. Janelas de Construção
- WC_BUILD_TOOLBAR, WC_SCEN_BUILD_TOOLBAR
- WC_BUILD_CONFIRMATION, WC_BUILD_SIGNAL
- WC_BUILD_TREES, WC_BUILD_INDUSTRY

### 4. Janelas de Informação
- WC_SMALLMAP, WC_LAND_INFO, WC_ERRMSG
- WC_EXTRA_VIEWPORT

### 5. Janelas de Gestão de Empresas
- WC_FINANCES, WC_COMPANY_LEAGUE
- WC_COMPANY_INFRASTRUCTURE, WC_BUY_COMPANY

### 6. Janelas de Veículos
- WC_VEHICLE_VIEWER, WC_VEHICLE_DETAILS
- WC_VEHICLE_ORDERS, WC_VEHICLE_REFIT
- WC_REPLACE_VEHICLE, WC_ENGINE_PREVIEW

### 7. Janelas de Gráficos e Estatísticas
- WC_INCOME_GRAPH, WC_OPERATING_PROFIT
- WC_DELIVERED_CARGO, WC_PERFORMANCE_HISTORY
- WC_COMPANY_VALUE, WC_PAYMENT_RATES
- WC_PERFORMANCE_DETAIL, WC_GRAPH_LEGEND

### 8. Janelas de Configuração
- WC_GAME_OPTIONS, WC_AI_SETTINGS
- WC_GRF_PARAMETERS, WC_CUSTOM_CURRENCY

### 9. Janelas de Rede
- WC_NETWORK_WINDOW, WC_CLIENT_LIST
- WC_NETWORK_STATUS_WINDOW, WC_SEND_NETWORK_MSG

### 10. Janelas de Editor/Cenário
- WC_SELECT_GAME, WC_SCEN_LAND_GEN
- WC_GENERATE_LANDSCAPE, WC_SET_DATE

### 11. Janelas de Debug
- WC_CONSOLE, WC_AI_DEBUG
- WC_NEWGRF_INSPECT, WC_SPRITE_ALIGNER
- WC_CHEATS, WC_FRAMERATE_DISPLAY

### 12. Janelas de Mídia e Entretenimento
- WC_MUSIC_WINDOW, WC_MUSIC_TRACK_SELECTION
- WC_TEXTFILE, WC_SCREENSHOT

### 13. Janelas de Fim de Jogo
- WC_HIGHSCORE, WC_ENDSCREEN

---

## Fluxos de Uso Típicos

### Abrir Nova Janela
```cpp
// Criar janela única (singleton por class+number)
Window *w = AllocateWindowDescFront(&window_desc, window_number);

// Ou permitir múltiplas instâncias
Window *w = new Window(window_desc, window_number);
```

### Invalidar Dados da Janela
```cpp
// Para forçar atualização de dados exibidos
window->InvalidateData(GOID_NEWGRF_CHANGES_MADE);

// A janela receberá chamada em OnInvalidateData(data)
```

### Verificar se Janela Existe
```cpp
Window *w = FindWindowById(WC_FINANCES, company_id);
if (w != nullptr) {
    // Janela já está aberta
}
```

### Fechar Janela
```cpp
DeleteWindowById(WC_VEHICLE_VIEWER, vehicle_id);
// ou
DeleteWindowByClass(WC_BUILD_TOOLBAR);
```

---

## Considerações de Design

### Sistema de Classes e Números
- **Classe (WindowClass)**: Define o TIPO funcional da janela
- **Número (WindowNumber)**: Diferencia INSTÂNCIAS da mesma classe
- Exemplo: WC_VEHICLE_VIEWER + VehicleID = janela específica para cada veículo

### Janelas Singleton vs Múltiplas
- **Singleton**: Apenas uma instância por classe (ex: WC_SMALLMAP)
- **Múltiplas**: Várias instâncias permitidas (ex: WC_VEHICLE_VIEWER para cada veículo)

### Invalidação de Dados
- Sistema eficiente de atualização seletiva
- Evita redesenho completo quando apenas dados mudam
- GameOptionsInvalidationData fornece contexto específico

### Separação por Domínio Funcional
- Janelas agrupadas por propósito (construção, informação, configuração, etc.)
- Facilita navegação no código e manutenção
- Permite otimizações específicas por categoria

### Suporte a Debug
- Categoria dedicada para ferramentas de desenvolvimento
- Separadas do build release (podem ser compiladas condicionalmente)
- Essenciais para modders e desenvolvedores de NewGRF

---

## Relacionamentos

### Dependências Internas
- `widget_type.h` → Definições de widgets usados nas janelas
- `window_gui.h` → Declarações de funções GUI de janelas
- `window_func.h` → Funções utilitárias para manipulação de janelas

### Integração com Sistema de Widgets
- Cada janela tem array de widgets definido por WindowDesc
- Classes de janela determinam quais widgets são válidos
- Números de janela podem afetar configuração de widgets

### Conexão com Sistema de Eventos
- EventState retorna se evento foi processado
- Janelas recebem eventos de mouse, teclado, timer, etc.
- Invalidação triggera redesenho/atualização

---

## Casos de Uso Avançados

### Janela com Múltiplos Números
```cpp
// WC_FINANCES usa CompanyID como número
// Permite abrir finanças de várias empresas simultaneamente
ShowCompanyFinances(COMPANY_FIRST);   // number = 0
ShowCompanyFinances(COMPANY_SECOND);  // number = 1
```

### Invalidação Condicional
```cpp
void OnInvalidateData(int data) override {
    switch ((GameOptionsInvalidationData)data) {
        case GOID_NEWGRF_RESCANNED:
            // Atualizar lista de NewGRFs disponíveis
            break;
        case GOID_NEWGRF_CHANGES_MADE:
            // Atualizar parâmetros do NewGRF selecionado
            break;
        default:
            // Atualização completa
            break;
    }
}
```

### Janela de Debug Condicional
```cpp
#ifdef WITH_DEBUG
    if (_debug_newgrf_level >= 5) {
        ShowNewGRFInspectWindow(type, id);
    }
#endif
```

---

## Notas de Implementação

⚠️ **Atenção**: Este é um arquivo conceitual traduzido para documentação em português. A implementação real mantém os nomes originais em inglês no código fonte.

📝 **Observação**: A enum WindowClass é extensa (~100 classes) e reflete a complexidade da interface do OpenTTD. Novas classes devem ser adicionadas ao final, antes de WC_INVALID.

🔧 **Manutenção**: Ao adicionar nova classe de janela:
1. Adicionar enum antes de WC_INVALID
2. Documentar WindowNumbers aceitos
3. Especificar widgets associados
4. Atualizar esta documentação

🎨 **Consistência**: Seguir padrões de nomenclatura existentes:
- WC_ para classes (uppercase)
- WN_ para números pré-definidos (uppercase)
- Descritivo e específico para o propósito da janela

---

**Status**: ✅ Traduzido Conceitualmente  
**Nível**: 02 - Sistemas Centrais de Interface  
**Categoria**: GUI / Sistema de Janelas  
**Última Atualização**: Dezembro 2024
