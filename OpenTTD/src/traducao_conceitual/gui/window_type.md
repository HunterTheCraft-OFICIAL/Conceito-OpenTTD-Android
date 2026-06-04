# Tipos de Janelas (Window Types)

## Visão Geral
Este arquivo define os tipos e enumerações relacionados a janelas no OpenTTD, incluindo números de janelas, classes de janelas e estados de eventos.

## Enumerações Principais

### WindowNumberEnum (Números de Janela)
Define números específicos para janelas comuns:

**Opções do Jogo:**
- `WN_GAME_OPTIONS_AI`: Configurações de IA
- `WN_GAME_OPTIONS_GS`: Configurações de GameScript
- `WN_GAME_OPTIONS_ABOUT`: Janela "Sobre"
- `WN_GAME_OPTIONS_NEWGRF_STATE`: Configurações NewGRF
- `WN_GAME_OPTIONS_GAME_OPTIONS`: Opções do jogo
- `WN_GAME_OPTIONS_GAME_SETTINGS`: Configurações do jogo

**Query String:**
- `WN_QUERY_STRING`: Query string padrão
- `WN_QUERY_STRING_SIGN`: Query string para sinais

**Popups de Confirmação:**
- `WN_CONFIRM_POPUP_QUERY`: Popup de confirmação padrão
- `WN_CONFIRM_POPUP_QUERY_BOOTSTRAP`: Confirmação para bootstrap

**Janelas de Rede:**
- `WN_NETWORK_WINDOW_GAME`: Janela de jogo em rede
- `WN_NETWORK_WINDOW_CONTENT_LIST`: Lista de conteúdo de rede
- `WN_NETWORK_WINDOW_START`: Iniciar servidor em rede
- `WN_NETWORK_STATUS_WINDOW_JOIN`: Status de entrada em rede
- `WN_NETWORK_STATUS_WINDOW_CONTENT_DOWNLOAD`: Status de download de conteúdo

### WindowClass (Classes de Janela)
Define todas as classes de janelas disponíveis no jogo:

**Janelas Principais:**
- `WC_NONE`: Nenhuma janela (redireciona para WC_MAIN_WINDOW)
- `WC_MAIN_WINDOW`: Janela principal do jogo
- `WC_MAIN_TOOLBAR`: Toolbar principal (barra superior)
- `WC_MAIN_TOOLBAR_RIGHT`: Parte direita da toolbar dividida
- `WC_STATUS_BAR`: Barra de status (inferior)

**Toolbars de Construção:**
- `WC_BUILD_CONFIRMATION`: Confirmação de construção
- `WC_BUILD_TOOLBAR`: Toolbar de construção (ferrovias, aeroportos, portos, estradas)
- `WC_SCEN_BUILD_TOOLBAR`: Toolbar de construção de cenário
- `WC_BUILD_TREES`: Toolbar de construção de árvores
- `WC_BUILD_SIGNAL`: Toolbar de construção de sinais
- `WC_TRANSPARENCY_TOOLBAR`: Toolbar de transparência

**Janelas de Informação:**
- `WC_SMALLMAP`: Mapa pequeno
- `WC_ERRMSG`: Mensagem de erro
- `WC_TOOLTIPS`: Tooltips
- `WC_LAND_INFO`: Informações do terreno
- `WC_DROPDOWN_MENU`: Menu dropdown
- `WC_OSK`: Teclado na tela (On Screen Keyboard)

**Janelas de Diálogo:**
- `WC_QUERY_STRING`: Janela de query string
- `WC_CONFIRM_POPUP_QUERY`: Popup de confirmação
- `WC_GOAL_QUESTION`: Popup de perguntas do GameScript
- `WC_SAVELOAD`: Janela de salvar/carregar
- `WC_SET_DATE`: Definir data
- `WC_TEXTFILE`: Visualizador de arquivos de texto

