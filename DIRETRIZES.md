# 📖 DIRETRIZES DE TRADUÇÃO - Conceito OpenTTD Android

## Visão Geral
Este documento estabelece os padrões e diretrizes para a tradução do código-fonte OpenTTD para o **Português Brasileiro (PT-BR)** em formato **Conceitual e Explicativo**.

O objetivo é criar uma documentação em português que não apenas traduza o código, mas **explique como a lógica funciona** e como cada arquivo interage com os outros.

---

## 1️⃣ FORMATO DE SAÍDA

### 1.1 Extensão de Arquivo
- **Formato:** Markdown (`.md`)
- **Nomeclatura:** `[NomeOriginal].h.md` ou `[NomeOriginal].cpp.md`
- **Local:** Pasta `Conceito-OpenTTD/` (espelhando a estrutura de `OpenTTD/src/`)

**Exemplo:**
```
OpenTTD/src/aircraft.h  →  Conceito-OpenTTD/aircraft.h.md
OpenTTD/src/vehicle_base.h  →  Conceito-OpenTTD/vehicle_base.h.md
```

### 1.2 Idioma
- **Língua Principal:** Português Brasileiro (PT-BR)
- **Termos Técnicos:** Mantidos em inglês (seguem padrão OpenTTD)
- **Comentários:** 100% em português
- **Explicações:** Claras e acessíveis

---

## 2️⃣ ESTRUTURA OBRIGATÓRIA DO ARQUIVO

Cada arquivo traduzido **DEVE** seguir esta estrutura:

```markdown
# [Nome do Arquivo Original]

**Arquivo Original:** `src/[caminho]/[arquivo].h` ou `.cpp`
**Linguagem Original:** C++ (ou outra linguagem)
**Versão OpenTTD:** [versão se disponível]
**Data de Tradução:** [data da tradução]

---

## 📌 Arquivos Relacionados (Interações Diretas)

| Arquivo | Tipo | Motivo da Interação |
|---------|------|-------------------|
| `vehicle_base.h` | Herança | Classe base para Aircraft |
| `station_map.h` | Include | Mapeamento de estações no mapa |
| `aircraft_cmd.cpp` | Implementação | Implementa comandos de aeronaves |
| `aircraft_gui.cpp` | Interface | Renderização gráfica da aeronave |
| `engine_type.h` | Dependência | Define tipos de engine/motor |

---

## 📚 [O que é este arquivo?]

[Explicação clara do propósito do arquivo em português]

---

## 🏗️ [Estrutura Principal]

### Enums
[Listar e explicar todos os enums]

### Structs
[Listar e explicar todas as estruturas]

### Funções Principais
[Listar as funções mais importantes]

---

## 🔄 [Fluxo de Lógica]

[Descrever como o arquivo funciona e interage com outros]

---

## 💡 [Notas Importantes]

[Informações relevantes sobre performance, otimizações, etc.]

---

## 📝 [Código Comentado]

[Seção com trechos-chave do código comentados em português]

```

---

## 3️⃣ CABEÇALHO OBRIGATÓRIO (Template)

Copie e cole este cabeçalho no início de cada arquivo:

```markdown
# [Nome do Arquivo Original]

**Arquivo Original:** `src/[caminho completo]/[arquivo].h`
**Linguagem Original:** C++
**Versão OpenTTD:** [versão]
**Data de Tradução:** [DD/MM/AAAA]
**Tradutor:** [@seu-usuario]

---

## 📌 Arquivos Relacionados (Interações Diretas)

| Arquivo | Tipo | Motivo |
|---------|------|--------|
| [arquivo1] | [tipo: Herança/Include/Implementação/Dependência] | [motivo breve] |
| [arquivo2] | [tipo] | [motivo breve] |

---

## 📚 O que é este arquivo?

[1-2 parágrafos explicando o propósito]

---
```

---

## 4️⃣ O QUE TRADUZIR vs. O QUE NÃO TRADUZIR

### ✅ TRADUZIR:
- ✅ Comentários em inglês (todas as linhas começadas com `//` ou `/* */`)
- ✅ Documentação doxygen (`/** @file ... */`)
- ✅ Explicações de lógica complexa
- ✅ Strings de contexto e descrição
- ✅ Toda documentação suplementar

