---
title: Azure RemoteApp en iyi uygulamalar | Microsoft Docs
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
ms.openlocfilehash: ab9c2dafc622e9b6f3bcd2767218cdc03e844847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Azure Remoteapp'in yapılandırılması ve kullanılması için en iyi uygulamalar
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) okuyun.
> 
> 

Aşağıdaki bilgiler yapılandırmanıza ve Azure RemoteApp üretken kullanmanıza yardımcı olabilir.

## <a name="connectivity"></a>Bağlantı
* Her zaman en son istemci sürümünü kullanın. Eski istemciler kullanarak bağlantı sorunları ve diğer düşürülmüş deneyimleri neden olabilir. Cihazınız için otomatik uygulama güncelleştirmeleri etkinleştirme son istemci her zaman yüklü olduğunu güvence altına alır.
* Her zaman kullanabileceğiniz en kararlı ve güvenilir Internet bağlantısı kullanır.  
* En iyi bağlantı performans için yalnızca desteklenen proxy bağlantıları kullanın.  SOCKS proxy desteklenmiyor.

## <a name="applications"></a>Uygulamalar
* Kaydetme ve uygulama ile işiniz bittiğinde RemoteApp uygulamaları kapatın. Uygulama kapama değil veri kaybına neden olabilir.
* Özel uygulamalar Azure Remoteapp'te kullanmadan önce doğrulayın. Bu, çoklu oturum platformu üzerinde çalışır ve bellek ve aynı koleksiyondaki başka bir kullanıcı tamamen Kaynaksız bırakabilir CPU gibi gereksiz kaynaklarını tüketebilir yok emin olmayı içerir. Bilgi için indirebilir ve gözden [Uzak Masaüstü Hizmetleri için uygulama uyumluluk en iyi uygulamaları](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Yapılandırması ve Yönetimi
* Şablon görüntüleri gerektiği gibi yazılım güncelleştirmeleri ve diğer önemli düzeltmelerin yüklenmesi güncel tutun. Bu, Azure RemoteApp otomatik-kapasitenizi karşılayacak şekilde ölçekler gibi her bir örnek düzeltme sağlar.  
* Active Directory Federasyon Hizmetleri (AD FS) dağıtımınızı güvenli ve güvenilir olduğundan emin olun. Aksi takdirde istemci kimlik doğrulama, kullanıcıların Azure RemoteApp erişmesini önleme başarısız olabilir.
* Şablon görüntüleri yüklü uygulamalar, roller veya özellikler durum bilgisiz gibi yapılandırın. Bir RemoteApp hizmetinde kalıcı bir durumda olan sanal makinelerin tüm örneklerinde güvenmemelisiniz.
  * Şirket içi dosya paylaşımları veya OneDrive gibi kullanıcı profilleri veya hizmet için dış diğer depolama konumları tüm kullanıcı verileri depolar.
  * Şirket içi dosya paylaşımları veya OneDrive gibi paylaşılan veri depolama konumları hizmetine dış depolayın.
  * Şablon görüntüsü yerine bir hizmette tek tek sanal makinelerde hiçbir sistem genelindeki ayarları yapılandırın.
  * Otomatik yazılım güncelleştirmeleri yayımlanan uygulamalar için devre dışı bırak - bunun yerine bunları el ile şablon görüntüye ve şablonu dağıtmadan önce bunları test.

