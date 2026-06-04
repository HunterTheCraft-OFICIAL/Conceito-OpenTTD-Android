# 📄 gui.h - Funções Gerais de Interface Gráfica

## Visão Geral
Arquivo de cabeçalho que declara **funções globais de interface gráfica** do OpenTTD, servindo como ponto de entrada para abertura de diversas janelas e inicialização do sistema GUI. Este arquivo atua como um "guarda-chuva" que agrega funções de múltiplos subsistemas de interface.

---

## Funções de Inicialização

### InitializeGUI()
Inicializa todo o sistema de interface gráfica do jogo.
- **Origem**: `main_gui.cpp`
- **Chamada**: Executada uma vez na inicialização do jogo
- **Responsabilidade**: Configurar sistemas base da GUI

---

## Funções de Configuração do Jogo

### ShowGameOptions()
Exibe a janela de **opções do jogo**.
- **Origem**: `settings_gui.cpp`
- **Uso**: Menu principal → Opções

### ShowGameSettings()
Exibe a janela de **configurações detalhadas do jogo**.
- **Origem**: `settings_gui.cpp`
- **Uso**: Acesso a parâmetros avançados de gameplay

---

## Funções de Veículos

### ShowOrdersWindow(v)
Exibe a janela de **ordens/pedidos** de um veículo.
- **Origem**: `train_gui.cpp`
- **Parâmetro**: `v` → Ponteiro para o Vehicle (veículo)
- **Uso**: Clicar em veículo → Botão "Ordens"
- **Aplicação**: Principalmente trens, mas usado para todos os veículos

---

## Funções de Construção - Transporte Aquaviário

### ShowBuildDocksToolbar()
Exibe a barra de ferramentas de **construção de docas/estações portuárias**.
- **Origem**: `dock_gui.cpp`
- **Retorno**: Ponteiro para Window criada
- **Uso**: Modo de construção → Docas

### ShowBuildDocksScenToolbar()
Exibe barra de ferramentas de docas para **modo cenário/editor**.
- **Origem**: `dock_gui.cpp`
- **Diferença**: Versão específica para edição de cenários

---

## Funções de Construção - Transporte Aéreo

### ShowBuildAirToolbar()
Exibe a barra de ferramentas de **construção de aeroportos**.
- **Origem**: `airport_gui.cpp`
- **Retorno**: Ponteiro para Window criada
- **Uso**: Modo de construção → Aeroportos

---

## Funções de Geração de Terreno

### ShowGenerateLandscape()
Exibe janela de **geração de paisagem/terreno**.
- **Origem**: `tgp_gui.cpp`
- **Uso**: Criar novo mapa → Gerar terreno proceduralmente
- **Algoritmo**: TGP (Terrain Generation Program)

### ShowHeightmapLoad()
Exibe janela para **carregar heightmap** (mapa de alturas).
- **Origem**: `tgp_gui.cpp`
- **Uso**: Importar terreno baseado em imagem de altura

---

## Funções de Informação e Consultas

### ShowLandInfo(tile)
Exibe informações detalhadas sobre um **tile/azulejo** específico.
- **Origem**: `misc_gui.cpp`
- **Parâmetro**: `tile` → Índice do tile (TileIndex)
- **Uso**: Ferramenta de informação → Clicar no terreno
- **Informações**: Tipo de terreno, propriedades, objetos, etc.

### ShowAboutWindow()
Exibe janela **"Sobre"** do OpenTTD.
- **Origem**: `misc_gui.cpp`
- **Conteúdo**: Créditos, versão, licenças

---

## Funções de Diretórios/Listagens

### ShowTownDirectory()
Exibe o **diretório/lista de cidades**.
- **Origem**: `misc_gui.cpp`
- **Uso**: Ver todas as cidades do mapa com estatísticas

### ShowIndustryDirectory()
Exibe o **diretório/lista de indústrias**.
- **Origem**: `misc_gui.cpp`
- **Uso**: Ver todas as indústrias do mapa

### ShowIndustryCargoesWindow()
Exibe janela de **cargas de indústrias**.
- **Origem**: `misc_gui.cpp`
- **Uso**: Visualizar cadeia produtiva e cargas processadas

### ShowSubsidiesList()
Exibe lista de **subsídios** disponíveis.
- **Origem**: `misc_gui.cpp`
- **Uso**: Ver rotas subsidiadas pelo governo

