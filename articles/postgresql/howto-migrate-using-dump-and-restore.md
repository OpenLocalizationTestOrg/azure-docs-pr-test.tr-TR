---
title: "aaaHow tooDump ve Azure veritabanı'nda PostgreSQL için geri yükleme | Microsoft Docs"
description: "Nasıl tooextract bir PostgreSQL veritabanı dökümü dosyasına ve geri yükleme için PostgreSQL pg_dump Azure veritabanında oluşturan bir arşiv dosyasına PostgreSQL veritabanından hello açıklar."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="bc80e-103">Döküm ve geri yükleme kullanarak PostgreSQL veritabanınızı geçirin</span><span class="sxs-lookup"><span data-stu-id="bc80e-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="bc80e-104">Kullanabileceğiniz [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract bir döküm dosyası PostgreSQL veritabanına ve [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) pg_dump tarafından oluşturulan bir arşiv dosyasına toorestore hello PostgreSQL veritabanından.</span><span class="sxs-lookup"><span data-stu-id="bc80e-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc80e-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bc80e-105">Prerequisites</span></span>
<span data-ttu-id="bc80e-106">toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="bc80e-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="bc80e-107">Bir [PostgreSQL sunucu için Azure veritabanı](quickstart-create-server-database-portal.md) güvenlik duvarı kuralları tooallow erişim ve altındaki veritabanı.</span><span class="sxs-lookup"><span data-stu-id="bc80e-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="bc80e-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) ve [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) yüklü komut satırı yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="bc80e-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="bc80e-109">Bu adımları toodump izleyin ve PostgreSQL veritabanınızı geri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="bc80e-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="bc80e-110">Yüklenen hello veri toobe içeren pg_dump kullanarak döküm dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc80e-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="bc80e-111">tooback var olan bir PostgreSQL yukarı şirket içi veritabanı veya bir VM'de, komutu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bc80e-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="bc80e-112">Örneğin, yerel bir sunucuya ve adlı bir veritabanı varsa **testdb** da</span><span class="sxs-lookup"><span data-stu-id="bc80e-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="bc80e-113">Merhaba veri pg_restore kullanarak PostrgeSQL için hello hedef Azure veritabanı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="bc80e-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="bc80e-114">Merhaba hedef veritabanı oluşturduktan sonra hello pg_restore komut ve hello -d--dbname parametre toorestore hello veri hello döküm dosyasından hello hedef veritabanına kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc80e-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="bc80e-115">Bu örnekte, hello döküm dosyadan hello verileri geri yüklemek **testdb.dump** hello veritabanına **mypgsqldb** hedef sunucu üzerindeki **mypgserver 20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="bc80e-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="bc80e-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc80e-116">Next steps</span></span>
- <span data-ttu-id="bc80e-117">dışarı ve içeri aktarma, kullanarak bir PostgreSQL veritabanı toomigrate bakın [verme kullanarak PostgreSQL veritabanınızı geçirin ve içeri aktarma](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="bc80e-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
