---
title: "SQL veritabanı için 1433 ötesinde aaaPorts | Microsoft Docs"
description: "ADO.NET tooAzure SQL veritabanı'ten istemci bağlantılarını bazen hello proxy atlayabilir ve doğrudan hello veritabanıyla etkileşim. 1433 dışındaki bağlantı noktaları önemli hale gelmiştir."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a>ADO.NET 4.5 için 1433 dışındaki bağlantı noktaları
Bu konu, ADO.NET 4.5 veya sonraki bir sürümünü kullanan istemciler için hello Azure SQL veritabanı bağlantı davranışını tanımlar. 

> [!IMPORTANT]
> Bağlantı mimarisi hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı bağlantısı mimarisi](sql-database-connectivity-architecture.md).
>

## <a name="outside-vs-inside"></a>Dış vs içinde
Bağlantıları tooAzure SQL veritabanı için biz ilk istemci programınız çalışıp çalışmayacağını başvurmalısınız *dışında* veya *içinde* hello Azure bulut sınır. Merhaba alt bölümlerde iki yaygın senaryolar açıklanmaktadır.

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*Dış:* istemcisi, masaüstü bilgisayarınızda çalıştırır
Bağlantı noktası 1433 SQL veritabanı istemci uygulamanızı barındıran masaüstü bilgisayarınızda açılmalıdır hello tek bağlantı noktasıdır.

#### <a name="inside-client-runs-on-azure"></a>*İç:* istemci Azure üzerinde çalışır
İstemciniz hello Azure bulut sınırının içinde çalıştığında, veririz kullandığı bir *doğrudan rota* toointeract hello SQL veritabanı sunucusu ile. Bağlantı kurulduktan sonra daha sonraki etkileşimler hello istemci ve veritabanı arasındaki hiçbir ara proxy içerir.

Merhaba dizisi aşağıdaki gibidir:

1. ADO.NET 4.5 (veya üzeri) hello Azure bulut kısa bir etkileşim başlatır ve dinamik olarak tanımlanan bağlantı noktası numarasını alır.
   
   * 11000 11999 veya 14000 14999 hello aralıkta dinamik olarak tanımlanan hello bağlantı noktası numarasıdır.
2. ADO.NET ardından toohello SQL veritabanı sunucusuna doğrudan hiçbir Ara yazılımla arasında bağlanır.
3. Sorgular doğrudan toohello veritabanı gönderilir ve sonuçları doğrudan toohello istemci döndürülür.

11000 11999 ve Azure İstemci makinenizde 14000 14999 aralıklarına SQL veritabanı ile ADO.NET 4.5 istemci etkileşimler için kullanılabilir kalan o hello bağlantı noktası emin olun.

* Özellikle, hello aralığındaki bağlantı noktalarına diğer giden blockers boş olması gerekir.
* Azure VM'nizi hello **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı** denetimleri hello bağlantı noktası ayarları.
  
  * Merhaba kullanabilirsiniz [güvenlik duvarının kullanıcı arabirimi](http://msdn.microsoft.com/library/cc646023.aspx) hello belirttiğiniz kuralı bir tooadd **TCP** protokolü bir bağlantı noktası aralığı hello sözdizimi ile birlikte ister **11000 11999**.

## <a name="version-clarifications"></a>Sürüm açıklamalar
Bu bölümde tooproduct sürümleri başvuran hello adlar açıklar. Ayrıca, bazı ürünler arasındaki sürümleri eşleştirmelerini listeler.

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 hello TDS 7.3 protokolünü kullanır, ancak değil 7.4 destekler.
* ADO.NET 4.5 ve sonraki hello TDS 7.4 protokolünü destekler.

## <a name="related-links"></a>İlgili bağlantılar
* ADO.NET 4.6 20 Temmuz 2015 tarihinde yayımlanmıştır. Merhaba .NET ekibi Web günlüğü duyurudan kullanılabilir [burada](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).
* ADO.NET 4.5 15 Ağustos 2012'de serbest bırakıldı. Merhaba .NET ekibi Web günlüğü duyurudan kullanılabilir [burada](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).
  
  * ADO.NET 4.5.1 hakkında bir blog gönderisini kullanılabilir [burada](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).
* [TDS Protokolü sürüm listesi](http://www.freetds.org/userguide/tdshistory.htm)
* [SQL veritabanı geliştirme genel bakış](sql-database-develop-overview.md)
* [Azure SQL veritabanı güvenlik duvarı](sql-database-firewall-configure.md)
* [Nasıl yapılır: SQL veritabanında güvenlik duvarı ayarlarını yapılandırma](sql-database-configure-firewall-settings.md)