### ShowGoalsList(company)
Exibe lista de **objetivos/metas** da empresa.
- **Origem**: `misc_gui.cpp`
- **Parâmetro**: `company` → ID da Company (empresa)
- **Uso**: Acompanhamento de progresso e conquistas

---

## Funções de Narrativa e Storytelling

### ShowGoalQuestion(id, type, button_mask, question)
Exibe janela de **pergunta de objetivo** com botões customizados.
- **Origem**: `misc_gui.cpp`
- **Parâmetros**:
  - `id` → Identificador único da pergunta
  - `type` → Tipo de pergunta (informação, escolha, etc.)
  - `button_mask` → Máscara definindo quais botões mostrar
  - `question` → Texto da pergunta
- **Uso**: Eventos scriptados, escolhas do jogador

### ShowStoryBook(company, page_id)
Exibe o **livro de história/narrativa** da empresa.
- **Origem**: `misc_gui.cpp`
- **Parâmetros**:
  - `company` → ID da Company (empresa)
  - `page_id` → Página específica (opcional, padrão: INVÁLIDO)
- **Uso**: Narrativa de cenários, tutoriais, storyline

---

## Funções de Informação Econômica

### ShowEstimatedCostOrIncome(cost, x, y)
Exibe estimativa visual de **custo ou receita**.
- **Origem**: `misc_gui.cpp`
- **Parâmetros**:
  - `cost` → Valor em Money (pode ser negativo para custo)
  - `x`, `y` → Posição na tela para exibição
- **Uso**: Feedback visual ao construir/comprar
- **Visual**: Tooltip flutuante mostrando valor

---

## Funções de Viewport Extra

### ShowExtraViewportWindow(tile)
Cria janela com **viewport adicional** focada em um tile.
- **Origem**: `misc_gui.cpp`
- **Parâmetro**: `tile` → Tile alvo (opcional, padrão: INVALID_TILE)
- **Uso**: Monitorar área específica enquanto trabalha em outra

### ShowExtraViewportWindowForTileUnderCursor()
Cria viewport extra focada no **tile sob o cursor**.
- **Origem**: `misc_gui.cpp`
- **Uso**: Atalho rápido para criar viewport na posição atual

---

## Funções de Construção - Pontes

### ShowBuildBridgeWindow(start, end, transport_type, bridge_type)
Exibe janela de **construção de pontes**.
- **Origem**: `bridge_gui.cpp`
- **Parâmetros**:
  - `start` → Tile inicial da ponte
  - `end` → Tile final da ponte
  - `transport_type` → Tipo de transporte (trem, estrada, etc.)
  - `bridge_type` → Tipo/materia l da ponte
- **Uso**: Selecionar tipo de ponte antes de construir

---

## Funções Diversas de Construção

### ShowBuildIndustryWindow()
Exibe janela para **construir indústria** manualmente.
- **Origem**: Não especificado (provavelmente `industry_gui.cpp`)
- **Uso**: Modo cenário/editor de mapas

### ShowFoundTownWindow()
Exibe janela para **fundar nova cidade**.
- **Origem**: Não especificado (provavelmente `town_gui.cpp`)
- **Uso**: Modo cenário/editor de mapas

### ShowMusicWindow()
Exibe janela de **controle de música**.
- **Origem**: Não especificado (provavelmente `music_gui.cpp`)
- **Uso**: Selecionar trilha sonora, ajustar volume

---

## Estrutura de Dependências

### Tipos Incluídos
- `vehicle_type.h` → Tipos de veículos
- `economy_type.h` → Tipos econômicos (Money, etc.)
- `tile_type.h` → Tipos de tiles/azulejos
- `transport_type.h` → Tipos de transporte
- `story_type.h` → Tipos de narrativa/storyline
- `company_type.h` → Tipos de empresas

### Forward Declarations
- `struct Window` → Declaração antecipada para evitar inclusão circular

---

## Organização por Módulos

