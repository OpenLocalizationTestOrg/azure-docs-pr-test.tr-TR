---
title: "Azure Active Directory'de özel etki alanı kullanıcıları atamak | Microsoft Docs"
description: "Azure Active Directory'de özel olarak etki alanı kullanıcı hesapları ile doldurmak nasıl."
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
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="68255-103">Özel bir etki alanına kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="68255-103">Assign users to a custom domain</span></span>
<span data-ttu-id="68255-104">Özel etki alanınızı Azure Active Directory'ye ekledikten sonra bunları kimlik doğrulaması başlayabilmeniz için bu etki alanı kullanıcı hesaplarını eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="68255-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68255-105">Microsoft, Azure AD’yi bu makalede bahsedilen Klasik Azure Portalı yerine Azure portalındaki [Azure AD yönetim merkezini](https://aad.portal.azure.com) kullanarak yönetmenizi öneriyor.</span><span class="sxs-lookup"><span data-stu-id="68255-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="68255-106">Azure AD Yönetim Merkezi'nden, etki alanı adlarını yönetmek için bkz: nasıl [Azure Active Directory'de özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68255-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="68255-107">Bir şirket içi Directory'den eşitlenen kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="68255-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="68255-108">Zaten bir bağlantı ayarlamak, şirket içi arasında Active Directory ve Azure Active Directory ayarladıysanız, eşitleme hesapları doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68255-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="68255-109">Şirket içi Active Directory ile Azure Active Directory eşitleme hakkında daha fazla bilgi için bkz: [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="68255-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="68255-110">Eklenen ve bulutta yönetilen kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="68255-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="68255-111">Varolan bir kullanıcı hesabı için etki alanını değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="68255-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="68255-112">Genel yönetici veya Kullanıcı Yöneticisi olan bir hesabı kullanarak Klasik Azure portalını açın</span><span class="sxs-lookup"><span data-stu-id="68255-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="68255-113">Dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="68255-113">Open your directory.</span></span>
3. <span data-ttu-id="68255-114">**Users (Kullanıcılar)** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="68255-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="68255-115">Kullanıcı listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="68255-115">Select the user from the list.</span></span>
5. <span data-ttu-id="68255-116">Kullanıcı için etki alanını değiştirmek ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="68255-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="68255-117">Bu ayrıca yapılabilir kullanarak [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) veya [grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="68255-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="68255-118">Yeni bir kullanıcı oluşturulurken özel bir etki alanı seçin</span><span class="sxs-lookup"><span data-stu-id="68255-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="68255-119">Genel yönetici veya Kullanıcı Yöneticisi olan bir hesabı kullanarak Klasik Azure portalını açın</span><span class="sxs-lookup"><span data-stu-id="68255-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="68255-120">Dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="68255-120">Open your directory.</span></span>
3. <span data-ttu-id="68255-121">**Users (Kullanıcılar)** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="68255-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="68255-122">Komut çubuğunda seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="68255-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="68255-123">Kullanıcı adı eklediğinizde, özel etki alanı etki alanı listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="68255-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="68255-124">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="68255-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68255-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="68255-125">Next steps</span></span>
* [<span data-ttu-id="68255-126">Kullanıcılarınız için oturum açma deneyimini basitleştirmek için özel etki alanı adlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="68255-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="68255-127">Özel etki alanı adlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="68255-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="68255-128">Azure AD'deki etki alanı yönetimi kavramları hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="68255-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

