#   Automação de Cadastros e Cotação de Fretes

##  Descrição do Projeto

Este projeto de automação foi desenvolvido para otimizar o processo de cadastro de novos clientes e cotação de fretes, eliminando tarefas manuais demoradas e propensas a erros. O robô extrai dados de uma planilha, consulta informações de CNPJ na Brasil API, realiza o cadastro no site RPA Challenge e faz cotações de frete nos sites dos Correios e Jadlog.

Com esta solução, observou-se uma redução substancial no tempo de processamento, a eliminação de erros e um aumento na escalabilidade para lidar com grandes volumes de dados.

##  Tecnologias Utilizadas

O robô foi desenvolvido utilizando as seguintes tecnologias:

* Python
* Selenium
* Pandas
* BotCity
* NumPy
* Requests
* Pillow
* Git
* Microsoft Teams
* GitHub
* Trello

##  Fluxo do Processo

O fluxo do processo de automação é o seguinte:

1.  **Planilha de Entrada:** O robô inicia lendo os dados de uma planilha de entrada (`Planilha de Entrada Grupos.xlsx` localizada em `Processar`).
2.  **Verificação de Registros Vazios:** O robô verifica se há campos vazios nos registros. Se houver, preenche a coluna `Status` na planilha de saída com a mensagem apropriada e segue para o próximo caso.
3.  **Requisição na Brasil API:** O robô consulta a Brasil API para obter informações do CNPJ, como razão social, nome fantasia, situação cadastral, endereço, etc.
4.  **Verificação de Situação Cadastral:** O robô verifica a situação cadastral do CNPJ. Se a situação for "Inativo", o robô preenche a coluna `Status` na planilha de saída com o motivo do erro. Se o e-mail estiver vazio, preenche com 'N/A'.
5.  **Cadastro no RPA Challenge:** O robô preenche os campos no site RPA Challenge com os dados obtidos da Brasil API.
6.  **Cotação nos Correios:** O robô acessa o site dos Correios, preenche as informações necessárias para a cotação do frete e captura o valor total e o prazo de entrega. Em caso de erro, preenche a coluna `Status` com "Erro ao realizar a cotação Correios".
7.  **Cotação na Jadlog:** O robô acessa o site da Jadlog, preenche as informações para a cotação e captura o valor total do frete. Em caso de erro, preenche a coluna `Status` com "Erro ao realizar a cotação Jadlog".
8.  **Comparação de Cotações:** O robô compara as cotações dos Correios e Jadlog e indica a mais barata.
9.  **Envio de E-mail:** O robô envia um e-mail de finalização da execução, contendo a planilha de saída como anexo.

##  Estrutura do Projeto

A estrutura do projeto é organizada nos seguintes diretórios e arquivos:

* `Cadastros_e_Fretes/`
    * `projeto_automacao_e_cadastro/`
        * `Emails/`
            * `E-mails para Notificações - RPA.xlsx`
        * `Processados/`
            * `placeholder.txt`
        * `Processar/`
            * `Planilha de Entrada Grupos.xlsx`
        * `resources/`
            * `start.png`
        * `Utils/`
            * `__init__.py`
            * `api_brasil.py`
            * `check_correios_variables.py`
            * `email_functions.py`
            * `functions_excel.py`
            * `helper_functions.py`
            * `IntegratedLogger.py`
            * `interact_correios.py`
            * `interactions_dataframe_correios.py`
            * `rpa_challenge.py`
            * `scriptProcessos.py`
    * `.env-example`
    * `bot.py`
    * `build.bat`
    * `build.ps1`
    * `build.sh`
    * `config.py`
    * `ProjetoFinalCompass.botproj`
    * `requirements.txt`
    * `.gitignore`

##  Detalhamento das Atividades do Robô

###   Acessar Planilha e Extrair Informações

O robô acessa a planilha de entrada localizada no diretório `Processar`. A planilha pode ser baixada manualmente do SharePoint e adicionada ao diretório local.

###   Buscar CNPJs na Brasil API

O robô utiliza a API do Brasil API para buscar informações detalhadas dos CNPJs, como razão social, nome fantasia, situação cadastral e endereço.

###   Preenchimento de Informações no RPA Challenge

O robô preenche um formulário no site RPA Challenge com as informações coletadas da Brasil API.

###   Realizar Cotação de Frete

* **Correios:** O robô acessa o site dos Correios e preenche o formulário de cotação com os dados da planilha de entrada.
* **Jadlog:** O robô acessa o site da Jadlog e preenche o formulário de cotação com os dados da planilha de entrada.

###   Planilha de Saída

O robô gera uma planilha de saída contendo todas as informações coletadas e os resultados das cotações de frete.

###   Logs de Execução e Monitoramento

O robô gera logs de execução para cada dia de processamento, armazenando informações sobre o status de cada tarefa executada.

###   Enviar E-mail de Finalização da Execução

O robô envia um e-mail para o cliente informando o final da execução, com a planilha de saída anexada.

###   Contingência/Fallbacks

Em caso de erros ou comportamentos não previstos, o robô realiza as seguintes ações:

* Tira um print da tela e armazena na pasta `Erros`.
* Adiciona informações de erro no arquivo de log.
* Notifica o erro via e-mail.

##  Requisitos de Sistemas e Componentes Lógicos

* **E-mail:** Caixa de e-mail para notificações e alertas.
* **RPA Challenge:** Sistema onde as informações dos novos clientes são preenchidas.
* **Brasil API:** Sistema utilizado para coletar dados do cliente.
* **Correios:** Sistema utilizado para realizar a cotação do frete.
* **Jadlog:** Sistema utilizado para realizar a cotação do frete.

##  Equipe

* [Bruno Guedes](https://github.com/b-guedes) - Desenvolvedor
* [Eduardo Kunzel](https://github.com/eduardo-kt) - Desenvolvedor
* [Luiz Felipe](https://github.com/felinjo) - Desenvolvedor
* [Marcos Ycaro](https://github.com/ycarotrindade) - Desenvolvedor
* [Tamirys Luamar](https://github.com/TamirysOliveira) - Desenvolvedora

##  Resultados

O robô demonstrou uma melhoria significativa na eficiência do processo. Enquanto uma pessoa leva em média 52 minutos para preencher 15 linhas da planilha de Excel, o robô executa a mesma tarefa em aproximadamente 5 minutos. Isso representa uma redução de mais de **10 vezes** no tempo de execução, permitindo que a equipe se concentre em atividades mais estratégicas.
