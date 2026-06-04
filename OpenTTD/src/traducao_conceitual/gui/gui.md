# Sistema de Interface Gráfica (GUI)

## Visão Geral
Este arquivo define funções de interface gráfica que não se encaixam em outros módulos específicos, servindo como ponto de entrada para diversas funcionalidades de GUI do OpenTTD.

## Funções Principais

### Inicialização
- `InitializeGUI()`: Inicializa o sistema de interface gráfica do jogo

### Configurações do Jogo
- `ShowGameOptions()`: Exibe a janela de opções do jogo
- `ShowGameSettings()`: Exibe a janela de configurações do jogo

### Gestão de Veículos
- `ShowOrdersWindow(const Vehicle *v)`: Exibe a janela de ordens para um veículo específico (trens)

### Barramentas de Construção
- `ShowBuildDocksToolbar()`: Exibe a barra de ferramentas de construção de docas
- `ShowBuildDocksScenToolbar()`: Exibe a barra de ferramentas de docas para editor de cenários
- `ShowBuildAirToolbar()`: Exibe a barra de ferramentas de construção de aeroportos
- `ShowBuildTreesToolbar()`: Exibe a barra de ferramentas de plantio de árvores
- `ShowBuildBridgeWindow(...)`: Exibe a janela de construção de pontes

### Informação e Diretórios
- `ShowLandInfo(TileIndex tile)`: Exibe informações detalhadas sobre um tile específico
- `ShowTownDirectory()`: Exibe o diretório de cidades
- `ShowIndustryDirectory()`: Exibe o diretório de indústrias
- `ShowIndustryCargoesWindow()`: Exibe janela de cargas das indústrias
- `ShowAboutWindow()`: Exibe a janela "Sobre" do jogo

### Janelas Especiais
- `ShowGenerateLandscape()`: Exibe a janela de geração de terreno
- `ShowHeightmapLoad()`: Exibe a janela de carregamento de heightmap
- `ShowSubsidiesList()`: Exibe a lista de subsídios
- `ShowGoalsList(CompanyID company)`: Exibe a lista de objetivos da empresa
- `ShowGoalQuestion(...)`: Exibe questão relacionada a objetivos
- `ShowStoryBook(...)`: Exibe o livro de histórias da empresa
- `ShowMusicWindow()`: Exibe a janela de seleção musical
- `ShowBuildIndustryWindow()`: Exibe janela de construção de indústrias
- `ShowFoundTownWindow()`: Exibe janela de fundação de cidades

### Sistema Econômico
- `ShowEstimatedCostOrIncome(Money cost, int x, int y)`: Exibe estimativa de custo ou renda em posição específica na tela

### Viewports Extras
- `ShowExtraViewportWindow(TileIndex tile)`: Exibe janela com viewport extra para um tile
- `ShowExtraViewportWindowForTileUnderCursor()`: Exibe viewport extra para o tile sob o cursor

## Estrutura de Dependências

O arquivo importa tipos de diversos módulos:
- **VehicleType**: Tipos de veículos
- **EconomyType**: Tipos econômicos (dinheiro, custos)
- **TileType**: Tipos de tiles/posições no mapa
- **TransportType**: Tipos de transporte (rodoviário, ferroviário, etc.)
- **StoryType**: Tipos relacionados ao sistema de histórias
- **CompanyType**: Tipos relacionados às empresas/jogadores

## Fluxo de Utilização

1. **Inicialização**: `InitializeGUI()` é chamado durante o startup do jogo
2. **Acesso do Usuário**: Jogador acessa menus e ferramentas através da interface
3. **Exibição de Janelas**: Funções específicas exibem janelas contextuais conforme necessário
4. **Interação**: Usuário interage com as janelas para configurar, construir ou visualizar informações
5. **Feedback Visual**: Sistema econômico exibe custos/rendas de forma contextual

## Notas de Implementação

- As funções estão distribuídas em diferentes arquivos `.cpp` (main_gui.cpp, settings_gui.cpp, train_gui.cpp, etc.)
- Este arquivo serve como um header unificador para acesso rápido às principais funcionalidades de GUI
- A estrutura permite modularidade enquanto mantém uma interface coesa para o usuário final
