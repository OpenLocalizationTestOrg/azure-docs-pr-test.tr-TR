---
title: "Öğretici: Workday ile şirket içi Active Directory ve Azure Active Directory sağlama otomatik olarak bir kullanıcı için yapılandırma | Microsoft Docs"
description: "Bilgi nasıl toouse Workday kimlik verilerinin Active Directory ve Azure Active Directory için kaynak olarak."
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a><span data-ttu-id="5c160-103">Öğretici: Workday ile şirket içi Active Directory ve Azure Active Directory sağlama otomatik olarak bir kullanıcı için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5c160-103">Tutorial: Configure Workday for automatic user provisioning with on-premises Active Directory and Azure Active Directory</span></span>
<span data-ttu-id="5c160-104">Bu öğreticinin Hello hedefi tooperform tooimport Workday kişilerden Active Directory ve Azure Active Directory'de bazı öznitelikler tooWorkday isteğe bağlı geri yazma ile ihtiyacınız adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="5c160-104">hello objective of this tutorial is tooshow you hello steps you need tooperform tooimport people from Workday into both Active Directory and Azure Active Directory, with optional writeback of some attributes tooWorkday.</span></span> 



## <a name="overview"></a><span data-ttu-id="5c160-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5c160-105">Overview</span></span>

<span data-ttu-id="5c160-106">Merhaba [hizmet sağlama Azure Active Directory kullanıcı](active-directory-saas-app-provisioning.md) hello ile tümleşir [Workday İnsan Kaynakları API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) , kullanıcı hesaplarını tooprovision sipariş.</span><span class="sxs-lookup"><span data-stu-id="5c160-106">hello [Azure Active Directory user provisioning service](active-directory-saas-app-provisioning.md) integrates with hello [Workday Human Resources API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) in order tooprovision user accounts.</span></span> <span data-ttu-id="5c160-107">Azure AD kullanıcı sağlama iş akışları şu Bu bağlantı tooenable hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="5c160-107">Azure AD uses this connection tooenable hello following user provisioning workflows:</span></span>

* <span data-ttu-id="5c160-108">**Kullanıcıların tooActive Directory sağlama** -Workday kullanıcı seçili kümeleri bir veya daha fazla Active Directory ormanları eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-108">**Provisioning users tooActive Directory** - Synchronize selected sets of users from Workday into one or more Active Directory forests.</span></span> 

* <span data-ttu-id="5c160-109">**Yalnızca bulut kullanıcıları tooAzure Active Directory sağlama** -hello ikinci kullanarak Active Directory ve Azure Active Directory içinde mevcut karma kullanıcılar sağlanabilir [AAD Connect](connect/active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="5c160-109">**Provisioning cloud-only users tooAzure Active Directory** - Hybrid users who exist in both Active Directory and Azure Active Directory can be provisioned into hello latter using [AAD Connect](connect/active-directory-aadconnect.md).</span></span> <span data-ttu-id="5c160-110">Ancak, salt bulut olan kullanıcılar doğrudan tooAzure Active Directory'yi kullanarak Azure AD kullanıcısının hizmet sağlama hello Workday'den sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-110">However, users that are cloud-only can be provisioned directly from Workday tooAzure Active Directory using hello Azure AD user provisioning service.</span></span>

* <span data-ttu-id="5c160-111">**Geri yazma e-posta adresleri tooWorkday** -hizmet sağlama hello Azure AD kullanıcı seçili Azure AD kullanıcı öznitelikleri geri tooWorkday, hello e-posta adresi gibi yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-111">**Writeback of email addresses tooWorkday** - hello Azure AD user provisioning service can write selected Azure AD user attributes back tooWorkday, such as hello email address.</span></span>

### <a name="scenarios-covered"></a><span data-ttu-id="5c160-112">Kapsanan senaryolar</span><span class="sxs-lookup"><span data-stu-id="5c160-112">Scenarios covered</span></span>

<span data-ttu-id="5c160-113">Hizmet sağlama hello Azure AD kullanıcı tarafından desteklenen iş akışları sağlama hello Workday kullanıcı İnsan Kaynakları ve kimlik yaşam döngüsü yönetimi senaryoları aşağıdaki hello otomasyonunu sağlar:</span><span class="sxs-lookup"><span data-stu-id="5c160-113">hello Workday user provisioning workflows supported by hello Azure AD user provisioning service enables automation of hello following human resources and identity lifecycle management scenarios:</span></span>

* <span data-ttu-id="5c160-114">**Yeni çalışan işe alma** - tooWorkday, yeni bir çalışan eklendiğinde, bir kullanıcı hesabı otomatik olarak Active Directory, Azure Active Directory ve Office 365 isteğe bağlı olarak oluşturulur ve [Azure AD tarafından desteklenen diğer SaaS uygulamaları ](active-directory-saas-app-provisioning.md), hello e-posta adresi tooWorkday arkasına yazma ile.</span><span class="sxs-lookup"><span data-stu-id="5c160-114">**Hiring new employees** - When a new employee is added tooWorkday, a user account will be automatically created in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md), with write back of hello email address tooWorkday.</span></span>

