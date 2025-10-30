## 1. Simple PHP Calculator

A basic calculator that handles addition, subtraction, multiplication, and division with error handling for division by zero.

```php
<?php
// Simple PHP Calculator
// This script handles both displaying the form and processing the calculation.

$error = '';
$result = '';
$operation = '+'; // Default operation

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $num1 = isset($_POST['num1']) ? floatval($_POST['num1']) : 0;
    $num2 = isset($_POST['num2']) ? floatval($_POST['num2']) : 0;
    $operation = isset($_POST['operation']) ? $_POST['operation'] : '+';

    switch ($operation) {
        case '+':
            $result = $num1 + $num2;
            break;
        case '-':
            $result = $num1 - $num2;
            break;
        case '*':
            $result = $num1 * $num2;
            break;
        case '/':
            if ($num2 != 0) {
                $result = $num1 / $num2;
            } else {
                $error = 'Error: Division by zero!';
            }
            break;
        default:
            $error = 'Error: Invalid operation!';
    }
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple PHP Calculator</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 400px; margin: 50px auto; padding: 20px; border: 1px solid #ccc; }
        input, select { width: 100%; padding: 10px; margin: 5px 0; }
        button { width: 100%; padding: 10px; background: #007bff; color: white; border: none; cursor: pointer; }
        .result { font-size: 18px; font-weight: bold; color: green; margin: 10px 0; }
        .error { color: red; }
    </style>
</head>
<body>
    <h2>Simple Calculator</h2>
    
    <?php if ($error): ?>
        <p class="error"><?php echo $error; ?></p>
    <?php endif; ?>
    
    <?php if ($result !== ''): ?>
        <p class="result">Result: <?php echo $result; ?></p>
    <?php endif; ?>
    
    <form method="POST">
        <label>First Number:</label>
        <input type="number" name="num1" step="0.01" required value="<?php echo isset($_POST['num1']) ? htmlspecialchars($_POST['num1']) : ''; ?>">
        
        <label>Operation:</label>
        <select name="operation">
            <option value="+" <?php echo $operation === '+' ? 'selected' : ''; ?>>+</option>
            <option value="-" <?php echo $operation === '-' ? 'selected' : ''; ?>>-</option>
            <option value="*" <?php echo $operation === '*' ? 'selected' : ''; ?>>*</option>
            <option value="/" <?php echo $operation === '/' ? 'selected' : ''; ?>>/</option>
        </select>
        
        <label>Second Number:</label>
        <input type="number" name="num2" step="0.01" required value="<?php echo isset($_POST['num2']) ? htmlspecialchars($_POST['num2']) : ''; ?>">
        
        <button type="submit">Calculate</button>
    </form>
</body>
</html>
```


## 2. Even Odd Number Checker

