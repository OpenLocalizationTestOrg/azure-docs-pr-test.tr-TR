---
title: "Kullanım senaryoları ve Azure AD katılım için dağıtım konuları | Microsoft Docs"
description: "Nasıl yöneticileri Azure AD'ye katılımı kendi son kullanıcıları için (çalışanlar, Öğrenciler, diğer kullanıcıları) ayarlayacakları açıklanmaktadır. Ayrıca, Azure AD katılım kullanmak için farklı gerçek senaryolar anlatılmaktadır."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: fd0aab1a14bbd324e734e5efe8fe101e8a8dfefa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="71f74-104">Kullanım senaryoları ve Azure AD katılım için dağıtım konuları</span><span class="sxs-lookup"><span data-stu-id="71f74-104">Usage scenarios and deployment considerations for Azure AD Join</span></span>
## <a name="usage-scenarios-for-azure-ad-join"></a><span data-ttu-id="71f74-105">Azure AD katılım için kullanım senaryoları</span><span class="sxs-lookup"><span data-stu-id="71f74-105">Usage scenarios for Azure AD Join</span></span>
### <a name="scenario-1-businesses-largely-in-the-cloud"></a><span data-ttu-id="71f74-106">Senaryo 1: İşletmeler büyük ölçüde bulutta</span><span class="sxs-lookup"><span data-stu-id="71f74-106">Scenario 1: Businesses largely in the cloud</span></span>
<span data-ttu-id="71f74-107">Azure Active Directory katılım (Azure AD katılımı), şu anda çalışır ve işinizi buluttaki için kimlikleri yönetme veya buluta yakında taşıyorsanız, yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71f74-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in the cloud or are moving to the cloud soon.</span></span> <span data-ttu-id="71f74-108">Windows 10'a oturum açmak için Azure AD içinde oluşturduğunuz bir hesap kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71f74-108">You can use an account that you have created in Azure AD to sign in to Windows 10.</span></span> <span data-ttu-id="71f74-109">Aracılığıyla [ilk çalıştırma deneyimi (FRX) işlem](active-directory-azureadjoin-user-frx.md), Azure AD'den katılarak ya [ayarlar menüsünü](active-directory-azureadjoin-user-upgrade.md), kullanıcılarınızın kendi makinelerine Azure AD ile birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71f74-109">Through [the first run experience (FRX) process](active-directory-azureadjoin-user-frx.md), or by joining Azure AD from [the settings menu](active-directory-azureadjoin-user-upgrade.md), your users can join their machines to Azure AD.</span></span>  <span data-ttu-id="71f74-110">Kullanıcılarınızın, aynı zamanda çoklu oturum açma (SSO) erişimi tarayıcılarını veya Office uygulamaları, Office 365 gibi bulut kaynaklarına keyfini çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71f74-110">Your users can also enjoy single sign-on (SSO) access to  cloud resources like Office 365, either in their browsers or in Office applications.</span></span>

### <a name="scenario-2-educational-institutions"></a><span data-ttu-id="71f74-111">Senaryo 2: Eğitim kurumları</span><span class="sxs-lookup"><span data-stu-id="71f74-111">Scenario 2: Educational institutions</span></span>
<span data-ttu-id="71f74-112">Eğitim kurumları genellikle iki kullanıcı türlerine sahip: Fakülte ve öğrenciler.</span><span class="sxs-lookup"><span data-stu-id="71f74-112">Educational institutions usually have two user types: faculty and students.</span></span> <span data-ttu-id="71f74-113">Fakülte üyeleri kuruluş daha uzun vadeli üyeleri olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="71f74-113">Faculty members are considered longer-term members of the organization.</span></span> <span data-ttu-id="71f74-114">Şirket içi hesapları kullanabiliyor tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="71f74-114">Creating on-premises accounts for them is desirable.</span></span> <span data-ttu-id="71f74-115">Ancak Öğrenciler kuruluşun shorter-term üyeleridir ve hesaplarını Azure AD'de yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="71f74-115">But students are shorter-term members of the organization and  their accounts can be managed in Azure AD.</span></span> <span data-ttu-id="71f74-116">Bu dizin ölçek şirket içi depolanan olmak yerine buluta gönderilemez anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="71f74-116">This means that directory scale can be pushed to the cloud instead of being stored on-premises.</span></span> <span data-ttu-id="71f74-117">Öğrenciler için Windows Azure AD hesaplarına ile oturum açın ve Office uygulamalarında Office 365 kaynaklara erişmek için olmayacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="71f74-117">It also means that students  will be able to sign in to Windows with their Azure AD accounts and get access to Office 365 resources in Office applications.</span></span>

