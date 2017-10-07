---
title: "Azure abonelikleri için faturalama veya kredi uyarılar aaaSet | Microsoft Docs"
description: "Fatura beklenmeyen durumları kaçınmak için nasıl uyarılarını Azure faturanızda ayarlayabileceğiniz açıklar."
keywords: "Kredi uyarı, fatura Uyarısı"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a>Microsoft Azure Abonelikleriniz için faturalama veya kredi uyarıları ayarlama
Bir Azure aboneliğine yönelik hello hesap yöneticisi değilseniz, hello Azure faturalama uyarı özelleştirilmiş toocreate faturalama izlemek ve fatura etkinlik, Azure hesaplarını yönetme yardımcı olacak uyarı hizmetini kullanabilirsiniz.

Tooenable gerekir böylece bu Önizleme'de, bu hello Önizleme özellikleri sayfasında ilk hizmetidir.

## <a name="set-hello-alert-threshold-and-email-recipients"></a>Merhaba uyarı eşiği ve e-posta alıcılarının ayarlama
1. Ziyaret [hello Önizleme özellikleri sayfasında](https://account.windowsazure.com/PreviewFeatures) ve etkinleştirme **faturalama uyarı hizmeti**.

1. Aboneliğiniz için hello faturalama hizmeti açık hello e-posta onayı aldıktan sonra ziyaret [hello abonelikler sayfası](https://account.windowsazure.com/Subscriptions) hello hesap portalındaki. Toomonitor istediğiniz ve ardından hello aboneliğe tıklayın **uyarıları**.

    ![Merhaba abonelikleri Azure hesap merkezi görünümünü ekran vurgulanmış uyarılar][Image1]

2. Bundan sonra öğesini **eklemek uyarı** toocreate, birinci. Farklı bir eşik ile abonelik başına beş faturalama uyarılarını toplam yukarı ve tootwo e-posta alıcılarını her uyarı için ayarlayabilirsiniz.

    ![Merhaba, uyarı ekleyebileceğiniz uyarılar görünümü ekran görüntüsü][Image2]

3. Bir uyarı eklediğinizde, harcama eşik seçin benzersiz bir ad verin ve hello uyarıları gönderildiği e-posta adresi seçin. Merhaba eşiği ayarlarken ya da seçebilirsiniz bir **faturalama toplamı** veya **kredi** hello gelen **için uyarı** listesi. Abonelik harcama hello eşiğini aştığında bir faturalama toplamı bir uyarı gönderilir. Parasal kredileriniz hello limitin altında bıraktığınızda kredi için bir uyarı gönderilir. Parasal kredileriniz genellikle tooFree deneme ve Visual Studio abonelikleri uygular.

    ![Alıcılar yapılandırabileceğiniz hello uyarı toplama görünümünün ekran görüntüsü][Image3]

Herhangi bir e-posta adresi Azure destekler ancak değil hello e-posta adresi çalıştığını doğrulamak, böylece yazım hataları denetleyin.

## <a name="check-on-your-alerts"></a>Uyarılarınızı üzerinde denetleyin
Uyarıları ayarlamak sonra hello hesap merkezi bunları listeler ve daha ayarlayabilirsiniz kaç gösterir. Her uyarı için hello tarih ve Saat Faturalama toplamı veya kredi için bir uyarı olup olmadığını gönderildiği ile ayarladığınız hello sınırı bakın. Merhaba tarih ve saat biçimi 24 saat Evrensel Saat koordinatı'nı (UTC) ve hello tarih yyyy-aa-gg biçiminde. Merhaba artı oturum hello listesi tooedit bir uyarıyla ilgili onu veya hello çöp can toodelete tıklatın.

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a>Kurumsal Anlaşma (Kurumsal Sözleşme) müşteriler için fatura uyarıları
EA müşteriler, bir kayıt kotaları harcama ayarlayarak altında her bölüm için uyarıları alabilirsiniz. Bkz: [departmanı harcama kotaları](https://ea.azure.com/helpdocs/departmentSpendingQuotas) hello EA portal tooget başlatılan içinde.

## <a name="learn-more-about-azure-cost-management"></a>Azure maliyeti yönetimi hakkında daha fazla bilgi edinin
- Hello kullanarak maliyetleri tahmin [fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/), [toplam sahip olma hesaplayıcı maliyeti](https://aka.ms/azure-tco-calculator), ve bir hizmet eklediğinizde.
- [Kullanım ve maliyetler Azure portalında düzenli olarak gözden](billing-getting-started.md#costs).
- Aç [Azure Advisor önerileri maliyet](../advisor/advisor-cost-recommendations.md).

toolearn daha, fazla [Azure maliyeti Yönetim Kılavuzu](billing-getting-started.md).

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