* <span data-ttu-id="5c160-115">**Çalışan özniteliği ve profil güncelleştirmeleri** - zaman (kendi adı, başlık veya Yöneticisi gibi) bir çalışan kaydı iş günü içinde güncelleştirilir, kendi kullanıcı hesabına otomatik olarak Active Directory, Azure Active Directory ve Office 365 isteğe bağlı olarak güncelleştirilir ve [Azure AD tarafından desteklenen diğer SaaS uygulamaları](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="5c160-115">**Employee attribute and profile updates** - When an employee record is updated in Workday (such as their name, title, or manager), their user account will be automatically updated in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="5c160-116">**Çalışan sonlandırmalar** - çalışan iş günü içinde sonlandırıldığında kendi kullanıcı hesabına otomatik olarak Active Directory, Azure Active Directory ve Office 365 isteğe bağlı olarak devre dışıdır ve [Azure AD tarafından desteklenen diğer SaaS uygulamaları](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="5c160-116">**Employee terminations** - When an employee is terminated in Workday, their user account is automatically disabled in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="5c160-117">**Çalışan yeniden anlaşır** - çalışan iş günü içinde rehired eski hesaplarına otomatik olarak yeniden etkinleştiren (bağlı olarak, tercihinize) yeniden sağlanan tooActive Directory, Azure Active Directory ve isteğe bağlı olarak Office 365 ve veya[Azure AD tarafından desteklenen diğer SaaS uygulamaları](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="5c160-117">**Employee re-hires** - When an employee is rehired in Workday, their old account can be automatically reactivated or re-provisioned (depending on your preference) tooActive Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>


## <a name="planning-your-solution"></a><span data-ttu-id="5c160-118">Çözümünüzü planlarken</span><span class="sxs-lookup"><span data-stu-id="5c160-118">Planning your solution</span></span>

<span data-ttu-id="5c160-119">Merhaba önkoşulları aşağıdaki ve okuma hello nasıl hakkında yönergeler aşağıdaki denetleyin, Workday entegrasyonu başlamadan önce geçerli bir Active Directory mimarisi ve kullanıcı gereksinimlerini hazırlama hello Azure Active tarafından sağlanan solution(s) toomatch Dizin.</span><span class="sxs-lookup"><span data-stu-id="5c160-119">Before beginning your Workday integration, check hello prerequisites below and read hello following guidance on how toomatch your current Active Directory architecture and user provisioning requirements with hello solution(s) provided by Azure Active Directory.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5c160-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5c160-120">Prerequisites</span></span>

<span data-ttu-id="5c160-121">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="5c160-121">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="5c160-122">Genel yönetici erişimi olan geçerli bir Azure AD Premium P1 abonelik</span><span class="sxs-lookup"><span data-stu-id="5c160-122">A valid Azure AD Premium P1 subscription with global administrator access</span></span>
* <span data-ttu-id="5c160-123">Sınama ve tümleştirme amaçları için bir iş günü uygulama Kiracı</span><span class="sxs-lookup"><span data-stu-id="5c160-123">A Workday implementation tenant for testing and integration purposes</span></span>
* <span data-ttu-id="5c160-124">Workday toocreate sistem tümleştirme kullanıcı yönetici izinleri ve test amacıyla marka değişiklikleri tootest çalışan verilerini</span><span class="sxs-lookup"><span data-stu-id="5c160-124">Administrator permissions in Workday toocreate a system integration user, and make changes tootest employee data for testing purposes</span></span>
* <span data-ttu-id="5c160-125">TooActive Directory sağlama kullanıcı için 2012 veya daha fazla Windows hizmeti çalıştıran bir etki alanına katılmış gerekli toohost hello sunucusudur [şirket içi eşitleme Aracısı](https://go.microsoft.com/fwlink/?linkid=847801)</span><span class="sxs-lookup"><span data-stu-id="5c160-125">For user provisioning tooActive Directory, a domain-joined server running Windows Service 2012 or greater is required toohost hello [on-premises synchronization agent](https://go.microsoft.com/fwlink/?linkid=847801)</span></span>
* <span data-ttu-id="5c160-126">[Azure AD Connect](connect/active-directory-aadconnect.md) Active Directory ve Azure AD arasında eşitlemek için</span><span class="sxs-lookup"><span data-stu-id="5c160-126">[Azure AD Connect](connect/active-directory-aadconnect.md) for synchronizing between Active Directory and Azure AD</span></span>

> [!NOTE]
> <span data-ttu-id="5c160-127">Azure AD kiracınıza Avrupa'da bulunuyorsa, lütfen hello bakın [bilinen sorunlar](#known-issues) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="5c160-127">If your Azure AD tenant is located in Europe, please see hello [Known issues](#known-issues) section below.</span></span>


### <a name="solution-architecture"></a><span data-ttu-id="5c160-128">Çözüm mimarisi</span><span class="sxs-lookup"><span data-stu-id="5c160-128">Solution architecture</span></span>

<span data-ttu-id="5c160-129">Azure AD sağlama ve kimlik yaşam döngüsü yönetimi Workday tooActive Directory, Azure AD, SaaS uygulamaları ve ötesinde çözmek bağlayıcılar toohelp sağlama zengin bir özellik kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c160-129">Azure AD provides a rich set of provisioning connectors toohelp you solve provisioning and identity lifecycle management from Workday tooActive Directory, Azure AD, SaaS apps, and beyond.</span></span> <span data-ttu-id="5c160-130">Hangi özellikleri kullanır ve hello çözümü ayarlama nasıl kuruluşunuzun ortamlarına ve gereksinimlerine bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="5c160-130">Which features you will use and how you set up hello solution will vary depending on your organization's environment and requirements.</span></span> <span data-ttu-id="5c160-131">İlk adım olarak, mevcut ve kuruluşunuzdaki dağıtılan hello aşağıdaki kaç, hisse senedi alın:</span><span class="sxs-lookup"><span data-stu-id="5c160-131">As a first step, take stock of how many of hello following are present and deployed in your organization:</span></span>

* <span data-ttu-id="5c160-132">Kaç tane Active Directory ormanları kullanılıyor?</span><span class="sxs-lookup"><span data-stu-id="5c160-132">How many Active Directory Forests are in use?</span></span>
* <span data-ttu-id="5c160-133">Kaç tane Active Directory etki alanları kullanılıyor?</span><span class="sxs-lookup"><span data-stu-id="5c160-133">How many Active Directory Domains are in use?</span></span>
* <span data-ttu-id="5c160-134">Kaç tane Active Directory kuruluş birimlerini (OU) kullanılıyor?</span><span class="sxs-lookup"><span data-stu-id="5c160-134">How many Active Directory Organizational Units (OUs) are in use?</span></span>
* <span data-ttu-id="5c160-135">Kaç tane Azure Active Directory kiracıları kullanılıyor?</span><span class="sxs-lookup"><span data-stu-id="5c160-135">How many Azure Active Directory tenants are in use?</span></span>
* <span data-ttu-id="5c160-136">Sağlanan toobe tooboth Active Directory ve Azure Active Directory (örneğin "karma" kullanıcılar) ihtiyaç duyan kullanıcılar var mı?</span><span class="sxs-lookup"><span data-stu-id="5c160-136">Are there users who need toobe provisioned tooboth Active Directory and Azure Active Directory (e.g. "hybrid" users)?</span></span>
* <span data-ttu-id="5c160-137">Sağlanan toobe tooAzure Active Directory, ancak Active Directory değil (örneğin "yalnızca bulut" kullanıcılar) olması gereken kullanıcılar var mı?</span><span class="sxs-lookup"><span data-stu-id="5c160-137">Are there users who need toobe provisioned tooAzure Active Directory, but not Active Directory (e.g. "cloud-only" users)?</span></span>
* <span data-ttu-id="5c160-138">Kullanıcı e-posta adreslerini geri tooWorkday yazılan toobe gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="5c160-138">Do user email addresses need toobe written back tooWorkday?</span></span>

<span data-ttu-id="5c160-139">Yanıtlar toothese sorular olduktan sonra dağıtım başlangıç kılavuzu izleyerek aşağıdaki sağlama İş gününüzün planlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-139">Once you have answers toothese questions, you can plan your Workday provisioning deployment by following hello guidance below.</span></span>

#### <a name="using-provisioning-connector-apps"></a><span data-ttu-id="5c160-140">Sağlama bağlayıcı uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="5c160-140">Using provisioning connector apps</span></span>

<span data-ttu-id="5c160-141">Azure Active Directory Workday ve çok sayıda diğer SaaS uygulamaları için önceden tümleştirilmiş sağlama bağlayıcıları destekler.</span><span class="sxs-lookup"><span data-stu-id="5c160-141">Azure Active Directory supports pre-integrated provisioning connectors for Workday and a large number of other SaaS applications.</span></span> 

<span data-ttu-id="5c160-142">Tek bir sağlama bağlayıcı tek kaynak sistem API hello ile arabirimleri ve sağlama verileri tooa tek hedef sistem yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5c160-142">A single provisioning connector interfaces with hello API of a single source system, and helps provision data tooa single target system.</span></span> <span data-ttu-id="5c160-143">Azure AD destekleyen çoğu sağlama bağlayıcılar tek kaynak ve hedef sistem (örneğin, Azure AD tooServiceNow) için ve Kurulum hello uygulama ekleyerek hello Azure AD uygulama galerisinde ' (örneğin ServiceNow) söz konusu olabilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-143">Most provisioning connectors that Azure AD supports are for a single source and target system (e.g. Azure AD tooServiceNow), and can be setup by simply adding hello app in question from hello Azure AD app gallery (e.g. ServiceNow).</span></span> 

<span data-ttu-id="5c160-144">Azure AD'de sağlama bağlayıcı örnekleri ve app örnekleri arasında bire bir ilişki vardır:</span><span class="sxs-lookup"><span data-stu-id="5c160-144">There is a one-to-one relationship between provisioning connector instances and app instances in Azure AD:</span></span>

| <span data-ttu-id="5c160-145">Kaynak sistemi</span><span class="sxs-lookup"><span data-stu-id="5c160-145">Source System</span></span> | <span data-ttu-id="5c160-146">Hedef sistem</span><span class="sxs-lookup"><span data-stu-id="5c160-146">Target System</span></span> |
| ---------- | ---------- | 
| <span data-ttu-id="5c160-147">Azure AD kiracısı</span><span class="sxs-lookup"><span data-stu-id="5c160-147">Azure AD tenant</span></span> | <span data-ttu-id="5c160-148">SaaS uygulaması</span><span class="sxs-lookup"><span data-stu-id="5c160-148">SaaS application</span></span> |


<span data-ttu-id="5c160-149">Ancak, Workday ve Active Directory ile çalışırken, birden çok kaynak ve hedef sistemleri toobe ilgili olarak kabul vardır:</span><span class="sxs-lookup"><span data-stu-id="5c160-149">However, when working with Workday and Active Directory, there are multiple source and target systems toobe considered:</span></span>

| <span data-ttu-id="5c160-150">Kaynak sistemi</span><span class="sxs-lookup"><span data-stu-id="5c160-150">Source System</span></span> | <span data-ttu-id="5c160-151">Hedef sistem</span><span class="sxs-lookup"><span data-stu-id="5c160-151">Target System</span></span> | <span data-ttu-id="5c160-152">Notlar</span><span class="sxs-lookup"><span data-stu-id="5c160-152">Notes</span></span> |
| ---------- | ---------- | ---------- |
| <span data-ttu-id="5c160-153">İş günü</span><span class="sxs-lookup"><span data-stu-id="5c160-153">Workday</span></span> | <span data-ttu-id="5c160-154">Active Directory ormanı</span><span class="sxs-lookup"><span data-stu-id="5c160-154">Active Directory Forest</span></span> | <span data-ttu-id="5c160-155">Her bir orman ayrı hedef sistem olarak kabul edilir</span><span class="sxs-lookup"><span data-stu-id="5c160-155">Each forest is treated as a distinct target system</span></span> |
| <span data-ttu-id="5c160-156">İş günü</span><span class="sxs-lookup"><span data-stu-id="5c160-156">Workday</span></span> | <span data-ttu-id="5c160-157">Azure AD kiracısı</span><span class="sxs-lookup"><span data-stu-id="5c160-157">Azure AD tenant</span></span> | <span data-ttu-id="5c160-158">Yalnızca bulut kullanıcıları için gerektiği şekilde</span><span class="sxs-lookup"><span data-stu-id="5c160-158">As required for cloud-only users</span></span> |
| <span data-ttu-id="5c160-159">Active Directory ormanı</span><span class="sxs-lookup"><span data-stu-id="5c160-159">Active Directory Forest</span></span> | <span data-ttu-id="5c160-160">Azure AD kiracısı</span><span class="sxs-lookup"><span data-stu-id="5c160-160">Azure AD tenant</span></span> | <span data-ttu-id="5c160-161">Bu akış AAD Connect tarafından bugün işlenir</span><span class="sxs-lookup"><span data-stu-id="5c160-161">This flow is handled by AAD Connect today</span></span> |
| <span data-ttu-id="5c160-162">Azure AD kiracısı</span><span class="sxs-lookup"><span data-stu-id="5c160-162">Azure AD tenant</span></span> | <span data-ttu-id="5c160-163">İş günü</span><span class="sxs-lookup"><span data-stu-id="5c160-163">Workday</span></span> | <span data-ttu-id="5c160-164">E-posta adreslerini geri yazma için</span><span class="sxs-lookup"><span data-stu-id="5c160-164">For writeback of email addresses</span></span> |

<span data-ttu-id="5c160-165">Bu birden çok iş akışı toomultiple kaynak ve hedef sistemleri, Azure AD toofacilitate hello Azure AD uygulama Galerisi'nden ekleyebilirsiniz birden fazla sağlama bağlayıcı uygulamalar sağlar:</span><span class="sxs-lookup"><span data-stu-id="5c160-165">toofacilitate these multiple workflows toomultiple source and target systems, Azure AD provides multiple provisioning connector apps that you can add from hello Azure AD app gallery:</span></span>

![AAD uygulama Galerisi](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* <span data-ttu-id="5c160-167">**İş günü tooActive Directory sağlama** -kullanıcı hesabı Workday tooa tek Active Directory ormanından sağlama bu uygulamayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5c160-167">**Workday tooActive Directory Provisioning** - This app facilitates user account provisioning from Workday tooa single Active Directory forest.</span></span> <span data-ttu-id="5c160-168">Birden çok ormanınız varsa, bu uygulamanın bir örneği hello Azure AD uygulama galerisinde tooprovision için gereksinim duyduğunuz her Active Directory ormanı için ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-168">If you have multiple forests, you can add one instance of this app from hello Azure AD app gallery for each Active Directory forest you need tooprovision to.</span></span>

* <span data-ttu-id="5c160-169">**İş günü tooAzure AD sağlama** -sırada AAD Connect kullanılan toosynchronize Active Directory Kullanıcıları tooAzure Active Directory olmalıdır hello aracı, bu uygulama kullanılan toofacilitate olabilir Workday tooa tek yalnızca bulut kullanıcılardan sağlama Azure Active Directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="5c160-169">**Workday tooAzure AD Provisioning** - While AAD Connect is hello tool that should be used toosynchronize Active Directory users tooAzure Active Directory, this app can be used toofacilitate provisioning of cloud-only users from Workday tooa single Azure Active Directory tenant.</span></span>

* <span data-ttu-id="5c160-170">**İş günü geri yazma** -bu uygulamayı Azure Active Directory tooWorkday kullanıcının e-posta adresleri için geri yazma kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5c160-170">**Workday Writeback** - This app facilitates writeback of user's email addresses from Azure Active Directory tooWorkday.</span></span>

> [!TIP]
> <span data-ttu-id="5c160-171">Merhaba normal "Workday" uygulaması, çoklu oturum açma Workday ve Azure Active Directory arasında ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5c160-171">hello regular "Workday" app is used for setting up single sign-on between Workday and Azure Active Directory.</span></span> 

<span data-ttu-id="5c160-172">Nasıl tooset ayarlama ve bu özel yapılandırma olan bölümleri Bu öğreticinin kalan hello hello konusunun bağlayıcı uygulamalar sağlama.</span><span class="sxs-lookup"><span data-stu-id="5c160-172">How tooset up and configure these special provisioning connector apps is hello subject of hello remaining sections of this tutorial.</span></span> <span data-ttu-id="5c160-173">Tooconfigure hangi sistemlerinde tooprovision için ve kaç tane Active Directory ormanları ve Azure AD ihtiyacınız bağlıdır seçtiğiniz hangi kiracılar ortamınızda uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="5c160-173">Which apps you choose tooconfigure will depend on which systems you need tooprovision to, and how many Active Directory Forests and Azure AD tenants are in your environment.</span></span>

![Genel Bakış](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a><span data-ttu-id="5c160-175">Bir sistem tümleştirme kullanıcı iş günü içinde yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5c160-175">Configure a system integration user in Workday</span></span>
<span data-ttu-id="5c160-176">Bunlar bir iş günü sistem tümleştirme hesabı tooconnect toohello için Workday İnsan Kaynakları API kimlik bilgileri gerektiren tüm hello Workday sağlama bağlayıcı ortak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="5c160-176">A common requirement of all hello Workday provisioning connectors is they require credentials for a Workday system integration account tooconnect toohello Workday Human Resources API.</span></span> <span data-ttu-id="5c160-177">Bu bölümde, nasıl toocreate bir sistem Tümleştirici hesap iş günü içinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5c160-177">This section describes how toocreate a system integrator account in Workday.</span></span>

> [!NOTE]
> <span data-ttu-id="5c160-178">Bu yordam, olası toobypass kullanılır ve bunun yerine bir iş günü genel yönetici hello sistem tümleştirme aynı hesabı kullan.</span><span class="sxs-lookup"><span data-stu-id="5c160-178">It is possible toobypass this procedure and instead use a Workday global administrator account as hello system integration account.</span></span> <span data-ttu-id="5c160-179">Bu tanıtımları için düzgün çalışıyor, ancak üretim dağıtımları için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="5c160-179">This may work fine for demos, but is not recommended for production deployments.</span></span>

### <a name="create-an-integration-system-user"></a><span data-ttu-id="5c160-180">Tümleştirme sistemi kullanıcısı oluştur</span><span class="sxs-lookup"><span data-stu-id="5c160-180">Create an integration system user</span></span>

<span data-ttu-id="5c160-181">**Tümleştirme sistemi kullanıcısı toocreate:**</span><span class="sxs-lookup"><span data-stu-id="5c160-181">**toocreate an integration system user:**</span></span>

1. <span data-ttu-id="5c160-182">Workday Kiracı yönetici hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5c160-182">Sign into your Workday tenant using an administrator account.</span></span> <span data-ttu-id="5c160-183">Merhaba, **Workday çalışma ekranı**, girin hello arama kutusuna kullanıcı oluşturmak ve ardından **tümleştirme sistemi kullanıcısı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5c160-183">In hello **Workday Workbench**, enter create user in hello search box, and then click **Create Integration System User**.</span></span> 
   
    <span data-ttu-id="5c160-184">![Kullanıcı oluşturma](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "kullanıcı oluşturma")</span><span class="sxs-lookup"><span data-stu-id="5c160-184">![Create user](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Create user")</span></span>
2. <span data-ttu-id="5c160-185">Tam hello **tümleştirme sistemi kullanıcısı Oluştur** yeni bir tümleştirme sistemi kullanıcısı için bir kullanıcı adı ve parola sağlayarak görev.</span><span class="sxs-lookup"><span data-stu-id="5c160-185">Complete hello **Create Integration System User** task by supplying a user name and password for a new Integration System User.</span></span>  
 * <span data-ttu-id="5c160-186">Merhaba bırakın **gerektiren yeni parolayı sonraki oturum açma** seçeneği işaretsiz, bu kullanıcının program aracılığıyla oturum açan olduğundan.</span><span class="sxs-lookup"><span data-stu-id="5c160-186">Leave hello **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span></span> 
 * <span data-ttu-id="5c160-187">Merhaba bırakın **oturum zaman aşımı dakika** ile varsayılan değeri 0 olan engeller hello kullanıcı oturumları erken zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="5c160-187">Leave hello **Session Timeout Minutes** with its default value of 0, which will prevent hello user’s sessions from timing out prematurely.</span></span> 
   
    <span data-ttu-id="5c160-188">![Tümleştirme sistemi kullanıcısı Oluştur](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "tümleştirme sistemi kullanıcısı oluştur")</span><span class="sxs-lookup"><span data-stu-id="5c160-188">![Create Integration System User](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Create Integration System User")</span></span>

### <a name="create-a-security-group"></a><span data-ttu-id="5c160-189">Bir güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="5c160-189">Create a security group</span></span>
<span data-ttu-id="5c160-190">Merhaba kullanıcı tooit atayın ve toocreate bir Kısıtlanmamış tümleştirme sistemi güvenlik grubunu gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c160-190">You need toocreate an unconstrained integration system security group and assign hello user tooit.</span></span>

<span data-ttu-id="5c160-191">**toocreate bir güvenlik grubu:**</span><span class="sxs-lookup"><span data-stu-id="5c160-191">**toocreate a security group:**</span></span>

1. <span data-ttu-id="5c160-192">Girin hello arama kutusuna güvenlik grubu oluşturun ve ardından **güvenlik grubu oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="5c160-192">Enter create security group in hello search box, and then click **Create Security Group**.</span></span> 
   
    <span data-ttu-id="5c160-193">![Güvenlik grubu oluştur](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "güvenlik grubu oluştur")</span><span class="sxs-lookup"><span data-stu-id="5c160-193">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "CreateSecurity Group")</span></span>
2. <span data-ttu-id="5c160-194">Tam hello **güvenlik grubu oluşturma** görev.</span><span class="sxs-lookup"><span data-stu-id="5c160-194">Complete hello **Create Security Group** task.</span></span>  
3. <span data-ttu-id="5c160-195">Tümleştirme sistemi güvenlik grubu seç — hello Kısıtlanmamış **kiralanan güvenlik grubu türü** açılır.</span><span class="sxs-lookup"><span data-stu-id="5c160-195">Select Integration System Security Group—Unconstrained from hello **Type of Tenanted Security Group** dropdown.</span></span>
4. <span data-ttu-id="5c160-196">Üyeleri açıkça eklenen bir güvenlik grubu toowhich oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c160-196">Create a security group toowhich members will be explicitly added.</span></span> 
   
    <span data-ttu-id="5c160-197">![Güvenlik grubu oluştur](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "güvenlik grubu oluştur")</span><span class="sxs-lookup"><span data-stu-id="5c160-197">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "CreateSecurity Group")</span></span>

### <a name="assign-hello-integration-system-user-toohello-security-group"></a><span data-ttu-id="5c160-198">Merhaba tümleştirme sistem kullanıcı toohello güvenlik grubu atayın</span><span class="sxs-lookup"><span data-stu-id="5c160-198">Assign hello integration system user toohello security group</span></span>

<span data-ttu-id="5c160-199">**tooassign hello tümleştirme sistemi kullanıcısı:**</span><span class="sxs-lookup"><span data-stu-id="5c160-199">**tooassign hello integration system user:**</span></span>

1. <span data-ttu-id="5c160-200">Güvenlik grubunu Düzenle hello arama kutusuna girin ve ardından **güvenlik grubunu Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="5c160-200">Enter edit security group in hello search box, and then click **Edit Security Group**.</span></span> 
   
    <span data-ttu-id="5c160-201">![Güvenlik grubunu Düzenle](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "güvenlik grubunu Düzenle")</span><span class="sxs-lookup"><span data-stu-id="5c160-201">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Edit Security Group")</span></span>
2. <span data-ttu-id="5c160-202">Arama ve ada göre hello yeni tümleştirme güvenlik grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="5c160-202">Search for, and select hello new integration security group by name.</span></span> 
   
    <span data-ttu-id="5c160-203">![Güvenlik grubunu Düzenle](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "güvenlik grubunu Düzenle")</span><span class="sxs-lookup"><span data-stu-id="5c160-203">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Edit Security Group")</span></span>
3. <span data-ttu-id="5c160-204">Merhaba yeni tümleştirme sistemi kullanıcı toohello yeni güvenlik grubunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-204">Add hello new integration system user toohello new security group.</span></span> 
   
    <span data-ttu-id="5c160-205">![Sistem güvenlik grubu](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "sistem güvenlik grubu")</span><span class="sxs-lookup"><span data-stu-id="5c160-205">![System Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "System Security Group")</span></span>  

### <a name="configure-security-group-options"></a><span data-ttu-id="5c160-206">Güvenlik grubu seçeneklerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5c160-206">Configure security group options</span></span>
<span data-ttu-id="5c160-207">Bu adımda, toohello yeni güvenlik grubu için izinleri **almak** ve **Put** etki alanı güvenlik ilkeleri aşağıdaki hello tarafından güvenliği sağlanan hello nesneleri işlemleri:</span><span class="sxs-lookup"><span data-stu-id="5c160-207">In this step, you grant toohello new security group permissions for **Get** and **Put** operations on hello objects secured by hello following domain security policies:</span></span>

* <span data-ttu-id="5c160-208">Harici hesap sağlama</span><span class="sxs-lookup"><span data-stu-id="5c160-208">External Account Provisioning</span></span>
* <span data-ttu-id="5c160-209">Çalışan verileri: Ortak çalışan raporları</span><span class="sxs-lookup"><span data-stu-id="5c160-209">Worker Data: Public Worker Reports</span></span>
* <span data-ttu-id="5c160-210">Çalışan verileri: Tüm Pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="5c160-210">Worker Data: All Positions</span></span>
* <span data-ttu-id="5c160-211">Çalışan verileri: Geçerli personel bilgileri</span><span class="sxs-lookup"><span data-stu-id="5c160-211">Worker Data: Current Staffing Information</span></span>
* <span data-ttu-id="5c160-212">Çalışan verileri: Çalışan profilindeki iş başlığı</span><span class="sxs-lookup"><span data-stu-id="5c160-212">Worker Data: Business Title on Worker Profile</span></span>

<span data-ttu-id="5c160-213">**tooconfigure güvenlik grubu seçenekleri:**</span><span class="sxs-lookup"><span data-stu-id="5c160-213">**tooconfigure security group options:**</span></span>

1. <span data-ttu-id="5c160-214">Etki alanı güvenlik ilkeleri hello arama kutusuna girin ve sonra hello bağlantısını tıklatın **işlevsel alanı için etki alanı güvenlik ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="5c160-214">Enter domain security policies in hello search box, and then click on hello link **Domain Security Policies for Functional Area**.</span></span>  
   
    <span data-ttu-id="5c160-215">![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "etki alanı güvenlik ilkeleri")</span><span class="sxs-lookup"><span data-stu-id="5c160-215">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Domain Security Policies")</span></span>  
2. <span data-ttu-id="5c160-216">Sistem ve select hello arama **sistem** işlevsel alan.</span><span class="sxs-lookup"><span data-stu-id="5c160-216">Search for system and select hello **System** functional area.</span></span>  <span data-ttu-id="5c160-217">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c160-217">Click **OK**.</span></span>  
   
    <span data-ttu-id="5c160-218">![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "etki alanı güvenlik ilkeleri")</span><span class="sxs-lookup"><span data-stu-id="5c160-218">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Domain Security Policies")</span></span>  
3. <span data-ttu-id="5c160-219">Merhaba sistem işlevsel alan için güvenlik ilkelerini Hello listesinde genişletin **güvenlik Yönetim** seçip hello etki alanı güvenlik ilkesi **Harici hesap sağlama**.</span><span class="sxs-lookup"><span data-stu-id="5c160-219">In hello list of security policies for hello System functional area, expand **Security Administration** and select hello domain security policy **External Account Provisioning**.</span></span>  
   
    <span data-ttu-id="5c160-220">![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "etki alanı güvenlik ilkeleri")</span><span class="sxs-lookup"><span data-stu-id="5c160-220">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Domain Security Policies")</span></span>  
4. <span data-ttu-id="5c160-221">Tıklatın **izinleri Düzenle**ve ardından hello **izinleri Düzenle**iletişim sayfasında, hello yeni güvenlik grubu toohello listesi güvenlik grupları eklemek **almak** ve **Put** tümleştirme izinleri.</span><span class="sxs-lookup"><span data-stu-id="5c160-221">Click **Edit Permissions**, and then, on hello **Edit Permissions**dialog page, add hello new security group toohello list of security groups with **Get** and **Put** integration permissions.</span></span> 
   
    <span data-ttu-id="5c160-222">![İzni Düzenle](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "düzenleme izni")</span><span class="sxs-lookup"><span data-stu-id="5c160-222">![Edit Permission](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Edit Permission")</span></span>  
5. <span data-ttu-id="5c160-223">İşlevsel alanlara seçme tooreturn toohello ekran yukarıdaki 1. adım ve bu süre, personel, arama seçin hello yineleyin **işlevsel alan personel** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5c160-223">Repeat step 1 above tooreturn toohello screen for selecting functional areas, and this time, search for staffing, select hello **Staffing functional area** and click **OK**.</span></span>
   
    <span data-ttu-id="5c160-224">![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "etki alanı güvenlik ilkeleri")</span><span class="sxs-lookup"><span data-stu-id="5c160-224">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Domain Security Policies")</span></span>  
6. <span data-ttu-id="5c160-225">Merhaba Staffing işlevsel alan için güvenlik ilkelerini Hello listesinde genişletin **çalışan verileri: Staffing** ve bunların güvenlik ilkeleri kalan her biri için adımı yukarıdaki 4 yineleyin:</span><span class="sxs-lookup"><span data-stu-id="5c160-225">In hello list of security policies for hello Staffing functional area, expand **Worker Data: Staffing** and repeat step 4 above for each of these remaining security policies:</span></span>

   * <span data-ttu-id="5c160-226">Çalışan verileri: Ortak çalışan raporları</span><span class="sxs-lookup"><span data-stu-id="5c160-226">Worker Data: Public Worker Reports</span></span>
   * <span data-ttu-id="5c160-227">Çalışan verileri: Tüm Pozisyonlar</span><span class="sxs-lookup"><span data-stu-id="5c160-227">Worker Data: All Positions</span></span>
   * <span data-ttu-id="5c160-228">Çalışan verileri: Geçerli personel bilgileri</span><span class="sxs-lookup"><span data-stu-id="5c160-228">Worker Data: Current Staffing Information</span></span>
   * <span data-ttu-id="5c160-229">Çalışan verileri: Çalışan profilindeki iş başlığı</span><span class="sxs-lookup"><span data-stu-id="5c160-229">Worker Data: Business Title on Worker Profile</span></span>
   
7. <span data-ttu-id="5c160-230">Yineleme adım 1 ' seçeneğini belirleyerek işlevsel alan tooreturn toohello ekranı üzerinde ve bu süre, arama için **irtibat bilgileri**hello Staffing işlevsel alanı seçin ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5c160-230">Repeat step 1, above, tooreturn toohello screen for selecting  functional areas, and this time, search for **Contact Information**,  select hello Staffing functional area, and click **OK**.</span></span>

8.  <span data-ttu-id="5c160-231">Merhaba Staffing işlevsel alan için güvenlik ilkelerini Hello listesinde genişletin **çalışan verileri: çalışma kişi bilgilerini**ve yineleme yukarıda adım 4'hello güvenlik ilkeleri için:</span><span class="sxs-lookup"><span data-stu-id="5c160-231">In hello list of security policies for hello Staffing functional area, expand **Worker Data: Work Contact Information**, and repeat step 4 above for hello security policies below:</span></span>

    * <span data-ttu-id="5c160-232">Çalışan verileri: İş e-posta</span><span class="sxs-lookup"><span data-stu-id="5c160-232">Worker Data: Work Email</span></span>

    <span data-ttu-id="5c160-233">![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "etki alanı güvenlik ilkeleri")</span><span class="sxs-lookup"><span data-stu-id="5c160-233">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Domain Security Policies")</span></span>  
    
### <a name="activate-security-policy-changes"></a><span data-ttu-id="5c160-234">Güvenlik İlkesi değişikliklerini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-234">Activate security policy changes</span></span>

<span data-ttu-id="5c160-235">**tooactivate güvenlik ilkesi değişikliklerini:**</span><span class="sxs-lookup"><span data-stu-id="5c160-235">**tooactivate security policy changes:**</span></span>

1. <span data-ttu-id="5c160-236">Girin hello arama kutusuna etkinleştirin ve daha sonra hello bağlantıdaki **etkinleştirme bekleyen güvenlik ilkesi değişikliklerini**.</span><span class="sxs-lookup"><span data-stu-id="5c160-236">Enter activate in hello search box, and then click on hello link **Activate Pending Security Policy Changes**.</span></span> 
   
    <span data-ttu-id="5c160-237">![Etkinleştirme](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "etkinleştir")</span><span class="sxs-lookup"><span data-stu-id="5c160-237">![Activate](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Activate")</span></span> 
2. <span data-ttu-id="5c160-238">Bekleyen Güvenlik İlkesi değişikliklerini etkinleştir görev denetim amacıyla bir açıklama girin ve ardından başlangıç hello **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5c160-238">Begin hello Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then click **OK**.</span></span> 
   
    <span data-ttu-id="5c160-239">![Bekleyen güvenlik ayarlarını etkinleştir](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "bekleyen güvenlik ayarlarını etkinleştir")</span><span class="sxs-lookup"><span data-stu-id="5c160-239">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Activate Pending Security")</span></span>   
3. <span data-ttu-id="5c160-240">Tam hello görev hello onay kutusunu işaretleyerek hello sonraki ekranında **Onayla**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5c160-240">Complete hello task on hello next screen by checking hello checkbox **Confirm**, and then click **OK**.</span></span> 
   
    <span data-ttu-id="5c160-241">![Bekleyen güvenlik ayarlarını etkinleştir](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "bekleyen güvenlik ayarlarını etkinleştir")</span><span class="sxs-lookup"><span data-stu-id="5c160-241">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Activate Pending Security")</span></span>  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a><span data-ttu-id="5c160-242">Workday tooActive Directory kullanıcı sağlamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5c160-242">Configuring user provisioning from Workday tooActive Directory</span></span>
<span data-ttu-id="5c160-243">Workday tooeach için sağlama gerektiren Active Directory ormanı'ndan sağlama bu yönergeleri tooconfigure kullanıcı hesabı izleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-243">Follow these instructions tooconfigure user account provisioning from Workday tooeach Active Directory forest that you require provisioning to.</span></span>

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a><span data-ttu-id="5c160-244">1. Kısım: hello sağlama bağlayıcı uygulama ekleme ve hello bağlantı tooWorkday oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c160-244">Part 1: Adding hello provisioning connector app and creating hello connection tooWorkday</span></span>

<span data-ttu-id="5c160-245">**tooconfigure Workday tooActive Directory sağlama:**</span><span class="sxs-lookup"><span data-stu-id="5c160-245">**tooconfigure Workday tooActive Directory provisioning:**</span></span>

1.  <span data-ttu-id="5c160-246">Çok Git<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="5c160-246">Go too<https://portal.azure.com></span></span>

2.  <span data-ttu-id="5c160-247">Merhaba sol gezinti çubuğunda seçin **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="5c160-247">In hello left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="5c160-248">Seçin **kurumsal uygulamalar**, ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5c160-248">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="5c160-249">Seçin **bir uygulama eklemek**ve select hello **tüm** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="5c160-249">Select **Add an application**, and select hello **All** category.</span></span>

5.  <span data-ttu-id="5c160-250">Arama **Workday sağlama tooActive dizin**ve bu uygulama hello Galerisi'nden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-250">Search for **Workday Provisioning tooActive Directory**, and add that app from hello gallery.</span></span>

6.  <span data-ttu-id="5c160-251">Merhaba sonra uygulama eklenir ve hello uygulama ayrıntıları ekran gösterilir, seçin **sağlama**</span><span class="sxs-lookup"><span data-stu-id="5c160-251">After hello app is added and hello app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="5c160-252">Değişiklik hello **sağlama** **modu** çok**otomatik**</span><span class="sxs-lookup"><span data-stu-id="5c160-252">Change hello **Provisioning** **Mode** too**Automatic**</span></span>

8.  <span data-ttu-id="5c160-253">Tam hello **yönetici kimlik bilgileri** gibi bölümünde:</span><span class="sxs-lookup"><span data-stu-id="5c160-253">Complete hello **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="5c160-254">**Yönetici kullanıcı adı** – eklenmiş hello Kiracı etki alanı adıyla hello kullanıcı hello Workday entegrasyonu sistem hesabı adını girin.</span><span class="sxs-lookup"><span data-stu-id="5c160-254">**Admin Username** – Enter hello username of hello Workday integration system account, with hello tenant domain name appended.</span></span> <span data-ttu-id="5c160-255">**Gibi görünmelidir:username@contoso4**</span><span class="sxs-lookup"><span data-stu-id="5c160-255">**Should look something like: username@contoso4**</span></span>

   * <span data-ttu-id="5c160-256">**Yönetici parolası –** hello Workday entegrasyonu sistem hesabı, hello parola gir</span><span class="sxs-lookup"><span data-stu-id="5c160-256">**Admin password –** Enter hello password of hello Workday    integration system account</span></span>

   * <span data-ttu-id="5c160-257">**Kiracı URL –** hello URL toohello Workday web hizmetleri uç kiracınız için girin.</span><span class="sxs-lookup"><span data-stu-id="5c160-257">**Tenant URL –** Enter hello URL toohello Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="5c160-258">Aşağıdaki gibi görünmelidir: https://wd3-impl-services1.workday.com/ccx/service/contoso4, burada contoso4 doğru Kiracı adınız ile değiştirilir ve wd3 impl hello doğru ortamı dize ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-258">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with hello correct environment string.</span></span>

   * <span data-ttu-id="5c160-259">**Active Directory ormanı -** hello Get-ADForest powershell komutunu tarafından döndürülen Active Directory ormanınızın "Name" Merhaba.</span><span class="sxs-lookup"><span data-stu-id="5c160-259">**Active Directory Forest -** hello “Name” of your Active Directory forest, as returned by hello Get-ADForest powershell commandlet.</span></span> <span data-ttu-id="5c160-260">Bu genellikle bir dize gibi olur: *contoso.com*</span><span class="sxs-lookup"><span data-stu-id="5c160-260">This is typically a string like: *contoso.com*</span></span>

   * <span data-ttu-id="5c160-261">**Active Directory kapsayıcısı -** hello kapsayıcı AD ormanınızdaki tüm kullanıcıları içeren bir dize girin.</span><span class="sxs-lookup"><span data-stu-id="5c160-261">**Active Directory Container -** Enter hello container string that contains all users in your AD forest.</span></span> <span data-ttu-id="5c160-262">Örnek: *OU standart kullanıcılar, OU = Kullanıcılar, DC = contoso, DC = test =*</span><span class="sxs-lookup"><span data-stu-id="5c160-262">Example: *OU=Standard Users,OU=Users,DC=contoso,DC=test*</span></span>

   * <span data-ttu-id="5c160-263">**Bildirim e-posta –** e-posta adresinizi girin ve "hatası oluşursa, e-posta Gönder" onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-263">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="5c160-264">Merhaba tıklatın **Bağlantıyı Sına** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5c160-264">Click hello **Test Connection** button.</span></span> <span data-ttu-id="5c160-265">Merhaba bağlantı testi başarılı olursa, hello tıklatın **kaydetmek** hello üst düğmesini.</span><span class="sxs-lookup"><span data-stu-id="5c160-265">If hello connection test succeeds, click hello **Save** button at hello top.</span></span> <span data-ttu-id="5c160-266">Başarısız olursa hello Workday kimlik iş günü içinde geçerli olduğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-266">If it fails, double-check that hello Workday credentials are valid in Workday.</span></span> 

![Azure portalına](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="5c160-268">2. Kısım: öznitelik eşlemelerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5c160-268">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="5c160-269">Bu bölümde, kullanıcı verilerini Workday'deki Active Directory ile nasıl akacağını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5c160-269">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="5c160-270">Merhaba sağlama sekmesinde altında **eşlemeleri**, tıklatın **eşitleme Workday çalışanları tooOnPremises**.</span><span class="sxs-lookup"><span data-stu-id="5c160-270">On hello Provisioning tab under **Mappings**, click **Synchronize Workday Workers tooOnPremises**.</span></span>

2.  <span data-ttu-id="5c160-271">Merhaba, **kaynak nesne kapsamı** alan, hangi kullanıcı kümeleri için iş günü içinde öznitelik tabanlı bir filtre kümesi tanımlayarak tooAD, sağlama kapsamında olmalıdır seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-271">In hello **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning tooAD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="5c160-272">"tüm kullanıcılar iş günü içinde" Hello varsayılan kapsamıdır.</span><span class="sxs-lookup"><span data-stu-id="5c160-272">hello default scope is “all users in Workday”.</span></span> <span data-ttu-id="5c160-273">Örnek filtreler:</span><span class="sxs-lookup"><span data-stu-id="5c160-273">Example filters:</span></span>

   * <span data-ttu-id="5c160-274">Örnek: Çalışan kimlikleri toousers 1000000 2000000 arasındaki kapsam</span><span class="sxs-lookup"><span data-stu-id="5c160-274">Example: Scope toousers with Worker IDs between 1000000 and    2000000</span></span>

      * <span data-ttu-id="5c160-275">Öznitelik: WorkerID</span><span class="sxs-lookup"><span data-stu-id="5c160-275">Attribute: WorkerID</span></span>

      * <span data-ttu-id="5c160-276">İşleci: REGEX eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="5c160-276">Operator: REGEX Match</span></span>

      * <span data-ttu-id="5c160-277">Değer: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="5c160-277">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="5c160-278">Örnek: Yalnızca çalışanlar ve değil contingent çalışanları</span><span class="sxs-lookup"><span data-stu-id="5c160-278">Example: Only employees and not contingent workers</span></span> 

      * <span data-ttu-id="5c160-279">Öznitelik: EmployeeID</span><span class="sxs-lookup"><span data-stu-id="5c160-279">Attribute: EmployeeID</span></span>

      * <span data-ttu-id="5c160-280">İşleci: NULL değil</span><span class="sxs-lookup"><span data-stu-id="5c160-280">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="5c160-281">Merhaba, **hedef nesne eylemleri** alan, genel filtre uygulayabilirsiniz hangi eylemleri Active Directory üzerinde gerçekleştirilen toobe izin verilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-281">In hello **Target Object Actions** field, you can globally filter what actions are allowed toobe performed on Active Directory.</span></span> <span data-ttu-id="5c160-282">**Oluşturma** ve **güncelleştirme** en sık kullanılan.</span><span class="sxs-lookup"><span data-stu-id="5c160-282">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="5c160-283">Merhaba, **öznitelik eşlemelerini** bölümünde, tek tek nasıl Workday harita tooActive dizin özniteliklerini öznitelikleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-283">In hello **Attribute mappings** section, you can define how individual Workday attributes map tooActive Directory attributes.</span></span>

5. <span data-ttu-id="5c160-284">Üzerinde var olan bir öznitelik eşleme tooupdate tıklatın veya tıklatın **yeni eklemesi** Merhaba ekranında tooadd yeni eşlemeler hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="5c160-284">Click on an existing attribute mapping tooupdate it, or click **Add new mapping** at hello bottom of hello screen tooadd new mappings.</span></span> <span data-ttu-id="5c160-285">Bir tek özniteliği eşlemesi bu özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="5c160-285">An individual attribute mapping supports these properties:</span></span>

      * <span data-ttu-id="5c160-286">**Eşleme türü**</span><span class="sxs-lookup"><span data-stu-id="5c160-286">**Mapping Type**</span></span>

         * <span data-ttu-id="5c160-287">**Doğrudan** – hello hello Workday özniteliği toohello AD özniteliğinin değeri, hiçbir değişiklik olmadan yazar</span><span class="sxs-lookup"><span data-stu-id="5c160-287">**Direct** – Writes hello value of hello Workday attribute      toohello AD attribute, with no changes</span></span>

         * <span data-ttu-id="5c160-288">**Sabit** -hello AD özniteliği için bir statik, sabit dize değeri yazma</span><span class="sxs-lookup"><span data-stu-id="5c160-288">**Constant** - Write a static, constant string value to      hello AD attribute</span></span>

         * <span data-ttu-id="5c160-289">**İfade** – toowrite hello AD özniteliği, bir veya daha fazla iş günü özniteliklerini temel alarak özel bir değere izin verir.</span><span class="sxs-lookup"><span data-stu-id="5c160-289">**Expression** – Allows you toowrite a custom value to hello AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="5c160-290">[Daha fazla bilgi için bu makalede ifadeleri bkz](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="5c160-290">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

      * <span data-ttu-id="5c160-291">**Kaynak özniteliği** -Workday hello kullanıcı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5c160-291">**Source attribute** - hello user attribute from Workday.</span></span>

      * <span data-ttu-id="5c160-292">**Varsayılan değer** – isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5c160-292">**Default value** – Optional.</span></span> <span data-ttu-id="5c160-293">Merhaba eşleme Hello kaynak özniteliği boş bir değer varsa, bu değer yerine yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5c160-293">If hello source attribute has an empty value, hello mapping will write this value instead.</span></span>
            <span data-ttu-id="5c160-294">Bu boş tooleave en yaygın yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="5c160-294">Most common configuration is tooleave this blank.</span></span>

      * <span data-ttu-id="5c160-295">**Hedef öznitelik** – hello Active Directory'deki kullanıcı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5c160-295">**Target attribute** – hello user attribute in Active     Directory.</span></span>

      * <span data-ttu-id="5c160-296">**Eşleşen nesneleri bu öznitelik kullanarak** – Bu eşleme kullanılmalıdır olup olmadığına bakılmaksızın toouniquely kullanıcılar Workday ve Active Directory arasında tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="5c160-296">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between Workday and Active Directory.</span></span> <span data-ttu-id="5c160-297">Bu genellikle, çalışan kimliği alanı genellikle hello çalışan kimliği öznitelikleri Active Directory'de birine eşlenmiş iş günü için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5c160-297">This is typically set on the Worker ID field for Workday, which is typically mapped to one of hello Employee ID attributes in Active Directory.</span></span>

      * <span data-ttu-id="5c160-298">**Öncelik eşleşen** – birden çok öznitelikleri eşleşen ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-298">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="5c160-299">Olduğunda birden çok, bu alana göre tanımlanan sırayla değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-299">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="5c160-300">Bir eşleşme olarak başka eşleştirme öznitelikleri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-300">As soon as a match is found, no further matching attributes are evaluated.</span></span>

      * <span data-ttu-id="5c160-301">**Bu eşleme Uygula**</span><span class="sxs-lookup"><span data-stu-id="5c160-301">**Apply this mapping**</span></span>
       
         * <span data-ttu-id="5c160-302">**Her zaman** – hem kullanıcı oluşturulması bu eşleme uygulamak ve güncelleştirme eylemleri</span><span class="sxs-lookup"><span data-stu-id="5c160-302">**Always** – Apply this mapping on both user creation      and update actions</span></span>

         * <span data-ttu-id="5c160-303">**Yalnızca oluşturma sırasında** -bu eşlemenin yalnızca kullanıcı oluşturma eylemlerini uygulamak</span><span class="sxs-lookup"><span data-stu-id="5c160-303">**Only during creation** - Apply this mapping only on      user creation actions</span></span>

6. <span data-ttu-id="5c160-304">toosave, eşlemeleri tıklatın **kaydetmek** eşleme özniteliği bölümünün hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="5c160-304">toosave your mappings, click **Save** at hello top of the      Attribute Mapping section.</span></span>

![Azure portalına](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

<span data-ttu-id="5c160-306">**Aşağıda bazı örnek, bazı ortak ifadelerle Workday ve Active Directory arasında öznitelik eşlemelerini verilmiştir**</span><span class="sxs-lookup"><span data-stu-id="5c160-306">**Below are some example attribute mappings between Workday and Active Directory, with some common expressions**</span></span>

-   <span data-ttu-id="5c160-307">toohello parentDistinguishedName AD özniteliği eşlemeleri hello ifade kullanılan tooprovision belirli OU bir veya daha fazla iş günü kaynak özniteliklerini temel alarak bir kullanıcı tooa olabilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-307">hello expression that maps toohello parentDistinguishedName AD attribute can be used tooprovision a user tooa specific OU based on one or more Workday source attributes.</span></span> <span data-ttu-id="5c160-308">Bu örnek kullanıcılar Şehir verilerine bağlı olarak farklı OU'lar iş günü içinde yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="5c160-308">This example places users in different OUs depending on their city data in Workday.</span></span>

-   <span data-ttu-id="5c160-309">toohello userPrincipalName AD özniteliği eşlemeleri hello ifadesi oluşturma UPN firstName.LastName@contoso.com. Geçersiz özel karakterler yerini alır.</span><span class="sxs-lookup"><span data-stu-id="5c160-309">hello expression that maps toohello userPrincipalName AD attribute create a UPN of firstName.LastName@contoso.com. It also replaces illegal special characters.</span></span>

-   [<span data-ttu-id="5c160-310">Burada ifadeleri yazma belge yok</span><span class="sxs-lookup"><span data-stu-id="5c160-310">There is documentation on writing expressions here</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| <span data-ttu-id="5c160-311">İŞ GÜNÜ ÖZNİTELİĞİ</span><span class="sxs-lookup"><span data-stu-id="5c160-311">WORKDAY ATTRIBUTE</span></span> | <span data-ttu-id="5c160-312">ACTIVE DIRECTORY ÖZNİTELİĞİ</span><span class="sxs-lookup"><span data-stu-id="5c160-312">ACTIVE DIRECTORY ATTRIBUTE</span></span> |  <span data-ttu-id="5c160-313">KİMLİĞİ EŞLEŞİYOR MU?</span><span class="sxs-lookup"><span data-stu-id="5c160-313">MATCHING ID?</span></span> | <span data-ttu-id="5c160-314">OLUŞTUR / GÜNCELLEŞTİR</span><span class="sxs-lookup"><span data-stu-id="5c160-314">CREATE / UPDATE</span></span> |
| ---------- | ---------- | ---------- | ---------- |
|  <span data-ttu-id="5c160-315">**WorkerID**</span><span class="sxs-lookup"><span data-stu-id="5c160-315">**WorkerID**</span></span>  |  <span data-ttu-id="5c160-316">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="5c160-316">EmployeeID</span></span> | <span data-ttu-id="5c160-317">**Evet**</span><span class="sxs-lookup"><span data-stu-id="5c160-317">**Yes**</span></span> | <span data-ttu-id="5c160-318">Yazılan üzerinde yalnızca oluştur</span><span class="sxs-lookup"><span data-stu-id="5c160-318">Written on create only</span></span> | 
|  <span data-ttu-id="5c160-319">**Belediye**</span><span class="sxs-lookup"><span data-stu-id="5c160-319">**Municipality**</span></span>   |   <span data-ttu-id="5c160-320">m</span><span class="sxs-lookup"><span data-stu-id="5c160-320">l</span></span>   |     | <span data-ttu-id="5c160-321">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-321">Create + update</span></span> |
|  <span data-ttu-id="5c160-322">**Şirket**</span><span class="sxs-lookup"><span data-stu-id="5c160-322">**Company**</span></span>         | <span data-ttu-id="5c160-323">Şirket</span><span class="sxs-lookup"><span data-stu-id="5c160-323">company</span></span>   |     |  <span data-ttu-id="5c160-324">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-324">Create + update</span></span> |
|  <span data-ttu-id="5c160-325">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="5c160-325">**CountryReferenceTwoLetter**</span></span>      |   <span data-ttu-id="5c160-326">Ortak</span><span class="sxs-lookup"><span data-stu-id="5c160-326">co</span></span> |     |   <span data-ttu-id="5c160-327">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-327">Create + update</span></span> |
| <span data-ttu-id="5c160-328">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="5c160-328">**CountryReferenceTwoLetter**</span></span>    |  <span data-ttu-id="5c160-329">C</span><span class="sxs-lookup"><span data-stu-id="5c160-329">c</span></span>  |     |         <span data-ttu-id="5c160-330">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-330">Create + update</span></span> |
| <span data-ttu-id="5c160-331">**SupervisoryOrganization**</span><span class="sxs-lookup"><span data-stu-id="5c160-331">**SupervisoryOrganization**</span></span>  | <span data-ttu-id="5c160-332">Bölüm</span><span class="sxs-lookup"><span data-stu-id="5c160-332">department</span></span>  |     |  <span data-ttu-id="5c160-333">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-333">Create + update</span></span> |
|  <span data-ttu-id="5c160-334">**PreferredNameData**</span><span class="sxs-lookup"><span data-stu-id="5c160-334">**PreferredNameData**</span></span>  |  <span data-ttu-id="5c160-335">Görünen adı</span><span class="sxs-lookup"><span data-stu-id="5c160-335">displayName</span></span> |     |   <span data-ttu-id="5c160-336">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-336">Create + update</span></span> |
| <span data-ttu-id="5c160-337">**EmployeeID**</span><span class="sxs-lookup"><span data-stu-id="5c160-337">**EmployeeID**</span></span>    |  <span data-ttu-id="5c160-338">CN =</span><span class="sxs-lookup"><span data-stu-id="5c160-338">cn</span></span>    |   |   <span data-ttu-id="5c160-339">Yazılan üzerinde yalnızca oluştur</span><span class="sxs-lookup"><span data-stu-id="5c160-339">Written on create only</span></span> |
| <span data-ttu-id="5c160-340">**Faks**</span><span class="sxs-lookup"><span data-stu-id="5c160-340">**Fax**</span></span>      | <span data-ttu-id="5c160-341">facsimileTelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="5c160-341">facsimileTelephoneNumber</span></span>     |     |    <span data-ttu-id="5c160-342">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-342">Create + update</span></span> |
| <span data-ttu-id="5c160-343">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="5c160-343">**FirstName**</span></span>   | <span data-ttu-id="5c160-344">givenName</span><span class="sxs-lookup"><span data-stu-id="5c160-344">givenName</span></span>       |     |    <span data-ttu-id="5c160-345">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-345">Create + update</span></span> |
| <span data-ttu-id="5c160-346">**Anahtar (\[etkin\],, "0", "True", "1")**</span><span class="sxs-lookup"><span data-stu-id="5c160-346">**Switch(\[Active\], , "0", "True", "1",)**</span></span> |  <span data-ttu-id="5c160-347">AccountDisabled</span><span class="sxs-lookup"><span data-stu-id="5c160-347">accountDisabled</span></span>      |     | <span data-ttu-id="5c160-348">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-348">Create + update</span></span> |
| <span data-ttu-id="5c160-349">**Mobil**</span><span class="sxs-lookup"><span data-stu-id="5c160-349">**Mobile**</span></span>  |    <span data-ttu-id="5c160-350">Mobil</span><span class="sxs-lookup"><span data-stu-id="5c160-350">mobile</span></span>       |     |       <span data-ttu-id="5c160-351">Yazılan üzerinde yalnızca oluştur</span><span class="sxs-lookup"><span data-stu-id="5c160-351">Written on create only</span></span> |
| <span data-ttu-id="5c160-352">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="5c160-352">**EmailAddress**</span></span>    | <span data-ttu-id="5c160-353">Posta</span><span class="sxs-lookup"><span data-stu-id="5c160-353">mail</span></span>    |     |     <span data-ttu-id="5c160-354">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-354">Create + update</span></span> |
| <span data-ttu-id="5c160-355">**ManagerReference**</span><span class="sxs-lookup"><span data-stu-id="5c160-355">**ManagerReference**</span></span>   | <span data-ttu-id="5c160-356">Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="5c160-356">manager</span></span>  |     |  <span data-ttu-id="5c160-357">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-357">Create + update</span></span> |
| <span data-ttu-id="5c160-358">**WorkSpaceReference**</span><span class="sxs-lookup"><span data-stu-id="5c160-358">**WorkSpaceReference**</span></span> | <span data-ttu-id="5c160-359">physicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="5c160-359">physicalDeliveryOfficeName</span></span>    |     |  <span data-ttu-id="5c160-360">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-360">Create + update</span></span> |
| <span data-ttu-id="5c160-361">**Posta kodu**</span><span class="sxs-lookup"><span data-stu-id="5c160-361">**PostalCode**</span></span>  |   <span data-ttu-id="5c160-362">posta kodu</span><span class="sxs-lookup"><span data-stu-id="5c160-362">postalCode</span></span>  |     | <span data-ttu-id="5c160-363">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-363">Create + update</span></span> |
| <span data-ttu-id="5c160-364">**LocalReference**</span><span class="sxs-lookup"><span data-stu-id="5c160-364">**LocalReference**</span></span> |  <span data-ttu-id="5c160-365">preferredLanguage</span><span class="sxs-lookup"><span data-stu-id="5c160-365">preferredLanguage</span></span>  |     |  <span data-ttu-id="5c160-366">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-366">Create + update</span></span> |
| <span data-ttu-id="5c160-367">** Değiştirin (Mid (Değiştir (\[EmployeeID\],, "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span><span class="sxs-lookup"><span data-stu-id="5c160-367">**Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span></span>|<span data-ttu-id="5c160-368">\\\\=\\\\,\\\\+\\\\\*\\\\?\\ \\ &lt; \\ \\ &gt; \]) "," ",), 1, 20)," ([\\\\.) \* \$] (file:///\\.) *$)", , "", , )**</span><span class="sxs-lookup"><span data-stu-id="5c160-368">\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**</span></span>      |    <span data-ttu-id="5c160-369">SAMAccountName</span><span class="sxs-lookup"><span data-stu-id="5c160-369">sAMAccountName</span></span>            |     |         <span data-ttu-id="5c160-370">Yazılan üzerinde yalnızca oluştur</span><span class="sxs-lookup"><span data-stu-id="5c160-370">Written on create only</span></span> |
| <span data-ttu-id="5c160-371">**Soyadı**</span><span class="sxs-lookup"><span data-stu-id="5c160-371">**LastName**</span></span>   |   <span data-ttu-id="5c160-372">sn</span><span class="sxs-lookup"><span data-stu-id="5c160-372">sn</span></span>   |     |  <span data-ttu-id="5c160-373">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-373">Create + update</span></span> |
| <span data-ttu-id="5c160-374">**CountryRegionReference**</span><span class="sxs-lookup"><span data-stu-id="5c160-374">**CountryRegionReference**</span></span> |  <span data-ttu-id="5c160-375">St</span><span class="sxs-lookup"><span data-stu-id="5c160-375">st</span></span>     |     | <span data-ttu-id="5c160-376">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-376">Create + update</span></span> |
| <span data-ttu-id="5c160-377">**AddressLineData**</span><span class="sxs-lookup"><span data-stu-id="5c160-377">**AddressLineData**</span></span>    |  <span data-ttu-id="5c160-378">StreetAddress</span><span class="sxs-lookup"><span data-stu-id="5c160-378">streetAddress</span></span>  |     |   <span data-ttu-id="5c160-379">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-379">Create + update</span></span> |
| <span data-ttu-id="5c160-380">**PrimaryWorkTelephone**</span><span class="sxs-lookup"><span data-stu-id="5c160-380">**PrimaryWorkTelephone**</span></span>  |  <span data-ttu-id="5c160-381">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="5c160-381">telephoneNumber</span></span>   |     | <span data-ttu-id="5c160-382">Yazılan üzerinde yalnızca oluştur</span><span class="sxs-lookup"><span data-stu-id="5c160-382">Written on create only</span></span> |
| <span data-ttu-id="5c160-383">**BusinessTitle**</span><span class="sxs-lookup"><span data-stu-id="5c160-383">**BusinessTitle**</span></span>   |  <span data-ttu-id="5c160-384">Başlık</span><span class="sxs-lookup"><span data-stu-id="5c160-384">title</span></span>     |     |  <span data-ttu-id="5c160-385">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-385">Create + update</span></span> |
| <span data-ttu-id="5c160-386">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])" ,, "m",), "([ñńňÑŃŇN])", "n",), "([öòőõôóÖÒŐÕÔÓO])", "o",), "([P])", "p",), "([Q])", "q",), "([řŘR])", "r",), "([ßšśŠŚS])", "s",), "([TŤť])", "t",), "([üùûúůűÜÙÛÚŮŰU])", "u",), "([V])", "v",), "([]) w" harfinin, "w",), "([ýÿýŸÝY])", "y",), "([źžżŹŽŻZ])", "z",), "",,, "",), "contoso.com")**</span><span class="sxs-lookup"><span data-stu-id="5c160-386">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**</span></span>   | <span data-ttu-id="5c160-387">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="5c160-387">userPrincipalName</span></span>     |     | <span data-ttu-id="5c160-388">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-388">Create + update</span></span>                                                   
| <span data-ttu-id="5c160-389">**Anahtar (\[belediye\], "OU standart kullanıcılar, OU = Kullanıcılar, OU = varsayılan, OU = konumları, DC = contoso, DC = com =", "Dallas" "OU standart kullanıcılar, OU = Kullanıcılar, OU = Dallas, OU = konumları, DC = contoso, DC = com =", "Ankara'da" "OU standart kullanıcılar, OU = Kullanıcılar, OU = Ankara'da, OU = konumları, DC = contoso, DC = com =", "Seattle", "OU standart kullanıcılar, OU = Kullanıcılar, OU = Seattle, OU = konumları, DC = contoso, DC = com =", "Londra", "OU standart kullanıcılar = OU Kullanıcılar, OU = Londra, OU = konumları, DC = contoso, DC = com = ")**</span><span class="sxs-lookup"><span data-stu-id="5c160-389">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span></span>  | <span data-ttu-id="5c160-390">parentDistinguishedName</span><span class="sxs-lookup"><span data-stu-id="5c160-390">parentDistinguishedName</span></span>     |     |  <span data-ttu-id="5c160-391">Oluştur + güncelleştir</span><span class="sxs-lookup"><span data-stu-id="5c160-391">Create + update</span></span> |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a><span data-ttu-id="5c160-392">3. Kısım: hello şirket içi eşitleme Aracısı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5c160-392">Part 3: Configure hello on-premises synchronization agent</span></span>

<span data-ttu-id="5c160-393">Sipariş tooprovision tooActive şirket içi dizin, bir aracı hello desire Active Directory ormanındaki bir etki alanına katılmış sunucuda yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c160-393">In order tooprovision tooActive Directory on-premises, an agent must be installed on a domain-joined server in hello desire Active Directory forest.</span></span> <span data-ttu-id="5c160-394">Merhaba yordamı tamamlamak için gerekli kimlik bilgileri etki alanı yöneticisi (veya Kurumsal Yönetici).</span><span class="sxs-lookup"><span data-stu-id="5c160-394">Domain admin (or Enterprise admin) credentials are required to complete hello procedure.</span></span>

<span data-ttu-id="5c160-395">**[Hello şirket içi eşitleme Aracısı buradan indirebilirsiniz](https://go.microsoft.com/fwlink/?linkid=847801)**</span><span class="sxs-lookup"><span data-stu-id="5c160-395">**[You can download hello on-premises synchronization agent here](https://go.microsoft.com/fwlink/?linkid=847801)**</span></span>

<span data-ttu-id="5c160-396">Aracıyı yükledikten sonra ortamınız için tooconfigure hello Aracısı aşağıda hello Powershell komutlarını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c160-396">After installing agent, run hello Powershell commands below tooconfigure hello agent for your environment.</span></span>

<span data-ttu-id="5c160-397">**#1 komutu**</span><span class="sxs-lookup"><span data-stu-id="5c160-397">**Command #1**</span></span>

> <span data-ttu-id="5c160-398">CD C:\\Program dosyaları\\Microsoft Azure Active Directory Eşitleme Aracı\\modülleri\\AADSyncAgent</span><span class="sxs-lookup"><span data-stu-id="5c160-398">cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent</span></span>

> <span data-ttu-id="5c160-399">Import-module AADSyncAgent.psd1</span><span class="sxs-lookup"><span data-stu-id="5c160-399">import-module AADSyncAgent.psd1</span></span>

<span data-ttu-id="5c160-400">**Komut #2**</span><span class="sxs-lookup"><span data-stu-id="5c160-400">**Command #2**</span></span>

> <span data-ttu-id="5c160-401">Ekleme ADSyncAgentActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c160-401">Add-ADSyncAgentActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="5c160-402">Giriş: "Dizin", başlangıç AD orman adı, kısmen girildiği gibi adı \#2</span><span class="sxs-lookup"><span data-stu-id="5c160-402">Input: For "Directory Name", enter hello AD Forest name, as entered in part \#2</span></span>
* <span data-ttu-id="5c160-403">Giriş: Yönetici kullanıcı adı ve parolası Active Directory ormanı için</span><span class="sxs-lookup"><span data-stu-id="5c160-403">Input: Admin username and password for Active Directory forest</span></span>

<span data-ttu-id="5c160-404">**Komut #3**</span><span class="sxs-lookup"><span data-stu-id="5c160-404">**Command #3**</span></span>

> <span data-ttu-id="5c160-405">Ekleme ADSyncAgentAzureActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c160-405">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="5c160-406">Giriş: Genel yönetici kullanıcı adı ve parola Azure AD kiracınız için</span><span class="sxs-lookup"><span data-stu-id="5c160-406">Input: Global admin username and password for your Azure AD tenant</span></span>

<span data-ttu-id="5c160-407">**Komut #4**</span><span class="sxs-lookup"><span data-stu-id="5c160-407">**Command #4**</span></span>

> <span data-ttu-id="5c160-408">Get-AdSyncAgentProvisioningTasks</span><span class="sxs-lookup"><span data-stu-id="5c160-408">Get-AdSyncAgentProvisioningTasks</span></span>

* <span data-ttu-id="5c160-409">Eylem: veriler döndürülür onaylayın.</span><span class="sxs-lookup"><span data-stu-id="5c160-409">Action: Confirm data is returned.</span></span> <span data-ttu-id="5c160-410">Bu komut, Azure AD kiracınıza uygulamalarında sağlama Workday otomatik olarak bulur.</span><span class="sxs-lookup"><span data-stu-id="5c160-410">This command automatically discovers Workday provisioning apps in your Azure AD tenant.</span></span> <span data-ttu-id="5c160-411">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="5c160-411">Example output:</span></span>

> <span data-ttu-id="5c160-412">Ad: AD Ormanım</span><span class="sxs-lookup"><span data-stu-id="5c160-412">Name          : My AD Forest</span></span>
>
> <span data-ttu-id="5c160-413">Etkin: True</span><span class="sxs-lookup"><span data-stu-id="5c160-413">Enabled       : True</span></span>
>
> <span data-ttu-id="5c160-414">DirectoryName: mydomain.contoso.com</span><span class="sxs-lookup"><span data-stu-id="5c160-414">DirectoryName : mydomain.contoso.com</span></span>
>
> <span data-ttu-id="5c160-415">Belgeli: yanlış</span><span class="sxs-lookup"><span data-stu-id="5c160-415">Credentialed  : False</span></span>
>
> <span data-ttu-id="5c160-416">Tanımlayıcı: WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span><span class="sxs-lookup"><span data-stu-id="5c160-416">Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span></span>

<span data-ttu-id="5c160-417">**Komut #5**</span><span class="sxs-lookup"><span data-stu-id="5c160-417">**Command #5**</span></span>

> <span data-ttu-id="5c160-418">Start-AdSyncAgentSynchronization-otomatik</span><span class="sxs-lookup"><span data-stu-id="5c160-418">Start-AdSyncAgentSynchronization -Automatic</span></span>

<span data-ttu-id="5c160-419">**Komut #6**</span><span class="sxs-lookup"><span data-stu-id="5c160-419">**Command #6**</span></span>

> <span data-ttu-id="5c160-420">net stop aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="5c160-420">net stop aadsyncagent</span></span>

<span data-ttu-id="5c160-421">**Komut #7**</span><span class="sxs-lookup"><span data-stu-id="5c160-421">**Command #7**</span></span>

> <span data-ttu-id="5c160-422">net start aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="5c160-422">net start aadsyncagent</span></span>

### <a name="part-4-start-hello-service"></a><span data-ttu-id="5c160-423">4. Kısım: Başlangıç hello hizmeti</span><span class="sxs-lookup"><span data-stu-id="5c160-423">Part 4: Start hello service</span></span>
<span data-ttu-id="5c160-424">Bölümleri 1-3 tamamladıktan sonra hello Azure Yönetim Portalı geri hizmetinde sağlama hello başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-424">Once parts 1-3 have been completed, you can start hello provisioning service back in hello Azure Management Portal.</span></span>

1.  <span data-ttu-id="5c160-425">Merhaba, **sağlama** sekmesi, kümesi hello **sağlama durumu** için **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="5c160-425">In hello **Provisioning** tab, set hello **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="5c160-426">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c160-426">Click **Save**.</span></span>

3. <span data-ttu-id="5c160-427">Bu değişken sayıda iş günü içinde kaç kullanıcılardır bağlı olarak saatler sürebilir hello ilk eşitlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="5c160-427">This will start hello initial sync, which can take a variable number of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="5c160-428">Hangi kullanıcıların gibi bireysel eşitleme olayları dışında Workday okunur ve ardından sonradan eklenen veya güncelleştirilen tooActive dizin görüntülenebilir hello **denetim günlüklerini** sekmesi. **[Ayrıntılı yönergeler için raporlama Kılavuzu nasıl tooread hello denetim günlüklerini üzerinde sağlama hello bakın](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="5c160-428">Individual sync events such as what users are being read out of  Workday, and then subsequently added or updated tooActive Directory,  can be viewed in hello **Audit Logs** tab. **[See hello provisioning reporting guide for detailed instructions on how tooread hello audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5.  <span data-ttu-id="5c160-429">Merhaba aracı makine üzerindeki Hello Windows Uygulama günlüğü hello Aracısı üzerinden gerçekleştirilen tüm işlemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="5c160-429">hello Windows Application log on hello agent machine will show all operations performed via hello agent.</span></span>

6. <span data-ttu-id="5c160-430">Bir tamamlandı, onu bir denetim özet raporu yazacak **sağlama** sekmesinde, aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="5c160-430">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

![Azure portalına](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a><span data-ttu-id="5c160-432">Kullanıcı tooAzure Active Directory hazırlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5c160-432">Configuring user provisioning tooAzure Active Directory</span></span>
<span data-ttu-id="5c160-433">Sağlama tooAzure Active Directory nasıl yapılandırdığınıza hello tabloda ayrıntılı olarak sağlama gereksinimlerinizi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5c160-433">How you configure provisioning tooAzure Active Directory will depend on your provisioning requirements, as detailed in hello table below.</span></span>

| <span data-ttu-id="5c160-434">Senaryo</span><span class="sxs-lookup"><span data-stu-id="5c160-434">Scenario</span></span> | <span data-ttu-id="5c160-435">Çözüm</span><span class="sxs-lookup"><span data-stu-id="5c160-435">Solution</span></span> |
| -------- | -------- |
| <span data-ttu-id="5c160-436">**Sağlanan toobe tooActive Directory ve Azure AD kullanıcıların gerekir**</span><span class="sxs-lookup"><span data-stu-id="5c160-436">**Users need toobe provisioned tooActive Directory and Azure AD**</span></span> | <span data-ttu-id="5c160-437">Kullanım  **[AAD bağlanma](connect/active-directory-aadconnect.md)**</span><span class="sxs-lookup"><span data-stu-id="5c160-437">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="5c160-438">**Kullanıcılar gerek sağlanan toobe tooActive Directory yalnızca**</span><span class="sxs-lookup"><span data-stu-id="5c160-438">**Users need toobe provisioned tooActive Directory only**</span></span> | <span data-ttu-id="5c160-439">Kullanım  **[AAD bağlanma](connect/active-directory-aadconnect.md)**</span><span class="sxs-lookup"><span data-stu-id="5c160-439">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="5c160-440">**Kullanıcıların, sağlanan toobe tooAzure AD yalnızca (yalnızca bulutta) gerekir.**</span><span class="sxs-lookup"><span data-stu-id="5c160-440">**Users need toobe provisioned tooAzure AD only (cloud only)**</span></span> | <span data-ttu-id="5c160-441">Kullanım hello **Workday tooAzure Active Directory sağlama** hello uygulama galerisinde uygulama</span><span class="sxs-lookup"><span data-stu-id="5c160-441">Use hello **Workday tooAzure Active Directory provisioning** app in hello app gallery</span></span> |

<span data-ttu-id="5c160-442">Azure AD Connect ayarlama hakkında yönergeler için bkz: Merhaba [Azure AD Connect belgelerini](connect/active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="5c160-442">For instructions on setting up Azure AD Connect, see hello [Azure AD Connect documentation](connect/active-directory-aadconnect.md).</span></span>

<span data-ttu-id="5c160-443">Aşağıdaki bölümlerde hello Workday ve Azure AD tooprovision yalnızca bulut kullanıcıları arasında bir bağlantı ayarı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5c160-443">hello following sections describe setting up a connection between Workday and Azure AD tooprovision cloud-only users.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c160-444">Sağlanan toobe tooAzure AD ve şirket içi Active Directory olması gereken yalnızca bulut kullanıcılar varsa, yalnızca aşağıdaki hello yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-444">Only follow hello procedure below if you have cloud-only users that need toobe provisioned tooAzure AD and not on-premises Active Directory.</span></span>

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a><span data-ttu-id="5c160-445">1. Kısım: hello Azure AD sağlama bağlayıcı uygulama ekleme ve hello bağlantı tooWorkday oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c160-445">Part 1: Adding hello Azure AD provisioning connector app and creating hello connection tooWorkday</span></span>

<span data-ttu-id="5c160-446">**tooconfigure Workday tooAzure yalnızca bulut kullanıcıları için Active Directory sağlama:**</span><span class="sxs-lookup"><span data-stu-id="5c160-446">**tooconfigure Workday tooAzure Active Directory provisioning for cloud-only users:**</span></span>

1.  <span data-ttu-id="5c160-447">Çok Git<https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="5c160-447">Go too<https://portal.azure.com>.</span></span>

2.  <span data-ttu-id="5c160-448">Merhaba sol gezinti çubuğunda seçin **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="5c160-448">In hello left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="5c160-449">Seçin **kurumsal uygulamalar**, ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5c160-449">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="5c160-450">Seçin **bir uygulama eklemek**ve ardından hello **tüm** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="5c160-450">Select **Add an application**, and then select hello **All** category.</span></span>

5.  <span data-ttu-id="5c160-451">Arama **Workday tooAzure AD sağlama**ve bu uygulama hello Galerisi'nden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-451">Search for **Workday tooAzure AD provisioning**, and add that app from hello gallery.</span></span>

6.  <span data-ttu-id="5c160-452">Merhaba sonra uygulama eklenir ve hello uygulama ayrıntıları ekran gösterilir, seçin **sağlama**</span><span class="sxs-lookup"><span data-stu-id="5c160-452">After hello app is added and hello app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="5c160-453">Değişiklik hello **sağlama** **modu** çok**otomatik**</span><span class="sxs-lookup"><span data-stu-id="5c160-453">Change hello **Provisioning** **Mode** too**Automatic**</span></span>

8.  <span data-ttu-id="5c160-454">Tam hello **yönetici kimlik bilgileri** gibi bölümünde:</span><span class="sxs-lookup"><span data-stu-id="5c160-454">Complete hello **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="5c160-455">**Yönetici kullanıcı adı** – eklenmiş hello Kiracı etki alanı adıyla hello kullanıcı hello Workday entegrasyonu sistem hesabı adını girin.</span><span class="sxs-lookup"><span data-stu-id="5c160-455">**Admin Username** – Enter hello username of hello Workday integration system account, with hello tenant domain name appended.</span></span> <span data-ttu-id="5c160-456">Gibi görünmelidir:username@contoso4</span><span class="sxs-lookup"><span data-stu-id="5c160-456">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="5c160-457">**Yönetici parolası –** hello Workday entegrasyonu sistem hesabı, hello parola gir</span><span class="sxs-lookup"><span data-stu-id="5c160-457">**Admin password –** Enter hello password of hello Workday    integration system account</span></span>

   * <span data-ttu-id="5c160-458">**Kiracı URL –** hello URL toohello Workday web hizmetleri uç kiracınız için girin.</span><span class="sxs-lookup"><span data-stu-id="5c160-458">**Tenant URL –** Enter hello URL toohello Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="5c160-459">Aşağıdaki gibi görünmelidir: https://wd3-impl-services1.workday.com/ccx/service/contoso4, burada contoso4 doğru Kiracı adınız ile değiştirilir ve (gerekirse) wd3 impl hello doğru ortamı dize ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-459">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with hello correct environment string (if necessary).</span></span>

   * <span data-ttu-id="5c160-460">**Bildirim e-posta –** e-posta adresinizi girin ve "hatası oluşursa, e-posta Gönder" onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-460">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="5c160-461">Merhaba tıklatın **Bağlantıyı Sına** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5c160-461">Click hello **Test Connection** button.</span></span>

   * <span data-ttu-id="5c160-462">Merhaba bağlantı testi başarılı olursa, hello tıklatın **kaydetmek** hello üst düğmesini.</span><span class="sxs-lookup"><span data-stu-id="5c160-462">If hello connection test succeeds, click hello **Save** button at hello top.</span></span> <span data-ttu-id="5c160-463">Başarısız olursa, o hello Workday URL'si iki kez kontrol edin ve kimlik bilgilerini iş günü içinde geçerli.</span><span class="sxs-lookup"><span data-stu-id="5c160-463">If it fails, double-check that hello Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="5c160-464">2. Kısım: öznitelik eşlemelerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5c160-464">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="5c160-465">Bu bölümde, kullanıcı verilerini Workday'deki Azure Active Directory'ye yalnızca bulut kullanıcıları için nasıl akacağını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5c160-465">In this section, you will configure how user data flows from Workday to Azure Active Directory for cloud-only users.</span></span>

1.  <span data-ttu-id="5c160-466">Merhaba sağlama sekmesinde altında **eşlemeleri**, tıklatın **eşitleme çalışanları tooAzure AD**.</span><span class="sxs-lookup"><span data-stu-id="5c160-466">On hello Provisioning tab under **Mappings**, click **Synchronize Workers tooAzure AD**.</span></span>

2.   <span data-ttu-id="5c160-467">Merhaba, **kaynak nesne kapsamı** alan, hangi kullanıcı kümeleri için iş günü içinde öznitelik tabanlı bir filtre kümesi tanımlayarak tooAzure AD, sağlama kapsamında olmalıdır seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-467">In hello **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning tooAzure AD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="5c160-468">"tüm kullanıcılar iş günü içinde" Hello varsayılan kapsamıdır.</span><span class="sxs-lookup"><span data-stu-id="5c160-468">hello default scope is “all users in Workday”.</span></span> <span data-ttu-id="5c160-469">Örnek filtreler:</span><span class="sxs-lookup"><span data-stu-id="5c160-469">Example filters:</span></span>

   * <span data-ttu-id="5c160-470">Örnek: Çalışan kimlikleri toousers 1000000 2000000 arasındaki kapsam</span><span class="sxs-lookup"><span data-stu-id="5c160-470">Example: Scope toousers with Worker IDs between 1000000 and   2000000</span></span>

      * <span data-ttu-id="5c160-471">Öznitelik: WorkerID</span><span class="sxs-lookup"><span data-stu-id="5c160-471">Attribute: WorkerID</span></span>

      * <span data-ttu-id="5c160-472">İşleci: REGEX eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="5c160-472">Operator: REGEX Match</span></span>

      * <span data-ttu-id="5c160-473">Değer: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="5c160-473">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="5c160-474">Örnek: Yalnızca contingent çalışanları ve değil Normal çalışanlar</span><span class="sxs-lookup"><span data-stu-id="5c160-474">Example: Only contingent workers and not regular employees</span></span>

      * <span data-ttu-id="5c160-475">Öznitelik: ContingentID</span><span class="sxs-lookup"><span data-stu-id="5c160-475">Attribute: ContingentID</span></span>

      * <span data-ttu-id="5c160-476">İşleci: NULL değil</span><span class="sxs-lookup"><span data-stu-id="5c160-476">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="5c160-477">Merhaba, **hedef nesne eylemleri** alan, genel filtre uygulayabilirsiniz hangi eylemleri üzerinde Azure AD gerçekleştirilen toobe izin verilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-477">In hello **Target Object Actions** field, you can globally filter what actions are allowed toobe performed on Azure AD.</span></span> <span data-ttu-id="5c160-478">**Oluşturma** ve **güncelleştirme** en sık kullanılan.</span><span class="sxs-lookup"><span data-stu-id="5c160-478">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="5c160-479">Merhaba, **öznitelik eşlemelerini** bölümünde, tek tek nasıl Workday harita tooActive dizin özniteliklerini öznitelikleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-479">In hello **Attribute mappings** section, you can define how individual Workday attributes map tooActive Directory attributes.</span></span>

5. <span data-ttu-id="5c160-480">Üzerinde var olan bir öznitelik eşleme tooupdate tıklatın veya tıklatın **yeni eklemesi** Merhaba ekranında tooadd yeni eşlemeler hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="5c160-480">Click on an existing attribute mapping tooupdate it, or click **Add new mapping** at hello bottom of hello screen tooadd new mappings.</span></span> <span data-ttu-id="5c160-481">Bir tek özniteliği eşlemesi bu özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="5c160-481">An individual attribute mapping supports these properties:</span></span>

   * <span data-ttu-id="5c160-482">**Eşleme türü**</span><span class="sxs-lookup"><span data-stu-id="5c160-482">**Mapping Type**</span></span>

      * <span data-ttu-id="5c160-483">**Doğrudan** – hello hello Workday özniteliği toohello AD özniteliğinin değeri, hiçbir değişiklik olmadan yazar</span><span class="sxs-lookup"><span data-stu-id="5c160-483">**Direct** – Writes hello value of hello Workday attribute         toohello AD attribute, with no changes</span></span>

      * <span data-ttu-id="5c160-484">**Sabit** -hello AD özniteliği için bir statik, sabit dize değeri yazma</span><span class="sxs-lookup"><span data-stu-id="5c160-484">**Constant** - Write a static, constant string value to         hello AD attribute</span></span>

      * <span data-ttu-id="5c160-485">**İfade** – toowrite hello AD özniteliği, bir veya daha fazla iş günü özniteliklerini temel alarak özel bir değere izin verir.</span><span class="sxs-lookup"><span data-stu-id="5c160-485">**Expression** – Allows you toowrite a custom value to hello AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="5c160-486">[Daha fazla bilgi için bu makalede ifadeleri bkz](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="5c160-486">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

   * <span data-ttu-id="5c160-487">**Kaynak özniteliği** -Workday hello kullanıcı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5c160-487">**Source attribute** - hello user attribute from Workday.</span></span>

   * <span data-ttu-id="5c160-488">**Varsayılan değer** – isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5c160-488">**Default value** – Optional.</span></span> <span data-ttu-id="5c160-489">Merhaba eşleme Hello kaynak özniteliği boş bir değer varsa, bu değer yerine yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5c160-489">If hello source attribute has an empty value, hello mapping will write this value instead.</span></span>
            <span data-ttu-id="5c160-490">Bu boş tooleave en yaygın yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="5c160-490">Most common configuration is tooleave this blank.</span></span>

   * <span data-ttu-id="5c160-491">**Hedef öznitelik** – Azure AD'de hello kullanıcı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5c160-491">**Target attribute** – hello user attribute in Azure AD.</span></span>

   * <span data-ttu-id="5c160-492">**Eşleşen nesneleri bu öznitelik kullanarak** – Bu eşleme kullanılmalıdır olup olmadığına bakılmaksızın toouniquely kullanıcılar Workday ve Azure AD arasında tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="5c160-492">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between Workday and Azure AD.</span></span> <span data-ttu-id="5c160-493">Bu genellikle, çalışan kimliği alanı genellikle Azure AD'de hello çalışan ID özniteliği (yeni) ya da uzantı özniteliği eşlenen iş günü için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5c160-493">This is typically set on the Worker ID field for Workday, which is typically mapped to hello Employee ID attribute (new) or an extension attribute in Azure AD.</span></span>

   * <span data-ttu-id="5c160-494">**Öncelik eşleşen** – birden çok öznitelikleri eşleşen ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-494">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="5c160-495">Olduğunda birden çok, bu alana göre tanımlanan sırayla değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-495">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="5c160-496">Bir eşleşme olarak başka eşleştirme öznitelikleri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-496">As soon as a match is found, no further matching attributes are evaluated.</span></span>

   * <span data-ttu-id="5c160-497">**Bu eşleme Uygula**</span><span class="sxs-lookup"><span data-stu-id="5c160-497">**Apply this mapping**</span></span>

     * <span data-ttu-id="5c160-498">**Her zaman** – hem kullanıcı oluşturulması bu eşleme uygulamak ve güncelleştirme eylemleri</span><span class="sxs-lookup"><span data-stu-id="5c160-498">**Always** – Apply this mapping on both user creation          and update actions</span></span>

     * <span data-ttu-id="5c160-499">**Yalnızca oluşturma sırasında** -bu eşlemenin yalnızca kullanıcı oluşturma eylemlerini uygulamak</span><span class="sxs-lookup"><span data-stu-id="5c160-499">**Only during creation** - Apply this mapping only on          user creation actions</span></span>

6. <span data-ttu-id="5c160-500">toosave, eşlemeleri tıklatın **kaydetmek** eşleme özniteliği bölümünün hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="5c160-500">toosave your mappings, click **Save** at hello top of the      Attribute Mapping section.</span></span>

### <a name="part-3-start-hello-service"></a><span data-ttu-id="5c160-501">3. Kısım: Başlangıç hello hizmeti</span><span class="sxs-lookup"><span data-stu-id="5c160-501">Part 3: Start hello service</span></span>
<span data-ttu-id="5c160-502">Bölümleri 1-2 tamamladıktan sonra hizmet sağlama hello başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-502">Once parts 1-2 have been completed, you can start hello provisioning service.</span></span>

1.  <span data-ttu-id="5c160-503">Merhaba, **sağlama** sekmesi, kümesi hello **sağlama durumu** için **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="5c160-503">In hello **Provisioning** tab, set hello **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="5c160-504">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c160-504">Click **Save**.</span></span>

3. <span data-ttu-id="5c160-505">Bu değişken sayıda iş günü içinde kaç kullanıcılardır bağlı olarak saatler sürebilir hello ilk eşitlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="5c160-505">This will start hello initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="5c160-506">Bireysel eşitleme olayları hello görüntülenebilir **denetim günlüklerini** sekmesi. **[Ayrıntılı yönergeler için raporlama Kılavuzu nasıl tooread hello denetim günlüklerini üzerinde sağlama hello bakın](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="5c160-506">Individual sync events can be viewed in hello **Audit Logs** tab. **[See hello provisioning reporting guide for detailed instructions on how tooread hello audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="5c160-507">Bir tamamlandı, onu bir denetim özet raporu yazacak **sağlama** sekmesinde, aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="5c160-507">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a><span data-ttu-id="5c160-508">E-posta adresleri tooWorkday geri yazma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5c160-508">Configuring writeback of email addresses tooWorkday</span></span>
<span data-ttu-id="5c160-509">Kullanıcı e-posta adreslerini bu yönergeleri tooconfigure geri yazma, Azure Active Directory tooWorkday izleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-509">Follow these instructions tooconfigure writeback of user email addresses from Azure Active Directory tooWorkday.</span></span>

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a><span data-ttu-id="5c160-510">1. Kısım: hello sağlama bağlayıcı uygulama ekleme ve hello bağlantı tooWorkday oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c160-510">Part 1: Adding hello provisioning connector app and creating hello connection tooWorkday</span></span>

<span data-ttu-id="5c160-511">**tooconfigure Workday tooActive Directory sağlama:**</span><span class="sxs-lookup"><span data-stu-id="5c160-511">**tooconfigure Workday tooActive Directory provisioning:**</span></span>

1.  <span data-ttu-id="5c160-512">Çok Git<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="5c160-512">Go too<https://portal.azure.com></span></span>

2.  <span data-ttu-id="5c160-513">Merhaba sol gezinti çubuğunda seçin **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="5c160-513">In hello left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="5c160-514">Seçin **kurumsal uygulamalar**, ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5c160-514">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="5c160-515">Seçin **bir uygulama eklemek**seçeneğini belirleyip hello **tüm** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="5c160-515">Select **Add an application**, then select hello **All** category.</span></span>

5.  <span data-ttu-id="5c160-516">Arama **Workday geri yazma**ve bu uygulama hello Galerisi'nden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-516">Search for **Workday Writeback**, and add that app from hello gallery.</span></span>

6.  <span data-ttu-id="5c160-517">Merhaba sonra uygulama eklenir ve hello uygulama ayrıntıları ekran gösterilir, seçin **sağlama**</span><span class="sxs-lookup"><span data-stu-id="5c160-517">After hello app is added and hello app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="5c160-518">Değişiklik hello **sağlama** **modu** çok**otomatik**</span><span class="sxs-lookup"><span data-stu-id="5c160-518">Change hello **Provisioning** **Mode** too**Automatic**</span></span>

8.  <span data-ttu-id="5c160-519">Tam hello **yönetici kimlik bilgileri** gibi bölümünde:</span><span class="sxs-lookup"><span data-stu-id="5c160-519">Complete hello **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="5c160-520">**Yönetici kullanıcı adı** – eklenmiş hello Kiracı etki alanı adıyla hello kullanıcı hello Workday entegrasyonu sistem hesabı adını girin.</span><span class="sxs-lookup"><span data-stu-id="5c160-520">**Admin Username** – Enter hello username of hello Workday integration system account, with hello tenant domain name appended.</span></span> <span data-ttu-id="5c160-521">Gibi görünmelidir:username@contoso4</span><span class="sxs-lookup"><span data-stu-id="5c160-521">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="5c160-522">**Yönetici parolası –** hello Workday entegrasyonu sistem hesabı, hello parola gir</span><span class="sxs-lookup"><span data-stu-id="5c160-522">**Admin password –** Enter hello password of hello Workday    integration system account</span></span>

   * <span data-ttu-id="5c160-523">**Kiracı URL –** hello URL toohello Workday web hizmetleri uç kiracınız için girin.</span><span class="sxs-lookup"><span data-stu-id="5c160-523">**Tenant URL –** Enter hello URL toohello Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="5c160-524">Aşağıdaki gibi görünmelidir: https://wd3-impl-services1.workday.com/ccx/service/contoso4, burada contoso4 doğru Kiracı adınız ile değiştirilir ve (gerekirse) wd3 impl hello doğru ortamı dize ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="5c160-524">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with hello correct environment string (if necessary).</span></span>

   * <span data-ttu-id="5c160-525">**Bildirim e-posta –** e-posta adresinizi girin ve "hatası oluşursa, e-posta Gönder" onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-525">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="5c160-526">Merhaba tıklatın **Bağlantıyı Sına** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5c160-526">Click hello **Test Connection** button.</span></span> <span data-ttu-id="5c160-527">Merhaba bağlantı testi başarılı olursa, hello tıklatın **kaydetmek** hello üst düğmesini.</span><span class="sxs-lookup"><span data-stu-id="5c160-527">If hello connection test succeeds, click hello **Save** button at hello top.</span></span> <span data-ttu-id="5c160-528">Başarısız olursa, o hello Workday URL'si iki kez kontrol edin ve kimlik bilgilerini iş günü içinde geçerli.</span><span class="sxs-lookup"><span data-stu-id="5c160-528">If it fails, double-check that hello Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="5c160-529">2. Kısım: öznitelik eşlemelerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5c160-529">Part 2: Configure attribute mappings</span></span> 


<span data-ttu-id="5c160-530">Bu bölümde, kullanıcı verilerini Workday'deki Active Directory ile nasıl akacağını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5c160-530">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="5c160-531">Merhaba sağlama sekmesinde altında **eşlemeleri**, tıklatın **eşitleme Azure AD kullanıcıları tooWorkday**.</span><span class="sxs-lookup"><span data-stu-id="5c160-531">On hello Provisioning tab under **Mappings**, click **Synchronize Azure AD Users tooWorkday**.</span></span>

2.  <span data-ttu-id="5c160-532">Merhaba, **kaynak nesne kapsamı** alan, isteğe bağlı olarak filtreleyebilir hangi kullanıcı kümeleri için Azure Active Directory'de e-posta adreslerini yazdığınız geri tooWorkday.</span><span class="sxs-lookup"><span data-stu-id="5c160-532">In hello **Source Object Scope** field, you can optionally filter which sets of users in Azure Active Directory should have their email addresses written back tooWorkday.</span></span> <span data-ttu-id="5c160-533">"tüm kullanıcılar Azure AD'de" Merhaba varsayılan kapsamıdır.</span><span class="sxs-lookup"><span data-stu-id="5c160-533">hello default scope is “all users in Azure AD”.</span></span> 

3.  <span data-ttu-id="5c160-534">Merhaba, **öznitelik eşlemelerini** bölümünde, tek tek nasıl Workday harita tooActive dizin özniteliklerini öznitelikleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-534">In hello **Attribute mappings** section, you can define how individual Workday attributes map tooActive Directory attributes.</span></span> <span data-ttu-id="5c160-535">Varsayılan olarak hello e-posta adresi için bir eşleme yoktur.</span><span class="sxs-lookup"><span data-stu-id="5c160-535">There is a mapping for hello email address by default.</span></span> <span data-ttu-id="5c160-536">Ancak, eşleşen kimliği hello güncelleştirilmiş toomatch kullanıcılar Azure AD'de Workday bunların karşılık gelen girdilere sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c160-536">However, hello matching ID must be updated toomatch users in Azure AD with their corresponding entries in Workday.</span></span> <span data-ttu-id="5c160-537">Popüler eşleşen yöntemi toosynchronize hello Workday çalışan kimliği veya çalışan Azure AD'de tooextensionAttribute1-15 kimliği ve ardından bu özniteliği Azure AD toomatch kullanıcılar geri iş günü içinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="5c160-537">A popular matching method is toosynchronize hello Workday worker ID or employee ID tooextensionAttribute1-15 in Azure AD, and then use this attribute in Azure AD toomatch users back in Workday.</span></span>

4.  <span data-ttu-id="5c160-538">toosave, eşlemeler'e tıklayın **kaydetmek** hello eşleme özniteliği bölüm hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="5c160-538">toosave your mappings, click **Save** at hello top of hello Attribute Mapping section.</span></span>

### <a name="part-3-start-hello-service"></a><span data-ttu-id="5c160-539">3. Kısım: Başlangıç hello hizmeti</span><span class="sxs-lookup"><span data-stu-id="5c160-539">Part 3: Start hello service</span></span>
<span data-ttu-id="5c160-540">Bölümleri 1-2 tamamladıktan sonra hizmet sağlama hello başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c160-540">Once parts 1-2 have been completed, you can start hello provisioning service.</span></span>

1.  <span data-ttu-id="5c160-541">Merhaba, **sağlama** sekmesi, kümesi hello **sağlama durumu** için **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="5c160-541">In hello **Provisioning** tab, set hello **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="5c160-542">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c160-542">Click **Save**.</span></span>

3. <span data-ttu-id="5c160-543">Bu değişken sayıda iş günü içinde kaç kullanıcılardır bağlı olarak saatler sürebilir hello ilk eşitlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="5c160-543">This will start hello initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="5c160-544">Bireysel eşitleme olayları hello görüntülenebilir **denetim günlüklerini** sekmesi. **[Ayrıntılı yönergeler için raporlama Kılavuzu nasıl tooread hello denetim günlüklerini üzerinde sağlama hello bakın](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="5c160-544">Individual sync events can be viewed in hello **Audit Logs** tab. **[See hello provisioning reporting guide for detailed instructions on how tooread hello audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="5c160-545">Bir tamamlandı, onu bir denetim özet raporu yazacak **sağlama** sekmesinde, aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="5c160-545">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

## <a name="known-issues"></a><span data-ttu-id="5c160-546">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="5c160-546">Known issues</span></span>

* <span data-ttu-id="5c160-547">**Denetim günlükleri Avrupa yerel ayarlarda** - Bu teknik önizleme hello sürümü olduğundan hello bilinen bir sorun [denetim günlüklerini](active-directory-saas-provisioning-reporting.md) hello görünmeyen hello Workday bağlayıcı uygulamalar için [Azure portal](https://portal.azure.com) hello Azure AD Kiracı Avrupa veri merkezinde bulunuyorsa.</span><span class="sxs-lookup"><span data-stu-id="5c160-547">**Audit logs in European locales** - As of hello release of this technical preview, there is a known issue with hello [audit logs](active-directory-saas-provisioning-reporting.md) for hello Workday connector apps not appearing in hello [Azure portal](https://portal.azure.com) if hello Azure AD tenant resides in a European data center.</span></span> <span data-ttu-id="5c160-548">Bu sorun için bir düzeltme yeni çıkacak.</span><span class="sxs-lookup"><span data-stu-id="5c160-548">A fix for this issue is forthcoming.</span></span> <span data-ttu-id="5c160-549">Lütfen bu alan yeniden hello yakın zaman güncelleştirmeleri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5c160-549">Please check this space again in hello near future for updates.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5c160-550">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5c160-550">Additional resources</span></span>
* [<span data-ttu-id="5c160-551">Öğretici: çoklu oturum açma Workday ve Azure Active Directory arasında yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5c160-551">Tutorial: Configuring single sign-on between Workday and Azure Active Directory</span></span>](active-directory-saas-workday-tutorial.md)
* [<span data-ttu-id="5c160-552">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5c160-552">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c160-553">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5c160-553">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="5c160-554">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c160-554">Next steps</span></span>

* [<span data-ttu-id="5c160-555">Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın</span><span class="sxs-lookup"><span data-stu-id="5c160-555">Learn how tooreview logs and get reports on provisioning activity</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
