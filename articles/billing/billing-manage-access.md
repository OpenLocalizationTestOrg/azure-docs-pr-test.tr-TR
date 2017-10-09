---
title: "rolleri kullanılarak faturalama aaaManage erişim tooAzure | Microsoft Docs"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>Azure rol tabanlı erişim denetimini kullanarak erişim toobilling bilgilerini Yönet

Kullanıcı rolleri tooyour abonelik aşağıdaki hello atayarak ekibinizin Azure faturalama bilgileri toomembers için erişim izni verebilir: Hesap Yöneticisi, Hizmet Yöneticisi, ortak yönetici, sahibi, katkıda bulunan, okuyucu ve fatura okuyucu. Hello erişim toobilling bilgileri olurdu [Azure portal](https://portal.azure.com/), ve hello kullanabilirsiniz [faturalama API'leri](billing-usage-rate-card-overview.md) tooprogrammatically Al (kez seçti-gelen) faturaları ve kullanım ayrıntıları. Hakkında daha fazla bilgi için kimin verin rollerini ve hangi rollerin ne, bkz: [Azure RBAC rollerinde](../active-directory/role-based-access-built-in-roles.md).

## <a name="opt-in"></a>Ek kullanıcılar tooaccess faturalar izin verme

Merhaba Hesap Yöneticisi hello kullanarak etmeniz gerekir [Azure portal](https://portal.azure.com/) diğer kullanıcılar için ve API aracılığıyla erişim tooinvoices izin verir.

1. Hesap Yöneticisi hello gibi hello aboneliğinizi seçin [abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) Azure portalında.

1. Seçin **faturalar** ve ardından **erişim tooinvoices**.

    ![Ekran toodelegate erişim nasıl tooinvoices gösterir](./media/billing-manage-access/AA-optin.png)

1. Kapatma **üzerinde** hello erişim ardından hello değişiklikleri, abonelik kapsamlı rolleri toodownload fatura tooallow kullanıcılar kaydederek.

    ![Ekran görüntüsü, açık-kapalı toodelegate erişim tooinvoice gösterir.](./media/billing-manage-access/AA-optinAllow.png)

Seçim hello abonelik toodownload PDF faturalarına hello Azure portal, Hizmet Yöneticisi, ortak yönetici, sahibi, katkıda bulunan, okuyucu ve faturalama okuyucu sağlar. Ancak, faturalar aralık 2016'den daha eski kullanılabilir yalnızca toohello Hesap Yöneticisi şu an için değildir.

Merhaba Hesap Yöneticisi, e-posta ile gönderilen toohave faturaları da yapılandırabilirsiniz. toolearn daha, fazla [faturanızı e-posta ile almak](billing-download-azure-invoice-daily-usage-date.md).

## <a name="adding-users-toohello-billing-reader-role"></a>Kullanıcılar toohello faturalama okuyucu rolü ekleme

salt okunur erişim toosubscription faturalama bilgileri Azure portalında ve hiçbir erişim tooservices sanal makineleri ve depolama hesapları gibi Hello faturalama okuyucu rolüne sahiptir. Erişim toohello abonelik faturalama bilgileri, ancak özelliği toomanage Azure hello değil hello faturalama okuyucu rolü toosomeone atamak Hizmetleri. Bu rol yalnızca Azure aboneliklerini finansal ve maliyet Yönetimi gerçekleştiren bir kuruluştaki kullanıcılar için uygun değildir.

1. Hello aboneliğinizi seçin [abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) Azure portalında.

1. Seçin **erişim denetimi (IAM)** ve ardından **Ekle**.

    ![Ekran görüntüsü IAM hello abonelik dikey penceresinde gösterir.](./media/billing-manage-access/select-iam.PNG)

1. Seçin **faturalama okuyucu** hello içinde **bir rol seçin** sayfası.

    ![Ekran görüntüsü, faturalama okuyucu hello açılan görünümünde gösterir.](./media/billing-manage-access/select-roles.PNG)

1. Tür hello tooinvite istediğiniz, ardından tıklatın hello kullanıcı için e-posta **Tamam** toosend hello davet.

    ![Birisi tooenter e-posta tooinvite gösteren ekran görüntüsü](./media/billing-manage-access/add-user.PNG)

1. Faturalama okuyucu olarak hello davet e-posta toolog'ndaki yönergeleri izleyin.

    ![Azure portalında ne faturalama okuyucu hello gösteren ekran görüntüsü görebilirsiniz](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> Merhaba faturalama okuyucu özellik Önizleme aşamasındadır ve kurumsal (EA) abonelikleri veya genel olmayan bulut henüz desteklemiyor.

## <a name="adding-users-tooother-roles"></a>Kullanıcıların tooother rol ekleme

Sahibi veya katkıda, gibi diğer rolleri yalnızca fatura bilgilerini, ancak Azure hizmetlerine erişebilir. Bu rolleri toomanage bkz [hello abonelik ya da hizmetleri yönetmek ekleme veya değiştirme Azure yönetici rolleri](billing-add-change-azure-subscription-administrator.md).

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>Kimin hello erişebilir [hesap Merkezi'nde](https://account.windowsazure.com)?

Yalnızca Hesap Yöneticisi hello toohello hesap Merkezi'nde oturum açabilir. Merhaba Hesap Yöneticisi hello yasal hello abonelik sahibi. Varsayılan olarak, kaydolup veya hello Azure aboneliği satın hello hello Hesap Yöneticisi sürece kişidir hello [abonelik sahipliği aktarılan](billing-subscription-transfer.md) toosomebody başka. Hello Hesap Yöneticisi abonelikleri oluşturma, aboneliklerinizi iptal edin, bir abonelik için faturalama adresinizi hello değiştirme ve hello abonelik için erişim ilkeleri yönetme.

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.

Hala daha fazla, sorularınız varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.
