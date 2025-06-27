# Diagrama UML - Sistema Diário Oficial

## Classe `DiarioOficial`

### Atributos:

- `- data: Date`
- `- numero: int`
- `- titulo: String`

### Métodos:

- `+ imprimirDiario(): void`
- `+ addPublicacao(pub: Publicacao): void`
- `+ deletePublicacao(pub: Publicacao): void`

### Associações:

- Possui uma composição de 1 para 0..\* com a classe `Publicacao`.
- Possui uma associação de 1 para 1 com a enumeração `Esfera`.

---

## Classe `Publicacao` (Abstrata)

### Atributos:

- `- id: int`
- `- tituloPrincipal: String`
- `- tituloAuxiliar: String`
- `- conteudo: String`

### Métodos:

- `+ imprimirPublicacao(): void` _(Método Abstrato)_

### Associações:

- Possui uma agregação de 1 para 1..\* com a classe `Bloco`.
- Possui uma associação de \* para 1 com a classe `Orgao`.

---

## Classe `Bloco`

### Atributos:

- `- texto: String`
- `- ordem: int`

### Associações:

- Possui uma associação de \* para 1 com a enumeração `TipoBloco`.

---

## Classe `Orgao`

### Atributos:

- `- id: int`
- `- nomeOrg: String`

### Associações:

- Possui uma associação de \* para 1 com a enumeração `Poder`.

---

## Classes Filhas de `Publicacao`

### Classe `Legislacao`

**Herança:** `extends Publicacao`

#### Associações:

- Possui uma associação de \* para 1 com a enumeração `TipoLegislacao`.

#### Métodos:

- `+ imprimirPublicacao(): void`

---

### Classe `Corrigenda`

**Herança:** `extends Publicacao`

#### Atributos:

- `- ring: String`

#### Métodos:

- `+ imprimirPublicacao(): void`

---

### Classe `Licitacao`

**Herança:** `extends Publicacao`

#### Atributos:

- `- dataAberturaFase: int`
- `- dataEncerramentoFase: int`

#### Associações:

- Possui uma associação de \* para 1 com a enumeração `Fase`.
- Possui uma associação de \* para 1 com a enumeração `Modalidade`.
- Possui uma associação de \* para 1 com a enumeração `EscolhaVencedor`.

#### Métodos:

- `+ imprimirPublicacao(): void`

---

### Classe `Contrato`

**Herança:** `extends Publicacao`

#### Atributos:

- `- aditivos: List<Aditivos>`

#### Associações:

- Possui uma composição de 1 para 0..\* com a classe `Aditivos`.

#### Métodos:

- `+ imprimirPublicacao(): void`

---

## Classe `Aditivos`

### Atributos:

- `- id: int`

### Associações:

- Possui uma associação de \* para 1 com a enumeração `TipoAditivo`.

---

## Interface `Repository`

### Métodos:

- `+ salvar(obj: Object): void`
- `+ novo(obj: Object): void`
- `+ apagar(obj: Object): void`
- `+ buscar(): Object`

---

## Classes de Repositório

### Classe `DiarioOficialRepository`

- **Implementa:** `Repository`
- **Depende de:** `DiarioOficial`

### Classe `PublicacaoRepository`

- **Implementa:** `Repository`
- **Depende de:** `Publicacao`

---

## Enumerações

### Enum `Esfera`

- `<<enum constant>> Estadual: String`
- `<<enum constant>> Municipal: String`
- `<<enum constant>> Federal: String`

### Enum `Poder`

- `<<enum constant>> Executivo: String`
- `<<enum constant>> Legislativo: String`
- `<<enum constant>> Judiciario: String`
- `<<enum constant>> Ministerio Publico: String`

### Enum `TipoBloco`

- `<<enum constant>> texto: String`
- `<<enum constant>> imagem: String`
- `<<enum constant>> tabela: String`

### Enum `TipoLegislacao`

- `<<enum constant>> Leis Ordinarias: String`
- `<<enum constant>> Leis Complementares: String`
- `<<enum constant>> Leis Delegadas: String`
- `<<enum constant>> Medidas Provisorias: String`
- `<<enum constant>> Emendas Constitucionais: String`
- `<<enum constant>> Decretos Legislativos: String`
- `<<enum constant>> Resolucoes: String`
- `<<enum constant>> Portaria: String`

### Enum `Fase`

- `<<enum constant>> Edital: int`
- `<<enum constant>> Apresentacao: int`
- `<<enum constant>> Julgamento: int`
- `<<enum constant>> Habilitacao: int`
- `<<enum constant>> Homologacao: int`

### Enum `Modalidade`

- `<<enum constant>> Convite: String`
- `<<enum constant>> Tomada de Precos: String`
- `<<enum constant>> Concorrencia: String`
- `<<enum constant>> Pregao: String`
- `<<enum constant>> Dispensa de Licitacao: String`
- `<<enum constant>> Inexigibilidade: String`
- `<<enum constant>> Concurso: String`

### Enum `EscolhaVencedor`

- `<<enum constant>> Preco: int`
- `<<enum constant>> Tecnica: String`
- `<<enum constant>> Tecnica e Preco: String`

### Enum `TipoAditivo`

- `<<enum constant>> Valor: int`
- `<<enum constant>> Vigencia: int`
- `<<enum constant>> Outro: int`

---

## Resumo dos Relacionamentos

### Composição:

- `DiarioOficial (1)` contém `Publicacao (0..*)`
- `Contrato (1)` contém `Aditivos (0..*)`

### Agregação:

- `Publicacao (1)` agrupa `Bloco (1..*)`

### Associação:

- `DiarioOficial (1)` → `Esfera (1)`
- `Publicacao (*)` → `Orgao (1)`
- `Bloco (*)` → `TipoBloco (1)`
- `Orgao (*)` → `Poder (1)`
- `Legislacao (*)` → `TipoLegislacao (1)`
- `Licitacao (*)` → `Fase (1)`
- `Licitacao (*)` → `Modalidade (1)`
- `Licitacao (*)` → `EscolhaVencedor (1)`
- `Aditivos (*)` → `TipoAditivo (1)`

### Herança:

- `Legislacao`, `Corrigenda`, `Licitacao`, `Contrato` herdam de `Publicacao`

### Implementação:

- `DiarioOficialRepository` implementa `Repository`
- `PublicacaoRepository` implementa `Repository`

### Dependência:

- `DiarioOficialRepository` depende de `DiarioOficial`
- `PublicacaoRepository` depende de `Publicacao`