### <a name="scenario-3-retail-businesses"></a><span data-ttu-id="71f74-118">Senaryo 3: Perakende işletmeler</span><span class="sxs-lookup"><span data-stu-id="71f74-118">Scenario 3: Retail businesses</span></span>
<span data-ttu-id="71f74-119">Perakende işletmeler Mevsimlik çalışanları ve uzun vadeli çalışanların sahip.</span><span class="sxs-lookup"><span data-stu-id="71f74-119">Retail businesses have seasonal workers and long-term employees.</span></span> <span data-ttu-id="71f74-120">Genellikle şirket içi hesapları oluşturabilir ve etki alanına katılan makineler daha uzun vadeli tam zamanlı çalışanlar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="71f74-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span></span> <span data-ttu-id="71f74-121">Ancak kuruluşun shorter-term üyeleri Mevsimlik çalışanlardır ve burada kullanıcı lisansları daha kolay taşınabildiğinden, hesaplarını yönetmek için tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="71f74-121">But seasonal workers are shorter-term members of the organization, and it's desirable to manage their accounts where user licenses can be more easily moved around.</span></span> <span data-ttu-id="71f74-122">Office 365 lisansına sahip bulutta, kullanıcı hesaplarını oluşturduğunuzda, bu kullanıcılar bunlar çıktıktan sonra lisansları ile daha fazla esneklik bakım yaparken Windows ve Office uygulamaları, Azure AD hesap ile oturum açma avantajlarını alır.</span><span class="sxs-lookup"><span data-stu-id="71f74-122">When you create their user accounts in the cloud with Office 365 licenses, these users get the benefits of signing in to Windows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span></span>

### <a name="scenario-4-additional-scenarios"></a><span data-ttu-id="71f74-123">Senaryo 4: İlave senaryolar</span><span class="sxs-lookup"><span data-stu-id="71f74-123">Scenario 4: Additional scenarios</span></span>
<span data-ttu-id="71f74-124">Daha önce bahsedilen avantajları yanı sıra, bir Basitleştirilmiş katılma deneyimi, verimli aygıt yönetimi, otomatik mobil cihaz Yönetimi kayıt ve Azure ad çoklu oturum açma nedeniyle cihazlarını Azure AD'ye ekler, kullanıcılarınızın kalmaktan yararlanabilir ve şirket içi kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="71f74-124">Along with the benefits discussed earlier, you  benefit from having your users join their devices to Azure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on to Azure AD and on-premises resources.</span></span>  

## <a name="deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="71f74-125">Azure AD katılım için dağıtım konuları</span><span class="sxs-lookup"><span data-stu-id="71f74-125">Deployment considerations for Azure AD Join</span></span>
### <a name="enable-your-users-to-join-a-company-owned-device-directly-to-azure-ad"></a><span data-ttu-id="71f74-126">Şirkete ait bir cihazı doğrudan Azure AD birleştirme etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="71f74-126">Enable your users to join a company-owned device directly to Azure AD</span></span>
<span data-ttu-id="71f74-127">Kuruluşlar, iş ortağı şirketlerden ve kuruluşlara yalnızca bulut hesapları sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="71f74-127">Enterprises can provide cloud-only accounts to partner companies and organizations.</span></span> <span data-ttu-id="71f74-128">Bu iş ortaklarının daha sonra kolayca şirket uygulamaları ve çoklu oturum açma ile kaynaklarına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71f74-128">These partners can then easily access company apps and resources with single sign-on.</span></span> <span data-ttu-id="71f74-129">Bu senaryo, kimlik doğrulaması için Azure AD Bel Office 365 veya SaaS uygulamaları gibi birincil buluttaki kaynaklara erişen kullanıcılar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="71f74-129">This scenario is applicable to users who access resources primarily in the cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="71f74-130">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="71f74-130">Prerequisites</span></span>
<span data-ttu-id="71f74-131">**Kurumsal düzeyde (Yönetici)**</span><span class="sxs-lookup"><span data-stu-id="71f74-131">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="71f74-132">Azure Active Directory ile Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="71f74-132">Azure subscription with Azure Active Directory</span></span>  