| Módulo | Funções | Arquivo Origem |
|--------|---------|----------------|
| **Inicialização** | `InitializeGUI` | `main_gui.cpp` |
| **Configurações** | `ShowGameOptions`, `ShowGameSettings` | `settings_gui.cpp` |
| **Veículos** | `ShowOrdersWindow` | `train_gui.cpp` |
| **Docas** | `ShowBuildDocksToolbar*` | `dock_gui.cpp` |
| **Aeroportos** | `ShowBuildAirToolbar` | `airport_gui.cpp` |
| **Terreno** | `ShowGenerateLandscape`, `ShowHeightmapLoad` | `tgp_gui.cpp` |
| **Informações** | `ShowLandInfo`, `ShowAboutWindow` | `misc_gui.cpp` |
| **Diretórios** | `Show*T Directory` | `misc_gui.cpp` |
| **Narrativa** | `ShowGoalQuestion`, `ShowStoryBook` | `misc_gui.cpp` |
| **Economia** | `ShowEstimatedCostOrIncome` | `misc_gui.cpp` |
| **Viewports** | `ShowExtraViewportWindow*` | `misc_gui.cpp` |
| **Pontes** | `ShowBuildBridgeWindow` | `bridge_gui.cpp` |
| **Editor** | `ShowBuildIndustry`, `ShowFoundTown` | Vários |
| **Música** | `ShowMusicWindow` | `music_gui.cpp` |

---

## Padrões de Nomenclatura

### Em Português (Conceitual)
- GUI → Interface Gráfica / Interface
- Window → Janela
- Toolbar → Barra de Ferramentas
- Viewport → Área de Visualização / Viewport
- Tile → Azulejo / Tile
- Company → Empresa
- Industry → Indústria
- Town → Cidade
- Vehicle → Veículo
- Orders → Ordens / Pedidos
- Landscape → Paisagem / Terreno
- Heightmap → Mapa de Alturas

---

## Fluxos de Uso Típicos

### Inicialização do Jogo
```
1. InitializeGUI()
2. Carregar configurações salvas
3. Exibir menu principal
```

### Construção de Infraestrutura
```
1. Jogador clica em botão de construção
2. Chama ShowBuild*Toolbar() apropriado
3. Barra de ferramentas é exibida
4. Jogador seleciona tipo e constrói
```

### Consulta de Informações
```
1. Jogador ativa ferramenta de informação
2. Clica em tile/objeto
3. ShowLandInfo(tile) é chamado
4. Janela com detalhes é exibida
```

### Gestão de Veículos
```
1. Jogador seleciona veículo
2. Clica em "Ordens"
3. ShowOrdersWindow(vehicle) é chamado
4. Janela de ordens permite editar rotas
```

---

## Considerações de Design

### Centralização de Acessos
Este arquivo serve como **ponto central** para abrir janelas de diversos módulos, evitando que cada parte do código precise conhecer os detalhes de implementação das outras.

### Separação de Responsabilidades
- Cada função chama implementação específica de seu módulo
- `gui.h` apenas declara, não implementa
- Facilita manutenção e testes

### Flexibilidade de Parâmetros
- Muitas funções aceitam parâmetros opcionais com valores padrão
- Permite chamadas simples ou complexas conforme necessidade

---

## Relacionamentos

### Integração com Sistema de Janelas
Todas as funções que retornam `Window*` criam novas instâncias de janelas que são gerenciadas pelo sistema de window manager do OpenTTD.

### Conexão com Input do Usuário
Funções são tipicamente chamadas em resposta a:
- Cliques em botões da interface
- Atalhos de teclado
- Comandos de console
- Scripts de cenário

### Dependência de Estados do Jogo
Algumas funções podem verificar estados antes de executar:
- Modo de jogo vs modo cenário
- Empresa ativa atual
- Permissões do jogador

---

## Notas de Implementação

⚠️ **Atenção**: Este é um arquivo conceitual traduzido para documentação em português. A implementação real mantém os nomes originais em inglês no código fonte.

📝 **Observação**: Comentários no arquivo original indicam "GUI functions that shouldn't be here", sugerindo que este é um arquivo legado que poderia ser refatorado para organização melhor.

🔧 **Manutenção**: Novas funções globais de GUI devem preferencialmente ser declaradas em seus próprios módulos específicos, não neste arquivo genérico.

---

**Status**: ✅ Traduzido Conceitualmente  
**Nível**: 02 - Sistemas Centrais de Interface  
**Categoria**: GUI / Sistema Geral  
**Última Atualização**: Dezembro 2024
