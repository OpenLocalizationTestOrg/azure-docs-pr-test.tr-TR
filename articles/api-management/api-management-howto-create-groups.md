---
title: "Azure API Management'te grupları kullanılarak Geliştirici hesaplarını yönetme | Microsoft Docs"
description: "Geliştirici hesaplarının Azure API Management'te grupları kullanarak yönetmeyi öğrenin"
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
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="ebb0b-103">Oluşturma ve Azure API Management'ta Geliştirici hesaplarını yönetmek için grupları kullanma</span><span class="sxs-lookup"><span data-stu-id="ebb0b-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="ebb0b-104">API Management’te, ürünlerin geliştiricilere görünürlüğünü yönetmek için gruplar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="ebb0b-105">Ürünler ilk gruplar tarafından görünür yapılır ve sonra bu gruplara geliştiriciler görüntülemek ve gruplarıyla ilişkili ürünlere abone.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="ebb0b-106">API Management aşağıdaki sabit sistem gruplarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="ebb0b-107">**Yöneticiler**: Azure aboneliği yöneticileri bu grubun üyesidir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="ebb0b-108">Yöneticiler, geliştiriciler tarafından kullanılan API’leri, işlemleri ve ürünleri oluşturarak API Management hizmet örneklerini yönetir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="ebb0b-109">**Geliştiriciler**: Kimliği doğrulanmış geliştirici portalı kullanıcıları bu gruba girer.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="ebb0b-110">Geliştiriciler, API'lerinizi kullanarak uygulama oluşturan müşterilerdir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="ebb0b-111">Geliştiriciler, geliştirici portalına erişim iznine sahiptir ve bir API’nin işlemlerini çağıran uygulamalar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="ebb0b-112">**Konuklar**: Kimliği doğrulanmamış geliştirici portalı kullanıcıları (bir API Management örneğinin geliştirici portalını ziyaret eden olası müşteriler gibi) bu gruba girer.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="ebb0b-113">Bunlara API’leri görüntüleyebilme ancak çağıramama gibi bazı salt okunur erişimler verilebilir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="ebb0b-114">Bu sistem gruplarına ek olarak, yöneticiler özel gruplar oluşturabilir veya [ilişkili Azure Active Directory kiracılarındaki dış grupları yararlanan][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="ebb0b-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="ebb0b-115">Özel ve dış gruplar, geliştiricilere görünürlük ve API ürünlerine erişim sağlayan sistem gruplarıyla birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="ebb0b-116">Örneğin, belirli bir iş ortağı kuruluşla ilişkili geliştiriciler için özel bir grup oluşturabilir ve bunlara yalnızca ilgili API'leri içeren bir üründen API'lere erişim izni verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="ebb0b-117">Bir kullanıcı birden fazla grubun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="ebb0b-118">Bu kılavuz, nasıl bir API Management örneğinin yöneticileri yeni gruplar eklemek ve ürünleri ve geliştiricilerin ilişkilendirmek gösterir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="ebb0b-119">Grup oluşturma ve yayımcı portalında yönetme ek olarak, oluşturmak ve gruplarınızı API Management REST API kullanarak yönetmek [grup](https://msdn.microsoft.com/library/azure/dn776329.aspx) varlık.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="ebb0b-120"><a name="create-group"></a>Bir grup oluşturun</span><span class="sxs-lookup"><span data-stu-id="ebb0b-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="ebb0b-121">Yeni bir grup oluşturmak için tıklatın **yayımcı portalına** API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="ebb0b-122">Bu sizi API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-122">This takes you to the API Management publisher portal.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="ebb0b-124">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="ebb0b-125">Tıklatın **grupları** gelen **API Management** sol menüsünde ve ardından **Grup Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Yeni Grup Ekle][api-management-add-group]

<span data-ttu-id="ebb0b-127">Grup ve isteğe bağlı bir açıklama için benzersiz bir ad girin ve tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Yeni Grup Ekle][api-management-add-group-window]

<span data-ttu-id="ebb0b-129">Yeni Grup grupları sekmesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="ebb0b-130">Düzenlenecek **adı** veya **açıklama** grubunu, listedeki grup adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="ebb0b-131">Grubunu silmek için tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-131">To delete the group, click **Delete**.</span></span>

![Eklenen grubu][api-management-new-group]

<span data-ttu-id="ebb0b-133">Grubu oluşturulan, ürünleri ve geliştiriciler ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="ebb0b-134"><a name="associate-group-product"></a>Bir grup ürünü ile ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="ebb0b-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="ebb0b-135">Bir grup olan bir ürün ilişkilendirmek için tıklatın **ürünleri** gelen **API Management** sol menüsünde ve istenen ürün adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Görünürlüğü Ayarla][api-management-add-group-to-product]

<span data-ttu-id="ebb0b-137">Seçin **görünürlük** sekme ekleme ve grupları kaldırmak için ve ürün için geçerli gruplarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="ebb0b-138">Grupları ekleyebilir veya kaldırabilirsiniz için denetleyin veya istenen grupları için onay kutusunun işaretini kaldırın ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Görünürlüğü Ayarla][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="ebb0b-140">Azure Active Directory grupları eklemek için bkz: [Azure API Management'te Azure Active Directory'yi kullanarak Geliştirici hesaplarını yetkilendirmede nasıl](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="ebb0b-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="ebb0b-141">Gruplardan yapılandırmak için **görünürlük** bir ürün sekmesini tıklatın, **grupları yönet**.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="ebb0b-142">Bir ürün grubu ile ilişkili olduğunda, o gruptaki geliştiriciler görüntüleyebilir ve ürüne abone.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="ebb0b-143"><a name="associate-group-developer"></a>Grupları geliştiricilerle ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="ebb0b-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="ebb0b-144">Grupları geliştiricilerle ilişkilendirme için tıklatın **kullanıcılar** gelen **API Management** sol menüsünde ve bir grubu ile ilişkilendirmek istediğiniz geliştiriciler yanındaki kutuyu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Geliştirici grubuna Ekle][api-management-add-group-to-developer]

<span data-ttu-id="ebb0b-146">İstenen geliştiriciler işaretlendiğinde, istenen grubunda tıklatın **gruba ekleyin** açılır.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="ebb0b-147">Geliştiriciler kaldırılabilir gruplarından kullanarak **grubundan** açılır.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![Geliştiriciler][api-management-add-group-to-developer-saved]

<span data-ttu-id="ebb0b-149">Geliştirici ve grubu ilişki eklendikten sonra içinde görüntüleyebilirsiniz **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="ebb0b-150"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ebb0b-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="ebb0b-151">Bir geliştirici bir gruba eklendikten sonra görüntüleyin ve bu grupla ilişkili ürünlere abone.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="ebb0b-152">Daha fazla bilgi için bkz: [oluşturma ve Azure API Management'te bir ürün yayımlama][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="ebb0b-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="ebb0b-153">Grup oluşturma ve yayımcı portalında yönetme ek olarak, oluşturmak ve gruplarınızı API Management REST API kullanarak yönetmek [grup](https://msdn.microsoft.com/library/azure/dn776329.aspx) varlık.</span><span class="sxs-lookup"><span data-stu-id="ebb0b-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