<span data-ttu-id="71f74-133">**Kullanıcı düzeyinde**</span><span class="sxs-lookup"><span data-stu-id="71f74-133">**At the user level**</span></span>

* <span data-ttu-id="71f74-134">Windows 10 (Professional ve Enterprise sürümleri)</span><span class="sxs-lookup"><span data-stu-id="71f74-134">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="71f74-135">Yönetici görevleri</span><span class="sxs-lookup"><span data-stu-id="71f74-135">Administrator tasks</span></span>
* [<span data-ttu-id="71f74-136">Cihaz kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="71f74-136">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="71f74-137">Kullanıcı görevleri</span><span class="sxs-lookup"><span data-stu-id="71f74-137">User tasks</span></span>
* [<span data-ttu-id="71f74-138">Kurulum sırasında Azure AD ile yeni bir Windows 10 cihazı ayarlama</span><span class="sxs-lookup"><span data-stu-id="71f74-138">Set up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md)
* [<span data-ttu-id="71f74-139">Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama</span><span class="sxs-lookup"><span data-stu-id="71f74-139">Set up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="71f74-140">Kişisel bir Windows 10 cihazı kuruluşunuza katma</span><span class="sxs-lookup"><span data-stu-id="71f74-140">Join a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a><span data-ttu-id="71f74-141">Windows 10 için kuruluşunuzdaki KCG etkinleştir</span><span class="sxs-lookup"><span data-stu-id="71f74-141">Enable BYOD in your organization for Windows 10</span></span>
<span data-ttu-id="71f74-142">Kendi kişisel Windows cihazlarını (BYOD) şirket uygulamalarına ve kaynaklarına kullanmak için kullanıcılar ve çalışanlar ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71f74-142">You can set up your users and employees to use their personal Windows devices (BYOD) to access company apps and resources.</span></span> <span data-ttu-id="71f74-143">Kullanıcılarınızın kişisel bir Windows aygıtı kaynaklarına güvenli ve uyumlu bir şekilde erişmek için Azure AD hesaplarına (iş veya Okul hesapları) ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71f74-143">Your users can add their Azure AD accounts (work or school accounts) to a personal Windows device to access resources in a secure and compliant fashion.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="71f74-144">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="71f74-144">Prerequisites</span></span>
<span data-ttu-id="71f74-145">**Kurumsal düzeyde (Yönetici)**</span><span class="sxs-lookup"><span data-stu-id="71f74-145">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="71f74-146">Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="71f74-146">Azure AD subscription</span></span>

<span data-ttu-id="71f74-147">**Kullanıcı düzeyinde**</span><span class="sxs-lookup"><span data-stu-id="71f74-147">**At the user level**</span></span>

* <span data-ttu-id="71f74-148">Windows 10 (Professional ve Enterprise sürümleri)</span><span class="sxs-lookup"><span data-stu-id="71f74-148">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="71f74-149">Yönetici görevleri</span><span class="sxs-lookup"><span data-stu-id="71f74-149">Administrator tasks</span></span>
* [<span data-ttu-id="71f74-150">Cihaz kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="71f74-150">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="71f74-151">Kullanıcı görevleri</span><span class="sxs-lookup"><span data-stu-id="71f74-151">User tasks</span></span>
* [<span data-ttu-id="71f74-152">Kişisel bir Windows 10 cihazı kuruluşunuza katma</span><span class="sxs-lookup"><span data-stu-id="71f74-152">Join a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a><span data-ttu-id="71f74-153">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="71f74-153">Additional information</span></span>
* [<span data-ttu-id="71f74-154">Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları</span><span class="sxs-lookup"><span data-stu-id="71f74-154">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="71f74-155">Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme</span><span class="sxs-lookup"><span data-stu-id="71f74-155">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="71f74-156">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="71f74-156">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="71f74-157">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="71f74-157">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="71f74-158">Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="71f74-158">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="71f74-159">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="71f74-159">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

