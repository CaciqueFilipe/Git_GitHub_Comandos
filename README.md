# Curso de Git & Github


## --------- Sistema Git ---------------

<div align="center">
Version 1	Version 2	Version 3	Version 4	Version 5
   A		   A1		   A1		   A2		   A2
   B		   B		   B1		   B2		   B2
   C		   C1		   C1		   C1		   C2
</div>
   
### O sistema git trabalha com este modelo de versão acima, sendo:
	- Controle de versão e snapshots para guardar o que não foi mechido
	
## ---------- Instalando git -----------------

### Para baixar o git no computador:
  https://git-scm.com/downloads

#### Caso você use o linux, ele já vem instalado no computador.


## ------- Configurando o git ----------------

### O git guarda as configurações em 3 lugares:
 - O gitconfig do sistema como um todo,
 - O gitconfig do usuário,
 - O gitconfig do projeto específico daquele repositório.
 
### Configurar o usuario (global)

 #### Configurando o username:
 	git config --global user.name "Filipe Cacique"
 #### Configurando o username:
 	git config --global user.email "felipe.cacique@hotmail.com"
 
 #### Configurando o editor principal do git:
 	git config --global core.editor vscode


### Para saber qual usuario ou email:
	git config user.name
	git config user.email
	
### Para saber tudo:
	git config --list
	

## ------- Inicializando o Repositório ------------

### Criando pasta do projeto:
	mkdir git-course
	cd git-course
	
### Iniciando o git
	git init

#### Consultar se foi criado o .git (pasta de inicialização)
	ls -la

Se quiser você pode entrar no diretório do git com cd .git/ e ver seu conteudo.


## ----- Ciclo de Vida dos Estados dos arquivos -----------

 untracked	unmodified	modified	staged    
 
- untracked: acabou de ser adicionado ao git;
- unmodified: após ser adicionado ainda não foi modificado;
- modified: arquivo foi modificado;
- staged: arquivo pronto para ser comitado;
- Após o staged, feito o commit o arquivo volta a ser unmodified.

#### exemplo de vista do ciclo em um commit de arquivo readme.md

	git status
	- Arquivo ainda não tem nada;
	Criado Readme
	git status
	- git verifica existencia de arquivo e da status de untracked
	git add Readme.md
	git status
	- Verifica que arquivo esta pronto para o commit (staged)
	
	* Se o arquivo Readme for editado ele tem que ser adicionado novamente com git add
	* Se verificar o git status ele vai mostrar o arquivo para commit mas que ele tbm foi modificado.
	git commit -m "Add Readme"
	- Criando commit no git
	git status
	- Mostra que não tem nada a ser feito pq acabei de fazer commit
	

## ----- Vizualizando logs no git -----------


#### Este comando mostra o commit, seu autor, data 
	git log
	
#### Este comando mostra se houve branche, staches geradas, etc.
	git log --decorate 
	
#### Comando para ver os commits de determinado autor:
	git log --autor="Filipe Cacique"
	
#### Comando para ver os commits do autor(es) e suas quantidades de commits:
	git shortlog

#### Mostrando apenas a quantidade e a pessoa:
	git shortlog -sn
	
#### Mostra em forma gráfica o que acontece com os branches e as versões:
	git log --graph
	
#### Mostra as alterações do commit especifico:
	git show "serial do commit"
	
## ----- Vizualizando as diferenças de versões -----------

#### Mostra as diferenças feitas:
	git diff

#### Mostra o nome do arquivo editado:
	git diff --name-only
	
#### Quando o arquivo ja existe usa-se:
	git commit -am "Edit Readme"
	
	
## ----- Desfazendo coisas com o reset -----------


#### Após edição se eu vi que fiz algo errado no arquivo, ex:
	git status (Arquivo em estado modified)
	git diff (Vi as diferenças e o erro que cometi)
	git checkout nome_arquivo
	git diff (nenhuma diferença)

#### Após adição do arquivo para commit:
	git add nome_arquivo
	git status (modified, area de staged)
	git diff (Não encontra diferença pq o arquivo já foi adicionado)
	git reset HEAD nome_arquivo (retira o arquivo da staged)
	git diff (Mostra as diferenças)	
	git checkout nome_arquivo (Tira todas as mudanças)


