# SQL-Practice

1. Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.
//SELECT FirstName, LastName, CustomerID, Country  FROM Customer WHERE Country != "USA"
2. Provide a query only showing the Customers from Brazil.
//SELECT *  FROM Customer WHERE Country = "Brazil"
3. Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.
//SELECT Customer.FirstName, Customer.LastName, InvoiceId, InvoiceDate, BillingCountry  FROM Customer JOIN Invoice ON Invoice.CustomerId = Customer.CustomerID WHERE Country = "Brazil"
4. Provide a query showing only the Employees who are Sales Agents.
//SELECT DISTINCT Employee.FirstName,Employee.LastName FROM Employee JOIN  Customer ON Customer.SupportRepId = EmployeeId 
5. Provide a query showing a unique list of billing countries from the Invoice table.
//SELECT DISTINCT BillingCountry FROM Invoice
6. Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name. 
//Select Employee.FirstName, EMployee.LastName, InvoiceId FROM Invoice JOIN Customer ON Invoice.CustomerId = Customer.CustomerId JOIN Employee on Customer.SupportRepId = Employee.EmployeeId
7. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers. 
//SELECT Invoice.Total, Customer.FirstName, Customer.LastName, Customer.Country, Customer.SupportRepId FROM Invoice Join Customer ON Invoice.CustomerId = Customer.CustomerId JOIN Employee ON Employee.employeeId = CUstomer.SupportRepId
8. How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?
//83(SELECT InvoiceId, InvoiceDate FROM Invoice where InvoiceDate LIKE '2011%') 83 (SELECT InvoiceId, InvoiceDate, COUNT(*) RunningTotal FROM Invoice where InvoiceDate LIKE '2011%') $449.46 (SELECT InvoiceId, InvoiceDate, SUM(Total) RunningTotal FROM Invoice where InvoiceDate LIKE '2009%') %469.58 (SELECT InvoiceId, InvoiceDate, SUM(Total) RunningTotal FROM Invoice where InvoiceDate LIKE '2011%')
10. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.
//SELECT InvoiceId, Count(*) Count FROM InvoiceLine where InvoiceId = 37
11. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: [GROUP BY](http://www.sqlite.org/lang_select.html#resultset)
//SELECT InvoiceId, Count(*) Count FROM InvoiceLine GROUP By InvoiceId
12. Provide a query that includes the track name with each invoice line item.
//SELECT InvoiceId, Track.Name FROM InvoiceLine JOIN Track ON InvoiceLine.TrackId = Track.TrackId
13. Provide a query that includes the purchased track name AND artist name with each invoice line item.
//SELECT InvoiceId, Track.Name, Artist.Name FROM InvoiceLine JOIN Track ON InvoiceLine.TrackId = Track.TrackId JOIN Album ON Track.AlbumId = Album.AlbumId JOIN Artist ON Album.ArtistId = Artist.ArtistId
14. Provide a query that shows the # of invoices per country. HINT: [GROUP BY](http://www.sqlite.org/lang_select.html#resultset)
//SELECT BillingCountry, Count(*) Count FROM Invoice GROUP BY BillingCountry
15. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be include on the resulant table.
//SELECT Playlist.Name, Count(*) Count FROM Track JOIN PlaylistTrack ON PlaylistTrack.TrackId = Track.TrackId JOIN Playlist ON Playlist.PlaylistId = PlaylistTrack.PlaylistId GROUP BY Playlist.Name
16. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.
//SELECT Track.Name, Album.Title, MediaType.Name, Genre.Name FROM Track JOIN Album ON Track.AlbumId = Album.AlbumId JOIN MediaType ON MediaType.MediaTypeId = Track.MediaTypeId JOIN Genre ON Genre.GenreId = Track.GenreId
17. Provide a query that shows all Invoices but includes the # of invoice line items.
//SELECT InvoiceId, Count(*) Count FROM InvoiceLine GROUP By InvoiceId
18. Provide a query that shows total sales made by each sales agent.
//SELECT Employee.LastName, Employee.FirstName, SUM(Invoice.Total) FROM Employee JOIN Customer ON Employee.EmployeeId = Customer.SupportRepId JOIN Invoice ON Customer.CustomerId = Invoice.CustomerId GROUP BY EmployeeId
19. Which sales agent made the most in sales in 2009? HINT: [MAX](https://www.sqlite.org/lang_aggfunc.html#maxggunc)
//Steve Johnson (SELECT Employee.LastName, Employee.FirstName, SUM(Invoice.Total) FROM Employee JOIN Customer ON Employee.EmployeeId = Customer.SupportRepId JOIN Invoice ON Customer.CustomerId = Invoice.CustomerId GROUP BY EmployeeId)
21. Which sales agent made the most in sales over all?
//Jane Peacock (SELECT FirstName, LastName, MAX(TotalSales) FROM(SELECT SUM(Total) AS TotalSales, Employee.LastName, Employee.FirstName FROM Employee JOIN Customer ON Employee.EmployeeId = Customer.SupportRepId JOIN Invoice ON Customer.CustomerId = Invoice.CustomerId GROUP BY EmployeeId))
22. Provide a query that shows the # of customers assigned to each sales agent.
//SELECT Employee.FirstName, Employee.LastName, Count(*) FROM Customer JOIN Employee ON Employee.EmployeeID = CUstomer.SupportRepId GROUP BY SupportRepId
23. Provide a query that shows the total sales per country. Which country's customers spent the most?
//(SELECT BillingCountry, SUM(Total) FROM Invoice GROUP BY BillingCountry)- USA
24. Provide a query that shows the most purchased track of 2013.
//
25. Provide a query that shows the top 5 most purchased tracks over all.
//SELECT Track.Name, COUNT(InvoiceLineId) AS Total FROM InvoiceLine JOIN Track on Track.TrackId = InvoiceLine.TrackId JOIN Invoice ON Invoice.InvoiceId = InvoiceLine.InvoiceId GROUP BY Track.Name ORDER BY Total DESC LIMIT 5
26. Provide a query that shows the top 3 best selling artists.
//SELECT Artist.Name, COUNT(InvoiceLineId) AS NumSold FROM InvoiceLine JOIN Track on Track.TrackId = InvoiceLine.TrackId JOIN Invoice ON Invoice.InvoiceId = InvoiceLine.InvoiceId JOIN Album ON Album.AlbumID = Track.AlbumId JOIN artist ON Artist.ArtistID = Album.ArtistId GROUP BY Artist.Name ORDER BY NumSold DESC LIMIT 3
27. Provide a query that shows the most purchased Media Type.
//SELECT MediaType.Name, COUNT(InvoiceLineId) AS NumSold FROM InvoiceLine JOIN Track on Track.TrackId = InvoiceLine.TrackId JOIN MediaType ON MediaType.MediaTypeId = Track.MediaTypeId GROUP BY MediaType.Name ORDER BY NumSold DESC LIMIT 1