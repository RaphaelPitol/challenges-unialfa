#### Desafio 2 Ex-4 Atividade segundo Bimestre.
---
*Crie dois arquivos PHP:
O primeiro deve conter um formulário com dois campos: login, password
Ao se submeter no formulário, deve ser gravado na sessao do PHP esse login e password.*
*O segundo arquivo deve capturar da sessao o login e o password (se existir)
Pode ser listado os valores com o print_r*
login.php
~~~~php
<?php
session_start();

if ($_POST) {
    $login = $_POST['login'] ?? null;
    $senha = $_POST['senha'] ?? null;
    if ($login & $senha) {
        $key = random_bytes(SODIUM_CRYPTO_SECRETBOX_KEYBYTES);
        $nonce = random_bytes(SODIUM_CRYPTO_SECRETBOX_NONCEBYTES);
        $senha = sodium_crypto_secretbox($senha, $nonce, $key);
        $senha = bin2hex($senha);
        $_SESSION['login'] = array("login"=>$login, "senha"=>$senha);

        echo "<script>location.href='index.php'</script>";
    }
}
?>
<html lang="en">
<head>
  <title>Trabalho</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css">
  <script src="https://cdn.jsdelivr.net/npm/jquery@3.6.4/dist/jquery.slim.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/js/bootstrap.bundle.min.js"></script>
</head>
<div class="container">
    <h1 style='text-align: center;'>Cadastro Login</h1>
    <form method="POST" style='text-align: center;'>
        <label for="login">Login</label>
        <input type="text" name="login" id="login" class="form-control" placeholder="Login">

        <br>

        <label for="senha">Senha:</label>
        <input type="password" name="senha" id="senha" class="form-control" placeholder="Senha">
        <br>

        <button type="submit" class="btn btn-primary">Efetuar login</button>


    </form>

</div>
~~~~
---



index.php
~~~~php
<?php
session_start();
?>

<!DOCTYPE html>
<html lang="en">
<head>
  <title>Trabalho</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css">
  <script src="https://cdn.jsdelivr.net/npm/jquery@3.6.4/dist/jquery.slim.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>
    <div class="container">
    <h1>Cadastro de Login</h1>
        <ul class="list-group">
            <li class="list-group-item">login: <?=$_SESSION['login']['login']?></li>
            <li class="list-group-item">senha: <?=$_SESSION['login']['senha']?></li>
        </ul>
        <a href="login.php" type="button" class="btn btn-secondary">Voltar</a>
    </div>
</body>

</html>
~~~~