---
title: "Node.js'den MySQL için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç MySQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz birkaç Node.js kod örnekleri sağlar."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="96169-103">Azure veritabanı için MySQL: kullanım Node.js tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="96169-103">Azure Database for MySQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="96169-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl MySQL kullanmak için [Node.js](https://nodejs.org/) Windows, Ubuntu Linux ve Mac platformları gelen.</span><span class="sxs-lookup"><span data-stu-id="96169-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="96169-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="96169-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="96169-106">Merhaba bu makaledeki adımları Node.js kullanarak geliştirme ile tanıdık olduğunuz ve Azure veritabanı için MySQL ile yeni tooworking olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="96169-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96169-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="96169-107">Prerequisites</span></span>
<span data-ttu-id="96169-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="96169-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="96169-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="96169-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="96169-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="96169-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="96169-111">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="96169-111">You also need to:</span></span>
- <span data-ttu-id="96169-112">Merhaba yüklemek [Node.js](https://nodejs.org) çalışma zamanı.</span><span class="sxs-lookup"><span data-stu-id="96169-112">Install hello [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="96169-113">Yükleme [mysql2](https://www.npmjs.com/package/mysql2) tooconnect tooMySQL hello Node.js uygulaması gelen paket.</span><span class="sxs-lookup"><span data-stu-id="96169-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package tooconnect tooMySQL from hello Node.js application.</span></span> 

## <a name="install-nodejs-and-hello-mysql-connector"></a><span data-ttu-id="96169-114">Node.js yükleyin ve MySQL bağlayıcı hello</span><span class="sxs-lookup"><span data-stu-id="96169-114">Install Node.js and hello MySQL connector</span></span>
<span data-ttu-id="96169-115">Platformunuz bağlı olarak hello uygun yönergeleri tooinstall Node.js izleyin.</span><span class="sxs-lookup"><span data-stu-id="96169-115">Depending on your platform, follow hello appropriate instructions tooinstall Node.js.</span></span> <span data-ttu-id="96169-116">Npm tooinstall hello mysql2 paketi ve bağımlılıklarını projeye klasörünüze kullanın.</span><span class="sxs-lookup"><span data-stu-id="96169-116">Use npm tooinstall hello mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="96169-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="96169-117">**Windows**</span></span>
1. <span data-ttu-id="96169-118">Merhaba ziyaret [Node.js indirmeler sayfası](https://nodejs.org/en/download/) ve istediğiniz Windows Installer seçiminizi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="96169-118">Visit hello [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="96169-119">`nodejsmysql` gibi yerel bir proje klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96169-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="96169-120">Merhaba komut istemi ve cd hello proje klasörüne gibi başlatın`cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="96169-120">Launch hello command prompt and cd into hello project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="96169-121">Merhaba NPM aracı tooinstall hello mysql2 kitaplığı hello proje klasörüne çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96169-121">Run hello NPM tool tooinstall hello mysql2 library into hello project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="96169-122">Merhaba denetleyerek Hello yüklemesini doğrulama `npm list` çıkış metnini `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="96169-122">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="96169-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="96169-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="96169-124">Çalışma hello aşağıdaki komutları tooinstall **Node.js** ve **npm** Node.js için hello Paket Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="96169-124">Run hello following commands tooinstall **Node.js** and **npm** hello package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="96169-125">Aşağıdaki komutları toomake hello proje klasöründe Çalıştır `mysqlnodejs` hello mysql2 paketini ve bu klasöre yükleyin.</span><span class="sxs-lookup"><span data-stu-id="96169-125">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="96169-126">Npm liste çıkış metnini denetleyerek Hello yüklemesini doğrulama `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="96169-126">Verify hello installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="96169-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="96169-127">**Mac OS**</span></span>
1. <span data-ttu-id="96169-128">Aşağıdaki komutları tooinstall hello girin **brew**, Mac OS X için kullanımı kolay Paket Yöneticisi ve **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="96169-128">Enter hello following commands tooinstall **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="96169-129">Aşağıdaki komutları toomake hello proje klasöründe Çalıştır `mysqlnodejs` hello mysql2 paketini ve bu klasöre yükleyin.</span><span class="sxs-lookup"><span data-stu-id="96169-129">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="96169-130">Merhaba denetleyerek Hello yüklemesini doğrulama `npm list` çıkış metnini `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="96169-130">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="96169-131">Yeni düzeltme ekleri yayımlanan hello sürüm numarası değişebilir.</span><span class="sxs-lookup"><span data-stu-id="96169-131">hello version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="96169-132">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="96169-132">Get connection information</span></span>
<span data-ttu-id="96169-133">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın.</span><span class="sxs-lookup"><span data-stu-id="96169-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="96169-134">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="96169-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="96169-135">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="96169-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="96169-136">Merhaba sol bölmede **tüm kaynakları**ve ardından oluşturduğunuz hello sunucusu için arama (örneğin, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="96169-136">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="96169-137">Merhaba sunucu adına tıklatarak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="96169-137">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="96169-138">Select hello sunucunun **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="96169-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="96169-139">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="96169-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="96169-140">![MySQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="96169-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="96169-141">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="96169-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="96169-142">Node.js içinde Hello JavaScript kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="96169-142">Running hello JavaScript code in Node.js</span></span>
1. <span data-ttu-id="96169-143">Hello JavaScript kodunu metin dosyasına yapıştırın ve C:\nodejsmysql\createtable.js veya /home/username/nodejsmysql/createtable.js gibi dosya uzantısı .js ile bir proje klasöre kaydedin</span><span class="sxs-lookup"><span data-stu-id="96169-143">Paste hello JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="96169-144">Merhaba komut istemi başlatın veya kabuk bash.</span><span class="sxs-lookup"><span data-stu-id="96169-144">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="96169-145">Dizini, proje klasörünüzle değiştirin (`cd nodejsmysql`).</span><span class="sxs-lookup"><span data-stu-id="96169-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="96169-146">toorun Merhaba uygulaması, ardından hello dosya adı, gibi hello düğüm komutu yazın `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="96169-146">toorun hello application, type hello node command followed by hello file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="96169-147">Merhaba düğümü uygulaması, ortam değişkeni yolunuzda değilse, Windows, toouse hello tam yolu toolaunch hello düğüm uygulama gibi gerekebilir`"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="96169-147">On Windows, if hello node application is not in your environment variable path, you may need toouse hello full path toolaunch hello node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="96169-148">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="96169-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="96169-149">Kullanım hello aşağıdakileri tooconnect kod ve verileri hello kullanarak yük **CREATE TABLE** ve **INSERT INTO** SQL deyimlerini.</span><span class="sxs-lookup"><span data-stu-id="96169-149">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="96169-150">Merhaba [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) hello MySQL server ile kullanılan toointerface bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="96169-151">Merhaba [connect()](https://github.com/mysqljs/mysql#establishing-connections) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="96169-151">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="96169-152">Merhaba [query()](https://github.com/mysqljs/mysql#performing-queries) MySQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="96169-152">hello [query()](https://github.com/mysqljs/mysql#performing-queries) function is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="96169-153">Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.</span><span class="sxs-lookup"><span data-stu-id="96169-153">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a><span data-ttu-id="96169-154">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="96169-154">Read data</span></span>
<span data-ttu-id="96169-155">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="96169-155">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="96169-156">Merhaba [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) hello MySQL server ile kullanılan toointerface bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="96169-157">Merhaba [connect()](https://github.com/mysqljs/mysql#establishing-connections) kullanılan tooestablish hello bağlantı toohello sunucusu bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-157">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="96169-158">Merhaba [query()](https://github.com/mysqljs/mysql#performing-queries) MySQL veritabanında kullanılan tooexecute hello SQL sorgu bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-158">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> <span data-ttu-id="96169-159">kullanılan toohold hello hello sorgunun sonuçlarını Hello sonuçları dizisidir.</span><span class="sxs-lookup"><span data-stu-id="96169-159">hello results array is used toohold hello results of hello query.</span></span>

<span data-ttu-id="96169-160">Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.</span><span class="sxs-lookup"><span data-stu-id="96169-160">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a><span data-ttu-id="96169-161">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="96169-161">Update data</span></span>
<span data-ttu-id="96169-162">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="96169-162">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="96169-163">Merhaba [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) hello MySQL server ile kullanılan toointerface bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="96169-164">Merhaba [connect()](https://github.com/mysqljs/mysql#establishing-connections) kullanılan tooestablish hello bağlantı toohello sunucusu bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-164">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="96169-165">Merhaba [query()](https://github.com/mysqljs/mysql#performing-queries) MySQL veritabanında kullanılan tooexecute hello SQL sorgu bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-165">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="96169-166">Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.</span><span class="sxs-lookup"><span data-stu-id="96169-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a><span data-ttu-id="96169-167">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="96169-167">Delete data</span></span>
<span data-ttu-id="96169-168">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="96169-168">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="96169-169">Merhaba [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) hello MySQL server ile kullanılan toointerface bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="96169-170">Merhaba [connect()](https://github.com/mysqljs/mysql#establishing-connections) kullanılan tooestablish hello bağlantı toohello sunucusu bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-170">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="96169-171">Merhaba [query()](https://github.com/mysqljs/mysql#performing-queries) MySQL veritabanında kullanılan tooexecute hello SQL sorgu bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="96169-171">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="96169-172">Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.</span><span class="sxs-lookup"><span data-stu-id="96169-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a><span data-ttu-id="96169-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96169-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="96169-174">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="96169-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
