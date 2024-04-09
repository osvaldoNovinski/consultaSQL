# consultaSQL
Consulta SQL que retorna as colunas de uma tabela preparada para virar uma entidade ou DTO em Java
~~~
SELECT CONCAT('private ',
    CASE 
        WHEN DATA_TYPE IN ('image') THEN 'byte[] '
        WHEN DATA_TYPE IN ('text', 'ntext', 'varchar', 'nvarchar', 'char', 'nchar') THEN 'String '
        WHEN DATA_TYPE IN ('uniqueidentifier') THEN 'UUID '
        WHEN DATA_TYPE IN ('date') THEN 'LocalDate '
        WHEN DATA_TYPE IN ('time') THEN 'LocalDateTime '
        WHEN DATA_TYPE IN ('datetime2', 'datetime', 'smalldatetime', 'datetimeoffset') THEN 'LocalDateTime '
        WHEN DATA_TYPE IN ('bigint') THEN 'Long '
		WHEN DATA_TYPE IN ('int') THEN 'Integer '
		WHEN DATA_TYPE IN ('tinyint', 'smallint') THEN 'Short '
        WHEN DATA_TYPE IN ('real', 'float') THEN 'Double '
        WHEN DATA_TYPE IN ('money', 'smallmoney', 'decimal', 'numeric') THEN 'Double '
        WHEN DATA_TYPE IN ('bit') THEN 'Boolean '
        WHEN DATA_TYPE IN ('hierarchyid', 'geometry', 'geography') THEN 'Object '
        WHEN DATA_TYPE IN ('timestamp') THEN 'LocalDateTime '
        WHEN DATA_TYPE IN ('xml') THEN 'String '
        WHEN DATA_TYPE IN ('sysname') THEN 'String '
        ELSE 'String '
    END,
    LOWER(SUBSTRING(COLUMN_NAME, 1, 1)) + SUBSTRING(COLUMN_NAME, 2, LEN(COLUMN_NAME)), 
    ';'
) AS JavaType
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'NomeDaTabela';
~~~
