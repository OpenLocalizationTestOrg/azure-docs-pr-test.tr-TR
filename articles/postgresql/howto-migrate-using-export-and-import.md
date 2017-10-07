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
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Dışarı aktarma kullanarak PostgreSQL veritabanınızı geçirin ve içeri aktarma
Kullanabileceğiniz [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract bir komut dosyası PostgreSQL veritabanına ve [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) bu dosyadan hello hedef veritabanına tooimport hello veri.

## <a name="prerequisites"></a>Ön koşullar
toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:
- Bir [PostgreSQL sunucu için Azure veritabanı](quickstart-create-server-database-portal.md) güvenlik duvarı kuralları tooallow erişim ve altındaki veritabanı.
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) komut satırı yardımcı programının yüklü olması
- [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) komut satırı yardımcı programının yüklü olması

Bu adımları tooexport izleyin ve PostgreSQL veritabanınızı içeri aktarın.

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Yüklenen hello veri toobe içeren pg_dump kullanarak bir komut dosyası oluşturma
tooexport varolan PostgreSQL veritabanı şirket içi veya bir VM tooa sql komut dosyasında var olan ortamınıza komutunda aşağıdaki hello çalıştırın:
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Örneğin, yerel bir sunucuya ve adlı bir veritabanı varsa **testdb** da
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a>Azure veritabanı PostrgeSQL için hedefte hello Veri Al
Merhaba psql komut satırı ve hello -d--dbname parametresi tooimport hello verilerini Azure veritabanı oluşturulur ve hello sql dosyasından veri yükleme PostrgeSQL için kullanabilirsiniz.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
Bu örnek psql yardımcı programı ve adlı bir komut dosyası kullanır **testdb.sql** hello veritabanına önceki adım tooimport verilerden **mypgsqldb** hedef sunucu üzerindeki  **mypgserver 20170401.postgres.database.azure.com**.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>Sonraki adımlar
- Döküm ve geri yükleme kullanarak bir PostgreSQL veritabanı toomigrate bakın [döküm ve geri yükleme kullanarak PostgreSQL veritabanınızı geçirin](howto-migrate-using-dump-and-restore.md)
