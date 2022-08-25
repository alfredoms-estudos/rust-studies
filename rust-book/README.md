# Estudos relacionados ao livro The Rust Programming Language

Mais informações em https://doc.rust-lang.org/book/title-page.html.


## Anotações:

<br>

### **Capítulo 3** - *Common Programming Concepts* (*Conceitos Comuns de Programação*)

<br>

#### **Variáveis ​​e Mutabilidade**

Por padrão, as variáveis em **Rust** são imutáveis. Isso ocorre para que o código aproveite a segurança e o fácil uso da concorrência que o **Rust** oferece.

O código abaixo, por exemplo, não deve funcionar, pois vamos tentar alterar a variável **x**, que é mutável por padrão, para **6**:

```rust
    let x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
```

No entanto, é possível tornar as variáveis mutáveis com a palavra reservada **mut**:

```rust
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
```

No caso acima, o código deve executar normalmente.

<br>

**Constantes**

Constantes, diferente de variáveis, são SEMPRE imutáveis.

Em relação às variáveis, as constantes possuem algumas diferenças:

1. Você não pode usar **mut** ao declará-las;
2. Precisam ser SEMPRE tipadas;
3. Podem ser declaradas em qualquer escopo, inclusive no escopo global. Portanto, são úteis para valores compartilhados em muitas partes do código;
4. Podem ser declaradas somente com expressões que não vão ser alteradas em tempo de execução.

Exemplo:

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

> A convenção padrão do Rust para constantes é de somente palavras maiúsculas com *underscore* entre elas (como no exemplo acima).

<br>

**Shadowing**

**Rust** permite declarar a mesma variável no escopo corrente, fazendo com que a variável declarada antes seja *"ofuscada"* (**shadowed**) pela nova variável declarada. Assim, somente a nova variável declarada será acessível. Caso o **shadowing** seja feito em um outro escopo, ele só será válido naquele escopo.

Exemplo:

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

A saída do exemplo acima será:

```shell
The value of x in the inner scope is: 12
The value of x is: 6
```

<br>

#### **Tipos de dados**

<br> 

**Tipos Escalares**

Um **tipo escalar** representa um único valor. **Rust** tem quatro tipos escalares primários: inteiros, números de ponto flutuante, booleanos e caracteres.

<br>

**Tipos Inteiros**

Tabela de tipos inteiros em **Rust**:

| Length | Signed |	Unsigned |
|--------|--------|----------|
| 8-bit | i8 | u8 |
| 16-bit | i16 | u16 |
| 32-bit | i32 | u32 |
| 64-bit | i64 | u64 |
| 128-bit | i128 | u128 |
| arch | isize | usize |

Caso seja um literal que possa ser de diversos tipos, pode-se usar um sufixo como em `57u8` para designar o tipo. Números literais também podem usar `_` como um separador visual para torná-lo mais fácil de ler. `1_000`, por exemplo, tem o mesmo valor de `1000`. Abaixo, algumas possibilidades de escrita para inteiros literais:

| Number literals | Example |
|-----------------|---------|
| Decimal | 98_222 |
| Hex | 0xff |
| Octal | 0o77 |
| Binary | 0b1111_0000 |
| Byte (u8 only) | b'A' |

<br>

**Tipos de Ponto Flutuante**
