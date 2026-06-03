# 📄 src/currency.h - Tradução Conceitual

> **Nota:** Este é um documento conceitual em português do Brasil baseado no arquivo original `src/currency.h` do OpenTTD.
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

/** @file currency.h Functions to handle different currencies. */

#ifndef CURRENCY_H
#define CURRENCY_H

#include "date_type.h"
#include "string_func.h"
#include "strings_type.h"

static const int CF_NOEURO = 0; ///< ...
```

---

## 📋 Estrutura Principal

### Funções e Classes Identificadas:

static const int CF_NOEURO = 0; ///< Currency never switches to the Euro (as far as known).
struct CurrencySpec {
void CheckSwitchToEuro();
void ResetCurrencies(bool preserve_custom = true);

---

## 🔍 Detalhes Conceituais

### Documentação Extraída do Código Original:

/** @file currency.h Functions to handle different currencies. */
/**
 * This enum gives the currencies a unique id which must be maintained for
 * savegame compatibility and in order to refer to them quickly, especially
 * for referencing the custom one.
 */
/** Specification of a currency. */
	/**
	 * The currency symbol is represented by two possible values, prefix and suffix
	 * Usage of one or the other is determined by #symbol_pos.
	 * 0 = prefix
	 * 1 = suffix
	 * 2 = both : Special case only for custom currency.
	 *            It is not a spec from Newgrf,
	 *            rather a way to let users do what they want with custom currency
	 */

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

- **Arquivo Original:** `src/currency.h`
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
