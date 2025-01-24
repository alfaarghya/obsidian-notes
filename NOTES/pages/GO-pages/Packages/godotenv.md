```bash
go get github.com/joho/godotenv
```
- `godotenv` is a Go package that loads environment variables from a `.env` file.
- It is similar to `dotenv` in the Node.js ecosystem.
- It allows developers to store sensitive information like API keys, database URIs, etc., in a `.env` file and load them into the application.

```GO
package main

import (
  "fmt"
  "log"
  "os"

  "github.com/joho/godotenv"
)

func main() {
  err := godotenv.Load(".env")
  if err != nil {
    log.Fatal("Error loading .env file")
  }

  MONGODB_URI := os.Getenv("MONGODB_URI")
}
```
