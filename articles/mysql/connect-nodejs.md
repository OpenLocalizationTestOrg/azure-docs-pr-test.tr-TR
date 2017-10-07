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
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a>Azure veritabanı için MySQL: kullanım Node.js tooconnect ve sorgu verileri
Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl MySQL kullanmak için [Node.js](https://nodejs.org/) Windows, Ubuntu Linux ve Mac platformları gelen. Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir. Merhaba bu makaledeki adımları Node.js kullanarak geliştirme ile tanıdık olduğunuz ve Azure veritabanı için MySQL ile yeni tooworking olduğunu varsayalım.

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-cli.md)

Şunları da yapmanız gerekir:
- Merhaba yüklemek [Node.js](https://nodejs.org) çalışma zamanı.
- Yükleme [mysql2](https://www.npmjs.com/package/mysql2) tooconnect tooMySQL hello Node.js uygulaması gelen paket. 

## <a name="install-nodejs-and-hello-mysql-connector"></a>Node.js yükleyin ve MySQL bağlayıcı hello
Platformunuz bağlı olarak hello uygun yönergeleri tooinstall Node.js izleyin. Npm tooinstall hello mysql2 paketi ve bağımlılıklarını projeye klasörünüze kullanın.

### <a name="windows"></a>**Windows**
1. Merhaba ziyaret [Node.js indirmeler sayfası](https://nodejs.org/en/download/) ve istediğiniz Windows Installer seçiminizi belirleyin.
2. `nodejsmysql` gibi yerel bir proje klasörü oluşturun. 
3. Merhaba komut istemi ve cd hello proje klasörüne gibi başlatın`cd c:\nodejsmysql\`
4. Merhaba NPM aracı tooinstall hello mysql2 kitaplığı hello proje klasörüne çalıştırın.

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. Merhaba denetleyerek Hello yüklemesini doğrulama `npm list` çıkış metnini `mysql2@1.3.5`.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
1. Çalışma hello aşağıdaki komutları tooinstall **Node.js** ve **npm** Node.js için hello Paket Yöneticisi.

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. Aşağıdaki komutları toomake hello proje klasöründe Çalıştır `mysqlnodejs` hello mysql2 paketini ve bu klasöre yükleyin.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. Npm liste çıkış metnini denetleyerek Hello yüklemesini doğrulama `mysql2@1.3.5`.

### <a name="mac-os"></a>**Mac OS**
1. Aşağıdaki komutları tooinstall hello girin **brew**, Mac OS X için kullanımı kolay Paket Yöneticisi ve **Node.js**.

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. Aşağıdaki komutları toomake hello proje klasöründe Çalıştır `mysqlnodejs` hello mysql2 paketini ve bu klasöre yükleyin.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. Merhaba denetleyerek Hello yüklemesini doğrulama `npm list` çıkış metnini `mysql2@1.3.6`. Yeni düzeltme ekleri yayımlanan hello sürüm numarası değişebilir.

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın. Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba sol bölmede **tüm kaynakları**ve ardından oluşturduğunuz hello sunucusu için arama (örneğin, **myserver4demo**).
3. Merhaba sunucu adına tıklatarak **myserver4demo**.
4. Select hello sunucunun **özellikleri** sayfası. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.
 ![MySQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/connect-nodejs/1_server-properties-name-login.png)
5. Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.

## <a name="running-hello-javascript-code-in-nodejs"></a>Node.js içinde Hello JavaScript kodu çalıştırma
1. Hello JavaScript kodunu metin dosyasına yapıştırın ve C:\nodejsmysql\createtable.js veya /home/username/nodejsmysql/createtable.js gibi dosya uzantısı .js ile bir proje klasöre kaydedin
2. Merhaba komut istemi başlatın veya kabuk bash. Dizini, proje klasörünüzle değiştirin (`cd nodejsmysql`).
3. toorun Merhaba uygulaması, ardından hello dosya adı, gibi hello düğüm komutu yazın `node createtable.js`.
4. Merhaba düğümü uygulaması, ortam değişkeni yolunuzda değilse, Windows, toouse hello tam yolu toolaunch hello düğüm uygulama gibi gerekebilir`"C:\Program Files\nodejs\node.exe" createtable.js`

## <a name="connect-create-table-and-insert-data"></a>Bağlanma, tablo oluşturma ve veri ekleme
Kullanım hello aşağıdakileri tooconnect kod ve verileri hello kullanarak yük **CREATE TABLE** ve **INSERT INTO** SQL deyimlerini.

Merhaba [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) hello MySQL server ile kullanılan toointerface bir yöntemdir. Merhaba [connect()](https://github.com/mysqljs/mysql#establishing-connections) kullanılan tooestablish hello bağlantı toohello sunucusu işlevdir. Merhaba [query()](https://github.com/mysqljs/mysql#performing-queries) MySQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir. 

Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.

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

## <a name="read-data"></a>Verileri okuma
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi. 

Merhaba [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) hello MySQL server ile kullanılan toointerface bir yöntemdir. Merhaba [connect()](https://github.com/mysqljs/mysql#establishing-connections) kullanılan tooestablish hello bağlantı toohello sunucusu bir yöntemdir. Merhaba [query()](https://github.com/mysqljs/mysql#performing-queries) MySQL veritabanında kullanılan tooexecute hello SQL sorgu bir yöntemdir. kullanılan toohold hello hello sorgunun sonuçlarını Hello sonuçları dizisidir.

Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.

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

## <a name="update-data"></a>Verileri güncelleştirme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **güncelleştirme** SQL deyimi. 

Merhaba [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) hello MySQL server ile kullanılan toointerface bir yöntemdir. Merhaba [connect()](https://github.com/mysqljs/mysql#establishing-connections) kullanılan tooestablish hello bağlantı toohello sunucusu bir yöntemdir. Merhaba [query()](https://github.com/mysqljs/mysql#performing-queries) MySQL veritabanında kullanılan tooexecute hello SQL sorgu bir yöntemdir. 

Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.

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

## <a name="delete-data"></a>Verileri silme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi. 

Merhaba [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) hello MySQL server ile kullanılan toointerface bir yöntemdir. Merhaba [connect()](https://github.com/mysqljs/mysql#establishing-connections) kullanılan tooestablish hello bağlantı toohello sunucusu bir yöntemdir. Merhaba [query()](https://github.com/mysqljs/mysql#performing-queries) MySQL veritabanında kullanılan tooexecute hello SQL sorgu bir yöntemdir. 

Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.

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

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme](./concepts-migrate-import-export.md)
