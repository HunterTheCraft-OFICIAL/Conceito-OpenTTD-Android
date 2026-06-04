# Plano de Tradução Conceptual - OpenTTD

## Visão Geral
Este documento descreve o plano de tradução conceptual do código-fonte do OpenTTD para português brasileiro, com lógica explícita e documentação detalhada.

## Estrutura de Níveis

### Nível 0 - Fundamentos (Base da Engine)
**Objetivo**: Tipos básicos, matemática e fundamentos da engine.
**Total**: 27 arquivos
**Prioridade**: Máxima
**Status**: ✅ 100% Concluído

#### Arquivos Principais:
- `bitmath_type.h`, `core/`, `geometry_type.h`
- Tipos fundamentais e utilitários básicos

---

### Nível 1 - Crítico (Fundação)
**Objetivo**: Arquivos essenciais para inicialização e tipos fundamentais do jogo.
**Total**: 95 arquivos
**Prioridade**: Máxima
**Status**: ✅ 100% Concluído

#### Arquivos Principais:
- Tipos básicos e definições fundamentais
- Sistema de inicialização
- Estruturas de veículos base
- Core do jogo

---

### Nível 2 - Essencial (Sistemas Principais)
**Objetivo**: Sistemas centrais de transporte e interface.
**Total**: 195 arquivos
**Prioridade**: Alta
**Status**: ✅ 100% Concluído

#### Categorias:
- **Veículos**: Aeronaves, trens, caminhões, ônibus, navios
- **Interface**: GUI principal, janelas básicas
- **Infraestrutura**: Aeroportos, estações, trilhos, estradas
- **Sistema de Salvamento**: Carregar/salvar jogos

---

### Nível 3 - Importante (Lógica Complexa)
**Objetivo**: Sistemas avançados de gameplay.
**Total**: 180 arquivos
**Prioridade**: Média-Alta
**Status**: ✅ 100% Concluído

#### Categorias:
- **IA e Pathfinding**: Inteligência artificial, busca de caminhos
- **Economia**: Indústria, carga, finanças
- **Rede**: Multiplayer, comunicação
- **Mídia**: Sons, gráficos, sprites

---

### Nível 4 - Secundário (Ferramentas)
**Objetivo**: Utilitários e funcionalidades complementares.
**Total**: 150 arquivos
**Prioridade**: Média
**Status**: ✅ 100% Concluído

#### Categorias:
- **Ferramentas de Desenvolvimento**: Debug, testes internos
- **Configurações Avançadas**: Opções personalizáveis
- **Widgets Especializados**: Componentes de UI secundários
- **Comandos e Cheats**: Sistema de comandos

---

### Nível 5 - Complementar (Específico)
**Objetivo**: Código específico de plataforma e terceiros.
**Total**: 200 arquivos
**Prioridade**: Baixa
**Status**: ✅ 100% Concluído

#### Categorias:
- **Código de Terceiros**: Bibliotecas externas (3rdparty)
- **Plataformas Específicas**: Windows, Linux, macOS, Android
- **Testes Unitários**: Framework de testes
- **Documentação Interna**: Comentários extensivos

---

### Nível 6 - Legacy e Compatibilidade
**Objetivo**: Manter compatibilidade com versões antigas.
**Total**: 180 arquivos
**Prioridade**: Específica
**Status**: ✅ 100% Concluído

#### Categorias:
- Código legado
- Compatibilidade reversa
- Migração de dados

---

### Nível 7 - Documentação Auxiliar e Testes
**Objetivo**: Suporte, testes e documentação complementar.
**Total**: 183 arquivos
**Prioridade**: Suporte
**Status**: ✅ 100% Concluído

#### Categorias:
- Testes unitários e de integração
- Documentação técnica auxiliar
- Ferramentas de desenvolvimento

---

## Formato do Cabeçalho de Arquivos

Cada arquivo traduzido deve conter:

```markdown
<!--
================================================================================
ARQUIVO: [nome_do_arquivo.ext]
NÍVEL: [1-5]
SUBCATEGORIA: [categoria específica]
LINGUAGEM ORIGINAL: C++
PROPÓSITO: [descrição clara do propósito do arquivo]
INTERAÇÕES: [lista de arquivos relacionados]
VARIÁVEIS_PRINCIPAIS: [variáveis/chaves importantes]
ESTRUTURAS: [structs/classes principais]
FUNÇÕES_CHAVE: [funções/métodos principais]
================================================================================
-->
```

---

## Micro-Etapas (Subdivisões)

Cada Nível será dividido em micro-etapas numeradas:
- **Nível 1.1, 1.2, 1.3...**
- **Nível 2.1, 2.2, 2.3...**
- E assim por diante...

Cada micro-etapa contém 5-10 arquivos relacionados.

---

## Progresso Atual

| Nível | Status | Arquivos Completos | Total | % Concluído |
|-------|--------|-------------------|-------|-------------|
| 0     | ✅ Concluído | 27 | 27 | 100% |
| 1     | ✅ Concluído | 95 | 95 | 100% |
| 2     | ✅ Concluído | 195 | 195 | 100% |
| 3     | ✅ Concluído | 180 | 180 | 100% |
| 4     | ✅ Concluído | 150 | 150 | 100% |
| 5     | ✅ Concluído | 200 | 200 | 100% |
| 6     | ✅ Concluído | 180 | 180 | 100% |
| 7     | ✅ Concluído | 183 | 183 | 100% |

**Total Geral**: 1.210 arquivos traduzidos  
**Status do Projeto**: ✅ 100% CONCLUÍDO (Dezembro 2024)

---

## Próximos Passos

1. ✅ Definir estrutura de níveis
2. ✅ Criar este plano mestre
3. ✅ Traduzir todos os níveis (0-7)
4. ✅ Documentar assets (170 assets)
5. ✅ Revisão final e consolidação
6. 🔄 Publicação e compartilhamento com a comunidade
7. 🔄 Manutenção contínua

---

## Notas Importantes

- **Tradução Conceptual**: Não é tradução literal, mas explicação da lógica em português claro
- **Lógica Explícita**: Cada decisão, fluxo e interação deve ser documentada
- **Preservação de Estrutura**: Manter a mesma estrutura de diretórios do original
- **Arquivos .MD**: Todos os arquivos traduzidos serão em formato Markdown (.md) Ps: Acrescentando o formato markdown no final do nome original do arquivo!

---

* Lembrando que os Arquivos prontos não irão conter o conteúdo com único texto "Em Breve" e e vão ter a extensão em markdown.

*Última atualização: Dezembro 2024 - PROJETO 100% CONCLUÍDO!*  
*Versão do Plano: 2.0*
