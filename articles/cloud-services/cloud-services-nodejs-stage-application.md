---
title: "aaaStage bir bulut hizmeti dağıtımı (Node.js) | Microsoft Docs"
description: "Öğrenin nasıl toodeploy ortamı, hazırlama, Azure uygulamanızı tooa tooa üretim ortamında sanal IP (VIP) takas kullanarak dağıtın."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>Bir Azure uygulamasında hazırlama
Paketlenmiş bir uygulama Azure toobe toohello üretim taşımadan önce test ortamında hazırlama dağıtılan toohello olabilir ortamı hangi hello uygulama hello Internet üzerinde erişilebilir. Azure tarafından oluşturulan karıştırılmış bir URL ile uygulama erişim hello hazırlanan yalnızca hazırlık ortamı hello üretim ortamı gibi tam olarak, olmasıdır. Uygulamanızın düzgün çalıştığını doğruladıktan sonra bir sanal IP (VIP) değiştirme gerçekleştirerek dağıtılan toohello üretim ortamına olabilir.

> [!NOTE]
> Merhaba bu makaledeki adımları yalnızca bir Azure bulut hizmeti olarak barındırılan toonode uygulamaları geçerlidir.
> 
> 

## <a name="step-1-stage-an-application"></a>1. adım: uygulamayı aşamalandırma
Bu görevi nasıl toostage kullanarak bir uygulama hello kapsayan **Microsoft Azure PowerShell**.

1. Hizmet yayımlama olduğunda, yalnızca hello geçir **-yuvası** hello parametresi **Publish-AzureServiceProject** cmdlet'i.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. Toohello üzerinde oturum [Klasik Azure portalı] seçip **bulut Hizmetleri**. Sonra Hello bulut hizmeti oluşturulur ve hello **hazırlama** sütun durumu çok güncelleştirilmiştir**çalıştıran**, hello hizmet adına tıklayın.
   
   ![portal çalışan bir hizmeti görüntüleme][cloud-service]
3. Select hello **Pano**ve ardından **hazırlama**.
   
   ![Bulut hizmeti Panosu][cloud-service-dashboard]
4. Not hello hello değerinde **Site URL'si** girişi toohello sağ. Merhaba DNS adı Azure oluşturulan karıştırılmış bir iç kimliğidir.
   
    ![site URL'si][cloud-service-staging-url]

Şimdi Merhaba uygulaması site URL'si hazırlama hello kullanarak ortam hazırlama hello içinde düzgün çalıştığını doğrulayabilirsiniz.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>2. adım: uygulama üretim yuvasıyla takas ediliyor VIP'ler tarafından yükseltme
Hazırlama ortamında bir uygulama yükseltilmiş sürümünü hello doğruladıktan sonra hızlı bir şekilde bu üretimde kullanılabilir takas tarafından yapabileceğiniz sanal IP (VIP) hello hazırlama ve üretim ortamlarını hello.

> [!NOTE]
> Bu adım zaten bir uygulama tooproduction dağıttıktan ve uygulamanın yükseltilmiş sürümünü hello hazırlanmış olduğunu varsayar.
> 
> 

1. Merhaba günlüğüne [Klasik Azure portalı], tıklatın **bulut Hizmetleri** ve hello hizmet adını seçin.
2. Merhaba gelen **Pano**seçin **hazırlama**ve ardından **takas** hello sayfanın hello sonundaki. Merhaba VIP takası iletişim kutusu açılır.
   
   ![VIP takas iletişim][vip-swap-dialog]
3. Merhaba bilgileri gözden geçirin ve ardından **Tamam**. Merhaba iki dağıtım dağıtım anahtarları tooproduction ve hello Üretim dağıtımı anahtarları toostaging hazırlama hello güncelleştirme başlar.

Başarıyla bir dağıtıma hazırlanan ve hazırlama hello dağıtımda olan VIP'ler takas Üretim dağıtımı yükseltildi.

## <a name="additional-resources"></a>Ek Kaynaklar
* [Nasıl tooDeploy hizmetini tooProduction VIP'ler takas Azure tarafından]

[Klasik Azure portalı]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[Nasıl tooDeploy hizmetini tooProduction VIP'ler takas Azure tarafından]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
