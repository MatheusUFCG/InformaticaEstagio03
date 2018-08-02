# InformaticaEstagio03

	#               Projeto de Banco de Dados  
	#     
	#     
	#       Aluno: Matheus Martins Monteiro 
	#              		113111142

	  
	  
	  

	#------------ Criação do Banco de Dados ----------------  
 
	CREATE database ROBOLIGHT;  
	use ROBOLIGHT;  
	  

	#------------ Criação de Tabelas ----------------  

	CREATE TABLE Usuario (  
	    ID int(32) NOT NULL AUTO_INCREMENT, 
	    Nome varchar(30) NOT NULL, 
            Senha varchar(50) NOT NULL,
	    Email varchar(30) NOT NULL UNIQUE, 
	    Apelido varchar(20) NOT NULL,    
	    CPF varchar(11) NOT NULL UNIQUE,  
	    ID_Endereco int(30) NOT NULL,   
	    ID_Admin int(32) ,  
	    PRIMARY KEY (ID,CPF)  
	);  
	  
	CREATE TABLE Endereco (  
	    ID int(32) NOT NULL AUTO_INCREMENT,  
	    Rua varchar(50) NOT NULL,  
	    Bairro varchar(50) NOT NULL,  
	    Numero int(5) NOT NULL,  
	    CEP int(10) NOT NULL,  
	    PRIMARY KEY (ID)  
	);  
	  
	CREATE TABLE Telefone_Usuarios (  
	    ID_Usuario int(32) NOT NULL,  
	    Telefone varchar(15),  
	    PRIMARY KEY (ID_Usuario,Telefone)  
	);  
	  
	CREATE TABLE Localidade (  
	    ID int(32) NOT NULL AUTO_INCREMENT,  
	    Setor varchar(30) NOT NULL,  
	    Comodo varchar(30) NOT NULL,  
	    ID_Modulo int(32) NOT NULL,  
	    PRIMARY KEY (ID,Comodo)  
	);  
	  
	CREATE TABLE Modulo (  
	    ID int(32) NOT NULL AUTO_INCREMENT,  
	    Codigo int(12) NOT NULL,  
	    DataFabricacao DATETIME(6) NOT NULL,  
	    Cor varchar(30) NOT NULL DEFAULT 'Magenta',  
	    PRIMARY KEY (ID,Codigo)  
	);  
	  
	CREATE TABLE Solicitacoes (  
	    ID int(32) NOT NULL AUTO_INCREMENT,   
	    ID_Modulo int(32) NOT NULL,   
	    Status enum('Concedido','Negado') NOT NULL,  
	    PRIMARY KEY (ID)  
	);  
	  
	
	  
	  
 
	#--------- Adicionando as chaves estrangeiras ---------  

	ALTER TABLE Usuario ADD CONSTRAINT Usuario_ss0 FOREIGN KEY (ID_Endereco) REFERENCES Endereco(ID);  
	  
	ALTER TABLE Usuario ADD CONSTRAINT Usuario_ss1 FOREIGN KEY (ID_Admin) REFERENCES Usuario(ID);  
	  
	ALTER TABLE Telefone_Usuarios ADD CONSTRAINT Telefone_Usuarios_ss0 FOREIGN KEY (ID_Usuario) REFERENCES Usuario(ID);  
  
	ALTER TABLE Localidade ADD CONSTRAINT Local_ss0 FOREIGN KEY (ID_Modulo) REFERENCES Modulo(ID);  
	  
	ALTER TABLE Solicitacoes ADD CONSTRAINT Solicitacoes_ss0 FOREIGN KEY (ID_Usuario) REFERENCES Usuario(ID);  
	  
	ALTER TABLE Solicitacoes ADD CONSTRAINT Solicitacoes_ss1 FOREIGN KEY (ID_Modulo) REFERENCES Modulo(ID);  
	  
	  
	  

	#----------------- Inserção de Usuarios ----------------  
 
	START TRANSACTION;  
	    INSERT INTO Endereco(Rua,Bairro,Numero,CEP)   
	        VALUES ('Rua 27 de Julho','Universitario', '1400', '58429130');      
	    SELECT @a:=ID FROM Endereco ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Usuario(Nome,Apelido,Email,CPF,Senha,ID_Endereco)   
	        VALUES ('Matheus Martins','matheus','matheus.martins@ee.ufcg.edu.br','1234567890','senha123', @a);  
	COMMIT;  
	  
	START TRANSACTION;  
	    INSERT INTO Endereco(Rua,Bairro,Numero,CEP)   
	        VALUES ('Rua Aprigio Veloso','Universitario','1429', '64800425');      
	    SELECT @a:=ID FROM Endereco ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Usuario(Nome,Apelido,Email,CPF,Senha,ID_Endereco)   
	        VALUES ('Danilo Freire','Danilo','danilo.santos@dee.ufcg.edu.br','12345678901','ufcg', @a);  
	COMMIT;   
	  
	START TRANSACTION;  
	    INSERT INTO Endereco(Rua,Bairro,Numero,CEP)   
	        VALUES ('Rua magalhes','Catole', '546', '64800000');   
	    SELECT @a:=ID FROM Endereco ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Usuario(Nome,Apelido,Email,CPF,Senha,ID_Endereco, ID_Admin)   
	        VALUES ('Ana','ana','ana.cardozo@ee.ufcg.edu.br','44488899512','sleep', @a, 1);  
	COMMIT;   
	  
	START TRANSACTION;  
	    INSERT INTO Endereco(Rua,Bairro,Numero,CEP)   
	        VALUES ('Avenida Floriano Peixoto','Centro','1248','64800740');     
	    SELECT @a:=ID FROM Endereco ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Usuario(Nome,Apelido,Email,CPF,Senha,ID_Endereco, ID_Admin)   
	        VALUES ('Zayra','zayra','zayra.silva@ee.ufcg.edu.com','15487651234','overwatch', @a, 1);  
	COMMIT;   
	  
	START TRANSACTION;  
	    INSERT INTO Endereco(Rua,Bairro,Numero,CEP)   
	        VALUES ('Rua das Flores','Morada Nova','496', '64800470');     
	    SELECT @a:=ID FROM Endereco ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Usuario(Nome,Apelido,Email,CPF,Senha,ID_Endereco, ID_Admin)   
	        VALUES ('Dona Florinda','Florinda','florinda@gmail.com','9876543210','girafales', @a, 1);  
	COMMIT;   
	  
	START TRANSACTION;  
	    INSERT INTO Endereco(Rua,Bairro,Numero,CEP)   
	        VALUES ('Rua João Suassuna','Centro','81', '64800456');    
	    SELECT @a:=ID FROM Endereco ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Usuario(Nome,Apelido,Email,CPF,Senha,ID_Endereco, ID_Admin)   
	        VALUES ('Jaquelina','jack','jaqueline@gmail.com','12312312312','supergirl', @a, 1);  
	COMMIT;   
	  
	START TRANSACTION;  
	    INSERT INTO Endereco(Rua,Bairro,Numero,CEP)   
	        VALUES ('Avenida Matheus Martins','Universitario', '1994','21101994');     
	    SELECT @a:=ID FROM Endereco ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Usuario(Nome,Apelido,Email,CPF,Senha,ID_Endereco, ID_Admin)   
	        VALUES ('Carolina','carol','carolina@gmail.com','0147852369','ccop', @a, 2),     
	             ('Rafael','rafa','rafael@gmail.com','9638527410','rsncs', @a, 2);  
	COMMIT;   
	  
	  
	  
 
	#------------ Inserção de Modulos e Locais--------------  
 
	  
	START TRANSACTION;  
	    INSERT INTO Modulo(Codigo, Cor, DataFabricacao)   
	        VALUES ('4560', 'Azul','2004-18-20');    
	    SELECT @a:=ID FROM Modulo ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Localidade(Setor, Comodo, ID_Modulo)   
	        VALUES ('Embedded','copa', @a);  
	COMMIT;   
	  
	START TRANSACTION;  
	    INSERT INTO Modulo(Codigo,Cor,DataFabricacao)   
	        VALUES ('5460','Amarelo','2002-02-14');     
	    SELECT @a:=ID FROM Modulo ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Localidade(Setor, Comodo, ID_Modulo)   
	        VALUES ('Embedded','Comodo', @a);  
	COMMIT;   
	  
	START TRANSACTION;  
	    INSERT INTO Modulo(Codigo,Cor,DataFabricacao)   
	        VALUES ('1604','Verde','1994-10-21');    
	    SELECT @a:=ID FROM Modulo ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Localidade(Setor, Comodo, ID_Modulo)   
	        VALUES ('Embedded','banheiro', @a);  
	COMMIT;   
	  
	START TRANSACTION;  
	    INSERT INTO Modulo(Codigo,Cor,DataFabricacao)   
	        VALUES ('3333','Vermelho','2004-18-20');     
	    SELECT @a:=ID FROM Modulo ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Localidade(Setor, Comodo, ID_Modulo)   
	        VALUES ('Embedded','3', @a);  
	COMMIT;   
	  
	START TRANSACTION;  
	    INSERT INTO Modulo(Codigo,Cor,DataFabricacao)   
	        VALUES ('4444','Preto','2002-02-14');     
	    SELECT @a:=ID FROM Modulo ORDER BY ID DESC LIMIT 1;      
	    INSERT INTO Localidade(Setor, Comodo, ID_Modulo)   
	        VALUES ('Embedded','4', @a);  
	COMMIT;   
	  

	#------------ Inserção de Solicitacoes ------------
 
	START TRANSACTION;    
	    INSERT INTO Solicitacoes(ID_Usuario,ID_Modulo,Status)  
	        VALUES  ('1','1','Permitido'),  
	                ('1','1','Negado'),  
	                ('3','5','Negado'),  
	                ('1','1','Permitido'),  
	                ('4','5','Permitido'),  
	                ('2','3','Permitido'),  
	                ('1','1','Permitido'),  
	                ('3','5','Permitido'),  
	                ('8','3','Permitido'),  
	                ('4','5','Permitido'),  
	                ('1','1','Negado');  
	COMMIT; 
	  
	  
	
