/* 
1. My partner and I want to come by each of the stores in person and meet the managers. 
Please send over the managers’ names at each store, with the full address 
of each property (street address, district, city, and country please).  
*/ 
select 
staff.first_name,
staff.last_name,
address.address,
address.district,
city.city,
country.country
from staff
inner join store on staff.store_id=store.store_id
inner join address on address.address_id=store.address_id
inner join city on address.city_id=city.city_id
inner join country on country.country_id=city.country_id;









	
/*
2.I would like to get a better understanding of all of the inventory that would come along with the business. 
Please pull together a list of each inventory item you have stocked, including the store_id number, 
the inventory_id, the name of the film, the film’s rating, its rental rate and replacement cost. 
*/

SELECT
   inventory.inventory_id,
   inventory.store_id,
   film.title,
   film.rating,
   film.rental_rate,
   film.replacement_cost
FROM inventory
LEFT JOIN film
ON inventory.film_id = film.film_id;

















/* 
3.	From the same list of films you just pulled, please roll that data up and provide a summary level overview 
of your inventory. We would like to know how many inventory items you have with each rating at each store. 
*/

SELECT
   inventory.store_id,
   film.rating,
   COUNT(inventory.inventory_id) AS inventory_count
FROM inventory
LEFT JOIN film ON inventory.film_id = film.film_id
GROUP BY film.rating, inventory.store_id;












/* 
4. Similarly, we want to understand how diversified the inventory is in terms of replacement cost. We want to 
see how big of a hit it would be if a certain category of film became unpopular at a certain store.
We would like to see the number of films, as well as the average replacement cost, and total replacement cost, 
sliced by store and film category. 
*/ 

SELECT
 store_id,
 name AS category,
 COUNT(film.film_id) AS count_film,
 AVG(replacement_cost) AS ave_rep_cost,
 SUM(replacement_cost) AS total_rep_cost
FROM film
LEFT JOIN inventory ON film.film_id = inventory.film_id
LEFT JOIN film_category ON inventory.film_id = film_category.film_id
LEFT JOIN category ON film_category.category_id = category.category_id
GROUP BY store_id, name
ORDER BY total_rep_cost DESC;











/*
5.	We want to make sure you folks have a good handle on who your customers are. Please provide a list 
of all customer names, which store they go to, whether or not they are currently active, 
and their full addresses – street address, city, and country. 
*/
SELECT
   first_name,
   last_name,
   customer.store_id,
   active,
   address,
   city,
   country
FROM customer
LEFT JOIN address ON customer.address_id = address.address_id
LEFT JOIN city ON address.city_id = city.city_id
LEFT JOIN country ON city.country_id = country.country_id;











/*
6.	We would like to understand how much your customers are spending with you, and also to know 
who your most valuable customers are. Please pull together a list of customer names, their total 
lifetime rentals, and the sum of all payments you have collected from them. It would be great to 
see this ordered on total lifetime value, with the most valuable customers at the top of the list. 
*/
SELECT
   first_name,
   last_name,
   COUNT(rental.rental_id) AS total_lifetime_rental,
   SUM(payment.amount) AS total_payments_collected 
FROM customer
LEFT JOIN rental ON customer.customer_id = rental.customer_id
LEFT JOIN payment ON rental.rental_id = payment.rental_id
GROUP BY first_name, last_name
ORDER BY total_payments_collected DESC;











    
/*
7. My partner and I would like to get to know your board of advisors and any current investors.
Could you please provide a list of advisor and investor names in one table? 
Could you please note whether they are an investor or an advisor, and for the investors, 
it would be good to include which company they work with. 
*/
SELECT
   ‘advisor’ AS type,
   advisor.first_name,
   advisor.last_name,
   NULL AS company_name_if_investor
FROM advisor
UNION ALL
SELECT
   ‘investor’ AS type,
   investor.first_name,
   investor.last_name,
   company_name
FROM investor;










/*
8. We're interested in how well you have covered the most-awarded actors. 
Of all the actors with three types of awards, for what % of them do we carry a film?
And how about for actors with two types of awards? Same questions. 
Finally, how about actors with just one award? 
*/

SELECT
  CASE
   WHEN actor_award.awards = ‘Emmy, Oscar, Tony ‘ THEN ‘3 awards’
   WHEN actor_award.awards IN (‘Emmy, Oscar’, ‘Emmy, Tony’, ‘Oscar, Tony’) THEN ‘2 awards’
   ELSE ‘1 award’ 
   END AS num_of_awards,
   AVG(CASE WHEN actor_award.actor_id IS NULL THEN 0 ELSE 1 END) AS pct_w_one_film
FROM actor_award

GROUP BY
  CASE
   WHEN actor_award.awards = ‘Emmy, Oscar, Tony ‘ THEN ‘3 awards’
   WHEN actor_award.awards IN (‘Emmy, Oscar’, ‘Emmy, Tony’, ‘Oscar, Tony’) THEN ‘2 awards’
   ELSE ‘1 award’
END;
