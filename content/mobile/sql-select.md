---
title: "SQL Refresher: SELECT"
date: 2021-11-15T17:40:46Z
draft: false
---

As part of me becoming more familiar with Room, I decided to make some notes on SQL to serve as a bit of a cheat sheet that I can refer back to. This first post covers `SELECT` statement.

## SELECT Statements
Read everything from the `places` database:
```
SELECT * FROM places
```
Read the `name` and `distance` columns, and limit to the first 5 results:
```
SELECT name, distance FROM places
LIMIT 5
```
Get the names of all the beaches that are less than 100km away:
```
SELECT name FROM places
WHERE type = "beach"
AND distance < 100
```

