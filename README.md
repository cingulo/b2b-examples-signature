# Exemplos de como assinar usando o Fernet


## Python

O pacote [cryptography](https://pypi.org/project/cryptography/) fornece a implementação do Fernet. 

Para instalar

```
$ pip install cryptography
```

Após instalado podemos criptografar os dados:
```
signature_token = 'bk7SwmpUmLoLosRBaQlQTSTgiK4eVVHf4nddgrrG-Is='  # Esse token é fornecido pela Cingulo
fernet = Fernet(signature_token)
data = {"bid": "@@123456ABCDE@@", "e1": "extra field 1", "e2": "extra field 2", "e3": "extra field 3", "e4": "extra field 4", "e5": "extra field 5"}
data = str(data).encode()
encrypted_data = fernet.encrypt(data).decode()
print(encrypted_data)
```

Para testar se a criptografia funcionou
```
result = fernet.decrypt(encrypted_data.encode('utf-8')).decode()
print(result)
```


## Java

Com o artefato [fernet-java8](https://mvnrepository.com/artifact/com.macasaet.fernet/fernet-java8) podemos utilizar a implementação do Fernet.

Adicione no pom.xml a dependencia 
```
<dependency>
  <groupId>com.macasaet.fernet</groupId>
  <artifactId>fernet-java8</artifactId>
  <version>1.4.2</version>
</dependency>
```

Após o build do projeto podemos criptografar os dados.
No exemplo estamos usando Gson, mas pode ser usado qualquer biblioteca para gerar o json
```
var key = new Key("bk7SwmpUmLoLosRBaQlQTSTgiK4eVVHf4nddgrrG-Is="); // Esse token é fornecido pela Cingulo
var data = "{\"bid\": \"@@123456ABCDE@@\, \"e1\": \"extra field 1\", \"e2\": \"extra field 2\", \"e3\": \"extra field 3\", \"e4\": \"extra field 4\", \"e5\": \"extra field 5\"}";
var token = Token.generate(key, data);
var encrypted = token.serialise();
System.out.println(encrypted);
```

Para testar se a criptografia funcionou
```
var decryptedToken = Token.fromString(encrypted);
var decrypted = decryptedToken.validateAndDecrypt(key, new StringValidator() {
});
System.out.println(decrypted);
```

## Javascript

Com o package `fernet` poderemos criptografar os dados

Adiciona o package:
```
$ npm install fernet
```

Após instalado podemos criptografar os dados:

```
const secret = new fernet.Secret("bk7SwmpUmLoLosRBaQlQTSTgiK4eVVHf4nddgrrG-Is=");  // Esse token é fornecido pela Cingulo
const token = new fernet.Token({ secret: secret })
const data = "{\"bid\": \"@@123456ABCDE@@\, \"e1\": \"extra field 1\", \"e2\": \"extra field 2\", \"e3\": \"extra field 3\", \"e4\": \"extra field 4\", \"e5\": \"extra field 5\"}";
const encrypted = token.encode(data)
console.info(encrypted)
```

Para testar se a criptografia funcionou
```
const token = new fernet.Token({
  secret: secret,
  token: encrypted
})
const decrypted =  token.decode();
console.indo(decrypted)
```
