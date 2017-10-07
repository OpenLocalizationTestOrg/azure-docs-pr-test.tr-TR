---
title: "Azure veritabanı PostgreSQL için için bağlantı kitaplıkları | Microsoft Docs"
description: "Bu makalede, çeşitli kitaplıkları ve geliştiriciler için PostgreSQL uygulamaları tooconnect ve sorgu Azure veritabanı kodlama yaparken kullanabileceğiniz sürücüleri açıklanmaktadır."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/15/2017
ms.openlocfilehash: 1f7234499d8abe37f8de9008e3158765b1fb0bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connection-libraries-for-azure-database-for-postgresql"></a>Azure veritabanı PostgreSQL için için bağlantı kitaplıkları
Bu konu, kitaplıklar ve uygulamaları tooconnect ve sorgu Azure veritabanı için PostgreSQL programlama için geliştiriciler tarafından kullanılmaya sürücüleri listeler.

## <a name="client-interfaces"></a>İstemci arabirimleri
Çoğu dil istemci kitaplıkları tooconnect tooPostgreSQL sunucu dış projeler ve bağımsız olarak dağıtılır. Bunlar, Windows, Linux ve Mac platformlarında desteklenir. Bazı hello popüler istemci sürücüleri listelenmiştir:

| **Dil** | **İstemci arabirimi** | **Ek bilgi** | **İndir** |
|--------------|----------------------------------------------------------------|-------------------------------------|--------------------------------------------------------------------|
| Python | [psycopg](http://initd.org/psycopg/) | DB API 2.0 uyumlu | [İndir](http://initd.org/psycopg/download/) |
| PHP | [PHP pgsql](https://php.net/manual/en/book.pgsql.php) | Veritabanı uzantısı | [Yükleme](https://secure.php.net/manual/en/pgsql.installation.php) |
| Node.js | [PG npm paket](https://www.npmjs.com/package/pg) | Saf JavaScript engelleyici olmayan istemci | [Yükleme](https://www.npmjs.com/package/pg) |
| Java | [JDBC](http://jdbc.postgresql.org/) | Tür 4 JDBC sürücüsü | [İndir](https://jdbc.postgresql.org/download.html)  |
| Ruby | [PG gem](https://deveiate.org/code/pg/) | Söyleniş arabirimi | [İndir](https://rubygems.org/downloads/pg-0.20.0.gem) |
| Başlayın | [Paket pq](https://godoc.org/github.com/lib/pq) | Saf Git postgres sürücüsü | [Yükleme](https://github.com/lib/pq/blob/master/README.md) |
| C\#/ .NET | [Npgsql](http://www.npgsql.org/) | ADO.NET veri sağlayıcı | [İndir](https://www.microsoft.com/net/) |
| ODBC | [psqlODBC](https://odbc.postgresql.org/) | ODBC Sürücüsü | [İndir](http://www.postgresql.org/ftp/odbc/versions/) |
| C | [libpq](https://www.postgresql.org/docs/9.6/static/libpq.html) | Birincil C dil arabirimi | Dahil |
| C++ | [libpqxx](http://pqxx.org/) | Yeni stil C++ arabirimi | [İndir](http://pqxx.org/download/software/) |

## <a name="next-steps"></a>Sonraki adımlar
Bu quickstarts nasıl okuma tooconnect sorgu Azure veritabanı ve dilinizi tercih kullanarak PostgreSQL için:

[Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [.NET (C#)](./connect-csharp.md)
