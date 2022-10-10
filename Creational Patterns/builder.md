O _Builder_ é um padrão arquitetural que permite a construção de objetos complexos de forma gradual. Este padrão permite que se desenvolva diferentes tipos e representações de um objeto usando o mesmo código de construtor.

# Proposta

Imagine um objeto complexo que requer uma trabalhosa inicialização de diversos campos e propriedades. Tal inicialização é comumente construida através de um monstruoso construtor com diversos parâmetros.

Por exemplo, vamos imaginar que gostariamos de construir um objeto do tipo `Casa`. Casa, como nós sabemos, possui diversas características: número de comodos, banheiros, quartos, garagem, portas, etc. Se durante uma implementação fosse necessário a construção de todo este objeto teriamos algo do tipo:

```
constructor (número de comodos, banheiros, quartos, garagem, portas, ...) {
    ...
}
```

Teriamos um construtor gigante. Além disso, dependendo das variações, algumas casas não tem garagem, não jardim, e isso levaria a propriedades no construtor a serem inutilizadas na classe. Algo assim:

```
constructor (número de comodos, banheiros, quartos, garagem, portas, = null, jardim = null, ...) {
    ...
}
```

Há algumas formas de resolver esses problemas:

- Criar classes especificas para cada tipo de objeto, mas naturalmente isso criaria uma serie de classes derivando do mesmo objeto. Além disso, possivelmente iria ter que duplicar código entre as classes.
- Colocar todos os parametros necessários em cada construtor de cada classe herdada. Porém isso feriria um dos principios SOLID de que, a cada mudança de requisito, a classe base precisaria ser mudada.

# Como resolver

O _Buider_ tenta resolver problemas como este. Este padrão propõe extrair a construção do objeto de dentro da classe base e os move para objetos separados chamados de _Builders_.
Como?

```
class BuilderObjectA {
    build() {
        return this;
    }

    buildDoors() {
        return this.doors();
    }

    buildRooms() {
        return this.rooms();
    }

    makeObjectA() {
        return new ObjectA();
    }
}
```

Para criar o objeto é necessário somente chamar os métodos que constroem as partes do objeto. Porém alguns métodos talvez precisem de implementação diferente. Dessa forma basta criar _Builders_ diferentes para diferentes tipos de objeto.
