---
title: "aaaSQL veritabanı uygulaması geliştirmeye genel bakış | Microsoft Docs"
description: "Kullanılabilir bağlantı kitaplıkları ve tooSQL veritabanına bağlanan uygulamalar için en iyi uygulamalar hakkında bilgi edinin."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a>SQL veritabanı uygulaması geliştirmeye genel bakış
Bu makalede, geliştiricinin kod tooconnect tooAzure SQL veritabanı yazarken bilmeniz gereken hello temel konuları anlatılmaktadır.

> [!TIP]
> Toocreate bir sunucu oluşturmak nasıl bir sunucu tabanlı güvenlik duvarı sunucusunun özelliklerini görüntüle, SQL Server Management Studio, sorgu hello ana veritabanını kullanarak bağlanmak, örnek bir veritabanı ve boş bir veritabanı oluşturmak, veritabanı özellikleri sorgu bir öğretici gösteren için bağlanmak SQL Server Management Studio ve sorgu hello örnek veritabanı kullanarak, bkz: [Öğreticisi almak](sql-database-get-started-portal.md).
>

## <a name="language-and-platform"></a>Dil ve platform
Çeşitli programlama dilleri ve platformları için kod örnekleri mevcuttur. Bağlantılar toohello kod örnekleri konumunda bulabilirsiniz: 

* Daha Fazla Bilgi: [SQL Veritabanı ve SQL Server için bağlantı kitaplıkları](sql-database-libraries.md)

## <a name="tools"></a>Araçlar 
[Cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli), [VS Code](https://code.visualstudio.com/) gibi açık kaynak araçlardan yararlanabilirsiniz. Ayrıca, Azure SQL Veritabanı [Visual Studio](https://www.visualstudio.com/downloads/) ve [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) gibi Microsoft araçlarıyla birlikte çalışır.  Hello Azure Yönetim Portalı, PowerShell de kullanabilirsiniz ve REST API'leri yardımcı ek verimlilik elde.

## <a name="resource-limitations"></a>Kaynak sınırlamaları
Azure SQL veritabanı iki farklı mekanizmalarını kullanarak hello kaynakları kullanılabilir tooa veritabanı yönetir: kaynak İdaresi ve zorlama, sınırlar.

* Daha Fazla Bilgi: [Azure SQL Veritabanı kaynak limitleri](sql-database-resource-limits.md)

## <a name="security"></a>Güvenlik
Azure SQL Veritabanı, bir SQL Veritabanında erişim sınırlama, veri koruma ve izleme etkinlikleri için kaynaklar sunar.

* Daha Fazla Bilgi: [SQL Veritabanınızı güvenli hale getirme](sql-database-security-overview.md)

## <a name="authentication"></a>Kimlik Doğrulaması
* Azure SQL Veritabanı, SQL Server kimlik doğrulama kullanıcıları ve oturum açma bilgilerinin yanı sıra [Azure Active Directory kimlik doğrulama](sql-database-aad-authentication.md) kullanıcılarını ve oturum açma bilgilerini destekler.
* Toospecify varsayılanı toohello yerine belirli bir veritabanının gereksinim *ana* veritabanı.
* Merhaba Transact-SQL kullanamazsınız **kullanım myDatabaseName;** SQL veritabanı tooswitch tooanother veritabanında deyimi.
* Daha fazla bilgi: [SQL Veritabanı güvenliği: Veritabanı erişim ve oturum açma güvenliğini yönetme](sql-database-manage-logins.md)

## <a name="resiliency"></a>Dayanıklılık
TooSQL veritabanına bağlanırken geçici bir hata ortaya çıktığında, kodunuzu hello çağrı yeniden denemeniz gerekir.  Öneririz yeniden deneme mantığı geri Çekilme mantığı kullanın, böylece değil doldurmaya SQL veritabanı ile birden çok istemci aynı anda yeniden deneniyor hello.

* Kod örnekleri: hello dili için örnek gösteren kod örnekleri mantığı yeniden denemek için bkz: [SQL Database ve SQL Server için bağlantı kitaplıkları](sql-database-libraries.md)
* Daha fazla bilgi: [SQL Veritabanı istemci programları için hata iletileri](sql-database-develop-error-messages.md)

## <a name="managing-connections"></a>Bağlantıları yönetme
* İstemci bağlantısı mantığında hello varsayılan zaman aşımı toobe 30 saniye geçersiz kılar.  Merhaba varsayılan değeri 15 saniye için çok fazla bağımlı bağlantıları hello Internet.
* Kullanıyorsanız bir [bağlantı havuzu](http://msdn.microsoft.com/library/8xx3tyca.aspx), emin tooclose hello bağlantı hello programınızı etkin olarak kullandığı değil ve tooreuse hazırlama değil anlık getirin.

## <a name="network-considerations"></a>Ağ konuları
* İstemci programınızı barındıran hello bilgisayarda hello güvenlik duvarı bağlantı noktası 1433 giden TCP iletişim kurmasına olanak tanıyan emin olun.  Daha fazla bilgi: [Azure SQL Veritabanı güvenlik duvarını yapılandırma](sql-database-configure-firewall-settings.md)
* İstemciniz bir Azure sanal makine (VM) üzerinde çalışırken, istemci programınızı tooSQL veritabanı bağlanıyorsa, belirli bağlantı noktası aralıkları hello VM üzerinde açmanız gerekir. Daha fazla bilgi: [ADO.NET 4.5 ve SQL veritabanı için 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md)
* İstemci bağlantıları tooAzure SQL veritabanı bazen hello proxy atlayabilir ve doğrudan hello veritabanıyla etkileşim. 1433 dışındaki bağlantı noktaları önemli hale gelmiştir. Daha fazla bilgi için [Azure SQL veritabanı bağlantısı mimarisi](sql-database-connectivity-architecture.md) ve [ADO.NET 4.5 ve SQL veritabanı için 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="data-sharding-with-elastic-scale"></a>Esnek ölçeklendirme ile veri parçalama
Esnek ölçeklendirme (ve) ölçeklendirme hello işlemini basitleştirir. 

* [Azure SQL Veritabanı ile Çok Kiracılı SaaS Uygulamaları için Tasarım Desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Verilere bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md)
* [Azure SQL Veritabanı Elastik Ölçeklendirmeyi Kullanmaya Başlama](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a>Sonraki adımlar
Tüm hello keşfedin [SQL veritabanı özellikleri](sql-database-technical-overview.md)
