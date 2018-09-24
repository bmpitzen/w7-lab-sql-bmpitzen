# SQL Queries!

## Query 1
### Original question
  Find all time entries.
### Final SQL Query
  ```SELECT * FROM time_entries;```
### Results
  500 rows returned in 6ms from: SELECT * FROM time_entries;

## Query 2
### Original question
  Find the developer who joined most recently.
### Final SQL Query
  ```
select max(joined_on) as 'Most Recent', * from developers;
  ```
### Results
  "34"	"Dr. Danielle McLaughlin"	"shakira.carter@kohler.org"	"2015-07-10"	"2015-07-14 16:15:19.224045"	"2015-07-14 16:15:19.224045"

## Query 3
### Original question
  Find the number of projects for each client.
### Final SQL Query
```
  SELECT client_id, COUNT(client_id) as count from projects
  GROUP BY client_id;
```
### Results
client_id|count
---------|---------
  "1"  | "3"
  "2"  | "3"
  "3"  | "3"
  "4"  | "3"
  "6"  | "6"
  "7"  | "3"
  "8"  | "3"
  "9"  | "3"
  "10" | "3"


## Query 4
### Original question
  Find all time entries, and show each one's client name next to it.
### Final SQL Query
```
  SELECT clients.name, time_entries.* FROM (time_entries
  LEFT JOIN projects on time_entries.project_id=projects.id)
  LEFT JOIN clients on projects.client_id=clients.id;
```
### Results
  500 rows returned in 8ms from: SELECT clients.name, time_entries.* FROM (time_entries
  LEFT JOIN projects on time_entries.project_id=projects.id)
  LEFT JOIN clients on projects.client_id=clients.id;

## Query 5
### Original question
  Find all developers in the "Ohio sheep" group.
### Final SQL Query
```
select * from developers
left join group_assignments on developers.id=group_assignments.developer_id
left join groups on group_assignments.group_id=groups.id
where groups.name='Ohio sheep';
```
### Results
3 rows returned in 1ms from: select * from developers
left join group_assignments on developers.id=group_assignments.developer_id
left join groups on group_assignments.group_id=groups.id
where groups.name='Ohio sheep';

## Query 6
### Original question
  Find the total number of hours worked for each client.
### Final SQL Query
```
  SELECT SUM(duration), clients.name FROM (time_entries
  LEFT JOIN projects on time_entries.project_id=projects.id)
  LEFT JOIN clients on projects.client_id=clients.id
  group by clients.name;
```
### Results
Hours|Client
-----|-----
"174"|"Carter, Farrell and Goodwin"
"188"|"Eichmann, Altenwerth and Morar"
"238"|"Goodwin Group"
"166"|"Jast LLC"
"223"|"Kuhic-Bartoletti"
"209"|"Mohr Inc"
"330"|"Ortiz, Gislason and Rutherford"
"176"|"West Group"
"166"|"Zieme-Ortiz"

## Query 7
### Original question
  Find the client for whom Mrs. Lupe Schowalter (the developer) has worked the greatest number of hours.
### Final SQL Query
```
SELECT developer, 
       client, 
       Max(totaltime) AS 'TotalTime' 
FROM   (SELECT developers.NAME            AS Developer, 
               clients.NAME               AS Client, 
               Sum(time_entries.duration) AS TotalTime 
        FROM   time_entries 
               LEFT JOIN developers 
                      ON developers.id = time_entries.developer_id 
               LEFT JOIN projects 
                      ON projects.id = time_entries.project_id 
               LEFT JOIN clients 
                      ON clients.id = projects.client_id 
        WHERE  developers.NAME = 'Mrs. Lupe Schowalter' 
        GROUP  BY clients.NAME); 
```
### Results
Developer|Client|Total Time
-----|-----|-----
"Mrs. Lupe Schowalter"|"Kuhic-Bartoletti"|"11"

## Query 8
### Original question
  List all client names with their project names (multiple rows for one client is fine).  Make sure that clients still show up even if they have no projects.
### Final SQL Query
```
SELECT * 
FROM   clients 
       LEFT JOIN projects 
              ON projects.client_id = clients.id; 
```
### Results
33 rows returned in 2ms from: select *
from clients
left join projects on projects.client_id=clients.id;

3 null entries.

## Query 9
### Original question
  Find all developers who have written no comments.
### Final SQL Query
```
SELECT * 
FROM   developers 
       LEFT JOIN comments 
              ON comments.developer_id = developers.id 
WHERE  comments.comment IS NULL;
```
### Results
13 rows returned in 2ms from: select *
from developers
left join comments on comments.developer_id=developers.id
where comments.comment is null
