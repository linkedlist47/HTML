I'll help you create a simple PHP application for inserting and updating records in a MySQL database. Here's a complete solution:

## 1. Database Setup

First, let's create the database and table:

```sql
CREATE DATABASE user_management;
USE user_management;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    phone VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 2. Configuration File (config.php)

```php
<?php
// config.php
class Database {
    private $host = "localhost";
    private $db_name = "user_management";
    private $username = "root"; // Change if needed
    private $password = ""; // Change if needed
    public $conn;

    public function getConnection() {
        $this->conn = null;
        try {
            $this->conn = new PDO("mysql:host=" . $this->host . ";dbname=" . $this->db_name, $this->username, $this->password);
            $this->conn->exec("set names utf8");
            $this->conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        } catch(PDOException $exception) {
            echo "Connection error: " . $exception->getMessage();
        }
        return $this->conn;
    }
}
?>
```

## 3. User Class (User.php)

```php
<?php
// User.php
class User {
    private $conn;
    private $table_name = "users";

    public $id;
    public $name;
    public $email;
    public $phone;

    public function __construct($db) {
        $this->conn = $db;
    }

    // Create user
    public function create() {
        $query = "INSERT INTO " . $this->table_name . " 
                 SET name=:name, email=:email, phone=:phone";
        
        $stmt = $this->conn->prepare($query);

        // Sanitize inputs
        $this->name = htmlspecialchars(strip_tags($this->name));
        $this->email = htmlspecialchars(strip_tags($this->email));
        $this->phone = htmlspecialchars(strip_tags($this->phone));

        // Bind parameters
        $stmt->bindParam(":name", $this->name);
        $stmt->bindParam(":email", $this->email);
        $stmt->bindParam(":phone", $this->phone);

        if($stmt->execute()) {
            return true;
        }
        return false;
    }

    // Update user
    public function update() {
        $query = "UPDATE " . $this->table_name . " 
                 SET name=:name, email=:email, phone=:phone 
                 WHERE id=:id";
        
        $stmt = $this->conn->prepare($query);

        // Sanitize inputs
        $this->name = htmlspecialchars(strip_tags($this->name));
        $this->email = htmlspecialchars(strip_tags($this->email));
        $this->phone = htmlspecialchars(strip_tags($this->phone));
        $this->id = htmlspecialchars(strip_tags($this->id));

        // Bind parameters
        $stmt->bindParam(":name", $this->name);
        $stmt->bindParam(":email", $this->email);
        $stmt->bindParam(":phone", $this->phone);
        $stmt->bindParam(":id", $this->id);

        if($stmt->execute()) {
            return true;
        }
        return false;
    }

    // Read single user
    public function readOne() {
        $query = "SELECT * FROM " . $this->table_name . " WHERE id = ? LIMIT 0,1";
        $stmt = $this->conn->prepare($query);
        $stmt->bindParam(1, $this->id);
        $stmt->execute();

        $row = $stmt->fetch(PDO::FETCH_ASSOC);

        if($row) {
            $this->name = $row['name'];
            $this->email = $row['email'];
            $this->phone = $row['phone'];
            return true;
        }
        return false;
    }

    // Read all users
    public function readAll() {
        $query = "SELECT * FROM " . $this->table_name . " ORDER BY created_at DESC";
        $stmt = $this->conn->prepare($query);
        $stmt->execute();
        return $stmt;
    }
}
?>
```

## 4. Main Form (index.php)

```php
<?php
// index.php
include_once 'config.php';
include_once 'User.php';

$database = new Database();
$db = $database->getConnection();
$user = new User($db);

$message = '';
$action = isset($_GET['action']) ? $_GET['action'] : 'create';
$user_id = isset($_GET['id']) ? $_GET['id'] : '';

// If editing, load user data
if($action == 'edit' && $user_id) {
    $user->id = $user_id;
    $user->readOne();
}

