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

  `DIV` - Retorna resultado inteiro de uma divisão, ignorando as casas decimais
`SELECT 10 DIV 3;` return = 3;

  `MOD` - Retorna o resto da divisão.(Descobrir se um número é impar ou par se resto for 0 ou 1, quando dividido por 2)
`SELECT 10 MOD 2;` return = 0
`SELECT 14 MOD 3;` return = 2
`SELECT 13 MOD 2;` return = 1

Desafios com DIV e MOD:

Monte uma query usando o MOD juntamente com o IF para descobrir se o valor 15 é par ou ímpar. Chame essa coluna de ‘Par ou Ímpar’, onde ela pode dizer ‘Par’ ou ‘Ímpar’.
`SELECT IF(15 MOD 2 = 0, 'Par', 'Impar') AS 'Par ou Ímpar';`

Temos uma sala de cinema que comporta 220 pessoas. Quantos grupos completos de 12 pessoas podemos levar ao cinema sem que ninguém fique de fora?
`SELECT 220 DIV 12;`

Utilizando o resultado anterior, responda à seguinte pergunta: temos lugares sobrando? Se sim, quantos?
`SELECT IF(220 MOD 12 = 0, 'NÃO', CONCAT('SIM, ', 220 MOD 12));`



ARREDONDANDO VALORES
  `ROUND` - se for >= a 0,5 arrendo pra cima, se for <= 0,5, pra baixo
`SELECT ROUND(10.4925);` -- 10
`SELECT ROUND(10.5136);` -- 11
`SELECT ROUND(-10.5136);` -- -11
`SELECT ROUND(10.4925, 2);` -- 10.49
`SELECT ROUND(10.4925, 3);` -- 10.493

  `CEIL` - arredonda sempre para cima
`SELECT CEIL(10.51);` -- 11
`SELECT CEIL(10.49);` -- 11
`SELECT CEIL(10.2);` -- 11

  `FLOOR` - arredonda sempre para baixo
`SELECT CEIL(10.51);` -- 10
`SELECT CEIL(10.49);` -- 10
`SELECT CEIL(10.2);` -- 10


EXPONENCIAÇÃO E RAIZ QUADRADA
  `POW` - exponenciação
`SELECT POW(2, 2);` -- 4
`SELECT POW(2, 4);` -- 16

  `SQRT` - raiz quadrada
`SELECT SQRT(9);` -- 3
`SELECT SQRT(16);` -- 4

GERANDO VALORES ALEATÓRIOS
  `RAND`
`SELECT RAND();` - gera vaor aleatório entre 0 e 1
`SELECT ROUND(7 + (RAND() * 6));`
- gera valor aleatório entre 7 e 13. É usado o `ROUND` para que seja um valor inteiro

TRABALHANDO COM DATAS
`SELECT CURRENT_DATE();` -- YYYY-MM-DD
`SELECT NOW();` -- YYYY-MM-DD HH:MM:SS
`SELECT DATEDIFF('2020-01-31', '2020-01-01');` -- 30
`SELECT DATEDIFF('2020-01-01', '2020-01-31');` -- -30
`SELECT TIMEDIFF('08:30:10', '09:30:10');` -- -01:00:00
`SELECT TIMEDIFF('2021-08-11 08:30:10', '2021-08-01 09:30:10');` -- -239:00:00
`SELECT YEAR(CURRENT_DATE());` -- retorna o ano atual
`SELECT HOUR(NOW());` -- retorna a hora atual
Monte uma query que exiba a diferença de dias entre '2030-01-20' e hoje.
```sql
SELECT DATEDIFF('2030-01-20', NOW());
-- OU
SELECT DATEDIFF('2030-01-20', CURRENT_DATE());
```


