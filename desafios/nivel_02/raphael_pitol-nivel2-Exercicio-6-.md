### Resolução Desafio 2 Exercicio 6
---

~~~~
<?php
$servidor = "localhost";
$usuario = "root";
$senha = "";
$banco = "ex6";

$pdo = new PDO("mysql:host={$servidor};dbname={$banco};port=3306;charset=utf8;",$usuario,$senha);
~~~~
