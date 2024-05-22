### Processamento de Logs com Atualização Automática usando MySQL

Neste artigo, vamos explorar uma abordagem eficiente e escalável para processar e analisar logs de acesso armazenados em uma tabela MySQL. Usaremos uma combinação de tabelas persistentes, procedimentos armazenados e eventos para automatizar a atualização e processamento dos dados de logs. Esta abordagem garante que os dados estejam sempre atualizados e prontos para análise sem a necessidade de intervenção manual constante.

#### Passo 1: Criação da Tabela de Logs de Acesso

Suponha que temos uma tabela chamada `sc_log` que armazena logs de acesso com a seguinte estrutura:

```sql
CREATE TABLE `sc_log` (
    `id` INT(8) NOT NULL AUTO_INCREMENT,
    `inserted_date` DATETIME NULL DEFAULT NULL,
    `username` VARCHAR(90) NOT NULL COLLATE 'latin1_swedish_ci',
    `application` VARCHAR(255) NOT NULL COLLATE 'latin1_swedish_ci',
    `creator` VARCHAR(30) NOT NULL COLLATE 'latin1_swedish_ci',
    `ip_user` VARCHAR(255) NOT NULL COLLATE 'latin1_swedish_ci',
    `action` VARCHAR(30) NOT NULL COLLATE 'latin1_swedish_ci',
    `description` TEXT NULL DEFAULT NULL COLLATE 'latin1_swedish_ci',
    PRIMARY KEY (`id`) USING BTREE
)
COLLATE='latin1_swedish_ci'
ENGINE=MyISAM
AUTO_INCREMENT=1170864;
```

#### Passo 2: Criação da Tabela para Dados Processados

Vamos criar uma tabela persistente chamada `processed_log` que armazenará os dados processados:

```sql
CREATE TABLE `processed_log` (
    `id` INT(8) NOT NULL,
    `username` VARCHAR(90) NOT NULL COLLATE 'latin1_swedish_ci',
    `start` DATETIME NULL DEFAULT NULL,
    `finish` DATETIME NULL DEFAULT NULL,
    `ip_user` VARCHAR(255) NOT NULL COLLATE 'latin1_swedish_ci',
    `elapsed_time` TIME NULL DEFAULT NULL,
    PRIMARY KEY (`id`)
)
COLLATE='utf8mb4_general_ci'
ENGINE=InnoDB;
```

#### Passo 3: Procedimento Armazenado para Processar Dados

Criamos um procedimento armazenado chamado `ProcessLogData` que irá processar os dados novos da tabela `sc_log` e inseri-los na tabela `processed_log`:

```sql
DELIMITER //

CREATE PROCEDURE ProcessLogData()
BEGIN
    -- Inserir dados na tabela processed_log
    INSERT INTO processed_log (id, username, start, finish, ip_user, elapsed_time)
    SELECT
        current_log.id,
        current_log.username,
        IFNULL(LAG(current_log.inserted_date) OVER (PARTITION BY current_log.username ORDER BY current_log.inserted_date), current_log.inserted_date) AS start,
        current_log.inserted_date AS finish,
        current_log.ip_user,
        SEC_TO_TIME(TIMESTAMPDIFF(SECOND, IFNULL(LAG(current_log.inserted_date) OVER (PARTITION BY current_log.username ORDER BY current_log.inserted_date), current_log.inserted_date), current_log.inserted_date)) AS elapsed_time
    FROM
        sc_log AS current_log
    WHERE
        DATE(current_log.inserted_date) = CURDATE()
        AND current_log.username <> ''
        AND current_log.id NOT IN (SELECT id FROM processed_log) -- Evitar duplicados
    ORDER BY
        current_log.username, current_log.inserted_date;
END //

DELIMITER ;
```

#### Passo 4: Agendamento do Procedimento

Para garantir que o procedimento `ProcessLogData` seja executado automaticamente em intervalos regulares, usamos um evento no MySQL:

```sql
DELIMITER //

CREATE EVENT ProcessLogDataEvent
ON SCHEDULE EVERY 1 HOUR -- Ajuste o intervalo conforme necessário
DO
    CALL ProcessLogData();

DELIMITER ;
```

Este evento será executado a cada hora, chamando o procedimento `ProcessLogData` e processando novos dados na tabela `sc_log`.

#### Passo 5: Consultas para Análise dos Dados

Com os dados processados na tabela `processed_log`, podemos realizar várias análises. Aqui estão duas consultas importantes:

**Total de Horas por Usuário Excluindo Tempos Maiores que 9 Minutos:**

```sql
SELECT
    username,
    SEC_TO_TIME(SUM(TIME_TO_SEC(elapsed_time))) AS total_elapsed_time
FROM
    processed_log
WHERE
    elapsed_time <= '00:09:00'
GROUP BY
    username
ORDER BY
    total_elapsed_time DESC;
```

**Listar Todas as Etapas de um Usuário Específico:**

```sql
SELECT
    id,
    username,
    start,
    finish,
    ip_user,
    elapsed_time
FROM
    processed_log
WHERE
    username = 'especificar_o_username_aqui'
ORDER BY
    start;
```

Substitua `'especificar_o_username_aqui'` pelo nome de usuário desejado.

#### Benefícios da Abordagem

1. **Persistência dos Dados:** Usar uma tabela persistente (`processed_log`) permite que os dados processados sejam armazenados permanentemente e acessíveis para análises futuras.
2. **Eficiência e Desempenho:** A tabela `processed_log` é atualizada incrementalmente, processando apenas os novos registros da tabela `sc_log`, o que melhora a eficiência.
3. **Automatização:** A utilização de eventos no MySQL garante que o procedimento de processamento dos logs seja executado automaticamente em intervalos regulares, eliminando a necessidade de intervenção manual.
4. **Escalabilidade:** Essa abordagem permite que múltiplas sessões e usuários utilizem o sistema simultaneamente sem problemas de concorrência, graças ao isolamento proporcionado pelas transações InnoDB.

#### Conclusão

Este artigo apresentou uma solução robusta para o processamento e análise de logs de acesso utilizando MySQL. Ao implementar uma tabela persistente para armazenar os dados processados e automatizar a atualização desses dados por meio de procedimentos armazenados e eventos, garantimos um sistema eficiente, escalável e fácil de manter. Essa abordagem é ideal para cenários onde a análise contínua e o histórico de logs são críticos para a operação e monitoramento de sistemas.
