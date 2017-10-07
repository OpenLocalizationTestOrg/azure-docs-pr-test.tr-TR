---
title: "aaaTroubleshoot RemoteApp bulut koleksiyonu - oluşturma | Microsoft Docs"
description: "Tootroubleshoot RemoteApp bulut koleksiyonu oluşturma hataları nasıl öğrenin"
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
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>RemoteApp bulut koleksiyonu oluşturma sorunlarını giderme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Bulut koleksiyonu oluşturma sorun yaşıyorsanız, aşağıdaki bilgilerle hello denetleyin.

## <a name="your-image-is-invalid"></a>Görüntünüzü geçersiz
Koleksiyonunuz için Azure tooprovision beklenirken "GoldImageInvalid" gibi bir ileti görürseniz, şablon görüntünüzü hello karşılamıyor demektir [görüntü gereksinimleri tanımlanan](remoteapp-imagereqs.md). Bu nedenle, bu okuma Git [gereksinimleri](remoteapp-imagereqs.md)görüntünüzü düzeltin ve toocreate koleksiyonunuzu yeniden deneyin.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>Hello Azure Yönetim Portalı'nda görülen yaygın hatalar
    DNS server could not be reached
    ProvisioningTimeout

Bulut koleksiyonları genellikle hata nedeniyle, oluşturma sırasında özel resimler kullanıyor.  Hatalar yukarıda hello birine bakın ve bir özel görüntü toocreate hello koleksiyon kullanıyorsanız Lütfen şeyler aşağıdaki hello kontrol edin:

* Karşıya yüklediğiniz, hello özel görüntü görüntü gereksinimleri karşıladığından emin olun.
* En sık hello ortak, hello görüntü düzgün Sysprep uygulanmış değildi sorunudur.  
* Doğrulama hello görüntü önyükleme Hyper-V içinde veya bir IAAS VM hello görüntüsünü kullanarak doğrudan Azure aboneliğinizde oluşturmayı deneyin. Merhaba VM tooboot ve başlatılmamasına başarısız olursa, bu genellikle, hello özel görüntü düzgün hazırlanmadı belirtir.  Merhaba özel görüntü hello nasıl toocreate özel bir şablon görüntü RemoteApp için oluşturulmuş doğrulayın

Aboneliğinizde yer alan hello Microsoft görüntülerden birini kullanıyorsanız, toocreate hello koleksiyonu yeniden deneyin. Merhaba sorun devam ederse lütfen Microsoft Destek'e başvurun.

    PlatformImageTrialModeOnly

Bu hatayı görürseniz, bu genellikle anlamına gelir, yükseltilmiş tooa Ücretli hesap ancak toouse yalnızca hello deneme modunda hello hizmetinin geçerli bir Microsoft sağlanan görüntüsü çalışıyorsunuz. Bu durumda, toocreate bulut koleksiyonu yeniden deneyin, ancak emin toospecify hello doğru görüntüyü olabilir.

