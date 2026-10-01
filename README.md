# TypeId Go

A Go implementation of [TypeID](https://github.com/jetify-com/typeid), which combines a type name with a [ULID](https://github.com/ulid/spec) to create globally unique, sortable, and human-readable identifiers.

## Features

- Format: `type_name_<ulid>` (e.g., `user_01h7xv8y5z9k7w2t4r3q6p8m9n`)
- Type name validation (lowercase alphanumeric characters and single underscores only)
- ULID generation and validation using [oklog/ulid/v2](https://github.com/oklog/ulid)
- Simple API for creating and parsing TypeIDs

## Installation

Install the package using `go get`:

```bash
go get github.com/pixeldump/typeid-go
```

## Usage

```go
package main

import (
	"fmt"

	typeid "github.com/pixeldump/typeid-go"
)

func main() {
	// Create a new TypeID for type "user"
	id, err := typeid.Make("user")
	if err != nil {
		panic(err)
	}
	fmt.Println(id.String()) // e.g., user_01h7xv8y5z9k7w2t4r3q6p8m9n
	fmt.Println(id.Type())   // user
	fmt.Println(id.Id())     // ULID part (lowercase)
	fmt.Println(id.Length()) // length of the full string

	// Parse an existing TypeID
	parsed, err := typeid.Parse("user", id.String())
	if err != nil {
		panic(err)
	}
	fmt.Println(parsed.String()) // same as original
}
```
