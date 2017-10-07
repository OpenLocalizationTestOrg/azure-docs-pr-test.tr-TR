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
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>Döküm ve geri yükleme kullanarak PostgreSQL veritabanınızı geçirin
Kullanabileceğiniz [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract bir döküm dosyası PostgreSQL veritabanına ve [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) pg_dump tarafından oluşturulan bir arşiv dosyasına toorestore hello PostgreSQL veritabanından.

## <a name="prerequisites"></a>Ön koşullar
toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:
- Bir [PostgreSQL sunucu için Azure veritabanı](quickstart-create-server-database-portal.md) güvenlik duvarı kuralları tooallow erişim ve altındaki veritabanı.
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) ve [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) yüklü komut satırı yardımcı programları

Bu adımları toodump izleyin ve PostgreSQL veritabanınızı geri yükleyin:

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Yüklenen hello veri toobe içeren pg_dump kullanarak döküm dosyası oluşturma
tooback var olan bir PostgreSQL yukarı şirket içi veritabanı veya bir VM'de, komutu aşağıdaki hello çalıştırın:
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
Örneğin, yerel bir sunucuya ve adlı bir veritabanı varsa **testdb** da
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a>Merhaba veri pg_restore kullanarak PostrgeSQL için hello hedef Azure veritabanı geri yükleme
Merhaba hedef veritabanı oluşturduktan sonra hello pg_restore komut ve hello -d--dbname parametre toorestore hello veri hello döküm dosyasından hello hedef veritabanına kullanabilirsiniz.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
Bu örnekte, hello döküm dosyadan hello verileri geri yüklemek **testdb.dump** hello veritabanına **mypgsqldb** hedef sunucu üzerindeki **mypgserver 20170401.postgres.database.azure.com**.
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>Sonraki adımlar
- dışarı ve içeri aktarma, kullanarak bir PostgreSQL veritabanı toomigrate bakın [verme kullanarak PostgreSQL veritabanınızı geçirin ve içeri aktarma](howto-migrate-using-export-and-import.md)
