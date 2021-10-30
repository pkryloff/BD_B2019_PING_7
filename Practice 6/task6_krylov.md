### 1. Для Олимпийских игр 2004 года сгенерируйте список (год рождения, количество игроков, количество золотых медалей), содержащий годы, в которые родились игроки, количество игроков, родившихся в каждый из этих лет, которые выиграли по крайней мере одну золотую медаль, и количество золотых медалей, завоеванных игроками, родившимися в этом году.

```sql
SELECT EXTRACT(YEAR FROM players.birthdate) as dob, COUNT(DISTINCT players.player_id) as player, COUNT(results.medal) as golds
FROM players
    JOIN results on players.player_id = results.player_id
    JOIN events on results.event_id = events.event_id
    JOIN olympics on events.olympic_id = olympics.olympic_id
WHERE olympics.year = 2004 AND results.medal = 'GOLD'
GROUP BY dob
```

### 2. Перечислите все индивидуальные (не групповые) соревнования, в которых была ничья в счете, и два или более игрока выиграли золотую медаль.

```sql
SELECT events.event_id FROM events
    JOIN results on events.event_id = results.event_id
WHERE events.is_team_event = 0 AND results.medal = 'GOLD'
GROUP BY events.event_id HAVING count(results.medal) >= 2
```

### 3. Найдите всех игроков, которые выиграли хотя бы одну медаль (GOLD, SILVER и BRONZE) на одной Олимпиаде. (player-name, olympic-id).

```sql
SELECT DISTINCT players.name, events.olympic_id FROM players
     JOIN results ON players.player_id = results.player_id
     JOIN events ON events.event_id = results.event_id
```

### 4. В какой стране был наибольший процент игроков (из перечисленных в наборе данных), чьи имена начинались с гласной?
```sql
SELECT vowel_names.country_id
FROM (
    SELECT players.country_id, COUNT(*) as num_of_names FROM players
        WHERE LEFT(players.name, 1) IN ('A', 'E', 'I', 'O', 'U')
        GROUP BY players.country_id
 ) AS vowel_names
JOIN (
    SELECT players.country_id, COUNT(DISTINCT players) AS num_of_players
    FROM players
    GROUP BY players.country_id
) AS players_by_country ON vowel_names.country_id = players_by_country.country_id
GROUP BY vowel_names.num_of_names, vowel_names.country_id, players_by_country.num_of_players
ORDER BY CAST(vowel_names.num_of_names AS decimal) / players_by_country.num_of_players DESC
LIMIT 1
```
### 5. Для Олимпийских игр 2000 года найдите 5 стран с минимальным соотношением количества групповых медалей к численности населения.
```sql
SELECT countries.country_id FROM olympics
     JOIN events ON events.olympic_id = olympics.olympic_id
     JOIN results ON events.event_id = results.event_id
     JOIN players ON players.player_id = results.player_id
     JOIN countries ON countries.country_id = players.country_id
WHERE olympics.year = 2000 AND events.is_team_event = 1
GROUP BY countries.country_id, countries.population
ORDER BY CAST(COUNT(results.medal) AS decimal) / countries.population
LIMIT 5
```
