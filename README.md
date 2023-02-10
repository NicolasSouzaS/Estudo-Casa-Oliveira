# Estudo de caso
## Casa Oliveira

Roberto é dono de um mercado no bairro de Vargem Grande, na cidade de Tupã. Ele herdou o negócio de seu pai, Gumercindo Oliveira, ela foi aberta em 1978 na garagem da casa da família, era uma pequena quitanda. Com o passar dos anos o negócio cresceu e Gumercindo foi obrigado a ir para outro ponto maior e ali permaneceu até os dias atuais.


Roberto, que agora é o novo dono do mercado continuou o negócio seguindo da mesma forma que o pai. Ele comprava diretamente com os fornecedores grandes volumes de produtos e armazenava em seu estoque. As vezes ele comprava muitos produtos que ainda havia em estoque causando uma sobrecarga de produtos, ele também tinha muitos produtos estragados, tais como: frutas, legumes, iogurtes, leites, frango, etc. Também havia muitos produtos com o prazo de validade vencido.


Os funcionários eram poucos e faziam muitas coisas ao mesmo tempo. O açougueiro também ajudava no estoque, a moça da limpeza ajudava na organização dos produtos das prateleira, além de ajudar na padaria, quanto o caixa estava vazio o operador ajudava a repor os laticínios e a limpar a loja. O repositor também fazia operação no caixa.


Ao realizar a venda o Roberto, que sabia o nome de quase todos os clientes, anotava em um caderno todos os produtos que vendia e que havia em estoque. Ao fim do dia , Roberto pegava o caderno de fazia os cálculos de o quanto havia vendido, somando o faturamento e realizando a atualização do estoque. Isso é feito todos os dias e tomava um tempo considerável para que tudo tenha sido feito.


Roberto fechava a loja as 18h, mas só ia para casa as 22h, após fazer todas as operações necessárias. Mesmo assim o negócio vai bem e Roberto pretende ir para outro ponto e aumentar o volume de negócios e contratar novos funcionários.


Marica, esposa de Roberto, vem conversando com ele há muito tempo para que ele contrate uma empresa para construir um sistema de informática para gerenciar o negócio e reduzir o tempo que ele passa trabalhando e tenha maior organização dos produtos, maior lucratividade e melhorar a gestão.
Com a intenção de aumentar o negócio, Roberto está disposto a informatizar sua empresa. Vamos ajudá-lo. Iremos começar construindo o banco de dados.


