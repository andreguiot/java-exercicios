# Diagrama UML - Avaliação de Java

---

## Classe `Engine`

**Métodos:**

- `+ main(args: String[]): void`
- `+ start(theStage: Stage): void`

**Dependência:**

- Utiliza as classes `Environment` e `Agent` para construir a cena.

---

## Classe `Environment`

**Atributos:**

- `- posX: int`
- `- posY: int`
- `- height: int`
- `- width: int`
- `- image: Image`
- `- gc: GraphicsContext`

**Composição:**

- `- protagonist: Protagonist`
- `- agents: List<Agent>`

---

## Classe Abstrata `Agent`

**Atributos:**

- `- posX: int`
- `- posY: int`
- `- height: int`
- `- width: int`
- `- speed: int`
- `- image: Image`

**Métodos:**

- `+ move(movements: List<String>): void`
- `+ chase(targetX: int, targetY: int): void`

---

## Classe `Protagonist`

**Herança:** `extends Agent`  
**Implementa:** `Power`  
**Composição:**

- `- bag: Bag`

---

## Classe `Enemy`

**Herança:** `extends Agent`  
**Composição:**

- `- weapon: Weapon`

---

## Interface `Power`

**Descrição:** Define o contrato para os poderes especiais.

**Métodos:**

- `+ superKick(): void`
- `+ megaPunch(): void`
- `+ fire(): void`

---

## Classe `Bag`

**Descrição:** Bolsa de itens do protagonista.

**Composição:**

- `- items: List<Item>`

---

## Classe `Weapon`

**Descrição:** Arma portada por um inimigo.

**Atributos sugeridos:**

- `- name: String`
- `- damage: int`

---

## Classe `Item`

**Descrição:** Item genérico guardado na bolsa.

**Atributos sugeridos:**

- `- name: String`
- `- description: String`

---

## Relacionamentos

### Herança:

- `Protagonist` herda de `Agent`
- `Enemy` herda de `Agent`

### Implementação:

- `Protagonist` implementa `Power`

### Composição:

- `Environment` possui `1..* Agent` (`agents`)
- `Environment` possui `1 Protagonist` (`protagonist`)
- `Protagonist` possui `1 Bag` (`bag`)
- `Enemy` possui `1 Weapon` (`weapon`)
- `Bag` possui `0..* Item` (`items`)

### Dependência:

- `Engine` depende de `Environment` e `Agent`
