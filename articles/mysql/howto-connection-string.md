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
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a><span data-ttu-id="a9034-103">Nasıl tooconnect uygulamaları tooAzure veritabanı için MySQL</span><span class="sxs-lookup"><span data-stu-id="a9034-103">How tooconnect applications tooAzure Database for MySQL</span></span>
<span data-ttu-id="a9034-104">Bu belgede Azure veritabanı tarafından MySQL için şablon ve örnek ile birlikte desteklenen hello bağlantı dizesi türlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="a9034-104">This document lists hello connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="a9034-105">Bağlantı dizenizi farklı parametreler ve farklı ayarlara sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="a9034-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="a9034-106">tooobtain hello sertifika bkz [nasıl tooconfigure SSL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a9034-106">tooobtain hello certificate, see [How tooconfigure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="a9034-107">{your_host} = <servername>. mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="a9034-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="a9034-108">{your_user}@{servername} UserID biçimi kimlik doğrulaması için doğru =.</span><span class="sxs-lookup"><span data-stu-id="a9034-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="a9034-109">Yalnızca hello UserID kullanarak hello kimlik doğrulama toofail neden olur.</span><span class="sxs-lookup"><span data-stu-id="a9034-109">Using just hello userID will cause hello authentication toofail.</span></span>

## <a name="adonet"></a><span data-ttu-id="a9034-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="a9034-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="a9034-111">Bu örnekte, hello sunucu adıdır `myserver4demo`, veritabanı adı `wpdb`, kullanıcı adı `WPAdmin`, ve parola `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="a9034-111">In this example, hello server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="a9034-112">Ardından, hello bağlantı dizesi olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="a9034-112">Then, hello connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="a9034-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="a9034-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="a9034-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="a9034-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="a9034-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="a9034-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="a9034-116">PHP</span><span class="sxs-lookup"><span data-stu-id="a9034-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="a9034-117">Python</span><span class="sxs-lookup"><span data-stu-id="a9034-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="a9034-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="a9034-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a><span data-ttu-id="a9034-119">Azure portal hello Hello bağlantı dizesi ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="a9034-119">Get hello connection string details from hello Azure portal</span></span>
<span data-ttu-id="a9034-120">Merhaba, [Azure portal](https://portal.azure.com), MySQL sunucusu için Azure veritabanı tooyour gidin ve ardından **bağlantı dizeleri** dizenizi listesinde Örneğiniz için tooget: ![hello bağlantı dizeleri Bölmesi'nde hello Azure portalı](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="a9034-120">In hello [Azure portal](https://portal.azure.com), go tooyour Azure Database for MySQL server, and then click **Connection strings** tooget your string list for your instance: ![hello Connection strings pane in hello Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="a9034-121">Merhaba dize hello sürücü, sunucu ve diğer veritabanı bağlantı parametrelerini gibi ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9034-121">hello string provides details such as hello driver, server, and other database connection parameters.</span></span> <span data-ttu-id="a9034-122">Bu örnekler, veritabanı adı, parola vb. gibi kendi parametrelerinizi kullanarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a9034-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="a9034-123">Daha sonra bu dize tooconnect toohello sunucu kodu ve uygulamalardan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9034-123">You can then use this string tooconnect toohello server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9034-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9034-124">Next steps</span></span>
- <span data-ttu-id="a9034-125">Bağlantı kitaplıkları hakkında daha fazla bilgi için bkz: [kavramlar - bağlantı kitaplıkları](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="a9034-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