**Configurações:**
- `WC_AI_SETTINGS`: Configurações de IA
- `WC_GRF_PARAMETERS`: Parâmetros NewGRF
- `WC_COMPANY_COLOUR`: Seleção de cor da empresa
- `WC_COMPANY_MANAGER_FACE`: Alterar face do gerente
- `WC_CUSTOM_CURRENCY`: Moeda personalizada
- `WC_CHEATS`: Janela de cheats

**Janelas de Veículos:**
- `WC_VEHICLE_DETAILS`: Detalhes do veículo
- `WC_VEHICLE_REFIT`: Reequipamento de veículo
- `WC_VEHICLE_ORDERS`: Ordens do veículo
- `WC_REPLACE_VEHICLE`: Substituição de veículo
- `WC_VEHICLE_TIMETABLE`: Horário do veículo
- `WC_VEHICLE_VIEW`: Vista do veículo
- `WC_VEHICLE_DEPOT`: Vista do depósito
- `WC_BUILD_VEHICLE`: Construção de veículo

**Listas e Diretórios:**
- `WC_TOWN_DIRECTORY`: Diretório de cidades
- `WC_INDUSTRY_DIRECTORY`: Diretório de indústrias
- `WC_SUBSIDIES_LIST`: Lista de subsídios
- `WC_MESSAGE_HISTORY`: Histórico de mensagens
- `WC_SIGN_LIST`: Lista de sinais
- `WC_AI_LIST`: Lista de IAs
- `WC_GOALS_LIST`: Lista de objetivos
- `WC_STORY_BOOK`: Livro de história
- `WC_STATION_LIST`: Lista de estações
- `WC_TRAINS_LIST`: Lista de trens
- `WC_ROADVEH_LIST`: Lista de veículos rodoviários
- `WC_SHIPS_LIST`: Lista de navios
- `WC_AIRCRAFT_LIST`: Lista de aeronaves
- `WC_CLIENT_LIST`: Lista de clientes

**Vistas Específicas:**
- `WC_TOWN_VIEW`: Vista da cidade
- `WC_STATION_VIEW`: Vista da estação
- `WC_WAYPOINT_VIEW`: Vista do waypoint
- `WC_INDUSTRY_VIEW`: Vista da indústria
- `WC_COMPANY`: Vista da empresa
- `WC_TOWN_AUTHORITY`: Autoridade da cidade

**Construção Especializada:**
- `WC_BUILD_OBJECT`: Construir objeto
- `WC_BUILD_BRIDGE`: Construir ponte
- `WC_BUILD_STATION`: Construir estação
- `WC_BUS_STATION`: Construir estação de ônibus
- `WC_TRUCK_STATION`: Construir estação de caminhões
- `WC_BUILD_DEPOT`: Construir depósito
- `WC_BUILD_WAYPOINT`: Construir waypoint
- `WC_FOUND_TOWN`: Fundar cidade
- `WC_BUILD_INDUSTRY`: Construir indústria

**Geração de Paisagem:**
- `WC_SELECT_GAME`: Selecionar jogo
- `WC_SCEN_LAND_GEN`: Geração de paisagem (editor de cenário)
- `WC_GENERATE_LANDSCAPE`: Gerar paisagem (novo jogo)
- `WC_MODAL_PROGRESS`: Progresso de geração de paisagem

**Rede:**
- `WC_NETWORK_WINDOW`: Janela de rede
- `WC_NETWORK_STATUS_WINDOW`: Status de rede
- `WC_NETWORK_ASK_RELAY`: Perguntar sobre retransmissão
- `WC_SEND_NETWORK_MSG`: Caixa de chat
- `WC_COMPANY_PASSWORD_WINDOW`: Senha da empresa