FUNÇÕES DE AGREGAÇÃO
`SELECT AVG(replacement_cost) FROM sakila.film;` -- 19.984000 (Média entre todos registros)
`SELECT MIN(replacement_cost) FROM sakila.film;` -- 9.99 (Menor valor encontrado)
`SELECT MAX(replacement_cost) FROM sakila.film;` -- 29.99 (Maior valor encontrado)
`SELECT SUM(replacement_cost) FROM sakila.film;` -- 19984.00 (Soma de todos registros)
`SELECT COUNT(replacement_cost) FROM sakila.film;` -- 1000 registros encontrados (Quantidade)
Monte um query que exiba:
    A média de duração dos filmes e dê o nome da coluna de ‘Media de Duracao’;
    A duração mínima dos filmes como ‘Duracao Minima’;
    A duração máxima dos filmes como ‘Duracao Maxima’;
    A soma de todas as durações como ‘Tempo de Exibicao Total’;
    E, finalmente, a quantidade total de filmes cadastrados na tabela sakila.film como ‘Filmes Registrados’.
```sql
SELECT AVG(length) AS 'Media de Duracao',
       MIN(length) AS 'Duracao Minima',
       MAX(length) AS 'Duracao Maxima',
       SUM(length) AS 'Tempo de Exibicao Total',
       COUNT(*) AS 'Filmes Registrados'
FROM sakila.film;
```
`GROUP BY` - Agrupa por uma ou mais colunas. Quando usado, remove duplicações.
```sql
SELECT first_name, COUNT(*) FROM sakila.actor
GROUP BY first_name;
--Dessa forma, COUNT contabiliza quantos first_name repetidos tem.
```

```sql
SELECT rating, rental_rate, COUNT(1) as total FROM sakila.film
GROUP BY rating, rental_rate 
ORDER BY rating, rental_rate;
/*Agrupa rating em uma coluna e rental_rate em outra coluna.
rating e rental_rate vão se agrupar de forma que não tenha
repetição de dados.
Só vai aparecer um rating = G rental_rate = 0.99.
A coluna ao lado que tem o COUNT, vai mostrar quantas vezes
esse "GROUP BY rating, rental_rate" se repete.*/
```
`GROUP BY` em conjunto com funções de agregação
```sql
-- Média de duração de filmes agrupados por classificação indicativa
SELECT rating, AVG(length)
FROM sakila.film
GROUP BY rating;

-- Valor mínimo de substituição dos filmes agrupados por classificação indicativa
SELECT rating, MIN(replacement_cost)
FROM sakila.film
GROUP BY rating;

-- Valor máximo de substituição dos filmes agrupados por classificação indicativa
SELECT rating, MAX(replacement_cost)
FROM sakila.film
GROUP BY rating;

-- Custo total de substituição de filmes agrupados por classificação indicativa
SELECT rating, SUM(replacement_cost)
FROM sakila.film
GROUP by rating;
```

JSON_ARRAYAGG(coluna);.

`HAVING` - usado depois do `GROUP BY`
         - estamos filtrando somente resultados gerados APÓS o `GROUP BY` ter sido executado.

```sql
SELECT first_name, COUNT(*)
FROM sakila.actor
GROUP BY first_name
HAVING COUNT(*) > 2;

-- Ou, melhor ainda, usando o AS para dar nomes às colunas de agregação,
-- melhorando a leitura do resultado
SELECT first_name, COUNT(*) AS nomes_cadastrados
FROM sakila.actor
GROUP BY first_name
HAVING nomes_cadastrados > 2;

-- Observação: o alias não funciona com strings para o HAVING,
-- então use o underline ("_") para separar palavras
-- Ou seja, o exemplo abaixo não vai funcionar
SELECT first_name, COUNT(*) AS 'nomes cadastrados'
FROM sakila.actor
GROUP BY first_name
HAVING 'nomes cadastrados' > 2;

/*Aqui estamos buscando todos os filmes de acordo com a classificação
por idade, coluna rating, e que possuam o mesmo preço de aluguel,
coluna rental_rate. E ainda exista um total de filmes nesse
agrupamento, que seja menor que 70.*/
SELECT rating, rental_rate, COUNT(1) as total FROM sakila.film
GROUP BY rental_rate, rating
HAVING total < 70
ORDER BY rating, rental_rate;
```