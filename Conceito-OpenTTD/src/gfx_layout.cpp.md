# 📄 src/gfx_layout.cpp - Tradução Conceitual

> **Nota:** Este é um documento conceitual em português do Brasil baseado no arquivo original `src/gfx_layout.cpp` do OpenTTD.
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

/** @file gfx_layout.cpp Handling of laying out text. */

#include "stdafx.h"
#include "gfx_layout.h"
#include "string_func.h"
#include "strings_func.h"
#include "zoom_func.h"
#include "debug.h"

#include "table/contro...
```

---

## 📋 Estrutura Principal

### Funções e Classes Identificadas:

class ICUParagraphLayout : public ParagraphLayouter {
class ICUVisualRun : public ParagraphLayouter::VisualRun {
ICUVisualRun(const icu::ParagraphLayout::VisualRun *vr) : vr(vr) { }
const Font *GetFont() const override          { return (const Font*)vr->getFont(); }
int GetGlyphCount() const override            { return vr->getGlyphCount(); }
const GlyphID *GetGlyphs() const override     { return vr->getGlyphs(); }
const float *GetPositions() const override    { return vr->getPositions(); }
int GetLeading() const override               { return vr->getLeading(); }
const int *GetGlyphToCharMap() const override { return vr->getGlyphToCharMap(); }
class ICULine : public std::vector<ICUVisualRun>, public ParagraphLayouter::Line {
for (int i = 0; i < l->countRuns(); i++) {
int GetLeading() const override { return l->getLeading(); }
int GetWidth() const override   { return l->getWidth(); }
int CountRuns() const override  { return l->countRuns(); }
const ParagraphLayouter::VisualRun &GetVisualRun(int run) const override { return this->at(run); }
void Reflow() override  { p->reflow(); }
return std::unique_ptr<const Line>(l == nullptr ? nullptr : new ICULine(l));
class ICUParagraphLayoutFactory {
class FallbackParagraphLayout : public ParagraphLayouter {
class FallbackVisualRun : public ParagraphLayouter::VisualRun {

---

## 🔍 Detalhes Conceituais

### Documentação Extraída do Código Original:

/** @file gfx_layout.cpp Handling of laying out text. */
/** Cache of ParagraphLayout lines. */
/** Cache of Font instances. */
/**
 * Construct a new font.
 * @param size   The font size to use for this font.
 * @param colour The colour to draw this font in.
 */
/**
 * Wrapper for doing layouts with ICU.
 */
	/** Visual run contains data about the bit of text with the same font. */
	/** A single line worth of VisualRuns. */
/**
 * Helper class to construct a new #ICUParagraphLayout.
 */
	/** Helper for GetLayouter, to get the right type. */
	/** Helper for GetLayouter, to get whether the layouter supports RTL. */
/*** Paragraph layout ***/
/**
 * Class handling the splitting of a paragraph of text into lines and
 * visual runs.
 *
 * One constructs this class with the text that needs to be split into
 * lines. Then nextLine is called with the maximum width until nullptr is
 * returned. Each nextLine call creates VisualRuns which contain the
 * length of text that are to be drawn with the same font. In other
 * words, the result of this class is a list of sub strings with their
 * font. The sub strings are then already fully laid out, and only
 * need actual drawing.
 *
 * The positions in a visual run are sequential pairs of X,Y of the
 * begin of each of the glyphs plus an extra pair to mark the end.
 *
 * @note This variant does not handle left-to-right properly. This
 *       is supported in the one ParagraphLayout coming from ICU.
 */
	/** Visual run contains data about the bit of text with the same font. */
	/** A single line worth of VisualRuns. */
/**
 * Helper class to construct a new #FallbackParagraphLayout.
 */
	/** Helper for GetLayouter, to get the right type. */
	/** Helper for GetLayouter, to get whether the layouter supports RTL. */
	/**
	 * Get the actual ParagraphLayout for the given buffer.
	 * @param buff The begin of the buffer.
	 * @param buff_end The location after the last element in the buffer.
	 * @param fontMapping THe mapping of the fonts.
	 * @return The ParagraphLayout instance.

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

- **Arquivo Original:** `src/gfx_layout.cpp`
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
