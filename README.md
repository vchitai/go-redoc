# go-redoc

[![GoDoc](https://godoc.org/github.com/vchitai/go-redoc?status.svg)](https://godoc.org/github.com/vchitai/go-redoc)
[![Go Report Card](https://goreportcard.com/badge/github.com/vchitai/go-redoc?_=1)](https://goreportcard.com/report/github.com/vchitai/go-redoc?_=1)

`go-redoc` is an embedded OpenAPI documentation ui for Go using [ReDoc](https://github.com/ReDocly/redoc) and Go's [1.16+'s embed package](https://golang.org/pkg/embed/), with middleware implementations for: `net/http`, `gin`, `fiber`, and `echo`.

The template is based on the ReDoc's [bundle template](https://github.com/ReDocly/redoc/blob/master/cli/template.hbs) with the script already placed in the html instead of depending on a CDN.

This package does not generate openapi spec file. Check [this example](_examples/gen) for using code generation with swag.

## Usage

```go
import "github.com/vchitai/go-redoc"

...

doc := redoc.Redoc{
    Title:       "Example API",
    Description: "Example API Description",
    SpecFile:    "./openapi.json", // "./openapi.yaml"
    SpecPath:    "/openapi.json",  // "/openapi.yaml"
    DocsPath:    "/docs",
}
```

- `net/http`

```go
import (
	"net/http"
	"github.com/vchitai/go-redoc"
)

...

http.ListenAndServe(address, doc.Handler())
```

- `gin`

```go
import (
	"github.com/gin-gonic/gin"
	"github.com/vchitai/go-redoc"
	ginredoc "github.com/vchitai/go-redoc/gin"
)

...

r := gin.New()
r.Use(ginredoc.New(doc))
```

- `echo`

```go
import (
	"github.com/labstack/echo/v4"
	"github.com/vchitai/go-redoc"
	echoredoc "github.com/vchitai/go-redoc/echo"
)

...

r := echo.New()
r.Use(echoredoc.New(doc))
```

- `fiber`

```go
import (
	"github.com/gofiber/fiber/v2"
	"github.com/vchitai/go-redoc"
	fiberredoc "github.com/vchitai/go-redoc/fiber"
)

...

r := fiber.New()
r.Use(fiberredoc.New(doc))
```

See [examples](/_examples)
