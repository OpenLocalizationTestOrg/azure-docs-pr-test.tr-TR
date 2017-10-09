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
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a>Azure veritabanı PostgreSQL için: kullanım Node.js tooconnect ve sorgu verileri
Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl PostgreSQL kullanmak için [Node.js](https://nodejs.org/). Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir. Merhaba bu makaledeki adımları Node.js kullanarak geliştirme ile tanıdık ve yeni tooworking Azure veritabanı PostgreSQL için sahip olduğunuz varsayılır.

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:
- [DB Oluşturma - Portal](quickstart-create-server-database-portal.md)
- [DB oluşturma - CLI](quickstart-create-server-database-azure-cli.md)

Şunları da yapmanız gerekir:
- [Node.js](https://nodejs.org)’yi yükleme

## <a name="install-pg-client"></a>pg istemcisini yükleme
Yükleme [pg](https://www.npmjs.com/package/pg), Node.js için PostgreSQL istemci olduğu.

toodo bu nedenle, çalıştırın hello düğüm paketi Yöneticisi (npm) JavaScript için komut satırı tooinstall hello pg istemcinizden.
```bash
npm install pg
```

Yüklenen hello paketler listeleyerek Hello yüklemeyi doğrulayın.
```bash
npm list
```

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın. Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve yeni oluşturduğunuz hello sunucu arayın.
3. Merhaba sunucu adına tıklayın.
4. Select hello sunucunun **genel bakış** sayfası. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.
 ![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-nodejs/1-connection-string.png)
5. Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.

## <a name="running-hello-javascript-code-in-nodejs"></a>Node.js içinde Hello JavaScript kodu çalıştırma
Yazarak kabuğundan ya da windows komut isteminden hello bash Node.js başlatabilir `node`, ardından hello örnek JavaScript kodunu copy etkileşimli olarak çalıştırmak ve hello istemi yapıştırma. Alternatif olarak, hello JavaScript kodu bir metin dosyası ve başlatma kaydettiğiniz `node filename.js` hello dosya adında bir parametre toorun olarak bunu.

## <a name="connect-create-table-and-insert-data"></a>Bağlanma, tablo oluşturma ve veri ekleme
Kullanım hello aşağıdakileri tooconnect kod ve verileri hello kullanarak yük **CREATE TABLE** ve **INSERT INTO** SQL deyimlerini.
Merhaba [pg. İstemci](https://github.com/brianc/node-postgres/wiki/Client) hello PostgreSQL sunucusuyla kullanılan toointerface nesnesidir. Merhaba [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir. Merhaba [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) PostgreSQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir. 

Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.

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

## <a name="read-data"></a>Verileri okuma
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi. Merhaba [pg. İstemci](https://github.com/brianc/node-postgres/wiki/Client) hello PostgreSQL sunucusuyla kullanılan toointerface nesnesidir. Merhaba [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir. Merhaba [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) PostgreSQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir. 

Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin. 

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

## <a name="update-data"></a>Verileri güncelleştirme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **güncelleştirme** SQL deyimi. Merhaba [pg. İstemci](https://github.com/brianc/node-postgres/wiki/Client) hello PostgreSQL sunucusuyla kullanılan toointerface nesnesidir. Merhaba [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir. Merhaba [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) PostgreSQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir. 

Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin. 

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

## <a name="delete-data"></a>Verileri silme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi. Merhaba [pg. İstemci](https://github.com/brianc/node-postgres/wiki/Client) hello PostgreSQL sunucusuyla kullanılan toointerface nesnesidir. Merhaba [pg. Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir. Merhaba [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) PostgreSQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir. 

Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin. 

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

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme](./howto-migrate-using-export-and-import.md)
