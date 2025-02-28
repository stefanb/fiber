---
id: recover
title: Recover
---

Recover middleware for [Fiber](https://github.com/gofiber/fiber) that recovers from panics anywhere in the stack chain and handles the control to the centralized [ErrorHandler](https://docs.gofiber.io/guide/error-handling).

## Signatures

```go
func New(config ...Config) fiber.Handler
```

## Examples

Import the middleware package that is part of the Fiber web framework

```go
import (
  "github.com/gofiber/fiber/v2"
  "github.com/gofiber/fiber/v2/middleware/recover"
)
```

After you initiate your Fiber app, you can use the following possibilities:

```go
// Initialize default config
app.Use(recover.New())

// This panic will be caught by the middleware
app.Get("/", func(c *fiber.Ctx) error {
    panic("I'm an error")
})
```

## Config

```go
// Config defines the config for middleware.
type Config struct {
    // Next defines a function to skip this middleware when returned true.
    //
    // Optional. Default: nil
    Next func(c *fiber.Ctx) bool

    // EnableStackTrace enables handling stack trace
    //
    // Optional. Default: false
    EnableStackTrace bool

    // StackTraceHandler defines a function to handle stack trace
    //
    // Optional. Default: defaultStackTraceHandler
    StackTraceHandler func(c *fiber.Ctx, e interface{})
}
```

## Default Config

```go
var ConfigDefault = Config{
    Next:              nil,
    EnableStackTrace:  false,
    StackTraceHandler: defaultStackTraceHandler,
}
```
