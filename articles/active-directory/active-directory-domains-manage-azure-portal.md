---
title: "Azure Active Directory'de özel etki alanı adlarını yönetme | Microsoft Docs"
description: "Yönetim Kavramları ve Azure Active Directory'de bir etki alanı adı yönetmek için nasıl yapılır?"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 402c1be07b8ee885ee5341128fb3f419611b924d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="7a50e-103">Azure Active Directory'de özel etki alanı adlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="7a50e-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="7a50e-104">Bir etki alanı adı tanımlayıcının birçok dizin kaynaklar için önemli bir parçasıdır: kullanıcı, bir grup adresi parçası için bir kullanıcı adı veya e-posta adresi bir parçasıdır ve bir uygulama için uygulama kimliği URI'SİNİN parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="7a50e-104">A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application.</span></span> <span data-ttu-id="7a50e-105">Azure Active Directory'de (Azure AD) bir kaynak, kaynak içeren dizine ait olarak zaten doğrulanmış bir etki alanı adı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a50e-105">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified as owned by the directory that contains the resource.</span></span> <span data-ttu-id="7a50e-106">Yalnızca genel yönetici Azure AD etki alanı yönetimi görevlerini gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="7a50e-106">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="7a50e-107">Azure AD dizininiz için birincil etki alanı adı ayarlama</span><span class="sxs-lookup"><span data-stu-id="7a50e-107">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="7a50e-108">Dizininizi oluşturulduğunda 'contoso.onmicrosoft.com,' gibi bir ilk etki alanı adı da birincil etki alanı adıdır.</span><span class="sxs-lookup"><span data-stu-id="7a50e-108">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name.</span></span> <span data-ttu-id="7a50e-109">Yeni bir kullanıcı oluşturduğunuzda, birincil etki alanı varsayılan etki alanı için yeni bir kullanıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="7a50e-109">The primary domain is the default domain name for a new user when you create a new user.</span></span> <span data-ttu-id="7a50e-110">Bir birincil etki alanı adı ayarlama Portalı'nda yeni kullanıcılar oluşturmak bir yöneticinin işlemini kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="7a50e-110">Setting a primary domain name streamlines the process for an administrator to create new users in the portal.</span></span> <span data-ttu-id="7a50e-111">Birincil etki alanı adını değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="7a50e-111">To change the primary domain name:</span></span>

