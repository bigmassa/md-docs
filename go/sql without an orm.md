# SQL Without an ORM

> Sometimes getting a database connection up and running can be a bit fiddly, we’ve all been there, and it can help to have an example to work from. This post aims to show you the complete basics of creating a database connection, forming a query to run and populating a struct with our resulting data.
>
> To do with we use the database/sql interface and load in the pq driver/library to actually do the work for us. We’re using QueryRow() which will only return the single row. If you need more than one row you can use Query() which returns multiple rows for you to turn each into a struct.

```go
package main

import (
	"database/sql"
	"fmt"
	"log"

	_ "github.com/lib/pq"
)

const (
	DB_DSN = "postgres://username:password@url.com:5432/dbName"
)

type User struct {
	ID       int
	Email    string
	Password string
}

func main() {

	// Create DB pool
	db, err := sql.Open("postgres", DB_DSN)
	if err != nil {
		log.Fatal("Failed to open a DB connection: ", err)
	}
	defer db.Close()

	// Create an empty user and make the sql query (using $1 for the parameter)
	var myUser User
	userSql := "SELECT id, email, password FROM users WHERE id = $1"

	err = db.QueryRow(userSql, 1).Scan(&myUser.ID, &myUser.Email, &myUser.Password)
	if err != nil {
		log.Fatal("Failed to execute query: ", err)
	}

	fmt.Printf("Hi %s, welcome back!\n", myUser.Email)
}
```

As a reference, this code uses a very basic schema structure:

```sql
CREATE TABLE users (
    id serial PRIMARY KEY,
    email VARCHAR (355) UNIQUE NOT NULL,
    password VARCHAR (50) NOT NULL
);
```