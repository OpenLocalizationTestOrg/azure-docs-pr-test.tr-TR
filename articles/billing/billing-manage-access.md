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
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="137ce-102">Azure rol tabanlı erişim denetimini kullanarak erişim toobilling bilgilerini Yönet</span><span class="sxs-lookup"><span data-stu-id="137ce-102">Manage access toobilling information for Azure using role-based access control</span></span>

<span data-ttu-id="137ce-103">Kullanıcı rolleri tooyour abonelik aşağıdaki hello atayarak ekibinizin Azure faturalama bilgileri toomembers için erişim izni verebilir: Hesap Yöneticisi, Hizmet Yöneticisi, ortak yönetici, sahibi, katkıda bulunan, okuyucu ve fatura okuyucu.</span><span class="sxs-lookup"><span data-stu-id="137ce-103">You can grant access for Azure billing information toomembers of your team by assigning one of hello following user roles tooyour subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="137ce-104">Hello erişim toobilling bilgileri olurdu [Azure portal](https://portal.azure.com/), ve hello kullanabilirsiniz [faturalama API'leri](billing-usage-rate-card-overview.md) tooprogrammatically Al (kez seçti-gelen) faturaları ve kullanım ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="137ce-104">They would have access toobilling information in hello [Azure portal](https://portal.azure.com/), and they can use hello [Billing APIs](billing-usage-rate-card-overview.md) tooprogrammatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="137ce-105">Hakkında daha fazla bilgi için kimin verin rollerini ve hangi rollerin ne, bkz: [Azure RBAC rollerinde](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="137ce-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="137ce-106"><a name="opt-in"></a>Ek kullanıcılar tooaccess faturalar izin verme</span><span class="sxs-lookup"><span data-stu-id="137ce-106"><a name="opt-in"></a> Allowing additional users tooaccess invoices</span></span>

<span data-ttu-id="137ce-107">Merhaba Hesap Yöneticisi hello kullanarak etmeniz gerekir [Azure portal](https://portal.azure.com/) diğer kullanıcılar için ve API aracılığıyla erişim tooinvoices izin verir.</span><span class="sxs-lookup"><span data-stu-id="137ce-107">hello Account Administrator must opt in using hello [Azure portal](https://portal.azure.com/) allow access tooinvoices for other users and via API.</span></span>

1. <span data-ttu-id="137ce-108">Hesap Yöneticisi hello gibi hello aboneliğinizi seçin [abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="137ce-108">As hello Account Administrator, select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="137ce-109">Seçin **faturalar** ve ardından **erişim tooinvoices**.</span><span class="sxs-lookup"><span data-stu-id="137ce-109">Select **Invoices** and then **Access tooinvoices**.</span></span>

    ![Ekran toodelegate erişim nasıl tooinvoices gösterir](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="137ce-111">Kapatma **üzerinde** hello erişim ardından hello değişiklikleri, abonelik kapsamlı rolleri toodownload fatura tooallow kullanıcılar kaydederek.</span><span class="sxs-lookup"><span data-stu-id="137ce-111">Turn **On** hello access followed by saving hello changes, tooallow users in subscription scoped roles toodownload invoice.</span></span>

    ![Ekran görüntüsü, açık-kapalı toodelegate erişim tooinvoice gösterir.](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="137ce-113">Seçim hello abonelik toodownload PDF faturalarına hello Azure portal, Hizmet Yöneticisi, ortak yönetici, sahibi, katkıda bulunan, okuyucu ve faturalama okuyucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="137ce-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on hello subscription toodownload PDF invoices in hello Azure portal.</span></span> <span data-ttu-id="137ce-114">Ancak, faturalar aralık 2016'den daha eski kullanılabilir yalnızca toohello Hesap Yöneticisi şu an için değildir.</span><span class="sxs-lookup"><span data-stu-id="137ce-114">However, invoices older than December 2016 are available only toohello Account Administrator for now.</span></span>

<span data-ttu-id="137ce-115">Merhaba Hesap Yöneticisi, e-posta ile gönderilen toohave faturaları da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="137ce-115">hello Account Administrator can also configure toohave invoices sent via email.</span></span> <span data-ttu-id="137ce-116">toolearn daha, fazla [faturanızı e-posta ile almak](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="137ce-116">toolearn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-toohello-billing-reader-role"></a><span data-ttu-id="137ce-117">Kullanıcılar toohello faturalama okuyucu rolü ekleme</span><span class="sxs-lookup"><span data-stu-id="137ce-117">Adding users toohello Billing Reader role</span></span>

<span data-ttu-id="137ce-118">salt okunur erişim toosubscription faturalama bilgileri Azure portalında ve hiçbir erişim tooservices sanal makineleri ve depolama hesapları gibi Hello faturalama okuyucu rolüne sahiptir.</span><span class="sxs-lookup"><span data-stu-id="137ce-118">hello Billing Reader role has read-only access toosubscription billing information in Azure portal, and no access tooservices such as VMs and storage accounts.</span></span> <span data-ttu-id="137ce-119">Erişim toohello abonelik faturalama bilgileri, ancak özelliği toomanage Azure hello değil hello faturalama okuyucu rolü toosomeone atamak Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="137ce-119">Assign hello Billing Reader role toosomeone that needs access toohello subscription billing information but not hello ability toomanage Azure services.</span></span> <span data-ttu-id="137ce-120">Bu rol yalnızca Azure aboneliklerini finansal ve maliyet Yönetimi gerçekleştiren bir kuruluştaki kullanıcılar için uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="137ce-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="137ce-121">Hello aboneliğinizi seçin [abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="137ce-121">Select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="137ce-122">Seçin **erişim denetimi (IAM)** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="137ce-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Ekran görüntüsü IAM hello abonelik dikey penceresinde gösterir.](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="137ce-124">Seçin **faturalama okuyucu** hello içinde **bir rol seçin** sayfası.</span><span class="sxs-lookup"><span data-stu-id="137ce-124">Choose **Billing Reader** in hello **Select a role** page.</span></span>

    ![Ekran görüntüsü, faturalama okuyucu hello açılan görünümünde gösterir.](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="137ce-126">Tür hello tooinvite istediğiniz, ardından tıklatın hello kullanıcı için e-posta **Tamam** toosend hello davet.</span><span class="sxs-lookup"><span data-stu-id="137ce-126">Type hello email for hello user you want tooinvite, then click **OK** toosend hello invitation.</span></span>

    ![Birisi tooenter e-posta tooinvite gösteren ekran görüntüsü](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="137ce-128">Faturalama okuyucu olarak hello davet e-posta toolog'ndaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="137ce-128">Follow instructions in hello invite email toolog in as a Billing Reader.</span></span>

    ![Azure portalında ne faturalama okuyucu hello gösteren ekran görüntüsü görebilirsiniz](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="137ce-130">Merhaba faturalama okuyucu özellik Önizleme aşamasındadır ve kurumsal (EA) abonelikleri veya genel olmayan bulut henüz desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="137ce-130">hello Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-tooother-roles"></a><span data-ttu-id="137ce-131">Kullanıcıların tooother rol ekleme</span><span class="sxs-lookup"><span data-stu-id="137ce-131">Adding users tooother roles</span></span>

<span data-ttu-id="137ce-132">Sahibi veya katkıda, gibi diğer rolleri yalnızca fatura bilgilerini, ancak Azure hizmetlerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="137ce-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="137ce-133">Bu rolleri toomanage bkz [hello abonelik ya da hizmetleri yönetmek ekleme veya değiştirme Azure yönetici rolleri](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="137ce-133">toomanage these roles, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="137ce-134">Kimin hello erişebilir [hesap Merkezi'nde](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="137ce-134">Who can access hello [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="137ce-135">Yalnızca Hesap Yöneticisi hello toohello hesap Merkezi'nde oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="137ce-135">Only hello Account Administrator can log in toohello Account center.</span></span> <span data-ttu-id="137ce-136">Merhaba Hesap Yöneticisi hello yasal hello abonelik sahibi.</span><span class="sxs-lookup"><span data-stu-id="137ce-136">hello Account Administrator is hello legal owner of hello subscription.</span></span> <span data-ttu-id="137ce-137">Varsayılan olarak, kaydolup veya hello Azure aboneliği satın hello hello Hesap Yöneticisi sürece kişidir hello [abonelik sahipliği aktarılan](billing-subscription-transfer.md) toosomebody başka.</span><span class="sxs-lookup"><span data-stu-id="137ce-137">By default, hello person who signed up for or bought hello Azure subscription is hello Account Administrator, unless hello [subscription ownership was transferred](billing-subscription-transfer.md) toosomebody else.</span></span> <span data-ttu-id="137ce-138">Hello Hesap Yöneticisi abonelikleri oluşturma, aboneliklerinizi iptal edin, bir abonelik için faturalama adresinizi hello değiştirme ve hello abonelik için erişim ilkeleri yönetme.</span><span class="sxs-lookup"><span data-stu-id="137ce-138">hello Account Administrator can create subscriptions, cancel subscriptions, change hello billing address for a subscription, and manage access policies for hello subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="137ce-139">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="137ce-139">Need help?</span></span> <span data-ttu-id="137ce-140">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="137ce-140">Contact support.</span></span>

<span data-ttu-id="137ce-141">Hala daha fazla, sorularınız varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.</span><span class="sxs-lookup"><span data-stu-id="137ce-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
