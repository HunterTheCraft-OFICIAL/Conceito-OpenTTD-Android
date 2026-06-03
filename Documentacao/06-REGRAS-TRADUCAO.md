# 📝 Regras de Tradução Conceitual

## 🎯 Princípios Fundamentais

### 1. Clareza sobre Literalidade

Priorize a compreensão do conceito em vez da tradução palavra por palavra.

**Exemplo:**
- ❌ Literal: "Veículo base consiste em..."
- ✅ Conceitual: "A estrutura base do veículo contém..."

### 2. Consistência Terminológica

Use sempre os mesmos termos para os mesmos conceitos. Consulte o [Glossário](./07-GLOSSARIO.md).

**Exemplo:**
- Use sempre "veículo" em vez de alternar entre "veículo", "transporte", "unidade"
- Use sempre "estação" em vez de "terminal", "parada", "ponto"

### 3. Contextualização

Sempre que possível, explique o contexto de uso do componente.

**Exemplo:**
```markdown
## VehicleType (Tipo de Veículo)

Este enum define os tipos básicos de veículos no jogo. É utilizado em:
- Sistema de compra de veículos
- Filtros de interface do usuário
- Lógica de substituição automática
```

## 📋 Formato Padrão dos Arquivos

### Estrutura de Diretórios

**IMPORTANTE:** A estrutura do diretório `Conceito-OpenTTD/` deve espelhar **exatamente** a estrutura do repositório original do OpenTTD.

- Cada arquivo mantém o **nome original exato**, apenas adicionando a extensão `.md` no final
- Não há tradução ou alteração nos nomes dos arquivos
- A organização em pastas/subpastas é idêntica à original

**Exemplo de Estrutura:**
```
OpenTTD Original:          Conceito-OpenTTD:
src/aircraft.h      →      src/aircraft.h.md
src/engine.cpp      →      src/engine.cpp.md
docs/multiplayer.md →      docs/multiplayer.md.md
README.md           →      README.md.md
```

### Conteúdo dos Arquivos

#### Antes da Tradução

Todo arquivo recém-criado (ainda não traduzido) deve conter **apenas** o texto:

```markdown
Em Breve
```

Isso indica que:
- O arquivo foi mapeado na estrutura
- Ainda não possui tradução conceitual
- Está aguardando ser trabalhado

#### Após a Tradução

O arquivo mantém o **mesmo nome** (com `.md`), mas o conteúdo é substituído pela tradução conceitual completa.

**Exemplo:**

**Arquivo:** `src/vehicle_type.h.md`

**Antes:**
```markdown
Em Breve
```

**Depois:**
```markdown
# vehicle_type.h

## Propósito

Este arquivo define os tipos básicos de veículos utilizados no OpenTTD...

[conteúdo completo da tradução conceitual]
```

## 🔤 Diretrizes de Tradução

### Termos Técnicos - Manter em Inglês

Alguns termos devem ser mantidos em inglês por serem padrão da indústria:

- `enum`, `struct`, `class`, `template`
- `namespace`, `include`, `define`
- Nomes de variáveis e funções (código)
- APIs e bibliotecas externas

### Termos Técnicos - Traduzir

Outros termos devem ser traduzidos para facilitar a compreensão:

| Inglês | Português |
|--------|-----------|
| vehicle | veículo |
| aircraft | aeronave |
| station | estação |
| cargo | carga |
| engine | motor/locomotiva |
| depot | depósito |
| track | trilho |
| signal | sinal |

### Comentários de Código

Traduza comentários explicativos, mas mantenha:

- Referências a nomes de variáveis/funções
- URLs e referências externas
- Exemplos de código

**Exemplo:**
```cpp
// Original:
// Check if vehicle is in depot for repairs

// Tradução:
// Verifica se o veículo está no depósito para reparos
```

## ✨ Boas Práticas

### 1. Seja Conciso

Evite textos muito longos. Vá direto ao ponto.

### 2. Use Exemplos

Quando apropriado, inclua exemplos de uso.

### 3. Mantenha Atualizado

Se o código original mudar, atualize a tradução conceitual.

### 4. Revise

Sempre revise sua tradução em busca de:
- Erros de português
- Termos inconsistentes
- Explicações confusas

## 🚫 Erros Comuns a Evitar

1. **Tradução literal demais**: Perde-se o significado conceitual
2. **Termos inconsistentes**: Usa palavras diferentes para o mesmo conceito
3. **Falta de contexto**: Não explica onde/quando algo é usado
4. **Excesso de detalhes**: Inclui informações óbvias ou irrelevantes
5. **Ignorar glossário**: Cria novos termos sem necessidade

## 📊 Processo de Tradução

### Passo a Passo

1. **Leia o arquivo original** completamente
2. **Identifique os componentes principais** (classes, funções, enums)
3. **Consulte o glossário** para termos já padronizados
4. **Escreva a tradução conceitual** seguindo o formato padrão
5. **Revise** buscando erros e inconsistências
6. **Compare** com arquivos similares já traduzidos
7. **Marque como concluído** no checklist

## 🔍 Checklist de Qualidade

Antes de considerar um arquivo como traduzido:

- [ ] O propósito do arquivo está claro?
- [ ] Os principais componentes foram documentados?
- [ ] A terminologia está consistente com o glossário?
- [ ] Há exemplos ou contextos de uso quando necessário?
- [ ] O formato segue o padrão estabelecido?
- [ ] Não há erros de português?
- [ ] Termos técnicos em código foram mantidos em inglês?

## 📞 Dúvidas Frequentes

### "Devo traduzir o nome das variáveis?"

**Não.** Nomes de variáveis, funções e classes fazem parte do código e não devem ser alterados.

### "E se não houver equivalente em português?"

Use o termo em inglês seguido da explicação entre parênteses na primeira ocorrência. Depois, use apenas o termo em português.

**Exemplo:** "O dispatcher (gerenciador de tarefas) é responsável por..."

### "Posso adicionar informações que não estão no original?"

**Sim!** A tradução conceitual tem como objetivo explicar, não apenas traduzir. Adicione contexto quando ajudar na compreensão.

---

*Documento criado como parte da reorganização da documentação - Junho 2024*
