<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WelcomeMobi CRM - Вхід</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; background: #f8f9fa; color: #333; text-align: center; }
        #login-container { max-width: 400px; margin: auto; padding: 20px; background: white; border-radius: 5px; box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); }
        input, button { width: 100%; padding: 10px; margin: 5px 0; border-radius: 5px; border: 1px solid #ccc; }
        button { background: #007bff; color: white; border: none; cursor: pointer; }
        button:hover { background: #0056b3; }
        #crm-container { display: none; }
    </style>
</head>
<body>

    <div id="login-container">
        <h2>🔐 Вхід у WelcomeMobi CRM</h2>
        <input type="text" id="username" placeholder="Логін">
        <input type="password" id="password" placeholder="Пароль">
        <button onclick="login()">Увійти</button>
        <p>Ще не маєте акаунта? <button onclick="register()">Зареєструватися</button></p>
    </div>

    <div id="crm-container">
        <h2>WelcomeMobi CRM - Управління кандидатами</h2>
        <button onclick="logout()">🚪 Вийти</button>
        <p>Завантажується CRM...</p>
        <iframe src="https://alena182004.github.io/SRM-W/" width="100%" height="600px" style="border:none;"></iframe>
    </div>

    <script>
        function login() {
            let username = document.getElementById("username").value;
            let password = document.getElementById("password").value;

            let users = JSON.parse(localStorage.getItem("users")) || [];

            let user = users.find(u => u.username === username && u.password === password);
            if (user) {
                localStorage.setItem("loggedIn", "true");
                showCRM();
            } else {
                alert("❌ Невірний логін або пароль!");
            }
        }

        function register() {
            let username = prompt("Введіть новий логін:");
            let password = prompt("Введіть новий пароль:");

            if (!username || !password) {
                alert("❌ Логін і пароль не можуть бути порожніми!");
                return;
            }

            let users = JSON.parse(localStorage.getItem("users")) || [];
            if (users.find(u => u.username === username)) {
                alert("❌ Цей логін вже зайнятий!");
                return;
            }

            users.push({ username, password });
            localStorage.setItem("users", JSON.stringify(users));
            alert("✅ Реєстрація успішна! Тепер увійдіть.");
        }

        function showCRM() {
            document.getElementById("login-container").style.display = "none";
            document.getElementById("crm-container").style.display = "block";
        }

        function logout() {
            localStorage.removeItem("loggedIn");
            location.reload();
        }

        window.onload = function() {
            if (localStorage.getItem("loggedIn") === "true") {
                showCRM();
            }
        };
    </script>

</body>
</html>
