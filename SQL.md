## Introduction sql

**Base de donnée** : C’est une table permettant de stocker des données afin de requêter et de récupérer ces données à tout moment en assurant une certaine cohérence entre ces données et protégeant les données.


**SGBDR** : base de donnée très forte en terme de relationnel centré dans la cohérence entre données de type données structurées.


D’autres bases sont apparues NOSQL : 

**Données structurées**
-	big tables (google)
-	classes (orienté objet)
-	graphe (orienté « relations » cf site de rencontre)
-	time series (orienté « temps » cf monitoring et ML)

**Données semi-structurées**
-	Doc json (orienté « REST »)
-	Doc* orienté « sémantique »


**Données déstructurées**
-	Clé valeur (orienté calcul,vitesse )

Chacune a ses avantages et inconvénients / on apprendra plus tard à choisir

**SGBDR | RDBMS (US) : Système de gestion de BD relationnelle | Relational DB management system**
-	Persister les données 
-	Accéder aux données depuis une application de manière normalisée
-	Garantir l’intégrité et la consistance des données

**SQL : Software query langage**
-	Manipuler des données relationnelles depuis une application
-	Normaliser
-	Gérer et structurer une BD


**Concepts fondamentaux**
-	Tables, lignes, colonnes
-	Clés primaires et étrangères
-	Cles étrangères
-	SQL SOFTWARE QUERY LANGAGE :
-		DML : SELECT INSERT UPDATE DELETE MERGE
-		TCL : COMMIT ROLLBACK SAVEPOINT
-		DDL : CREATE ALTER DROP RENAME TRUNCATE COMMENT
-		DCL : GRANT REVOQIE


## TP #1 : SQL BASIQUE

### Sélectionner tous les albums

```sql
SELECT * FROM Album;
```

### N’afficher que les titres des albums
```sql
SELECT title FROM Album ;
```

### Rechercher les albums signées « AC/DC »
```sql
SELECT title FROM Album
WHERE ArtistId = 1;


SELECT Title FROM Album alb , Artist art
where alb.ArtistId = art.ArtistId 
and art.Name ="AC/DC";
```

##  TP #2 : SQL & JOINTURES

### Afficher pour chaque titre d’album, le nom de son artiste
```sql
SELECT album.Title, artist.Name
FROM album
JOIN artist ON album.ArtistId = artist.ArtistId;
```

ou bien

```sql
SELECT album.title, artist.name FROM album, Artist
WHERE album.ArtistId = artist.ArtistId;
```

On peut utiliser des alias :

```sql
SELECT album.title, artist.name FROM album AL, artist AR
WHERE AL.ArtistId = AR.ArtistId;
```

### Afficher pour chaque titre de piste, le titre de l’album, le genre, et le média
```sql
SELECT Track.Name, Album.Title, Genre.Name, MediaType.Name 
From Track, Album , Genre, MediaType 
WHERE track.AlbumId =album.AlbumId and track.GenreId =genre.GenreId and track.MediaTypeId =mediatype.MediaTypeId 
```

### Idem en allant chercher le nom de l’artiste…
```sql
SELECT Track.Name, Album.Title, Genre.Name, MediaType.Name, artist.Name 
From Track, Album , Genre, MediaType, Artist
WHERE track.AlbumId =album.AlbumId and track.GenreId =genre.GenreId and track.MediaTypeId =mediatype.MediaTypeId  and album.ArtistId =artist.ArtistId 

SELECT Track.Name, Album.Title, Genre.Name, Mediatype.Name, Artist.Name 
FROM Track, Album
JOIN Genre ON  Genre.GenreId = Track.GenreId
JOIN MediaType ON MediaType.MediaTypeId  = Track.MediaTypeId 
JOIN Artist ON Artist.ArtistId = Album.ArtistId 



```

