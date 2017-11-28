---
title: "Azure Active Directory'de aaaManaging özel etki alanı adları | Microsoft Docs"
description: "Yönetim Kavramları ve Azure Active Directory'de özel etki alanı yönetmek için nasıl yapılır?"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="65085-103">Azure Active Directory'de özel etki alanı adlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="65085-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="65085-104">Bir etki alanı adı, birçok dizin kaynaklar için önemli bir tanımlayıcı bir parçası olarak şunlar olabilir:</span><span class="sxs-lookup"><span data-stu-id="65085-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="65085-105">Bir kullanıcı için bir kullanıcı adı veya e-posta adresi</span><span class="sxs-lookup"><span data-stu-id="65085-105">A user name or email address for a user</span></span>
* <span data-ttu-id="65085-106">bir grup için başlangıç adresi</span><span class="sxs-lookup"><span data-stu-id="65085-106">hello address for a group</span></span>
* <span data-ttu-id="65085-107">bir uygulama için Hello uygulama kimliği URI'si</span><span class="sxs-lookup"><span data-stu-id="65085-107">hello app ID URI for an application</span></span>

<span data-ttu-id="65085-108">Azure Active Directory'de (Azure AD) bir kaynak hello kaynak içeren toobe hello dizine ait zaten doğrulanmış bir etki alanı adı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65085-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified toobe owned by hello directory that contains hello resource.</span></span> <span data-ttu-id="65085-109">Yalnızca genel yönetici Azure AD etki alanı yönetimi görevlerini gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="65085-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65085-110">Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="65085-110">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="65085-111">Hello Azure AD Yönetim Merkezi'nde etki alanınızın nasıl toomanage adları için bkz: [Azure Active Directory'de özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="65085-111">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="65085-112">Azure AD dizininiz için Hello birincil etki alanı adı ayarlama</span><span class="sxs-lookup"><span data-stu-id="65085-112">Set hello primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="65085-113">Dizininize oluşturulduğunda 'contoso.onmicrosoft.com,' gibi hello ilk etki alanı adı da hello birincil etki alanı dizininizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="65085-113">When your directory is created, hello initial domain name, such as ‘contoso.onmicrosoft.com,’ is also hello primary domain name for your directory.</span></span> <span data-ttu-id="65085-114">Merhaba birincil etki alanı olduğunda hello varsayılan etki alanı adını yeni bir kullanıcı için yeni bir kullanıcı hello oluşturmak [Klasik Azure portalı](https://manage.windowsazure.com/), veya diğer portallarını hello Office 365 Yönetici portalı gibi.</span><span class="sxs-lookup"><span data-stu-id="65085-114">hello primary domain is hello default domain name for a new user when you create a new user in hello [Azure classic portal](https://manage.windowsazure.com/), or other portals such as hello Office 365 admin portal.</span></span> <span data-ttu-id="65085-115">Bu, bir yönetici toocreate yeni kullanıcılar için hello portal hello işlemini kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="65085-115">This streamlines hello process for an administrator toocreate new users in hello portal.</span></span>

<span data-ttu-id="65085-116">dizininiz için toochange hello birincil etki alanı adı:</span><span class="sxs-lookup"><span data-stu-id="65085-116">toochange hello primary domain name for your directory:</span></span>

1. <span data-ttu-id="65085-117">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Azure AD dizininizin genel yöneticisi olan bir kullanıcı hesabı ile.</span><span class="sxs-lookup"><span data-stu-id="65085-117">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="65085-118">Seçin **Active Directory** hello sol gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="65085-118">Select **Active Directory** on hello left navigation bar.</span></span>
3. <span data-ttu-id="65085-119">Dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="65085-119">Open your directory.</span></span>
4. <span data-ttu-id="65085-120">Select hello **etki alanları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="65085-120">Select hello **Domains** tab.</span></span>
5. <span data-ttu-id="65085-121">Select hello **değişiklik birincil** hello komut çubuğunda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65085-121">Select hello **Change primary** button on hello command bar.</span></span>
6. <span data-ttu-id="65085-122">Dizininiz için toobe hello yeni birincil etki alanı istediğiniz hello etki alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="65085-122">Select hello domain that you want toobe hello new primary domain for your directory.</span></span>

<span data-ttu-id="65085-123">Birleşik olmadığı herhangi doğrulanmış özel etki alanı, dizin toobe hello birincil etki alanı adını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65085-123">You can change hello primary domain name for your directory toobe any verified custom domain that is not federated.</span></span> <span data-ttu-id="65085-124">Merhaba birincil etki alanı değişen dizininiz için var olan tüm kullanıcılar hello kullanıcı adları değişmez.</span><span class="sxs-lookup"><span data-stu-id="65085-124">Changing hello primary domain for your directory will not change hello user names for any existing users.</span></span>

## <a name="add-custom-domain-names-tooyour-azure-ad"></a><span data-ttu-id="65085-125">Özel etki alanı adları tooyour Azure AD ekleyin</span><span class="sxs-lookup"><span data-stu-id="65085-125">Add custom domain names tooyour Azure AD</span></span>
<span data-ttu-id="65085-126">Too900 özel etki alanı adları tooeach Azure AD dizini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65085-126">You can add up too900 custom domain names tooeach Azure AD directory.</span></span> <span data-ttu-id="65085-127">işlem çok hello[bir ek özel etki alanı adı ekleyin](active-directory-add-domain.md) olan hello aynı hello ilk özel etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="65085-127">hello process too[add an additional custom domain name](active-directory-add-domain.md) is hello same for hello first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="65085-128">Özel bir etki alanının alt etki alanlarını ekleme</span><span class="sxs-lookup"><span data-stu-id="65085-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="65085-129">Tooadd 'europe.contoso.com' tooyour dizini gibi bir üçüncü düzey etki alanı adı istiyorsanız, önce ekleyin ve contoso.com gibi hello ikinci düzey etki doğrulamanız gerekir. Merhaba alt etki alanı otomatik olarak Azure AD tarafından doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="65085-129">If you want tooadd a third-level domain name such as ‘europe.contoso.com’ tooyour directory, you should first add and verify hello second-level domain, such as contoso.com. hello subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="65085-130">Yeni eklediğiniz alt etki alanı hello toosee doğrulandı, yenileme hello sayfasını hello tarayıcıda dizininizde hello etki alanları listelenir.</span><span class="sxs-lookup"><span data-stu-id="65085-130">toosee that hello subdomain that you just added has been verified, refresh hello page in hello browser that lists hello domains in your directory.</span></span>

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="65085-131">Özel etki alanı adınızı hello DNS kayıt şirketi değiştirirseniz, hangi toodo</span><span class="sxs-lookup"><span data-stu-id="65085-131">What toodo if you change hello DNS registrar for your custom domain name</span></span>
<span data-ttu-id="65085-132">Özel etki alanı adınızı hello DNS kayıt şirketi değiştirirseniz, özel etki alanı adınızı Azure AD ile kendini kesinti olmadan ek yapılandırma görevleri ve toouse devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65085-132">If you change hello DNS registrar for your custom domain name, you can continue toouse your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="65085-133">Office 365, Intune veya Azure AD içinde özel etki alanı adları kullanan diğer hizmetler ile özel etki alanı adınızı kullanırsanız, bu hizmetleri toohello belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="65085-133">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer toohello documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="65085-134">Özel etki alanı silme</span><span class="sxs-lookup"><span data-stu-id="65085-134">Delete a custom domain name</span></span>
<span data-ttu-id="65085-135">Kuruluşunuz artık bu etki alanı adını kullanıyorsa ya da başka bir Azure AD etki alanı adını toouse gereksinim duyarsanız, özel etki alanı adı, Azure AD'den silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65085-135">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need toouse that domain name with another Azure AD.</span></span>

<span data-ttu-id="65085-136">toodelete bir özel etki alanı adı, dizininizdeki hiçbir kaynak hello etki alanı adını kullanan ilk emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="65085-136">toodelete a custom domain name, you must first ensure that no resources in your directory rely on hello domain name.</span></span> <span data-ttu-id="65085-137">Bir etki alanı adı, varsa dizininizden silinemiyor:</span><span class="sxs-lookup"><span data-stu-id="65085-137">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="65085-138">Herhangi bir kullanıcı, bir kullanıcı adı, e-posta adresi veya hello etki alanı adını içeren proxy adresi vardır.</span><span class="sxs-lookup"><span data-stu-id="65085-138">Any user has a user name, email address, or proxy address that include hello domain name.</span></span>
* <span data-ttu-id="65085-139">Herhangi bir grup, bir e-posta adresi veya hello etki alanı adını içeren proxy adresi vardır.</span><span class="sxs-lookup"><span data-stu-id="65085-139">Any group has an email address or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="65085-140">Azure ad herhangi bir uygulama kimliği URI'hello etki alanı adını içeren bir uygulama vardır.</span><span class="sxs-lookup"><span data-stu-id="65085-140">Any application in your Azure AD has an app ID URI that includes hello domain name.</span></span>

<span data-ttu-id="65085-141">Değiştirme veya hello özel etki alanı adı silmeden önce herhangi bir kaynağa Azure AD dizininizi silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="65085-141">You must change or delete any such resource in your Azure AD directory before you can delete hello custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a><span data-ttu-id="65085-142">PowerShell veya grafik API'si toomanage etki alanı adlarını kullanın</span><span class="sxs-lookup"><span data-stu-id="65085-142">Use PowerShell or Graph API toomanage domain names</span></span>
<span data-ttu-id="65085-143">Azure Active Directory etki alanı adları için yönetim görevlerinin çoğunu Microsoft PowerShell veya program aracılığıyla Azure AD Graph API kullanarak tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="65085-143">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="65085-144">Azure AD PowerShell toomanage etki alanı adlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="65085-144">Using PowerShell toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="65085-145">Azure AD grafik API'si toomanage etki alanı adlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="65085-145">Using Graph API toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="65085-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65085-146">Next steps</span></span>
* [<span data-ttu-id="65085-147">Azure AD içinde etki alanı adları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="65085-147">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="65085-148">Özel etki alanı adlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="65085-148">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

