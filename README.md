# Query-Aux-Development
Querys para auxiliar no desenvolvimento de classes VB.NET

## Criar ou Dropar a Tabela Auxiliar

```sql
  DROP TABLE [dbo].[X_AUX_TYPES];
  
  CREATE TABLE [dbo].[X_AUX_TYPES](
    [idSql] [int] NULL,
    [nameSql] [varchar](1000) NULL,
    [nameVbNet] [varchar](1000) NULL,
    [nameCSharp] [varchar](1000) NULL
  ) ON [PRIMARY]
  
```

## Popular a Tabela Auxiliar

```sql 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (34, N'image', NULL, NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (35, N'text', N'String', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (36, N'uniqueidentifier', N'String', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (40, N'date', N'Date', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (41, N'time', N'String', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (42, N'datetime2', N'DateTime', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (43, N'datetimeoffset', N'DateTime', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (48, N'tinyint', N'Integer', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (52, N'smallint', N'Integer', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (56, N'int', N'Integer', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (58, N'smalldatetime', N'DateTime', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (59, N'real', N'Decimal', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (60, N'money', N'Decimal', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (61, N'datetime', N'DateTime', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (62, N'float', N'Decimal', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (98, N'sql_variant', NULL, NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (99, N'ntext', NULL, NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (104, N'bit', N'Boolean', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (106, N'decimal', N'Decimal', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (108, N'numeric', N'Decimal', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (122, N'smallmoney', N'Decimal', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (127, N'bigint', N'Long', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (240, N'hierarchyid', NULL, NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (240, N'geometry', NULL, NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (240, N'geography', NULL, NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (165, N'varbinary', N'String', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (167, N'varchar', N'String', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (173, N'binary', NULL, NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (175, N'char', N'String', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (189, N'timestamp', N'DateTime', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (231, N'nvarchar', N'DateTime', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (239, N'nchar', N'DateTime', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (241, N'xml', N'String', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (231, N'sysname', N'String', NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (243, N'LISTA_INT', NULL, NULL) 
INSERT X_AUX_TYPES (idSql, nameSql, nameVbNet, nameCSharp) VALUES (243, N'LISTA_INT_STR', NULL, NULL) 
```

## Query criar função

```sql
CREATE FUNCTION TratarNameColumn (@nameProperty AS VARCHAR(100)) RETURNS VARCHAR(100)
AS
BEGIN

	declare @t as int = len(@nameProperty)
	declare @i as int = 2

	declare @strFinal as varchar(100) = Upper(substring(@nameProperty, 1,1))

	while @i <= @t 
	begin

		declare @letra as varchar(1) = substring(@nameProperty, @i, 1)
		declare @codigo as int = ASCII(@letra)

		if @codigo >= 65 and @codigo <= 90 begin 
			set @strFinal = @strFinal + ' ' +  substring(@nameProperty, @i, 1)

		end else begin 
			set @strFinal = @strFinal +  substring(@nameProperty, @i, 1)
		end

		set @i = @i + 1
	end

	RETURN @strFinal 

END
```

## Query para Aux Procedures

```sql
select	'@' + c.name + ' ' +
		tt.name + 
		case when tt.name = 'decimal' then '(18, 2)'
			 when tt.name = 'varchar' then
				case when c.max_length > -1 then '(' + cast(c.max_length as varchar(10))+ ')'
					 else '(MAX)'
				end
			 else ''
		end + ', ' As Tipagem,
		c.name + ',',
		c.name + ' = @' + c.name + ',' 

from sys.columns  c
join sys.tables t on c.object_id = t.object_id
join sys.types tt on c.system_type_id = tt.system_type_id
where t.name = 'NomeTabela'
```

## Query para Aux Classes

```sql
select	c.name,
		'Private _' + c.name + ' As ' + X.nameVbNet +  
		 CASE when c.is_nullable = 1 and x.namevbNet <> 'String' THEN '?' ELSE '' END,
		'If Not IsDBNull(dr.Item("'+c.name+'")) Then Me._'+c.name+' = dr.Item("'+c.name+'")',
		'cmd.Parameters.Add("@' + c.name + '", SqlDbType.' + X.nameSql +
		CASE when x.namevbNet = 'String' THEN
				', ' + cast(c.max_length as varchar(10))
			 when c.max_length = -1  then
				', -1 '
			 when c.scale > 0 and x.namevbNet <> 'DateTime' then
				', ' + cast(c.scale as varchar(10))
			 else ''
		END +
		CASE when c.is_nullable = 1   THEN
				').Value = IF(Me._' + c.name + ', DBNull.Value)'     
			 ELSE
				').Value = Me._' + c.name
		END,
		'<asp:ListItem Text="'+c.name+'" Value="'+c.name+'"></asp:ListItem>' as filtro 

from sys.columns c
join sys.tables t on c.object_id = t.object_id
join X_AUX_TYPES X on c.system_type_id = X.idSql
where t.name = 'NomeTabela'
```
