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
```

### Lister les quantités d’achat d’une commande (invoice) pour chaque piste
```sql
SELECT Track.Name , sum(invoiceLine.Quantity) as Somme_de_facture
FROM Invoice,  InvoiceLine, Track
WHERE Track.TrackId = InvoiceLine.TrackId  and invoiceline.InvoiceId = invoice.InvoiceId 
GROUP by Track.Name
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
```

### Calculer le nombre de vente (somme des quantités) de chaque album
```sql
SELECT Album.Title, sum(invoiceLine.Quantity) as Nombre_de_ventes
FROM Invoice,  InvoiceLine, Track, Album 
WHERE Track.TrackId = InvoiceLine.TrackId  and invoiceline.InvoiceId = invoice.InvoiceId and Track.AlbumId =Album.AlbumId 
GROUP by Album.Title 
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
```

### Trouver l’artiste le plus riche
```sql

```


### Trouver conjointement le top 10 des ventes et les flops (0 vente)
```sql

```

