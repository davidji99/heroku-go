# Heroku Platform API

[![GoDoc](https://godoc.org/github.com/heroku/heroku-go?status.svg)](https://godoc.org/github.com/heroku/heroku-go)

An API client interface for Heroku Platform API for the Go (golang) programming language.

## Usage

	$ go mod init myproj
	$ cd myproj

## Example

```go
package main

import (
	"context"
	"flag"
	"fmt"
	"log"

	heroku "github.com/davidji99/heroku-go/v5"
)

var (
	username = flag.String("username", "", "api username")
	password = flag.String("password", "", "api password")
)

func main() {
	log.SetFlags(0)
	flag.Parse()

	heroku.DefaultTransport.Username = *username
	heroku.DefaultTransport.Password = *password

	h := heroku.NewService(heroku.DefaultClient)
	addons, err := h.AddOnList(context.TODO(), &heroku.ListRange{Field: "name"})
	if err != nil {
		log.Fatal(err)
	}
	for _, addon := range addons {
		fmt.Println(addon.Name)
	}
}
```

	$ go build