#### Após commit: (Subi algo errado e quero voltar)
	git commit -am "Subi errado"
	git log (Mostra o commit feito por mim, que identifiquei estar errado, preciso da hash dele)
	

	git reset --soft --mixed --hard (reset pode ser usado tres comandos para ele)
	
##### - soft: Retorna o commit mas o arquivo estara na staged prontinho para ser commitado de novo;
##### - mixed: Retorna o commit para antes do staged, para o modified;
##### - hard: Ignora todo o commit e mata as alterações feitas nele

	git reset --soft hash_commmit
	ou	
	git reset --mixed hash_commmit		
	ou	
	git reset --hard hash_commmit
	


## ----- Github -----------

 Rede social para compartilhar código e projetos.
 
#### Adicionando repositório remoto, ex:
	git remote add origin git@github.com:CaciqueFilipe/github.course.git

#### Verificar se existe repositório, ex:
	git remote
	
#### Verificar se existe repositório e tras mais informações, ex:
	git remote -v
	
#### Envia as alterações para o repositório que estou determinando:
	git push -u origin master

- Após este comando ele faz o envio para o repositório



## ----- Autenticação do usuário remoto ao servidor (SSH) -----------

#### Para gerar chave SSH (Cole o texto abaixo, substituindo o endereço de e-mail pelo seu GitHub)
	git push -u origin master$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"


## maiores informações: <a href="https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent"/>

#### Para vizualizar ssh nas pastas:
	cd ~/.ssh/
	ls
	cat id_rsa.pub (Se tiver o arquivo)

## ----- Subindo alteração para o github ----------------
#### Após commit realize o comando push:
 	git push origin master

## ----- Clonando repositório do github ----------------
#### Após achar o repositório que deseja clonar:
 	git clone git@github.com:usuario_git/nome_do_repositorio.git nome_clone_na_maquina
 	
OBS: o clone funciona para meus repositórios, dos outros melhor usar o fork;

## ----- Fork (Pegando outros projetos e fazendo cópia) ----------------
#### No github, o repositório que deseja contribuir, você clica em fork
	Depois consigo fazer modificações e mandar para o usuario do repositorio confirmar se quer as alterações ou não


## ---------- Branch -----------------------

#### O que é branch:
Ponteiro móvel que leva a um commit.
	Posso criar branches que apontam para mesmo lugar ou para diferentes:
	
#### Por que usar:
	###### Vantagens:
		- Poder modificar sem alterar o local principal(master)
		- Facilmente "desligável" (criar e apagar branches com facilidade)
		- Múltiplas pessoas trabalhando
		- Evita conflitos
		
#### Criando um branch:
	git checkout -b testing (Cria a branch e entra nela)
	git branch (mostra as branches existentes e com * indica qual vc esta)
	
#### Movendo entre branches:
	git branch (para ver as branchs no momento)
	git checkout testing (Move para o branch testing)
	git checkout master (Move para o branch master)
	
#### Deletando branch que não quero mais:
	git branch -D testing
	git branch (para confirmar deleção)


## ----------- Merge -----------------------
	#### Serve para unir os branches, criando um novo commit
	
#### Pros						Contras

- Operação não destrutiva			- Commit extra
						- Histórico poluído
						
#### Fazendo merge:
	git commit -m "Add foo" (Após primeiro commit)
	git checkout -b testing (Crio a branch testing)
	nano bar.txt (crio arquivo na branch)
	git add bar (adicionei o arquivo)
	git commit -m "Add bar" (comitei o novo arquivo)
	git log (Mostra o Add foo e o Add bar)
	git checkout master (Se for para a master )
	git log (Só possuo o Add foo)
	nano fiz.txt (Criei arquivo na master)
	git add fiz (Adicionei para comitar)
	git commit -m "Add fiz" (comitei arquivo)
	git log (Possuo o Add fiz e Add foo na master)
	git merge testing (Chamando o merge)  ESC, :wq para sair
	Depois mostra Merge mode by 'recursive' strategy.
	git log (Mostra o foo, bar e fiz)
	git log --graph (Mostra a arvore do merge em grafico)
	
	
## ------------- Rebase -----------------------
	#### Serve para unir os branches

#### move a branch para frente da master deixando linear

