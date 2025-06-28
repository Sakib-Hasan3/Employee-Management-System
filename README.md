# 👨‍💼 Employee Management System (C# .NET MVC + SQL Server)

A web-based Employee Management System built with ASP.NET MVC and SQL Server. It allows an organization to manage employees, attendance, payroll, leaves, shifts, and productivity efficiently.

---

## 🔧 Technologies Used

- **Frontend**: HTML, CSS, JavaScript, Bootstrap  
- **Backend**: ASP.NET MVC (C#)
- **Database**: Microsoft SQL Server
- **ORM**: Entity Framework
- **IDE**: Visual Studio

---

## ⚙️ Features

- Employee CRUD operations  
- Attendance tracking  
- Leave management  
- Payroll processing  
- Shift scheduling & productivity  
- Role-based user authentication  

---

## 🗂 Folder Structure

```
/EmployeeManagementSystem
├── Controllers/
├── Models/
├── Views/
│   ├── Employee/
│   ├── Attendance/
│   └── Shared/
├── Scripts/
├── App_Data/
├── web.config
└── Global.asax
```

---

## 🏁 Getting Started

### 🔗 Prerequisites

- Visual Studio 2019 or later  
- SQL Server 2016 or later  
- .NET Framework 4.7.2 or later  

### 🔨 Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/EmployeeManagementSystem.git
   cd EmployeeManagementSystem
   ```

2. **Open in Visual Studio**
   - Open `EmployeeManagementSystem.sln` file

3. **Configure the Database**
   - Update the connection string in `web.config`:
   ```xml
   <connectionStrings>
       <add name="DefaultConnection" 
            connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=EmployeeDB;Integrated Security=True"
            providerName="System.Data.SqlClient" />
   </connectionStrings>
   ```

4. **Run Entity Framework Migrations (Optional)**
   ```powershell
   Update-Database
   ```

5. **Build and Run**
   - Press `F5` to start the development server

---

## 📦 Sample Code Snippets

### 🚀 Employee Model

```csharp
public class Employee
{
    public int EmployeeID { get; set; }

    [Required]
    public string Name { get; set; }

    public string Department { get; set; }

    public DateTime JoiningDate { get; set; }

    public decimal Salary { get; set; }
}
```

### 🧠 Employee Controller

```csharp
public class EmployeeController : Controller
{
    private ApplicationDbContext db = new ApplicationDbContext();

    public ActionResult Index()
    {
        return View(db.Employees.ToList());
    }

    public ActionResult Create()
    {
        return View();
    }

    [HttpPost]
    public ActionResult Create(Employee emp)
    {
        if (ModelState.IsValid)
        {
            db.Employees.Add(emp);
            db.SaveChanges();
            return RedirectToAction("Index");
        }
        return View(emp);
    }
}
```

### 📄 Employee View (Index.cshtml)

```html
@model IEnumerable<EmployeeManagementSystem.Models.Employee>

<table class="table table-bordered">
    <tr>
        <th>Name</th>
        <th>Department</th>
        <th>Joining Date</th>
        <th>Salary</th>
    </tr>
@foreach (var item in Model) {
    <tr>
        <td>@item.Name</td>
        <td>@item.Department</td>
        <td>@item.JoiningDate.ToShortDateString()</td>
        <td>@item.Salary</td>
    </tr>
}
</table>
```

---

## 📁 SQL Script for Table Creation

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY IDENTITY,
    Name NVARCHAR(100) NOT NULL,
    Department NVARCHAR(50),
    JoiningDate DATE,
    Salary DECIMAL(18,2)
);
```

---

## ✅ TODO (for Expansion)

- [ ] Add Role-Based Access Control  
- [ ] Implement AJAX search/filtering  
- [ ] Generate PDF reports  
- [ ] Add Email Notifications  

---

## 📜 License

This project is licensed under the MIT License. See `LICENSE` for more details.

---

