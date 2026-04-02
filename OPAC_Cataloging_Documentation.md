## OPAC and Cataloging Documentation
This file will document how I set up my OPAC and Cataloging modules. 

## Introduction
To begin, an OPAC is an online public access catalog, which is a web-accessible interface that facilitates user information retrieval.

## Relational Database Structure
Relational databases are the key feature of the OPAC. The relational database stores all of the bibliographic records created for the library's materials. When connected to the OPAC, the relational database can be browsed or searched by users through the OPAC interface.

## Step-by-Step Setup
Here are instructions for the setup.

### Connection to the database
These steps will cover creating the OPAC web-based interface, and connecting it to the database.

1. Navigate to the document root, then create the page mylibrary.html
``` cd /var/www/html ```
``` sudo tilde mylibrary.html ```

2. Insert the provided code.
``` TYPE html>
<html>
    <head>
            <meta charset="UTF-8">
	            <title>MySQL Server Example</title>
		        </head>
			<body>
			
			    <h1>A Basic OPAC</h1>
			    
			        <p>In the form below, <b>optionally</b> enter text in the search field.
				    Your search query will search by author, title, or publisher.
				        Capitalization is usually not necessary on default case-insensitive MySQL collations.
					    It's okay to enter partial information, like part of an author's, title's, or publisher's name.</p>
					    
					        <p>You can leave the search field empty and only enter dates.
						    Regardless, both start and end dates are required for all searches.
						        You can use the date fields to limit results, too.
							    I added some extra records, which you can view to know what you can query:</p>
							    
							        <p><a href="opac.php">OPAC</a></p>
								
								    <p>This is very much a toy, stripped down
								        <a href="https://en.wikipedia.org/wiki/Online_public_access_catalog">OPAC</a>.
									    The records are basic.
									        Not only do they not conform to <a href="https://www.loc.gov/marc/">MARC</a>,
										    they don't even conform to something as simple as <a href="https://www.dublincore.org/">Dublin Core</a>.</p>
										    
										        <p>I also don't provide options to select different fields, like author, title, or publisher fields.
											    Instead the search field below searches key bibliographic fields (author, title, publisher) in our <b>books</b> table.</p>
											    
											        <p>The key idea is to get a sense of how an OPAC works, though.</p>
												
												    <h2>My Basic Library OPAC</h2>
												    
												        <form method="post" action="search.php">
													        <label for="search">Search Terms (optional):</label>
														        <input type="text" name="search" id="search">
															        
																        <br>
																	        
																		        <label for="start_date">Start Date:</label>
																			        <input type="date" name="start_date" id="start_date" required>
																				        
																					        <br>
																						        
																							        <label for="end_date">End Date:</label>
																								        <input type="date" name="end_date" id="end_date" required>
																									        
																										        <br>
																											        
																												        <input type="submit" value="Search">
																													    </form>
																													    
																													    </body>
																													    </html>
```			


3. Create the search.php file, then insert the provided code.
```
TYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
	    <title>Search Results</title>
	    <style>
	        table {
		        border-collapse: collapse;
			        width: 100%;
				    }
				        th, td {
					        border: 1px solid black;
						        padding: 8px;
							        text-align: left;
								    }
								    </style>
								    </head>
								    <body>
								    
								        <h1>Search Results</h1>
									
									    <?php
									        // Load MySQL credentials
										    require_once '/var/www/login.php';
										    
										        // Enable MySQL error reporting
											    mysqli_report(MYSQLI_REPORT_ERROR | MYSQLI_REPORT_STRICT);
											    
											        // Establish connection
												    $conn = new mysqli($db_hostname, $db_username, $db_password, $db_database);
												        if ($conn->connect_error) {
													        die("Connection failed: " . $conn->connect_error);
														    }
														    
														        if ($_SERVER["REQUEST_METHOD"] == "POST") {
															        $search = trim($_POST['search']);
																        $start_date = $_POST['start_date'];
																	        $end_date = $_POST['end_date'];
																		
																		        // Prepared statement to prevent SQL injection
																			        $stmt = $conn->prepare("SELECT id, author, title, publisher, copyright FROM books 
																				                                WHERE (author LIKE ? OR title LIKE ? OR publisher LIKE ?) 
																								                                AND copyright BETWEEN ? AND ?");
																												
																												        // Use wildcard search
																													        $search_param = "%$search%";
																														        $stmt->bind_param("sssss", $search_param, $search_param, $search_param, $start_date, $end_date);
																															        $stmt->execute();
																																        $result = $stmt->get_result();
																																	
																																	        if ($result->num_rows > 0) {
																																		            echo "<table>";
																																			                echo "<tr><th>ID</th><th>Author</th><th>Title</th><th>Publisher</th><th>Copyright</th></tr>";
																																					
																																					            while ($row = $result->fetch_assoc()) {
																																						                    echo "<tr>";
																																								                    echo "<td>" . htmlspecialchars($row["id"]) . "</td>";
																																										                    echo "<td>" . htmlspecialchars($row["author"]) . "</td>";
																																												                    echo "<td>" . htmlspecialchars($row["title"]) . "</td>";
																																														                    echo "<td>" . htmlspecialchars($row["publisher"]) . "</td>";
																																																                    echo "<td>" . htmlspecialchars($row["copyright"]) . "</td>";
																																																		                    echo "</tr>";
																																																				                }
																																																						
																																																						            echo "</table>";
																																																							            } else {
																																																								                echo "<p>No results found.</p>";
																																																										        }
																																																											
																																																											        $stmt->close();
																																																												    }
																																																												    
																																																												        $conn->close();
																																																													    ?>
																																																													    
																																																													        <p><a href="mylibrary.html">Return to search page</a></p>
																																																														
																																																														</body>
																																																														</html>
																																																														
```																																																
### Cataloging Module Structure
These steps will provide instructions for creating the cataloging module

