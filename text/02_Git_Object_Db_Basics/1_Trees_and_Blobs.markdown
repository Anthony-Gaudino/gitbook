### Objeto Blob ###

Um blob geralmente armazena o conte�do de um arquivo.

[fig:object-blob]

Voc� pode usar linkgit:git-show[1] para examinar o conte�do de qualquer blob.
Supondo que temos um SHA para um blob, podemos examinar seu conte�do assim:

    $ git show 6ff87c4664

     Note that the only valid version of the GPL as far as this project
     is concerned is _this_ particular version of the license (ie v2, not
     v2.2 or v3.x or whatever), unless explicitly otherwise stated.
    ...

Um objeto "blob" n�o � nada mais que um grande peda�o de dados bin�rios. Ele
n�o se referencia a nada ou possue atributos de qualquer tipo, nem mesmo um nome
de arquivo.  

Desde que o blob � inteiramente definido por esses dados, se dois arquivos em 
uma �rvore de diret�rio (ou dentro de m�ltiplas vers�es diferentes desse 
reposit�rio) possui o mesmo conte�do, eles ir�o compartilhar o mesmo objeto 
blob. O objeto � totalmente independente da localiza��o do arquivo na �rvore de 
diret�rio, e renomeando esse arquivo n�o muda o objeto com o qual est�  
associado.


### Objeto Tree ###

Um tree � um objeto simples que possui um conjunto de ponteiros para blobs e 
outras trees - ele geralmente representa o conte�do de um diret�rio ou sub 
diret�rio.

[fig:object-tree]

O sempre vers�til comando linkgit:git-show[1] pode tamb�m ser usado para 
examinar objetos tree, mas linkgit:git-ls-tree[1] dar� a voc� mais detalhes.
Supondo que temos um SHA para uma tree, podemos examinar ele assim:

    $ git ls-tree fb3a8bdd0ce
    100644 blob 63c918c667fa005ff12ad89437f2fdc80926e21c    .gitignore
    100644 blob 5529b198e8d14decbe4ad99db3f7fb632de0439d    .mailmap
    100644 blob 6ff87c4664981e4397625791c8ea3bbb5f2279a3    COPYING
    040000 tree 2fb783e477100ce076f6bf57e4a6f026013dc745    Documentation
    100755 blob 3c0032cec592a765692234f1cba47dfdcc3a9200    GIT-VERSION-GEN
    100644 blob 289b046a443c0647624607d471289b2c7dcd470b    INSTALL
    100644 blob 4eb463797adc693dc168b926b6932ff53f17d0b1    Makefile
    100644 blob 548142c327a6790ff8821d67c2ee1eff7a656b52    README
    ...

Como voc� pode ver, um objeto tree cont�m uma lista de entradas, cada uma com um 
modo de acesso, tipo, nome SHA1, e nome de arquivo, ordenado pelo nome de 
arquivo. Ele representa o conte�do de uma simples �rvore de diret�rio.

Um objeto referenciado por uma tree pode ser um blob, representando o conte�do
de um arquivo, ou outra tree, representando o conte�do de um sub diret�rio. 
Desde trees e blobs, como todos os outros objetos, s�o nomeados por um hash SHA1
de seus conte�dos, duas trees possui o mesmo hash SHA1 se somente se seus 
conte�dos (incluindo, recursivamente, o conte�do de todos os sub diret�rios) s�o
id�nticos.
Isso permite ao git determinar rapidamente as diferen�as entre dois objetos tree
,desde que ele possa ignorar qualquer entrada com nome de objetos id�nticos.  

(Nota: na presen�a de sub m�dulos, trees pode tamb�m ter commits como entradas. 
veja a se��o **Sub M�dulos**.)

Perceba que todos os arquivos possuem o modo de acesso 644 ou 755: git 
normalmente d� aten��o para o bit execut�vel. 
