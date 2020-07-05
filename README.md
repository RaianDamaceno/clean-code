# clean-code


# Origem
As técnicas do Clean Code apareceram pela primeira vez no livro “Clean Code: A Handbook of Agile Software Craftsmanship”, lançado em 2008. Ele foi escrito por Robert Cecil Martin, conhecido na comunidade como Uncle Bob. O autor atua na área de desenvolvimento desde 1970 e é um dos profissionais por trás do Manifesto Ágil, lançado em 2001.
Com seus longos anos de experiência, ele conseguiu perceber que o gargalo principal no desenvolvimento de software estava justamente na manutenção. Ou seja, um código mal escrito desde a sua primeira versão pode funcionar, mas vai gerar prejuízos enormes.

# O que é?
Clean Code é uma filosofia de desenvolvimento cuja o principal objetivo é aplicar técnicas simples que visam facilitar a escrita e leitura de um código, tornando-o de fácil compreensão e revelando a sua real intenção.

# Por quê?
A produtividade de um programador está diretamente ligada a qualidade do código em que ele trabalha. Por isso, realizar a manutenção de um software é bem mais complicado do que desenvolver um do início. Os programadores passam a maior parte do tempo lendo e entendo o código do que programando. A proporção de leitura para escrita do código é de 10:1— Essa afirmação foi feita pelo Robert C. Martin ao analisar o histórico de atividades do seu próprio editor quando estava programando.
É impossível escrever um código sem lê-lo, constantemente lemos um código antigo quando estamos criando um. Por isso, escrever um código que facilite a leitura é de suma importância. Se você quiser ser um programador melhor e mais produtivo, não há como escapar, comece escrevendo um código mais limpo.


# EXEMPLOS

## Variaveis

Use nomes de variáveis significativos e pronunciáveis
### Errado:

```JAVA
String a = new SimpleDateFormat("YYYY/MM/DD").format(new Date());
```

### Certo:

```JAVA
String dataAtual = new SimpleDateFormat("YYYY/MM/DD").format(new Date());
```

## Use o mesmo vocabulario para o mesmo tipo de variavel

### Errado:
```JAVA
  getUsuarioInfo();
  getUsuarioRegistro();
  getCliente();
```

### Correto:
```JAVA
  getUsuario();
```

## Use nomes que possam ser consultados e lembrados

Este passo é muito importante pois o livro ressalta que passsamos mais tempo lendo código do que _codando_ e por isso devemos deixar de uma forma que para quem for ler não seja doloroso.

### Errado

```JAVA
  //O que significa o 5 ?
  
  boolean podeTerMaisDependentes(){
    return pessoa.dependentes.size() > 5
  }
  ```
### Correto
  ```JAVA
  boolean podeTerMaisDependentes(){
    int NUMERO_MAXIMO_DE_DEPENDENTES = 5; 
    return pessoa.dependentes.size() > NUMERO_MAXIMO_DE_DEPENDENTES
  }
  ```

## Evite ter que ficar lembrando o que cada coisa faz
Explicito é melhor que implicito

### Errado:
```JAVA
  String [] f = {"Maçã", "Pera", "Banana"}
  
  for (int i = 0; i < l.length; i++) {
    String fi = f[i];
    funcao1();
    funcao2();
    // ...
    // Chega uma hora que você esquece o que fi faz. 
    funcaoN(fi);
 }
```
### Correto

```JAVA
  String [] fruta = {"Maçã", "Pera", "Banana"}
  
  for (String fruta : frutas) {
    funcao1();
    funcao2();
    // ...
    // ...
    // ...
    funcaoN(fruta);
 }
```

## Não adicione o que não é necessário
Se o objeto ou a classe já te indicam algo, não é preciso repeti-los

### Errado:
```JAVA
  class Cachorro{
    public String cachorroNome;
    public String cachorroRaca;
    public String cachorroCor
    //...
  }
```
### Correto:
```JAVA
  class Cachorro{
    public String nome;
    public String raca;
    public String cor
    //...
  }
```

## Funções

## Funções com menos de dois argumento é o ideal

Um ou dois argumentos é o caso ideal, e três devem ser evitados (se possível). Qualquer coisa além disso deve ser consolidada. Normalmente, se você tiver mais de dois argumentos, sua função está tentando fazer muito.

Ter mais de três leva a uma explosão combinatória, na qual é necessário testar toneladas de casos diferentes com cada argumento separado.
Limitar a quantidade de parâmetros de função é muito importante, isso facilita o teste de sua função.
  

## Funções devem fazer somente uma coisa

Essa é de longe a regra mais importante na engenharia de software. Quando as funções fazem mais de uma coisa, são mais difíceis de compor, testar e raciocinar. 
Quando você isola uma função em apenas uma ação, elas podem ser refatoradas facilmente e seu código ficará muito mais limpo.

### Errado:
```JAVA
  public void enviarEmail(List<Usuario> usuarios) {
    for (Usuario usuario : usuarios) {
        String status = usuario.getStatus();
        int idade = usuario.getIdade();
        if (status == "ativo" && idade >= 18){
            email(usuario);
        }
    }
  }
```

### Certo:
```JAVA
  public void enviarEmail(List<Usuario> usuarios) {
    for (Usuario usuario : usuarios) {
        if (verificaUsuario(usuario)){
            email(usuario);
        }
    }
  }
  
  public boolean verificaUsuario(Usuario usuario){
    int IDADE_MINIMA = 18;
    String status = usuario.getStatus();
    int idade = usuario.getIdade();
    return status == "ativo" && idade >= IDADE_MINIMA;
  }
```

## O nome da funções devem dizer o que elas fazem
### Errado:

```JAVA
private void adicionar(Pessoa p1, Pessoa p2){
    //...
}
Pessoa p1 = new Pessoa();
Pessoa p2 = new Pessoa();
adicionar(p1, p2);
```
### Certo:

```JAVA
private void vincularDependente(Pessoa pessoa, Pessoa dependente){
    //...
}

Pessoa pessoa = new Pessoa();
Pessoa dependente = new Pessoa();
vincularDependente(pessoa, dependente);
```


## As funções devem ter apenas um nível de abstração
Quando você tem mais de um nível de abstração sua função geralmente está fazendo muito. A divisão de funções leva à reutilização e testes mais fáceis.

## Comentários
Apenas comente o que tiver um grau de complexidade envolvendo a regra de negócio ~e olhe lá~
Um bom codigo já é sua própria documentação.

### Errado:

```JAVA
  //Essa função soma dois números
  private somar(numero1, numero2){
  //Essa linha retorna a soma dos dois números
    return numero1 + numero2
  }
```
### Certo:
```JAVA
  private somar(numero1, numero2){
    return numero1 + numero2
  }
```

## Não use comentários quando você pode usar uma função ou uma variavel
O melhor comentário é não comentar

### Errado:

```JAVA
  // Verifica se o usuario pode ser cobrado
  if (usuario.status() == "ativo" && usuario.ultimoPagamento() < umMesAtras){
  //...
  }

```
### Correto:

```JAVA
  if(usuario.podeSerCobrado()){
  //...
  }
```

## Não deixe código legado comentado
Versionamento é o responsável por manter o histórico do seu código.

### Errado:
```JAVA
  funcao()
  //funcaoX()
  //funcaoY()
  //funcaoZ()
```
### Certo:

```JAVA
  funcao()
```