1. Create a new directory for the cataloging module
``` cd /var/www/html  ```
``` sudo mkdir cataloging ```

2. Create the index.html file and add the provided coding
``` cd cataloging ```
``` sudo tilde index.html ```
``` TYPE html>
<html>
<head>
    <title>Enter Records</title>
</head>
<body>
    <h1>OPAC Library Administration</h1>
	
    <p>This is the library administration page for entering records into the OPAC.</p>
    <p>Please do not use this page unless you are an authorized cataloger.</p>
		
    <form action="insert.php" method="post">
	<label for="author">Author:</label>
	<input type="text" name="author" id="author" required><br><br>
				    
	<label for="title">Book Title:</label>
	<input type="text" name="title" id="title" required><br><br>
						    
	<label for="publisher">Publisher:</label>
	<input type="text" name="publisher" id="publisher" required><br><br>
								    
	<label for="copyright">Copyright:</label>
	<input type="date" name="copyright" id="copyright" required>
										    
	<input type="submit" value="Submit">
    </form>
</body>
</html> ```

3. Create the insert.php file, then insert the provided code.
``` cd /var/www/html/ ```
``` <!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cataloging: Data Entry</title>
</head>
<body>

<h1>Cataloging: Data Entry</h1>

<?php

// Load MySQL credentials
require_once '/var/www/login.php';

// Enable MySQL error reporting
mysqli_report(MYSQLI_REPORT_ERROR | MYSQLI_REPORT_STRICT);

// Establish connection
$conn = new mysqli($db_hostname, $db_username, $db_password, $db_database);
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $author = trim($_POST["author"] ?? "");
    $title = trim($_POST["title"] ?? "");
    $publisher = trim($_POST["publisher"] ?? "");
    $copyright = $_POST["copyright"] ?? "";

    if ($author === "" || $title === "" || $publisher === "" || $copyright === "") {
        echo "All fields are required.";
    } elseif (!preg_match('/^\d{4}-\d{2}-\d{2}$/', $copyright)) {
        echo "Copyright date must use YYYY-MM-DD format.";
    } else {
        // Prepare and bind SQL statement
        $stmt = $conn->prepare("INSERT INTO books (author, title, publisher, copyright) VALUES (?, ?, ?, ?)");
        $stmt->bind_param("ssss", $author, $title, $publisher, $copyright);

        if ($stmt->execute() === TRUE) {
            echo "New record created successfully";
        } else {
            echo "Error: " . $stmt->error;
        }
        $stmt->close();
    }
} else {
    echo "Please submit records using the cataloging form.";
}

// Close connection
$conn->close();
?>

<p><a href='index.html'>Return to Cataloging Page</a></p>
<p><a href='../mylibrary.html'>Return to Library Home Page</a></p>
</body>
</html>
```
The provided code utilizes the login.php file to load our MySQL credentials. Then, the code allows the user to insert their values into the books table in the relational database.

### Configuration
Security is an important configuration step to prevent unauthorized access.

1. Create an authentication file in our Apache2 configuration files
``` smysqludo htpasswd -c /etc/apache2/.htpasswd libcat ```

2. Modify the Apache2 configuration file to use the htpasswd file for control access.
``` sudo tilde /etc/apache2/apache2.conf ```

3. Move to the cataloging directory, then create a file for the access web request. Add the provided content to .htaccess.
``` cd /var/www/html/cataloging ```
``` sudo tilde .htaccess ```
``` 
AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```

4. Verify the configuration file, then restart the server and check it's status.
``` sudo apachectl configtest ```
``` sudo systemctl restart apache2 ```
``` sudo systemctl status apache2 ```

### Real-world Updates
In a real-world OPAC, note that the security measures and cataloging module would be much more robust.
* The security needed for our OPAC is simple compared to the multiple security measures that would be necessary for a real library.
* Additionally, the cataloging module shows the basic, underlying idea of cataloging data transferred from a web-based browser to the relational database. For a real library, though, more data would be required in the bibliographic records to meet professional metadata standards.

### Search and Retrieval
Search and retrieval in the OPAC are facilitated through the web-browser.

1. Navigate to ``` http://34.132.167.164/mylibrary.html ```

2. To retrieve a specific material from the database, use the search term or end and start date fields to input the correlated record data.

## Key Details
One important detail is to limit permissions and ownership of the Apache2 server to the Linux server.

1. Retrieve the  user's information using the following:
```
grep "www-data" /etc/passwd
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
```

2. Change the ownership of the Apache2 server's document root to the Linux server user
```
sudo chown :www-data /var/www/html
```

3. Set the setgid bit of the document root. This ensures new files inherit these ownership rules.
```
sudo find /var/www/html -type d -exec chmod g+s {} +
```

## Using Documentation
While exploring the relational database in MySQL, I referenced the MySQL Server reference documentation to research the functions and operators section and the stored objects section. These seemed to be related to the uses we have for MySQL, but I didn't really find anything applicable. It is still interesting to see the variety of functions and commands for this program, though, even though they are out of our scope.  

