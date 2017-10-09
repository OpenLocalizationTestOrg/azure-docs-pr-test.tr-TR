---
title: "aaaHow kullanıcı hesapları Azure API Management'te yönetme | Microsoft Docs"
description: "Bilgi nasıl toocreate veya davet kullanıcılar Azure API Management"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="7a3e2-103">Azure API Management'te nasıl toomanage kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="7a3e2-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="7a3e2-104">API Yönetimi'nde, geliştiricilerin hello API Management kullanarak kullanıma API'leri hello kullanıcılarının önerilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="7a3e2-105">Bu kılavuzu gösterir toohow toocreate ve davet geliştiriciler toouse hello API'leri ve ürünleri API Management örneğinizle kullanılabilir toothem olun.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="7a3e2-106">Merhaba programlı olarak kullanıcı hesaplarını yönetme hakkında daha fazla bilgi için bkz [kullanıcı varlığı](https://msdn.microsoft.com/library/azure/dn776330.aspx) hello belgelerinde [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) başvuru.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="7a3e2-107"><a name="create-developer"></a>Yeni bir geliştirici oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a3e2-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="7a3e2-108">toocreate yeni bir geliştirici tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="7a3e2-109">Bu toohello API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="7a3e2-110">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Yayımcı portalı][api-management-management-console]

<span data-ttu-id="7a3e2-112">Tıklatın **kullanıcılar** hello gelen **API Management** sol hello ve ardından menüsünde **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![Geliştirici oluşturma][api-management-create-developer]

<span data-ttu-id="7a3e2-114">Merhaba girin **e-posta**, **parola**, ve **adı** hello yeni Geliştirici ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![Geliştirici oluşturma][api-management-add-new-user]

<span data-ttu-id="7a3e2-116">Varsayılan olarak, yeni oluşturulan Geliştirici hesaplardır **etkin**ve hello ile ilişkili **geliştiriciler** grubu.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![Yeni Geliştirici][api-management-new-developer]

<span data-ttu-id="7a3e2-118">Geliştirici hesaplarının bir **etkin** durumu kullanılan tooaccess olabilir tüm abonelikleri sahiptirler hello API'leri.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="7a3e2-119">Ek gruplarla tooassociate yeni oluşturulan hello Geliştirici bkz [nasıl tooassociate geliştiricilere grupları][How tooassociate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="7a3e2-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="7a3e2-120"><a name="invite-developer"></a>Geliştirici davet et</span><span class="sxs-lookup"><span data-stu-id="7a3e2-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="7a3e2-121">tooinvite bir geliştirici tıklatın **kullanıcılar** hello gelen **API Management** sol hello ve ardından menüsünde **davet kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![Geliştirici davet et][api-management-invite-developer]

<span data-ttu-id="7a3e2-123">Merhaba Geliştirici Hello adını ve e-posta adresini girin ve tıklayın **davet**.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![Geliştirici davet et][api-management-invite-developer-window]

<span data-ttu-id="7a3e2-125">Bir onay iletisi görüntülenir, ancak bunlar hello daveti kabul ettikten sonra yeni davet hello Geliştirici hello listesi kadar görünmez.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![Onay davet et][api-management-invite-developer-confirmation]

<span data-ttu-id="7a3e2-127">Bir geliştirici davet e-posta toohello Geliştirici gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="7a3e2-128">Bu e-posta şablonu kullanılarak oluşturulan ve özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="7a3e2-129">Daha fazla bilgi için bkz: [yapılandırma e-posta şablonlarını][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="7a3e2-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="7a3e2-130">Merhaba daveti kabul edildikten sonra hello hesabı etkin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="7a3e2-131"><a name="block-developer"></a> Devre dışı bırakın veya bir geliştirici hesabını yeniden etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7a3e2-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="7a3e2-132">Varsayılan olarak, yeni oluşturulan veya davet edilen Geliştirici hesaplardır **etkin**.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="7a3e2-133">toodeactivate bir geliştirici hesabını tıklatın **blok**.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="7a3e2-134">tooreactivate engellenen Geliştirici hesabını tıklatın **etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="7a3e2-135">Engellenen Geliştirici hesabını değil hello Geliştirici portalına erişmek veya tüm API'leri çağırın.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="7a3e2-136">bir kullanıcı hesabı toodelete tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-136">toodelete a user account, click **Delete**.</span></span>

![Blok Geliştirici][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="7a3e2-138">Kullanıcı parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="7a3e2-138">Reset a user password</span></span>
<span data-ttu-id="7a3e2-139">tooreset hello bir kullanıcı hesabının parolasını hello hello hesabının adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![Parola sıfırlama][api-management-view-developer]

<span data-ttu-id="7a3e2-141">Tıklatın **parola sıfırlama** toosend bağlantı toohello kullanıcı tooreset parolalarını.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![Parola sıfırlama][api-management-reset-password]

<span data-ttu-id="7a3e2-143">bkz: hello kullanıcı hesapları ile tooprogrammatically çalışma [kullanıcı varlığı](https://msdn.microsoft.com/library/azure/dn776330.aspx) hello belgelerinde [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) başvuru.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="7a3e2-144">kullanıcı hesabı parolasını tooa belirli bir değer tooreset, kullanabileceğiniz hello [kullanıcıyı güncelleştirmek](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) işlemi ve hello istenen parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="7a3e2-145">Bekleyen doğrulama</span><span class="sxs-lookup"><span data-stu-id="7a3e2-145">Pending verification</span></span>
![Bekleyen doğrulama][api-management-pending-verification]

## <span data-ttu-id="7a3e2-147"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a3e2-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="7a3e2-148">Bir geliştirici hesabı oluşturulduktan sonra rolleriyle ilişkilendirmek ve tooproducts ve API'leri abone olun.</span><span class="sxs-lookup"><span data-stu-id="7a3e2-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="7a3e2-149">Daha fazla bilgi için bkz: [nasıl toocreate ve kullanım grupları][How toocreate and use groups].</span><span class="sxs-lookup"><span data-stu-id="7a3e2-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
