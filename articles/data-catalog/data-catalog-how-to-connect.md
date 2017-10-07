---
title: "aaaHow tooconnect toodata kaynakları | Microsoft Docs"
description: "Azure veri Kataloğu ile nasıl tooconnect toodata kaynakları bulunan vurgulama nasıl-tooarticle."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>Nasıl tooconnect toodata kaynakları
## <a name="introduction"></a>Giriş
**Microsoft Azure veri Kataloğu** bir kayıt ve sistemi kurumsal veri kaynakları için bulma görevi gören bir tam olarak yönetilen bir bulut hizmetidir. Diğer bir deyişle, **Azure veri Kataloğu** tüm yardımcı kişilerle ilgili bulmak, anlamak ve veri kaynaklarını kullanmak ve kuruluşların tooget yardımcı olacak daha fazla kendi varolan veriler değeri. Temel bir yönü bu senaryo, bir kullanıcı bir veri bulur sonra veri – kaynağı ve amacı anlar hello kullanarak, hello sonraki adım, veri toouse tooput tooconnect toohello veri kaynağı.

## <a name="data-source-locations"></a>Veri kaynağı konumları
Veri kaynağı kaydı sırasında **Azure veri Kataloğu** hello veri kaynağı ile ilgili meta verileri alır. Bu meta veriler hello veri kaynağının konumu hello ayrıntılarını içerir. Başlangıç konumu Hello ayrıntılarını veri kaynağı toodata kaynağından farklılık gösterir ancak her zaman hello gerekli bilgileri tooconnect içerecektir. Örneğin, hello sunucu adını ve hello yolu toohello rapor bir SQL Server Reporting Services rapor için başlangıç konumu içerir ancak hello konumunu bir SQL Server tablo için hello sunucu adı, veritabanı adı, şema adı ve tablo adı içerir. Diğer veri kaynağı türleri hello yapısı ve hello kaynak sistemi özelliklerini yansıtan konumları sahip olur.

## <a name="integrated-client-tools"></a>Tümleşik istemci araçlarında
Merhaba en basit yolu tooconnect tooa veri kaynağıdır toouse hello "içinde Aç..." Merhaba menüde **Azure veri Kataloğu** portal. Bu menü toohello seçili veri varlığına bağlanma seçeneklerin bir listesini görüntüler.
Merhaba varsayılan döşeme görünümünü kullanırken, bu menüsünde kullanılabilir her bölme'üzerinde hello.

 ![Bir SQL Server tablo Excel'de hello veri varlık kutucuğunda açma](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Merhaba liste görünümünü kullanırken hello menü hello portal penceresinin hello üstünde hello arama çubuğunda kullanılabilir.

 ![SQL Server Reporting Services raporunun Rapor Yöneticisi'nde hello Arama çubuğundan açma](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>Desteklenen istemci uygulamaları
Merhaba kullanılırken "içinde Aç..." hello Azure veri Kataloğu portalında menü veri kaynakları, Merhaba doğru istemci uygulaması hello istemci bilgisayarda yüklü olmalıdır.

| Uygulama Aç | Dosya uzantısı / Protokolü | Desteklenen uygulama sürümleri |
| --- | --- | --- |
| Excel |.odc |Excel 2010 veya üzeri |
| Excel (ilk 1000) |.odc |Excel 2010 veya üzeri |
| Power Query |.xlsx |Excel 2016 veya Excel 2010 veya Excel 2013 için Excel eklentisi hello Power Query ile yüklü |
| Power BI Desktop |.pbix |Power BI Desktop Temmuz 2016 veya sonraki |
| SQL Server Veri Araçları |vsweb: / / |Visual Studio 2013 güncelleştirme 4 veya üstü yüklü SQL Server araçları ile |
| Rapor Yöneticisi |http:// |Bkz: [SQL Server Reporting Services için tarayıcı gereksinimleri](https://technet.microsoft.com/en-us/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>Araçlarınızı verilerinizi
Merhaba hello menüsünde kullanılabilir seçenekleri hello şu anda seçili veri varlık türüne bağlıdır. Elbette, tüm olası araçları hello eklenecektir "içinde Aç..." Menü, ancak herhangi bir istemci araç kullanarak hala kolay tooconnect toohello veri kaynağına olur. Bir veri varlığına hello seçili olduğunda **Azure veri Kataloğu** portal, hello tam konum hello Özellikler bölmesinde da görüntülenir.

 ![Bağlantı bilgilerini bir SQL Server tablosu](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

Ayrıntılar veri kaynağı türü toodata kaynak türü, ancak hello Portalı'nda eklenen hello bilgileri farklılık gösterecektir hello bağlantı bilgilerini tooconnect toohello veri kaynağı herhangi bir istemci aracında ihtiyaç duyduğunuz her şeyi verir. Kullanıcılar, hello bağlantı ayrıntıları kullanılarak bulunan hello veri kaynakları için kopyalayabilir **Azure veri Kataloğu**, kendi aracında tercih hello verilerle toowork etkinleştirme.

## <a name="connecting-and-data-source-permissions"></a>Bağlanma ve veri kaynağı izinleri
Ancak **Azure veri Kataloğu** bulunabilir, access veri kaynaklarını yapar toohello verilerin kendisini hello veri kaynağına sahip veya yönetici hello denetiminde kalır. Bir veri kaynağı bulma **Azure veri Kataloğu** bir kullanıcı tüm izinleri tooaccess hello veri kaynağı kendisini sağlamaz.

toomake kolaylaştırır veri Bul kullanıcılar kaynak ancak izni tooaccess kendi verileriniz yoksa, kullanıcılar hello istek erişimi özellik bilgileri bir veri kaynağına açıklama durumlarda sağlayabilir. Merhaba veri kaynağı konumu bilgileri hello portalında yanında – dahil, bağlantılar toohello işlem veya veri kaynağına erişim kazanmak için iletişim noktası – burada sağlanan bilgiler sunulur.

 ![Sağlanan istek erişim yönergeleri ile bağlantı bilgileri](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>Özet
Veri kaynağı ile kaydetme **Azure veri Kataloğu** katalog hizmeti hello hello veri kaynağından yapısal ve açıklayıcı meta verileri kopyalayarak verileri bulunabilir hale getirir. Bir veri kaynağı kaydedildi, bulunan ve sonra kullanıcılar hello toohello veri kaynağına bağlanabilir **Azure veri Kataloğu** portalı "içinde Aç..." " menü veya tercih ettiğiniz kendi veri Araçları'nı kullanarak.

## <a name="see-also"></a>Ayrıca bkz.
* [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md) hakkında adım adım ayrıntılar için öğretici tooconnect toodata kaynakları.
