# Diagrama UML - Sistema de Heróis

Este repositório contém a modelagem UML em Markdown referente ao sistema de heróis.

---

## Classe `Person`

**Atributos:**

- `- name: String`
- `- surname: String`

---

## Classe `Hero`

**Herança:** `extends Person`

**Atributos:**

- `- nickname: String`
- `- energy: int`
- `- strength: int`
- `- speed: int`

**Associação:**

- Muitos para um com a classe `Team`

---

## Classe `Team`

**Associação:**

- `- heroes: List<Hero>` — relação um para muitos

---

## Classes Filhas de `Hero`

### Classe `Homelander`

**Herança:** `extends Hero`  
**Dependência:** `HeroCompoundV`

### Classe `Starlight`

**Herança:** `extends Hero`  
**Dependência:** `HeroCompoundV`

---

## Interface `BasicPower<T>`

**Métodos:**

- `+ activateDurability(T hero): void`
- `+ giveStrength(T hero): void`
- `+ maxSpeed(T hero): void`
- `+ fly(T hero): void`

---

## Interface `SpecialPower<T>`

**Métodos:**

- `+ usePower(T hero): void`

---

## Classe `HeroCompoundV`

**Implementa:**

- `BasicPower`
- `SpecialPower`

---

## Relacionamentos

### Herança:

- `Hero` herda de `Person`
- `Homelander` herda de `Hero`
- `Starlight` herda de `Hero`

### Associação:

- `Team` possui `0..* Hero` (`heroes`)

### Implementação:

- `HeroCompoundV` implementa `BasicPower`
- `HeroCompoundV` implementa `SpecialPower`

### Dependência:

- `Homelander` depende de `HeroCompoundV`
- `Starlight` depende de `HeroCompoundV`
