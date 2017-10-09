---
title: "aaaAzure veri Kataloğu önkoşulları | Microsoft Docs"
description: "Azure veri Kataloğu ile çalışmaya tooget ihtiyacınız hello önkoşullar hakkında bilgi edinin."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="a5c9f-103">Azure Veri Kataloğu önkoşulları</span><span class="sxs-lookup"><span data-stu-id="a5c9f-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="a5c9f-104">Azure veri Kataloğu ayarlamadan önce birkaç care of tootake gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="a5c9f-105">Endişelenmeyin, bu işlem uzun sürmez.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="a5c9f-106">Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="a5c9f-106">Azure subscription</span></span>
<span data-ttu-id="a5c9f-107">tooset veri Kataloğu, hello sahibi veya bir Azure aboneliğinin ortak sahibi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="a5c9f-108">Azure abonelikleri erişim toocloud hizmet kaynakları veri Kataloğu gibi düzenlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="a5c9f-109">Abonelikleri nasıl kaynak kullanımı bildirilen faturalandırılır ve ödendiği denetlemenize yardımcı.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="a5c9f-110">Abonelikler ve departman, proje, bölgesel ofise vb. göre farklılık planları alacak şekilde her abonelik bir ayrı faturalandırma ve ödeme ayarına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="a5c9f-111">Her bir bulut hizmeti tooa aboneliği aittir ve veri Kataloğu ayarlamak önce toohave bir abonelik gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="a5c9f-112">toolearn daha, fazla [hesapları, abonelikleri ve yönetici rollerini yönetme](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a5c9f-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="a5c9f-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5c9f-113">Azure Active Directory</span></span>
<span data-ttu-id="a5c9f-114">tooset veri Kataloğu'nu ayarlamak, bir Azure Active Directory (Azure AD) kullanıcı hesabıyla oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="a5c9f-115">Azure AD iş toomanage kimlik ve erişim, hem de hello Bulut ve şirket içi için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="a5c9f-116">Şirket içi web uygulaması ve kullanıcılar için çoklu oturum açma tooany bulut tek bir iş veya Okul hesabınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="a5c9f-117">Azure AD tooauthenticate oturum açma veri kataloğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="a5c9f-118">toolearn daha, fazla [Azure Active Directory nedir?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5c9f-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a5c9f-119">Hello kullanarak [Azure portal](http://portal.azure.com/), oturum kişisel bir Microsoft hesabı veya bir Azure Active Directory oturum iş veya Okul hesabı.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="a5c9f-120">kullanarak tooset veri Kataloğu yukarı ya da hello Azure portal veya hello [veri Kataloğu portalını](http://www.azuredatacatalog.com), bir kişisel hesap bir Azure Active Directory hesabıyla oturum açması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="a5c9f-121">Active Directory ilke yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a5c9f-121">Active Directory policy configuration</span></span>
<span data-ttu-id="a5c9f-122">Toohello veri Kataloğu portalında oturum açabildiğiniz, ancak toohello veri kaynağı kayıt aracını toosign çalıştığınızda bir durum karşılaşabilirsiniz, açmasını engelleyen bir hata iletisiyle karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="a5c9f-123">Bu sorunu davranış yalnızca hello şirket ağda bulunuyorsanız veya yalnızca zaman dış hello şirket ağdan bağlantı kurduğunuz oluşabilecek oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="a5c9f-124">Merhaba veri kaynağı kayıt aracını form kimlik doğrulaması toovalidate Active Directory, kullanıcı kimlik bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="a5c9f-125">başarıyla oturum toohelp, Active Directory yönetici hello genel kimlik doğrulama ilkesini form kimlik doğrulamasını etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="a5c9f-126">Hello genel kimlik doğrulama İlkesi, hello ekran aşağıdaki gösterildiği gibi intranet için ayrı ayrı etkinse ve extranet bağlantıları, kimlik doğrulama yöntemleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="a5c9f-127">Bağlantı kurduğunuz hello ağ için form kimlik doğrulaması etkin değilse oturum açma hataları oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="a5c9f-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Active Directory genel kimlik doğrulama İlkesi](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="a5c9f-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a5c9f-129">Next steps</span></span>
<span data-ttu-id="a5c9f-130">Daha fazla bilgi için bkz: [kimlik doğrulaması ilkelerini yapılandırma](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5c9f-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
