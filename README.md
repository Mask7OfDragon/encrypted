# encrypted
Very basic encryption system for login systems 

# To do list
- [ ] Add class to improve use
- [ ] Add More Encryption Options

## How to use
Here you will find how to use the file to encrypt or decrypt

### encrypted

```php
<?php 

	require_once('encrypted_config.php'); // Llamamos a nuestra configuracion 

	function encrypt($string) // Creamos el metodo de encriptacion
	{
		$output = FALSE;
		$key = hash('sha256', SECRET_KEY); // Establecemos nuestra SECRET_KEY
		$iv = substr(hash('sha256', SECRET_KEY), 0, 16); // Añadimos la encriptacion a usar en este caso sha256

		$output = openssl_encrypt($string, METHOD, $key, 0, $iv);
		$output = base64_encode($output);

		return $output;
	}

$ejemplo = "4600 5600 5600 5600"; // En este ejemplo estoy imitando una tarjeta de crédito
echo encrypt($ejemplo) // Mostramos la string, ya con el metodo aplicado 

?>
```

### desencrypter

```php
<?php 

	require_once('encrypted_config.php'); // Llamamos a nuestra configuracion 

	function decrypt($string) // Creamos el metodo de desencriptacion
	{
		$output = FALSE;
		$key = hash('sha256', SECRET_KEY); // Establecemos nuestra SECRET_KEY
		$iv = substr(hash('sha256', SECRET_KEY), 0, 16); // Los parametros correctos, para asegurar la integridad del resultado

		$output = openssl_decrypt(base64_decode($string), METHOD, $key, 0, $iv); // Resolvemos

		return $output;
	}

echo decrypt('TnlWbEJqR0gvRUxxQ2x5ZjNFczJoSldmQk4zUGR5MlloOFJyaWNodlFKMD0='); // Adjuntamos el valor a desencriptar

?>
```
