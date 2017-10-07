---
title: "SQL veri ambarı aaaUser tanımlı şemalarda | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse'da Transact-SQL şemalarını kullanma ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>Kullanıcı tanımlı şemaları SQL veri ambarı
Geleneksel veri ambarları genellikle kullanım ayrı veritabanlarını toocreate uygulama sınırlarını iş yükü, etki alanı veya güvenlik dayanarak. Örneğin, geleneksel SQL Server veri ambarı Hazırlama veritabanı, veri ambarı veritabanı ve bazı veri reyonu veritabanı içerebilir. Bu topolojide, her veritabanı iş yükü ve güvenlik sınırı hello mimarisinde olarak çalışır.

Bunun aksine, SQL Data Warehouse hello tüm veri ambarı iş yükü bir veritabanı içinde çalışır. Veritabanı birleştirmeler izin verilmez. Bu nedenle SQL Data Warehouse hello bir veritabanı içinde depolanan hello ambar toobe tarafından kullanılan bütün tablolar bekliyor.

> [!NOTE]
> SQL veri ambarı veritabanları arası sorguları herhangi bir türde desteklemez. Sonuç olarak, bu deseni yararlanan veri ambarı uygulamaları düzenlendi toobe gerekir.
> 
> 

## <a name="recommendations"></a>Öneriler
Kullanıcı tanımlı şemalarını kullanarak iş yükleri, güvenlik, etki alanı ve işlevsel sınırları birleştirilmesi için öneriler bunlar

1. Bir SQL Data Warehouse veritabanı toorun, tüm veri ambarı iş yükü kullanın
2. Var olan veri ambarı ortamında toouse bir SQL Data Warehouse veritabanınız birleştirin
3. Dengeleme **kullanıcı tanımlı şemaları** veritabanları kullanılarak daha önce uygulanan tooprovide hello sınır.

Kullanıcı tanımlı şemaları kullanılmadı önceden sonra temiz bir Kurşun varsa. Yalnızca hello eski veritabanı adı, kullanıcı tanımlı şemaları hello SQL veri ambarı veritabanındaki için hello temel olarak kullanın.

Ardından şemaları zaten kullandıysanız, birkaç seçeneğiniz vardır:

1. Merhaba eski şema adlarını kaldırın ve yeniden Başlat
2. Merhaba eski şema adları önceden bekleyen hello eski şema toohello tablo adı ile koruyun
3. Bir ek şema toore hello tabloda üzerinden görünümleri uygulayarak Hello eski şema adlarını korumak-hello eski şema yapısı oluşturun.

> [!NOTE]
> İlk denetimi seçenek 3 hello en cazip seçeneği gibi görünebilir. Ancak, hello Şeytan hello ayrıntılı olarak vardır. Görünümler, yalnızca SQL veri ambarında salt okunurdur. Tüm veri veya tabloda değişiklik hello temel tablo karşı gerçekleştirilen toobe gerekir. Seçenek 3, aynı zamanda bir katman görünümlerinin sisteminize sunar. Görünümler, mimarisinde zaten kullanıyorsanız, bu bazı ek bir düşünce toogive isteyebilirsiniz.
> 
> 

### <a name="examples"></a>Örnekler:
Kullanıcı tanımlı şemaları veritabanı adlarına göre uygulama

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

Korumak eski şema adları tarafından önceden bekleyen bunları toohello tablo adı. Şemalar hello iş yükü sınırı için kullanın.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

Görünümleri kullanarak eski şema adlarını korur

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> Şema stratejisi herhangi bir değişikliği hello güvenlik modeli gözden hello veritabanı için gerekir. Çoğu durumda hello şema düzeyinde izinler atayarak mümkün toosimplify hello güvenlik modeli olabilir. Daha ayrıntılı izinler gerekli olduğunda, veritabanı rolleri kullanabilirsiniz.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
