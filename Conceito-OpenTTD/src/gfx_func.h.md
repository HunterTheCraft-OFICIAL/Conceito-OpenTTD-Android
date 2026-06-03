# 📄 src/gfx_func.h - Tradução Conceitual

> **Nota:** Este é um documento conceitual em português do Brasil baseado no arquivo original `src/gfx_func.h` do OpenTTD.
> 
> **Objetivo:** Explicar o propósito, estrutura e funcionalidades deste arquivo para falantes de português, sem ser uma tradução literal linha-por-linha.

---

## 🎯 Propósito do Arquivo

Este arquivo faz parte do núcleo do OpenTTD e contém implementações relacionadas a funcionalidades específicas do jogo. 

### Contexto Original (em inglês):
```cpp
/*
 * This file is part of OpenTTD.
 * OpenTTD is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, version 2.
 * OpenTTD is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
 * See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with OpenTTD. If not, see <http://www.gnu.org/licenses/>.
 */

/** @file gfx_func.h Functions related to the gfx engine. */

/**
 * @defgroup dirty Dirty
 *
 * Handles the repaint of some part of the screen.
 *
 * Some places in the code are called functions which makes something ...
```

---

## 📋 Estrutura Principal

### Funções e Classes Identificadas:

void GameLoop();
void CreateConsole();
extern bool _screen_disable_anim;   ///< Disable palette animation (important for 32bpp-anim blitter
void HandleToolbarHotkey(int hotkey);
void HandleKeypress(uint keycode, WChar key);
void HandleTextInput(const char *str, bool marked = false, const char *caret = nullptr, const char *
void HandleCtrlChanged();
void HandleMouseEvents();
void UpdateWindows();
void ChangeGameSpeed(bool enable_fast_forward);
void DrawMouseCursor();
void ScreenSizeChanged();
void GameSizeChanged();
bool AdjustGUIZoom(bool automatic);
void UndrawMouseCursor();
void RedrawScreenRect(int left, int top, int right, int bottom);
void GfxScroll(int left, int top, int width, int height, int xo, int yo);
Dimension GetSpriteSize(SpriteID sprid, Point *offset = nullptr, ZoomLevel zoom = ZOOM_LVL_GUI);
void DrawSpriteViewport(SpriteID img, PaletteID pal, int x, int y, const SubSprite *sub = nullptr);
void DrawSprite(SpriteID img, PaletteID pal, int x, int y, const SubSprite *sub = nullptr, ZoomLevel

---

## 🔍 Detalhes Conceituais

### Documentação Extraída do Código Original:

/** @file gfx_func.h Functions related to the gfx engine. */
/**
 * @defgroup dirty Dirty
 *
 * Handles the repaint of some part of the screen.
 *
 * Some places in the code are called functions which makes something "dirty".
 * This has nothing to do with making a Tile or Window darker or less visible.
 * This term comes from memory caching and is used to define an object must
 * be repaint. If some data of an object (like a Tile, Window, Vehicle, whatever)
 * are changed which are so extensive the object must be repaint its marked
 * as "dirty". The video driver repaint this object instead of the whole screen
 * (this is btw. also possible if needed). This is used to avoid a
 * flickering of the screen by the video driver constantly repainting it.
 *
 * This whole mechanism is controlled by an rectangle defined in #_invalid_rect. This
 * rectangle defines the area on the screen which must be repaint. If a new object
 * needs to be repainted this rectangle is extended to 'catch' the object on the
 * screen. At some point (which is normally uninteresting for patch writers) this
 * rectangle is send to the video drivers method
 * VideoDriver::MakeDirty and it is truncated back to an empty rectangle. At some
 * later point (which is uninteresting, too) the video driver
 * repaints all these saved rectangle instead of the whole screen and drop the
 * rectangle information. Then a new round begins by marking objects "dirty".
 *
 * @see VideoDriver::MakeDirty
 * @see _invalid_rect
 * @see _screen
 */
/** Size of the buffer used for drawing strings. */
/**
 * Determine where to draw a centred object inside a widget.
 * @param min The top or left coordinate.
 * @param max The bottom or right coordinate.
 * @param size The height or width of the object to draw.
 * @return Offset of where to start drawing the object.
 */
/** Height of characters in the small (#FS_SMALL) font. @note Some characters may be oversized. */
/** Height of characters in the normal (#FS_NORMAL) font. @note Some characters may be oversized. */
/** Height of characters in the large (#FS_LARGE) font. @note Some characters may be oversized. */
/** Height of characters in the large (#FS_MONO) font. @note Some characters may be oversized. */
/**
 * Return where to start drawing a centered object inside a widget.
 * @param top The top coordinate (or the left coordinate) of the widget.
 * @param height The height (or width) of the widget.
 * @param size The height (or width) of the object to draw.
 * @return The coordinate where to start drawing the centered object.
 */
/**
 * Returns fint/button size, rescaled to current screen resolution from the base Android resolution, which is 854x480

---

## 🇧🇷 Explicação em Português

[Esta seção será preenchida com a explicação detalhada em português sobre:
- O que este arquivo faz no contexto do jogo
- Como ele interage com outros sistemas
- Quais são suas responsabilidades principais
- Exemplos de uso e fluxo de execução]

---

## 🔗 Dependências e Relacionamentos

- **Arquivos que este arquivo importa:** [a ser mapeado]
- **Arquivos que importam este arquivo:** [a ser mapeado]
- **Sistemas relacionados:** [a ser identificado]

---

## 📝 Notas de Tradução

- **Arquivo Original:** `src/gfx_func.h`
- **Status:** ✅ Tradução conceitual inicial concluída
- **Versão OpenTTD:** Baseado em https://github.com/pelya/openttd-android
- **Data da Tradução:** [automático]

---

## ⏭️ Próximos Passos

1. [ ] Revisar e expandir a explicação conceitual em português
2. [ ] Mapear todas as dependências deste arquivo
3. [ ] Adicionar exemplos práticos de uso
4. [ ] Incluir diagramas de fluxo se aplicável
5. [ ] Revisão final por colaborador nativo em português

---

*Documento gerado como parte do projeto Conceito-OpenTTD - Tradução conceitual para a comunidade brasileira*
