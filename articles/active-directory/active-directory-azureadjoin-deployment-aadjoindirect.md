---
title: "aaaUsage senaryoları ve Azure AD katılım için dağıtım konuları | Microsoft Docs"
description: "Nasıl yöneticileri Azure AD'ye katılımı kendi son kullanıcıları için (çalışanlar, Öğrenciler, diğer kullanıcıları) ayarlayacakları açıklanmaktadır. Ayrıca, Azure AD katılım kullanarak hello farklı gerçek senaryolar anlatılmaktadır."
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
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="2356e-104">Kullanım senaryoları ve Azure AD katılım için dağıtım konuları</span><span class="sxs-lookup"><span data-stu-id="2356e-104">Usage scenarios and deployment considerations for Azure AD Join</span></span>
## <a name="usage-scenarios-for-azure-ad-join"></a><span data-ttu-id="2356e-105">Azure AD katılım için kullanım senaryoları</span><span class="sxs-lookup"><span data-stu-id="2356e-105">Usage scenarios for Azure AD Join</span></span>
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a><span data-ttu-id="2356e-106">Senaryo 1: İşletmeler hello bulutta büyük ölçüde</span><span class="sxs-lookup"><span data-stu-id="2356e-106">Scenario 1: Businesses largely in hello cloud</span></span>
<span data-ttu-id="2356e-107">Azure Active Directory katılım (Azure AD katılımı), şu anda çalışır ve hello bulut işinizde için kimlikleri yönetme veya toohello bulut yakında taşıyorsanız, yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2356e-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in hello cloud or are moving toohello cloud soon.</span></span> <span data-ttu-id="2356e-108">Azure AD toosign tooWindows 10 içinde oluşturduğunuz bir hesap kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2356e-108">You can use an account that you have created in Azure AD toosign in tooWindows 10.</span></span> <span data-ttu-id="2356e-109">Aracılığıyla [ilk çalıştırma deneyimi (FRX) işlemi hello](active-directory-azureadjoin-user-frx.md), Azure AD'den katılarak ya [hello ayarları menüsü](active-directory-azureadjoin-user-upgrade.md), kullanıcılarınızın kendi makineler tooAzure AD katılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2356e-109">Through [hello first run experience (FRX) process](active-directory-azureadjoin-user-frx.md), or by joining Azure AD from [hello settings menu](active-directory-azureadjoin-user-upgrade.md), your users can join their machines tooAzure AD.</span></span>  <span data-ttu-id="2356e-110">Kullanıcılarınızın aynı zamanda çoklu oturum açma (SSO) keyfini çıkarabilirsiniz erişim çok tarayıcılarında veya Office uygulamalarında kaynakları, Office 365 gibi bulut.</span><span class="sxs-lookup"><span data-stu-id="2356e-110">Your users can also enjoy single sign-on (SSO) access too cloud resources like Office 365, either in their browsers or in Office applications.</span></span>

### <a name="scenario-2-educational-institutions"></a><span data-ttu-id="2356e-111">Senaryo 2: Eğitim kurumları</span><span class="sxs-lookup"><span data-stu-id="2356e-111">Scenario 2: Educational institutions</span></span>
<span data-ttu-id="2356e-112">Eğitim kurumları genellikle iki kullanıcı türlerine sahip: Fakülte ve öğrenciler.</span><span class="sxs-lookup"><span data-stu-id="2356e-112">Educational institutions usually have two user types: faculty and students.</span></span> <span data-ttu-id="2356e-113">Fakülte üyeleri hello kuruluş daha uzun vadeli üyeleri olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="2356e-113">Faculty members are considered longer-term members of hello organization.</span></span> <span data-ttu-id="2356e-114">Şirket içi hesapları kullanabiliyor tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="2356e-114">Creating on-premises accounts for them is desirable.</span></span> <span data-ttu-id="2356e-115">Ancak Öğrenciler hello kuruluşun shorter-term üyeleridir ve hesaplarını Azure AD'de yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="2356e-115">But students are shorter-term members of hello organization and  their accounts can be managed in Azure AD.</span></span> <span data-ttu-id="2356e-116">Bu dizin ölçek şirket içi depolanan olmak yerine toohello bulut gönderilemez anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2356e-116">This means that directory scale can be pushed toohello cloud instead of being stored on-premises.</span></span> <span data-ttu-id="2356e-117">Ayrıca Öğrenciler tooWindows kendi Azure AD hesapları ile de yükleyebilirsiniz toosign olması ve Office uygulamalarında tooOffice 365 kaynaklara erişmek anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2356e-117">It also means that students  will be able toosign in tooWindows with their Azure AD accounts and get access tooOffice 365 resources in Office applications.</span></span>

