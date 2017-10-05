---
title: "MySQL için Azure veritabanı uygulamalarını bağlamak | Microsoft Docs"
description: "Bu belge, uygulamalarının ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python ve Ruby gibi MySQL için Azure veritabanı ile bağlantı şu anda desteklenen bağlantı dizeleri listeler."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: 2f40da41bcfda7e35f6fc63ead5d055246ab390c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a><span data-ttu-id="1d924-103">MySQL için Azure veritabanı uygulamalara bağlanma</span><span class="sxs-lookup"><span data-stu-id="1d924-103">How to connect applications to Azure Database for MySQL</span></span>
<span data-ttu-id="1d924-104">Bu belgede Azure veritabanı tarafından MySQL için şablon ve örnek ile birlikte desteklenen bağlantı dizesi türlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="1d924-104">This document lists the connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="1d924-105">Bağlantı dizenizi farklı parametreler ve farklı ayarlara sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="1d924-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="1d924-106">Sertifikayı edinmek için bkz: [SSL nasıl yapılandırılacağı](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="1d924-106">To obtain the certificate, see [How to configure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="1d924-107">{your_host} = <servername>. mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="1d924-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="1d924-108">{your_user}@{servername} UserID biçimi kimlik doğrulaması için doğru =.</span><span class="sxs-lookup"><span data-stu-id="1d924-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="1d924-109">Yalnızca UserID kullanarak kimlik doğrulamasının başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="1d924-109">Using just the userID will cause the authentication to fail.</span></span>

## <a name="adonet"></a><span data-ttu-id="1d924-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="1d924-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="1d924-111">Bu örnekte, sunucu adı olan `myserver4demo`, veritabanı adı `wpdb`, kullanıcı adı `WPAdmin`, ve parola `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="1d924-111">In this example, the server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="1d924-112">Ardından, bağlantı dizesi olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="1d924-112">Then, the connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="1d924-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="1d924-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="1d924-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="1d924-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="1d924-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="1d924-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="1d924-116">PHP</span><span class="sxs-lookup"><span data-stu-id="1d924-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="1d924-117">Python</span><span class="sxs-lookup"><span data-stu-id="1d924-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="1d924-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="1d924-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a><span data-ttu-id="1d924-119">Bağlantı dizesi ayrıntıları Azure portalından alın.</span><span class="sxs-lookup"><span data-stu-id="1d924-119">Get the connection string details from the Azure portal</span></span>
<span data-ttu-id="1d924-120">İçinde [Azure portal](https://portal.azure.com), MySQL sunucusu için Azure veritabanınızı gidin ve ardından **bağlantı dizeleri** Örneğiniz için dize listenize alınacağı: ![bağlantı dizeleri Azure bölmesinde Portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="1d924-120">In the [Azure portal](https://portal.azure.com), go to your Azure Database for MySQL server, and then click **Connection strings** to get your string list for your instance: ![The Connection strings pane in the Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="1d924-121">Dize bağlantı parametrelerini sürücü, sunucu ve diğer veritabanı gibi ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d924-121">The string provides details such as the driver, server, and other database connection parameters.</span></span> <span data-ttu-id="1d924-122">Bu örnekler, veritabanı adı, parola vb. gibi kendi parametrelerinizi kullanarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1d924-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="1d924-123">Ardından bu dize, kod ve uygulamalarınızı sunucuya bağlanmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d924-123">You can then use this string to connect to the server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d924-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d924-124">Next steps</span></span>
- <span data-ttu-id="1d924-125">Bağlantı kitaplıkları hakkında daha fazla bilgi için bkz: [kavramlar - bağlantı kitaplıkları](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="1d924-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
