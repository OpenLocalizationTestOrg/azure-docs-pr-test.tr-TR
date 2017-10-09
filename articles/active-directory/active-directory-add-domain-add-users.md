---
title: "aaaAssign kullanıcılar tooa özel etki alanı Azure Active Directory'de | Microsoft Docs"
description: "Nasıl toopopulate özel bir etki alanı Azure Active Directory'deki kullanıcı hesaplarına sahip."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="94b98-103">Kullanıcıların tooa özel etki alanı atayın</span><span class="sxs-lookup"><span data-stu-id="94b98-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="94b98-104">Active Directory, özel etki alanı tooAzure ekledikten sonra bunları kimlik doğrulaması başlayabilmesi hello kullanıcı hesaplarını bu etki alanı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="94b98-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94b98-105">Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="94b98-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="94b98-106">Hello Azure AD Yönetim Merkezi'nde etki alanınızın nasıl toomanage adları için bkz: [Azure Active Directory'de özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94b98-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="94b98-107">Bir şirket içi Directory'den eşitlenen kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="94b98-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="94b98-108">Zaten bir bağlantı ayarlamak, şirket içi arasında Active Directory ve Azure Active Directory ayarladıysanız, eşitleme hello hesapları doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94b98-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="94b98-109">Azure Active Directory, şirket içi Active Directory ile nasıl toosynchronize bakın hakkında daha fazla bilgi için [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="94b98-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="94b98-110">Eklenen ve hello bulutta yönetilen kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="94b98-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="94b98-111">Varolan bir kullanıcı hesabı için toochange hello etki alanı:</span><span class="sxs-lookup"><span data-stu-id="94b98-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="94b98-112">Açık hello genel yönetici veya Kullanıcı Yöneticisi olan bir hesabı kullanarak Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="94b98-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="94b98-113">Dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="94b98-113">Open your directory.</span></span>
3. <span data-ttu-id="94b98-114">Select hello **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="94b98-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="94b98-115">Merhaba kullanıcı hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="94b98-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="94b98-116">Hello etki alanı hello kullanıcı için değiştirin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="94b98-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="94b98-117">Bu ayrıca yapılabilir kullanarak [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) veya hello [grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="94b98-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="94b98-118">Yeni bir kullanıcı oluşturulurken özel bir etki alanı seçin</span><span class="sxs-lookup"><span data-stu-id="94b98-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="94b98-119">Açık hello genel yönetici veya Kullanıcı Yöneticisi olan bir hesabı kullanarak Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="94b98-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="94b98-120">Dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="94b98-120">Open your directory.</span></span>
3. <span data-ttu-id="94b98-121">Select hello **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="94b98-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="94b98-122">Merhaba komut çubuğunda seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="94b98-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="94b98-123">Merhaba kullanıcı adı eklediğinizde, hello özel etki alanı hello etki alanı listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="94b98-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="94b98-124">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="94b98-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94b98-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94b98-125">Next steps</span></span>
* [<span data-ttu-id="94b98-126">Kullanıcılarınız için oturum açma, özel etki alanı adları toosimplify hello deneyimi kullanma</span><span class="sxs-lookup"><span data-stu-id="94b98-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="94b98-127">Özel etki alanı adlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="94b98-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="94b98-128">Azure AD'deki etki alanı yönetimi kavramları hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="94b98-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

