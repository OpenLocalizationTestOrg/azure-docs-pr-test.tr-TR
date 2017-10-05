---
title: "Visual Studio'da bağlı hizmetler kullanarak bir Azure Active Directory'ye ekleme | Microsoft Docs"
description: "Visual Studio bağlı Hizmetleri Ekle iletişim kutusunu kullanarak bir Azure Active Directory'ye ekleme"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: a767c93fb271f3aa33d9556c69c511bcac7cb0d5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="3d255-103">Visual Studio'da bağlı hizmetler kullanarak bir Azure Active Directory'ye ekleme</span><span class="sxs-lookup"><span data-stu-id="3d255-103">Adding an Azure Active Directory by using Connected Services in Visual Studio</span></span>
<span data-ttu-id="3d255-104">Azure Active Directory (Azure AD) kullanarak, çoklu oturum açma (SSO) ASP.NET MVC web uygulamaları veya Active Directory kimlik doğrulaması için Web API Hizmetleri'ni destekler.</span><span class="sxs-lookup"><span data-stu-id="3d255-104">By using Azure Active Directory (Azure AD), you can support Single Sign-On (SSO) for ASP.NET MVC web applications, or Active Directory Authentication in Web API services.</span></span> <span data-ttu-id="3d255-105">Azure Active Directory kimlik doğrulaması ile kullanıcılarınız, web uygulamalarınızı bağlanmak için Azure Active Directory hesaplarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="3d255-105">With Azure Active Directory Authentication, your users can use their accounts from Azure Active Directory to connect to your web applications.</span></span> <span data-ttu-id="3d255-106">Bir web uygulamasından bir API gösterme işlemlerinde, Azure Active Directory kimlik doğrulaması Web API ile avantajları gelişmiş veri güvenliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="3d255-106">The advantages of Azure Active Directory Authentication with Web API include enhanced data security when exposing an API from a web application.</span></span> <span data-ttu-id="3d255-107">Azure AD ile ayrı kimlik doğrulama sistemi kendi hesabı ve kullanıcı yönetimi ile yönetmek zorunda değildir.</span><span class="sxs-lookup"><span data-stu-id="3d255-107">With Azure AD, you do not have to manage a separate authentication system with its own account and user management.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d255-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3d255-108">Prerequisites</span></span>
- <span data-ttu-id="3d255-109">Azure hesabı - bir Azure hesabınız yoksa şunları yapabilirsiniz [ücretsiz deneme için kaydolun](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="3d255-109">Azure account - If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

### <a name="connect-to-azure-active-directory-using-the-connected-services-dialog"></a><span data-ttu-id="3d255-110">Azure Active bağlı Hizmetleri iletişim kutusu kullanılarak dizinine bağlanma</span><span class="sxs-lookup"><span data-stu-id="3d255-110">Connect to Azure Active Directory using the Connected Services dialog</span></span>
1. <span data-ttu-id="3d255-111">Visual Studio'da oluşturun veya bir ASP.NET MVC projesini ya da bir ASP.NET Web API projesini açın.</span><span class="sxs-lookup"><span data-stu-id="3d255-111">In Visual Studio, create or open an ASP.NET MVC project, or an ASP.NET Web API project.</span></span>

1. <span data-ttu-id="3d255-112">Çözüm Gezgini'nden sağ **bağlantılı Hizmetler** düğümünü ve bağlam menüsünden seçin **bağlı Hizmetleri Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3d255-112">From the Solution Explorer, right-click the **Connected Services** node, and, from the context menu, select **Add Connected Services**.</span></span>

1. <span data-ttu-id="3d255-113">Üzerinde **bağlantılı Hizmetler** sayfasında, **Azure Active Directory ile kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="3d255-113">On the **Connected Services** page, select **Authentication with Azure Active Directory**.</span></span>
   
    ![Bağlı hizmetler sayfası](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. <span data-ttu-id="3d255-115">Üzerinde **giriş** sayfasında **yapılandırma Azure AD kimlik doğrulama** seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3d255-115">On the **Introduction** page of the **Configure Azure AD Authentication** wizard, select **Next**.</span></span>
   
    ![Giriş sayfası](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. <span data-ttu-id="3d255-117">Üzerinde **tek oturum açma** sayfasında **yapılandırma Azure AD kimlik doğrulama** Sihirbazı, bir etki alanından seçin **etki alanı** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="3d255-117">On the **Single-Sign On** page of the **Configure Azure AD Authentication** wizard, select a domain from the **Domain** drop-down list.</span></span> <span data-ttu-id="3d255-118">Etki alanlarının listesi, hesap ayarları iletişim kutusunda listelenen hesapları tarafından erişilebilir tüm etki alanlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="3d255-118">The list of domains contains all domains accessible by the accounts listed in the Account Settings dialog.</span></span> <span data-ttu-id="3d255-119">Alternatif olarak, aradığınız, gibi bir bulamazsanız, bir etki alanı adını girebilirsiniz `mydomain.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="3d255-119">As an alternative, you can enter a domain name if you don’t find the one you’re looking for, such as `mydomain.onmicrosoft.com`.</span></span> <span data-ttu-id="3d255-120">Bir Azure Active Directory uygulama oluşturmak veya mevcut bir Azure Active Directory Uygulama ayarlarından kullanmak için seçeneğini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d255-120">You can choose the option to create an Azure Active Directory app or use the settings from an existing Azure Active Directory app.</span></span> <span data-ttu-id="3d255-121">Seçin **sonraki** bittiğinde.</span><span class="sxs-lookup"><span data-stu-id="3d255-121">Select **Next** when done.</span></span>
   
    ![Çoklu oturum açma sayfası](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. <span data-ttu-id="3d255-123">Üzerinde **dizin erişimi** sayfasında **yapılandırma Azure AD kimlik doğrulama** Sihirbazı'nı emin olun **dizin verilerini okuma** seçeneği denetlenir.</span><span class="sxs-lookup"><span data-stu-id="3d255-123">On the **Directory Access** page of the **Configure Azure AD Authentication** wizard, ensure that the **Read directory data** option is checked.</span></span> 
   
    ![Dizin erişim sayfası](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. <span data-ttu-id="3d255-125">Seçin **son** gerekli yapılandırma kodu ve projenizi Azure AD kimlik doğrulaması için etkinleştirmek için başvurular eklemek için.</span><span class="sxs-lookup"><span data-stu-id="3d255-125">Select **Finish** to add the necessary configuration code and references to enable your project for Azure AD authentication.</span></span> <span data-ttu-id="3d255-126">Active Directory etki alanı görebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3d255-126">You can see the Active Directory domain on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="3d255-127">Visual Studio görüntüler bir [ne](#how-your-project-is-modified) projenizi nasıl değiştirildiği göstermek için makale.</span><span class="sxs-lookup"><span data-stu-id="3d255-127">Visual Studio will display a [What Happened](#how-your-project-is-modified) article to show you how your project was modified.</span></span> <span data-ttu-id="3d255-128">Her şeyin çalıştığı denetleyin, değiştirilen yapılandırma dosyalarından birini açın ve doğrulamak istiyorsanız makalede değinilen ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="3d255-128">If you want to check that everything worked, open one of the modified configuration files and verify that the settings mentioned in the article are there.</span></span> 

## <a name="how-your-project-is-modified"></a><span data-ttu-id="3d255-129">Projenizi nasıl değiştirilir</span><span class="sxs-lookup"><span data-stu-id="3d255-129">How your project is modified</span></span>
<span data-ttu-id="3d255-130">Sihirbazı'nı çalıştırdığınızda, Visual Studio Azure Active Directory ve ilişkili başvuruları projenize ekler.</span><span class="sxs-lookup"><span data-stu-id="3d255-130">When you run the wizard, Visual Studio adds Azure Active Directory and associated references to your project.</span></span> <span data-ttu-id="3d255-131">Azure AD için destek eklemek için yapılandırma dosyalarını ve kod dosyaları projenizdeki değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="3d255-131">Configuration files and code files in your project are also modified to add support for Azure AD.</span></span> <span data-ttu-id="3d255-132">Visual Studio yapar belirli değişiklikleri proje türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3d255-132">The specific modifications that Visual Studio makes depend on the project type.</span></span> <span data-ttu-id="3d255-133">ASP.NET MVC projeleri nasıl değiştirilir hakkında ayrıntılı bilgi için bkz: [hangi happened – MVC projeleri](http://go.microsoft.com/fwlink/p/?LinkID=513809).</span><span class="sxs-lookup"><span data-stu-id="3d255-133">For detailed information about how ASP.NET MVC projects are modified, see [What happened– MVC Projects](http://go.microsoft.com/fwlink/p/?LinkID=513809).</span></span> <span data-ttu-id="3d255-134">Web API projeleri için bkz: [ne – Web API projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513810).</span><span class="sxs-lookup"><span data-stu-id="3d255-134">For Web API projects, see [What happened – Web API Projects](http://go.microsoft.com/fwlink/p/?LinkId=513810).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d255-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d255-135">Next steps</span></span>
* [<span data-ttu-id="3d255-136">Azure Active Directory için MSDN Forumu</span><span class="sxs-lookup"><span data-stu-id="3d255-136">MSDN Forum for Azure Active Directory</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [<span data-ttu-id="3d255-137">Azure Active Directory belgeleri</span><span class="sxs-lookup"><span data-stu-id="3d255-137">Azure Active Directory Documentation</span></span>](https://azure.microsoft.com/documentation/services/active-directory/)
* [<span data-ttu-id="3d255-138">Blog postası: Azure Active Directory giriş</span><span class="sxs-lookup"><span data-stu-id="3d255-138">Blog Post: Intro to Azure Active Directory</span></span>](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

