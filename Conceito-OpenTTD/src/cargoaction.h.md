# 📄 src/cargoaction.h - Tradução Conceitual

> **Nota:** Este é um documento conceitual em português do Brasil baseado no arquivo original `src/cargoaction.h` do OpenTTD.
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

/** @file cargoaction.h Actions to be applied to cargo packets. */

#ifndef CARGOACTION_H
#define CARGOACTION_H

#include "cargopacket.h"

/**
 * Abstract action of removing cargo from a vehicle or a station.
 * @tpara...
```

---

## 📋 Estrutura Principal

### Funções e Classes Identificadas:

class CargoRemoval {
uint Preprocess(CargoPacket *cp);
bool Postprocess(CargoPacket *cp, uint remove);
CargoRemoval(Tsource *source, uint max_move) : source(source), max_move(max_move) {}
uint MaxMove() { return this->max_move; }
bool operator()(CargoPacket *cp);
class CargoDelivery : public CargoRemoval<VehicleCargoList> {
bool operator()(CargoPacket *cp);
class CargoMovement {
CargoMovement(Tsource *source, Tdest *destination, uint max_move) : source(source), destination(dest
uint MaxMove() { return this->max_move; }
class CargoTransfer : public CargoMovement<VehicleCargoList, StationCargoList> {
bool operator()(CargoPacket *cp);
class CargoLoad : public CargoMovement<StationCargoList, VehicleCargoList> {
bool operator()(CargoPacket *cp);
class CargoReservation : public CargoLoad {
bool operator()(CargoPacket *cp);
class CargoReturn : public CargoMovement<VehicleCargoList, StationCargoList> {
bool operator()(CargoPacket *cp);
class CargoShift : public CargoMovement<VehicleCargoList, VehicleCargoList> {

---

## 🔍 Detalhes Conceituais

### Documentação Extraída do Código Original:

/** @file cargoaction.h Actions to be applied to cargo packets. */
/**
 * Abstract action of removing cargo from a vehicle or a station.
 * @tparam Tsource CargoList subclass to remove cargo from.
 */
	/**
	 * Returns how much more cargo can be removed with this action.
	 * @return Amount of cargo this action can still remove.
	 */
/** Action of final delivery of cargo. */
/**
 * Abstract action for moving cargo from one list to another.
 * @tparam Tsource CargoList subclass to remove cargo from.
 * @tparam Tdest CargoList subclass to add cargo to.
 */
	/**
	 * Returns how much more cargo can be moved with this action.
	 * @return Amount of cargo this action can still move.
	 */
/** Action of transferring cargo from a vehicle to a station. */
/** Action of loading cargo from a station onto a vehicle. */
/** Action of reserving cargo from a station to be loaded onto a vehicle. */
/** Action of returning previously reserved cargo from the vehicle to the station. */
/** Action of shifting cargo from one vehicle to another. */
/** Action of rerouting cargo between different cargo lists and/or next hops. */
/** Action of rerouting cargo in a station. */
/** Action of rerouting cargo staged for transfer in a vehicle. */

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

- **Arquivo Original:** `src/cargoaction.h`
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
