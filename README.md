# data-warehouse
Modelo criado para treinamento e consultas 


O Data Warehouse é feito pensando nas necessidades do negócio. Ele existe para unir e dar sentido a todos os dados de forma que seja possível extrair os relatórios ou dashboards que se precisa.

Ele é adaptável e flexível às várias fontes de dados, além de ser desenhado para sofrer alterações contínuas, garantindo que vai continuar a atender as necessidades da empresa.

Assim, além de garantir que todas informações estão centralizadas, você também garante que todas as permissões de acesso estão corretas, e que os critérios e regras com os quais os dados estão sendo trabalhados são únicos.
Nesse exemplo desenvolvi as 3 tabelas dimenção e a tabela fato.
Foi usado sgbr oracle 11g e sql developer

--TABELAS DIMENÇÃO:--

CREATE TABLE DIM_PRODUTO (
ID_PRODUTO NUMBER,
PRIMARY KEY(ID_PRODUTO),
NOME_PRODUTO VARCHAR2(50), 
TIPO_PRODUTO VARCHAR2(50),
NOME_FABRICANTE VARCHAR2(100)
);

CREATE TABLE DIM_CLIENTE (
ID_CLIENTE NUMBER,
 PRIMARY KEY(ID_CLIENTE),
NOME_CLIENTE VARCHAR2(50), 
STATUS_CLIENTE VARCHAR2(50),
DATA_CADASTRO_CLIENTE VARCHAR2(100)
);

CREATE TABLE DIM_FORMA_PAGAMENTO (
    ID_FORMA_PAGAMENTO       NUMBER,
    PRIMARY KEY(ID_FORMA_PAGAMENTO),
    DESC_FORMA_PAGAMENTO     NUMBER,
    FLG_FATURAMENTO_IMEDIATO NUMBER
);
--TABELA FATO--

CREATE TABLE FATO_VENDA (
DATA_VENDA DATE,
ID_VENDA NUMBER,
PRIMARY KEY(ID_VENDA),
CONSTRAINT FK_DIM_PRODUTO FOREIGN KEY (ID_VENDA) REFERENCES DIM_PRODUTO(ID_PRODUTO),
CONSTRAINT FK_DIM_CLIENTE FOREIGN KEY (ID_VENDA)REFERENCES  DIM_CLIENTE(ID_CLIENTE),
CONSTRAINT FK_DIM_FORMA_PAGAMENTO FOREIGN KEY (ID_VENDA)REFERENCES DIM_FORMA_PAGAMENTO(ID_FORMA_PAGAMENTO ),
QTD_PRODUTO NUMBER, 
VALOR_UNITARIO_PRODUTO NUMBER,
VALOR_TOTAL NUMBER
);