1. <span data-ttu-id="7a50e-112">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="7a50e-112">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="7a50e-113">Seçin **daha fazla hizmet**, girin **Azure Active Directory** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="7a50e-113">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
   
   ![Açılış kullanıcı yönetimi](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="7a50e-115">Üzerinde ***dizin adı*** dikey penceresinde, select **etki alanı adları**.</span><span class="sxs-lookup"><span data-stu-id="7a50e-115">On the ***directory-name*** blade, select **Domain names**.</span></span>
4. <span data-ttu-id="7a50e-116">Üzerinde  ***dizin adı* -etki alanı adları** dikey penceresinde istediğiniz etki alanı adı seçin, birincil etki alanı adı olun.</span><span class="sxs-lookup"><span data-stu-id="7a50e-116">On the ***directory-name* - Domain names** blade, select the domain name you would like to make the primary domain name.</span></span>
5. <span data-ttu-id="7a50e-117">Üzerinde ***etki alanı adı*** (yeni etki alanı adınızı başlığında sahip açan diğer bir deyişle, dikey), dikey penceresinde seçin **birincil olun** komutu.</span><span class="sxs-lookup"><span data-stu-id="7a50e-117">On the ***domain name*** blade (that is, the blade that opens that has your new domain name in the title), select the **Make primary** command.</span></span> <span data-ttu-id="7a50e-118">Sorulduğunda Seçiminizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="7a50e-118">Confirm your choice when prompted.</span></span>
   
   ![Bir etki alanı adı birincil olun](./media/active-directory-domains-manage-azure-portal/make-primary.png)

<span data-ttu-id="7a50e-120">Birleşik olmadığı herhangi doğrulanmış özel etki alanı olmasını dizininiz için birincil etki alanı adını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a50e-120">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="7a50e-121">Dizininiz için birincil etki alanı değiştirme var olan tüm kullanıcılar kullanıcı adlarını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="7a50e-121">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="7a50e-122">Azure AD ile özel etki alanı adlarını Ekle</span><span class="sxs-lookup"><span data-stu-id="7a50e-122">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="7a50e-123">Her Azure AD dizinine 900 özel etki alanı adları ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7a50e-123">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="7a50e-124">İşleme [bir ek özel etki alanı adı ekleyin](add-custom-domain.md) ilk özel etki alanı adı için aynıdır.</span><span class="sxs-lookup"><span data-stu-id="7a50e-124">The process to [add an additional custom domain name](add-custom-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="7a50e-125">Özel bir etki alanının alt etki alanlarını ekleme</span><span class="sxs-lookup"><span data-stu-id="7a50e-125">Add subdomains of a custom domain</span></span>
<span data-ttu-id="7a50e-126">'Europe.contoso.com' gibi bir üçüncü düzey etki alanı adı dizininize eklemek istiyorsanız, önce ekleyin ve contoso.com gibi ikinci düzey etki alanı doğrulamanız gerekir. Alt etki alanı otomatik olarak Azure AD tarafından doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="7a50e-126">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com. The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="7a50e-127">Yeni eklediğiniz alt etki alanı doğrulandı görmek için etki alanları listelenir tarayıcıda sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="7a50e-127">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="7a50e-128">Özel etki alanı adınız için DNS kayıt şirketi değiştirirseniz yapmanız gerekenler</span><span class="sxs-lookup"><span data-stu-id="7a50e-128">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="7a50e-129">Özel etki alanı adınız için DNS kayıt şirketi değiştirirseniz, Azure AD ile kendini kesinti olmadan ek yapılandırma görevleri ve özel etki alanı adınızı kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a50e-129">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="7a50e-130">Office 365, Intune veya Azure AD içinde özel etki alanı adları kullanan diğer hizmetler ile özel etki alanı adınızı kullanırsanız, bu hizmetlerin belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="7a50e-130">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="7a50e-131">Özel etki alanı silme</span><span class="sxs-lookup"><span data-stu-id="7a50e-131">Delete a custom domain name</span></span>
<span data-ttu-id="7a50e-132">Kuruluşunuz artık bu etki alanı adını kullanıyorsa ya da bu etki alanı adı başka bir Azure AD ile kullanmanız gerekiyorsa, özel etki alanı adı, Azure AD'den silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a50e-132">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="7a50e-133">Bir özel etki alanı adı silmek için önce dizininizdeki hiçbir kaynak etki alanı adını kullanan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="7a50e-133">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="7a50e-134">Bir etki alanı adı, varsa dizininizden silinemiyor:</span><span class="sxs-lookup"><span data-stu-id="7a50e-134">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="7a50e-135">Herhangi bir kullanıcı, bir kullanıcı adı, e-posta adresi veya etki alanı adını içeren proxy adresi vardır.</span><span class="sxs-lookup"><span data-stu-id="7a50e-135">Any user has a user name, email address, or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="7a50e-136">Herhangi bir grup, bir e-posta adresi veya etki alanı adını içeren proxy adresi vardır.</span><span class="sxs-lookup"><span data-stu-id="7a50e-136">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="7a50e-137">Azure ad herhangi bir uygulama, bir uygulama etki alanı adını içeren kimliği URI sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7a50e-137">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="7a50e-138">Değiştirme veya özel etki alanı adını silmeden önce herhangi bir kaynağa Azure AD dizininizi silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a50e-138">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="7a50e-139">Etki alanı adlarını yönetmek için PowerShell veya grafik API'sini kullanın</span><span class="sxs-lookup"><span data-stu-id="7a50e-139">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="7a50e-140">Azure Active Directory etki alanı adları için yönetim görevlerinin çoğunu Microsoft PowerShell veya program aracılığıyla Azure AD Graph API kullanarak tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7a50e-140">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="7a50e-141">Azure AD içinde etki alanı adlarını yönetmek için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="7a50e-141">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="7a50e-142">Azure AD içinde etki alanı adlarını yönetmek için grafik API'si kullanma</span><span class="sxs-lookup"><span data-stu-id="7a50e-142">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="7a50e-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a50e-143">Next steps</span></span>
* [<span data-ttu-id="7a50e-144">Özel etki alanı adlarını Ekle</span><span class="sxs-lookup"><span data-stu-id="7a50e-144">Add custom domain names</span></span>](add-custom-domain.md)

