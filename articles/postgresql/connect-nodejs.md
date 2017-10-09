---
title: "Node.js'den PostgreSQL için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç PostgreSQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz bir Node.js kodu örneği sağlar."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="756a2-103">Azure veritabanı PostgreSQL için: kullanım Node.js tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="756a2-103">Azure Database for PostgreSQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="756a2-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl PostgreSQL kullanmak için [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="756a2-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="756a2-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="756a2-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="756a2-106">Merhaba bu makaledeki adımları Node.js kullanarak geliştirme ile tanıdık ve yeni tooworking Azure veritabanı PostgreSQL için sahip olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="756a2-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="756a2-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="756a2-107">Prerequisites</span></span>
<span data-ttu-id="756a2-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="756a2-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="756a2-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="756a2-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="756a2-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="756a2-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="756a2-111">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="756a2-111">You also need to:</span></span>
- <span data-ttu-id="756a2-112">[Node.js](https://nodejs.org)’yi yükleme</span><span class="sxs-lookup"><span data-stu-id="756a2-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="756a2-113">pg istemcisini yükleme</span><span class="sxs-lookup"><span data-stu-id="756a2-113">Install pg client</span></span>
<span data-ttu-id="756a2-114">Yükleme [pg](https://www.npmjs.com/package/pg), Node.js için PostgreSQL istemci olduğu.</span><span class="sxs-lookup"><span data-stu-id="756a2-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="756a2-115">toodo bu nedenle, çalıştırın hello düğüm paketi Yöneticisi (npm) JavaScript için komut satırı tooinstall hello pg istemcinizden.</span><span class="sxs-lookup"><span data-stu-id="756a2-115">toodo so, run hello node package manager (npm) for JavaScript from your command line tooinstall hello pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="756a2-116">Yüklenen hello paketler listeleyerek Hello yüklemeyi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="756a2-116">Verify hello installation by listing hello packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="756a2-117">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="756a2-117">Get connection information</span></span>
<span data-ttu-id="756a2-118">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın.</span><span class="sxs-lookup"><span data-stu-id="756a2-118">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="756a2-119">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="756a2-119">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="756a2-120">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="756a2-120">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="756a2-121">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve yeni oluşturduğunuz hello sunucu arayın.</span><span class="sxs-lookup"><span data-stu-id="756a2-121">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created.</span></span>
3. <span data-ttu-id="756a2-122">Merhaba sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="756a2-122">Click hello server name.</span></span>
4. <span data-ttu-id="756a2-123">Select hello sunucunun **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="756a2-123">Select hello server's **Overview** page.</span></span> <span data-ttu-id="756a2-124">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="756a2-124">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="756a2-125">![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="756a2-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="756a2-126">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="756a2-126">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="756a2-127">Node.js içinde Hello JavaScript kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="756a2-127">Running hello JavaScript code in Node.js</span></span>
<span data-ttu-id="756a2-128">Yazarak kabuğundan ya da windows komut isteminden hello bash Node.js başlatabilir `node`, ardından hello örnek JavaScript kodunu copy etkileşimli olarak çalıştırmak ve hello istemi yapıştırma.</span><span class="sxs-lookup"><span data-stu-id="756a2-128">You may launch Node.js from hello bash shell or windows command prompt by typing `node`, then run hello example JavaScript code interactively by copy and pasting it onto hello prompt.</span></span> <span data-ttu-id="756a2-129">Alternatif olarak, hello JavaScript kodu bir metin dosyası ve başlatma kaydettiğiniz `node filename.js` hello dosya adında bir parametre toorun olarak bunu.</span><span class="sxs-lookup"><span data-stu-id="756a2-129">Alternatively, you may save hello JavaScript code into a text file and launch `node filename.js` with hello file name as a parameter toorun it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="756a2-130">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="756a2-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="756a2-131">Kullanım hello aşağıdakileri tooconnect kod ve verileri hello kullanarak yük **CREATE TABLE** ve **INSERT INTO** SQL deyimlerini.</span><span class="sxs-lookup"><span data-stu-id="756a2-131">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="756a2-132">Merhaba [pg. İstemci](https://github.com/brianc/node-postgres/wiki/Client) hello PostgreSQL sunucusuyla kullanılan toointerface nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="756a2-132">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="756a2-133">Merhaba [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="756a2-133">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="756a2-134">Merhaba [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) PostgreSQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="756a2-134">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="756a2-135">Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="756a2-135">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a><span data-ttu-id="756a2-136">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="756a2-136">Read data</span></span>
<span data-ttu-id="756a2-137">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="756a2-137">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="756a2-138">Merhaba [pg. İstemci](https://github.com/brianc/node-postgres/wiki/Client) hello PostgreSQL sunucusuyla kullanılan toointerface nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="756a2-138">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="756a2-139">Merhaba [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="756a2-139">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="756a2-140">Merhaba [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) PostgreSQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="756a2-140">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="756a2-141">Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="756a2-141">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a><span data-ttu-id="756a2-142">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="756a2-142">Update data</span></span>
<span data-ttu-id="756a2-143">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="756a2-143">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="756a2-144">Merhaba [pg. İstemci](https://github.com/brianc/node-postgres/wiki/Client) hello PostgreSQL sunucusuyla kullanılan toointerface nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="756a2-144">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="756a2-145">Merhaba [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="756a2-145">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="756a2-146">Merhaba [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) PostgreSQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="756a2-146">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="756a2-147">Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="756a2-147">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a><span data-ttu-id="756a2-148">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="756a2-148">Delete data</span></span>
<span data-ttu-id="756a2-149">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="756a2-149">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="756a2-150">Merhaba [pg. İstemci](https://github.com/brianc/node-postgres/wiki/Client) hello PostgreSQL sunucusuyla kullanılan toointerface nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="756a2-150">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="756a2-151">Merhaba [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="756a2-151">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="756a2-152">Merhaba [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) PostgreSQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="756a2-152">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="756a2-153">Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="756a2-153">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a><span data-ttu-id="756a2-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="756a2-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="756a2-155">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="756a2-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
