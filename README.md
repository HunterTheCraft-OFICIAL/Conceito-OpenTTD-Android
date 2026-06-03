# Conceito-OpenTTD-Android

| |
| --- |
| [✓] Etapa 01 - Baixar Clone na Subpasta da Raiz do Projeto |
| [✓] Etapa 02 - Recriar a estrutura do Clone baixado no Endereço correspondente |
| [🔄] Etapa 03 - Traduzir a Linguagem de Programação e Lógica para Língua Portuguesa do Brasil em formato de conceito e com a Lógica explícita de arquivo por arquivo |

## 📁 Estrutura do Projeto

### Diretório `Documentacao/`

Este diretório contém **toda a documentação organizada** do projeto de tradução conceitual:

- **[README.md](Documentacao/README.md)** - Índice central com links para todos os documentos
- **[01-VISÃO-GERAL.md](Documentacao/01-VISÃO-GERAL.md)** - Visão completa do projeto, estrutura e objetivos
- **[02-PROGRESSO.md](Documentacao/02-PROGRESSO.md)** - Status atual do progresso da tradução
- **[03-CHECKLIST-GERAL.md](Documentacao/03-CHECKLIST-GERAL.md)** - Lista completa de todos os arquivos (972 total)
- **[04-PLANO-NIVEIS.md](Documentacao/04-PLANO-NIVEIS.md)** - Estratégia de 5 níveis de prioridade
- **[05-ETAPA-03.md](Documentacao/05-ETAPA-03.md)** - Detalhes da Etapa 03 atual
- **[06-REGRAS-TRADUCAO.md](Documentacao/06-REGRAS-TRADUCAO.md)** - Padrões de formatação e tradução conceitual
- **[07-GLOSSARIO.md](Documentacao/07-GLOSSARIO.md)** - Glossário de termos técnicos Inglês ↔ Português
- **[08-MAPA-DEPENDENCIAS.md](Documentacao/08-MAPA-DEPENDENCIAS.md)** - Ordem lógica de leitura e dependências
- **[09-HISTORICO-ETAPAS.md](Documentacao/09-HISTORICO-ETAPAS.md)** - Histórico detalhado das etapas concluídas
- **[10-CHECKLIST-NIVEL-*.md](Documentacao/)** - Checklists divididas por nível de prioridade (5 arquivos)

> 💡 **Dica:** Comece pelo [01-VISÃO-GERAL.md](Documentacao/01-VISÃO-GERAL.md) para entender o projeto e consulte o [07-GLOSSARIO.md](Documentacao/07-GLOSSARIO.md) durante as traduções.

---

## Progresso da Etapa 03

### Estrutura de Níveis

O projeto foi dividido em **5 NÍVEIS** para gerenciamento eficiente do escopo:

| Nível | Descrição | Status | Arquivos |
|-------|-----------|--------|----------|
| 1 | Crítico - Fundação | ⏳ Iniciando | ~25 arquivos |
| 2 | Essencial - Sistemas Principais | 🔄 Em andamento | ~60 arquivos |
| 3 | Importante - Lógica Complexa | ⏸️ Aguardando | ~125 arquivos |
| 4 | Secundário - Ferramentas | ⏸️ Aguardando | ~175 arquivos |
| 5 | Complementar - Específico | ⏸️ Aguardando | ~200+ arquivos |

### Arquivos Traduzidos

#### Nível 1 - Crítico (Fundação)
- ✅ `src/conceito/vehicle_type.h.md` - Tipos fundamentais de veículos (367 linhas)
- ✅ `src/conceito/vehicle_base.h.md` - Classe base Vehicle (1271 linhas traduzidas)
- ✅ `src/conceito/station_type.h.md` - Tipos fundamentais de estações (585 linhas)
- ✅ `src/conceito/engine_type.h.md` - Tipos de motores/engines (612 linhas)

#### Nível 2 - Essencial
- ✅ `src/conceito/aircraft.h.md` - Base para Aeronaves (301 linhas)

### Próximos Arquivos (Nível 1.1 - Fundação)
1. ~~`vehicle_base.h`~~ ✅ CONCLUÍDO
2. ~~`vehicle.h`~~ ✅ vehicle_type.h CONCLUÍDO  
3. ~~`station.h`~~ ✅ station_type.h CONCLUÍDO
4. ~~`engine_type.h`~~ ✅ CONCLUÍDO
5. ~~`tile_type.h`~~ ✅ CONCLUÍDO (em vehicle_type.h)
6. `tilearea_type.h` - Tipos de área de tiles
7. `order_type.h` - Tipos de ordens/comandos
8. `cargo_type.h` - Tipos de carga

### Documentação de Apoio
- 📄 [`04-PLANO-NIVEIS.md`](Documentacao/04-PLANO-NIVEIS.md) - Plano mestre detalhado com estratégias, formatos e micro-etapas
- 📄 [`06-REGRAS-TRADUCAO.md`](Documentacao/06-REGRAS-TRADUCAO.md) - Padrões de tradução conceitual
- 📄 [`07-GLOSSARIO.md`](Documentacao/07-GLOSSARIO.md) - Glossário de termos técnicos

---

Veja a lista de status sobre a situação atual

*Última atualização: Junho 2024*
