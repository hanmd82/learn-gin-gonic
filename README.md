# Learn Gin

### Setup
```go
touch main.go
go mod init github.com/hanmd82/learn-gin-gonic
```

### Notes on Gin Middleware
Context is shared between all of the middleware in a single request, and the main handler.

```go
func (c *Context) Get(key string) (value interface{}, exists bool)
func (c *Context) MustGet(key string) interface{}
func (c *Context) Set(key string, value interface{})

func (c *Context) Next() # pass to next middleware down the chain
func (c *Context) Abort() # AbortWithStatus AbortWithError
```

Pre-packaged middleware in Gin
- BasicAuth
- Bind: read values out of HTTP request and bind to an object
- ErrorLogger / Logger
- Recovery: recover from panic

`gin.New()` no middleware included

`gin.Default()`: comes with Logger, Recovery middleware

How to use custom middleware with Gin
```go
# handler function signature
type HandlerFunc func(*gin.Context)

# register middleware
func (group *RouterGroup) Use(middleware ...HandlerFunc) IRoutes
func (group *RouterGroup) GET(relativePath string, handlers ...HandlerFunc) IRoutes
```
