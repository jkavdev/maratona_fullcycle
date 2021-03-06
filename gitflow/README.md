-- aplicar gitflow

-- configurar protecao de branchs

-- trabalhar com pull requests

-- code review ?!

-- SemVer - padronizar o versionamento do projeto

--CMDER WINDOWS TERMINAL
https://programmer.help/blogs/just-like-using-cmder-use-windows-terminal.html
https://zimmergren.net/using-third-party-terminals-within-windows-terminal/
	
	{
        "commandline": "cmd.exe /k \"C:/MyPrograms/DevTools/CMDs/Cmder/vendor/init.bat\"",
        "guid": "{b272da29-fe93-41b3-8194-fe87213db4a9}",
        "icon": "C:\\MyPrograms\\DevTools\\CMDs\\Cmder\\icons\\cmder.ico",
        "name": "Cmder",
        "startingDirectory" : "%USERPROFILE%"
    }

--GPG KEY
-- listando as chaves
	gpg --list-secret-key --keyid-form LONG

-- gerando uma chave
	gpg --full-generate-key	

-- exportando a chave criada
	gpg --armor --export D59E2F4522F9A5BF/ID_CHAVE | clip/pbcopy-copia_a_chave

-- configurando a chave criada com o usuario
	 git config user.signingkey D59E2F4522F9A5BF/ID_CHAVE	

-- assinando os commit
	git config commit.gpgsign true	 
	git config tag.gpgSign true

-- adicionando um segunda conta a chave gpg
	gpg --edit-key D59E2F4522F9A5BF
	-- adicionando a segunda conta
		adduid
	-- selecionando a conta
		uid 2
	-- tornando a conta confiavel
		trust
	-- salvando as alteracoes
		save

-- se subiu algum commit nao assinado
	https://webdevstudios.com/2020/05/26/retroactively-sign-git-commits/		

-- como selecionar uma conta da chave gpg		

--SSH KEY
https://stackoverflow.com/questions/16638092/copying-a-rsa-public-key-to-clipboard

-- gerando um chave ssh
	ssh-keygen

-- copiando a chave gerada
	cat ~/.ssh/id_rsa.pub - gera no console
	clip < ~/.ssh/id_rsa.pub - copia para a area de transferencia

--PULL REQUEST TEMPLATE	
-- configurar um template para os pull request, seguir os passos do link:
	https://embeddedartistry.com/blog/2017/08/04/a-github-pull-request-template-for-your-projects/

--SEMVER
-- aplicando a especificacao de versionamento do projeto
	https://semver.org/	

--CONVENTIONAL COMMITS
-- padronizando as mensagens dos commits	
	https://www.conventionalcommits.org/en/v1.0.0/

-- testando o commitlint
	echo fix: send cors headers' | npx commitlint

-- instalando o hook do husky que valida os commits
	 husky add C:/Users/jkavdev/repo/local/fullcycle/git/.husky/commit-msg "npx commitlint --edit $1"	
-- se o comando acima nao funcionar cria o arquivo com o comando dentro dele
	commit-msg -> 
		#!/bin/sh
		npx commitlint --edit $1

-- tentando o ultimo commit do projeto
	npx commitlint --from HEAD~1 --to HEAD --verbose		

--COMMITZEN
-- adicionando o commitzen para padronizar o commit, no momento do commit
	npm install -g commitizen

-- se a versao minor for incrementada, o valor do patch sera resetado para 0
-- se a versao major for incrementada, o valor do da minor e patch sera resetado para 0
-- quando comecar o projeto, indicado comecar com 0.1.0
-- quando o projeto for pra producao 1.0.0
-- quando acontecer uma depreciacao do uma funcionalidade, deve lancar uma versao minor com a depreciacao
	--- e depois uma versao major, removendo a funcionalidade depreciada, dando ao clientes tempo para a transicao	


--GIT
-- mudar para https ou ssh
	git remote set-url origin git@bitbucket.org:tutorials/tutorials.git	

-- ver apontamentos do repositorio
	git remote -v	

-- ver diferenca do arquivo
	git diff
-- ver a diferenca entre commit
	git diff sha1 sha2


--GIT FLOW
- LINKS
- https://stackoverflow.com/questions/13887454/git-flow-releasing-selected-features

- CONCEITOS
-- quando finalizando uma feature com apenas um commit, o git flow apenas realiza o fast forward na develop
	nao criando o commit de merge
-- mas quando a feature possui mais de um commit, o git flow realiza fast forward e no final cria o comando de merge da feature

--- podemos manter este comportamento, pois se precisarmos reverte uma feature com apenas um commit, como a feature tem apenas um commit
--- precisamos apenas reverter o commit em questao
--- se a feature possui varios commits, como o git flow criou o commit de merge, soh precisamos reverter o commit de merge

--- se uma feature nao deve subir para producao, entao ela nao deve ir para a develop
--- e se uma feature for impedida de subir para producao no ultimo momento, quando ja estiver dentro da release?
--- se formos jogar a develop na feature, pode ser que tenha alguma feature que nao deva sabir agora na release
--- mas todas as features na develop, nao quer dizer que ela ja eh candidata a subir na proxima release?

-- configurar a branch principal do repositorio develop, para que as operacoes sejam feitas nela, e nao na master
-- proteger develop e master, para certos grupo ou usuarios, restringir o acesso para alguns usuarios

-- implementar ferramenta para validar os commits que ja foram commitados - commitsar

=======

-- removendo todos os arquivos do staged
	git restore --staged .

-- inicializando uma feature
	git flow feature start nome_feature

-- finalizando uma feature
	git flow feature finish nome_feature