---
title: "RemoteApp bulut koleksiyonu - oluşturma sorunlarını giderme | Microsoft Docs"
description: "RemoteApp bulut koleksiyonu oluşturma hatalarını giderme öğrenin"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>RemoteApp bulut koleksiyonu oluşturma sorunlarını giderme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Bulut koleksiyonu oluşturma sorun yaşıyorsanız, aşağıdaki bilgileri kontrol edin.

## <a name="your-image-is-invalid"></a>Görüntünüzü geçersiz
Koleksiyonunuz sağlamak Azure için beklenirken "GoldImageInvalid" gibi bir ileti görürseniz, şablon görüntünüzü karşılamıyor demektir [görüntü gereksinimleri tanımlanan](remoteapp-imagereqs.md). Bu nedenle, bu okuma Git [gereksinimleri](remoteapp-imagereqs.md)görüntünüzü düzeltin ve koleksiyonunuzu yeniden oluşturmayı deneyin.

## <a name="common-errors-seen-in-the-azure-management-portal"></a>Azure Yönetim Portalı'nda görülen yaygın hatalar
    DNS server could not be reached
    ProvisioningTimeout

Bulut koleksiyonları genellikle hata nedeniyle, oluşturma sırasında özel resimler kullanıyor.  Yukarıdaki hatalar birine bakın ve o koleksiyonu oluşturmak için özel bir görüntü kullanıyorsanız, lütfen şunları kontrol edin:

* Karşıya yüklediğiniz özel görüntü görüntü gereksinimleri karşıladığından emin olun.
* En sık sık karşılaşılan görüntünün doğru Sysprep uygulanmış olmadığını sorundur.  
* Doğrulama görüntü önyükleme Hyper-V içinde veya bir IAAS VM görüntüsünü kullanarak doğrudan Azure aboneliğinizde oluşturmayı deneyin. Önyükleme ve değil başlatmak VM başarısız olursa, bu genellikle özel görüntü düzgün hazırlanmadı belirtir.  Özel görüntü nasıl aşağıdaki yapılmış doğrulayın RemoteApp için bir özel şablon görüntüsü oluşturmak için

Aboneliğinizde yer alan Microsoft görüntülerden birini kullanıyorsanız, koleksiyonu yeniden oluşturmayı deneyin. Sorun devam ederse lütfen Microsoft Destek'e başvurun.

    PlatformImageTrialModeOnly

Bu hatayı görürseniz, bu genellikle anlamına gelir, ücretli bir hesabınız yükseltilmiş ancak yalnızca hizmetini deneme modunda geçerli bir Microsoft sağlanan görüntüsü kullanmaya çalışıyorsunuz. Bu durumda, bulut koleksiyonu yeniden oluşturun, ancak doğru görüntüyü belirttiğinizden emin olun deneyin.