### Lister les quantités d’achat d’une commande (invoice) pour chaque piste
```sql
SELECT Track.Name , sum(invoiceLine.Quantity) as Somme_de_facture
FROM Invoice,  InvoiceLine, Track
WHERE Track.TrackId = InvoiceLine.TrackId  and invoiceline.InvoiceId = invoice.InvoiceId 
GROUP by Track.Name

SELECT Track.Name, sum(InvoiceLine.Quantity) as sum_qte_achat
from InvoiceLine
join Track on Track.trackId = InvoiceLine.TrackId 
group by Track.Name
```

### Lister les chefs
```sql
SELECT DISTINCT E.LastName AS LastNameChef, E.FirstName AS FirstNameChef
FROM Employee E
JOIN Employee Chef ON E.EmployeeId = Chef.ReportsTo;
```

ou bien 

```sql
SELECT Employee.LastName AS LastNameChef, Employee.FirstName as FirstNameChef
FROM Employee 
WHERE Employee.EmployeeId in (
					SELECT ReportsTo
    				FROM Employee Chef
						)
```

ou bien 

```sql
SELECT DISTINCT E.LastName AS LastNameChef, E.FirstName AS FirstNameChef
FROM Employee E, Employee Chef
WHERE E.EmployeeId = Chef.ReportsTo;
```

## TP #3 : SQL & FONCTIONS, GROUPEMENTS ET UNIONS

### Compter le nombre d’artiste référencés
```sql
SELECT count(*) as "Nombres d'artistes ref"
FROM Artist 
```

### Compter le nombre de piste par album d’AC/DC
```sql
SELECT count(Track.TrackId) as Nombre_track, Album.Title as Title_ACDC
FROM track, album, artist
WHERE Track.AlbumId = Album.AlbumId and Album.ArtistId = Artist.ArtistId and Artist.Name = "AC/DC"
group by Album.Title 


SELECT COUNT(Track.TrackId) as "nombre piste", album.Title as "Album AC/DC"
FROM Track 
JOIN Album on album.AlbumId = track.AlbumId 
Join Artist on album.ArtistId = Artist.ArtistId 
where Artist.Name ="AC/DC"
Group BY album.Title

```

### Calculer le nombre de vente (somme des quantités) de chaque album
```sql
SELECT Album.Title, sum(invoiceLine.Quantity) as Nombre_de_ventes
FROM  InvoiceLine, Track, Album 
WHERE Track.TrackId = InvoiceLine.TrackId  and Track.AlbumId =Album.AlbumId 
GROUP by Album.Title 

SELECT SUM (InvoiceLine.Quantity) as "Nombre de vente", Album.Title as "Titre album"
FROM InvoiceLine, Track, Album
WHERE InvoiceLine.TrackId = Track.TrackId AND Track.AlbumId = Album.AlbumId 
GROUP BY Album.Title 

```

###  Calculer le top 10 des titres puis des albums vendus en unité de vente, puis en $
```sql
SELECT t.Name as Name, sum(il.Quantity) as Nombre_de_ventes_unite, sum(il.Quantity*il.UnitPrice) as "calcul_$"
FROM Album a
	LEFT JOIN track t ON t.AlbumId = a.AlbumId
	LEFT JOIN InvoiceLine il ON il.TrackId = t.TrackId
	LEFT JOIN Invoice i ON i.InvoiceId =il.InvoiceId
group by t.Name
order by Nombre_de_ventes_unite DESC 
LIMIT 10
```

### Classer les genres par succès
```sql
SELECT g.Name as Name, sum(il.Quantity) as Nombre_de_ventes_unite
FROM Album a
	LEFT JOIN track t ON t.AlbumId = a.AlbumId
	LEFT JOIN InvoiceLine il ON il.TrackId = t.TrackId
	LEFT JOIN Genre g ON g.GenreId =t.GenreId 
	LEFT JOIN Invoice i ON i.InvoiceId =il.InvoiceId
group by g.Name
order by Nombre_de_ventes_unite DESC 



SELECT Genre.Name as type_genre, sum(InvoiceLine.Quantity) as nombre_vente_unite
FROM Genre
LEFT JOIN Track ON Genre.GenreId =Track.GenreId 
LEFT JOIN InvoiceLine ON Track.TrackId = InvoiceLine.TrackId 
GROUP BY Genre.Name
ORDER BY nombre_vente_unite DESC

```

