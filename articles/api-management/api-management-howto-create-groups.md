---
title: "Azure API Management'te grupları kullanarak aaaManage Geliştirici hesapları | Microsoft Docs"
description: "Nasıl toomanage Geliştirici kullanarak hesapları öğrenin Azure API Management'te grupları"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="ae06d-103">Azure API Management'te nasıl toocreate ve kullanım grupları toomanage Geliştirici hesapları</span><span class="sxs-lookup"><span data-stu-id="ae06d-103">How toocreate and use groups toomanage developer accounts in Azure API Management</span></span>
<span data-ttu-id="ae06d-104">API Management'te, ürünlerin toodevelopers kullanılan toomanage hello görünürlüğünü gruplarıdır.</span><span class="sxs-lookup"><span data-stu-id="ae06d-104">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="ae06d-105">İlk yapılan görünür toogroups ürünleri olan ve sonra bu gruplara geliştiriciler görüntülemek ve hello gruplarıyla ilişkili toohello ürünleri abone.</span><span class="sxs-lookup"><span data-stu-id="ae06d-105">Products are first made visible toogroups, and then developers in those groups can view and subscribe toohello products that are associated with hello groups.</span></span> 

<span data-ttu-id="ae06d-106">API Management aşağıdaki sabit sistem gruplarına hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ae06d-106">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="ae06d-107">**Yöneticiler**: Azure aboneliği yöneticileri bu grubun üyesidir.</span><span class="sxs-lookup"><span data-stu-id="ae06d-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="ae06d-108">Yöneticiler API Management hizmet örneklerini yönetir API'leri, işlemleri ve geliştiriciler tarafından kullanılan ürünleri hello oluşturma.</span><span class="sxs-lookup"><span data-stu-id="ae06d-108">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="ae06d-109">**Geliştiriciler**: Kimliği doğrulanmış geliştirici portalı kullanıcıları bu gruba girer.</span><span class="sxs-lookup"><span data-stu-id="ae06d-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="ae06d-110">Geliştiriciler, Apı'lerinizi kullanan uygulamalar oluşturmak hello müşterilerdir.</span><span class="sxs-lookup"><span data-stu-id="ae06d-110">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="ae06d-111">Geliştiriciler erişim toohello Geliştirici Portalı verilir ve hello bir API'nin işlemlerini çağıran uygulamalar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ae06d-111">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="ae06d-112">**Konuklar** -kimliği doğrulanmamış Geliştirici portalı kullanıcıları, bu gruba bir API Management örneği sonbaharda hello Geliştirici portalını ziyaret eden olası müşteriler gibi.</span><span class="sxs-lookup"><span data-stu-id="ae06d-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="ae06d-113">Bunlar hello özelliği tooview API'leri gibi bazı salt okunur erişim hakkı verilebilir, ancak çağıramama.</span><span class="sxs-lookup"><span data-stu-id="ae06d-113">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="ae06d-114">Toplama toothese sistem gruplarında yöneticiler özel gruplar oluşturabilir veya [ilişkili Azure Active Directory kiracılarındaki dış grupları yararlanan][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="ae06d-114">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="ae06d-115">Özel ve dış gruplar tooAPI ürünleri erişmek ve geliştiricilere görünürlük vererek sistem grupları yanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ae06d-115">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="ae06d-116">Örneğin, özel bir grup oluşturmak için belirli bir ile ilişkili Geliştiriciler iş ortağı kuruluş ve erişim izni yalnızca ilgili API'leri içeren bir üründen toohello API'leri.</span><span class="sxs-lookup"><span data-stu-id="ae06d-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="ae06d-117">Bir kullanıcı birden fazla grubun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="ae06d-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="ae06d-118">Bu kılavuz, nasıl bir API Management örneğinin yöneticileri yeni gruplar eklemek ve ürünleri ve geliştiricilerin ilişkilendirmek gösterir.</span><span class="sxs-lookup"><span data-stu-id="ae06d-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="ae06d-119">Ayrıca toocreating ve hello yayımcı portalında gruplarını yönetme, oluşturabilir ve gruplarınızı hello API Management REST API kullanarak yönetmek [grup](https://msdn.microsoft.com/library/azure/dn776329.aspx) varlık.</span><span class="sxs-lookup"><span data-stu-id="ae06d-119">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="ae06d-120"><a name="create-group"></a>Bir grup oluşturun</span><span class="sxs-lookup"><span data-stu-id="ae06d-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="ae06d-121">toocreate yeni bir grubu tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="ae06d-121">toocreate a new group, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="ae06d-122">Bu toohello API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="ae06d-122">This takes you toohello API Management publisher portal.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="ae06d-124">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ae06d-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="ae06d-125">Tıklatın **grupları** hello gelen **API Management** sol hello ve ardından menüsünde **Grup Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ae06d-125">Click **Groups** from hello **API Management** menu on hello left, and then click **Add Group**.</span></span>

![Yeni Grup Ekle][api-management-add-group]

<span data-ttu-id="ae06d-127">Merhaba grubu ve isteğe bağlı bir açıklama için benzersiz bir ad girin ve tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ae06d-127">Enter a unique name for hello group and an optional description, and click **Save**.</span></span>

![Yeni Grup Ekle][api-management-add-group-window]

<span data-ttu-id="ae06d-129">Merhaba yeni Grup hello grupları sekmesini tooedit hello görüntülenen **adı** veya **açıklama** hello grubunun hello hello listedeki hello grup adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ae06d-129">hello new group is displayed in hello groups tab. tooedit hello **Name** or **Description** of hello group, click hello name of hello group in hello list.</span></span> <span data-ttu-id="ae06d-130">toodelete hello grubu tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="ae06d-130">toodelete hello group, click **Delete**.</span></span>

![Eklenen grubu][api-management-new-group]

<span data-ttu-id="ae06d-132">Merhaba grup oluşturulur, ürünleri ve geliştiriciler ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="ae06d-132">Now that hello group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="ae06d-133"><a name="associate-group-product"></a>Bir grup ürünü ile ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="ae06d-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="ae06d-134">tooassociate bir ürüne sahip bir grubu tıklatın **ürünleri** hello gelen **API Management** hello menüsünde sol ve ardından hello istenen ürün hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ae06d-134">tooassociate a group with a product, click **Products** from hello **API Management** menu on hello left, and then click hello name of hello desired product.</span></span>

![Görünürlüğü Ayarla][api-management-add-group-to-product]

<span data-ttu-id="ae06d-136">Select hello **görünürlük** tooadd sekmesinde ve grupları ve hello ürünün tooview hello geçerli grupları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ae06d-136">Select hello **Visibility** tab tooadd and remove groups, and tooview hello current groups for hello product.</span></span> <span data-ttu-id="ae06d-137">tooadd veya kaldırma grupları denetleyin veya grupları ve tıklatın hello istenen için hello onay kutusunun işaretini kaldırın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ae06d-137">tooadd or remove groups, check or uncheck hello checkboxes for hello desired groups and click **Save**.</span></span>

![Görünürlüğü Ayarla][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="ae06d-139">bkz: tooadd Azure Active Directory grupları [nasıl tooauthorize Geliştirici kullanarak hesapları Azure API Management'te Azure Active Directory](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="ae06d-139">tooadd Azure Active Directory groups, see [How tooauthorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="ae06d-140">Merhaba tooconfigure gruplarından **görünürlük** bir ürün sekmesini tıklatın, **grupları yönet**.</span><span class="sxs-lookup"><span data-stu-id="ae06d-140">tooconfigure groups from hello **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="ae06d-141">Bir ürün grubu ile ilişkili olduğunda, o gruptaki geliştiriciler görüntüleyebilir ve toohello ürün abone.</span><span class="sxs-lookup"><span data-stu-id="ae06d-141">Once a product is associated with a group, developers in that group can view and subscribe toohello product.</span></span>

## <span data-ttu-id="ae06d-142"><a name="associate-group-developer"></a>Grupları geliştiricilerle ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="ae06d-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="ae06d-143">Geliştiriciler ile tooassociate gruplar **kullanıcılar** hello gelen **API Management** sol hello ve hello geliştiriciler yanındaki kutuyu hello menüsünden istediğiniz tooassociate sahip bir grup.</span><span class="sxs-lookup"><span data-stu-id="ae06d-143">tooassociate groups with developers, click **Users** from hello **API Management** menu on hello left, and then check hello box beside hello developers you wish tooassociate with a group.</span></span>

![Geliştirici toogroup Ekle][api-management-add-group-to-developer]

<span data-ttu-id="ae06d-145">Geliştiriciler denetlenir Hello istenen sonra hello istenen hello grubunda tıklayın **tooGroup ekleme** açılır.</span><span class="sxs-lookup"><span data-stu-id="ae06d-145">Once hello desired developers are checked, click hello desired group in hello **Add tooGroup** drop-down.</span></span> <span data-ttu-id="ae06d-146">Geliştiriciler kaldırılabilir gruplarından hello kullanarak **grubundan** açılır.</span><span class="sxs-lookup"><span data-stu-id="ae06d-146">Developers can be removed from groups by using hello **Remove from Group** drop-down.</span></span> 

![Geliştiriciler][api-management-add-group-to-developer-saved]

<span data-ttu-id="ae06d-148">Merhaba ilişkilendirme hello Geliştirici ve hello grubu arasında eklendikten sonra hello görüntüleyebilirsiniz **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ae06d-148">Once hello association is added between hello developer and hello group, you can view it in hello **Users** tab.</span></span>

## <span data-ttu-id="ae06d-149"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ae06d-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="ae06d-150">Bir geliştirici tooa grubuna eklendikten sonra görüntüleyin ve bu grupla ilişkili toohello ürünleri abone olun.</span><span class="sxs-lookup"><span data-stu-id="ae06d-150">Once a developer is added tooa group, they can view and subscribe toohello products associated with that group.</span></span> <span data-ttu-id="ae06d-151">Daha fazla bilgi için bkz: [oluşturma ve Azure API Management'te bir ürün yayımlama][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="ae06d-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="ae06d-152">Ayrıca toocreating ve hello yayımcı portalında gruplarını yönetme, oluşturabilir ve gruplarınızı hello API Management REST API kullanarak yönetmek [grup](https://msdn.microsoft.com/library/azure/dn776329.aspx) varlık.</span><span class="sxs-lookup"><span data-stu-id="ae06d-152">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
