# Funções de Timer de Interface (GUI Timer)

## Visão Geral
Este arquivo define a classe `GUITimer`, um sistema de temporização para controle de eventos na interface gráfica do OpenTTD. É usado para gerenciar animações, atualizações periódicas de janelas e outros eventos baseados em tempo na UI.

## Classe GUITimer

### Propósito
Fornecer um mecanismo leve para controle de temporização de eventos na interface gráfica, permitindo que ações ocorram em intervalos específicos sem bloquear o loop principal do jogo.

### Membros Protegidos

#### timer
**Tipo:** `uint`

**Propósito:** Acumulador de tempo decorrido desde o último evento disparado.

**Comportamento:**
- Incrementa a cada chamada de `CountElapsed()` ou `Elapsed()`
- Resetado quando um intervalo completo é atingido
- Mantém o resto (módulo) do tempo não utilizado

#### interval
**Tipo:** `uint`

**Propósito:** Define o intervalo de tempo entre eventos consecutivos.

**Valores Especiais:**
- `0`: Timer desativado ou já disparou (dependendo do contexto)
- `>0`: Intervalo em unidades de tempo (tipicamente milissegundos ou ticks)

### Construtores

#### Construtor Padrão
```cpp
GUITimer()
```
**Inicialização:**
- `timer = 0`
- `interval = 0`
- **Uso:** Cria timer desativado, requer configuração posterior com `SetInterval()`

#### Construtor com Intervalo
```cpp
explicit GUITimer(uint interval)
```
**Parâmetros:**
- `interval`: Intervalo inicial em unidades de tempo

**Inicialização:**
- `timer = 0`
- `interval = valor fornecido`
- **Uso:** Cria timer já configurado para disparar após `interval` unidades de tempo

### Métodos Públicos

#### HasElapsed
**Assinatura:** `bool HasElapsed() const`

**Retorno:** `true` se o timer está desativado (interval == 0), `false` caso contrário

**Propósito:** Verifica rapidamente se o timer está inativo.

**Nota:** Não modifica estado interno, apenas consulta valor de `interval`.

#### SetInterval
**Assinatura:** `void SetInterval(uint interval)`

**Parâmetros:**
- `interval`: Novo valor de intervalo

**Efeitos:**
- `timer = 0` (reseta acumulador)
- `interval = novo valor`

**Casos de Uso:**
- Reiniciar timer após evento disparar
- Mudar dinâmica de temporização em runtime
- Desativar timer (passando 0)

#### CountElapsed
**Assinatura:** `uint CountElapsed(uint delta)`

**Parâmetros:**
- `delta`: Tempo decorrido desde última verificação

**Retorno:** Número de vezes que o intervalo foi completado neste período

**Algoritmo:**
1. Se `interval == 0`, retorna 0 (timer desativado)
2. Calcula divisões inteiras: `count = delta / interval`
3. Verifica se tempo restante + acumulador completa mais um intervalo
4. Atualiza acumulador com tempo residual
5. Retorna contagem total

**Caso de Uso Típico:** Animações que precisam de múltiplos frames por atualização
```cpp
// Exemplo: Animação que precisa de 3 updates por segundo
GUITimer animTimer(333); // 333ms por frame
uint frames = animTimer.CountElapsed(delta_time);
for (uint i = 0; i < frames; i++) {
    AdvanceAnimation();
}
```

#### Elapsed
**Assinatura:** `bool Elapsed(uint delta)`

**Parâmetros:**
- `delta`: Tempo decorrido desde última verificação

**Retorno:** `true` se pelo menos um intervalo completou, `false` caso contrário

**Efeitos Colaterais:**
- Se timer disparou, automaticamente desativa (`interval = 0`)
- Internamente usa `CountElapsed()` para cálculo

**Caso de Uso Típico:** Atualizações únicas de UI
```cpp
// Exemplo: Atualizar display a cada 500ms
GUITimer updateTimer(500);
if (updateTimer.Elapsed(delta_time)) {
    UpdateWindowDisplay();
    updateTimer.SetInterval(500); // Reativar para próximo ciclo
}
```

## Diferenças Entre CountElapsed e Elapsed

| Característica | CountElapsed | Elapsed |
|---------------|--------------|---------|
| **Retorno** | Contagem numérica | Booleano |
| **Auto-reset** | Não | Sim (desativa após disparo) |
| **Múltiplos eventos** | Suporta | Apenas um por vez |
| **Uso típico** | Animações | Atualizações únicas |

## Exemplos Práticos

### Animação Contínua
```cpp
class AnimatedWidget {
    GUITimer frameTimer;
    int currentFrame;
    
public:
    AnimatedWidget() : frameTimer(100) {} // 10fps
    
    void OnTick(uint delta) {
        uint frames = frameTimer.CountElapsed(delta);
        for (uint i = 0; i < frames; i++) {
            currentFrame = (currentFrame + 1) % totalFrames;
        }
    }
};
```

### Atualização Periódica de Janela
```cpp
class StatusWindow : public Window {
    GUITimer refreshTimer;
    
public:
    StatusWindow() : refreshTimer(1000) {} // Atualizar a cada 1s
    
    void OnRealTimeTick(uint delta) {
        if (refreshTimer.Elapsed(delta)) {
            RefreshStatusData();
            refreshTimer.SetInterval(1000); // Reagendar
        }
    }
};
```

### Controle de Blink/Flash
```cpp
class BlinkingText {
    GUITimer blinkTimer;
    bool visible;
    
public:
    BlinkingText() : blinkTimer(500), visible(true) {}
    
    void Update(uint delta) {
        if (blinkTimer.Elapsed(delta)) {
            visible = !visible; // Alternar visibilidade
            blinkTimer.SetInterval(500);
        }
    }
};
```

## Considerações de Performance

- **Leve:** Apenas dois inteiros como estado
- **Inline:** Todos métodos são inline para evitar overhead de chamada
- **Precisão:** Usa aritmética inteira, sem floating point
- **Thread-safe:** Assume uso single-threaded (típico para UI)

## Limitações

- Não suporta timers assimétricos (intervalos diferentes para on/off)
- Precisa de chamadas manuais com delta time
- Não integra automaticamente com loop de renderização
- Intervalo zero significa "desativado", não "disparar imediatamente"

## Integração com Sistema de Janelas

- Usado extensivamente em classes derivadas de `Window`
- Tipicamente chamado em `OnRealTimeTick()` ou `OnTick()`
- Permite atualizações assíncronas sem travar UI
- Complementa sistema de invalidação/redraw de janelas