### <a name="scenario-3-retail-businesses"></a><span data-ttu-id="2356e-118">Senaryo 3: Perakende işletmeler</span><span class="sxs-lookup"><span data-stu-id="2356e-118">Scenario 3: Retail businesses</span></span>
<span data-ttu-id="2356e-119">Perakende işletmeler Mevsimlik çalışanları ve uzun vadeli çalışanların sahip.</span><span class="sxs-lookup"><span data-stu-id="2356e-119">Retail businesses have seasonal workers and long-term employees.</span></span> <span data-ttu-id="2356e-120">Genellikle şirket içi hesapları oluşturabilir ve etki alanına katılan makineler daha uzun vadeli tam zamanlı çalışanlar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="2356e-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span></span> <span data-ttu-id="2356e-121">Ancak Mevsimlik çalışanlardır hello kuruluş shorter-term üyeleri ve bu arzu toomanage burada kullanıcı lisansları daha kolay taşınabilir geçici hesaplarını.</span><span class="sxs-lookup"><span data-stu-id="2356e-121">But seasonal workers are shorter-term members of hello organization, and it's desirable toomanage their accounts where user licenses can be more easily moved around.</span></span> <span data-ttu-id="2356e-122">Office 365 lisansına sahip hello bulutta, kullanıcı hesaplarını oluşturduğunuzda, bu kullanıcılar bunlar çıktıktan sonra lisansları ile daha fazla esneklik bakım yaparken tooWindows ve bir Azure AD hesabının Office uygulamalarıyla imzalama hello avantajlarını alır.</span><span class="sxs-lookup"><span data-stu-id="2356e-122">When you create their user accounts in hello cloud with Office 365 licenses, these users get hello benefits of signing in tooWindows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span></span>

### <a name="scenario-4-additional-scenarios"></a><span data-ttu-id="2356e-123">Senaryo 4: İlave senaryolar</span><span class="sxs-lookup"><span data-stu-id="2356e-123">Scenario 4: Additional scenarios</span></span>
<span data-ttu-id="2356e-124">Daha önce bahsedilen hello avantajları yanı sıra, kullanıcılarınızın kendi aygıtlarını tooAzure AD Basitleştirilmiş katılma deneyimi, verimli aygıt yönetimi, otomatik mobil cihaz Yönetimi kayıt ve oturum açma tek tooAzure nedeniyle katılma kalmaktan yararlanabilir AD ve şirket içi kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="2356e-124">Along with hello benefits discussed earlier, you  benefit from having your users join their devices tooAzure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on tooAzure AD and on-premises resources.</span></span>  

## <a name="deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="2356e-125">Azure AD katılım için dağıtım konuları</span><span class="sxs-lookup"><span data-stu-id="2356e-125">Deployment considerations for Azure AD Join</span></span>
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a><span data-ttu-id="2356e-126">Kullanıcıların toojoin şirkete ait bir cihazı etkinleştirme doğrudan tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="2356e-126">Enable your users toojoin a company-owned device directly tooAzure AD</span></span>
<span data-ttu-id="2356e-127">Kuruluşlar, yalnızca bulut hesapları toopartner şirketler ve kuruluşlar sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="2356e-127">Enterprises can provide cloud-only accounts toopartner companies and organizations.</span></span> <span data-ttu-id="2356e-128">Bu iş ortaklarının daha sonra kolayca şirket uygulamaları ve çoklu oturum açma ile kaynaklarına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2356e-128">These partners can then easily access company apps and resources with single sign-on.</span></span> <span data-ttu-id="2356e-129">Birincil kimlik doğrulaması için Azure AD Bel Office 365 veya SaaS uygulamaları gibi hello bulut kaynaklara erişim geçerli toousers senaryodur.</span><span class="sxs-lookup"><span data-stu-id="2356e-129">This scenario is applicable toousers who access resources primarily in hello cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2356e-130">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2356e-130">Prerequisites</span></span>
<span data-ttu-id="2356e-131">**Merhaba Kurumsal düzeyde (Yönetici)**</span><span class="sxs-lookup"><span data-stu-id="2356e-131">**At hello enterprise level (administrator)**</span></span>