Checks numbers in a range and displays even and odd numbers in a staggered table.

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Even Odd Checker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh; /* Fixed: was 10vh */
            background: #f0f0f0;
        }
        .container {
            background: white;
            padding: 30px;
            border-radius: 8px;
            max-width: 400px;
            width: 100%;
        }
        input[type="number"], button[type="submit"] { /* Fixed: button instead of input[type="submit"] */
            width: 100%;
            padding: 8px;
            margin-top: 8px;
            font-size: 16px;
        }
        .result {
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
  <div class="container">
    <h2>Even Odd Number Checker</h2>
    <form method="post">
      <label>Enter Starting Point:</label>
      <input type="number" name="start" required>
      <label>Enter Ending Point:</label>
      <input type="number" name="end" required>
      <button type="submit" name="submit">Go</button>
    </form>
    <?php
    if (isset($_POST['submit'])) {
      $start = intval($_POST['start']);
      $end = intval($_POST['end']);
      $even = [];
      $odd = [];
      for ($i = $start; $i <= $end; $i++) {
        if ($i % 2 == 0) {
          $even[] = $i;
        } else {
          $odd[] = $i;
        }
      }
      echo "<div class='result'>";
      echo "<table border='1' style='width:100%;text-align:center;'>";
      echo "<tr><th>Even</th><th>Odd</th></tr>";
      $maxCount = max(count($even), count($odd));
      for ($i = 0; $i < $maxCount; $i++) {
        echo "<tr>";
        echo "<td>" . ($even[$i] ?? '') . "</td><td>" . ($odd[$i] ?? '') . "</td>";
        echo "</tr>";
      }
      echo "</table></div>";
    }
    ?>
    </div>
</body>
</html>
```


## 3. Simple Login Page

A basic login form with hardcoded credentials.

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Page</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh; /* Fixed: was 70vh for full screen */
        }
        .login-container {
            background: white;
            padding: 48px;
            width: 420px;
            border-radius: 16px;
            box-shadow: 0px 6px 18px rgba(8, 8, 8, 0.18);
            text-align: center;
        }
        .login-container h2 {
            margin-bottom: 28px;
            color: #333;
            font-size: 2.2em;
            font-weight: bold;
        }
        .input-box {
            margin-bottom: 22px;
        }
        .input-box input {
            width: 100%;
            padding: 16px;
            border: 1px solid #aaa;
            border-radius: 8px;
            outline: none;
            font-size: 1.3em;
            text-align: center;
        }
        .btn {
            width: 100%;
            padding: 16px;
            background: #28a745;
            border: none;
            border-radius: 8px;
            font-size: 1.3em;
            font-weight: bold;
            color: white;
            cursor: pointer;
            transition: background 0.3s ease;
        }
        .btn:hover {
            background: #218838;
        }
        .message {
            margin-top: 22px;
            font-size: 1.0em;
        }
    </style>
</head>
<body>
    <div class="login-container">
        <h2>Login</h2>
        <form method="POST">
            <div class="input-box">
                <input type="text" name="username" placeholder="Enter Username" required>
            </div>
            <div class="input-box">
                <input type="password" name="password" placeholder="Enter Password" required>
            </div>
            <button type="submit" class="btn">Login</button>
        </form>
        <div class="message">
        <?php
            // PHP Login Validation
            $valid_username = "admin";
            $valid_password = "12345";
            $message = "";
            if ($_SERVER["REQUEST_METHOD"] == "POST") {
                $username = trim($_POST['username']);
                $password = $_POST['password'];
                if ($username === $valid_username && $password === $valid_password) {
                    $message = "<h2 style='color:green;'> Welcome, " . htmlspecialchars($username) . " 🎉</h2>";
                } else {
                    $message = "<h2 style='color:red;'> Invalid Username or Password!</h2>";
                }
            }
        ?>
        <?php echo $message; ?>
        </div>
    </div>
</body>
</html>
```


## 4. Electricity Bill Calculator

Calculates bill based on tiered rates.

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Electricity Bill Calculator</title>
    <style>
    body { background: #f7f7f7; font-family: Arial, sans-serif; }
    .card {
        background: #fff;
        padding: 32px;
        border-radius: 10px;
        width: 380px;
        margin: 60px auto;
        box-shadow: 0 2px 10px #ccc;
        text-align: center;
        height: auto; /* Fixed: was 30vh, too short */
    }
    h1 {
        font-size: 2em;
        margin-bottom: 18px;
        font-weight: bold;
    }
    input[type="number"] {
        width: 90%;
        margin: 12px auto;
        padding: 12px;
        font-size: 1.2em;
        border-radius: 6px;
        border: 1px solid #ccc;
        display: block;
        text-align: center;
    }
    button {
        width: 92%;
        padding: 12px;
        font-size: 1.15em;
        border-radius: 6px;
        background: #28a745;
        color: #fff;
        border: none;
        margin: 14px auto 0 auto;
        display: block;
    }
    .result {
        margin-top: 25px;
        font-size: 1.7em;
        font-weight: bold;
        text-align: center;
    }
    </style>
</head>
<body>
    <div class="card">
        <h1>Electricity Bill Calculator</h1>
        <form method="post">
            <input type="number" id="units" name="units" min="0" placeholder="Units" required>
            <button type="submit" name="calculate">Calculate Bill</button>
        </form>
        <?php
        if (isset($_POST['calculate'])) {
            function calculateElectricityBill($units) {
                $rate1 = 3.50;
                $rate2 = 4.00;
                $rate3 = 5.20;
                $rate4 = 6.50;
                $totalBill = 0.00;
                if ($units <= 50) {
                    $totalBill = $units * $rate1;
                }
                elseif ($units <= 150) {
                    $totalBill = (50 * $rate1) + (($units - 50) * $rate2);
                }
                elseif ($units <= 250) {
                    $totalBill = (50 * $rate1) + (100 * $rate2) + (($units - 150) * $rate3);
                }
                else {
                    $totalBill = (50 * $rate1) + (100 * $rate2) + (100 * $rate3) + (($units - 250) * $rate4);
                }
                return $totalBill;
            }
            $unitsUsed = intval($_POST['units']);
            $billAmount = calculateElectricityBill($unitsUsed);
            echo "<div class='result'>Bill for $unitsUsed units: Rs " . number_format($billAmount, 2) . "</div>";
        }
        ?>
    </div>
</body>
</html>
```


## 5. PHP Database Connection (Based on GeeksforGeeks)

Reference: [PHP Database Connection](https://www.geeksforgeeks.org/php/php-database-connection/)

Script to connect to MySQL and create a database.

```php
<?php
// Server name must be localhost
$servername = "localhost";

// In my case, user name will be root
$username = "root";

// Password is empty
$password = "";

// Creating a connection
$conn = new mysqli($servername, $username, $password);

// Check connection
if ($conn->connect_error) {
    die("Connection failure: " . $conn->connect_error);
} 

// Creating a database named geekdata
$sql = "CREATE DATABASE IF NOT EXISTS geekdata"; // Fixed: Added IF NOT EXISTS to avoid errors if exists
if ($conn->query($sql) === TRUE) {
    echo "Database 'geekdata' created successfully."; // Fixed: Completed sentence
} else {
    echo "Error: " . $conn->error;
}

// Closing connection
$conn->close();
?>
```

## 6. Session Management: Login System

A simple session-based login system with login, dashboard, and logout. Files: `login.php`, `login-check.php`, `dashboard.php`, `logout.php`.

### login.php
```php
<?php
// Session management: Check if user is already logged in
session_start();
// If already logged in, go to dashboard
if (isset($_SESSION['user'])) {
    header('Location: dashboard.php');
    exit;
}

$error = '';
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $username = isset($_POST['username']) ? trim($_POST['username']) : '';
    $password = isset($_POST['password']) ? $_POST['password'] : '';

    // Hard-coded demo credentials (change for production)
    $validUser = 'admin';
    $validPass = 'password123';

    if ($username === $validUser && $password === $validPass) {
        $_SESSION['user'] = $username;
        header('Location: dashboard.php');
        exit;
    } else {
        $error = 'Invalid username or password.';
    }
}
?>
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>Login</title>
    <style>body{font-family:Arial;max-width:420px;margin:40px auto;padding:20px;border:1px solid #ddd;}label,input{display:block;width:100%;margin-bottom:10px;}input[type=text],input[type=password]{padding:8px}</style>
</head>
<body>
    <h2>Login</h2>
    <?php if ($error): ?><p style="color:red"><?php echo htmlspecialchars($error); ?></p><?php endif; ?>
    <form method="post">
        <label>Username
            <input type="text" name="username" required autofocus>
        </label>
        <label>Password
            <input type="password" name="password" required>
        </label>
        <button type="submit">Login</button>
    </form>
    <p><small>Demo credentials: <strong>admin / password123</strong></small></p>
</body>
</html>
```

### login-check.php
```php
<?php
// Simple session check to protect pages
session_start();
if (!isset($_SESSION['user'])) {
    header('Location: login.php');
    exit;
}
?>
```

### dashboard.php
```php
<?php
require_once __DIR__ . '/login-check.php';
?>
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>Dashboard</title>
    <style>body{font-family:Arial;max-width:720px;margin:40px auto;padding:20px;} a{display:inline-block;margin-top:10px;}</style>
</head>
<body>
    <h1>Dashboard</h1>
    <p>Welcome, <strong><?php echo htmlspecialchars($_SESSION['user']); ?></strong>!</p>
    <p><a href="logout.php">Logout</a></p>
</body>
</html>
```

### logout.php
```php
<?php
session_start();
// Remove all session data and destroy session
$_SESSION = array();
if (ini_get('session.use_cookies')) {
    $params = session_get_cookie_params();
    setcookie(session_name(), '', time() - 42000,
        $params['path'], $params['domain'],
        $params['secure'], $params['httponly']
    );
}
session_destroy();
header('Location: login.php');
exit;
?>
```
