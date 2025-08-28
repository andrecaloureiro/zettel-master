### a00

 - dados
	 - qualitativos
		 - nominal
		 - ordinal
	 - quantitativos
		 - discreto
		 - contínuo

- Dados: níveis de acesso 
	- públicos
	- internos 
	- restritos 
	- confidenciais

- Dados: estrutura
	- não estruturado
	- semi-estruturado
	- estrurado

- DAdos Abertos
	- inclusao, transparencia e responsabilidade
	- Decreto nº 8.777/2016
	- Brasil:
		- CGU
		- Infraestrutura Nacional de Dados Abertos (INDA)

- Dec 8777/2016 -INDA
	- Objetivos
	- Conceitos
		- Dado
		- Dado acessivel ao publico
		- abertos
		- formato aberto
		- plano de dados abertos
	- Principios ( OpenGovData/OCDE)
		- 1 - COMPLETUDE
		- 2 - PRIMARIEDADE
		- 3 -ATUALIDADE
		- 4 - ACESSIBILIDADE
		- 5 - PROCESSÁVEIS POR MÁQUINAS
		- 6 - ACESSO NÃO DISCRIMINATÓRIO
		- 7 - FORMATOS NÃO PROPRIETÁRIOS
		- 8 - LIVRES DE LICENÇAS -- acesso apenas para quem concluisse 

- piramide Data - Info - Knowlege - Wisdom
	- Dados
		- ERP
	- info = dado + contexto
		- Biz Intel
	- conhecimento = info + significado
		- Analise descritiva
	- wisdom = significado + aplicação
		- analise preditiva

- formatos
	- Númericos:  (int, float, real)
	- datas: (DATE , TIME)
	- string ( Char, Varchar, text)
	- unicode (Nchar, Nvarchar, ntext)
	- binarios: ( binary , varbinary)


- Banco de dados
	- esquemas
	- CRUD - operações basicas
		- Create
		- read
		- Update
		- Delete
	- Tipos
		- relacionais
		- dimensionais
		- NoSQL
		- Orient a obj
	- Caracteristicas
		- Natureza de autodescrição 
		- Abstração de dados 
		- Suporte a múltiplas visões 
		- Suporte a múltiplas transações
	- Acid - transações
		- Atomicidade, 
		- Consistência, 
		- Isolamento 
		- Durabilidade
	- Metadados - dados sobre os dados
		- estruturais - deficnicoes e relações
		- descritivos - index de dados - recuperação e ident dos dados
		- administrativos - integridade e segurança

- Arquitetura ANSI/SPARC - 3 niveis independentes
	- Externo - visao do usuario --> modelo conceitual
	- conceitual - estrtura sem SGBD especifico ---> modelo logico
	- Interno / visao Fisica - forma de armazenar os dados --> modelo fisico
	- ![[Pasted image 20241120213318.png]]

- Indices
	- ponteiros para local real de dados
	- uteis para grandes bases de dados - otimiza consultas
	- tipos
		- hash
		- arvore
		- clusterizado
		- balanceados
		- etc

- Visoes - view
	- representação virtual
	- dinamicas - processam a abse de dados em tempo real
	- materializada - estatica de u mmometno - necessita pedir atualização

- SGBD
	- principais no mercado
		- MYSQL
		- MS SQL Server
		- PostgreSQl
		- Oracle