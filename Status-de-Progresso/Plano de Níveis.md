# Plano de Tradução Conceptual - OpenTTD

## Visão Geral
Este documento descreve o plano de tradução conceptual do código-fonte do OpenTTD para português brasileiro, com lógica explícita e documentação detalhada.

## Estrutura de Níveis

### Nível 1 - Crítico (Fundação)
**Objetivo**: Arquivos essenciais para inicialização e tipos fundamentais do jogo.
**Estimativa**: 20-30 arquivos
**Prioridade**: Máxima

#### Arquivos Principais:
- Tipos básicos e definições fundamentais
- Sistema de inicialização
- Estruturas de veículos base
- Core do jogo

---

### Nível 2 - Essencial (Sistemas Principais)
**Objetivo**: Sistemas centrais de transporte e interface.
**Estimativa**: 50-70 arquivos
**Prioridade**: Alta

#### Categorias:
- **Veículos**: Aeronaves, trens, caminhões, ônibus, navios
- **Interface**: GUI principal, janelas básicas
- **Infraestrutura**: Aeroportos, estações, trilhos, estradas
- **Sistema de Salvamento**: Carregar/salvar jogos

---

### Nível 3 - Importante (Lógica Complexa)
**Objetivo**: Sistemas avançados de gameplay.
**Estimativa**: 100-150 arquivos
**Prioridade**: Média-Alta

#### Categorias:
- **IA e Pathfinding**: Inteligência artificial, busca de caminhos
- **Economia**: Indústria, carga, finanças
- **Rede**: Multiplayer, comunicação
- **Mídia**: Sons, gráficos, sprites

---

### Nível 4 - Secundário (Ferramentas)
**Objetivo**: Utilitários e funcionalidades complementares.
**Estimativa**: 150-200 arquivos
**Prioridade**: Média

#### Categorias:
- **Ferramentas de Desenvolvimento**: Debug, testes internos
- **Configurações Avançadas**: Opções personalizáveis
- **Widgets Especializados**: Componentes de UI secundários
- **Comandos e Cheats**: Sistema de comandos

---

### Nível 5 - Complementar (Específico)
**Objetivo**: Código específico de plataforma e terceiros.
**Estimativa**: Restante dos arquivos (~200+)
**Prioridade**: Baixa

#### Categorias:
- **Código de Terceiros**: Bibliotecas externas (3rdparty)
- **Plataformas Específicas**: Windows, Linux, macOS, Android
- **Testes Unitários**: Framework de testes
- **Documentação Interna**: Comentários extensivos

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

| Nível | Status | Arquivos Completos | Total Estimado | % Concluído |
|-------|--------|-------------------|----------------|-------------|
| 1     | ⏳ Iniciando | 0 | ~25 | 0% |
| 2     | ⏸️ Aguardando | 0 | ~60 | 0% |
| 3     | ⏸️ Aguardando | 0 | ~125 | 0% |
| 4     | ⏸️ Aguardando | 0 | ~175 | 0% |
| 5     | ⏸️ Aguardando | 0 | ~200+ | 0% |

**Total Geral**: ~585 arquivos na raiz de `src/` + subdiretórios

---

## Próximos Passos

1. ✅ Definir estrutura de níveis
2. ✅ Criar este plano mestre
3. 🔄 Iniciar Nível 1.1 (Arquivos fundamentais)
4. ⏳ Traduzir aircraft.h (exemplo piloto)
5. ⏳ Continuar com próximos arquivos do Nível 1

---

## Notas Importantes

- **Tradução Conceptual**: Não é tradução literal, mas explicação da lógica em português claro
- **Lógica Explícita**: Cada decisão, fluxo e interação deve ser documentada
- **Preservação de Estrutura**: Manter a mesma estrutura de diretórios do original
- **Arquivos .MD**: Todos os arquivos traduzidos serão em formato Markdown (.md) Ps: Acrescentando o formato markdown no final do nome original do arquivo!

---

* Lembrando que os Arquivos prontos não irão conter o conteúdo com único texto "Em Breve" e e vão ter a extensão em markdown.

*Última atualização: Junho 2024*
*Versão do Plano: 1.1*
