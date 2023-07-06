-- Converte o texto da string para CAIXA ALTA
`SELECT UCASE('Oi, eu sou uma string');`
-- Converte o texto da string para caixa baixa
`SELECT LCASE('Oi, eu sou uma string');`
-- Substitui as ocorrências de uma substring em uma string
-- Primeiro elemento é a frase, segundo o que será substituido e terceiro o que será colocado no lugar
`SELECT REPLACE('Oi, eu sou uma string', 'string', 'cadeia de caracteres');`
`SELECT REPLACE(title, 'ACADEMY', 'FOO') FROM sakila.film WHERE film_id = 1;`
-- Retorna a parte da esquerda de uma string de acordo com o
-- número de caracteres especificado
`SELECT LEFT('Oi, eu sou uma string', 3);`
-- Retorna a parte da direita de uma string de acordo com o
-- número de caracteres especificado
`SELECT RIGHT('Oi, eu sou uma string', 6);`
-- Exibe o tamanho, em caracteres, da string, a função LENGTH retorna o tamanho em bytes
`SELECT CHAR_LENGTH('Oi, eu sou uma string');`
-- Extrai parte de uma string de acordo com o índice de um caractere inicial
-- e a quantidade de caracteres a extrair
`SELECT SUBSTRING('Oi, eu sou uma string', 5, 2);`
-- Se a quantidade de caracteres a extrair não for definida,
-- então a string será extraída do índice inicial definido, até o seu final
`SELECT SUBSTRING('Oi, eu sou uma string', 5);`
Exercicios do course - manipulação de strings:
`SELECT REPLACE('A Internet mudou o mundo', 'Internet', 'IA');`
`SELECT CHAR_LENGTH('Uma frase qualquer');`
`SELECT SUBSTRING('A linguagem JavaScript está entre as mais usadas', 13, 10);`



CONDICIONAIS
Usando o IF na tabela sakila.film, exiba o id do filme, o título e uma coluna extra chamada ‘filme visto?’, em que deve-se avaliar se o nome do filme é ‘ACE GOLDFINGER‘. Caso seja, exiba “OK”. Caso contrário, exiba “FALTA ASSISTIR”.
`SELECT title, rating, IF(title = 'ACE GOLDFINGER', 'OK', 'FALTA ASSISTIR') AS 'filme visto?' FROM sakila.film;`

Usando o CASE na tabela sakila.film, exiba o título, a classificação indicativa (rating) e uma coluna extra que vamos chamar de ‘grupo-alvo’ em que colocaremos a classificação do filme de acordo com as seguintes siglas(G:"Livre para todas as idades", PG:"Maio..."...): 
```sql
SELECT
	title,
	rating,
    CASE
		    WHEN rating = 'G' THEN 'Livre para todas as idades'
        WHEN rating = 'PG' THEN 'Maiores de 10 anos'
        WHEN rating = 'PG-13' THEN 'Maiores de 13 anos'
        WHEN rating = 'R' THEN 'Maiores de 17 anos'
        ELSE 'Proibido para menores de idade'
	END AS 'grupo-alvo'
FROM sakila.film;
```

FUNÇÕES MATEMÁTICAS NO MYSQL
a