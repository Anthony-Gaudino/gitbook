## O Modelo de Objetos do Git ##

### O SHA ###

Todas as informa��es necess�rias para representar a hist�ria do projeto
s�o armazenados em arquivos referenciados por um "nome do objeto" de 40 
d�gitos que se parece com isso:
    
    6ff87c4664981e4397625791c8ea3bbb5f2279a3

Voc� ver� esses 40 d�gitos em todo lugar no Git.    
Em cada caso o nome � calculado baseado no valor hash SHA1 do conte�do do
objeto. O hash SHA1 � uma fun��o criptogr�fica.
O que isso significa para n�s � que isso � virtualmente imposs�vel encontrar
dois objetos diferentes com o mesmo nome. Isso tem in�meras vantagens; entre
outras:

- Git pode rapidamente determinar se dois objetos s�o id�nticos ou n�o, somente
  comparando os seus nomes.
- Desde que os nomes dos objetos sejam calculados da mesma forma em todo o 
  reposit�rio, o mesmo conte�do armazenado em dois reposit�rios sempre ser� 
  armazenado sobre o mesmo nome. 
- Git pode detectar erros quando l� um objeto, atrav�s da checagem do nome 
  do objeto que ainda � o hash SHA1 do seu conte�do.

### Os Objetos ###

Todo objeto consiste em 3 coisas - um **tipo**, um **tamanho** e **conte�do**.
O _tamanho_ � simplesmente o tamanho do conte�do, o conte�do depende do tipo
que o objeto �, e existem quatro tipos de objetos:
"blob", "tree", "commit", and "tag".

- Um **"blob"** � usado para armazenar dados do arquivo - � geralmente um 
  arquivo. 
- Um **"tree"** � basicamente como um diret�rio - ele referencia um conjunto
  de outras trees e/ou blobs (ex.: arquivos e sub diret�rios)
- Um **"commit"** aponta para uma simples �rvore, fazendo com que o projeto
  se pare�a em um determinado ponto no tempo. Ele cont�m meta informa��es
  sobre aquele ponto no tempo, como um timestamp, o autor das modifica��es
  desde o �ltimo commit, um ponteiro para um commit anterior, etc.
- Uma **"tag"** � uma forma de marcar um commit espec�fico de alguma forma 
  como especial. Ele � normalmente usado para identificar certos commits como
  vers�es ou revis�es espec�ficas ou alguma coisa junto a aquelas linhas.

Quase tudo do Git � construido atrav�s da manipula��o dessas simples estruturas
de quatro tipos de objetos diferentes. Eles s�o organizados dentro se seu 
pr�prio sistema de arquivos que est�o sobre o sistema de arquivos de sua 
m�quina. 

### Diferen�as do SVN ###

� importante notar que isso � muito diferente da maioria dos sistemas SCM com 
que voc� pode estar familiarizado. Subversion, CVS, Perforce, Mercurial e como
todos eles usam sistemas _Delta Storage_ - como eles armazenam as diferen�as 
entre um commit e o pr�ximo. Git n�o faz isso - ele armazena um snapshot de 
todos os arquivos de seu projeto como eram nessa estrutura de �rvore no momento
que faz um commit. Isso � um conceito muito importante quando est� usando Git.