# Criando um gerenciador de espaçonaves do star wars com SQL Server

#### O referido desafio está em incluir os scripts das tabelas no banco de dados SQL Server.



##### No primeiro passo, estamos criando a tabela Planetas e suas colunas, e seus valores não podem ser nulos. Segue abaixo:

CREATE TABLE Planetas(
IdPlaneta int NOT NULL,
Nome varchar(50) NOT NULL,
Rotacao float NOT NULL,
Orbita float NOT NULL,
Diametro float NOT NULL,
Clima varchar(50) NOT NULL,
Populacao int NOT NULL)



##### Logo adiante, estamos adicionando uma chave primária chamada de "PK_Planetas", referenciando a coluna IdPlaneta.

GO
ALTER TABLE Planetas ADD CONSTRAINT PK_Planetas PRIMARY KEY (IdPlaneta)

____

##### Em seguida, estaremos criando a tabela Planetas, e, mais uma vez, com valores que não podem ser nulos:

CREATE TABLE Pilotos(
IdPiloto int NOT NULL,
Nome varchar(200) NOT NULL,
AnoNascimento varchar(10) NOT NULL,
IdPlaneta int NOT NULL)



#####  Agora estaremos adicionando a chave primária "PK_Planets" e a estrangeira "FK_Pilotos_Planetas". Toda chave estrangeira deve referenciar a chave primária de outra tabela, informando sua coluna em parênteses.

GO
ALTER TABLE Pilotos ADD CONSTRAINT PK_Planets PRIMARY KEY (IdPiloto)
GO
ALTER TABLE Pilotos ADD CONSTRAINT FK_Pilotos_Planetas FOREIGN KEY (IdPlaneta)
REFERENCES Planetas (IdPlaneta);

____

##### Em seguida, estaremos criando a tabela PilotosNaves com valores que não podem ser nulos:

CREATE TABLE PilotosNaves(
IdPiloto int NOT NULL,
IdNave int NOT NULL,
FlagAutorizado bit NOT NULL)



##### Agora estaremos adicionando a chave primária "PK_PilotosNaves" e as chaves estrangeira "PK_PilotosNaves_Pilotos" e "PK_PilotosNaves_Naves" e o padrão Default de "FlagAutorizado".

GO
ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPiloto, IdNave);
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Pilotos FOREIGN KEY (IdPiloto)
REFERENCES Pilotos (IdPiloto)
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Naves FOREIGN KEY (IdNave)
REFERENCES Naves (IdNave)
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT DF_PilotosNaves_FlagAutorizado DEFAULT (1) FOR FlagAutorizado;

____

##### Por fim, estaremos criando a tabela para registrar histórico de viagens, chamada "HistoricoViagens":

CREATE TABLE HistoricoViagens(
IdPiloto int NOT NULL,
IdNave int NOT NULL,
DtSaida datetime NOT NULL,
DtChegada datetime NULL)

##### Estaremos incluindo a chave estrangeira "FK_HistoricoViagens_PilotosNaves" fazendo referência a tabela PilotosNaves e suas colunas "IdPiloto" e "IdNave".

GO
ALTER TABLE HistoricoViagens ADD CONSTRAINT FK_HistoricoViagens_PilotosNaves FOREIGN KEY (IdPiloto, IdNave)
REFERENCES PilotosNaves (IdPiloto, IdNave)
GO
ALTER TABLE HistoricoViagens CHECK CONSTRAINT FK_HistoricoViagens_PilotosNaves

____

##### Para melhor visualização, segue diagrama do banco de dados:

![

](C:\Users\CABRAL'S HOME\AppData\Roaming\Typora\typora-user-images\image-20211115221917389.png)