**Gráficos e Finanças:**
- `WC_INDUSTRY_CARGOES`: Cadeia de cargas da indústria
- `WC_GRAPH_LEGEND`: Legenda de gráficos
- `WC_FINANCES`: Finanças da empresa
- `WC_INCOME_GRAPH`: Gráfico de renda
- `WC_OPERATING_PROFIT`: Gráfico de lucro operacional
- `WC_DELIVERED_CARGO`: Gráfico de carga entregue
- `WC_PERFORMANCE_HISTORY`: Histórico de performance
- `WC_COMPANY_VALUE`: Valor da empresa
- `WC_COMPANY_LEAGUE`: Liga de empresas
- `WC_PAYMENT_RATES`: Taxas de pagamento
- `WC_PERFORMANCE_DETAIL`: Detalhes de performance
- `WC_COMPANY_INFRASTRUCTURE`: Infraestrutura da empresa

**Negócios:**
- `WC_BUY_COMPANY`: Comprar empresa (fusão)
- `WC_ENGINE_PREVIEW`: Prévia de motor

**Música e Som:**
- `WC_MUSIC_WINDOW`: Janela de música
- `WC_MUSIC_TRACK_SELECTION`: Seleção de trilha musical

**Opções do Jogo:**
- `WC_GAME_OPTIONS`: Opções do jogo (IA, GS, NewGRF, etc.)

**Debug e Desenvolvimento:**
- `WC_CONSOLE`: Console
- `WC_AI_DEBUG`: Debug de IA
- `WC_NEWGRF_INSPECT`: Inspetor NewGRF
- `WC_SPRITE_ALIGNER`: Alinhador de sprites
- `WC_LINKGRAPH_LEGEND`: Legenda de linkgraph
- `WC_FRAMERATE_DISPLAY`: Display de framerate
- `WC_FRAMETIME_GRAPH`: Gráfico de tempo de frame

**Outras:**
- `WC_BOOTSTRAP`: Bootstrap
- `WC_HIGHSCORE`: Highscore
- `WC_ENDSCREEN`: Tela final
- `WC_SAVE_PRESET`: Salvar preset
- `WC_SCREENSHOT`: Janela de screenshot
- `WC_EXTRA_VIEWPORT`: Viewport extra
- `WC_SELECT_STATION`: Selecionar estação (ao unir estações)
- `WC_NEWS_WINDOW`: Janela de notícias
- `WC_GOAL_QUESTION`: Perguntas de objetivo

### GameOptionsInvalidationData
Dados de invalidação para janelas de opções do jogo:
- `GOID_DEFAULT`: Padrão
- `GOID_NEWGRF_RESCANNED`: NewGRFs foram rescaneados
- `GOID_NEWGRF_CURRENT_LOADED`: Lista atual de NewGRFs ativos carregada
- `GOID_NEWGRF_LIST_EDITED`: Lista de NewGRFs ativos está sendo editada
- `GOID_NEWGRF_CHANGES_MADE`: Mudanças feitas em um NewGRF (paleta ou parâmetros)
- `GOID_NEWGRF_CHANGES_APPLIED`: Mudanças na lista de NewGRFs aplicadas

### EventState
Estado de processamento de eventos:
- `ES_HANDLED`: Evento foi processado
- `ES_NOT_HANDLED`: Evento não foi processado

### WindowNumber
Tipo inteiro (int32) para diferenciar janelas da mesma classe.

## Uso Típico

```cpp
// Exemplo: Abrir janela de detalhes de veículo
WindowDesc *desc = &VehicleDetailsWindow::desc;
VehicleDetailsWindow *w = new VehicleDetailsWindow(desc, vehicle_id);

// Exemplo: Verificar classe de janela
if (window->window_class == WC_VEHICLE_ORDERS) {
    // Processar janela de ordens
}

// Exemplo: Invalidar dados de janela de opções
InvalidateWindowData(WC_GAME_OPTIONS, GOID_NEWGRF_RESCANNED);
```

## Notas Importantes

1. **WC_INVALID**: Valor 0xFFFF indica janela inválida
2. **WindowNumber**: Cada classe pode ter múltiplas instâncias diferenciadas pelo número
3. **Hierarquia**: Algumas janelas têm relação pai-filho definida
4. **Ini Key**: Janelas podem salvar configurações no openttd.cfg usando ini_key
