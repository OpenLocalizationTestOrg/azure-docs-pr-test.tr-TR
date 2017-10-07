---
title: "Azure veritabanı PostgreSQL için aaaUsing PostgreSQL uzantıları | Microsoft Docs"
description: "Merhaba özelliği tooextend hello uzantıları için PostgreSQL Azure veritabanı'nda kullanarak veritabanını işlevselliğini açıklar."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>Azure veritabanı PostgreSQL için PostgreSQL uzantıları
PostgreSQL hello özelliği tooextend hello uzantıları kullanarak veritabanını işlevselliğini sağlar. Uzantıları tek bir paket birlikte gruplanır, birden çok, ilgili SQL nesneleri toobe izin verir ve yüklenen veya tek bir komutla, veritabanından kaldırıldı. Bir kez hello veritabanına yüklenen uzantıları yalnızca içinde yerleşik özellikler gibi işlev görebilir. PostgreSQL uzantıları hakkında daha fazla bilgi için bkz: [uzantı paketleme ilgili nesnelerini](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).

## <a name="how-toouse-postgresql-extensions"></a>Nasıl toouse PostgreSQL uzantıları?
PostgreSQL uzantıları kullanabilmek için önce veritabanınız için yüklü toobe gerekir. çalıştırma tooinstall belirli bir uzantıyı [UZANTI Oluştur](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) psql aracı tooload komuttan hello paketlenmiş nesneleri veritabanınıza.

Azure veritabanı PostgreSQL için burada listelenen gibi bir alt anahtar uzantıları kümesini destekler. Merhaba listelenen olanlar diğer uzantılar desteklenmez. Kendi uzantısı PostgreSQL hizmeti için Azure veritabanı oluşturulamıyor.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>Azure veritabanı tarafından PostgreSQL için desteklenen uzantıları
Merhaba aşağıdaki Azure veritabanı tarafından PostgreSQL için şu anda desteklenen listesi hello standart PostgreSQL uzantıları tablolarını. Bu bilgiler pg sorgulayarak da elde edebilirsiniz\_kullanılabilir\_uzantıları. 

### <a name="data-types-extensions"></a>Veri türleri uzantıları

> [!div class="mx-tableFixed"]
| **Uzantısı** | **Açıklama** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | Bir küçük harf karakter dize türü sağlar |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | Anahtar/değer çiftleri kümesi depolamak için veri türü sağlar |

### <a name="functions-extensions"></a>İşlevler uzantıları

> [!div class="mx-tableFixed"]
| **Uzantısı** | **Açıklama** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | Çeşitli işlevler toodetermine benzerlikler ve dizeler arasındaki uzaklığı sağlar. |
| [int](https://www.postgresql.org/docs/9.6/static/intarray.html) | İşlevler ve işleçler null serbest diziler tamsayıların yönlendirmek için sağlar. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | Şifreleme işlevleri sağlar |
| [PG\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | Bölümlenmiş tablolar zaman veya Kimliğe göre yönetir |
| [PG\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | Merhaba benzerlik trigram eşleşmesini temel alan alfasayısal metnin belirlemek için İşlevler ve işleçler sağlar |
| [UUID ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | Evrensel benzersiz tanımlayıcıları (UUID) oluştur |

### <a name="full-text-search-extensions"></a>Tam metin arama uzantıları

> [!div class="mx-tableFixed"]
| **Uzantısı** | **Açıklama** |
|---|---|
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | Lexemes vurgular (vurgu işaretlerini) kaldırır metin arama sözlük. |

### <a name="index-types-extensions"></a>Dizin türleri uzantıları

> [!div class="mx-tableFixed"]
| **Uzantısı** | **Açıklama** |
|---|---|
| [BTree\_GIN](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | Gibi belirli veri türleri için davranış B-Ağacı uygulayan örnek GIN işleci sınıflar sağlar. |
| [BTree\_gist](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | B-Ağacı uygulayan GiST dizin işleci sınıflar sağlar. |

### <a name="language-extensions"></a>Dil uzantıları

> [!div class="mx-tableFixed"]
| **Uzantısı** | **Açıklama** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | PL/pgSQL yüklenebilir yordam dili |

### <a name="miscellaneous-extensions"></a>Çeşitli uzantıları

> [!div class="mx-tableFixed"]
| **Uzantısı** | **Açıklama** |
|---|---|
| [PG\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | Gerçek zamanlı paylaşılan hello arabellek önbelleğindeki neler olduğunu incelemek için bir yol sağlar. |
| [PG\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Bir şekilde tooload ilişkisi veri hello arabellek önbelleğine sağlar. |
| [PG\_stat\_deyimleri](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | Bir sunucu tarafından yürütülen tüm SQL deyimlerini Yürütme istatistiklerini izlemek için bir yol sağlar. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | Dış PostgreSQL sunucuları depolanan tooaccess verileri yabancı veri sarmalayıcı kullanılan |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **Uzantısı** | **Açıklama** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topoloji, postgis\_tiger\_geocoder, postgis\_sfcgal | Uzamsal ve coğrafi nesneleri PostgreSQL için. |
| Adres\_standardizer, adresi\_standardizer\_veri\_bize | Kullanılan tooparse bağlı öğelerine bir adres. Toosupport coğrafi kodlama adresi normalleştirme adım kullanılır. |
| [pgrouting](http://pgrouting.org/) | Merhaba PostGIS genişletir / PostgreSQL Jeo-uzamsal veritabanı tooprovide Jeo-uzamsal yönlendirme işlevi. |

## <a name="next-steps"></a>Sonraki adımlar
Uzantı toouse istediğiniz görmüyorum? Lütfen bize bildirin. Var olan istekleri için oy verin veya yeni geri bildirim ve içinde dileklerimle oluşturmak bizim [müşteri geri bildirim Forumunda](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).
