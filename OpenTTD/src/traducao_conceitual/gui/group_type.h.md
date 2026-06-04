# Tipos de Grupo (Group Type)

## Visão Geral
Este arquivo define os tipos básicos e constantes relacionadas ao sistema de grupos do OpenTTD. Grupos são usados para organizar veículos da frota de uma empresa, permitindo gerenciamento eficiente de ordens, substituição e monitoramento.

## Definições de Tipo

### GroupID
**Tipo:** `uint16` (inteiro sem sinal de 16 bits)

**Propósito:** Tipo base para todos os identificadores de grupo no jogo.

**Intervalo de Valores:**
- `0x0000` a `0xFFFB`: IDs de grupos normais (definidos pelo usuário)
- `0xFFFC` a `0xFFFF`: IDs especiais/reservados

## Constantes Especiais de GroupID

### NEW_GROUP
**Valor:** `0xFFFC` (65500)

**Propósito:** Sentinela indicando que um novo grupo deve ser criado.

**Uso Típico:**
- Quando jogador solicita criação de novo grupo através da UI
- Parâmetro em funções que podem criar grupos sob demanda
- Indica operação "criar novo" em vez de "usar existente"

### ALL_GROUP
**Valor:** `0xFFFD` (65501)

**Propósito:** Representa virtualmente TODOS os veículos de um tipo.

**Comportamento:**
- Não é um grupo real armazenado
- Usado para aplicar operações a toda a frota
- Útil para ordens globais ou estatísticas consolidadas
- Veículos não são explicitamente adicionados a este grupo

### DEFAULT_GROUP
**Valor:** `0xFFFE` (65502)

**Propósito:** Grupo padrão para veículos não agrupados.

**Comportamento:**
- Todos os veículos recém-comprados vão automaticamente para este grupo
- Veículos removidos de grupos personalizados retornam aqui
- Pode ter ordens e configurações próprias
- Sempre existe, não pode ser deletado

### INVALID_GROUP
**Valor:** `0xFFFF` (65503)

**Propósito:** Sentinela para indicar grupo inválido ou inexistente.

**Uso Típico:**
- Valor inicial para variáveis de GroupID não inicializadas
- Retorno de funções quando grupo não é encontrado
- Verificação de validade de referências a grupos
- Similar a `nullptr` para ponteiros de grupo

## Constantes de String

### MAX_LENGTH_GROUP_NAME_CHARS
**Valor:** `32` caracteres (incluindo caractere nulo `'\0'`)

**Propósito:** Define o comprimento máximo permitido para nomes de grupos.

**Implicações:**
- Nomes de grupos podem ter até 31 caracteres visíveis
- 1 caractere reservado para terminação nula
- Aplicado em validação de entrada na UI
- Afeta alocação de buffers para armazenamento de nomes

## Estruturas Forward-Declared

### Group (struct)
**Declaração:** `struct Group;`

**Propósito:** Declaração antecipada da estrutura completa de grupo.

**Nota:** A definição completa está em `group.h`, não neste arquivo de tipos.

## Hierarquia de Grupos

```
ALL_GROUP (virtual - todos os veículos)
├── DEFAULT_GROUP (veículos não agrupados)
├── Grupo Personalizado 1
├── Grupo Personalizado 2
└── ... (mais grupos definidos pelo usuário)
```

## Casos de Uso Comuns

1. **Criação de Grupo:** Usar `NEW_GROUP` como parâmetro para factory methods
2. **Ordens Globais:** Aplicar ordem a `ALL_GROUP` para afetar toda frota
3. **Veículos Novos:** Automaticamente atribuídos a `DEFAULT_GROUP`
4. **Validação:** Checar se `group_id != INVALID_GROUP` antes de usar
5. **UI:** Limitar input de nome a 31 caracteres baseado em `MAX_LENGTH_GROUP_NAME_CHARS`

## Integração com Outros Sistemas

- **Veículos:** Cada veículo tem referência ao seu `GroupID`
- **Ordens:** Grupos podem ter ordens compartilhadas
- **UI:** Janelas de grupo usam estas constantes para lógica especial
- **Save/Load:** IDs especiais são serializados/desserializados corretamente
- **NewGRF:** Scripts podem acessar informações de grupos via API

## Considerações de Implementação

- IDs especiais estão no topo do intervalo `uint16` para evitar colisões
- Comparisons devem usar valores completos (não assumir overflow)
- Sempre validar GroupID antes de usar como índice em arrays
- `INVALID_GROUP` é útil para assertions e verificações de debug
