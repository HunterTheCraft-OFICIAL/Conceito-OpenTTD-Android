# 🚧 Status do Projeto: Tradução OpenTTD PT-BR

## ⚠️ AVISO IMPORTANTE: Leitura Obrigatória

**Atenção ao status dos arquivos:**

*   ✅ **CONCLUÍDO:** O arquivo foi totalmente traduzido, revisado e está pronto para uso como referência conceitual.
*   🚧 **EM ANDAMENTO:** O arquivo está sendo traduzido atualmente. Pode conter partes incompletas.
*   ⏳ **EM BREVE (PLACEHOLDER):** O arquivo **NÃO FOI TRADUZIDO**.
    *   Estes arquivos existem apenas como marcação de futuro trabalho.
    *   O conteúdo interno destes arquivos é apenas um esqueleto ou cópia da estrutura original sem a tradução conceitual aplicada.
    *   **Não utilize estes arquivos como fonte de verdade ainda.** Eles serão preenchidos sequencialmente conforme a evolução do projeto.

---

## 📋 Lista de Pendências por Classificação

O projeto segue uma estratégia de 5 Níveis de profundidade. Abaixo, o status atual de cada arquivo chave.

### Nível 1: Fundação (Tipos Básicos e Inicialização)
*A base de dados e tipos primitivos.*

| Arquivo Original | Status | Arquivo Conceito (.md) | Notas |
| :--- | :---: | :--- | :--- |
| `vehicle_type.h` | ✅ | `vehicle_type.h.md` | Tipos de veículos, IDs, constantes básicas. |
| `vehicle_base.h` | ✅ | `vehicle_base.h.md` | Estrutura principal `Vehicle`, caches e métodos. |
| `station_type.h` | ✅ | `station_type.h.md` | Tipos de estações, facilidades, áreas de captura. |
| `engine_type.h` | ✅ | `engine_type.h.md` | Definição de motores/engines e propriedades. |
| `tile_type.h` | ⏳ | `tile_type.h.md` | **EM BREVE** - Definições de Tiles. |
| `tilearea_type.h` | ⏳ | `tilearea_type.h.md` | **EM BREVE** - Áreas de tiles. |
| `cargo_type.h` | ⏳ | `cargo_type.h.md` | **EM BREVE** - Tipos de carga e classes. |
| `order_type.h` | ⏳ | `order_type.h.md` | **EM BREVE** - Tipos de ordens. |
| `order_base.h` | ⏳ | `order_base.h.md` | **EM BREVE** - Implementação de ordens. |
| `company_type.h` | ⏳ | `company_type.h.md` | **EM BREVE** - Dados das empresas/jogadores. |

### Nível 2: Sistemas Principais (Veículos e Movimento)
*Lógica de transporte, pathfinding e economia.*

| Arquivo Original | Status | Arquivo Conceito (.md) | Notas |
| :--- | :---: | :--- | :--- |
| `vehicle_func.h` | ⏳ | `vehicle_func.h.md` | **EM BREVE** - Funções auxiliares de veículos. |
| `train.h` | ⏳ | `train.h.md` | **EM BREVE** - Lógica específica de trens. |
| `roadveh.h` | ⏳ | `roadveh.h.md` | **EM BREVE** - Lógica de caminhões/ônibus. |
| `ship.h` | ⏳ | `ship.h.md` | **EM BREVE** - Lógica de navios. |
| `aircraft.h` | ⏳ | `aircraft.h.md` | **EM BREVE** - Lógica de aeronaves. |
| `pathfinder_type.h`| ⏳ | `pathfinder_type.h.md`| **EM BREVE** - Tipos de algoritmos de caminho. |
| `yapf/` (pasta) | ⏳ | `yapf/` (pasta) | **EM BREVE** - Pathfinding avançado (Yet Another PathFinder). |

### Nível 3: Infraestrutura e Mapa
*Construção, trilhos, estradas e sinais.*