### ❌ NÃO TRADUZIR:
- ❌ Nomes de classes, structs, enums (ex: `Aircraft`, `AircraftFlyingAltitude`)
- ❌ Nomes de variáveis (ex: `crashed_counter`, `targetairport`)
- ❌ Nomes de funções (ex: `HandleAircraftEnterHangar()`)
- ❌ Constantes técnicas (ex: `AIRCRAFT_MIN_FLYING_ALTITUDE`)
- ❌ Identificadores e símbolos do código
- ❌ URLs e referências externas
- ❌ Nomes de projetos e softwares

**Exemplo:**
```c++
/* TRADUZIR ISTO */
// Alterar a altitude de voo do avião para o nível mínimo seguro
int min_altitude = AIRCRAFT_MIN_FLYING_ALTITUDE; // NÃO traduzir constante

/* NÃO TRADUZIR ISTO */
struct Aircraft { // Manter "Aircraft"
    int crashed_counter; // Manter "crashed_counter"
};
```

---

## 5️⃣ FORMATO DE EXPLICAÇÃO

### 5.1 Explicação de Estruturas

```markdown
### Struct: `Aircraft`

**Propósito:** Representa uma aeronave (avião ou helicóptero) no mapa.

**Campos Principais:**
- `uint16 crashed_counter` - Contador para animações de queda (em ticks)
- `byte pos` - Próxima posição desejada da aeronave
- `StationID targetairport` - Identificador do aeroporto de destino

**Relacionamentos:**
- Herda de: `SpecializedVehicle<Aircraft, VEH_AIRCRAFT>`
- Utilizado por: `aircraft_cmd.cpp`, `aircraft_gui.cpp`
```

### 5.2 Explicação de Enums

```markdown
### Enum: `AircraftSubType`

**Propósito:** Define os diferentes tipos de subtipo de aeronaves.

| Valor | Nome | Descrição |
|-------|------|-----------|
| 0 | `AIR_HELICOPTER` | Helicóptero |
| 2 | `AIR_AIRCRAFT` | Avião comercial |
| 4 | `AIR_SHADOW` | Sombra da aeronave (renderização) |
| 6 | `AIR_ROTOR` | Rotor de helicóptero (renderização) |

**Notas:**
- Valores pares e pulados propositalmente para evitar conflitos
- Usados para determinação correta de sprites e comportamento
```

### 5.3 Explicação de Funções

```markdown
### Função: `HandleAircraftEnterHangar()`

**Assinatura:**
```cpp
void HandleAircraftEnterHangar(Aircraft *v);
```

**Propósito:** Processa a entrada de uma aeronave no hangar, pausando animações e ocultando sprites.

**Parâmetros:**
- `Aircraft *v` - Ponteiro para a aeronave que está entrando no hangar

**O que faz:**
1. Define velocidade da aeronave para 0
2. Define progresso para 0
3. Oculta sprites de sombra e rotor (se helicóptero)
4. Atualiza posição visual

**Chamado por:**
- `aircraft_cmd.cpp` - Quando ordem para hangar é executada
- `disaster_vehicle.cpp` - Para desastres aéreos

**Exemplo de Uso:**
```cpp
Aircraft *meu_aviao = Aircraft::Get(id);
HandleAircraftEnterHangar(meu_aviao);
```
```

---

## 6️⃣ PADRÃO DE COMENTÁRIOS EM PORTUGUÊS

### Exemplo de Conversão

**Original (Inglês):**
```cpp
/**
 * Handle Aircraft specific tasks when an Aircraft enters a hangar
 * @param *v Vehicle that enters the hangar
 */
void HandleAircraftEnterHangar(Aircraft *v)
{
    v->subspeed = 0;
    v->progress = 0;
    
    /* Shadow aircraft must be hidden */
    Aircraft *u = v->Next();
    u->vehstatus |= VS_HIDDEN;
}
```

**Traduzido (Português):**
```markdown
### Função: `HandleAircraftEnterHangar()`

**Propósito:** Processa tarefas específicas da aeronave quando ela entra em um hangar.

**Assinatura:**
```cpp
void HandleAircraftEnterHangar(Aircraft *v);
```

**Parâmetros:**
- `Aircraft *v` - Ponteiro para o veículo (aeronave) que está entrando no hangar

**Implementação:**
```cpp
/**
 * Processa tarefas específicas da aeronave quando ela entra em um hangar
 * @param *v Veículo (aeronave) que está entrando no hangar
 */