* <span data-ttu-id="2356e-132">Azure Active Directory ile Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="2356e-132">Azure subscription with Azure Active Directory</span></span>  

<span data-ttu-id="2356e-133">**Merhaba kullanıcı düzeyinde**</span><span class="sxs-lookup"><span data-stu-id="2356e-133">**At hello user level**</span></span>

* <span data-ttu-id="2356e-134">Windows 10 (Professional ve Enterprise sürümleri)</span><span class="sxs-lookup"><span data-stu-id="2356e-134">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="2356e-135">Yönetici görevleri</span><span class="sxs-lookup"><span data-stu-id="2356e-135">Administrator tasks</span></span>
* [<span data-ttu-id="2356e-136">Cihaz kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2356e-136">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="2356e-137">Kullanıcı görevleri</span><span class="sxs-lookup"><span data-stu-id="2356e-137">User tasks</span></span>
* [<span data-ttu-id="2356e-138">Kurulum sırasında Azure AD ile yeni bir Windows 10 cihazı ayarlama</span><span class="sxs-lookup"><span data-stu-id="2356e-138">Set up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md)
* [<span data-ttu-id="2356e-139">Merhaba Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama</span><span class="sxs-lookup"><span data-stu-id="2356e-139">Set up a Windows 10 device with Azure AD from hello settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="2356e-140">Kişisel bir Windows 10 cihaz tooyour kuruluş katılma</span><span class="sxs-lookup"><span data-stu-id="2356e-140">Join a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a><span data-ttu-id="2356e-141">Windows 10 için kuruluşunuzdaki KCG etkinleştir</span><span class="sxs-lookup"><span data-stu-id="2356e-141">Enable BYOD in your organization for Windows 10</span></span>
<span data-ttu-id="2356e-142">Kullanıcılar ve çalışanlar toouse kendi kişisel Windows cihazlarını (BYOD) tooaccess şirket uygulamalarına ve kaynaklarına ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2356e-142">You can set up your users and employees toouse their personal Windows devices (BYOD) tooaccess company apps and resources.</span></span> <span data-ttu-id="2356e-143">Kullanıcılarınızın Azure AD hesapları (iş veya Okul hesapları) tooa kişisel Windows aygıt tooaccess kaynaklarına güvenli ve uyumlu bir biçimde ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2356e-143">Your users can add their Azure AD accounts (work or school accounts) tooa personal Windows device tooaccess resources in a secure and compliant fashion.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2356e-144">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2356e-144">Prerequisites</span></span>
<span data-ttu-id="2356e-145">**Merhaba Kurumsal düzeyde (Yönetici)**</span><span class="sxs-lookup"><span data-stu-id="2356e-145">**At hello enterprise level (administrator)**</span></span>

* <span data-ttu-id="2356e-146">Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2356e-146">Azure AD subscription</span></span>

<span data-ttu-id="2356e-147">**Merhaba kullanıcı düzeyinde**</span><span class="sxs-lookup"><span data-stu-id="2356e-147">**At hello user level**</span></span>

* <span data-ttu-id="2356e-148">Windows 10 (Professional ve Enterprise sürümleri)</span><span class="sxs-lookup"><span data-stu-id="2356e-148">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="2356e-149">Yönetici görevleri</span><span class="sxs-lookup"><span data-stu-id="2356e-149">Administrator tasks</span></span>
* [<span data-ttu-id="2356e-150">Cihaz kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2356e-150">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="2356e-151">Kullanıcı görevleri</span><span class="sxs-lookup"><span data-stu-id="2356e-151">User tasks</span></span>
* [<span data-ttu-id="2356e-152">Kişisel bir Windows 10 cihaz tooyour kuruluş katılma</span><span class="sxs-lookup"><span data-stu-id="2356e-152">Join a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a><span data-ttu-id="2356e-153">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="2356e-153">Additional information</span></span>
* [<span data-ttu-id="2356e-154">Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için</span><span class="sxs-lookup"><span data-stu-id="2356e-154">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="2356e-155">Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme</span><span class="sxs-lookup"><span data-stu-id="2356e-155">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="2356e-156">Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="2356e-156">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="2356e-157">Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2356e-157">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="2356e-158">Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan</span><span class="sxs-lookup"><span data-stu-id="2356e-158">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="2356e-159">Azure AD'ye Katılım ayarlama</span><span class="sxs-lookup"><span data-stu-id="2356e-159">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

