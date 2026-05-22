# Golang Inventory Management System (CRUD)

[![Go Version](https://img.shields.io/badge/Go-1.21+-blue.svg)](https://golang.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)]()

> A comprehensive web-based inventory management system built with Go, featuring user authentication, product management, and stock control.

**สำหรับเวอร์ชันภาษาไทย:** [README_TH.md](Readme/README_TH.md)

## ✨ Features

### 🔐 Authentication & Authorization
- User login with username/password
- Session management using Gorilla Sessions
- Role-based access control (Admin/Staff)
- Secure logout functionality
- Login middleware protection

### 📦 Product Management
- Create, Read, Update, Delete products
- Product categorization
- Stock level tracking (min/max)
- Unit measurement support
- Cost and price tracking
- Product status management
- Barcode support

### 🏷️ Category Management
- Manage product categories
- Organize products by category
- Quick filtering by category

### 📊 Stock Management
- **Stock In (รับสินค้าเข้า)**: Record incoming inventory
- **Stock Out (เบิกออก)**: Record outgoing inventory
- **Stock Movements**: Track all stock transactions
- Automatic stock level updates
- Low stock alerts

### 🔍 Search & Filter
- Search by product name
- Search by product code
- Filter by category
- Filter by status
- Dynamic filtering

### 📈 Dashboard
- Quick overview of inventory
- Stock status visualization
- Recent transactions
- System status

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Backend** | Go (1.21+) |
| **Database** | MySQL |
| **Frontend** | HTML5, CSS3, JavaScript |
| **Templates** | Go html/template |
| **Session Management** | Gorilla Sessions |
| **HTTP Framework** | Go net/http |

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Go 1.21** or higher - [Download](https://golang.org/dl/)
- **MySQL 5.7** or higher - [Download](https://www.mysql.com/downloads/)
- **Git** - [Download](https://git-scm.com/)
- **PowerShell** (for Windows users)

## ⚙️ Installation

### Step 1: Clone or Setup the Repository

```bash
# Clone from git
git clone <your-repository-url>
cd golang-crud
```

### Step 2: Setup Database

```bash
# Open MySQL Command Line
mysql -u root -p

# Create database
CREATE DATABASE golang_crud;
USE golang_crud;

# Import database schema
SOURCE Readme/database.sql;

# Exit MySQL
EXIT;
```

**Default Login Credentials:**
- Username: `admin`
- Password: `admin123`

### Step 3: Install Go Dependencies

```bash
go mod download
go mod tidy
```

Required packages:
- `github.com/go-sql-driver/mysql` - MySQL database driver
- `github.com/gorilla/sessions` - Session management
- `github.com/gorilla/securecookie` - Secure cookies

### Step 4: Update Database Connection

Edit `main.go` and update the database connection string (usually around line 50):

```go
// Update with your MySQL credentials
dsn := "username:password@tcp(localhost:3306)/golang_crud?parseTime=true"
```

### Step 5: Run the Application

**Option 1: Using PowerShell Script (Windows)**
```powershell
.\Readme\start.ps1
```

**Option 2: Using Go directly**
```bash
go run main.go
```

The application will start on: **http://localhost:8080**

## 🚀 Quick Start

1. **Access the Application**
   - Open your web browser
   - Navigate to: http://localhost:8080

2. **Login**
   - Username: `admin`
   - Password: `admin123`

3. **First Time Setup**
   - Click "สินค้า" (Products) to add your first product
   - Fill in product details (name, code, price, stock)
   - Save the product
   - Test stock movements using "รับสินค้าเข้า" (Stock In)

## 📁 Project Structure

```
golang-crud/
├── main.go                 # Main application file
├── go.mod                  # Go module definition
├── README.md              # This file
├── Readme/                # Documentation folder
│   ├── QUICKSTART.md      # Quick start guide
│   ├── FEATURES.md        # Detailed features list
│   ├── SETUP.md           # Setup instructions
│   ├── USAGE_GUIDE.md     # User guide
│   ├── USER_MANUAL.md     # User manual
│   ├── CATEGORY_MANAGEMENT.md
│   ├── README_INVENTORY.md
│   ├── README_TH.md       # Thai documentation
│   ├── database.sql       # Database schema
│   └── start.ps1          # PowerShell startup script
└── templates/             # HTML templates
    ├── layout.html        # Base layout template
    ├── login.html         # Login page
    ├── dashboard.html     # Dashboard
    ├── product_list.html  # Product list
    ├── product_form.html  # Product form
    ├── category_list.html # Category list
    ├── category_form.html # Category form
    ├── stock_in.html      # Stock in form
    ├── stock_out.html     # Stock out form
    ├── stock_movements.html # Stock movements
    ├── form.html          # Generic form
    └── list.html          # Generic list
```

## 📖 Core Data Structures

### User
```go
type User struct {
    ID        int
    Name      string
    Email     string
    Phone     string
    Address   string
    CreatedAt time.Time
}
```

### Product
```go
type Product struct {
    ID            int
    Code          string
    Name          string
    CategoryID    int
    CategoryName  string
    Description   string
    Unit          string
    Price         float64
    Cost          float64
    StockQuantity int
    MinStock      int
    MaxStock      int
    // ... additional fields
}
```

### Category
```go
type Category struct {
    ID          int
    Name        string
    Description string
    CreatedAt   time.Time
}
```

## 🔧 Configuration

### Database Connection
Update the DSN (Data Source Name) in `main.go`:

```go
dsn := "username:password@tcp(localhost:3306)/golang_crud?parseTime=true"
```

### Session Secret Key
Change the session secret key in production:

```go
var store = sessions.NewCookieStore([]byte("change-this-secret-key-in-production"))
```

### Server Port
Default port is `:8080`. To change, modify the server configuration in `main.go`.

## 🧪 Testing Checklist

- [ ] User login/logout works
- [ ] Add new product
- [ ] Edit product
- [ ] Delete product (soft delete)
- [ ] Add category
- [ ] Stock in operation
- [ ] Stock out operation
- [ ] Search functionality
- [ ] Filter functionality
- [ ] Dashboard displays correctly

## 📝 Database Tables

The application uses the following main tables:

- `users` - User authentication and details
- `products` - Product inventory
- `categories` - Product categories
- `stock_movements` - Stock transaction history
- `stock_in` - Incoming stock records
- `stock_out` - Outgoing stock records

See [database.sql](Readme/database.sql) for the complete schema.

## 🐛 Troubleshooting

### Connection Refused
```
Error: Connection refused
```
**Solution**: Ensure MySQL is running and the connection string is correct.

### Module Not Found
```
Error: cannot find module
```
**Solution**: Run `go mod download` and `go mod tidy`

### Port Already in Use
```
Error: Address already in use
```
**Solution**: Change the port in main.go or stop the process using port 8080.

### Session Errors
Ensure the session secret key is set correctly and hasn't changed between restarts.

## 📚 Documentation

For more detailed information, see:
- [Quick Start Guide](Readme/QUICKSTART.md)
- [Complete Features List](Readme/FEATURES.md)
- [Setup Instructions](Readme/SETUP.md)
- [Usage Guide](Readme/USAGE_GUIDE.md)
- [User Manual](Readme/USER_MANUAL.md)

## 🎯 Future Enhancements

- [ ] Role-based access control improvements
- [ ] API endpoints (REST)
- [ ] Advanced reporting
- [ ] Email notifications
- [ ] Mobile app
- [ ] Multi-warehouse support
- [ ] Barcode scanning integration
- [ ] Export to Excel/PDF

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

**Punyawit**
- GitHub: [@Punyawit](https://github.com/Punyawit)
- Facebook: [Punyawit](https://www.facebook.com/punyawit.richut/)

## 📞 Support

If you encounter any issues, please:
1. Check the [Troubleshooting](#-troubleshooting) section
2. Review the [Documentation](Readme/)
3. Open an issue on GitHub

---

**Last Updated**: May 2026

**Status**: ✅ Active Development
