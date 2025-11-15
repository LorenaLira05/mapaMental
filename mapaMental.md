# 🧠 Mapa Mental — Comandos e Funções do MySQL
 
## 1️⃣ TRANSAÇÕES
- BEGIN / START TRANSACTION  
  - Inicia uma transação (modo seguro de execução)  
  - 💻 `START TRANSACTION;`
- COMMIT  
  - Confirma todas as operações da transação  
  - 💻 `COMMIT;`
- ROLLBACK  
  - Desfaz alterações não confirmadas  
  - 💻 `ROLLBACK;`
- SAVEPOINT nome  
  - Cria um ponto de restauração intermediário  
  - 💻 `SAVEPOINT etapa1;`
- ROLLBACK TO nome  
  - Retorna até um ponto específico  
  - 💻 `ROLLBACK TO etapa1;`
- SET TRANSACTION ISOLATION LEVEL  
  - Define o nível de isolamento (controle de concorrência)  
  - 💻 `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;`
 
---
 
## 2️⃣ VISÕES (VIEWS)
- CREATE VIEW  
  - Cria uma tabela virtual com base em uma consulta  
  - 💻 `CREATE VIEW vw_vendas AS SELECT cliente, SUM(total) AS total FROM vendas GROUP BY cliente;`
- SELECT * FROM view  
  - Consulta a visão  
  - 💻 `SELECT * FROM vw_vendas;`
- ALTER VIEW  
  - Modifica uma visão existente  
  - 💻 `ALTER VIEW vw_vendas AS SELECT cliente, COUNT(*) AS qtd FROM vendas GROUP BY cliente;`
- DROP VIEW  
  - Remove uma visão  
  - 💻 `DROP VIEW vw_vendas;`
 
---
 
## 3️⃣ GATILHOS (TRIGGERS)
- CREATE TRIGGER nome_timing_event  
  - Cria uma ação automática que ocorre antes ou depois de um evento  
  - 💻  
    ```sql
    CREATE TRIGGER log_vendas
    AFTER INSERT ON vendas
    FOR EACH ROW
    INSERT INTO logs(acao, data) VALUES ('Nova venda', NOW());
    ```
- BEFORE INSERT / UPDATE / DELETE  
  - Executa antes da ação ocorrer  
  - 💻  
    ```sql
    CREATE TRIGGER validar_preco
    BEFORE INSERT ON produtos
    FOR EACH ROW
    IF NEW.preco < 0 THEN SET NEW.preco = 0; END IF;
    ```
- AFTER INSERT / UPDATE / DELETE  
  - Executa após o evento ocorrer  
  - 💻  
    ```sql
    CREATE TRIGGER atualizar_log
    AFTER UPDATE ON clientes
    FOR EACH ROW
    INSERT INTO log_acoes VALUES (NOW(), 'Atualização de cliente');
    ```
- DROP TRIGGER nome  
  - Remove um gatilho  
  - 💻 `DROP TRIGGER atualizar_log;`
 
---
 
## 4️⃣ PROCEDURES (PROCEDIMENTOS)
- CREATE PROCEDURE nome()  
  - Cria um bloco de comandos armazenado no servidor  
  - 💻  
    ```sql
    DELIMITER //
    CREATE PROCEDURE listar_clientes()
    BEGIN
      SELECT * FROM clientes;
    END //
    DELIMITER ;
    ```
- CALL nome()  
  - Executa uma procedure  
  - 💻 `CALL listar_clientes();`
- CREATE PROCEDURE nome(param)  
  - Cria procedure com parâmetros de entrada  
  - 💻  
    ```sql
    DELIMITER //
    CREATE PROCEDURE buscar_cliente(IN id_cliente INT)
    BEGIN
      SELECT * FROM clientes WHERE id = id_cliente;
    END //
    DELIMITER ;
    ```
- OUT / INOUT  
  - Define parâmetros de saída e bidirecionais  
  - 💻  
    ```sql
    CREATE PROCEDURE somar(IN a INT, IN b INT, OUT resultado INT)
    BEGIN
      SET resultado = a + b;
    END;
    ```
- DROP PROCEDURE nome  
  - Remove uma procedure  
  - 💻 `DROP PROCEDURE listar_clientes;`
 
---
 
## 5️⃣ ÍNDICES (INDEXAÇÃO)
- CREATE INDEX  
  - Cria um índice para acelerar consultas  
  - 💻 `CREATE INDEX idx_nome ON clientes(nome);`
- CREATE UNIQUE INDEX  
  - Cria índice que impede duplicações  
  - 💻 `CREATE UNIQUE INDEX idx_cpf ON clientes(cpf);`
- CREATE INDEX nome ON tabela (col1, col2)  
  - Índice composto para múltiplas colunas  
  - 💻 `CREATE INDEX idx_nome_cidade ON clientes(nome, cidade);`
- SHOW INDEX FROM tabela  
  - Lista os índices existentes  
  - 💻 `SHOW INDEX FROM clientes;`
- DROP INDEX nome ON tabela  
  - Remove um índice  
  - 💻 `DROP INDEX idx_nome ON clientes;`
