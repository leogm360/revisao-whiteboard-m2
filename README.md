# REVISÃO WHITE BOARD M2

- SUMÁRIO
  - [SUMÁRIO](#sumário)
  - [ESCOPO DE BLOCO](#escopo-de-bloco)
  - [ESCOPO DE VARIÁVEL](#escopo-de-variável)
  - [OBJETOS](#objetos)
  - [THIS](#this)
  - [FORÇANDO O CONTEXTO THIS](#forçando-o-contexto-this)
  - [ABSTRAÇÃO, OBJETOS MODELO E INSTANCIAÇÃO (PROGRAMAÇÃO ORIENTADA A OBJETOS - POO)](#abstração-objetos-modelo-e-instanciação-programação-orientada-a-objetos---poo)
  - [ABSTRAÇÕES COM SUGAR SYNTAX (CLASS)](#abstrações-com-sugar-syntax-class)
  - [METODOS ACESSADORES (GET E SET)](#metodos-acessadores-get-e-set)
  - [HERANÇA](#herança)

## ESCOPO DE BLOCO

---

Uma boa parte das palvras chave da sintaxe do Javascript possuem um escopo de bloco bem definido (if...else, for, function, class, etc), ele normalmente é visivel e determinado através dos caracteres '{' e '}'. Eles abrem e fecham o escopo, respectivamente.

Exemplo:

```js
function minhaFuncao () {
    // -> escopo do bloco minhaFuncao

    for () {
        // -> escopo do bloco for

        if () {
            // -> escopo do bloco if

        } else {
            // -> escopo do bloco else
        }
    }
}
```

OBSERVAÇÃO: É IMPORTANTE NOTAR QUE OS ESCOPOS DE BLOCO PODEM SE LOCALIZAR UNS DENTRO DOS OUTROS, ISTO É O QUE SE CHAMA DE ANINHAMENTO. O ANINHAMENTO DEFINE A SEQUÊNCIA EM QUE UM CÓDIGO SERÁ EXECUTADO E TAMBÉM PODE DEFINIR QUESTÕES DE ACESSIBILIDADE DOS DADOS.

## ESCOPO DE VARIÁVEL

---

Diferente da definição anterior de escopo de bloco, o escopo de uma variável faz referencia ao "local" onde uma ou mais variáveis são acessíveis para escrita e/ou leitura.

Exemplo:

```js
function minhaFuncao() {
  var minhaVariavel1 = "um";

  for (let i = 0; i < 1; i++) {
    var minhaVariavel2 = "dois";

    let minhaVariavel3 = "três";

    const minhaVariavel4 = "quatro";

    console.log(minhaVariavel1); //'um'

    console.log(minhaVariavel2); //'dois'

    console.log(minhaVariavel3); //'três'

    console.log(minhaVariavel4); //'quatro'

    minhaVariavel3 = "seis";

    minhaVariavel4 = "sete"; //ERRO

    console.log(minhaVariavel3); //'seis'
  }

  minhaVariavel3 = "oito"; //ERRO

  minhaVariavel4 = "nove"; //ERRO

  console.log(minhaVariavel1); //'um'

  console.log(minhaVariavel2); //'dois'

  console.log(minhaVariavel3); //ERRO

  console.log(minhaVariavel4); //ERRO
}

console.log(minhaVariavel1); //ERRO

console.log(minhaVariavel2); //ERRO

console.log(minhaVariavel3); //ERRO

console.log(minhaVariavel4); //ERRO
```

OBSERVAÇÃO: AS VARIÁVEIS SÃO DECLARADAS ATRAVÉS DAS PALAVRAS CHAVE VAR, LET E CONST, PORÉM CADA UMA DELAS POSSUE UM FUNCIONAMENTO COM RELAÇÃO AO ESCOPO DE VARIÁVEL. ANTES DE DECIDIR QUAL USAR É NECESSÁRIO SE TER EM MENTE COMO O ESCOPO DELAS FUNCIONA E QUAL É A APLICAÇÃO QUE SERÁ DADA A VARIÁVEL.

## OBJETOS

---

Um objeto é uma forma inteligente e eficiente se estruturar e armazenar dados. Eles são construídos utilizando os caracteres de definição de escopo (i.e. { e }) e dentro de seu bloco são encontrados pares do tipo 'chave: valor'. Ao acessar estes objetos podemos interagir com estes pares e neste momento chamamos eles de propriedades.

Podemos acessar as propriedades de duas formas distintas, são elas: objeto['chave'] ou objeto.chave. Apesar de parecerem iguais, é importante notar que cada forma de acessar as propriedades de um objeto possuem suas limitações.

Exemplo:

```js
const objeto = {
  chave1: "valor1",
  chave2: "valor2",
  chave3: "valor3",
  chave4: "valor4",
  chave5: "valor5",
};

objeto["chave3"]; //'valor3';

//OU

objeto.chave3; //'valor3';
```

## THIS

---

O this é uma variável de contexto que armazena
a referência do objeto cujo escopo ela está
inserida. Ela é utilizada para chamá-lo no corpo do objeto e utilizar suas propriedades sem a necessidade de repetir o nome dele a todo momento.

Exemplo:

```js
const pessoa = {
  nome: "Márcia",
  nascimento: "17/08/1970",

  objeto1: () => {
    return this;
  },

  objeto2: function () {
    return this;
  },

  bio: function () {
    return ` Meu nome é ${this.nome} e nasci em ${this.nascimento}`;
  },
};

pessoa.objeto1(); //Window

pessoa.objeto2(); //pessoa

pessoa.bio(); //'Meu nome é Márcia e nasci em 17/08/1970'

console.log(this); //Window
```

OBSERVAÇÃO: ARROW FUNCTIONS NÃO DEFINEM
CONTEXTO, PORTANTO, COMO VISTO ACIMA, DENTRO DELAS O THIS SEMPRE FARÁ REFERÊNCIA AO OBJETO WINDOW.

## FORÇANDO O CONTEXTO THIS

---

Como visto acima os métodos (funções inseridas em objetos), ao definir um contexto, respeitam o objeto no qual estão inseridos. Isso pode inoportuno quando se quer utilizar outro objeto como this dentro de um método. Para isso existem três métodos, pertencentes ao objeto Function, que permitem forçar o contexto definido por uma função/método para um objeto específico.

Eles são o call, apply e bind. Todas as funções declaradas com a palavra chave function podem utilizar estes métodos.

Exemplo:

```js
const objeto1 = {
    metodo1: function () {
        return this;
    }
}

objeto1.metodo1() -> objeto1;

const objeto2 = {
    metodo2: function () {
        return 'Olá mundo!';
    }
}

const metodo1NovoContexto = objeto1.metodo1.bind(objeto2);

metodo1NovoContexto() //objeto2

metodo1NovoContexto().metodo2 //'Olá mundo!'
```

OBSERVAÇÃO1: COMO AS ARROW FUNCTIONS NÃO DEFINEM CONTEXTO, NÃO É POSSÍVEL FORÇAR UM CONTEXTO NELAS. NO CASO DE PRECISAR UTILIZAR UM CONTEXTO ESPECÍFICO É NECESSÁRIO USAR A PALAVRA CHAVE FUNCTION.

OBSERVAÇÃO2: CADA MÉTODO PARA FORÇAR CONTEXTO FUNCIONA DE UMA FORMA DIFERENTE. VERIFIQUE O FUNCIONAMENTO DELES NA DOCUMENTAÇÃO DA MDN.

## ABSTRAÇÃO, OBJETOS MODELO E INSTANCIAÇÃO (PROGRAMAÇÃO ORIENTADA A OBJETOS - POO)

---

Para muito além de armazenamento e estruturação de dados, os objetos são utilizados como modelos para a criação de diversas entidades identicas, porém com valores de propriedades diferentes.

O processo de extrair as propriedades de uma situação-problema, juntá-las e modelar um objeto é chamado de abstração.

As abstrações permitem criar várias entidades com propriedades identicas, mas que possuem valores distintos para as mesmas propriedades. Isso evita a necessidade de criar manualmente cada entidade e ter que lembrar quais propriedades devem ser definidas.

As entidades, por sua vez, são construções feitas a partir da abstração, porém são totalmente independentes umas das outras. Por este motivo, elas são chamadas de instâncias. Como dito, cada instância de um objeto é totalmente independente da outra e pode ser trabalhada de forma individual. Ao processo de criar uma nova instância de uma abstração é dado o nome de instânciação.

Portanto: realiza-se a ABSTRAÇÃO -> cria-se um OBJETO MODELO -> incia-se uma NOVA INSTÂNCIA que é totalmente independe do modelo e de suas irmãs -> INSTÂNCIAÇÃO.

Exemplo:

```js
/*
    Situação-problema: é necessário montar o perfil de uma pessoa que contenham informações identificadoras e pelo menos três formas de contato. Esse perfil, posteriormente, será utilizado para criar a base de dados de nossos professores.
*/

//ABSTRAÇÃO:

//Possíveis informações identificadoras:
// - nome completo;
// - data de nascimento;
// - RG com UF;
// - CPF;

//Possíveis formas de contato:
// - endereço completo;
// - e-mail;
// - telefone celular;

//Aqui se inicia a construção do objeto modelo com a sintaxe que achar mais conveniente:

function Perfil(
  nome,
  sobrenome,
  nascimento,
  rgComUF,
  cpf,
  endereco,
  email,
  celular
) {
  this.nome = nome;
  this.sobrenome = sobrenome;
  this.nascimento = nascimento;
  this.rgComUF = rgComUF;
  this.cpf = cpf;
  this.endereco = endereco;
  this.email = email;
  this.celular = celular;

  this.getBio = function () {
    return `Meu nome é ${this.nome} ${this.sobrenome} e nasci em ${this.nascimento}`;
  };
}

//Aqui instânciamos o objeto modelo, criando duas instâncias dele:
const perfil1 = new Perfil(
  "Marcia",
  "Gomes",
  "17/08/1970",
  "142589877 MG",
  "14532147898",
  "Rua do Pão de Queijo Nº 103",
  "marcia.gomes@gmail.com",
  "31 91111-1111"
);

const perfil2 = new Perfil(
  "Rafael",
  "Oliveira",
  "24/02/1985",
  "258459653 RJ",
  "45898775869",
  "Rua da Bala Perdida Nº71",
  "rafael.oliveira@protonmail.com",
  "21 98745-5632"
);

console.log(perfil1); //perfil1

console.log(perfil2); //perfil2

perfil1.getBio(); //Meu nome é Márcia Gomes e nasci em 17/08/1970

perfil2.getBio(); //Meu nome é Rafel Oliveira e nasci em 24/02/1985

//Ambos objetos instânciados acima são identicos no que se refere as propriedades contidas neles, porém o valor das mesmas propriedades são distintos em cada instância. Eles também são independes um do outro e do objeto modelo que os criou.
```

OBSERVAÇÃO1: A POO É UM DOS CHAMADOS PARADIGMAS DA PROGRAMAÇÃO E TENTA FORNECER UM PADRÃO DE TRABALHO PARA UMA APLICAÇÃO ESPECÍFICA. ELA NÃO SE LIMITA SÓ AO QUE ESTÁ ESCRITO ACIMA E O CONHECIMENTO SOBRE ELA PODE/DEVE SER APROFUNDADO SEMPRE QUE NECESSÁRIO.

OBSERVAÇÃO2: ALGUNS OUTROS PARADIGMAS DA PROGRAMAÇÃO SÃO PARADIGMA IMPERATIVO, PARADIGMA DECLARATIVO, PARADIGMA FUNCIONAL, PARADIGMA LÓGICO E PARADIGMA ORIENTADO A EVENTOS.

OBSERVAÇÃO3: O JAVASCRIPT É CONSIDERADO UMA LINGUAGEM MULTIPARADIGMA, POIS PERMITE O USO DE VÁRIOS DOS PARADIGMAS DESCRITOS ACIMA.

OBSERVAÇÃO4: A SINTAXE UTILIZADA ACIMA PARA CONSTRUIR O OBJETO MODELO É CHAMADA DE FUNÇÃO CONSTRUTORA. É POSSÍVEL UTILIZAR A SUGAR SYNTAX DE CLASSE PARA ESSA FINALIDADE, VEREMOS ELA A SEGUIR.

## ABSTRAÇÕES COM SUGAR SYNTAX (CLASS)

---

A chamada sugar syntax (sintaxe adicicada) é uma forma simplificada de escrever funções construtoras, ela é especialmente consistente na questão de herança que veremos mais abaixo.
Para utilizá-la temos a palavra chave classe e o método padrão constructor, eles são utilizados como abaixo:

Exemplo:

```js
class Perfil {
  constructor(
    nome,
    sobrenome,
    nascimento,
    rgComUF,
    cpf,
    endereco,
    email,
    celular
  ) {
    this.nome = nome;
    this.sobrenome = sobrenome;
    this.nascimento = nascimento;
    this.rgComUF = rgComUF;
    this.cpf = cpf;
    this.endereco = endereco;
    this.email = email;
    this.celular = celular;
  }

  getBio() {
    return `Meu nome é ${this.nome} ${this.sobrenome} e nasci em ${this.nascimento}`;
  }
}

const perfil1 = new Perfil(
  "Marcia",
  "Gomes",
  "17/08/1970",
  "142589877 MG",
  "14532147898",
  "Rua do Pão de Queijo Nº 103",
  "marcia.gomes@gmail.com",
  "31 91111-1111"
);

const perfil2 = new Perfil(
  "Rafael",
  "Oliveira",
  "24/02/1985",
  "258459653 RJ",
  "45898775869",
  "Rua da Bala Perdida Nº71",
  "rafael.oliveira@protonmail.com",
  "21 98745-5632"
);

console.log(perfil1); //perfil1

console.log(perfil2); //perfil2

perfil1.getBio(); //Meu nome é Márcia Gomes e nasci em 17/08/1970

perfil2.getBio(); //Meu nome é Rafel Oliveira e nasci em 24/02/1985
```

## METODOS ACESSADORES (GET E SET)

---

Os métodos acessadores get e set (também chamados de getters and setters) são um conjuto de métodos utilizados para retornar/modificar os valores das propriedades de um objeto. Na linguagem Javascript o seu uso NÃO É OBRIGATÓRIO, mas ele é considerado uma boa prática.

Apesar de não ter efeitos práticos para a segurança do código, é possível adicionar constraints (restrições) para o acesso e modificação do valor das propriedades. Isso permite evitar que os valores sejam acessados ou modificados sob condições indesejadas.

O método get NÃO LEVA NENHUM PARÂMETRO e sua função é apenas retornar algum valor. Já o método set LEVA APENAS UM PARÂMETRO e sua função é modificar alguma propriedade, sem retornar nada.

Exemplo:

```js
//Utilizando o exemplo acima:
class Perfil {
  constructor(
    nome,
    sobrenome,
    nascimento,
    rgComUF,
    cpf,
    endereco,
    email,
    celular
  ) {
    this.nome = nome;
    this.sobrenome = sobrenome;
    this.nascimento = nascimento;
    this.rgComUF = rgComUF;
    this.cpf = cpf;
    this._endereco = endereco;
    this.email = email;
    this.celular = celular;
  }

  get endereco() {
    if (typeof this._endereco !== "undefined") {
      return this._endereco;
    } else {
      return "Endereço não definido";
    }
  }

  set endereco(sentenca) {
    if (typeof sentenca === "string") {
      this._endereco = sentenca;
    }
  }

  getBio() {
    return `Meu nome é ${this.nome} ${this.sobrenome} e nasci em ${this.nascimento}`;
  }
}

const perfil1 = new Perfil(
  "Marcia",
  "Gomes",
  "17/08/1970",
  "142589877 MG",
  "14532147898",
  undefined,
  "marcia.gomes@gmail.com",
  "31 91111-1111"
);

perfil1.endereco; //'Endereço não definido'

perfil1.endereco = 1;

perfil1.endereco; //'Endereço não definido'

perfil1.endereco = "Rua do Pão de Queijo Nº 103";

perfil1.endereco; //'Rua do Pão de Queijo Nº 103'
```

OBSERVAÇÃO1: NOTE QUE SE RETIRAR O GET/SET ENDERECO, AINDA É POSSÍVEL ACESSAR OU ALTERAR A PROPRIEDADE. NO ENTANTO, COM OS MÉTODOS É POSSÍVEL COLOCAR RESTRIÇÕES PARA ESSAS OPERAÇÕES, COMO NO CASO DOS DESVIOS CONDICIONAIS ACIMA.

OBSERVAÇÃO2: NO EXEMPLO ACIMA UTILIZAMOS UM UNDERSCORE "\_" (SUBLINHADO) PARA NOMEAR A PROPRIEDADE ENDERECO. ISSO É NECESSÁRIO PARA EVITAR QUE A CHAMADA DO MÉTODO GET ENDERECO E A PROPRIEDADE ENDERECO ENTREM EM LOOP, ONDE UM REDIRECIONA PARA O OUTRO. NESTE PONTO QUALQUER CARACTERE PODERIA SER UTILIZADO NO LUGAR DO UNDERSCORE, PORÉM A CONVENÇÃO DE BOA PRÁTICA PARA ESTE CASO É A PREFERÊNCIA PELO USO DO UNDERSCORE.

OBSERVAÇÃO3: SEMPRE QUE A PROPRIEDADE PERFIL1.ENDERECO FOR CHAMADA, O MÉTODO GET ENDERECO SERÁ INVOCADO. SEMPRE QUE A PROPRIEDADE PERFIL1.ENDERECO = 'STRING' FOR CHAMADA, O MÉTODO SET ENDERECO SERÁ CHAMADO. O JAVASCRIPT FAZ ISSO DE FORMA AUTOMÁTICA, PORTANTO NÃO É NECESSÁRIO SE PREOCUPAR.

## HERANÇA

---

A herança é uma ferramenta extremamente poderosa presente em praticamente todas as linguagens de programação de [alto nível](https://kenzie.com.br/blog/linguagem-de-alto-nivel/). É através dela que fazemos com que objetos modelo filhos de um pai qualquer adquiram as propriedades e métodos definidos neste pai, tudo isso sem depender de reescrever os mesmos blocos de código.

Na maior parte das linguagens que utilizam a sintaxe de classe, fazer com que uma classe filha herde as propriedades de um pai qualquer é relativamente fácil. Já no Javascript a herança é feita, na pratica, através de uma prototipação, com uma sintaxe bem específica.

É aí que entra a sugar syntax de classes vista anteriormente, ela facilita bastante a herança de propriedades sem que seja necessário usar a complicada sintaxe de prototipação do Javascript. Com ela o próprio [interpretador Javascript](https://pt.wikipedia.org/wiki/Interpretador_de_JavaScript) se encarrega de configurar a prototipação de forma "automática" para que a herança seja realizada.

Exemplo 1 - Prototipação:

```js
//Definindo um construtor pai:
function Perfil(
  nome,
  sobrenome,
  nascimento,
  rgComUF,
  cpf,
  endereco,
  email,
  celular
) {
  this.nome = nome;
  this.sobrenome = sobrenome;
  this.nascimento = nascimento;
  this.rgComUF = rgComUF;
  this.cpf = cpf;
  this.endereco = endereco;
  this.email = email;
  this.celular = celular;
}

//Definindo um método prototipo para o pai:
Perfil.prototype.getBio = function () {
  return `Meu nome é ${this.nome} ${this.sobrenome} e nasci em ${this.nascimento}`;
};

//Criando um filho que herda o construtor do pai:
function Professor(
  nome,
  sobrenome,
  nascimento,
  rgComUF,
  cpf,
  endereco,
  email,
  celular,
  disciplina
) {
  Perfil.call(
    this,
    nome,
    sobrenome,
    nascimento,
    rgComUF,
    cpf,
    endereco,
    email,
    celular
  );

  this.disciplina = disciplina;
}

//Herdando os prototipos do pai:
Professor.prototype = Object.create(Perfil.prototype);

//Definindo o construtor do protipo da filha:
Professor.prototype.constructor = Professor;

//Sobrescrevendo o método prototipe do pai:
Professor.prototype.getBio = function () {
  return `Meu nome é ${this.nome} ${this.sobrenome} e nasci em ${this.nascimento}, sou professora e ministro a disciplina de ${this.disciplina}.`;
};

const perfil1 = new Perfil(
  "Marcia",
  "Gomes",
  "17/08/1970",
  "142589877 MG",
  "14532147898",
  "Rua do Pão de Queijo Nº 103",
  "marcia.gomes@gmail.com",
  "31 91111-1111"
);

const professor1 = new Professor(
  "Marcia",
  "Gomes",
  "17/08/1970",
  "142589877 MG",
  "14532147898",
  "Rua do Pão de Queijo Nº 103",
  "marcia.gomes@gmail.com",
  "31 91111-1111",
  "História"
);

console.log(perfil1); //perfil1

console.log(professor1); //professor1

perfil1.getBio(); //'Meu nome é Márcia Gomes e nasci em 17/08/1970.'

professor1.getBio(); //'Meu nome é Márcia Gomes e nasci em 17/08/1970, sou professora e ministro a disciplina de História.'
```

Exemplo 2 - Sugar Syntax de Classe:

```js
class Perfil {
  constructor(
    nome,
    sobrenome,
    nascimento,
    rgComUF,
    cpf,
    endereco,
    email,
    celular
  ) {
    this.nome = nome;
    this.sobrenome = sobrenome;
    this.nascimento = nascimento;
    this.rgComUF = rgComUF;
    this.cpf = cpf;
    this.endereco = endereco;
    this.email = email;
    this.celular = celular;
  }

  getBio() {
    return `Meu nome é ${this.nome} ${this.sobrenome} e nasci em ${this.nascimento}.`;
  }
}

class Professor extends Perfil {
  constructor(
    nome,
    sobrenome,
    nascimento,
    rgComUF,
    cpf,
    endereco,
    email,
    celular,
    disciplina
  ) {
    super(nome, sobrenome, nascimento, rgComUF, cpf, endereco, email, celular);

    this.disciplina = disciplina;
  }

  getBio() {
    return `Meu nome é ${this.nome} ${this.sobrenome} e nasci em ${this.nascimento}, sou professora e ministro a disciplina de ${this.disciplina}.`;
  }
}

const perfil1 = new Perfil(
  "Marcia",
  "Gomes",
  "17/08/1970",
  "142589877 MG",
  "14532147898",
  "Rua do Pão de Queijo Nº 103",
  "marcia.gomes@gmail.com",
  "31 91111-1111"
);

const professor1 = new Professor(
  "Marcia",
  "Gomes",
  "17/08/1970",
  "142589877 MG",
  "14532147898",
  "Rua do Pão de Queijo Nº 103",
  "marcia.gomes@gmail.com",
  "31 91111-1111",
  "História"
);

console.log(perfil1); //perfil1

console.log(professor1); //professor1

perfil1.getBio(); //'Meu nome é Márcia Gomes e nasci em 17/08/1970.'

professor1.getBio(); //'Meu nome é Márcia Gomes e nasci em 17/08/1970, sou professora e ministro a disciplina de História.'
```

OBSERCAÇÃO1: CONFORME VISTO ACIMA AMBOS OS EXEMPLOS DÃO O MESMO RESULTADO, PORÉM UM UTILIZA O MÉTODO ORIGINAL DO JAVASCRIPT (PROTOTIPAÇÃO) E O SEGUNDO UTILIZA A SINTAXE DE CLASSE (CLASS SUGAR SYNTAX). É POSSÍVEL PERCEBER A DIFERENÇA NA QUANTIDADE DE PASSOS NECESSÁRIOS PARA CONCLUIR A HERANÇA DE UMA E DA OUTRA FORMA, SENDO A FORMA ORIGINAL BEM MAIS COMPLEXA. ISSO É POSSÍVEL POIS O INTERPRETADOR DA LINGUAGEM JAVASCRIPT FAZ A PROTOTIPAÇÃO DE FORMA "AUTOMÁTICA" QUANDO USAMOS SINTAXE DE CLASSES.

OBSERVAÇÃO2: É POSSÍVEL VER QUE EM AMBOS OS CASOS ACIMA O MÉTODO GETBIO SOFRE UMA PEQUENA ALTERAÇÃO DA CLASSE PAI PARA A FILHA. ESSA ALTERAÇÃO É CHAMADA DE POLIMORFISMO, UMA CLASSE FILHA PODE OU NÃO SER POLIMÓRFICA DEPENDENDO DA NECESSIDADE DO DESENVOLVEDOR. PARA QUE ELE ACONTEÇA É NECESSÁRIO QUE O MÉTODO DA FILHA TENHA EXATAMENTE O MESMO NOME DA CLASSE PAI.
