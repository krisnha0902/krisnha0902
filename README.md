// Database connection
$conn = new mysqli('localhost', 'username', 'password', 'vet_db');

// User registration
if(isset($_POST['register'])){
    $email = $_POST['email'];
    $password = password_hash($_POST['password'], PASSWORD_BCRYPT);

    $query = "INSERT INTO users (email, password) VALUES ('$email', '$password')";
    $conn->query($query);
}

// User login
if(isset($_POST['login'])){
    $email = $_POST['email'];
    $password = $_POST['password'];

    $query = "SELECT * FROM users WHERE email='$email'";
    $result = $conn->query($query);
    $user = $result->fetch_assoc();

    if(password_verify($password, $user['password'])){
        $_SESSION['user'] = $user['email'];
    } else {
        echo "Invalid credentials";
    }
}

