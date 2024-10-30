## 1. Introdução

    Este projeto foi desenvolvido com o objetivo de extrair, processar e armazenar dados de CNPJs de empresas brasileiras a partir de APIs públicas ou privadas. Ele realiza a consulta de dados em diversas tabelas (Tabela1, Tabela2 e Tabela3), faz a limpeza e padronização dessas informações, e finalmente salva os dados em um banco de dados SQLite para fácil acesso e manipulação futura.

## 2. Requisitos do Sistema
    Para a correta execução do projeto, os seguintes requisitos são necessários:
        2.1. Softwares Necessários
            •	Python: 3.8 ou superior
            •	SQLite: versão 3.0 ou superior (integrado ao Python via sqlite3)
            •	Bibliotecas Python:
            o	aiohttp: para requisições assíncronas às APIs.
            o	pandas: para manipulação de dados em formato tabular.
            o	SQLAlchemy: para manipulação do banco de dados SQLite.
            o	plyer: para notificações de status durante a execução do programa.
        2.2. Sistema Operacional
        O código é compatível com os seguintes sistemas operacionais:
            •	Windows
            •	Linux
            •	macOS
## 3. Estrutura e Descrição do Código
        3.1. Arquitetura Geral
        O projeto foi desenvolvido em torno de três pilares principais:
            •  	Extração de Dados: utilização de APIs para coletar dados de CNPJs.
            •	Limpeza de Dados: padronização e tratamento dos dados brutos, removendo inconsistências.
            •	Salvamento de Dados: persistência dos dados em um banco de dados local (SQLite).
            A arquitetura é modular, com funções separadas para cada responsabilidade, permitindo fácil manutenção e escalabilidade.
        3.2. Extração de Dados
        As funções de extração são implementadas de forma assíncrona usando a biblioteca aiohttp, o que permite realizar várias requisições simultaneamente e otimizar o tempo de espera.
            Função Principal: fazer_requisicao()
            •	Objetivo: Faz a requisição aos endpoints das APIs e trata possíveis erros, como falhas de conexão e respostas incompletas.
            •	Parâmetros:
            o	url: URL da API a ser consultada.
            o	cnpj: CNPJ da empresa cujos dados serão buscados.
            o	sessao: sessão aiohttp para gerenciar conexões.
            •	Tratamento de Erros:
            o	Códigos de erro HTTP são capturados e exibidos no log.
            o	Requisições são reexecutadas em caso de falha no servidor.
        3.3. Limpeza e Tratamento de Dados
        Depois da extração, os dados são passados por um processo de limpeza. Isso inclui o preenchimento de valores nulos, padronização de strings e remoção de colunas desnecessárias.
            Função de Limpeza: limpar_dados()
            •	Objetivo: Limpa e padroniza os dados extraídos, garantindo que estejam em um formato consistente antes de serem armazenados.
            •	Principais Ações:
            o	Preenchimento de campos vazios com valores padrão.
            o	Remoção de colunas duplicadas ou desnecessárias.
            o	Conversão de tipos de dados para facilitar o armazenamento.
        3.4. Salvamento de Dados no Banco de Dados SQLite
        Os dados processados são salvos em um banco de dados SQLite, usando a biblioteca SQLAlchemy. Para cada CNPJ, são criadas três tabelas separadas que armazenam informações de diferentes aspectos.
            Função Principal: to_sql()
            •	Objetivo: Salva cada DataFrame (representando uma tabela) no banco de dados.
            •	Parâmetros:
            o	nome: nome da tabela no banco.
            o	cnpj: identificador da empresa.
            o	engine: conexão com o banco de dados SQLite.
        3.5. Execução Assíncrona
        A utilização de asyncio e aiohttp permite que múltiplas requisições sejam feitas em paralelo. Isso reduz significativamente o tempo de execução do programa, especialmente quando se lida com um grande volume de dados.
            •	Módulo Assíncrono: A função async def é usada para definir funções assíncronas que fazem as requisições de dados.
            •	await: Comando usado para esperar pela conclusão de cada requisição antes de prosseguir com o restante do processamento.
        3.6. Notificações de Status
        Durante a execução, notificações são enviadas usando a biblioteca plyer, que integra com o sistema operacional para exibir alertas. Isso auxilia no monitoramento do progresso do programa.
            Função de Notificação: alerta()
            •	Objetivo: Enviar uma notificação de sucesso ou erro ao usuário.
            •	Parâmetros:
            o	nivel: nível de severidade (erro ou sucesso).
            o	mensagem: texto descritivo da notificação.
            o	cnpj: CNPJ relacionado à notificação.
        3.7. Possíveis Melhorias e Considerações
            •	Otimização do Merge de Tabelas: A função de junção de tabelas foi inicialmente implementada, mas pode ser revisada para garantir melhor performance e consistência nos dados, especialmente quando se trata de grandes volumes.
            •	Adição de Logs: O sistema poderia ser aprimorado com logs mais detalhados, usando uma biblioteca como logging, para facilitar a depuração e monitoramento.
## 4. Instruções para Configuração e Execução
        4.1. Ambiente Virtual e Dependências
            1.	Criação do Ambiente Virtual:
            o	Navegue até o diretório do projeto e crie um ambiente virtual apropriado para garantir que as dependências não conflitem com outras instalações.
            2.	Instalação das Dependências: Após a criação e ativação do ambiente virtual, as dependências necessárias deverão ser instaladas conforme listadas no arquivo de requisitos.
        4.2. Execução do Código
            Com o ambiente devidamente configurado, o código pode ser executado diretamente a partir do terminal ou de um ambiente de desenvolvimento integrado. Durante a execução, os dados serão extraídos, limpos e salvos no banco de dados SQLite, além de notificações serem exibidas para acompanhamento do progresso.
## 5. Considerações Finais
    O projeto desenvolvido oferece uma solução eficiente para extração, limpeza e armazenamento de dados empresariais. Através da utilização de bibliotecas assíncronas, a performance do código é otimizada, enquanto o uso de pandas e SQLAlchemy permite um processamento robusto e confiável dos dados.
## 6. Referências
    •	Documentação das principais bibliotecas utilizadas no projeto, como aiohttp, pandas, SQLAlchemy e plyer, para referência futura.


