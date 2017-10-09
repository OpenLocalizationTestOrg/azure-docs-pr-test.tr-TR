---
title: "aaaSupported kaynak türleri aracılığıyla Azure kaynak durumu | Microsoft Docs"
description: "Desteklenen kaynak türleri aracılığıyla Azure kaynak durumu"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fc7bef214702f8ba6954b5aca62236b38023d27a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Kaynak türleri ve sistem durumu denetler Azure kaynak durumu
Kaynak durumu kaynak türleri tarafından yürütülen tüm hello denetimleri tam bir listesi aşağıda verilmiştir.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Yürütülen denetimleri|
|---|
|<ul><li>Tüm hello önbellek düğümler hazır olduğunda ve çalışıyor?</li><li>Merhaba önbellek hello veri merkezi içinde erişilebilir?</li><li>Önbellek hello en fazla bağlantı sayısı üst sınırına hello var mı?</li><li> Merhaba önbellek kullanılabilir bellek tükendi? </li><li>Merhaba önbellek çok sayıda sayfa hataları yaşıyor?</li><li>Olduğunu aşırı yük durumunda önbellek hello?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Yürütülen denetimleri|
|---|
|<ul> <li>Merhaba uç noktaları hiçbirini, kaldırılan veya yanlış yapılandırılmış durduruldu mu?</li><li>Merhaba ek portal CDN yapılandırma işlemleri için erişilebilir mi?</li><li>CDN uç noktası hello ile devam eden teslim sorunlar var mı?</li><li>Kullanıcılar kendi CDN kaynakların hello yapılandırmasını değiştirebilir miyim?</li><li>Yapılandırma değişiklikleri beklenen hello hızında yayılıyor misiniz?</li><li>Kullanıcıların hello Azure portal, PowerShell veya hello API kullanarak hello CDN yapılandırmasını yönetebilir miyim?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Yürütülen denetimleri|
|---|
|<ul><li>Merhaba ana bilgisayar açık ve çalışıyor?</li><li>Merhaba ana bilgisayar işletim sistemi önyükleme tamamlandı?</li><li>Merhaba sanal makine kapsayıcısını sağlandığında ve güç?</li><li>Merhaba konak ve hello depolama hesabı arasında ağ bağlantısı var mı?</li><li>Merhaba hello konuk işletim sistemi önyükleme tamamlandı?</li><li>Devam eden planlı bakım var mı?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/Accounts
|Yürütülen denetimleri|
|---|
|<ul><li>Merhaba hesap hello veri merkezi içinde erişilebilir?</li><li>Bilişsel hizmetler kaynak sağlayıcısı kullanılabilir hello olduğu?</li><li>Olan Bilişsel hizmet kullanılabilir hello uygun bölgede hello?</li><li>Okuyabilir işlemleri hello kaynak meta verilerini tutan hello depolama hesabında gerçekleştirilmesi?</li><li>Merhaba API çağrısı kotasına ulaşıldı?</li><li>Merhaba API çağrısı okuma-sınırına ulaşıldı?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.COMPUTE/virtualmachines
|Yürütülen denetimleri|
|---|
|<ul><li>Merhaba sunucu yukarı bu sanal makine barındırma ve çalışır?</li><li>Merhaba ana bilgisayar işletim sistemi önyükleme tamamlandı?</li><li>Merhaba sanal makine kapsayıcısını sağlandığında ve güç?</li><li>Merhaba konak ve hello depolama hesabı arasında ağ bağlantısı var mı?</li><li>Merhaba hello konuk işletim sistemi önyükleme tamamlandı?</li><li>Devam eden planlı bakım var mı?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/Accounts
|Yürütülen denetimleri|
|---|
|<ul><li>Gönderme tooData Lake Analytics işleri kullanıcıların bölge hello?</li><li>Temel işleri çalıştırma ve eksiksiz başarıyla hello bölge musunuz?</li><li>Kullanıcılar, katalog öğelerini hello bölgede listeleyebilirsiniz?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/Accounts
|Yürütülen denetimleri|
|---|
|<ul><li>Kullanıcıların veri tooData Lake deposu hello bölgede yükleyebilir miyim?</li><li>Kullanıcılar verileri Data Lake Store hello bölgede yükleyebilir?</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Yürütülen denetimleri|
|---|
|<ul><li>Bulunmamış tooa DocumentDB hizmet kullanılamazlık hizmet olmayan veritabanı veya koleksiyon istekleri?</li><li>Bulunmamış tooa DocumentDB hizmet kullanılamazlık hizmet olmayan herhangi bir belge isteğini?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.Network/Connections
|Yürütülen denetimleri|
|---|
|<ul><li>Merhaba VPN tüneli bağlı mı?</li><li>Yapılandırma çakışmaları hello bağlantısında var mı?</li><li>Merhaba önceden paylaşılan anahtarlar düzgün yapılandırılmış?</li><li>Merhaba VPN şirket içi cihaz ulaşılabilir mu?</li><li>Eşleşmeler hello IPSec/IKE güvenlik ilkesi var mı?</li><li>Merhaba S2S VPN bağlantısı düzgün sağlanan veya başarısız durumda mı?</li><li>Merhaba VNET-VNET bağlantısı düzgün sağlanan veya başarısız durumda mı?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Yürütülen denetimleri|
|---|
|<ul><li>Merhaba VPN ağ geçidi alanından erişilebildiğinden Internet hello?</li><li>Olan bekleme modunda VPN ağ geçidi hello?</li><li>Merhaba VPN hizmeti üzerinde hello ağ geçidi çalışıyor mu?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Yürütülen denetimleri|
|---|
|<ul><li> Çalışma zamanı işlemleri kayıt, yükleme veya gönderme gibi hello ad gerçekleştirilebilir?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Yürütülen denetimleri|
|---|
|<ul><li>Hello konak işletim sistemi için açık ve çalışıyor?</li><li>Merhaba workspaceCollection hello veri merkezi dışında erişilebildiğinden?</li><li>Olduğundan Powerbı kaynak sağlayıcısı hello?</li><li>Olduğundan Powerbı hizmeti kullanılabilir hello uygun bölgede hello?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Yürütülen denetimleri|
|---|
|<ul><li>Tanılama işlemleri hello kümede gerçekleştirilebilir?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Yürütülen denetimleri|
|---|
|<ul><li> Oturum açma bilgileri toohello veritabanı bulunmamış mi?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Yürütülen denetimleri|
|---|
|<ul><li>Burada hello iş yukarı yürütme ve çalışan tüm hello ana misiniz?</li><li>Merhaba işi oluşturulamıyor toostart oldu mu?</li><li>Devam eden çalışma zamanı yükseltmeler var mı?</li><li>Merhaba iş beklenen durumda (Örneğin çalışan veya müşteri tarafından durduruldu)?</li><li>Merhaba işi çıkışı bellek özel durumları karşılaştı?</li><li>Devam eden zamanlanmış işlem güncelleştirmeler var mı?</li><li>Olan hello yürütme Yöneticisi (Denetim plan) kullanılabilir?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Yürütülen denetimleri|
|---|
|<ul><li>Merhaba ana bilgisayar açık ve çalışıyor?</li><li>Internet Information Services çalışıyor mu?</li><li>Merhaba yük dengeleyici çalışıyor mu?</li><li>Merhaba Web Service planı hello veri merkezi içinde erişilebilir?</li><li>Merhaba depolama hesabı barındırma hello siteleri içerik hello sunucu grubu için kullanılabilir??</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.Web/Sites
|Yürütülen denetimleri|
|---|
|<ul><li>Merhaba ana bilgisayar açık ve çalışıyor?</li><li>Internet Information server çalışıyor mu?</li><li>Merhaba yük dengeleyici çalışıyor mu?</li><li>Web uygulaması Hello hello veri merkezi içinde erişilebilir?</li><li>Merhaba depolama hesabı hello site içeriğini barındıran?</li></ul>|

# <a name="next-steps"></a>Sonraki Adımlar
-  Bkz: [giriş tooAzure hizmet durumu](service-health-overview.md) ve [giriş tooAzure kaynak durumu](resource-health-overview.md) toounderstand bunları hakkında daha fazla bilgi. 
-  [Azure kaynak durumu hakkında sık sorulan sorular](resource-health-faq.md)
- Sistem durumu sorunları, bildirim almak için uyarıları ayarlayın. Daha fazla bilgi için bkz: [hizmet durumu uyarıları yapılandırmak](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 