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
        $_SESSION['login'] = $login;

        $key = random_bytes(SODIUM_CRYPTO_SECRETBOX_KEYBYTES);
        $nonce = random_bytes(SODIUM_CRYPTO_SECRETBOX_NONCEBYTES);
        $senha = sodium_crypto_secretbox($senha, $nonce, $key);
        $senha = bin2hex($senha);
        $_SESSION['senha'] = $senha;

        echo "<script>location.href='index.php'</script>";
    }
}
?>

<div>
    <h1 style='text-align: center;'>Cadastro Login</h1>
    <form method="POST" style='text-align: center;'>
        <label for="login">Login</label>
        <input type="text" name="login" id="login" class="form-control" placeholder="Login">

        <label for="senha">Senha:</label>
        <input type="password" name="senha" id="senha" class="form-control" placeholder="Senha">

        <button type="submit" class="btn btn-success w-100">Efetuar login</button>


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
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Cadastro de Login</h1>
    <?php
    print_r($_SESSION);
    ?>
    <a href="login.php">Voltar</a>
</body>
</html>
~~~~