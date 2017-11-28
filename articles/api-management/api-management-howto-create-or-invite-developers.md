---
title: "Nasıl kullanıcı hesaplarını Azure API Management'te yönetme | Microsoft Docs"
description: "Oluşturma ve Azure API Management'te kullanıcıları davet öğrenin"
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
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="e5048-103">Kullanıcı hesapları Azure API Management'te yönetme</span><span class="sxs-lookup"><span data-stu-id="e5048-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="e5048-104">API Yönetimi'nde, geliştiriciler API Management kullanarak kullanıma API'leri kullanıcılardır.</span><span class="sxs-lookup"><span data-stu-id="e5048-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="e5048-105">Bu kılavuz, API'ları ve ürünlerini kullanmak için için nasıl oluşturulacağını ve geliştiricilerin davet gösterir, API Management örneği ile kendileri için kullanılabilir hale.</span><span class="sxs-lookup"><span data-stu-id="e5048-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="e5048-106">Kullanıcı hesaplarını program aracılığıyla yönetme hakkında daha fazla bilgi için bkz: [kullanıcı varlığı](https://msdn.microsoft.com/library/azure/dn776330.aspx) belgelerinde [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) başvuru.</span><span class="sxs-lookup"><span data-stu-id="e5048-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="e5048-107"><a name="create-developer"></a>Yeni bir geliştirici oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5048-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="e5048-108">Yeni bir geliştirici oluşturmak için tıklatın **yayımcı portalına** API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="e5048-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="e5048-109">Bu sizi API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="e5048-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="e5048-110">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="e5048-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Yayımcı portalı][api-management-management-console]

<span data-ttu-id="e5048-112">Tıklatın **kullanıcılar** gelen **API Management** sol menüsünde ve ardından **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="e5048-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Geliştirici oluşturma][api-management-create-developer]

<span data-ttu-id="e5048-114">Girin **e-posta**, **parola**, ve **adı** tıklatın ve yeni geliştirici için **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e5048-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Geliştirici oluşturma][api-management-add-new-user]

<span data-ttu-id="e5048-116">Varsayılan olarak, yeni oluşturulan Geliştirici hesaplardır **etkin**ve ilişkili **geliştiriciler** grubu.</span><span class="sxs-lookup"><span data-stu-id="e5048-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![Yeni Geliştirici][api-management-new-developer]

<span data-ttu-id="e5048-118">Geliştirici hesaplarının bir **etkin** durumu, tüm abonelikleri sahiptirler API'leri erişmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e5048-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="e5048-119">Yeni oluşturulan Geliştirici ek gruplarıyla ilişkilendirmek için bkz: [grupları geliştiricilerle ilişkilendirme][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="e5048-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="e5048-120"><a name="invite-developer"></a>Geliştirici davet et</span><span class="sxs-lookup"><span data-stu-id="e5048-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="e5048-121">Bir geliştirici davet etmek için tıklatın **kullanıcılar** gelen **API Management** sol menüsünde ve ardından **davet kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="e5048-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Geliştirici davet et][api-management-invite-developer]

<span data-ttu-id="e5048-123">Geliştirici adını ve e-posta adresini girin ve tıklayın **davet**.</span><span class="sxs-lookup"><span data-stu-id="e5048-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Geliştirici davet et][api-management-invite-developer-window]

<span data-ttu-id="e5048-125">Bir onay iletisi görüntülenir, fakat daveti kabul ettikten sonra yeni davet edilen Geliştirici kadar listesinde görünmez.</span><span class="sxs-lookup"><span data-stu-id="e5048-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Onay davet et][api-management-invite-developer-confirmation]

<span data-ttu-id="e5048-127">Bir geliştirici davet, geliştiriciler için bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="e5048-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="e5048-128">Bu e-posta şablonu kullanılarak oluşturulan ve özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e5048-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="e5048-129">Daha fazla bilgi için bkz: [yapılandırma e-posta şablonlarını][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="e5048-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="e5048-130">Daveti kabul edildikten sonra hesap etkin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="e5048-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="e5048-131"><a name="block-developer"></a> Devre dışı bırakın veya bir geliştirici hesabını yeniden etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e5048-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="e5048-132">Varsayılan olarak, yeni oluşturulan veya davet edilen Geliştirici hesaplardır **etkin**.</span><span class="sxs-lookup"><span data-stu-id="e5048-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="e5048-133">Bir geliştirici hesabını devre dışı bırakmak için tıklatın **blok**.</span><span class="sxs-lookup"><span data-stu-id="e5048-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="e5048-134">Engellenen Geliştirici hesabı yeniden etkinleştirmek için tıklatın **etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e5048-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="e5048-135">Engellenen Geliştirici hesabını değil Geliştirici portalına erişmek veya tüm API'leri çağırın.</span><span class="sxs-lookup"><span data-stu-id="e5048-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="e5048-136">Bir kullanıcı hesabını silmek için tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e5048-136">To delete a user account, click **Delete**.</span></span>

![Blok Geliştirici][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="e5048-138">Kullanıcı parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="e5048-138">Reset a user password</span></span>
<span data-ttu-id="e5048-139">Bir kullanıcı hesabının parolasını sıfırlamak için hesap adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5048-139">To reset the password for a user account, click the name of the account.</span></span>

![Parola sıfırlama][api-management-view-developer]

<span data-ttu-id="e5048-141">Tıklatın **parola sıfırlama** kullanıcının parolasını sıfırlamak için bir bağlantı göndermek için.</span><span class="sxs-lookup"><span data-stu-id="e5048-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![Parola sıfırlama][api-management-reset-password]

<span data-ttu-id="e5048-143">Program aracılığıyla kullanıcı hesapları ile çalışmak için bkz: [kullanıcı varlığı](https://msdn.microsoft.com/library/azure/dn776330.aspx) belgelerinde [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) başvuru.</span><span class="sxs-lookup"><span data-stu-id="e5048-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="e5048-144">Belirli bir değere bir kullanıcı hesabı parolasını sıfırlamak için kullanabileceğiniz [kullanıcıyı güncelleştirmek](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) işlemi ve istenilen parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="e5048-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="e5048-145">Bekleyen doğrulama</span><span class="sxs-lookup"><span data-stu-id="e5048-145">Pending verification</span></span>
![Bekleyen doğrulama][api-management-pending-verification]

## <span data-ttu-id="e5048-147"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5048-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="e5048-148">Bir geliştirici hesabı oluşturulduktan sonra rolleriyle ilişkilendirmek ve ürünleri ve API'ler için abone olun.</span><span class="sxs-lookup"><span data-stu-id="e5048-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="e5048-149">Daha fazla bilgi için bkz: [grupları oluşturma ve kullanma konusunda][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="e5048-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

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
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
