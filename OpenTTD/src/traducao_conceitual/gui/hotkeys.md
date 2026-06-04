# Sistema de Teclas de Atalho (Hotkeys)

## Visão Geral
Este arquivo define o sistema de teclas de atalho do OpenTTD, permitindo que os jogadores personalizem e utilizem combinações de teclas para executar ações rapidamente nas janelas do jogo.

## Estruturas Principais

### Hotkey
Representa uma única tecla de atalho com suas configurações:
- **name**: Nome identificador da tecla (usado para salvar/carregar configurações)
- **num**: Número identificador único da tecla de atalho
- **keycodes**: Lista de códigos de teclas associados a este atalho

**Métodos:**
- `AddKeycode(keycode)`: Adiciona um novo código de tecla ao atalho
- Construtores: Permitem criar hotkeys com uma ou múltiplas teclas padrão

### HotkeyList
Gerencia uma lista completa de teclas de atalho para uma janela específica:
- **ini_group**: Nome do grupo no arquivo de configuração INI
- **items**: Array de objetos Hotkey
- **global_hotkey_handler**: Função opcional para processar atalhos globais

**Funcionalidades:**
- `Load(ini)`: Carrega configurações de hotkeys de um arquivo INI
- `Save(ini)`: Salva configurações atuais para arquivo INI
- `CheckMatch(keycode, global_only)`: Verifica se uma tecla pressionada corresponde a algum hotkey definido

## Funções Globais

### Gerenciamento de Configuração
- `LoadHotkeysFromConfig()`: Carrega todas as configurações de hotkeys do arquivo de configuração
- `SaveHotkeysToConfig()`: Salva as configurações atuais no arquivo de configuração

### Processamento de Eventos
- `HandleGlobalHotkeys(key, keycode)`: Processa teclas de atalho globais durante o input do usuário
- `IsQuitKey(keycode)`: Verifica se uma tecla específica é configurada como tecla de saída do jogo

## Constantes Especiais

### HOTKEY_LIST_END
Marcador especial para indicar o fim de uma lista de hotkeys. Usado como sentinela em arrays de hotkeys.

## Fluxo de Funcionamento

1. **Inicialização**: Listas de hotkeys são definidas para cada tipo de janela
2. **Carregamento**: Configurações do usuário são lidas do arquivo de configuração
3. **Detecção**: Quando uma tecla é pressionada, o sistema verifica correspondências
4. **Execução**: Se houver match, a ação associada é executada
5. **Salvamento**: Alterações do usuário são persistidas no arquivo de configuração

## Casos de Uso Típicos

- **Atalhos de Janela**: Ctrl+S para salvar, F1 para ajuda
- **Navegação**: Tab para alternar entre campos, Enter para confirmar
- **Ferramentas**: Números 1-9 para selecionar ferramentas de construção
- **Visualização**: Zoom in/out, rotação de mapa

## Considerações de Implementação

- Suporta múltiplas teclas para o mesmo atalho (OR lógico)
- Permite sobrescrita de configurações padrão pelo usuário
- Separação entre hotkeys locais (da janela) e globais (do jogo)
- Prevenção de cópia não intencional através de construtor privado
