---
title: "aaaAzure rol tabanlı erişim denetimi (RBAC) toocontrol erişim hakları toocreate ve Destek isteklerini yönetme | Microsoft Docs"
description: "Azure rol tabanlı erişim denetimi (RBAC) toocontrol hakları toocreate erişmek ve Destek isteklerini yönet"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="b31ca-103">Azure rol tabanlı erişim denetimi (RBAC) toocontrol hakları toocreate erişmek ve Destek isteklerini yönet</span><span class="sxs-lookup"><span data-stu-id="b31ca-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="b31ca-104">[Rol tabanlı erişim denetimi (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) Azure için ayrıntılı erişim yönetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b31ca-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="b31ca-105">Hello Azure portal, isteği oluşturmayı destekleyen [portal.azure.com](https://portal.azure.com), oluşturabilen ve Destek isteklerini yönet Azure RBAC modeli toodefine kullanır.</span><span class="sxs-lookup"><span data-stu-id="b31ca-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="b31ca-106">Merhaba uygun RBAC rolü toousers, grupları ve uygulamaları bir abonelik, kaynak grubu veya bir kaynak olabilen bir kapsamda belirli, atanarak erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="b31ca-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="b31ca-107">Bir örnek atalım: hello abonelik kapsamında Okuma izinlerine sahip bir kaynak grubu sahibi olarak Web siteleri, sanal makineler ve alt ağlar gibi hello kaynak grubundaki tüm hello kaynakları yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="b31ca-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="b31ca-108">Ancak, toocreate bir destek isteği hello sanal makine kaynağı karşı çalıştığınızda, aşağıdaki hata hello karşılaşırsanız</span><span class="sxs-lookup"><span data-stu-id="b31ca-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![Abonelik hatası](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="b31ca-110">Destek isteği Yönetimi ' nde yazma izni veya hello sahip bir rolü hello abonelik kapsam toobe mümkün toocreate Microsoft.Support/* eylemde desteklemek ve Destek isteklerini yönetin.</span><span class="sxs-lookup"><span data-stu-id="b31ca-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="b31ca-111">aşağıdaki makaleye bakın hello nasıl Azure'un özel rol tabanlı erişim denetimi (RBAC) toocreate kullanın ve Destek isteklerine hello Azure portalı Yönet açıklar.</span><span class="sxs-lookup"><span data-stu-id="b31ca-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b31ca-112">Başlarken</span><span class="sxs-lookup"><span data-stu-id="b31ca-112">Getting Started</span></span>