#### Pros						Contras

- Evita commits extras				- Perde a ordem cronológica
- Histórico linear					

#### Fazendo rebase:
	nano buzz.txt (Criando arquivo)
	git add buzz (Adicionado ao comit)
	git commit -m "Add buzz" (Criado commit)
	git log (Mostra o que continha + o novo commit buzz)
	git checkout -b rebase-branch (Crio novo branch)
	nano bla.txt (Criando novo arquivo na branch)
	git add bla (Adicionado ao commit)
	git commit -m "Add bla" (Commit do arquivo)
	git log (Mostra os commits que continha + buzz e bla)
	git log --graph (Mostra o gráfico linear)
	git checkout master (Vou para a master)
	git log (Não tenho o commit bla)
	nano seila.txt (Crio um novo arquivo)
	git add seila (Adicionado ao commit)
	git commit -m "Add seila" (Commit do arquivo)
	git log (Vejo os commits + buzz + seila)
	git rebase rebase-branch (Cria o rebase com a branch rebase-branch e coloca no topo da fila )
	git log (Vera o seila, bla, buzz e outros commits que continha)
	git log --graph (Mostra linear o grafico)


## OBS:
	Para casos de adição de nova feature no final é legal utilizar o merge, 
	Enquanto tiver trabalhando e adicionando novos commits com outros branches o legal é usar rebase.

## ------------- Arquivo Gitignore (.gitignore) -----------------------
	#### Serve para ignorar alguns arquivos do projeto que contenham senha, configurações protegidas, etc..
	Ele sobe o projeto mas com as pastas escondidas

#### Criando arquivo .gitignore:
	nano gitignore.txt
	Ex: *.json (Ignora tudo que tem .json) ESC, :wq para fechar
	git status (mostra o arquivo .gitignore)

##### OBS: No site <a href="https://github.com/github/gitignore"/> mostra os arquivos exemplo de .gitignore que posso usar no meu projeto


## ------------- Comandos importantes (caso necessário)-----------------------

#### Criando stash:
	Edito arquivo;
	git status (Mostra o modified)
	git stash (Guarda a modificação em stash)
	git status (Não mosta a modified)
	
	(Aqui faço outras branchs, commito e tal)
	
#### Pegando a stash:
	git stash apply (Traz a stash que tinha feito de volta)
	git diff (Mostra as diferenças que fiz)
	
#### Stash é util quando ainda não quero commitar e quero guardar num canto para depois mexer

#### Vendo lista de stash:	
	git stash list
	
#### Limpando a lista de stash:	
	git stash clear



## ------------- Criando alias (atalhos dos comandos) -----------------------

#### Ao invés de "git status" pq não "git s"
	git config --global alias.s status
	git s (Funciona normal igual o git status)


## ------------- Versionamento (Tags) -----------------------

#### Criando tag:
	git tag -a 1.0.0 -m "Readme finalizado"

#### Subindo tags:
	git push origin master --tags
	
#### Vendo listas de tags:
	git tag


## --------- Git revert (Sexta você errou commit e quer ir embora) ---------------

#### Revertendo commits com git revert:
	git log (Busco o hash do meu commit e copio ele)
	git revert hash_do_commit 
	git log (Mostra que reverteu)
	git show hash_do_commit (Apaga o que tinha feito, mas não some com commit anterior)
	
#### Pra que usar revert, qual sua utilidade:
	Estou trabalhando em uma grande feature e subi ela para produção e ela quebrou em produção, se desse um reset ia perder tudo que eu fiz e não quero isso. Quero trabalhar nisso depois e ver o que errei, ai dou git revert, revertendo minhas mudanças colocando o código anterior de novo que ai assim eu subo isso, mas depois se eu quiser eu posso dar um checkout no commit estragado para poder entender ele melhor, modificar e subir corrigido.


## --------- Apagando tags e branches remotas ---------------

#### Vendo as tags:
	git tag

#### Apagando a tag local:
	git tag -d 1.0.1
	git push origin master --tags (Ele mostra que apagou localmente, porem no repositorio do github ainda tem)
	
#### Apagando a tag no repositorio github:	
	git push origin :1.0.0
	git push origin :1.0.1
	
#### O mesmo vale para um branch:	
	git push origin :testing
