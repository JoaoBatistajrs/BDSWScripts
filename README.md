<h2>Scripts para a criação de um banco de dados para utilização da API do Star Wars</h2>

* Criação do Banco de Dados:
CRETE DATABASE EstrelaDaMorte;

* Criação da Tabela Planetas: 

CREATE TABLE Planetas(
	IdPlaneta int NOT NULL,
	Nome varchar (50) NOT NULL,
	Rotacao float NOT NULL,
	Orbita float NOT NULL,
	Diametro float NOT NULL,
	Clima varchar (50) NOT NULL,
	Populacao int NOT NULL
)
 
ALTER TABLE Planetas ADD CONSTRAINT PK_Planetas PRIMARY KEY (IdPlaneta);

* Criação da tabela Naves: 

CREATE TABLE Naves(
	IdNave int NOT NULL,
	Nome varchar (100) NOT NULL,
	Modelo varchar (150) NOT NULL,
	Passageiros int NOT NULL,
	Carga float NOT NULL,
	Classe varchar (100) NOT NULL
)

ALTER TABLE Naves ADD CONSTRAINT PK_Naves PRIMARY KEY (IdNave);

* Criação da tabela Pilotos: 

CREATE TABLE Pilotos(
	IdPiloto int NOT NULL,
	Nome varchar (200) NOT NULL,
	AnoNascimento varchar (10) NOT NULL,
	IdPlaneta int NOT NULL
)

GO

ALTER TABLE Pilotos ADD CONSTRAINT PK_Pilotos PRIMARY KEY (IdPiloto);

GO

ALTER TABLE Pilotos ADD CONSTRAINT FK_Pilotos_Planetas FOREING KEY (IdPlaneta)
REFERENCES Planetas (IdPlaneta)

* Criação da Tabela PilotosNaves: 

CREATE  TABLE PilotosNaves(
	IdPiloto int NOT NULL,	
	IdNave int NOT NULL,
	FlagAutorizado bit NOT NULL
)

GO

ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPiloto, IdNave)

GO

ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Pilotos FOREING KEY (IdPiloto)
REFERENCES Pilotos (IdPiloto)

GO

ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Naves FOREING KEY (IdNave)
REFERENCES Pilotos (IdNave)

GO

ALTER TABLE PilotosNaves ADD CONSTRAINT DF_PilotosNaves_FlagAutorizado DEFAULT (1) FOR FlagAutorizado

* Criação da tabela HistoricoViagens: 

CREATE TABLE HistoricoViagens(
	IdNave int NOT NULL,
	IdPiloto int NOT NULL,
	DtSaida datetime NOT NULL,
	DtChegada datetime Null
)

GO

ALTER TABLE HistoricoViagens ADD CONSTRAINT FK_HistoricoViagens_PilotosNaves FOREING KEY (IdNave, IdPiloto)
REFERENCES PilotosNaves (IdNave, IdPiloto)

GO

ALTER TABLE HistoricoViagens CHECK CONSTRAINT FK_HistoricoViagens_PilotosNaves