<span data-ttu-id="b31ca-113">Bir özel RBAC rolü hello abonelikte hello abonelik sahibi tarafından atanmış ise yukarıdaki hello örneği kullanarak, mümkün toocreate bir destek isteği bir kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="b31ca-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="b31ca-114">[Özel RBAC rolleri](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) Azure PowerShell, Azure komut satırı arabirimi (CLI) ve hello REST API'si kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="b31ca-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="b31ca-115">özel bir rol Hello Eylemler özelliği hello Azure işlemleri toowhich hello rol erişim verir belirtir.</span><span class="sxs-lookup"><span data-stu-id="b31ca-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="b31ca-116">toocreate destek isteği yönetimi için özel bir rol, hello rolü hello eylem Microsoft.Support/* sahip olması gerekir</span><span class="sxs-lookup"><span data-stu-id="b31ca-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="b31ca-117">Toocreate kullanın ve yönetmek için özel bir rol örneği destek istekleri.</span><span class="sxs-lookup"><span data-stu-id="b31ca-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="b31ca-118">Bu rolün "Destek isteği katkıda bulunan" adlı ve nasıl Biz bu makalede özel rol toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="b31ca-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="b31ca-119">Özetlenen hello adımları [bu videoyu](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn nasıl toocreate aboneliğiniz için özel bir rol.</span><span class="sxs-lookup"><span data-stu-id="b31ca-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="b31ca-120">Oluşturma ve Destek isteklerine hello Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="b31ca-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="b31ca-121">Bir örnek atalım – abonelik "Visual Studio MSDN aboneliğiniz." Merhaba sahibi olan</span><span class="sxs-lookup"><span data-stu-id="b31ca-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="b31ca-122">Joe kimin kaynak sahibi toosome bu Abonelikteki hello kaynak gruplarının olduğunu ve izin toohello abonelik okuma, eş ' dir.</span><span class="sxs-lookup"><span data-stu-id="b31ca-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="b31ca-123">Toogive erişim tooyour eş, Can, hello özelliği toocreate istiyor ve bu abonelik altında hello kaynaklar için destek biletlerini yönetme.</span><span class="sxs-lookup"><span data-stu-id="b31ca-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="b31ca-124">Merhaba ilk toogo toohello abonelik adımdır ve "Ayarlar" altında kullanıcıların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b31ca-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="b31ca-125">Merhaba kullanıcı abonelik hello üzerinde okuyucu erişimi olan Can'i tıklatın ve şimdi yeni bir özel rol toohim atayın.</span><span class="sxs-lookup"><span data-stu-id="b31ca-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![Rol Ekle](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="b31ca-127">"Ekle" hello "Kullanıcılar" dikey altında tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b31ca-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="b31ca-128">Merhaba özel rol "Destek isteği katkıda bulunan" Merhaba rollerinin listesinden seçin</span><span class="sxs-lookup"><span data-stu-id="b31ca-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![Destek katkıda bulunan rolü Ekle](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="b31ca-130">Merhaba rol adı seçtikten sonra "Kullanıcı Ekle" yi tıklatın ve hello Can'ın e-posta kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="b31ca-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="b31ca-131">"Seç"'i tıklatın</span><span class="sxs-lookup"><span data-stu-id="b31ca-131">Click "Select"</span></span>

    ![Kullanıcı ekle](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="b31ca-133">"Tamam" tooproceed tıklatın</span><span class="sxs-lookup"><span data-stu-id="b31ca-133">Click "Ok" tooproceed</span></span>

    ![Erişim Ekle](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="b31ca-135">Şimdi hello yeni eklenen özel rol "Destek isteği katkıda bulunan" Merhaba sahibi olduğunuz hello abonelik altında hello kullanıcıyla bakın</span><span class="sxs-lookup"><span data-stu-id="b31ca-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![Eklenen kullanıcı](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="b31ca-137">Joe hello Portalı'nda oturum açtığında, kendisinin eklendi hello abonelik toowhich görür.</span><span class="sxs-lookup"><span data-stu-id="b31ca-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="b31ca-138">Joe "Yeni destek isteği" hello "Yardım ve desteği" dikey penceresinden tıklar ve "Visual Studio Ultimate ile MSDN için" destek istekleri oluşturabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b31ca-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Yeni destek isteği](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="b31ca-140">"Tüm istekleri desteği" tıklatarak CAN Bu abonelik için oluşturduğunuz destek isteklerini hello listesini görebilir ![durum görünümü ayrıntıları](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="b31ca-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="b31ca-141">Destek isteği erişim hello Azure portal Kaldır</span><span class="sxs-lookup"><span data-stu-id="b31ca-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="b31ca-142">Yalnızca bu olası toogrant erişim tooa kullanıcı toocreate ve Destek isteklerini yönetme gibi olası tooremove erişim hello kullanıcı için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b31ca-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="b31ca-143">tooremove özelliği toocreate hello ve Destek isteklerini yönetin, toohello abonelik gidin, "Ayarlar"'ı tıklatın ve hello kullanıcıya (Bu örnekte, Can) tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b31ca-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="b31ca-144">Merhaba rol adı, "Destek isteği katkıda bulunan" sağ tıklatın ve "Kaldır"</span><span class="sxs-lookup"><span data-stu-id="b31ca-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![Destek isteği erişimi Kaldır](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="b31ca-146">Joe toohello Portalı'nda günlüğe kaydeder ve toocreate bir destek isteği çalışırsa, kendisinin aşağıdaki hata hello karşılaştığında</span><span class="sxs-lookup"><span data-stu-id="b31ca-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![Abonelik hata-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="b31ca-148">Joe herhangi göremezsiniz "Tüm istekleri desteği" tıklatır dağıtırken istekleri desteği</span><span class="sxs-lookup"><span data-stu-id="b31ca-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Servis Talebi Ayrıntıları görünümü-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