| Arquivo Original | Status | Arquivo Conceito (.md) | Notas |
| :--- | :---: | :--- | :--- |
| `rail_type.h` | ⏳ | `rail_type.h.md` | **EM BREVE** - Tipos de trilhos. |
| `road_type.h` | ⏳ | `road_type.h.md` | **EM BREVE** - Tipos de estradas. |
| `signal_type.h` | ⏳ | `signal_type.h.md` | **EM BREVE** - Lógica de sinais. |
| `tunnelbridge_type.h`| ⏳ | `tunnelbridge_type.h.md`| **EM BREVE** - Túneis e pontes. |
| `waypoint_type.h` | ⏳ | `waypoint_type.h.md` | **EM BREVE** - Pontos de parada opcionais. |

### Nível 4: Interface e Interação (GUI)
*Como o jogador vê e interage com o jogo.*

| Arquivo Original | Status | Arquivo Conceito (.md) | Notas |
| :--- | :---: | :--- | :--- |
| `window_type.h` | ⏳ | `window_type.h.md` | **EM BREVE** - Sistema de janelas. |
| `widget_type.h` | ⏳ | `widget_type.h.md` | **EM BREVE** - Componentes de UI (botões, listas). |
| `gfx_type.h` | ⏳ | `gfx_type.h.md` | **EM BREVE** - Gráficos e sprites. |
| `strings_type.h` | ⏳ | `strings_type.h.md` | **EM BREVE** - Sistema de strings e localização. |

### Nível 5: Economia e Meta-Jogo
*Dinheiro, datas, cenários e configurações.*

| Arquivo Original | Status | Arquivo Conceito (.md) | Notas |
| :--- | :---: | :--- | :--- |
| `economy_type.h` | ⏳ | `economy_type.h.md` | **EM BREVE** - Dinheiro, custos, preços. |
| `date_type.h` | ⏳ | `date_type.h.md` | **EM BREVE** - Tempo, datas, ticks. |
| `settings_type.h` | ⏳ | `settings_type.h.md` | **EM BREVE** - Configurações do jogo. |
| `scenario_type.h` | ⏳ | `scenario_type.h.md` | **EM BREVE** - Cenários e objetivos. |

---

## 📜 Diretrizes de Tradução Atuais

Para garantir a consistência enquanto expandimos o projeto, seguimos estas regras estritas:

1.  **Tradução Conceitual, Não Literal:**
    *   O objetivo não é traduzir o código C++ linha por linha para português (o que quebraria a compilação), mas sim criar um documento `.md` que explique **o que** aquele código faz em português claro.
    *   Exemplo: Em vez de `void UpdatePosition()`, documentamos como "Atualiza a posição do veículo no mapa baseada na velocidade atual".

2.  **Manutenção da Estrutura:**
    *   A ordem das definições no arquivo `.md` deve espelhar a ordem no arquivo `.h` original. Isso facilita a comparação lado a lado (diff) entre o código fonte e a documentação.

3.  **Formato Markdown (.md):**
    *   Todos os arquivos de saída devem estar em `/workspace/Conceito-OpenTTD/src/conceito/`.
    *   Uso de blocos de código para trechos críticos, mas com comentários explicativos em PT-BR.

4.  **Fluxo de Trabalho (Um por Vez):**
    *   Para facilitar o versionamento (Git) e revisão, estamos gerando **um arquivo por vez**.
    *   Cada arquivo concluído é commitado individualmente antes de passar para o próximo.

5.  **Identificação de Pendências:**
    *   Qualquer arquivo criado que ainda não tenha recebido a tradução completa deve ter seu conteúdo substituído por um aviso claro de "EM BREVE" para evitar uso indevido.

---

## 🔄 Próximos Passos Imediatos

1.  Selecionar o próximo arquivo do **Nível 1** (ex: `tile_type.h` ou `cargo_type.h`).
2.  Realizar a tradução conceitual completa.
3.  Atualizar este arquivo `STATUS.md` movendo o item de "⏳ EM BREVE" para "✅ CONCLUÍDO".
4.  Commitar as mudanças.

*Última atualização: Agora*
