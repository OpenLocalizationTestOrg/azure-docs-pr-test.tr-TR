---
title: "aaaAzure SDK .NET 2.6 sürüm notları"
description: "2.6 .NET için Azure SDK sürüm notları"
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>2.6 .NET için Azure SDK sürüm notları
Bu belge .NET 2.6 yayımı için Azure SDK'sı hello hello sürüm notları içeriyor. 

Azure SDK 2.6 ile bulut hizmet uygulamaları (PaaS) bulut hizmet rolü hello üzerinde hello hedef .NET Framework'ü el ile yüklemeniz koşuluyla .NET 4.5.2 veya .NET 4.6 hedefleme geliştirebilirsiniz. Bkz: [bir bulut hizmeti rolü'nde .NET yükleme](http://go.microsoft.com/fwlink/?LinkID=309796).

## <a name="service-bus-updates"></a>Hizmet veri yolu güncelleştirmeleri
* Olay hub'ları: 
  
  * Şimdi olayları Event Hubs için ek yayımcı uç nokta göstererek gönderirken hedeflenen erişim denetimi sağlar.
  * Ek kararlılık ve geliştirme tooEvent hub özellik eklemiştir.
  * İleti için Amqp protokolünü desteği WebSocket üzerinden ekleme ve Event Hubs.

## <a name="hdinsight-tools-for-visual-studio-updates"></a>Visual Studio için Hdınsight araçları güncelleştirir
* **IntelliSense geliştirme**: Uzak meta veri önerisi
  
    Şimdi, Hive betiğinizi düzenlerken Visual Studio için Hdınsight araçları alma uzak meta veri destekler. Örneğin, yazabilirsiniz **seçin * FROM** ve tüm hello tablo adları gösterilir. Ayrıca, bir tablo belirttikten sonra hello sütun adları gösterilir.
* **Hdınsight öykünücü desteği**
  
    Artık herhangi bir maliyeti oluşturmaksızın Hive komut dosyalarınızı yerel olarak geliştirebilir şekilde tooHDInsight öykünücüsü bağlanma Visual Studio desteği için Hdınsight araçları, ardından bu komut, Hdınsight kümeleri karşı yürütün. 
  
    Daha fazla bilgi için çok başvurun[bu el ile](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).
* **Visual Studio için Hdınsight araçları desteklemek için genel Hadoop kümeleri** (Önizleme)
  
    Şimdi Visual Studio toodo hello şunlar için Hdınsight araçları kullanabilmeniz için Visual Studio için Hdınsight Araçları Genel Hadoop kümelerini destekler:
  
  * tooyour küme Bağlan 
  * Otomatik/IntelliSense-tamamlama desteği Hive sorgusu Yaz, 
  * sezgisel bir kullanıcı Arabirimi ile kümenizdeki tüm hello işleri görüntüleyin. 
    
    Daha fazla bilgi için çok başvurun[bu el ile](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).

## <a name="in-role-cache-updates"></a>Rol içi önbelleği güncelleştirmeleri
* **Rol içi önbelleği** güncelleştirilmiş toouse olan **Microsoft Azure depolama SDK'sı** sürümü 4.3. Şimdiye kadar hello **rol içi önbelleği** Azure depolama SDK'sı 1.7 sürümü kullanıyordu.
  
    Müşterilerin Azure SDK 2.5 kullanarak veya aşağıda tooAzure SDK 2.6 güncelleştirmek ve Azure depolama SDK'ın yeni sürümü toohello taşıyın. 
  
    Bu zaman Azure depolama 2011 08 18 1 Ağustos 2016 kaldırılan zamanlanmış toobe sürümüdür. Rol içi önbelleği Azure SDK 2.5 veya too2.6 altındaki tüm geçirilmesi bu zamana kadar tamamlanmış olması gerekir. Azure Storage 2011 08 18 sürüm hello bırakma hakkında daha fazla bilgi için bkz: [Microsoft Azure depolama hizmeti sürüm kaldırma güncelleştirmesi: uzantısı too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).

> [!IMPORTANT]
> Biz hello 30 Kasım 2016'den itibaren Azure yönetilen önbellek hizmeti ve Azure rol içi önbelleği için devre dışı bırakma Duyurusu. Bu devre dışı bırakma hazırlığı tooAzure Redis önbelleği geçirmek öneririz. Tarihler ve Geçiş Kılavuzu hakkında daha fazla bilgi için bkz: [Azure önbelleği tekliftir benim için en uygun?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Azure uygulama hizmeti araçları
Aşağıdaki öğelerindeki hello'hello Azure SDK 2.6 sürümünde güncelleştirildi.

* Azure yayımlama tooinclude Azure API uygulamaları dağıtım hedefi olarak geliştirilmiştir.
* API işlevleri tooenable API uygulaması oluşturma kullanıcılarla sağlama ve işlevsellik sağlama uygulamaları.
* Sunucu Gezgini değiştirilen tooreflect yeni uygulama hizmeti düğümünde, kaynak grubuna göre gruplandırılmış Web, mobil ve API apps ile.
* Azure API uygulama istemcisi hareketi eklenen toomost C# projeleri eklemek Swagger özellikli API kullanıcının Azure aboneliğindeki çalışan uygulamalar otomatik olarak oluşturulmasını etkinleştirir.
* API Apps araçları ve uygulama hizmeti düğümünde Sunucu Gezgini yalnızca Visual Studio 2013'te kullanılabilir. 

## <a name="azure-resource-manager-tools-updates"></a>Azure Kaynak Yöneticisi Araçları güncelleştirmeleri
Sanal makineler, ağ ve depolama için güncelleştirilmiş tooinclude şablonları Hello Azure Kaynak Yöneticisi Araçları olmuştur. Merhaba JSON düzenleme deneyimi güncelleştirilmiş tooinclude şablonları ve JSON parçacıkları hello özelliği tooedit hello şablonları için yeni bir anahat görünümü olmuştur. Visual Studio'dan dağıtılan şablonları toohello betik yapılan tüm değişiklikler Visual Studio tarafından kullanılacak şekilde hello project ile sağlanan bir PowerShell komut dosyasını kullanın.

## <a name="diagnostics-improvements-for-cloud-services"></a>Bulut Hizmetleri için tanılama geliştirmeleri
Azure SDK 2.6 hello Azure işlem öykünücüsü'nde tanılama günlüklerinin toplanması ve bunları aktarma için destek toodevelopment depolama geri getirir. Tüm tanılama günlükleri (uygulama izleme de dahil olmak üzere Windows (ETW) günlükleri, performans sayaçları, altyapı izleme günlükleri ve windows olay günlüklerini Olay günlükleri) Merhaba uygulaması hello öykünücüsünde çalışırken aktarılan toodevelopment oluşturulabilir Tanılama günlükleri, yerel makinede çalışıyor depolama tooverify. 

Merhaba tanılama depolama hesabı artık daha kolay toouse farklı tanılama depolama hesapları farklı ortamlar için yapmadan hello hizmet yapılandırma (.cscfg) dosyasında belirtilebilir. Azure SDK 2.4 ve Azure SDK 2.6 hello bağlantı dizesini nasıl çalıştığı arasında önemli bazı farklar vardır. Toouse hello tanılama depolama bağlantı dizesi ve nasıl projelerinizi etkiler nasıl görürüm hakkında daha fazla bilgi için [Azure bulut Hizmetleri için yapılandırma tanılama](http://go.microsoft.com/fwlink/?LinkID=532784).

## <a name="breaking-changes"></a>Yeni değişiklikler
### <a name="azure-resource-manager-tools"></a>Azure Kaynak Yöneticisi Araçları
* Merhaba **bulut dağıtım projeleri** proje türü Azure SDK 2.5 çok adlandırılmıştır hello kullanılabilir**Azure kaynak grubu**.
* **Bulut dağıtım projeleri** hello Azure SDK 2.5 oluşturulan projeleri türünü 2.6 içinde kullanılabilir ancak Visual Studio dağıtma hello şablondan başarısız olur. Ancak, PowerShell Betiği hello ile dağıtma işlemi, hala daha önce yaptığınız gibi çalışır.  Hakkında bilgi için toouse **bulut dağıtım projeleri** bu okuma 2.6 sürümündeki [sonrası](http://go.microsoft.com/fwlink/?LinkID=534086).

## <a name="known-issues"></a>Bilinen sorunlar
* Merhaba öykünücüsü tanılama günlükleri toplama 64-bit işletim sistemi gerektirir. Tanılama günlüklerini bir 32 bit işletim sisteminde çalışırken toplanmaz. Bu, herhangi bir öykünücü işlevsellik etkilemez. 
* Azure SDK 2.6 4/29/2015 tarihinde yayımlanan iki sorunları vardı: 
  
  * Azure SDK 2.6 hello makinede yüklendiğinde Evrensel uygulama Visual Studio 2015'te yüklenemedi.
  * Bir bulut hizmeti projesi hata ayıklama Visual Studio 2013 ve Visual Studio burada yanıt vermeyi ve selamlama iletisine "Yapılandırma tanılama öykünücüsü" içeren bir iletişim kutusu görüntülenirken çöküyor Visual Studio 2015 başarısız olur.
    
    Bir güncelleştirme tooAzure SDK 2.6 18/5/2015 tarihinde yayımlanmıştır. güncelleştirilmiş Merhaba, 2.6.30508.1601 sürümüdür; Yukarıda açıklanan iki sorunlar için düzeltmeler içerir. Merhaba hello yapısını tanımlayabilir SDK Denetim Masası -> Programlar ve Özellikler -> Microsoft Azure Araçları Microsoft Visual Studio 2013 için – v 2.6. Merhaba sürüm sütununda hello yapı numarası görüntüler.
    
    Merhaba sorunları yukarıda hala bakacak, hello en son sürümünü yükleyin hello için Azure 2.6 SDK [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) veya [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).

## <a name="see-also"></a>Ayrıca Bkz.
[Destek ve devre dışı bırakma bilgi hello .NET ve API'ler için Azure SDK'sı için](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

