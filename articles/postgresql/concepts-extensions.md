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
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a><span data-ttu-id="b549a-103">Azure veritabanı PostgreSQL için PostgreSQL uzantıları</span><span class="sxs-lookup"><span data-stu-id="b549a-103">PostgreSQL Extensions in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="b549a-104">PostgreSQL hello özelliği tooextend hello uzantıları kullanarak veritabanını işlevselliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b549a-104">PostgreSQL provides hello ability tooextend hello functionality of your database using extensions.</span></span> <span data-ttu-id="b549a-105">Uzantıları tek bir paket birlikte gruplanır, birden çok, ilgili SQL nesneleri toobe izin verir ve yüklenen veya tek bir komutla, veritabanından kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="b549a-105">Extensions allow for multiple related SQL objects toobe bundled together in a single package and can be loaded or removed from your database with a single command.</span></span> <span data-ttu-id="b549a-106">Bir kez hello veritabanına yüklenen uzantıları yalnızca içinde yerleşik özellikler gibi işlev görebilir.</span><span class="sxs-lookup"><span data-stu-id="b549a-106">Extensions once loaded into hello database can function just like features that are built in.</span></span> <span data-ttu-id="b549a-107">PostgreSQL uzantıları hakkında daha fazla bilgi için bkz: [uzantı paketleme ilgili nesnelerini](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).</span><span class="sxs-lookup"><span data-stu-id="b549a-107">For more information on PostgreSQL extensions, see [Packaging Related Objects into an Extension](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).</span></span>

## <a name="how-toouse-postgresql-extensions"></a><span data-ttu-id="b549a-108">Nasıl toouse PostgreSQL uzantıları?</span><span class="sxs-lookup"><span data-stu-id="b549a-108">How toouse PostgreSQL extensions?</span></span>
<span data-ttu-id="b549a-109">PostgreSQL uzantıları kullanabilmek için önce veritabanınız için yüklü toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b549a-109">PostgreSQL extensions need toobe installed for your database before you can use them.</span></span> <span data-ttu-id="b549a-110">çalıştırma tooinstall belirli bir uzantıyı [UZANTI Oluştur](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) psql aracı tooload komuttan hello paketlenmiş nesneleri veritabanınıza.</span><span class="sxs-lookup"><span data-stu-id="b549a-110">tooinstall a particular extension, run the [CREATE EXTENSION](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) command from psql tool tooload hello packaged objects into your database.</span></span>

<span data-ttu-id="b549a-111">Azure veritabanı PostgreSQL için burada listelenen gibi bir alt anahtar uzantıları kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="b549a-111">Azure Database for PostgreSQL supports a subset of key extensions as listed here.</span></span> <span data-ttu-id="b549a-112">Merhaba listelenen olanlar diğer uzantılar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="b549a-112">Beyond hello ones listed, other extensions are not supported.</span></span> <span data-ttu-id="b549a-113">Kendi uzantısı PostgreSQL hizmeti için Azure veritabanı oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="b549a-113">You cannot create your own extension with Azure Database for PostgreSQL service.</span></span>

## <a name="extensions-supported-by-azure-database-for-postgresql"></a><span data-ttu-id="b549a-114">Azure veritabanı tarafından PostgreSQL için desteklenen uzantıları</span><span class="sxs-lookup"><span data-stu-id="b549a-114">Extensions supported by Azure Database for PostgreSQL</span></span>
<span data-ttu-id="b549a-115">Merhaba aşağıdaki Azure veritabanı tarafından PostgreSQL için şu anda desteklenen listesi hello standart PostgreSQL uzantıları tablolarını.</span><span class="sxs-lookup"><span data-stu-id="b549a-115">hello following tables list hello standard PostgreSQL extensions that are currently supported by Azure Database for PostgreSQL.</span></span> <span data-ttu-id="b549a-116">Bu bilgiler pg sorgulayarak da elde edebilirsiniz\_kullanılabilir\_uzantıları.</span><span class="sxs-lookup"><span data-stu-id="b549a-116">You can also obtain this information by querying pg\_available\_extensions.</span></span> 

