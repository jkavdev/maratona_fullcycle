# CI - integracao continua

## principais processos

* testes
* linter
* qualidade codigo
* seguranca
* gerar artefatos pra deploy
* identificacao de versao por software
* gerar tags e releases

## criando arquivo de configuracao do ``github actions``

        # nome workflow
        name: ci-teste

        # especificando quando sera executado a acao
        on: 
        # no pull request
        pull_request:
        # especificando a branch que ira ser aplicado a action
            branches: 
            - develop

        # quais os passos a serem executados
        jobs:
        # especificando o passo a ser executado
        check-application:
            # escolhendo o ambiente da action
            runs-on: ubuntu-latest
            # escolhendo as acoes
            steps: 
            # acao de realizar o checkout do codigo no ambiente da action
            - uses: actions/checkout@v2
            # realiza a configuracao do ambiente GO
            - uses: actions/setup-go@v2
                with: 
                go-version: 1.15
            # rodando os testes
            - run : go test ./ci/app
            # rodando a aplicacao
            - run : go run ./ci/app/math.go