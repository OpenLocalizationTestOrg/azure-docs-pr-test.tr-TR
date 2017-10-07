---
title: "aaaConnect uygulamaları tooAzure veritabanı için MySQL | Microsoft Docs"
description: "Bu belgede Azure veritabanı ile uygulamaları tooconnect için şu anda desteklenen hello bağlantı dizelerini ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python ve Ruby gibi MySQL için listeler."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a>Nasıl tooconnect uygulamaları tooAzure veritabanı için MySQL
Bu belgede Azure veritabanı tarafından MySQL için şablon ve örnek ile birlikte desteklenen hello bağlantı dizesi türlerini listeler. Bağlantı dizenizi farklı parametreler ve farklı ayarlara sahip olabilir.

- tooobtain hello sertifika bkz [nasıl tooconfigure SSL](./howto-configure-ssl.md).
- {your_host} = <servername>. mysql.database.azure.com
- {your_user}@{servername} UserID biçimi kimlik doğrulaması için doğru =.  Yalnızca hello UserID kullanarak hello kimlik doğrulama toofail neden olur.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

Bu örnekte, hello sunucu adıdır `myserver4demo`, veritabanı adı `wpdb`, kullanıcı adı `WPAdmin`, ve parola `mypassword!2`. Ardından, hello bağlantı dizesi olması gerekir:

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a>JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a>Node.js
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a>ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a>PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a>Python
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a>Ruby
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a>Azure portal hello Hello bağlantı dizesi ayrıntıları
Merhaba, [Azure portal](https://portal.azure.com), MySQL sunucusu için Azure veritabanı tooyour gidin ve ardından **bağlantı dizeleri** dizenizi listesinde Örneğiniz için tooget: ![hello bağlantı dizeleri Bölmesi'nde hello Azure portalı](./media/howto-connection-strings/connection-strings-on-portal.png)

Merhaba dize hello sürücü, sunucu ve diğer veritabanı bağlantı parametrelerini gibi ayrıntıları sağlar. Bu örnekler, veritabanı adı, parola vb. gibi kendi parametrelerinizi kullanarak değiştirin. Daha sonra bu dize tooconnect toohello sunucu kodu ve uygulamalardan kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
- Bağlantı kitaplıkları hakkında daha fazla bilgi için bkz: [kavramlar - bağlantı kitaplıkları](./concepts-connection-libraries.md).
