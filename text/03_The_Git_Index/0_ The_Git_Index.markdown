## O Index do Git ##

O index do Git � usado como uma �rea de prepara��o entre o seu diret�rio de 
trabalho e o seu reposit�rio. Voc� pode usar o index para contruir um conjunto 
de modifica��es que voc� quer levar para o pr�ximo commit juntos. Quando voc� 
cria um commit, o que � commitado � o que est� no index atualmente, n�o o que 
est� no seu diret�rio de trabalho. 

### Visualizando o Index ###

A forma mais f�cil para ver o que est� no index � com o comando 
linkgit:git-status[1]. Quando voc� roda o git status, voc� pode ver quais
arquivos est�o preparados para o pr�ximo commit (atualmente no seu index), 
quais est�o modificados mas n�o ainda n�o preparados, e quais est�o 
completamente sem nenhuma prepara��o.

    $>git status
    # On branch master
    # Your branch is behind 'origin/master' by 11 commits, and can be fast-forwarded.
    #
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #	modified:   daemon.c
    #
    # Changed but not updated:
    #   (use "git add <file>..." to update what will be committed)
    #
    #	modified:   grep.c
    #	modified:   grep.h
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #	blametree
    #	blametree-init
    #	git-gui/git-citool

Se voc� descartar o index completamente, voc� em geral n�o perde qualquer 
informa��o contanto que voc� tenha o nome da tree que ele descreveu.

E com isso, voc� deveria ter um bom entendimento das coisas b�sicas que o Git 
faz por traz da cena, e porque ele � um pouco direfente da maioria dos outros
sistemas SCM. N�o se preocupe se voc� n�o entendeu completamente tudo at� 
agora; iremos revisar todos esses t�picos nas pr�ximas se��es. Agora estamos
prontos para ir a instala��o, configura��o e uso do Git.