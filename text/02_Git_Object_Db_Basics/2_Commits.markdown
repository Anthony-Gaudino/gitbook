### Objeto Commit ###

O objeto "commit" liga o estado f�sico de uma �rvore com a descri��o de como 
a conseguimos e porque.

[fig:object-commit]

Voc� pode usar a op��o --pretty=raw para linkgit:git-show[1] ou 
linkgit:git-log[1] para examinar seu commit favorito: 

    $ git show -s --pretty=raw 2be7fcb476
    commit 2be7fcb4764f2dbcee52635b91fedb1b3dcf7ab4
    tree fb3a8bdd0ceddd019615af4d57a53f43d8cee2bf
    parent 257a84d9d02e90447b149af58b271c19405edb6a
    author Dave Watson <dwatson@mimvista.com> 1187576872 -0400
    committer Junio C Hamano <gitster@pobox.com> 1187591163 -0700

        Fix misspelling of 'suppress' in docs

        Signed-off-by: Junio C Hamano <gitster@pobox.com>

Como voc� pode ver, um commit � definido por:

- uma **tree**: O nome SHA1 do objeto tree (como definido acima), representando
  o conte�do de um diret�rio em um certo ponto no tempo. 
- **parent(s)**: O nome SHA1 de algum n�mero de commits que representa 
  imediatamente o(s) passo(s) anterior(es) na hist�ria do projeto. O exemplo 
  acima possui um parent; commits gerados por um merge podem ter mais do que um. 
  Um commit sem nenhum parent � chamado de commit "root", e representa a 
  vers�o/revis�o inicial do projeto. Cada projeto deve possuir pelo menos um 
  root. Um projeto pode tamb�m ter m�ltiplos roots, mesmo assim n�o � comum
  (ou necessariamente uma boa id�ia).
- um **author**: O nome da pessoa respons�vel pela altera��o, junto com uma 
  data. 
- um **committer**: O nome da pessoa que de fato criou o commit, com a data
  que foi feita. Ele pode ser diferente do autor, por exemplo, se o autor 
  escreveu um patch e enviou-o para outra pessoa que usou o patch para criar o
  commit.  
- um **comment** descrevendo esse commit.

Note que um commit n�o cont�m qualquer informa��o sobre o que foi alterado;
todas as altera��es s�o calculadas pela compara��o dos conte�dos da tree
referenciada por esse commit com as trees associdadas com o seu parent.
De forma particular, o git n�o d� aten��o para arquivos renomeados 
explicitamente, embora possa identificar casos onde a exist�ncia do mesmo 
conte�do do arquivo na altera��o sugira a renomea��o. (Veja, por exemplo, a 
op��o -M para linkgit:git-diff[1]).  

Um commit � normalmente criado por linkgit:git-commit[1], que cria um commit no 
qual o parent � normalmente o HEAD atual, e do qual a tree � levada do conte�do
atualmente armazenado no index.

### O Modelo de Objeto ###

Ent�o, agora o que vimos os 3 pricipais tipos de objetos (blob, tree e commit),
vamos dar uma r�pida olhada em como eles todos se relacionam juntos.

Se tiv�ssemos um simples projeto com a seguinte estrutura de diret�rio:

    $>tree
    .
    |-- README
    `-- lib
        |-- inc
        |   `-- tricks.rb
        `-- mylib.rb

    2 directories, 3 files

E comitamos ele para um reposit�rio Git, seria representado assim:

[fig:objects-example]

Voc� pode ver que temos criado um objeto **tree** para cada diret�rio 
(incluindo o root) e um objeto **blob** para cada arquivo. Ent�o temos um 
objeto **commit** apontando para o root, ent�o podemos rastre�-lo at� o momento 
em que o nosso projeto se parecia quando foi commitado.