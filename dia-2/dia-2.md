`INNER JOIN`
```sql
-- A sintaxe do INNER JOIN é a seguinte:
SELECT t1.coluna, t2.coluna
FROM tabela1 AS t1
INNER JOIN tabela2 AS t2
ON t1.coluna_em_comum = t2.coluna_em_comum;

-- Ex:
SELECT a.first_name, a.actor_id, f.actor_id
FROM sakila.actor AS a
INNER JOIN sakila.film_actor AS f
ON a.actor_id = f.actor_id;
```
Exerciício do course de `INNER JOIN`
```sql
/**/
/*Monte uma query que exiba o id do ator,
nome do ator e id do filme em que ele já
atuou,usando as tabelas actor e film_actor.
*/
SELECT a.actor_id, a.first_name, fa.film_id
FROM sakila.actor AS a
INNER JOIN sakila.film_actor AS fa
ON a.actor_id = fa.actor_id;

/*Use o JOIN para exibir o nome, sobrenome e
endereço de cada um dos funcionários do banco.
Use as tabelas staff e address.
*/
SELECT s.first_name, s.last_name, a.address
FROM sakila.staff AS s
INNER JOIN sakila.address AS a
ON s.address_id = a.address_id;

/*Exiba o id do cliente, nome e email dos
primeiros 100 clientes, ordenados pelo nome
em ordem decrescente, juntamente com o id do
endereço e o nome da rua onde o cliente mora.
Essas informações podem ser encontradas nas tabelas customer e address.
*/
SELECT
	c.customer_id, c.first_name, c.email,
  a.address_id, a.address
FROM
	sakila.customer AS c
INNER JOIN
	sakila.address AS a
ON c.address_id = a.address_id
ORDER BY c.first_name DESC
LIMIT 100;

/*Exiba o nome, email, id do endereço, endereço
e distrito dos clientes que moram no distrito
da California e que contêm “rene” em seus nomes.
As informações podem ser encontradas nas tabelas address e customer.
*/
SELECT
	c.first_name, c.email,
	a.address_id, a.address, a.district
FROM
	sakila.customer AS c
INNER JOIN
	sakila.address AS a
ON c.address_id = a.address_id
WHERE
	a.district = 'california'
		AND first_name LIKE '%rene%';

/*Exiba o nome, o sobrenome e a quantidade de
filmes alugados por cada cliente cadastrado.
Ordene seus resultados por nome e sobrenome de
forma decrescente. Exiba somente os clientes ativos.
As informações podem ser encontradas nas tabelas customer e rental.
*/
SELECT
	c.first_name, c.last_name,
    COUNT(r.rental_id) AS 'Quantidade de filmes alugados'
FROM sakila.customer AS c
INNER JOIN sakila.rental AS r
ON c.customer_id = r.customer_id
WHERE c.active = 1
GROUP BY c.customer_id
ORDER BY 
	c.first_name DESC,
    c.last_name DESC;

/*Monte uma query que exiba o nome, sobrenome
e a media de pagamento (amount) paga aos funcionários
no ano de 2006. Use as tabelas payment e staff.
Os resultados devem estar agrupados pelo
nome e sobrenome do funcionário.
*/
SELECT
	s.first_name, s.last_name,
    AVG(p.amount) AS 'Media de pagamento'
FROM sakila.staff AS s
INNER JOIN sakila.payment AS p
ON s.staff_id = p.staff_id
WHERE YEAR(p.payment_date) = '2006'
GROUP BY s.first_name, s.last_name;

/*Monte uma query que exiba o id do ator, nome,
id do filme e título do filme, usando as tabelas
actor, film_actor e film. Dica: você precisará
fazer mais de um JOIN na mesma query.
*/
SELECT
	a.actor_id, a.first_name,
    fa.film_id, f.title
FROM sakila.actor AS a
INNER JOIN sakila.film_actor AS fa
ON a.actor_id = fa.actor_id
INNER JOIN sakila.film AS f
ON fa.film_id = f.film_id;
```