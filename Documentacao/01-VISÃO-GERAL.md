# 📖 Visão Geral do Projeto - Tradução Conceitual OpenTTD

## 🎯 Objetivo do Projeto

Este projeto tem como objetivo criar uma **tradução conceitual** completa do código-fonte do OpenTTD, um jogo de simulação de transporte de código aberto. Diferente de uma tradução literal, focamos em:

- **Compreensão dos conceitos**: Explicar o propósito e funcionamento de cada componente
- **Documentação em Português**: Tornar o código acessível para desenvolvedores lusófonos
- **Preservação técnica**: Manter a precisão técnica dos termos quando necessário

## 📁 Estrutura do Projeto

```
/workspace/
├── OpenTTD/                 # Código-fonte original (inglês)
├── Conceito-OpenTTD/        # Tradução conceitual (português)
└── Documentacao/            # Esta documentação
    ├── README.md
    ├── 01-VISÃO-GERAL.md
    ├── 02-PROGRESSO.md
    ├── 03-CHECKLIST-GERAL.md
    ├── 04-PLANO-NIVEIS.md
    ├── 05-ETAPA-03.md
    ├── 06-REGRAS-TRADUCAO.md
    ├── 07-GLOSSARIO.md
    ├── 08-MAPA-DEPENDENCIAS.md
    └── 09-HISTORICO-ETAPAS.md
```

## 🔍 O Que é Tradução Conceitual?

A tradução conceitual vai além da simples tradução de comentários. Ela inclui:

1. **Explicação de Propósito**: Por que este arquivo/classe/função existe?
2. **Contexto de Uso**: Como este componente se relaciona com outros?
3. **Padrões de Design**: Quais padrões de programação são utilizados?
4. **Terminologia Técnica**: Glossário consistente de termos técnicos

## 📊 Escopo do Projeto

### Quantidade de Arquivos
- **Total:** 972 arquivos para traduzir
- **Organizados por:** Diretórios do código-fonte original
- **Prioridade:** Divididos em 5 níveis de importância

### Categorias de Arquivos

| Categoria | Exemplos | Prioridade |
|-----------|----------|------------|
| Núcleo do Jogo | `vehicle_type.h`, `engine_type.h` | Nível 01 (Crítico) |
| Sistemas Principais | `airport.cpp`, `station.cpp` | Nível 02 (Essencial) |
| Interfaces | `gui.cpp`, `window.cpp` | Nível 03 (Importante) |
| Utilitários | `math.cpp`, `string.cpp` | Nível 04 (Secundário) |
| Suporte | `blitter/`, `sdl/` | Nível 05 (Complementar) |

## 🚀 Como Contribuir

1. **Leia a documentação**: Comece por este arquivo e [06-REGRAS-TRADUCAO.md](./06-REGRAS-TRADUCAO.md)
2. **Consulte o glossário**: Use [07-GLOSSARIO.md](./07-GLOSSARIO.md) para termos padronizados
3. **Escolha um arquivo**: Baseie-se nos checklists por nível de prioridade
4. **Siga o padrão**: Mantenha consistência com arquivos já traduzidos
5. **Revise**: Verifique se a tradução está clara e precisa

## 📈 Progresso Atual

- **Início do Projeto:** Junho 2024
- **Arquivos Traduzidos:** 10 de 972 (~1%)
- **Etapa Atual:** Consolidação da documentação e estrutura

## 🎓 Benefícios deste Projeto

- **Aprendizado**: Compreensão profunda da arquitetura do OpenTTD
- **Comunidade**: Acesso facilitado para desenvolvedores brasileiros/portugueses
- **Contribuição**: Possibilidade de contribuir com um projeto open-source relevante
- **Portfólio**: Demonstração de habilidades técnicas e de documentação

## 📞 Links Úteis

- [OpenTTD Oficial](https://www.openttd.org/)
- [Repositório GitHub](https://github.com/OpenTTD/OpenTTD)
- [Documentação do Projeto](./README.md)
- [Checklist Geral](./03-CHECKLIST-GERAL.md)

---

*Documento criado como parte da reorganização da documentação - Junho 2024*
