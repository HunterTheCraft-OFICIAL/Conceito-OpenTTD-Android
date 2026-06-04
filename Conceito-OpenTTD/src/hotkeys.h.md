# 📄 hotkeys.h - Sistema de Teclas de Atalho

## Visão Geral
Arquivo de cabeçalho que define o sistema de **teclas de atalho (hotkeys)** do OpenTTD, permitindo que os jogadores personalizem controles de teclado para ações específicas em janelas e funcionalidades globais.

---

## Estruturas Principais

### Hotkey
Representa uma única tecla de atalho com seus dados completos.

**Atributos:**
- `name` → Nome da tecla (para salvar/carregar no arquivo de configuração)
- `num` → Número identificador único da tecla
- `keycodes` → Lista de códigos de teclas associados

**Métodos:**
- `AddKeycode(keycode)` → Adiciona um novo código de tecla ao atalho

**Construtores:**
- `Hotkey(default_keycode, name, num)` → Cria atalho com única tecla padrão
- `Hotkey(default_keycodes, name, num)` → Cria atalho com múltiplas teclas padrão

---

### HotkeyList
Gerencia uma lista completa de teclas de atalho para uma janela específica.

**Atributos:**
- `ini_group` → Nome do grupo no arquivo INI para salvamento
- `items` → Ponteiro para array de objetos Hotkey
- `global_hotkey_handler` → Função manipuladora de atalhos globais (opcional)

**Métodos:**
- `Load(ini)` → Carrega configurações de teclas do arquivo INI
- `Save(ini)` → Salva configurações atuais no arquivo INI
- `CheckMatch(keycode, global_only)` → Verifica se uma tecla corresponde a algum atalho cadastrado

**Tipo Especial:**
- `GlobalHotkeyHandlerFunc` → Tipo de função para manipular atalhos globais

---

## Constantes

### HOTKEY_LIST_END
Marcador especial que indica o fim da lista de teclas de atalho.
```cpp
#define HOTKEY_LIST_END Hotkey((uint16)0, nullptr, -1)
```

---

## Funções Globais

### Gerenciamento de Configuração
- `LoadHotkeysFromConfig()` → Carrega todas as teclas de atalho salvas na configuração
- `SaveHotkeysToConfig()` → Salva todas as teclas de atalho atuais na configuração

### Manipulação de Eventos
- `HandleGlobalHotkeys(key, keycode)` → Processa teclas pressionadas para atalhos globais
- `IsQuitKey(keycode)` → Verifica se a tecla pressionada é a tecla de saída do jogo

---

## Fluxo de Funcionamento

1. **Inicialização**: Listas de atalhos são criadas com valores padrão
2. **Carregamento**: Configurações do usuário são lidas do arquivo INI
3. **Detecção**: Quando uma tecla é pressionada, `CheckMatch` verifica correspondências
4. **Execução**: Se houver match, a ação associada é executada
5. **Salvamento**: Alterações do usuário são persistidas no arquivo de configuração

---

## Casos de Uso Típicos

### Para Desenvolvedores de Janelas
```cpp
// Definir lista de atalhos para uma janela
Hotkey my_hotkeys[] = {
    Hotkey(WKC_DELETE, "delete", 0),
    Hotkey(WKC_RETURN, "confirm", 1),
    HOTKEY_LIST_END
};

HotkeyList window_hotkeys("my_window", my_hotkeys);
```

### Para Personalização do Usuário
Os jogadores podem editar o arquivo de configuração para:
- Remapear teclas existentes
- Adicionar múltiplas teclas para mesma ação
- Criar combinações personalizadas

---

## Considerações de Design

### Separação de Responsabilidades
- **Hotkey**: Dados individuais de cada atalho
- **HotkeyList**: Gerenciamento de coleção e persistência
- **Funções Globais**: Interface com o sistema de configuração

### Flexibilidade
- Suporte a múltiplas teclas por ação
- Handler global opcional para atalhos que funcionam em qualquer contexto
- Sistema de identificação numérica para referência interna

### Persistência
- Integração nativa com sistema INI do OpenTTD
- Carregamento automático na inicialização
- Salvamento sob demanda quando configurações mudam

---

## Relacionamentos

### Dependências Internas
- `core/smallvec_type.hpp` → Vetores otimizados para armazenamento
- `gfx_type.h` → Tipos gráficos (códigos de teclas)
- `window_type.h` → Tipos relacionados a janelas
- `string_type.h` → Manipulação de strings

### Integração com Outros Sistemas
- **Sistema de Janelas**: Cada janela pode ter sua própria lista de atalhos
- **Sistema de Configuração**: Leitura/escrita em arquivos INI
- **Sistema de Input**: Processamento de eventos de teclado
- **Sistema Global**: Atalhos que funcionam em qualquer contexto do jogo

---

## Padrões de Nomenclatura

### Em Português (Conceitual)
- Hotkey → Tecla de Atalho
- HotkeyList → Lista de Teclas de Atalho
- Keycode → Código da Tecla
- GlobalHotkeyHandler → Manipulador de Atalhos Globais
- IniFile → Arquivo de Configuração INI

---

## Notas de Implementação

⚠️ **Atenção**: Este é um arquivo conceitual traduzido para documentação em português. A implementação real mantém os nomes originais em inglês no código fonte.

📝 **Observação**: O sistema usa `nullptr` para indicar fim de listas e valores nulos, seguindo padrões modernos de C++.

🔧 **Extensibilidade**: Novos atalhos podem ser adicionados sem quebrar compatibilidade com configurações existentes.

---

**Status**: ✅ Traduzido Conceitualmente  
**Nível**: 02 - Sistemas Centrais de Interface  
**Categoria**: GUI / Input  
**Última Atualização**: Dezembro 2024
