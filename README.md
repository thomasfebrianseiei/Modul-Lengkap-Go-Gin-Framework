# Modul Lengkap Go & Gin Framework
## Basic Go sampai ORM dengan PostgreSQL dan MongoDB

---

## Table of Contents
1. [Pengenalan Go](#pengenalan-go)
2. [Instalasi dan Setup](#instalasi-dan-setup)
3. [Dasar-dasar Go](#dasar-dasar-go)
4. [Gin Framework](#gin-framework)
5. [ORM dengan GORM (PostgreSQL)](#orm-dengan-gorm-postgresql)
6. [ODM dengan MongoDB](#odm-dengan-mongodb)
7. [Proyek Praktik](#proyek-praktik)

---

## Pengenalan Go

Go (Golang) adalah bahasa pemrograman open-source yang dikembangkan oleh Google. Go dirancang untuk menjadi bahasa yang simple, cepat, dan mudah dipelajari.

### Keunggulan Go:
- **Performance tinggi** - Compiled language dengan garbage collector
- **Concurrency** - Goroutines dan channels untuk concurrent programming
- **Simple syntax** - Mudah dipelajari dan dipahami
- **Cross-platform** - Dapat berjalan di berbagai OS
- **Rich standard library** - Library bawaan yang lengkap

---

## Instalasi dan Setup

### 1. Install Go
```bash
# Download dari https://golang.org/dl/
# Atau menggunakan package manager

# Ubuntu/Debian
sudo apt update
sudo apt install golang-go

# macOS
brew install go

# Windows
# Download installer dari website resmi
```

### 2. Verifikasi Instalasi
```bash
go version
```

### 3. Setup Environment
```bash
# Tambahkan ke ~/.bashrc atau ~/.zshrc
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```

### 4. Inisialisasi Project
```bash
mkdir my-go-project
cd my-go-project
go mod init my-go-project
```

---

## Dasar-dasar Go

### 1. Hello World
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

### 2. Variables dan Types
```go
package main

import "fmt"

func main() {
    // Deklarasi variable
    var name string = "John"
    var age int = 30
    var height float64 = 175.5
    var isActive bool = true
    
    // Short declaration
    city := "Jakarta"
    
    // Multiple variables
    var (
        firstName = "John"
        lastName  = "Doe"
        email     = "john@example.com"
    )
    
    fmt.Printf("Name: %s, Age: %d, Height: %.1f, Active: %t\n", 
               name, age, height, isActive)
    fmt.Printf("City: %s\n", city)
    fmt.Printf("Full name: %s %s, Email: %s\n", 
               firstName, lastName, email)
}
```

### 3. Data Types
```go
package main

import "fmt"

func main() {
    // Numeric types
    var i8 int8 = 127
    var i16 int16 = 32767
    var i32 int32 = 2147483647
    var i64 int64 = 9223372036854775807
    
    var ui8 uint8 = 255
    var ui16 uint16 = 65535
    
    var f32 float32 = 3.14
    var f64 float64 = 3.141592653589793
    
    // String
    var str string = "Hello Go"
    
    // Boolean
    var flag bool = true
    
    // Array
    var numbers [5]int = [5]int{1, 2, 3, 4, 5}
    
    // Slice
    var fruits []string = []string{"apple", "banana", "orange"}
    
    // Map
    var person map[string]interface{} = map[string]interface{}{
        "name": "John",
        "age":  30,
        "city": "Jakarta",
    }
    
    fmt.Printf("Numbers: %v\n", numbers)
    fmt.Printf("Fruits: %v\n", fruits)
    fmt.Printf("Person: %v\n", person)
}
```

### 4. Control Structures
```go
package main

import "fmt"

func main() {
    // If-else
    age := 18
    if age >= 18 {
        fmt.Println("Adult")
    } else {
        fmt.Println("Minor")
    }
    
    // If with initialization
    if score := 85; score >= 90 {
        fmt.Println("A")
    } else if score >= 80 {
        fmt.Println("B")
    } else {
        fmt.Println("C")
    }
    
    // Switch
    day := "Monday"
    switch day {
    case "Monday":
        fmt.Println("Start of work week")
    case "Friday":
        fmt.Println("TGIF!")
    case "Saturday", "Sunday":
        fmt.Println("Weekend")
    default:
        fmt.Println("Regular day")
    }
    
    // For loops
    // Traditional for
    for i := 0; i < 5; i++ {
        fmt.Printf("Count: %d\n", i)
    }
    
    // While-like for
    count := 0
    for count < 3 {
        fmt.Printf("While count: %d\n", count)
        count++
    }
    
    // Range
    fruits := []string{"apple", "banana", "orange"}
    for index, fruit := range fruits {
        fmt.Printf("Index: %d, Fruit: %s\n", index, fruit)
    }
    
    // Range with map
    person := map[string]int{"John": 30, "Jane": 25, "Bob": 35}
    for name, age := range person {
        fmt.Printf("Name: %s, Age: %d\n", name, age)
    }
}
```

### 5. Functions
```go
package main

import "fmt"

// Basic function
func greet(name string) string {
    return "Hello, " + name
}

// Multiple parameters
func add(a, b int) int {
    return a + b
}

// Multiple return values
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("division by zero")
    }
    return a / b, nil
}

// Named return values
func calculate(a, b int) (sum, product int) {
    sum = a + b
    product = a * b
    return // naked return
}

// Variadic function
func sum(numbers ...int) int {
    total := 0
    for _, num := range numbers {
        total += num
    }
    return total
}

// Higher-order function
func operation(a, b int, op func(int, int) int) int {
    return op(a, b)
}

func main() {
    // Function calls
    fmt.Println(greet("World"))
    fmt.Println(add(5, 3))
    
    result, err := divide(10, 2)
    if err != nil {
        fmt.Printf("Error: %v\n", err)
    } else {
        fmt.Printf("Result: %.2f\n", result)
    }
    
    s, p := calculate(4, 5)
    fmt.Printf("Sum: %d, Product: %d\n", s, p)
    
    fmt.Printf("Sum of numbers: %d\n", sum(1, 2, 3, 4, 5))
    
    // Anonymous function
    multiply := func(a, b int) int {
        return a * b
    }
    
    fmt.Printf("Operation result: %d\n", operation(6, 7, multiply))
}
```

### 6. Structs dan Methods
```go
package main

import "fmt"

// Struct definition
type Person struct {
    FirstName string
    LastName  string
    Age       int
    Email     string
}

// Method with receiver
func (p Person) FullName() string {
    return p.FirstName + " " + p.LastName
}

// Method with pointer receiver (can modify struct)
func (p *Person) SetAge(age int) {
    p.Age = age
}

// Method with pointer receiver
func (p *Person) HaveBirthday() {
    p.Age++
}

// Constructor function
func NewPerson(firstName, lastName string, age int, email string) *Person {
    return &Person{
        FirstName: firstName,
        LastName:  lastName,
        Age:       age,
        Email:     email,
    }
}

func main() {
    // Create struct instance
    person1 := Person{
        FirstName: "John",
        LastName:  "Doe",
        Age:       30,
        Email:     "john@example.com",
    }
    
    // Using constructor
    person2 := NewPerson("Jane", "Smith", 25, "jane@example.com")
    
    fmt.Printf("Person 1: %+v\n", person1)
    fmt.Printf("Person 1 Full Name: %s\n", person1.FullName())
    
    fmt.Printf("Person 2: %+v\n", *person2)
    fmt.Printf("Person 2 Full Name: %s\n", person2.FullName())
    
    // Modify using pointer method
    person2.SetAge(26)
    person2.HaveBirthday()
    fmt.Printf("Person 2 after birthday: %+v\n", *person2)
}
```

### 7. Interfaces
```go
package main

import "fmt"

// Interface definition
type Shape interface {
    Area() float64
    Perimeter() float64
}

// Struct that implements Shape
type Rectangle struct {
    Width  float64
    Height float64
}

func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

func (r Rectangle) Perimeter() float64 {
    return 2 * (r.Width + r.Height)
}

// Another struct that implements Shape
type Circle struct {
    Radius float64
}

func (c Circle) Area() float64 {
    return 3.14159 * c.Radius * c.Radius
}

func (c Circle) Perimeter() float64 {
    return 2 * 3.14159 * c.Radius
}

// Function that accepts interface
func printShapeInfo(s Shape) {
    fmt.Printf("Area: %.2f, Perimeter: %.2f\n", s.Area(), s.Perimeter())
}

func main() {
    rectangle := Rectangle{Width: 5, Height: 3}
    circle := Circle{Radius: 4}
    
    printShapeInfo(rectangle)
    printShapeInfo(circle)
    
    // Slice of interfaces
    shapes := []Shape{rectangle, circle}
    for i, shape := range shapes {
        fmt.Printf("Shape %d: ", i+1)
        printShapeInfo(shape)
    }
}
```

### 8. Error Handling
```go
package main

import (
    "errors"
    "fmt"
)

// Custom error type
type ValidationError struct {
    Field   string
    Message string
}

func (e ValidationError) Error() string {
    return fmt.Sprintf("validation error on field '%s': %s", e.Field, e.Message)
}

// Function that returns error
func validateAge(age int) error {
    if age < 0 {
        return ValidationError{Field: "age", Message: "age cannot be negative"}
    }
    if age > 150 {
        return ValidationError{Field: "age", Message: "age cannot be greater than 150"}
    }
    return nil
}

// Function with multiple error scenarios
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}

func main() {
    // Error handling
    ages := []int{25, -5, 200, 45}
    
    for _, age := range ages {
        if err := validateAge(age); err != nil {
            fmt.Printf("Error for age %d: %v\n", age, err)
        } else {
            fmt.Printf("Age %d is valid\n", age)
        }
    }
    
    // Multiple return with error
    result, err := divide(10, 2)
    if err != nil {
        fmt.Printf("Error: %v\n", err)
    } else {
        fmt.Printf("Result: %.2f\n", result)
    }
    
    result, err = divide(10, 0)
    if err != nil {
        fmt.Printf("Error: %v\n", err)
    } else {
        fmt.Printf("Result: %.2f\n", result)
    }
}
```

---

## Gin Framework

Gin adalah HTTP web framework yang ditulis dalam Go. Gin memiliki performance yang sangat baik dan API yang mudah digunakan.

### 1. Instalasi Gin
```bash
go mod init gin-example
go get github.com/gin-gonic/gin
```

### 2. Basic Gin Server
```go
package main

import (
    "net/http"
    
    "github.com/gin-gonic/gin"
)

func main() {
    // Create Gin router
    router := gin.Default()
    
    // Basic route
    router.GET("/", func(c *gin.Context) {
        c.JSON(http.StatusOK, gin.H{
            "message": "Hello, Gin!",
        })
    })
    
    // Start server on port 8080
    router.Run(":8080")
}
```

### 3. Routing
```go
package main

import (
    "net/http"
    "strconv"
    
    "github.com/gin-gonic/gin"
)

type User struct {
    ID   int    `json:"id"`
    Name string `json:"name"`
    Email string `json:"email"`
}

var users = []User{
    {ID: 1, Name: "John Doe", Email: "john@example.com"},
    {ID: 2, Name: "Jane Smith", Email: "jane@example.com"},
}

func main() {
    router := gin.Default()
    
    // GET all users
    router.GET("/users", getUsers)
    
    // GET user by ID
    router.GET("/users/:id", getUserByID)
    
    // POST create user
    router.POST("/users", createUser)
    
    // PUT update user
    router.PUT("/users/:id", updateUser)
    
    // DELETE user
    router.DELETE("/users/:id", deleteUser)
    
    // Route group
    api := router.Group("/api/v1")
    {
        api.GET("/health", healthCheck)
        api.GET("/status", getStatus)
    }
    
    router.Run(":8080")
}

func getUsers(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{
        "data": users,
    })
}

func getUserByID(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.Atoi(idParam)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }
    
    for _, user := range users {
        if user.ID == id {
            c.JSON(http.StatusOK, gin.H{
                "data": user,
            })
            return
        }
    }
    
    c.JSON(http.StatusNotFound, gin.H{
        "error": "User not found",
    })
}

func createUser(c *gin.Context) {
    var newUser User
    
    if err := c.ShouldBindJSON(&newUser); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    // Generate new ID
    newUser.ID = len(users) + 1
    users = append(users, newUser)
    
    c.JSON(http.StatusCreated, gin.H{
        "message": "User created successfully",
        "data":    newUser,
    })
}

func updateUser(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.Atoi(idParam)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }
    
    var updatedUser User
    if err := c.ShouldBindJSON(&updatedUser); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    for i, user := range users {
        if user.ID == id {
            updatedUser.ID = id
            users[i] = updatedUser
            c.JSON(http.StatusOK, gin.H{
                "message": "User updated successfully",
                "data":    updatedUser,
            })
            return
        }
    }
    
    c.JSON(http.StatusNotFound, gin.H{
        "error": "User not found",
    })
}

func deleteUser(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.Atoi(idParam)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }
    
    for i, user := range users {
        if user.ID == id {
            users = append(users[:i], users[i+1:]...)
            c.JSON(http.StatusOK, gin.H{
                "message": "User deleted successfully",
            })
            return
        }
    }
    
    c.JSON(http.StatusNotFound, gin.H{
        "error": "User not found",
    })
}

func healthCheck(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{
        "status": "healthy",
    })
}

func getStatus(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{
        "status": "running",
        "version": "1.0.0",
    })
}
```

### 4. Middleware
```go
package main

import (
    "fmt"
    "log"
    "net/http"
    "time"
    
    "github.com/gin-gonic/gin"
)

// Custom logging middleware
func Logger() gin.HandlerFunc {
    return func(c *gin.Context) {
        start := time.Now()
        path := c.Request.URL.Path
        raw := c.Request.URL.RawQuery
        
        // Process request
        c.Next()
        
        // Log request details
        latency := time.Since(start)
        clientIP := c.ClientIP()
        method := c.Request.Method
        statusCode := c.Writer.Status()
        
        if raw != "" {
            path = path + "?" + raw
        }
        
        log.Printf("[%s] %s %s %d %v",
            clientIP, method, path, statusCode, latency)
    }
}

// Authentication middleware
func AuthMiddleware() gin.HandlerFunc {
    return func(c *gin.Context) {
        token := c.GetHeader("Authorization")
        
        if token == "" {
            c.JSON(http.StatusUnauthorized, gin.H{
                "error": "Authorization header required",
            })
            c.Abort()
            return
        }
        
        // Simple token validation (in real app, use JWT or similar)
        if token != "Bearer secret-token" {
            c.JSON(http.StatusUnauthorized, gin.H{
                "error": "Invalid token",
            })
            c.Abort()
            return
        }
        
        // Set user info in context
        c.Set("user", "john_doe")
        c.Next()
    }
}

// CORS middleware
func CORSMiddleware() gin.HandlerFunc {
    return func(c *gin.Context) {
        c.Writer.Header().Set("Access-Control-Allow-Origin", "*")
        c.Writer.Header().Set("Access-Control-Allow-Credentials", "true")
        c.Writer.Header().Set("Access-Control-Allow-Headers", "Content-Type, Content-Length, Accept-Encoding, X-CSRF-Token, Authorization, accept, origin, Cache-Control, X-Requested-With")
        c.Writer.Header().Set("Access-Control-Allow-Methods", "POST, OPTIONS, GET, PUT, DELETE")
        
        if c.Request.Method == "OPTIONS" {
            c.AbortWithStatus(204)
            return
        }
        
        c.Next()
    }
}

func main() {
    router := gin.New()
    
    // Use custom middleware
    router.Use(Logger())
    router.Use(CORSMiddleware())
    
    // Public routes
    router.GET("/", func(c *gin.Context) {
        c.JSON(http.StatusOK, gin.H{
            "message": "Public endpoint",
        })
    })
    
    // Protected routes group
    protected := router.Group("/api")
    protected.Use(AuthMiddleware())
    {
        protected.GET("/profile", func(c *gin.Context) {
            user, _ := c.Get("user")
            c.JSON(http.StatusOK, gin.H{
                "message": "Protected endpoint",
                "user":    user,
            })
        })
        
        protected.GET("/dashboard", func(c *gin.Context) {
            c.JSON(http.StatusOK, gin.H{
                "message": "Dashboard data",
                "data":    []string{"item1", "item2", "item3"},
            })
        })
    }
    
    router.Run(":8080")
}
```

### 5. Request Validation
```go
package main

import (
    "net/http"
    
    "github.com/gin-gonic/gin"
    "github.com/go-playground/validator/v10"
)

type CreateUserRequest struct {
    Name     string `json:"name" binding:"required,min=2,max=50"`
    Email    string `json:"email" binding:"required,email"`
    Age      int    `json:"age" binding:"required,min=18,max=100"`
    Password string `json:"password" binding:"required,min=8"`
}

type UpdateUserRequest struct {
    Name  string `json:"name" binding:"omitempty,min=2,max=50"`
    Email string `json:"email" binding:"omitempty,email"`
    Age   int    `json:"age" binding:"omitempty,min=18,max=100"`
}

// Custom validation function
func validatePassword(fl validator.FieldLevel) bool {
    password := fl.Field().String()
    // Check if password contains at least one number
    hasNumber := false
    for _, char := range password {
        if char >= '0' && char <= '9' {
            hasNumber = true
            break
        }
    }
    return hasNumber
}

func main() {
    router := gin.Default()
    
    // Register custom validator
    if v, ok := binding.Validator.Engine().(*validator.Validate); ok {
        v.RegisterValidation("password", validatePassword)
    }
    
    router.POST("/users", createUser)
    router.PUT("/users/:id", updateUser)
    
    router.Run(":8080")
}

func createUser(c *gin.Context) {
    var req CreateUserRequest
    
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error":   "Validation failed",
            "details": err.Error(),
        })
        return
    }
    
    // Process user creation
    user := gin.H{
        "id":    1,
        "name":  req.Name,
        "email": req.Email,
        "age":   req.Age,
    }
    
    c.JSON(http.StatusCreated, gin.H{
        "message": "User created successfully",
        "data":    user,
    })
}

func updateUser(c *gin.Context) {
    id := c.Param("id")
    
    var req UpdateUserRequest
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error":   "Validation failed",
            "details": err.Error(),
        })
        return
    }
    
    // Process user update
    c.JSON(http.StatusOK, gin.H{
        "message": "User updated successfully",
        "id":      id,
        "data":    req,
    })
}
```

---

## ORM dengan GORM (PostgreSQL)

GORM adalah ORM library yang populer untuk Go. GORM mendukung auto-migration dan berbagai database termasuk PostgreSQL.

### 1. Instalasi Dependencies
```bash
go get -u gorm.io/gorm
go get -u gorm.io/driver/postgres
go get -u github.com/gin-gonic/gin
```

### 2. Database Configuration
```go
package main

import (
    "fmt"
    "log"
    "os"
    
    "gorm.io/driver/postgres"
    "gorm.io/gorm"
    "gorm.io/gorm/logger"
)

type Config struct {
    Host     string
    Port     string
    User     string
    Password string
    DBName   string
    SSLMode  string
}

func DatabaseConnection() *gorm.DB {
    config := Config{
        Host:     getEnv("DB_HOST", "localhost"),
        Port:     getEnv("DB_PORT", "5432"),
        User:     getEnv("DB_USER", "postgres"),
        Password: getEnv("DB_PASSWORD", "password"),
        DBName:   getEnv("DB_NAME", "testdb"),
        SSLMode:  getEnv("DB_SSLMODE", "disable"),
    }
    
    dsn := fmt.Sprintf("host=%s port=%s user=%s password=%s dbname=%s sslmode=%s",
        config.Host, config.Port, config.User, config.Password, config.DBName, config.SSLMode)
    
    db, err := gorm.Open(postgres.Open(dsn), &gorm.Config{
        Logger: logger.Default.LogMode(logger.Info),
    })
    
    if err != nil {
        log.Fatal("Failed to connect to database:", err)
    }
    
    return db
}

func getEnv(key, defaultValue string) string {
    if value := os.Getenv(key); value != "" {
        return value
    }
    return defaultValue
}
```

### 3. Models dan Auto Migration
```go
package main

import (
    "time"
    
    "gorm.io/gorm"
)

// User model
type User struct {
    ID        uint      `json:"id" gorm:"primaryKey"`
    Name      string    `json:"name" gorm:"not null;size:100"`
    Email     string    `json:"email" gorm:"uniqueIndex;not null;size:100"`
    Age       int       `json:"age" gorm:"not null"`
    Active    bool      `json:"active" gorm:"default:true"`
    CreatedAt time.Time `json:"created_at"`
    UpdatedAt time.Time `json:"updated_at"`
    DeletedAt gorm.DeletedAt `json:"deleted_at" gorm:"index"`
    
    // Relationships
    Posts []Post `json:"posts,omitempty"`
}

// Post model
type Post struct {
    ID        uint      `json:"id" gorm:"primaryKey"`
    Title     string    `json:"title" gorm:"not null;size:200"`
    Content   string    `json:"content" gorm:"type:text"`
    UserID    uint      `json:"user_id" gorm:"not null"`
    Published bool      `json:"published" gorm:"default:false"`
    CreatedAt time.Time `json:"created_at"`
    UpdatedAt time.Time `json:"updated_at"`
    DeletedAt gorm.DeletedAt `json:"deleted_at" gorm:"index"`
    
    // Relationships
    User User `json:"user,omitempty"`
    Tags []Tag `json:"tags,omitempty" gorm:"many2many:post_tags;"`
}

// Tag model
type Tag struct {
    ID    uint   `json:"id" gorm:"primaryKey"`
    Name  string `json:"name" gorm:"uniqueIndex;not null;size:50"`
    Posts []Post `json:"posts,omitempty" gorm:"many2many:post_tags;"`
}

// Profile model (One-to-One with User)
type Profile struct {
    ID       uint   `json:"id" gorm:"primaryKey"`
    UserID   uint   `json:"user_id" gorm:"uniqueIndex;not null"`
    Bio      string `json:"bio" gorm:"type:text"`
    Website  string `json:"website" gorm:"size:200"`
    Location string `json:"location" gorm:"size:100"`
    
    User User `json:"user,omitempty"`
}

// Auto migrate all models
func AutoMigrate(db *gorm.DB) error {
    return db.AutoMigrate(&User{}, &Post{}, &Tag{}, &Profile{})
}

// Table names (optional)
func (User) TableName() string {
    return "users"
}

func (Post) TableName() string {
    return "posts"
}

func (Tag) TableName() string {
    return "tags"
}

func (Profile) TableName() string {
    return "profiles"
}
```

### 4. Repository Pattern
```go
package main

import (
    "errors"
    
    "gorm.io/gorm"
)

// User Repository Interface
type UserRepositoryInterface interface {
    Create(user *User) error
    GetByID(id uint) (*User, error)
    GetByEmail(email string) (*User, error)
    GetAll(limit, offset int) ([]User, error)
    Update(user *User) error
    Delete(id uint) error
    GetWithPosts(id uint) (*User, error)
}

// User Repository Implementation
type UserRepository struct {
    db *gorm.DB
}

func NewUserRepository(db *gorm.DB) UserRepositoryInterface {
    return &UserRepository{db: db}
}

func (r *UserRepository) Create(user *User) error {
    return r.db.Create(user).Error
}

func (r *UserRepository) GetByID(id uint) (*User, error) {
    var user User
    err := r.db.First(&user, id).Error
    if err != nil {
        if errors.Is(err, gorm.ErrRecordNotFound) {
            return nil, errors.New("user not found")
        }
        return nil, err
    }
    return &user, nil
}

func (r *UserRepository) GetByEmail(email string) (*User, error) {
    var user User
    err := r.db.Where("email = ?", email).First(&user).Error
    if err != nil {
        if errors.Is(err, gorm.ErrRecordNotFound) {
            return nil, errors.New("user not found")
        }
        return nil, err
    }
    return &user, nil
}

func (r *UserRepository) GetAll(limit, offset int) ([]User, error) {
    var users []User
    err := r.db.Limit(limit).Offset(offset).Find(&users).Error
    return users, err
}

func (r *UserRepository) Update(user *User) error {
    return r.db.Save(user).Error
}

func (r *UserRepository) Delete(id uint) error {
    return r.db.Delete(&User{}, id).Error
}

func (r *UserRepository) GetWithPosts(id uint) (*User, error) {
    var user User
    err := r.db.Preload("Posts").First(&user, id).Error
    if err != nil {
        if errors.Is(err, gorm.ErrRecordNotFound) {
            return nil, errors.New("user not found")
        }
        return nil, err
    }
    return &user, nil
}

// Post Repository Interface
type PostRepositoryInterface interface {
    Create(post *Post) error
    GetByID(id uint) (*Post, error)
    GetAll(limit, offset int) ([]Post, error)
    GetByUserID(userID uint) ([]Post, error)
    Update(post *Post) error
    Delete(id uint) error
    GetWithUser(id uint) (*Post, error)
}

// Post Repository Implementation
type PostRepository struct {
    db *gorm.DB
}

func NewPostRepository(db *gorm.DB) PostRepositoryInterface {
    return &PostRepository{db: db}
}

func (r *PostRepository) Create(post *Post) error {
    return r.db.Create(post).Error
}

func (r *PostRepository) GetByID(id uint) (*Post, error) {
    var post Post
    err := r.db.First(&post, id).Error
    if err != nil {
        if errors.Is(err, gorm.ErrRecordNotFound) {
            return nil, errors.New("post not found")
        }
        return nil, err
    }
    return &post, nil
}
```

### 5. Service Layer
```go
package main

import (
    "errors"
    "fmt"
)

// User Service Interface
type UserServiceInterface interface {
    CreateUser(name, email string, age int) (*User, error)
    GetUser(id uint) (*User, error)
    GetUserByEmail(email string) (*User, error)
    GetUsers(page, limit int) ([]User, error)
    UpdateUser(id uint, name, email string, age int) (*User, error)
    DeleteUser(id uint) error
    GetUserWithPosts(id uint) (*User, error)
}

// User Service Implementation
type UserService struct {
    userRepo UserRepositoryInterface
}

func NewUserService(userRepo UserRepositoryInterface) UserServiceInterface {
    return &UserService{userRepo: userRepo}
}

func (s *UserService) CreateUser(name, email string, age int) (*User, error) {
    // Validation
    if name == "" {
        return nil, errors.New("name is required")
    }
    if email == "" {
        return nil, errors.New("email is required")
    }
    if age < 0 {
        return nil, errors.New("age must be positive")
    }
    
    // Check if email exists
    existingUser, _ := s.userRepo.GetByEmail(email)
    if existingUser != nil {
        return nil, errors.New("email already exists")
    }
    
    user := &User{
        Name:   name,
        Email:  email,
        Age:    age,
        Active: true,
    }
    
    err := s.userRepo.Create(user)
    if err != nil {
        return nil, fmt.Errorf("failed to create user: %w", err)
    }
    
    return user, nil
}

func (s *UserService) GetUser(id uint) (*User, error) {
    return s.userRepo.GetByID(id)
}

func (s *UserService) GetUserByEmail(email string) (*User, error) {
    return s.userRepo.GetByEmail(email)
}

func (s *UserService) GetUsers(page, limit int) ([]User, error) {
    if page < 1 {
        page = 1
    }
    if limit < 1 {
        limit = 10
    }
    
    offset := (page - 1) * limit
    return s.userRepo.GetAll(limit, offset)
}

func (s *UserService) UpdateUser(id uint, name, email string, age int) (*User, error) {
    user, err := s.userRepo.GetByID(id)
    if err != nil {
        return nil, err
    }
    
    // Validation
    if name != "" {
        user.Name = name
    }
    if email != "" {
        // Check if email exists for other users
        existingUser, _ := s.userRepo.GetByEmail(email)
        if existingUser != nil && existingUser.ID != id {
            return nil, errors.New("email already exists")
        }
        user.Email = email
    }
    if age > 0 {
        user.Age = age
    }
    
    err = s.userRepo.Update(user)
    if err != nil {
        return nil, fmt.Errorf("failed to update user: %w", err)
    }
    
    return user, nil
}

func (s *UserService) DeleteUser(id uint) error {
    _, err := s.userRepo.GetByID(id)
    if err != nil {
        return err
    }
    
    return s.userRepo.Delete(id)
}

func (s *UserService) GetUserWithPosts(id uint) (*User, error) {
    return s.userRepo.GetWithPosts(id)
}

// Post Service Interface
type PostServiceInterface interface {
    CreatePost(title, content string, userID uint) (*Post, error)
    GetPost(id uint) (*Post, error)
    GetPosts(page, limit int) ([]Post, error)
    GetPostsByUser(userID uint) ([]Post, error)
    UpdatePost(id uint, title, content string) (*Post, error)
    DeletePost(id uint) error
    PublishPost(id uint) (*Post, error)
}

// Post Service Implementation
type PostService struct {
    postRepo PostRepositoryInterface
    userRepo UserRepositoryInterface
}

func NewPostService(postRepo PostRepositoryInterface, userRepo UserRepositoryInterface) PostServiceInterface {
    return &PostService{postRepo: postRepo, userRepo: userRepo}
}

func (s *PostService) CreatePost(title, content string, userID uint) (*Post, error) {
    // Validation
    if title == "" {
        return nil, errors.New("title is required")
    }
    if content == "" {
        return nil, errors.New("content is required")
    }
    
    // Check if user exists
    _, err := s.userRepo.GetByID(userID)
    if err != nil {
        return nil, errors.New("user not found")
    }
    
    post := &Post{
        Title:     title,
        Content:   content,
        UserID:    userID,
        Published: false,
    }
    
    err = s.postRepo.Create(post)
    if err != nil {
        return nil, fmt.Errorf("failed to create post: %w", err)
    }
    
    return post, nil
}

func (s *PostService) GetPost(id uint) (*Post, error) {
    return s.postRepo.GetWithUser(id)
}

func (s *PostService) GetPosts(page, limit int) ([]Post, error) {
    if page < 1 {
        page = 1
    }
    if limit < 1 {
        limit = 10
    }
    
    offset := (page - 1) * limit
    return s.postRepo.GetAll(limit, offset)
}

func (s *PostService) GetPostsByUser(userID uint) ([]Post, error) {
    // Check if user exists
    _, err := s.userRepo.GetByID(userID)
    if err != nil {
        return nil, errors.New("user not found")
    }
    
    return s.postRepo.GetByUserID(userID)
}

func (s *PostService) UpdatePost(id uint, title, content string) (*Post, error) {
    post, err := s.postRepo.GetByID(id)
    if err != nil {
        return nil, err
    }
    
    if title != "" {
        post.Title = title
    }
    if content != "" {
        post.Content = content
    }
    
    err = s.postRepo.Update(post)
    if err != nil {
        return nil, fmt.Errorf("failed to update post: %w", err)
    }
    
    return post, nil
}

func (s *PostService) DeletePost(id uint) error {
    _, err := s.postRepo.GetByID(id)
    if err != nil {
        return err
    }
    
    return s.postRepo.Delete(id)
}

func (s *PostService) PublishPost(id uint) (*Post, error) {
    post, err := s.postRepo.GetByID(id)
    if err != nil {
        return nil, err
    }
    
    post.Published = true
    err = s.postRepo.Update(post)
    if err != nil {
        return nil, fmt.Errorf("failed to publish post: %w", err)
    }
    
    return post, nil
}
```

### 6. Controllers
```go
package main

import (
    "net/http"
    "strconv"
    
    "github.com/gin-gonic/gin"
)

// User Controller
type UserController struct {
    userService UserServiceInterface
}

func NewUserController(userService UserServiceInterface) *UserController {
    return &UserController{userService: userService}
}

func (ctrl *UserController) CreateUser(c *gin.Context) {
    var req struct {
        Name  string `json:"name" binding:"required"`
        Email string `json:"email" binding:"required,email"`
        Age   int    `json:"age" binding:"required,min=0"`
    }
    
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    user, err := ctrl.userService.CreateUser(req.Name, req.Email, req.Age)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusCreated, gin.H{
        "message": "User created successfully",
        "data":    user,
    })
}

func (ctrl *UserController) GetUser(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.ParseUint(idParam, 10, 32)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }
    
    user, err := ctrl.userService.GetUser(uint(id))
    if err != nil {
        c.JSON(http.StatusNotFound, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "data": user,
    })
}

func (ctrl *UserController) GetUsers(c *gin.Context) {
    page, _ := strconv.Atoi(c.DefaultQuery("page", "1"))
    limit, _ := strconv.Atoi(c.DefaultQuery("limit", "10"))
    
    users, err := ctrl.userService.GetUsers(page, limit)
    if err != nil {
        c.JSON(http.StatusInternalServerError, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "data": users,
        "pagination": gin.H{
            "page":  page,
            "limit": limit,
        },
    })
}

func (ctrl *UserController) UpdateUser(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.ParseUint(idParam, 10, 32)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }
    
    var req struct {
        Name  string `json:"name"`
        Email string `json:"email"`
        Age   int    `json:"age"`
    }
    
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    user, err := ctrl.userService.UpdateUser(uint(id), req.Name, req.Email, req.Age)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "message": "User updated successfully",
        "data":    user,
    })
}

func (ctrl *UserController) DeleteUser(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.ParseUint(idParam, 10, 32)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }
    
    err = ctrl.userService.DeleteUser(uint(id))
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "message": "User deleted successfully",
    })
}

func (ctrl *UserController) GetUserWithPosts(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.ParseUint(idParam, 10, 32)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }
    
    user, err := ctrl.userService.GetUserWithPosts(uint(id))
    if err != nil {
        c.JSON(http.StatusNotFound, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "data": user,
    })
}

// Post Controller
type PostController struct {
    postService PostServiceInterface
}

func NewPostController(postService PostServiceInterface) *PostController {
    return &PostController{postService: postService}
}

func (ctrl *PostController) CreatePost(c *gin.Context) {
    var req struct {
        Title   string `json:"title" binding:"required"`
        Content string `json:"content" binding:"required"`
        UserID  uint   `json:"user_id" binding:"required"`
    }
    
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    post, err := ctrl.postService.CreatePost(req.Title, req.Content, req.UserID)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusCreated, gin.H{
        "message": "Post created successfully",
        "data":    post,
    })
}

func (ctrl *PostController) GetPost(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.ParseUint(idParam, 10, 32)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid post ID",
        })
        return
    }
    
    post, err := ctrl.postService.GetPost(uint(id))
    if err != nil {
        c.JSON(http.StatusNotFound, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "data": post,
    })
}

func (ctrl *PostController) GetPosts(c *gin.Context) {
    page, _ := strconv.Atoi(c.DefaultQuery("page", "1"))
    limit, _ := strconv.Atoi(c.DefaultQuery("limit", "10"))
    
    posts, err := ctrl.postService.GetPosts(page, limit)
    if err != nil {
        c.JSON(http.StatusInternalServerError, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "data": posts,
        "pagination": gin.H{
            "page":  page,
            "limit": limit,
        },
    })
}

func (ctrl *PostController) UpdatePost(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.ParseUint(idParam, 10, 32)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid post ID",
        })
        return
    }
    
    var req struct {
        Title   string `json:"title"`
        Content string `json:"content"`
    }
    
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    post, err := ctrl.postService.UpdatePost(uint(id), req.Title, req.Content)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "message": "Post updated successfully",
        "data":    post,
    })
}

func (ctrl *PostController) DeletePost(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.ParseUint(idParam, 10, 32)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid post ID",
        })
        return
    }
    
    err = ctrl.postService.DeletePost(uint(id))
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "message": "Post deleted successfully",
    })
}

func (ctrl *PostController) PublishPost(c *gin.Context) {
    idParam := c.Param("id")
    id, err := strconv.ParseUint(idParam, 10, 32)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid post ID",
        })
        return
    }
    
    post, err := ctrl.postService.PublishPost(uint(id))
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "message": "Post published successfully",
        "data":    post,
    })
}
```

---

## ODM dengan MongoDB

Untuk MongoDB, kita akan menggunakan mongo-driver resmi dari MongoDB dengan pattern yang mirip dengan GORM.

### 1. Instalasi Dependencies
```bash
go get go.mongodb.org/mongo-driver/mongo
go get go.mongodb.org/mongo-driver/mongo/options
go get go.mongodb.org/mongo-driver/bson
go get go.mongodb.org/mongo-driver/bson/primitive
```

### 2. MongoDB Configuration
```go
package main

import (
    "context"
    "fmt"
    "log"
    "time"
    
    "go.mongodb.org/mongo-driver/mongo"
    "go.mongodb.org/mongo-driver/mongo/options"
)

type MongoConfig struct {
    Host     string
    Port     string
    Username string
    Password string
    Database string
}

func ConnectMongoDB() *mongo.Client {
    config := MongoConfig{
        Host:     getEnv("MONGO_HOST", "localhost"),
        Port:     getEnv("MONGO_PORT", "27017"),
        Username: getEnv("MONGO_USERNAME", ""),
        Password: getEnv("MONGO_PASSWORD", ""),
        Database: getEnv("MONGO_DATABASE", "testdb"),
    }
    
    var uri string
    if config.Username != "" && config.Password != "" {
        uri = fmt.Sprintf("mongodb://%s:%s@%s:%s/%s",
            config.Username, config.Password, config.Host, config.Port, config.Database)
    } else {
        uri = fmt.Sprintf("mongodb://%s:%s/%s",
            config.Host, config.Port, config.Database)
    }
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    client, err := mongo.Connect(ctx, options.Client().ApplyURI(uri))
    if err != nil {
        log.Fatal("Failed to connect to MongoDB:", err)
    }
    
    // Test connection
    err = client.Ping(ctx, nil)
    if err != nil {
        log.Fatal("Failed to ping MongoDB:", err)
    }
    
    fmt.Println("Connected to MongoDB successfully!")
    return client
}

func GetDatabase(client *mongo.Client) *mongo.Database {
    return client.Database(getEnv("MONGO_DATABASE", "testdb"))
}
```

### 3. MongoDB Models
```go
package main

import (
    "time"
    
    "go.mongodb.org/mongo-driver/bson/primitive"
)

// User model for MongoDB
type MongoUser struct {
    ID        primitive.ObjectID `json:"id" bson:"_id,omitempty"`
    Name      string             `json:"name" bson:"name"`
    Email     string             `json:"email" bson:"email"`
    Age       int                `json:"age" bson:"age"`
    Active    bool               `json:"active" bson:"active"`
    CreatedAt time.Time          `json:"created_at" bson:"created_at"`
    UpdatedAt time.Time          `json:"updated_at" bson:"updated_at"`
}

// Post model for MongoDB
type MongoPost struct {
    ID        primitive.ObjectID `json:"id" bson:"_id,omitempty"`
    Title     string             `json:"title" bson:"title"`
    Content   string             `json:"content" bson:"content"`
    UserID    primitive.ObjectID `json:"user_id" bson:"user_id"`
    Published bool               `json:"published" bson:"published"`
    Tags      []string           `json:"tags" bson:"tags"`
    CreatedAt time.Time          `json:"created_at" bson:"created_at"`
    UpdatedAt time.Time          `json:"updated_at" bson:"updated_at"`
}

// Comment model for MongoDB (nested document)
type MongoComment struct {
    ID        primitive.ObjectID `json:"id" bson:"_id,omitempty"`
    PostID    primitive.ObjectID `json:"post_id" bson:"post_id"`
    UserID    primitive.ObjectID `json:"user_id" bson:"user_id"`
    Content   string             `json:"content" bson:"content"`
    CreatedAt time.Time          `json:"created_at" bson:"created_at"`
}

// Category model with embedded posts
type MongoCategory struct {
    ID          primitive.ObjectID `json:"id" bson:"_id,omitempty"`
    Name        string             `json:"name" bson:"name"`
    Description string             `json:"description" bson:"description"`
    Posts       []MongoPost        `json:"posts" bson:"posts"`
    CreatedAt   time.Time          `json:"created_at" bson:"created_at"`
    UpdatedAt   time.Time          `json:"updated_at" bson:"updated_at"`
}
```

### 4. MongoDB Repository
```go
package main

import (
    "context"
    "errors"
    "time"
    
    "go.mongodb.org/mongo-driver/bson"
    "go.mongodb.org/mongo-driver/bson/primitive"
    "go.mongodb.org/mongo-driver/mongo"
    "go.mongodb.org/mongo-driver/mongo/options"
)

// MongoDB User Repository Interface
type MongoUserRepositoryInterface interface {
    Create(ctx context.Context, user *MongoUser) error
    GetByID(ctx context.Context, id primitive.ObjectID) (*MongoUser, error)
    GetByEmail(ctx context.Context, email string) (*MongoUser, error)
    GetAll(ctx context.Context, limit, skip int64) ([]MongoUser, error)
    Update(ctx context.Context, id primitive.ObjectID, user *MongoUser) error
    Delete(ctx context.Context, id primitive.ObjectID) error
    Count(ctx context.Context) (int64, error)
}

// MongoDB User Repository Implementation
type MongoUserRepository struct {
    collection *mongo.Collection
}

func NewMongoUserRepository(db *mongo.Database) MongoUserRepositoryInterface {
    collection := db.Collection("users")
    
    // Create indexes
    indexModel := mongo.IndexModel{
        Keys: bson.M{"email": 1},
        Options: options.Index().SetUnique(true),
    }
    collection.Indexes().CreateOne(context.Background(), indexModel)
    
    return &MongoUserRepository{collection: collection}
}

func (r *MongoUserRepository) Create(ctx context.Context, user *MongoUser) error {
    user.CreatedAt = time.Now()
    user.UpdatedAt = time.Now()
    
    result, err := r.collection.InsertOne(ctx, user)
    if err != nil {
        return err
    }
    
    user.ID = result.InsertedID.(primitive.ObjectID)
    return nil
}

func (r *MongoUserRepository) GetByID(ctx context.Context, id primitive.ObjectID) (*MongoUser, error) {
    var user MongoUser
    err := r.collection.FindOne(ctx, bson.M{"_id": id}).Decode(&user)
    if err != nil {
        if err == mongo.ErrNoDocuments {
            return nil, errors.New("user not found")
        }
        return nil, err
    }
    return &user, nil
}

func (r *MongoUserRepository) GetByEmail(ctx context.Context, email string) (*MongoUser, error) {
    var user MongoUser
    err := r.collection.FindOne(ctx, bson.M{"email": email}).Decode(&user)
    if err != nil {
        if err == mongo.ErrNoDocuments {
            return nil, errors.New("user not found")
        }
        return nil, err
    }
    return &user, nil
}

func (r *MongoUserRepository) GetAll(ctx context.Context, limit, skip int64) ([]MongoUser, error) {
    var users []MongoUser
    
    opts := options.Find()
    if limit > 0 {
        opts.SetLimit(limit)
    }
    if skip > 0 {
        opts.SetSkip(skip)
    }
    opts.SetSort(bson.M{"created_at": -1})
    
    cursor, err := r.collection.Find(ctx, bson.M{}, opts)
    if err != nil {
        return nil, err
    }
    defer cursor.Close(ctx)
    
    err = cursor.All(ctx, &users)
    return users, err
}

func (r *MongoUserRepository) Update(ctx context.Context, id primitive.ObjectID, user *MongoUser) error {
    user.UpdatedAt = time.Now()
    
    update := bson.M{
        "$set": bson.M{
            "name":       user.Name,
            "email":      user.Email,
            "age":        user.Age,
            "active":     user.Active,
            "updated_at": user.UpdatedAt,
        },
    }
    
    result, err := r.collection.UpdateOne(ctx, bson.M{"_id": id}, update)
    if err != nil {
        return err
    }
    
    if result.MatchedCount == 0 {
        return errors.New("user not found")
    }
    
    return nil
}

func (r *MongoUserRepository) Delete(ctx context.Context, id primitive.ObjectID) error {
    result, err := r.collection.DeleteOne(ctx, bson.M{"_id": id})
    if err != nil {
        return err
    }
    
    if result.DeletedCount == 0 {
        return errors.New("user not found")
    }
    
    return nil
}

func (r *MongoUserRepository) Count(ctx context.Context) (int64, error) {
    return r.collection.CountDocuments(ctx, bson.M{})
}

// MongoDB Post Repository Interface
type MongoPostRepositoryInterface interface {
    Create(ctx context.Context, post *MongoPost) error
    GetByID(ctx context.Context, id primitive.ObjectID) (*MongoPost, error)
    GetAll(ctx context.Context, limit, skip int64) ([]MongoPost, error)
    GetByUserID(ctx context.Context, userID primitive.ObjectID) ([]MongoPost, error)
    Update(ctx context.Context, id primitive.ObjectID, post *MongoPost) error
    Delete(ctx context.Context, id primitive.ObjectID) error
    GetPublished(ctx context.Context, limit, skip int64) ([]MongoPost, error)
    SearchByTitle(ctx context.Context, title string) ([]MongoPost, error)
}

// MongoDB Post Repository Implementation
type MongoPostRepository struct {
    collection *mongo.Collection
}

func NewMongoPostRepository(db *mongo.Database) MongoPostRepositoryInterface {
    collection := db.Collection("posts")
    
    // Create indexes
    indexModels := []mongo.IndexModel{
        {
            Keys: bson.M{"user_id": 1},
        },
        {
            Keys: bson.M{"title": "text", "content": "text"},
        },
        {
            Keys: bson.M{"published": 1, "created_at": -1},
        },
    }
    collection.Indexes().CreateMany(context.Background(), indexModels)
    
    return &MongoPostRepository{collection: collection}
}

func (r *MongoPostRepository) Create(ctx context.Context, post *MongoPost) error {
    post.CreatedAt = time.Now()
    post.UpdatedAt = time.Now()
    
    result, err := r.collection.InsertOne(ctx, post)
    if err != nil {
        return err
    }
    
    post.ID = result.InsertedID.(primitive.ObjectID)
    return nil
}

func (r *MongoPostRepository) GetByID(ctx context.Context, id primitive.ObjectID) (*MongoPost, error) {
    var post MongoPost
    err := r.collection.FindOne(ctx, bson.M{"_id": id}).Decode(&post)
    if err != nil {
        if err == mongo.ErrNoDocuments {
            return nil, errors.New("post not found")
        }
        return nil, err
    }
    return &post, nil
}

func (r *MongoPostRepository) GetAll(ctx context.Context, limit, skip int64) ([]MongoPost, error) {
    var posts []MongoPost
    
    opts := options.Find()
    if limit > 0 {
        opts.SetLimit(limit)
    }
    if skip > 0 {
        opts.SetSkip(skip)
    }
    opts.SetSort(bson.M{"created_at": -1})
    
    cursor, err := r.collection.Find(ctx, bson.M{}, opts)
    if err != nil {
        return nil, err
    }
    defer cursor.Close(ctx)
    
    err = cursor.All(ctx, &posts)
    return posts, err
}

func (r *MongoPostRepository) GetByUserID(ctx context.Context, userID primitive.ObjectID) ([]MongoPost, error) {
    var posts []MongoPost
    
    opts := options.Find().SetSort(bson.M{"created_at": -1})
    cursor, err := r.collection.Find(ctx, bson.M{"user_id": userID}, opts)
    if err != nil {
        return nil, err
    }
    defer cursor.Close(ctx)
    
    err = cursor.All(ctx, &posts)
    return posts, err
}

func (r *MongoPostRepository) Update(ctx context.Context, id primitive.ObjectID, post *MongoPost) error {
    post.UpdatedAt = time.Now()
    
    update := bson.M{
        "$set": bson.M{
            "title":      post.Title,
            "content":    post.Content,
            "published":  post.Published,
            "tags":       post.Tags,
            "updated_at": post.UpdatedAt,
        },
    }
    
    result, err := r.collection.UpdateOne(ctx, bson.M{"_id": id}, update)
    if err != nil {
        return err
    }
    
    if result.MatchedCount == 0 {
        return errors.New("post not found")
    }
    
    return nil
}

func (r *MongoPostRepository) Delete(ctx context.Context, id primitive.ObjectID) error {
    result, err := r.collection.DeleteOne(ctx, bson.M{"_id": id})
    if err != nil {
        return err
    }
    
    if result.DeletedCount == 0 {
        return errors.New("post not found")
    }
    
    return nil
}

func (r *MongoPostRepository) GetPublished(ctx context.Context, limit, skip int64) ([]MongoPost, error) {
    var posts []MongoPost
    
    opts := options.Find()
    if limit > 0 {
        opts.SetLimit(limit)
    }
    if skip > 0 {
        opts.SetSkip(skip)
    }
    opts.SetSort(bson.M{"created_at": -1})
    
    cursor, err := r.collection.Find(ctx, bson.M{"published": true}, opts)
    if err != nil {
        return nil, err
    }
    defer cursor.Close(ctx)
    
    err = cursor.All(ctx, &posts)
    return posts, err
}

func (r *MongoPostRepository) SearchByTitle(ctx context.Context, title string) ([]MongoPost, error) {
    var posts []MongoPost
    
    filter := bson.M{
        "$text": bson.M{
            "$search": title,
        },
    }
    
    opts := options.Find().SetSort(bson.M{"score": bson.M{"$meta": "textScore"}})
    cursor, err := r.collection.Find(ctx, filter, opts)
    if err != nil {
        return nil, err
    }
    defer cursor.Close(ctx)
    
    err = cursor.All(ctx, &posts)
    return posts, err
}
```

### 5. MongoDB Service Layer
```go
package main

import (
    "context"
    "errors"
    "fmt"
    "time"
    
    "go.mongodb.org/mongo-driver/bson/primitive"
)

// MongoDB User Service Interface
type MongoUserServiceInterface interface {
    CreateUser(ctx context.Context, name, email string, age int) (*MongoUser, error)
    GetUser(ctx context.Context, id string) (*MongoUser, error)
    GetUserByEmail(ctx context.Context, email string) (*MongoUser, error)
    GetUsers(ctx context.Context, page, limit int) ([]MongoUser, int64, error)
    UpdateUser(ctx context.Context, id string, name, email string, age int) (*MongoUser, error)
    DeleteUser(ctx context.Context, id string) error
}

// MongoDB User Service Implementation
type MongoUserService struct {
    userRepo MongoUserRepositoryInterface
}

func NewMongoUserService(userRepo MongoUserRepositoryInterface) MongoUserServiceInterface {
    return &MongoUserService{userRepo: userRepo}
}

func (s *MongoUserService) CreateUser(ctx context.Context, name, email string, age int) (*MongoUser, error) {
    // Validation
    if name == "" {
        return nil, errors.New("name is required")
    }
    if email == "" {
        return nil, errors.New("email is required")
    }
    if age < 0 {
        return nil, errors.New("age must be positive")
    }
    
    // Check if email exists
    existingUser, _ := s.userRepo.GetByEmail(ctx, email)
    if existingUser != nil {
        return nil, errors.New("email already exists")
    }
    
    user := &MongoUser{
        Name:   name,
        Email:  email,
        Age:    age,
        Active: true,
    }
    
    err := s.userRepo.Create(ctx, user)
    if err != nil {
        return nil, fmt.Errorf("failed to create user: %w", err)
    }
    
    return user, nil
}

func (s *MongoUserService) GetUser(ctx context.Context, id string) (*MongoUser, error) {
    objectID, err := primitive.ObjectIDFromHex(id)
    if err != nil {
        return nil, errors.New("invalid user ID")
    }
    
    return s.userRepo.GetByID(ctx, objectID)
}

func (s *MongoUserService) GetUserByEmail(ctx context.Context, email string) (*MongoUser, error) {
    return s.userRepo.GetByEmail(ctx, email)
}

func (s *MongoUserService) GetUsers(ctx context.Context, page, limit int) ([]MongoUser, int64, error) {
    if page < 1 {
        page = 1
    }
    if limit < 1 {
        limit = 10
    }
    
    skip := int64((page - 1) * limit)
    users, err := s.userRepo.GetAll(ctx, int64(limit), skip)
    if err != nil {
        return nil, 0, err
    }
    
    total, err := s.userRepo.Count(ctx)
    if err != nil {
        return nil, 0, err
    }
    
    return users, total, nil
}

func (s *MongoUserService) UpdateUser(ctx context.Context, id string, name, email string, age int) (*MongoUser, error) {
    objectID, err := primitive.ObjectIDFromHex(id)
    if err != nil {
        return nil, errors.New("invalid user ID")
    }
    
    user, err := s.userRepo.GetByID(ctx, objectID)
    if err != nil {
        return nil, err
    }
    
    // Validation and update
    if name != "" {
        user.Name = name
    }
    if email != "" {
        // Check if email exists for other users
        existingUser, _ := s.userRepo.GetByEmail(ctx, email)
        if existingUser != nil && existingUser.ID != objectID {
            return nil, errors.New("email already exists")
        }
        user.Email = email
    }
    if age > 0 {
        user.Age = age
    }
    
    err = s.userRepo.Update(ctx, objectID, user)
    if err != nil {
        return nil, fmt.Errorf("failed to update user: %w", err)
    }
    
    return user, nil
}

func (s *MongoUserService) DeleteUser(ctx context.Context, id string) error {
    objectID, err := primitive.ObjectIDFromHex(id)
    if err != nil {
        return errors.New("invalid user ID")
    }
    
    _, err = s.userRepo.GetByID(ctx, objectID)
    if err != nil {
        return err
    }
    
    return s.userRepo.Delete(ctx, objectID)
}

// MongoDB Post Service Interface
type MongoPostServiceInterface interface {
    CreatePost(ctx context.Context, title, content string, userID string, tags []string) (*MongoPost, error)
    GetPost(ctx context.Context, id string) (*MongoPost, error)
    GetPosts(ctx context.Context, page, limit int) ([]MongoPost, error)
    GetPostsByUser(ctx context.Context, userID string) ([]MongoPost, error)
    UpdatePost(ctx context.Context, id string, title, content string, tags []string) (*MongoPost, error)
    DeletePost(ctx context.Context, id string) error
    PublishPost(ctx context.Context, id string) (*MongoPost, error)
    SearchPosts(ctx context.Context, query string) ([]MongoPost, error)
}

// MongoDB Post Service Implementation
type MongoPostService struct {
    postRepo MongoPostRepositoryInterface
    userRepo MongoUserRepositoryInterface
}

func NewMongoPostService(postRepo MongoPostRepositoryInterface, userRepo MongoUserRepositoryInterface) MongoPostServiceInterface {
    return &MongoPostService{postRepo: postRepo, userRepo: userRepo}
}

func (s *MongoPostService) CreatePost(ctx context.Context, title, content string, userID string, tags []string) (*MongoPost, error) {
    // Validation
    if title == "" {
        return nil, errors.New("title is required")
    }
    if content == "" {
        return nil, errors.New("content is required")
    }
    
    // Convert userID to ObjectID
    userObjectID, err := primitive.ObjectIDFromHex(userID)
    if err != nil {
        return nil, errors.New("invalid user ID")
    }
    
    // Check if user exists
    _, err = s.userRepo.GetByID(ctx, userObjectID)
    if err != nil {
        return nil, errors.New("user not found")
    }
    
    post := &MongoPost{
        Title:     title,
        Content:   content,
        UserID:    userObjectID,
        Published: false,
        Tags:      tags,
    }
    
    err = s.postRepo.Create(ctx, post)
    if err != nil {
        return nil, fmt.Errorf("failed to create post: %w", err)
    }
    
    return post, nil
}

func (s *MongoPostService) GetPost(ctx context.Context, id string) (*MongoPost, error) {
    objectID, err := primitive.ObjectIDFromHex(id)
    if err != nil {
        return nil, errors.New("invalid post ID")
    }
    
    return s.postRepo.GetByID(ctx, objectID)
}

func (s *MongoPostService) GetPosts(ctx context.Context, page, limit int) ([]MongoPost, error) {
    if page < 1 {
        page = 1
    }
    if limit < 1 {
        limit = 10
    }
    
    skip := int64((page - 1) * limit)
    return s.postRepo.GetAll(ctx, int64(limit), skip)
}

func (s *MongoPostService) GetPostsByUser(ctx context.Context, userID string) ([]MongoPost, error) {
    userObjectID, err := primitive.ObjectIDFromHex(userID)
    if err != nil {
        return nil, errors.New("invalid user ID")
    }
    
    // Check if user exists
    _, err = s.userRepo.GetByID(ctx, userObjectID)
    if err != nil {
        return nil, errors.New("user not found")
    }
    
    return s.postRepo.GetByUserID(ctx, userObjectID)
}

func (s *MongoPostService) UpdatePost(ctx context.Context, id string, title, content string, tags []string) (*MongoPost, error) {
    objectID, err := primitive.ObjectIDFromHex(id)
    if err != nil {
        return nil, errors.New("invalid post ID")
    }
    
    post, err := s.postRepo.GetByID(ctx, objectID)
    if err != nil {
        return nil, err
    }
    
    if title != "" {
        post.Title = title
    }
    if content != "" {
        post.Content = content
    }
    if tags != nil {
        post.Tags = tags
    }
    
    err = s.postRepo.Update(ctx, objectID, post)
    if err != nil {
        return nil, fmt.Errorf("failed to update post: %w", err)
    }
    
    return post, nil
}

func (s *MongoPostService) DeletePost(ctx context.Context, id string) error {
    objectID, err := primitive.ObjectIDFromHex(id)
    if err != nil {
        return errors.New("invalid post ID")
    }
    
    _, err = s.postRepo.GetByID(ctx, objectID)
    if err != nil {
        return err
    }
    
    return s.postRepo.Delete(ctx, objectID)
}

func (s *MongoPostService) PublishPost(ctx context.Context, id string) (*MongoPost, error) {
    objectID, err := primitive.ObjectIDFromHex(id)
    if err != nil {
        return nil, errors.New("invalid post ID")
    }
    
    post, err := s.postRepo.GetByID(ctx, objectID)
    if err != nil {
        return nil, err
    }
    
    post.Published = true
    err = s.postRepo.Update(ctx, objectID, post)
    if err != nil {
        return nil, fmt.Errorf("failed to publish post: %w", err)
    }
    
    return post, nil
}

func (s *MongoPostService) SearchPosts(ctx context.Context, query string) ([]MongoPost, error) {
    return s.postRepo.SearchByTitle(ctx, query)
}
```

### 6. MongoDB Controllers
```go
package main

import (
    "context"
    "net/http"
    "strconv"
    "time"
    
    "github.com/gin-gonic/gin"
)

// MongoDB User Controller
type MongoUserController struct {
    userService MongoUserServiceInterface
}

func NewMongoUserController(userService MongoUserServiceInterface) *MongoUserController {
    return &MongoUserController{userService: userService}
}

func (ctrl *MongoUserController) CreateUser(c *gin.Context) {
    var req struct {
        Name  string `json:"name" binding:"required"`
        Email string `json:"email" binding:"required,email"`
        Age   int    `json:"age" binding:"required,min=0"`
    }
    
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    user, err := ctrl.userService.CreateUser(ctx, req.Name, req.Email, req.Age)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusCreated, gin.H{
        "message": "User created successfully",
        "data":    user,
    })
}

func (ctrl *MongoUserController) GetUser(c *gin.Context) {
    id := c.Param("id")
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    user, err := ctrl.userService.GetUser(ctx, id)
    if err != nil {
        c.JSON(http.StatusNotFound, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "data": user,
    })
}

func (ctrl *MongoUserController) GetUsers(c *gin.Context) {
    page, _ := strconv.Atoi(c.DefaultQuery("page", "1"))
    limit, _ := strconv.Atoi(c.DefaultQuery("limit", "10"))
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    users, total, err := ctrl.userService.GetUsers(ctx, page, limit)
    if err != nil {
        c.JSON(http.StatusInternalServerError, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    totalPages := (total + int64(limit) - 1) / int64(limit)
    
    c.JSON(http.StatusOK, gin.H{
        "data": users,
        "pagination": gin.H{
            "page":        page,
            "limit":       limit,
            "total":       total,
            "total_pages": totalPages,
        },
    })
}

func (ctrl *MongoUserController) UpdateUser(c *gin.Context) {
    id := c.Param("id")
    
    var req struct {
        Name  string `json:"name"`
        Email string `json:"email"`
        Age   int    `json:"age"`
    }
    
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    user, err := ctrl.userService.UpdateUser(ctx, id, req.Name, req.Email, req.Age)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "message": "User updated successfully",
        "data":    user,
    })
}

func (ctrl *MongoUserController) DeleteUser(c *gin.Context) {
    id := c.Param("id")
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    err := ctrl.userService.DeleteUser(ctx, id)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "message": "User deleted successfully",
    })
}

// MongoDB Post Controller
type MongoPostController struct {
    postService MongoPostServiceInterface
}

func NewMongoPostController(postService MongoPostServiceInterface) *MongoPostController {
    return &MongoPostController{postService: postService}
}

func (ctrl *MongoPostController) CreatePost(c *gin.Context) {
    var req struct {
        Title   string   `json:"title" binding:"required"`
        Content string   `json:"content" binding:"required"`
        UserID  string   `json:"user_id" binding:"required"`
        Tags    []string `json:"tags"`
    }
    
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    post, err := ctrl.postService.CreatePost(ctx, req.Title, req.Content, req.UserID, req.Tags)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusCreated, gin.H{
        "message": "Post created successfully",
        "data":    post,
    })
}

func (ctrl *MongoPostController) GetPost(c *gin.Context) {
    id := c.Param("id")
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    post, err := ctrl.postService.GetPost(ctx, id)
    if err != nil {
        c.JSON(http.StatusNotFound, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "data": post,
    })
}

func (ctrl *MongoPostController) GetPosts(c *gin.Context) {
    page, _ := strconv.Atoi(c.DefaultQuery("page", "1"))
    limit, _ := strconv.Atoi(c.DefaultQuery("limit", "10"))
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    posts, err := ctrl.postService.GetPosts(ctx, page, limit)
    if err != nil {
        c.JSON(http.StatusInternalServerError, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "data": posts,
        "pagination": gin.H{
            "page":  page,
            "limit": limit,
        },
    })
}

func (ctrl *MongoPostController) SearchPosts(c *gin.Context) {
    query := c.Query("q")
    if query == "" {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "search query is required",
        })
        return
    }
    
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()
    
    posts, err := ctrl.postService.SearchPosts(ctx, query)
    if err != nil {
        c.JSON(http.StatusInternalServerError, gin.H{
            "error": err.Error(),
        })
        return
    }
    
    c.JSON(http.StatusOK, gin.H{
        "data":  posts,
        "query": query,
    })
}
```

---

## Proyek Praktik

### 1. Complete Application dengan PostgreSQL
```go
package main

import (
    "log"
    
    "github.com/gin-gonic/gin"
)

func main() {
    // Initialize database connection
    db := DatabaseConnection()
    
    // Auto migrate
    err := AutoMigrate(db)
    if err != nil {
        log.Fatal("Failed to migrate database:", err)
    }
    
    // Initialize repositories
    userRepo := NewUserRepository(db)
    postRepo := NewPostRepository(db)
    
    // Initialize services
    userService := NewUserService(userRepo)
    postService := NewPostService(postRepo, userRepo)
    
    // Initialize controllers
    userController := NewUserController(userService)
    postController := NewPostController(postService)
    
    // Setup Gin router
    router := gin.Default()
    
    // Middleware
    router.Use(Logger())
    router.Use(CORSMiddleware())
    
    // Routes
    api := router.Group("/api/v1")
    {
        // User routes
        users := api.Group("/users")
        {
            users.POST("", userController.CreateUser)
            users.GET("", userController.GetUsers)
            users.GET("/:id", userController.GetUser)
            users.PUT("/:id", userController.UpdateUser)
            users.DELETE("/:id", userController.DeleteUser)
            users.GET("/:id/posts", userController.GetUserWithPosts)
        }
        
        // Post routes
        posts := api.Group("/posts")
        {
            posts.POST("", postController.CreatePost)
            posts.GET("", postController.GetPosts)
            posts.GET("/:id", postController.GetPost)
            posts.PUT("/:id", postController.UpdatePost)
            posts.DELETE("/:id", postController.DeletePost)
            posts.PATCH("/:id/publish", postController.PublishPost)
        }
    }
    
    // Health check
    router.GET("/health", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "status":   "healthy",
            "database": "postgresql",
        })
    })
    
    log.Println("Server starting on :8080")
    router.Run(":8080")
}
```

### 2. Complete Application dengan MongoDB
```go
package main

import (
    "context"
    "log"
    
    "github.com/gin-gonic/gin"
)

func main() {
    // Initialize MongoDB connection
    client := ConnectMongoDB()
    db := GetDatabase(client)
    
    // Close connection when main exits
    defer func() {
        if err := client.Disconnect(context.TODO()); err != nil {
            log.Fatal("Failed to disconnect from MongoDB:", err)
        }
    }()
    
    // Initialize repositories
    userRepo := NewMongoUserRepository(db)
    postRepo := NewMongoPostRepository(db)
    
    // Initialize services
    userService := NewMongoUserService(userRepo)
    postService := NewMongoPostService(postRepo, userRepo)
    
    // Initialize controllers
    userController := NewMongoUserController(userService)
    postController := NewMongoPostController(postService)
    
    // Setup Gin router
    router := gin.Default()
    
    // Middleware
    router.Use(Logger())
    router.Use(CORSMiddleware())
    
    // Routes
    api := router.Group("/api/v1")
    {
        // User routes
        users := api.Group("/users")
        {
            users.POST("", userController.CreateUser)
            users.GET("", userController.GetUsers)
            users.GET("/:id", userController.GetUser)
            users.PUT("/:id", userController.UpdateUser)
            users.DELETE("/:id", userController.DeleteUser)
        }
        
        // Post routes
        posts := api.Group("/posts")
        {
            posts.POST("", postController.CreatePost)
            posts.GET("", postController.GetPosts)
            posts.GET("/:id", postController.GetPost)
            posts.GET("/search", postController.SearchPosts)
        }
    }
    
    // Health check
    router.GET("/health", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "status":   "healthy",
            "database": "mongodb",
        })
    })
    
    log.Println("Server starting on :8080")
    router.Run(":8080")
}
```

### 3. Environment Configuration (.env)
```bash
# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=password
DB_NAME=myapp
DB_SSLMODE=disable

# MongoDB Configuration
MONGO_HOST=localhost
MONGO_PORT=27017
MONGO_USERNAME=
MONGO_PASSWORD=
MONGO_DATABASE=myapp

# Server Configuration
PORT=8080
GIN_MODE=debug

# JWT Configuration (Optional)
JWT_SECRET=your-secret-key
JWT_EXPIRE_HOURS=24
```

### 4. Docker Setup
```dockerfile
# Dockerfile
FROM golang:1.21-alpine AS builder

WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN go build -o main .

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/

COPY --from=builder /app/main .
COPY --from=builder /app/.env .

CMD ["./main"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - DB_HOST=postgres
      - MONGO_HOST=mongodb
    depends_on:
      - postgres
      - mongodb
    volumes:
      - .:/app
    working_dir: /app

  postgres:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
      POSTGRES_DB: myapp
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  mongodb:
    image: mongo:6-alpine
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db

  adminer:
    image: adminer
    ports:
      - "8081:8080"
    depends_on:
      - postgres

volumes:
  postgres_data:
  mongodb_data:
```

### 5. Testing Examples
```go
package main

import (
    "bytes"
    "encoding/json"
    "net/http"
    "net/http/httptest"
    "testing"
    
    "github.com/gin-gonic/gin"
    "github.com/stretchr/testify/assert"
)

func TestCreateUser(t *testing.T) {
    // Setup
    gin.SetMode(gin.TestMode)
    router := gin.New()
    
    // Mock service
    userService := &MockUserService{}
    userController := NewUserController(userService)
    
    router.POST("/users", userController.CreateUser)
    
    // Test data
    user := map[string]interface{}{
        "name":  "John Doe",
        "email": "john@example.com",
        "age":   30,
    }
    
    jsonData, _ := json.Marshal(user)
    
    // Create request
    req, _ := http.NewRequest("POST", "/users", bytes.NewBuffer(jsonData))
    req.Header.Set("Content-Type", "application/json")
    
    // Create response recorder
    w := httptest.NewRecorder()
    
    // Perform request
    router.ServeHTTP(w, req)
    
    // Assertions
    assert.Equal(t, http.StatusCreated, w.Code)
    
    var response map[string]interface{}
    json.Unmarshal(w.Body.Bytes(), &response)
    assert.Equal(t, "User created successfully", response["message"])
}

// Mock service for testing
type MockUserService struct{}

func (m *MockUserService) CreateUser(name, email string, age int) (*User, error) {
    return &User{
        ID:    1,
        Name:  name,
        Email: email,
        Age:   age,
    }, nil
}

func (m *MockUserService) GetUser(id uint) (*User, error) {
    return &User{ID: id, Name: "John Doe", Email: "john@example.com", Age: 30}, nil
}

// Implement other methods...
```

### 6. Makefile
```makefile
# Makefile
.PHONY: build run test clean docker-up docker-down migrate

# Variables
APP_NAME=myapp
DOCKER_COMPOSE=docker-compose

# Build the application
build:
	go build -o bin/$(APP_NAME) .

# Run the application
run:
	go run .

# Run with hot reload (requires air)
dev:
	air

# Run tests
test:
	go test -v ./...

# Run tests with coverage
test-coverage:
	go test -v -coverprofile=coverage.out ./...
	go tool cover -html=coverage.out

# Clean build artifacts
clean:
	rm -rf bin/
	go clean

# Install dependencies
deps:
	go mod download
	go mod tidy

# Start Docker services
docker-up:
	$(DOCKER_COMPOSE) up -d

# Stop Docker services
docker-down:
	$(DOCKER_COMPOSE) down

# Build and run with Docker
docker-build:
	$(DOCKER_COMPOSE) build

# Run database migrations (PostgreSQL)
migrate-up:
	migrate -path migrations -database "postgresql://postgres:password@localhost:5432/myapp?sslmode=disable" up

migrate-down:
	migrate -path migrations -database "postgresql://postgres:password@localhost:5432/myapp?sslmode=disable" down

# Format code
fmt:
	go fmt ./...

# Lint code
lint:
	golangci-lint run

# Install development tools
install-tools:
	go install github.com/cosmtrek/air@latest
	go install github.com/golang-migrate/migrate/v4/cmd/migrate@latest
	go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
```

### 7. API Documentation (README.md)
```markdown
# Go Gin API Documentation

## Endpoints

### Users

#### Create User
- **POST** `/api/v1/users`
- **Body:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "age": 30
}
```

#### Get All Users
- **GET** `/api/v1/users?page=1&limit=10`

#### Get User by ID
- **GET** `/api/v1/users/{id}`

#### Update User
- **PUT** `/api/v1/users/{id}`
- **Body:**
```json
{
  "name": "John Updated",
  "email": "john.updated@example.com",
  "age": 31
}
```

#### Delete User
- **DELETE** `/api/v1/users/{id}`

### Posts

#### Create Post
- **POST** `/api/v1/posts`
- **Body:**
```json
{
  "title": "My First Post",
  "content": "This is the content of my first post",
  "user_id": 1
}
```

#### Get All Posts
- **GET** `/api/v1/posts?page=1&limit=10`

#### Get Post by ID
- **GET** `/api/v1/posts/{id}`

#### Update Post
- **PUT** `/api/v1/posts/{id}`

#### Delete Post
- **DELETE** `/api/v1/posts/{id}`

#### Publish Post
- **PATCH** `/api/v1/posts/{id}/publish`

## Response Format

### Success Response
```json
{
  "message": "Success message",
  "data": {
    // Response data
  }
}
```

### Error Response
```json
{
  "error": "Error message"
}
```

### Pagination Response
```json
{
  "data": [...],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 100,
    "total_pages": 10
  }
}
```
```

---

## Penjelasan dan Best Practices

### 1. **Struktur Project**
```
myapp/
├── models/          # Database models
├── repositories/    # Data access layer
├── services/        # Business logic layer
├── controllers/     # HTTP handlers
├── middleware/      # Custom middleware
├── config/          # Configuration
├── migrations/      # Database migrations
├── tests/           # Test files
├── docs/            # Documentation
├── docker-compose.yml
├── Dockerfile
├── Makefile
├── .env
├── go.mod
├── go.sum
└── main.go
```

### 2. **GORM vs MongoDB Driver**

**GORM (PostgreSQL):**
- ✅ Auto-migration sangat mudah
- ✅ Relationship handling otomatis  
- ✅ Query builder yang powerful
- ✅ Hooks dan callbacks
- ✅ Soft delete built-in

**MongoDB Driver:**
- ✅ Schema flexibility
- ✅ Better performance untuk read-heavy apps
- ✅ Natural JSON handling
- ✅ Horizontal scaling
- ✅ Full-text search built-in

### 3. **Auto Migration**

**GORM:**
```go
// Otomatis membuat/update tabel
db.AutoMigrate(&User{}, &Post{})

// Dengan options
db.Set("gorm:table_options", "ENGINE=InnoDB").AutoMigrate(&User{})
```

**MongoDB:**
```go
// Index creation otomatis di repository
indexModel := mongo.IndexModel{
    Keys: bson.M{"email": 1},
    Options: options.Index().SetUnique(true),
}
collection.Indexes().CreateOne(context.Background(), indexModel)
```

### 4. **Best Practices**

1. **Repository Pattern**: Pisahkan logic database dari business logic
2. **Service Layer**: Tempatkan business logic di service layer
3. **Dependency Injection**: Gunakan interface untuk loose coupling
4. **Error Handling**: Consistent error response format
5. **Validation**: Validate input di controller dan service level
6. **Context**: Gunakan context untuk timeout dan cancellation
7. **Logging**: Implement proper logging middleware
8. **Testing**: Write unit tests dan integration tests
9. **Environment**: Gunakan environment variables untuk configuration
10. **Documentation**: Dokumentasikan API endpoints

### 5. **Environment Setup untuk Development**

```bash
# Install tools
make install-tools

# Start databases
make docker-up

# Run with hot reload
make dev

# Run tests
make test

# Format and lint
make fmt && make lint
```

### 6. **Monitoring dan Performance**

- Gunakan middleware untuk logging request/response
- Implement health check endpoints
- Monitor database query performance
- Use connection pooling
- Implement caching strategy
- Add rate limiting untuk production

Modul ini memberikan foundation yang solid untuk membangun REST API menggunakan Go dan Gin dengan dukungan PostgreSQL dan MongoDB yang mudah digunakan dan tidak ribet!


func (r *PostRepository) GetAll(limit, offset int) ([]Post, error) {
    var posts []Post
    err := r.db.Limit(limit).Offset(offset).Order("created_at desc").Find(&posts).Error
    return posts, err
}

func (r *PostRepository) GetByUserID(userID uint) ([]Post, error) {
    var posts []Post
    err := r.db.Where("user_id = ?", userID).Order("created_at desc").Find(&posts).Error
    return posts, err
}

func (r *PostRepository) Update(post *Post) error {
    return r.db.Save(post).Error
}

func (r *PostRepository) Delete(id uint) error {
    return r.db.Delete(&Post{}, id).Error
}

func (r *PostRepository) GetWithUser(id uint) (*Post, error) {
    var post Post
    err := r.db.Preload("User").First(&post, id).Error
    if err != nil {
        if errors.Is(err, gorm.ErrRecordNotFound) {
            return nil, errors.New("post not found")
        }
        return nil, err
    }
    return &post, nil
}