void HandleAircraftEnterHangar(Aircraft *v)
{
    v->subspeed = 0;                    // Define velocidade do sub-movimento para 0
    v->progress = 0;                    // Define progresso de animação para 0
    
    /* A aeronave sombra deve ser ocultada */
    Aircraft *u = v->Next();            // Obtém a próxima aeronave (geralmente sombra)
    u->vehstatus |= VS_HIDDEN;          // Marca como oculta (não renderizar)
}
```

**Notas:**
- A sombra é uma entidade separada para renderização correta
- Velocidade zerada evita comportamento inesperado enquanto no hangar
```

---

## 7️⃣ ESTRUTURA DE NÍVEIS DE PRIORIDADE

### Nível 1 - CRÍTICO (Fundação)
**~25 arquivos** - Estruturas base do sistema

Exemplos:
- `vehicle_base.h` - Classe base para todos os veículos
- `vehicle.h` - Definições principais de veículos
- `tile_type.h` - Tipos fundamentais de tiles

### Nível 2 - ESSENCIAL (Sistemas Principais)
**~60 arquivos** - Sistemas principais do jogo

Exemplos:
- `aircraft.h` - Definições de aeronaves
- `train.h` - Definições de trens
- `station.h` - Definições de estações

### Nível 3 - IMPORTANTE (Lógica Complexa)
**~125 arquivos** - Lógica complexa e comportamentos

Exemplos:
- `pathfinder.h` - Algoritmos de caminho
- `network/` - Sistema de rede multiplayer
- `saveload/` - Sistema de salvamento

### Nível 4 - SECUNDÁRIO (Ferramentas)
**~175 arquivos** - Utilitários e ferramentas

Exemplos:
- `console/` - Sistema de console
- `debug/` - Ferramentas de debug
- `misc/` - Utilitários diversos

### Nível 5 - COMPLEMENTAR (Específico)
**~200+ arquivos** - Conteúdo específico e complementar

Exemplos:
- Localizações específicas
- Sistemas de easter eggs
- Recursos específicos da plataforma

---

## 8️⃣ CHECKLIST PARA CADA ARQUIVO TRADUZIDO

Antes de finalizar a tradução, verifique:

- [ ] **Cabeçalho Completo**
  - [ ] Nome do arquivo original
  - [ ] Caminho completo
  - [ ] Arquivos relacionados com tabela
  - [ ] Data de tradução

- [ ] **Conteúdo**
  - [ ] Todos os comentários traduzidos
  - [ ] Nenhum identificador de código traduzido
  - [ ] Estruturas explicadas
  - [ ] Enums documentados
  - [ ] Funções principais descritas
  - [ ] Fluxo de lógica claro

- [ ] **Formatação**
  - [ ] Markdown válido
  - [ ] Títulos com `#` apropriado
  - [ ] Código em blocos ` ``` `
  - [ ] Tabelas bem formatadas
  - [ ] Links funcionais (se houver)

- [ ] **Qualidade**
  - [ ] Português claro e correto
  - [ ] Termos técnicos consistentes
  - [ ] Exemplos práticos incluídos
  - [ ] Sem repetições desnecessárias

---

## 9️⃣ EXEMPLO COMPLETO DE ARQUIVO TRADUZIDO

Veja `Conceito-OpenTTD/aircraft.h.md` para um exemplo prático de como um arquivo deve ser traduzido seguindo estas diretrizes.

---

## 🔟 PROCESSO DE CONTRIBUIÇÃO

1. **Escolha um arquivo** de acordo com o nível de prioridade
2. **Copie o template** do cabeçalho
3. **Analise o arquivo original** em `OpenTTD/src/`
4. **Identifique as dependências** (arquivos relacionados)
5. **Crie a tradução** seguindo as diretrizes
6. **Teste o Markdown** (abra em preview)
7. **Faça o commit** com mensagem descritiva
8. **Atualize o README.md** com o arquivo traduzido

---

## 📞 DÚVIDAS E CONTRIBUIÇÕES

- **Termo não sei traduzir?** Mantenha em inglês e adicione explicação
- **Arquivo complexo?** Divida em sub-seções
- **Descobriu erro?** Corrija no commit seguinte
- **Sugestão de melhoria?** Abra uma Issue

---

## 📋 HISTÓRICO DE VERSÕES

| Versão | Data | Alterações |
|--------|------|-----------|
| 1.0 | 02/06/2026 | Versão inicial - Baseada nas práticas existentes |

---

**Última atualização:** 02 de Junho de 2026
**Criado por:** GitHub Copilot Assistant
**Status:** ✅ Ativo

