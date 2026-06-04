# Tradução Conceitual: viewport_func

## Descrição Original
Functions related to (drawing on) viewports. */

## Visão Geral
Este arquivo `viewport_func.h` contém 35 declarações de funções, 2 estruturas, 1 definições/macros relacionados ao sistema.

## Dependências (Includes)
- `gfx_type.h`
- `viewport_type.h`
- `window_type.h`
- `tile_map.h`
- `station_type.h`

## Funções Principais
- `SetSelectionRed`: Função relacionada à funcionalidade do sistema
- `DeleteWindowViewport`: Função relacionada à funcionalidade do sistema
- `InitializeWindowViewport`: Função relacionada à funcionalidade do sistema
- `UpdateViewportPosition`: Função relacionada à funcionalidade do sistema
- `MarkAllViewportsDirty`: Função relacionada à funcionalidade do sistema
- `DoZoomInOutWindow`: Função relacionada à funcionalidade do sistema
- `ZoomInOrOutToCursorWindow`: Função relacionada à funcionalidade do sistema
- `FixTitleGameZoom`: Função relacionada à funcionalidade do sistema
- `HandleZoomMessage`: Função relacionada à funcionalidade do sistema
- `OffsetGroundSprite`: Função relacionada à funcionalidade do sistema
- `DrawGroundSprite`: Função relacionada à funcionalidade do sistema
- `DrawGroundSpriteAt`: Função relacionada à funcionalidade do sistema
- `AddSortableSpriteToDraw`: Função relacionada à funcionalidade do sistema
- `AddChildSpriteScreen`: Função relacionada à funcionalidade do sistema
- `ViewportAddString`: Função relacionada à funcionalidade do sistema
- ... e mais 20 funções

## Estruturas de Dados
- `Station`: Estrutura para gerenciamento de dados
- `Town`: Estrutura para gerenciamento de dados

## Definições e Macros
- `VIEWPORT_FUNC_H`: Macro de definição

## Responsabilidades
- Gerenciar operações relacionadas ao sistema
- Fornecer interface para outros módulos
- Definir tipos e constantes utilizados pelo sistema

## Integração
Este arquivo se integra com outros componentes do OpenTTD através das funções e tipos exportados, permitindo a comunicação entre diferentes subsistemas do jogo.