### <a name="data-types-extensions"></a><span data-ttu-id="b549a-117">Veri türleri uzantıları</span><span class="sxs-lookup"><span data-stu-id="b549a-117">Data types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="b549a-118">**Uzantısı**</span><span class="sxs-lookup"><span data-stu-id="b549a-118">**Extension**</span></span> | <span data-ttu-id="b549a-119">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b549a-119">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="b549a-120">citext</span><span class="sxs-lookup"><span data-stu-id="b549a-120">citext</span></span>](https://www.postgresql.org/docs/9.6/static/citext.html) | <span data-ttu-id="b549a-121">Bir küçük harf karakter dize türü sağlar</span><span class="sxs-lookup"><span data-stu-id="b549a-121">Provides a case-insensitive character string type</span></span> |
| [<span data-ttu-id="b549a-122">hstore</span><span class="sxs-lookup"><span data-stu-id="b549a-122">hstore</span></span>](https://www.postgresql.org/docs/9.6/static/hstore.html) | <span data-ttu-id="b549a-123">Anahtar/değer çiftleri kümesi depolamak için veri türü sağlar</span><span class="sxs-lookup"><span data-stu-id="b549a-123">Provides data type for storing sets of key/value pairs</span></span> |

### <a name="functions-extensions"></a><span data-ttu-id="b549a-124">İşlevler uzantıları</span><span class="sxs-lookup"><span data-stu-id="b549a-124">Functions extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="b549a-125">**Uzantısı**</span><span class="sxs-lookup"><span data-stu-id="b549a-125">**Extension**</span></span> | <span data-ttu-id="b549a-126">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b549a-126">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="b549a-127">fuzzystrmatch</span><span class="sxs-lookup"><span data-stu-id="b549a-127">fuzzystrmatch</span></span>](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | <span data-ttu-id="b549a-128">Çeşitli işlevler toodetermine benzerlikler ve dizeler arasındaki uzaklığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b549a-128">Provides several functions toodetermine similarities and distance between strings.</span></span> |
| [<span data-ttu-id="b549a-129">int</span><span class="sxs-lookup"><span data-stu-id="b549a-129">intarray</span></span>](https://www.postgresql.org/docs/9.6/static/intarray.html) | <span data-ttu-id="b549a-130">İşlevler ve işleçler null serbest diziler tamsayıların yönlendirmek için sağlar.</span><span class="sxs-lookup"><span data-stu-id="b549a-130">Provides functions and operators for manipulating null-free arrays of integers.</span></span> |
| [<span data-ttu-id="b549a-131">pgcrypto</span><span class="sxs-lookup"><span data-stu-id="b549a-131">pgcrypto</span></span>](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | <span data-ttu-id="b549a-132">Şifreleme işlevleri sağlar</span><span class="sxs-lookup"><span data-stu-id="b549a-132">Provides cryptographic functions</span></span> |
| [<span data-ttu-id="b549a-133">PG\_partman</span><span class="sxs-lookup"><span data-stu-id="b549a-133">pg\_partman</span></span>](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | <span data-ttu-id="b549a-134">Bölümlenmiş tablolar zaman veya Kimliğe göre yönetir</span><span class="sxs-lookup"><span data-stu-id="b549a-134">Manages partitioned tables by time or ID</span></span> |
| [<span data-ttu-id="b549a-135">PG\_trgm</span><span class="sxs-lookup"><span data-stu-id="b549a-135">pg\_trgm</span></span>](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | <span data-ttu-id="b549a-136">Merhaba benzerlik trigram eşleşmesini temel alan alfasayısal metnin belirlemek için İşlevler ve işleçler sağlar</span><span class="sxs-lookup"><span data-stu-id="b549a-136">Provides functions and operators for determining hello similarity of alphanumeric text based on trigram matching</span></span> |
| [<span data-ttu-id="b549a-137">UUID ossp</span><span class="sxs-lookup"><span data-stu-id="b549a-137">uuid-ossp</span></span>](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | <span data-ttu-id="b549a-138">Evrensel benzersiz tanımlayıcıları (UUID) oluştur</span><span class="sxs-lookup"><span data-stu-id="b549a-138">Generate universally unique identifiers (UUIDs)</span></span> |

### <a name="full-text-search-extensions"></a><span data-ttu-id="b549a-139">Tam metin arama uzantıları</span><span class="sxs-lookup"><span data-stu-id="b549a-139">Full-text Search extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="b549a-140">**Uzantısı**</span><span class="sxs-lookup"><span data-stu-id="b549a-140">**Extension**</span></span> | <span data-ttu-id="b549a-141">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b549a-141">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="b549a-142">unaccent</span><span class="sxs-lookup"><span data-stu-id="b549a-142">unaccent</span></span>](https://www.postgresql.org/docs/9.6/static/unaccent.html) | <span data-ttu-id="b549a-143">Lexemes vurgular (vurgu işaretlerini) kaldırır metin arama sözlük.</span><span class="sxs-lookup"><span data-stu-id="b549a-143">A text search dictionary that removes accents (diacritic signs) from lexemes.</span></span> |

### <a name="index-types-extensions"></a><span data-ttu-id="b549a-144">Dizin türleri uzantıları</span><span class="sxs-lookup"><span data-stu-id="b549a-144">Index Types extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="b549a-145">**Uzantısı**</span><span class="sxs-lookup"><span data-stu-id="b549a-145">**Extension**</span></span> | <span data-ttu-id="b549a-146">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b549a-146">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="b549a-147">BTree\_GIN</span><span class="sxs-lookup"><span data-stu-id="b549a-147">btree\_gin</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | <span data-ttu-id="b549a-148">Gibi belirli veri türleri için davranış B-Ağacı uygulayan örnek GIN işleci sınıflar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b549a-148">Provides sample GIN operator classes that implement B-tree like behavior for certain data types.</span></span> |
| [<span data-ttu-id="b549a-149">BTree\_gist</span><span class="sxs-lookup"><span data-stu-id="b549a-149">btree\_gist</span></span>](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | <span data-ttu-id="b549a-150">B-Ağacı uygulayan GiST dizin işleci sınıflar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b549a-150">Provides GiST index operator classes that implement B-tree.</span></span> |

### <a name="language-extensions"></a><span data-ttu-id="b549a-151">Dil uzantıları</span><span class="sxs-lookup"><span data-stu-id="b549a-151">Language extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="b549a-152">**Uzantısı**</span><span class="sxs-lookup"><span data-stu-id="b549a-152">**Extension**</span></span> | <span data-ttu-id="b549a-153">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b549a-153">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="b549a-154">plpgsql</span><span class="sxs-lookup"><span data-stu-id="b549a-154">plpgsql</span></span>](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | <span data-ttu-id="b549a-155">PL/pgSQL yüklenebilir yordam dili</span><span class="sxs-lookup"><span data-stu-id="b549a-155">PL/pgSQL loadable procedural language</span></span> |

### <a name="miscellaneous-extensions"></a><span data-ttu-id="b549a-156">Çeşitli uzantıları</span><span class="sxs-lookup"><span data-stu-id="b549a-156">Miscellaneous extensions</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="b549a-157">**Uzantısı**</span><span class="sxs-lookup"><span data-stu-id="b549a-157">**Extension**</span></span> | <span data-ttu-id="b549a-158">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b549a-158">**Description**</span></span> |
|---|---|
| [<span data-ttu-id="b549a-159">PG\_buffercache</span><span class="sxs-lookup"><span data-stu-id="b549a-159">pg\_buffercache</span></span>](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | <span data-ttu-id="b549a-160">Gerçek zamanlı paylaşılan hello arabellek önbelleğindeki neler olduğunu incelemek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="b549a-160">Provides a means for examining what's happening in hello shared buffer cache in real time.</span></span> |
| [<span data-ttu-id="b549a-161">PG\_prewarm</span><span class="sxs-lookup"><span data-stu-id="b549a-161">pg\_prewarm</span></span>](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | <span data-ttu-id="b549a-162">Bir şekilde tooload ilişkisi veri hello arabellek önbelleğine sağlar.</span><span class="sxs-lookup"><span data-stu-id="b549a-162">Provides a way tooload relation data into hello buffer cache.</span></span> |
| [<span data-ttu-id="b549a-163">PG\_stat\_deyimleri</span><span class="sxs-lookup"><span data-stu-id="b549a-163">pg\_stat\_statements</span></span>](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | <span data-ttu-id="b549a-164">Bir sunucu tarafından yürütülen tüm SQL deyimlerini Yürütme istatistiklerini izlemek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="b549a-164">Provides a means for tracking execution statistics of all SQL statements executed by a server.</span></span> |
| [<span data-ttu-id="b549a-165">postgres\_fdw</span><span class="sxs-lookup"><span data-stu-id="b549a-165">postgres\_fdw</span></span>](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | <span data-ttu-id="b549a-166">Dış PostgreSQL sunucuları depolanan tooaccess verileri yabancı veri sarmalayıcı kullanılan</span><span class="sxs-lookup"><span data-stu-id="b549a-166">Foreign-data wrapper used tooaccess data stored in external PostgreSQL servers</span></span> |

### <a name="postgis"></a><span data-ttu-id="b549a-167">PostGIS</span><span class="sxs-lookup"><span data-stu-id="b549a-167">PostGIS</span></span>

> [!div class="mx-tableFixed"]
| <span data-ttu-id="b549a-168">**Uzantısı**</span><span class="sxs-lookup"><span data-stu-id="b549a-168">**Extension**</span></span> | <span data-ttu-id="b549a-169">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b549a-169">**Description**</span></span> |
|---|---|
| <span data-ttu-id="b549a-170">[PostGIS](http://www.postgis.net/), postgis\_topoloji, postgis\_tiger\_geocoder, postgis\_sfcgal</span><span class="sxs-lookup"><span data-stu-id="b549a-170">[PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal</span></span> | <span data-ttu-id="b549a-171">Uzamsal ve coğrafi nesneleri PostgreSQL için.</span><span class="sxs-lookup"><span data-stu-id="b549a-171">Spatial and geographic objects for PostgreSQL.</span></span> |
| <span data-ttu-id="b549a-172">Adres\_standardizer, adresi\_standardizer\_veri\_bize</span><span class="sxs-lookup"><span data-stu-id="b549a-172">address\_standardizer, address\_standardizer\_data\_us</span></span> | <span data-ttu-id="b549a-173">Kullanılan tooparse bağlı öğelerine bir adres.</span><span class="sxs-lookup"><span data-stu-id="b549a-173">Used tooparse an address into constituent elements.</span></span> <span data-ttu-id="b549a-174">Toosupport coğrafi kodlama adresi normalleştirme adım kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b549a-174">Used toosupport geocoding address normalization step.</span></span> |
| [<span data-ttu-id="b549a-175">pgrouting</span><span class="sxs-lookup"><span data-stu-id="b549a-175">pgrouting</span></span>](http://pgrouting.org/) | <span data-ttu-id="b549a-176">Merhaba PostGIS genişletir / PostgreSQL Jeo-uzamsal veritabanı tooprovide Jeo-uzamsal yönlendirme işlevi.</span><span class="sxs-lookup"><span data-stu-id="b549a-176">Extends hello PostGIS / PostgreSQL geospatial database tooprovide geospatial routing functionality.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b549a-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b549a-177">Next steps</span></span>
<span data-ttu-id="b549a-178">Uzantı toouse istediğiniz görmüyorum?</span><span class="sxs-lookup"><span data-stu-id="b549a-178">Don't see an extension you'd like toouse?</span></span> <span data-ttu-id="b549a-179">Lütfen bize bildirin.</span><span class="sxs-lookup"><span data-stu-id="b549a-179">Please let us know.</span></span> <span data-ttu-id="b549a-180">Var olan istekleri için oy verin veya yeni geri bildirim ve içinde dileklerimle oluşturmak bizim [müşteri geri bildirim Forumunda](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).</span><span class="sxs-lookup"><span data-stu-id="b549a-180">Vote for existing requests or create new feedback and wishes in our [Customer feedback forum](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).</span></span>
