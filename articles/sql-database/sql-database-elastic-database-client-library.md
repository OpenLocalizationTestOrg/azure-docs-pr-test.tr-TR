---
title: "aaaBuilding ölçeklenebilir bulut veritabanları | Microsoft Docs"
description: "Merhaba esnek veritabanı istemci kitaplığı ile ölçeklenebilir .NET veritabanı uygulamalar oluşturma"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a>Ölçeklenebilir bulut veritabanları oluşturma
Veritabanları ölçeklendirme Azure SQL veritabanı için ölçeklenebilir araçları ve özelliklerinin kullanılarak kolayca gerçekleştirilebilir. Özellikle, hello kullanabilirsiniz **esnek veritabanı istemci Kitaplığı** toocreate ölçeklendirilmiş veritabanlarını ve yönetme. Bu özellik kolayca yüzlerce kullanarak parçalı uygulamalar geliştirmenize olanak sağlar; veya hatta binlerce — Azure SQL veritabanlarının. [Esnek iş](sql-database-elastic-jobs-powershell.md) kullanılan toohelp kolaylığı yönetim bu veritabanlarının sonra olabilir.

tooinstall hello kitaplığı, çok Git[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="documentation"></a>Belgeler
1. [Esnek Veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md)
2. [Esnek veritabanı özellikleri](sql-database-elastic-scale-introduction.md)
3. [Parça eşleme yönetimi](sql-database-elastic-scale-shard-map-management.md)
4. [Varolan veritabanları tooscale kullanıma geçirme](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [Verilere bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md)
6. [Çok parça sorguları](sql-database-elastic-scale-multishard-querying.md)
7. [Esnek veritabanı araçlarını kullanarak bir parça ekleme](sql-database-elastic-scale-add-a-shard.md)
8. [Çok kiracılı uygulamalarla esnek veritabanı araçlarını ve satır düzeyi güvenlik](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [İstemci Kitaplığı uygulamaları yükseltme](sql-database-elastic-scale-upgrade-client-library.md) 
10. [Esnek sorgular genel bakış](sql-database-elastic-query-overview.md)
11. [Esnek veritabanı araçları sözlüğü](sql-database-elastic-scale-glossary.md)
12. [Entity Framework ile esnek veritabanı istemci kitaplığı](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [Dapper ile esnek veritabanı istemci kitaplığı](sql-database-elastic-scale-working-with-dapper.md)
14. [Bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md)
15. [Parça eşleme yöneticisi için performans sayaçları](sql-database-elastic-database-client-library.md) 
16. [Esnek veritabanı araçlarını hakkında SSS](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a>İstemci özellikleri
Ölçeklendirme kullanarak uygulamaları *parçalama* hem hello geliştirici, hem de Merhaba yönetici sorunları gösterir. Her iki geliştiriciler olanak sağlayan araçlar vererek Hello istemci kitaplığı hello yönetim görevlerini basitleştirir ve yöneticiler ölçeklendirilmiş veritabanları yönetin. Tipik bir örnekte "parça," toomanage bilinen birçok veritabanı vardır. Müşteriler içinde birlikte bulunur hello aynı veritabanını ve müşteri (tek Kiracı düzeni) başına tek bir veritabanı yok. Merhaba istemci kitaplığı, şu özellikleri içerir:

- **Parça eşleme Yönetim**: hello "parça eşleme manager" adlı özel bir veritabanı oluşturulur. Parça eşleme yönetimi, bir uygulama toomanage meta verileri, parça hakkında hello yeteneğidir. Geliştiriciler bu işlevselliği tooregister veritabanları parça, tek tek parçalama anahtarları ve anahtar aralıklarına toothose veritabanları eşlemeleri açıklamak ve kullanabileceğiniz hello sayı olarak bu meta verileri korumak ve veritabanlarının birleşim tooreflect kapasite değişiklikleri dönüşmesi. Merhaba esnek veritabanı istemci kitaplığı toospend çok parçalama uygularken hello yönetim kod yazma zaman gerekir. Ayrıntılar için bkz [parça eşleme Yönetim](sql-database-elastic-scale-shard-map-management.md).

- **Veri bağımlı yönlendirme**: hello uygulamasına gelen bir istek düşünün. Merhaba parçalama anahtar değeri hello istek temel alınarak, veritabanı hello anahtar değere göre doğru toodetermine hello Merhaba uygulaması gerekir. Ardından, bir bağlantı toohello veritabanı tooprocess hello isteği açar. Veri bağımlı yönlendirme hello parça eşleme tek kolay çağrısını tooopen bağlantılarla hello uygulamasının hello yeteneği sağlar. Veri bağımlı yönlendirme şimdi hello esnek veritabanı istemci Kitaplığı'nda işlevi tarafından kapsanan altyapı kodu başka bir alanı oluştu. Ayrıntılar için bkz [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md).
- **Çok parça sorgular (MSQ)**: çok parça sorgulama bir istek çeşitli (veya tüm) parça gerektirdiğinde çalışır. Merhaba çok parça Sorguyu yürüten tüm parça veya parça kümesi aynı T-SQL kodu. Parça katılan hello Hello sonuçlarından UNION ALL semantiği kullanılarak ayarlanan bir genel sonuç birleştirilir. Merhaba hello istemci kitaplığı gösterilen işlevselliği işleme dahil birçok görevi: bağlantı yönetimi, iş parçacığı yönetimi, hata işleme ve Ara sonuçların işleniyor. MSQ parça toohundreds sorgulayabilirsiniz. Ayrıntılar için bkz [çok parça sorgulama](sql-database-elastic-scale-multishard-querying.md).

Genel olarak, esnek veritabanı araçlarını kullanan müşteriler parça yerel işlemleri kendi semantiklerine sahip karşılıklı toocross parça işlemleri olarak gönderirken tooget işlevlerini T-SQL bekleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba deneyin [örnek uygulaması](sql-database-elastic-scale-get-started.md) hello istemci işlevleri gösterir. 

tooinstall hello kitaplığı, çok Git[esnek veritabanı istemci Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Merhaba bölünmüş birleştirme aracını kullanma hakkında yönergeler için bkz hello [bölünmüş birleştirme aracına genel bakış](sql-database-elastic-scale-overview-split-and-merge.md).

[Esnek veritabanı istemci kitaplığı olan şimdi açık kaynaklı!](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

Kullanım [esnek sorgular](sql-database-elastic-query-overview.md).

Merhaba Kitaplığı açık kaynak yazılımının olarak kullanılabilir [GitHub](https://github.com/Azure/elastic-db-tools). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

