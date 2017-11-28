---
title: "bir veritabanını kullanarak içeri ve dışarı aktarma Azure veritabanı'nda PostgreSQL için aaaMigrate | Microsoft Docs"
description: "Açıklar nasıl bir komut dosyasına bir PostgreSQL veritabanına ayıklayın ve bu dosyadaki hello hedef veritabanına hello veri içeri aktarın."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="3d1c7-103">Dışarı aktarma kullanarak PostgreSQL veritabanınızı geçirin ve içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="3d1c7-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="3d1c7-104">Kullanabileceğiniz [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract bir komut dosyası PostgreSQL veritabanına ve [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) bu dosyadan hello hedef veritabanına tooimport hello veri.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d1c7-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3d1c7-105">Prerequisites</span></span>
<span data-ttu-id="3d1c7-106">toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="3d1c7-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="3d1c7-107">Bir [PostgreSQL sunucu için Azure veritabanı](quickstart-create-server-database-portal.md) güvenlik duvarı kuralları tooallow erişim ve altındaki veritabanı.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="3d1c7-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="3d1c7-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="3d1c7-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) komut satırı yardımcı programının yüklü olması</span><span class="sxs-lookup"><span data-stu-id="3d1c7-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="3d1c7-110">Bu adımları tooexport izleyin ve PostgreSQL veritabanınızı içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="3d1c7-111">Yüklenen hello veri toobe içeren pg_dump kullanarak bir komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d1c7-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="3d1c7-112">tooexport varolan PostgreSQL veritabanı şirket içi veya bir VM tooa sql komut dosyasında var olan ortamınıza komutunda aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3d1c7-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="3d1c7-113">Örneğin, yerel bir sunucuya ve adlı bir veritabanı varsa **testdb** da</span><span class="sxs-lookup"><span data-stu-id="3d1c7-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="3d1c7-114">Azure veritabanı PostrgeSQL için hedefte hello Veri Al</span><span class="sxs-lookup"><span data-stu-id="3d1c7-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="3d1c7-115">Merhaba psql komut satırı ve hello -d--dbname parametresi tooimport hello verilerini Azure veritabanı oluşturulur ve hello sql dosyasından veri yükleme PostrgeSQL için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="3d1c7-116">Bu örnek psql yardımcı programı ve adlı bir komut dosyası kullanır **testdb.sql** hello veritabanına önceki adım tooimport verilerden **mypgsqldb** hedef sunucu üzerindeki  **mypgserver 20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="3d1c7-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d1c7-117">Next steps</span></span>
- <span data-ttu-id="3d1c7-118">Döküm ve geri yükleme kullanarak bir PostgreSQL veritabanı toomigrate bakın [döküm ve geri yükleme kullanarak PostgreSQL veritabanınızı geçirin](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="3d1c7-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
