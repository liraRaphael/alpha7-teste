# Teste para Alpha 7

**Por:** *Raphael Lira*
**Data:** *09/10/2020*


## Perguntas:

1. Discorra sobre as principais características das seguintes Estruturas de Dados, e para quê são normalmente utilizadas:

a.	Pilhas
  > Estrutura de dados conhecida por empilhar(ou colocar por cima), onde o primeiro a entrar é o último a sair(FILO); seu uso, se dá muito em gerenciador de memória(nisso é como um erro *Stack Overflow*, ou *Estouro de pilha*), algoritmos de Browsers, telas para aplicativo em celulares, etc...

b.	Filas
  > Estrutura de dados conhecida por encaixar no final da lista(podendo ser inserido no início também), onde o primeiro a entrar é o primeiro a sair(FIFO); seu uso é comum por exemplo, em arquivos para ser impresso.

c.	Árvores
  > Estrutura de dados para tomada de decisão, tem como objetivo agilizar busca por elemento(diferindo-se de lista encadeada), havendo um elemento raiz, seu(s) respectivo(s) nó(s); como dito, seu objetivo é agilizar buscas, então podemos dizer que seu uso mais recorrente é em banco de dados(usando mais *Arvore B+*) na indexação, busca por elemento de número maior ou menor, etc...

2. O que são WebServices e por que podem ser utilizados como um bom método de Integração entre sistemas (EDI - Eletronic Data Interchange)?
  > O WebService é um programa que tem como objetivo a comunicação entre duas aplicações por meio de um protocolo de rede(como HTTP/HTTPS), onde se processam dados(implementam as regras de negócios), lendo, criado, atualizado e excluído informações. Geralmente, a comunicação é feita por linguagem de marcação, e mais popularmente por XML e JSON.
  >
  > Sua vantagem está em evitar ter que escrever códigos para aplicação cliente que já forem feitos, poupar em manutenção(já que será uma única aplicação para o processamento) e mantendo a segurança dó código do WebService, enquanto para o EDIs, só necessário fazer a integração de comunicação, ou seja, menos código a ser escrito.
  >

3. O que são Design Patterns?  Cite exemplos de alguns Design Patterns conhecidos.
  > Design Patterns são metodologia para padrões de projetos, que tem como objetivo a solução de problemas recorrente.
  >
  > Alguns dos mais conhecidos(e que já tive a oportunidade de usar) são: 
  >
  > Refatoração de código: É reescrever o código já existe, melhorando sua estrutura e deixando mais legível.
  >
  > Arquitetura de Projeto MVC: Esta metodologia serve para separar o que é *Model*(tudo pertencente ao banco de dados), *View*(tudo que for UI), *Controller*(responsável por controlar e usar os *Models* e *Views*).
  >
  > Abstracty Factory: Serve para padronizar objetos semelhantes ou relacionados.
  >
  > DAO: Responsável pela comunicação com o Banco de Dados.

4. Discorra sobre os seguintes conceitos relacionados à Orientação a Objetos:

a.	Herança
  > Relacionamento entre classes onde a classe filha(que estende ao pai), herdando tudo da classe pai.

b.	Polimorfismo
  > Polimorfismo é a sobrescrita de método de uma classe pai na classe filha.

c.	Acoplamento
  > Acoplamento é o quão interligado e dependente estão os componentes, sendo muito dependente *fortemente acoplado*, enquanto pouco dependente *fracamente acoplado*. Sempre deve ter por objetivo deixar o software *fracamente acoplado*, pois, quanto mais *fortemente acoplado*, mais difícil será a manutenção.

d.	Coesão
  > Coesão diz respeita a quantidade de responsabilidade que essa classe tem, dizemos que é *Alta Coesão*, quando tem apenas uma responsabilidade, e *Baixa Coesão* quando tem diversar. Sempre devemos manter uma *Alta coesão*, pois, ajuda na manutenção e na reutilização do código.
  >
  > Ex: Uma classe *Pneu* não deve ter Componentes de *Porta*

e.	Classe Abstrata
  > É uma classe não concreta, que não é instanciada, porém, é implementada por um classe filha, como objetivo de evitar a reescrita de código.


5. Explique os seguintes termos/conceitos relacionados a Bancos de Dados:


a.	Foreign Key (Chave Estrangeira)
  > Campo(s) de uma tabela que identifica(m) registro de outra tabela

b.	Primary Key (Chave Primária)
  > Campo(s) de uma tabela que identifica um registro

c.	View (Visões)
  > É uma estrutura que armazena um "select"(geralmente com JOINs) para facilitar a consulta ao banco de dados

d.	Stored Procedure (Procedimento Armazenado)
  > Semelhante a *funções* em programação, tem como objetivo realização de diversos comando de uma só vez

e.	Trigger (Gatilho)
  > É um recurso do banco de dados, realizado quando se faz alguma alteração (Insert, Update, Delete) podendo ser antes ou depois da execução. Nesse é realizado comandos já definido para aquela tabela e tarefa(novamente, com exceção do SELECT).


6. 

![Imagem fornecida no teste](https://raw.githubusercontent.com/liraRaphael/alpha7-teste/main/bd.jpg)

a.	Todos os itens vendidos no mês de Janeiro de 2012.

```
  SELECT 
    DISTINCT(NomeProduto)
  FROM 
    ItemVenda iv
  WHERE
    IDVenda IN (SELECT v.IDVenda FROM Venda v WHERE v.DataVenda BETWEEN '2012-01-01' AND '2012-01-31')
```

b.	A soma do Valor do Item multiplicado pela quantidade dos itens vendidos para o cliente ‘José’.

```
  SELECT 
    sum(Quantidade * ValorItem)
  FROM 
    ItemVenda iv
  WHERE
    IDVenda IN (SELECT v.IDVenda FROM Venda v WHERE v.NomeCliente = "José")
```

c.	A contagem de todos os itens vendidos por cliente.

```
  SELECT 
    NomeCliente,
    sum(Quantidade) as QtdTotal
  FROM 
    Venda v INNER JOIN (SELECT Quantidade,IDVenda FROM ItemVenda iv) ivf
      ON v.IDVenda = ivf.IDVenda
  GROUP BY
    v.NomeCliente
```

d.	Soma das quantidades vendidas por produto, onde essa soma seja maior que 10.

```
  SELECT 
    ivf.NomeProduto,    
    ivf.QtdTotal
  FROM 
    (SELECT NomeProduto,sum(Quantidade) QtdTotal FROM ItemVenda iv GROUP BY NomeProduto) ivf
  WHERE
    ivf.QtdTotal > 10
```