###  Trouver les artistes n’ayant rien vendu

```sql
SELECT art.Name  
FROM artist art
	LEFT JOIN Album a ON art.artistId = a.ArtistId 
	LEFT JOIN track t ON t.AlbumId = a.AlbumId
	LEFT JOIN InvoiceLine il ON il.TrackId = t.TrackId
	LEFT JOIN Invoice i ON i.InvoiceId =il.InvoiceId
group by art.Name
HAVING sum(il.Quantity) ISNULL 

SELECT Artist.Name as "nom_artiste"
FROM Artist
LEFT JOIN Album ON Artist.ArtistId = Album.ArtistId 
LEFT JOIN Track ON Track.AlbumId = Album.AlbumId 
LEFT JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId 
GROUP BY Artist.Name
HAVING SUM(InvoiceLine.Quantity) ISNULL 

WHERE il.TrackId = t.TrackId and t.AlbumId = alb.AlbumId and alb.ArtistId  = art.ArtistId 
```

### Trouver les artistes ayant vendu plus de 10 titres
```sql
SELECT art.Name  
FROM artist art
	LEFT JOIN Album a ON art.artistId = a.ArtistId 
	LEFT JOIN track t ON t.AlbumId = a.AlbumId
	LEFT JOIN InvoiceLine il ON il.TrackId = t.TrackId
	LEFT JOIN Invoice i ON i.InvoiceId =il.InvoiceId
group by art.Name
HAVING sum(il.Quantity) >=10



SELECT Artist.Name as "Nom_artiste"
FROM Artist
LEFT JOIN Album ON Artist.ArtistId = Album.ArtistId 
LEFT JOIN Track ON Album.AlbumId = Track.AlbumId 
LEFT JOIN InvoiceLine ON Track.TrackId = InvoiceLine.TrackId 
GROUP BY Nom_artiste
HAVING sum(InvoiceLine.Quantity) >=10
```

### Trouver l’artiste le plus riche
```sql
SELECT Artist.Name 
FROM Artist
LEFT JOIN Album ON Artist.ArtistId = Album.ArtistId 
LEFT JOIN Track ON Album.AlbumId = Track.AlbumId 
LEFT JOIN InvoiceLine ON Track.TrackId = InvoiceLine.TrackId 
GROUP BY Artist.Name
ORDER BY SUM(InvoiceLine.UnitPrice * InvoiceLine.Quantity) DESC
LIMIT 1

```


### Trouver conjointement le top 10 des ventes et les flops (0 vente)
```sql
SELECT Track.Name AS "top_10", NULL AS "flop"
FROM Track
LEFT JOIN InvoiceLine ON Track.TrackId = InvoiceLine.TrackId
GROUP BY Track.Name
ORDER BY SUM(InvoiceLine.Quantity) DESC
LIMIT 10

UNION ALL

-- Flops (0 vente)
SELECT Track.Name AS "flop", NULL AS "top_10"
FROM Track
LEFT JOIN InvoiceLine ON Track.TrackId = InvoiceLine.TrackId
WHERE InvoiceLine.TrackId IS NULL
GROUP BY Track.Name
LIMIT 10
```

## NOSQL

MONGODB (Techno la plus connu) ou CLOUD FIRESTORE (pour une comparaison car c'est completement different)

base de donnée en json ce sont des base de données semi structuré (structuré c'est sql), les non structurés sont les clefs valeurs ou drive par exemple.
On va se concentrer sur les semi structuré qui est le json qui represente un arbre de donnée, c'est orienté.

Interet de json c'est que la base du web est en json donc utilisation et affichage simple.

On va reflechir sur les avantages et inconvenient entre le sql et nosql. --> Dans des grandes entreprises on fait un mashup des base de donnée sql et nosql 


### MONGODB

les requetages quasi pareil 

```sql

```