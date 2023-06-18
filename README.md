# Assignment1-PHP
!DOCTYPE html>
<html>
<head>
    
    <header>
      

  <title>Employee Portal</title>
</head>
<body>
  <h1>Welcome to the Employee Portal</h1>
  </nav>
    <img src="logo.png" alt="Logo">

  <form>
    <h2>Employee Login</h2>
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required><br>

    <label for="password">Password:</label>
    <input type="password" id="password" name="password" required><br>

    <button type="submit">Login</button>
  </form>

  <hr>

  <h2>Employee Information</h2>
  <table>
    <tr>
      <th>Name</th>
      <th>Position</th>
      <th>Hours Worked</th>
    </tr>
    <tr>
      <td>John Doe</td>
      <td>Software Engineer</td>
      <td>40</td>
    </tr>
    <tr>
      <td>Jane Smith</td>
      <td>Project Manager</td>
      <td>35</td>
    </tr>
    <!-- Add more employee rows here -->
  </table>

  <hr>

  <h2>Track Hours</h2>
  <form>
    <label for="employee-name">Employee Name:</label>
    <input type="text" id="employee-name" name="employee-name" required><br>

    <label for="hours-worked">Hours Worked:</label>
    <input type="number" id="hours-worked" name="hours-worked" min="0" required><br>

    <button type="submit">Submit</button>
  </form>
</body>
</html>

       
    </header>

    <form method="POST" action="save_content.php">
      
        <input type="text" name="title" placeholder="Title" required>
        <textarea name="content" placeholder="Content" required></textarea>
        <input type="submit" value="Submit">
    </form>

    <footer>
        
    </footer>
</body>
</html>

PHP (save_content.php):
<?php
// Establish a database connection
$host = "localhost";
$db_name = "your_database_name";
$username = "your_username";
$password = "your_password";

try {
    $conn = new PDO("mysql:host=$host;dbname=$db_name", $username, $password);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch(PDOException $e) {
    die("Database connection failed: " . $e->getMessage());
}

// Validate and store form data
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $title = $_POST["title"];
    $content = $_POST["content"];

    // Save the form data to the database table
    $stmt = $conn->prepare("INSERT INTO your_table_name (title, content) VALUES (:title, :content)");
    $stmt->bindParam(":title", $title);
    $stmt->bindParam(":content", $content);

    try {
        $stmt->execute();
        echo "Content saved successfully!";
    } catch(PDOException $e) {
        echo "Error: " . $e->getMessage();
    }
}

// Close the database connection
$conn = null;
?>
