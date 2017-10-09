---
title: aaaAzure RemoteApp en iyi uygulamalar | Microsoft Docs
description: "Azure Remoteapp'in yapılandırılması ve kullanılması için en iyi uygulamalar."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Azure Remoteapp'in yapılandırılması ve kullanılması için en iyi uygulamalar
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) Ayrıntılar için.
> 
> 

Aşağıdaki bilgilerle hello yapılandırmanıza ve Azure RemoteApp üretken kullanmanıza yardımcı olabilir.

## <a name="connectivity"></a>Bağlantı
* Her zaman hello son istemci sürümünü kullanın. Eski istemciler kullanarak bağlantı sorunları ve diğer düşürülmüş deneyimleri neden olabilir. Cihazınız için otomatik uygulama güncelleştirmeleri etkinleştirme hello son istemci her zaman yüklü güvence altına alır.
* Her zaman hello en kararlı ve güvenilir Internet bağlantısı kullanılabilir tooyou kullanın.  
* En iyi bağlantı performans için yalnızca desteklenen proxy bağlantıları kullanın.  Merhaba SOCKS proxy desteklenmiyor.

## <a name="applications"></a>Uygulamalar
* Kaydedin ve hello uygulamayla bittiğinde RemoteApp uygulamaları kapatın. Merhaba uygulaması kapama değil veri kaybına neden olabilir.
* Özel uygulamalar Azure Remoteapp'te kullanmadan önce doğrulayın. Bu bir çoklu oturum platformda çalışmak ve bellek ve başka bir kullanıcı hello tamamen Kaynaksız bırakabilir CPU gibi gereksiz kaynaklarını tüketebilir yok emin olmayı içerir aynı koleksiyonu. Bilgi için indirme ve hello gözden [Uzak Masaüstü Hizmetleri için uygulama uyumluluk en iyi uygulamaları](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Yapılandırması ve Yönetimi
* Şablon görüntülerinizi gerektiği gibi yazılım güncelleştirmeleri ve diğer önemli düzeltmelerin yüklenmesi toodate yukarı tutun. Bu, Azure RemoteApp otomatik-toomeet ölçekler gibi her bir örnek kapasitenizi düzeltme sağlar.  
* Active Directory Federasyon Hizmetleri (AD FS) dağıtımınızı güvenli ve güvenilir olduğundan emin olun. Aksi takdirde istemci kimlik doğrulama, kullanıcıların Azure RemoteApp erişmesini önleme başarısız olabilir.
* Şablon görüntüleri yüklü uygulamalar, roller veya özellikler durum bilgisiz gibi yapılandırın. Merhaba sanal makinelerin durumunu sürekli bir RemoteApp Hizmeti'nin'ın tüm örneklerini dayanarak doğrulamamalısınız.
  * Şirket içi dosya paylaşımları veya OneDrive gibi kullanıcı profilleri veya diğer depolama konumları dış toohello hizmeti tüm kullanıcı verileri depolar.
  * Şirket içi dosya paylaşımları veya OneDrive gibi paylaşılan veri depolama konumları dış toohello Hizmeti'nde depolayabilirsiniz.
  * Merhaba şablon görüntüsü yerine bir hizmette tek tek sanal makinelerde hiçbir sistem genelindeki ayarları yapılandırın.
  * Otomatik yazılım güncelleştirmeleri yayımlanan uygulamalar için devre dışı bırak - bunun yerine toohello şablon görüntüsü'bunları el ile geçerli ve hello şablondan dağıtmadan önce bunları test.