### Problemas a solucionar
- Gerenciamento de estoque;
- Falta de funcionários;
- Funcionários ocupando funções diferentes;
- Fluxo de caixa. (Entrada | saída de valores);
- Baixa no estoque;
- Gestão do patrimônio (Computadores, prateleiras, geladeiras, fogões, carrinhos, caixas, balcões padaria e açougue, balanças, etc...
- Setor de compras;
- Setor financeiro;



- Gestão do Estoque
- Informações sobre os produtos (Validade, valor, lote, descrição, nome, descrição,        marca, categoria, fornecedor e ID do produto.).
- Volume de produtos em estoque (Quantidade atual dos produtos, quantidade por lote, ultima movimentação, quantidade máxima/mínima, ID do produto

- Funcionário
- Informações (Nome, função|cargo, salario, matricula, CPF, RG, Telefone, E-mail, estado civil, data de admissão, data de nascimento, endereço, usuário, senha, idfuncionario.)
- Fluxo de caixa
	(forma_pagamento, limite_sangria, valor, entrada|saída, registro_venda)

-Gestão de patrimônio
Informação_patrimonio(idpatrimonio, códigopatrimonio, descrição, valor, nome, setor_pertecente, data_aquisição, setor_responsavel, data_baixa)
- Setor de compras
Informação_compra(idcompra, valor_pago, funcionário, fornecedor, data_compra,numero_fiscal,nome_produto,descrição,quantidade,setor_destino)
-Setor financeiro
Informação_financeiro(idfinanceiro, despesas, lucro, disponibilidade_cofre ,valor, tipo_valor, descrição, data_operacao, idendentificação_responsavel)


### Modelo conceitual

!['Diagrama do modelo conceitual'](./ModelagemConceitual.png)


### Modelo lógico

!["Diagrama de modelo lógico de estoque"](./Modelo%20l%C3%B3gico.png)


---
### Modelo físico

#### Código e documentação do modelo físico 

/*
Para o projeto de banco de dados da casa Oliveira, será criado
uma estrutura físifca que com os comandos SQL(Structure Query Language
Iremos começar com o comando de criação de banco de dados. Este comando
pertence a categoria de comandos DDL(Data Definition Language)
Comando:
	CREATE DATABASE nome_do_banco -> CREATE DATABASE casaoliveira
*/

CREATE DATABASE casaoliveira;
/*
Após a criação do banco de dados, é necessário selecioná-lo. Para isso
iremos usar o comando "USE" nome_do_bancodedados
*/
USE casaoliveira;

/*
Criação das entidades em modo físico usando os comandos SQL.
Para criar uma tabela(entidade) usaremos o comando
CREATE TABLE nome_da_tabela seguido por parenteses e os 
atributos(campos) da tabela, bem como a sua tipificação, ou seja,
devemos dizer qual o tipo de dados que cada campo (atributo) da 
tabela deve-se receber. EX.: O campo idade deve reeber valores
numéricos e, portanto será definido como int(inteiro).

Vamos criar a tabela de produtos. Esta tabela possui os seguintes campos:
    -idproduto, descricao, fornecedor, validade, lote, preco, nome, marca, categoria
	
```
	Para cada campo será definido um tipo de dado
    para o idproduto, iremos definir como:
		- Chave-Primaria (Primary Key) é nosso campo indexador, por ele será
        realizado o relacionamento com outras tabelas
        - Vamos definir este campo com auto_incremente, o que permite gerar
        os ids de forma automática. Esse passo é importante, pois elimina alguns problemas,
        tais como: Concorroência, geração incrementada de valores e exclusividade
        de valores;
        - Vamos definir o campo com o tipo de dado numérico int(inteiro)
```

```
Para o campo descricao, usaremos o tipo de dado Text. Com este tipo, podemos inserir até
64mil caracteres. Como neste campo pode haver a possiblidade de uma descrição longa do produto,
se faz nescessário um tamanho maior. 
```

```
Para o campo fornecedor iremos usar o tipo de dado VARCHAR. Este tipo de dado nos permite
inserir textos, mas com um limite que pode ser pré definido pelo usuário ou podemos utilizar
o limite total de 255 caracteres. Para o fornecedor usaremos 50 caracteres.
```

```
Para o campo validade iremos usar o tipo de dado DATE. 
```

```
Para o campo lote será definido o tipo de dado VARCHAR, pois há a possibilidade de o valor conter
caracteres alfadecimais. Sendo assim, o VARCHAR é uma ótima opção por aceitar valores diversos.
```
```
O campo preco será definido como DECIMAL. Com este tipo é possível inserir valores númericos
com a aplicação de casas decimais. Você define o comprimento e deste tamanho é configurado as
casas decimais. Ex.: DECIMAL(10,2) -> COMPRIMENTO DE 10 DIGITOS E DESTES TEMOS 2 CASAS DECIMAIS
VEJA: R$ 11111111,11 -> 11.111.111,11
```
```
Para os campos nome, marca, categoria será definido o tipo de dado VARCHAR, pois este tipo
é capaz de receber caracteres de texto. Precisaremos apenas definir, o tamanho de cada campo.
Ex.: nome pode ficar com o tamanho 50, marca pode ser com 30 e categoria 20. 
```

*/

```
CREATE TABLE produto(
idproduto int auto_increment primary key,
descricao text,
fornecedor varchar(50),
validade date,
lote varchar(20),
preco decimal(8,2),
nome varchar(50),
marca varchar(30),
categoria varchar(20)
);
```


```
CREATE TABLE estoque(
idestoque int auto_increment primary key,
idproduto int,
quantidade_maxima int,
quantidade_minima int,
quantidade_atual int,
ultima_movimentacao date,
quantidade_lote int
);
```