// Process form submission
if($_POST){
    $user->name = $_POST['name'];
    $user->email = $_POST['email'];
    $user->phone = $_POST['phone'];
    
    if($action == 'edit' && isset($_POST['id'])) {
        $user->id = $_POST['id'];
        if($user->update()){
            $message = "<div class='alert alert-success'>User was updated.</div>";
            $action = 'create'; // Reset to create mode
        } else{
            $message = "<div class='alert alert-danger'>Unable to update user.</div>";
        }
    } else {
        if($user->create()){
            $message = "<div class='alert alert-success'>User was created.</div>";
        } else{
            $message = "<div class='alert alert-danger'>Unable to create user.</div>";
        }
    }
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Management</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .container { max-width: 800px; margin-top: 50px; }
        .table-actions { white-space: nowrap; }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="mb-4">User Management System</h1>
        
        <?php echo $message; ?>
        
        <div class="card mb-4">
            <div class="card-header">
                <h5 class="mb-0">
                    <?php echo ($action == 'edit') ? 'Edit User' : 'Add New User'; ?>
                </h5>
            </div>
            <div class="card-body">
                <form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>" method="post">
                    <?php if($action == 'edit'): ?>
                        <input type="hidden" name="id" value="<?php echo $user->id; ?>">
                    <?php endif; ?>
                    
                    <div class="mb-3">
                        <label for="name" class="form-label">Name *</label>
                        <input type="text" class="form-control" id="name" name="name" 
                               value="<?php echo isset($user->name) ? $user->name : ''; ?>" required>
                    </div>
                    
                    <div class="mb-3">
                        <label for="email" class="form-label">Email *</label>
                        <input type="email" class="form-control" id="email" name="email" 
                               value="<?php echo isset($user->email) ? $user->email : ''; ?>" required>
                    </div>
                    
                    <div class="mb-3">
                        <label for="phone" class="form-label">Phone</label>
                        <input type="text" class="form-control" id="phone" name="phone" 
                               value="<?php echo isset($user->phone) ? $user->phone : ''; ?>">
                    </div>
                    
                    <button type="submit" class="btn btn-primary">
                        <?php echo ($action == 'edit') ? 'Update User' : 'Create User'; ?>
                    </button>
                    
                    <?php if($action == 'edit'): ?>
                        <a href="index.php" class="btn btn-secondary">Cancel</a>
                    <?php endif; ?>
                </form>
            </div>
        </div>

        <!-- Users List -->
        <div class="card">
            <div class="card-header">
                <h5 class="mb-0">Users List</h5>
            </div>
            <div class="card-body">
                <?php
                $stmt = $user->readAll();
                $num = $stmt->rowCount();

                if($num > 0){
                    echo "<div class='table-responsive'>";
                    echo "<table class='table table-striped'>";
                    echo "<thead>";
                    echo "<tr>";
                    echo "<th>ID</th>";
                    echo "<th>Name</th>";
                    echo "<th>Email</th>";
                    echo "<th>Phone</th>";
                    echo "<th>Actions</th>";
                    echo "</tr>";
                    echo "</thead>";
                    echo "<tbody>";

                    while ($row = $stmt->fetch(PDO::FETCH_ASSOC)){
                        extract($row);
                        echo "<tr>";
                        echo "<td>{$id}</td>";
                        echo "<td>{$name}</td>";
                        echo "<td>{$email}</td>";
                        echo "<td>{$phone}</td>";
                        echo "<td class='table-actions'>";
                        echo "<a href='index.php?action=edit&id={$id}' class='btn btn-sm btn-warning'>Edit</a>";
                        echo "</td>";
                        echo "</tr>";
                    }
                    echo "</tbody>";
                    echo "</table>";
                    echo "</div>";
                } else {
                    echo "<p class='text-muted'>No users found.</p>";
                }
                ?>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

## 5. How to Use

1. **Setup Database**: Run the SQL script to create the database and table
2. **Configure**: Update database credentials in `config.php`
3. **Run Application**: Place all files in your web server directory and access `index.php`

## Features

- **Add Users**: Fill the form and click "Create User"
- **Edit Users**: Click "Edit" button next to any user in the list
- **Form Validation**: Basic HTML5 validation for required fields
- **Responsive Design**: Bootstrap-based responsive layout
- **Error Handling**: Shows success/error messages for operations

## File Structure

```
/your-project-folder/
├── config.php
├── User.php
└── index.php
```

## Security Notes

- The code includes basic input sanitization
- Uses PDO prepared statements to prevent SQL injection
- Consider adding more validation and CSRF protection for production use
- Add password fields and proper authentication for real applications

This provides a complete CRUD (Create, Read, Update) application for user management. You can extend it further by adding delete functionality, pagination, search, and more advanced features as needed.
