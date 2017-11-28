---
title: "bir Azure farklı çalıştır hesabı aaaConfigure | Microsoft Docs"
description: "Bu öğreticide, Azure automation'da güvenlik sorumlusu kimlik doğrulaması hello oluşturma, test ve örnek kullanım açıklanmaktadır."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "hizmet asıl adı, setspn, azure kimlik doğrulaması"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="3e06e-104">Azure Farklı Çalıştır hesabıyla kimlik doğrulaması runbook’ları</span><span class="sxs-lookup"><span data-stu-id="3e06e-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="3e06e-105">Bu makalede nasıl tooconfigure bir Azure Otomasyonu hesabı hello Azure portal gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-105">This article shows you how tooconfigure an Azure Automation account in hello Azure portal.</span></span> <span data-ttu-id="3e06e-106">toodo bu nedenle, Azure Resource Manager veya Azure Service Management kaynakları yönetme hello farklı çalıştır hesabı özelliği tooauthenticate runbook'ları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-106">toodo so, you use hello Run As account feature tooauthenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="3e06e-107">Hello Azure portalında bir Otomasyon hesabı oluşturduğunuzda, otomatik olarak iki hesapları oluştur:</span><span class="sxs-lookup"><span data-stu-id="3e06e-107">When you create an Automation account in hello Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="3e06e-108">Bir Farklı Çalıştır hesabı.</span><span class="sxs-lookup"><span data-stu-id="3e06e-108">A Run As account.</span></span> <span data-ttu-id="3e06e-109">Bu hesap, Azure Active Directory'de (Azure AD) bir hizmet sorumlusu ve bir sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3e06e-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="3e06e-110">Ayrıca, runbook'lar kullanılarak Resource Manager kaynaklarını yöneten hello katkıda bulunan rol tabanlı erişim denetimi (RBAC) atar.</span><span class="sxs-lookup"><span data-stu-id="3e06e-110">It also assigns hello Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="3e06e-111">Klasik Farklı Çalıştır hesabı.</span><span class="sxs-lookup"><span data-stu-id="3e06e-111">A Classic Run As account.</span></span> <span data-ttu-id="3e06e-112">Bu hesabı olan bir yönetim sertifikası karşıya yükleme kullanılan toomanage Hizmet Yönetimi veya Klasik kaynakları runbook'ları kullanarak.</span><span class="sxs-lookup"><span data-stu-id="3e06e-112">This account uploads a management certificate, which is used toomanage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="3e06e-113">Bir Otomasyon hesabı hello işlemi, oluşturma ve runbook'ları toosupport dağıtmaya hemen başlamanıza yardımcı olur için basitleştirir automation'ınızı oluşturma gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-113">Creating an Automation account simplifies hello process for you and helps you quickly start building and deploying runbooks toosupport your automation needs.</span></span>

<span data-ttu-id="3e06e-114">Farklı Çalıştır ve Klasik Farklı Çalıştır hesapları ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3e06e-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="3e06e-115">Hello Azure portalındaki runbook'lardan kaynak yöneticisi veya Service Management kaynaklarına yönetirken standartlaştırılmış yol tooauthenticate Azure ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-115">Provide a standardized way tooauthenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in hello Azure portal.</span></span>
* <span data-ttu-id="3e06e-116">Azure Uyarıları'nda yapılandırabileceğiniz genel runbook'ların Hello kullan otomatikleştirin.</span><span class="sxs-lookup"><span data-stu-id="3e06e-116">Automate hello use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="3e06e-117">Merhaba [Azure uyarı tümleştirme özelliği](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) ile Otomasyon genel runbook'ları farklı çalıştır hesabı ve klasik farklı çalıştır hesabı ile yapılandırılmış bir Otomasyon hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-117">hello [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="3e06e-118">Farklı Çalıştır ve klasik farklı çalıştır hesaplarını önceden tanımlanmış bir Otomasyon hesabı seçebilir veya yeni bir Otomasyon hesabı toocreate seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e06e-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose toocreate a new Automation account.</span></span>
>  

<span data-ttu-id="3e06e-119">Bu makalede nasıl toocreate hello Azure portalında bir Otomasyon hesabının Azure PowerShell kullanarak Automation hesabını güncelleştirme, hello hesap yapılandırmasını yönetmek ve larınızda kimlik doğrulamasının gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-119">This article shows how toocreate an Automation account from hello Azure portal, update an Automation account by using Azure PowerShell, manage hello account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="3e06e-120">Bir Otomasyon hesabı oluşturmaya başlamadan önce bir fikir toounderstand olan ve hello aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="3e06e-120">Before you begin creating an Automation account, it's a good idea toounderstand and consider hello following:</span></span>

* <span data-ttu-id="3e06e-121">Bir Otomasyon hesabı oluşturulurken zaten hello Klasik veya Resource Manager dağıtım modeli oluşturmuş olabileceğiniz Otomasyon hesaplarını etkilemez.</span><span class="sxs-lookup"><span data-stu-id="3e06e-121">Creating an Automation account does not affect Automation accounts you might have already created in either hello classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="3e06e-122">Merhaba işlem hello Azure portalında oluşturduğunuz Automation hesapları için çalışır.</span><span class="sxs-lookup"><span data-stu-id="3e06e-122">hello process works only for Automation accounts that you create in hello Azure portal.</span></span> <span data-ttu-id="3e06e-123">Toocreate hello Klasik Azure portalında bir hesaptan çalışırken hello farklı çalıştır hesabının yapılandırması çoğaltılmaz.</span><span class="sxs-lookup"><span data-stu-id="3e06e-123">Attempting toocreate an account from hello Azure classic portal does not replicate hello Run As account configuration.</span></span>
* <span data-ttu-id="3e06e-124">Runbook'ları ve varlıkları (örneğin, zamanlamaları veya değişkenleri) yer toomanage Klasik kaynaklar zaten ve runbook'ları tooauthenticate hello yeni Klasik farklı çalıştır hesabıyla istiyorsanız hello aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="3e06e-124">If you already have runbooks and assets (such as schedules or variables) in place toomanage classic resources, and you want runbooks tooauthenticate with hello new Classic Run As account, do either of hello following:</span></span>

  * <span data-ttu-id="3e06e-125">toocreate bir Klasik farklı çalıştır hesabı ", farklı çalıştır hesabı yönetme" Merhaba bölümündeki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="3e06e-125">toocreate a Classic Run As account, follow hello instructions in hello "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="3e06e-126">tooupdate, var olan hesabınızı, kullanım hello PowerShell'hello "PowerShell kullanarak Automation hesabınız güncelleştir" bölümünde komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="3e06e-126">tooupdate your existing account, use hello PowerShell script in hello "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="3e06e-127">Merhaba yeni farklı çalıştır hesabını ve klasik farklı çalıştır Otomasyon hesabını kullanarak tooauthenticate ihtiyacınız var olan runbook'larınızla hello hello bölümünde sağlanan örnek kod toomodify [kimlik doğrulaması kodu örnekleri](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="3e06e-127">tooauthenticate by using hello new Run As account and Classic Run As Automation account, you  need toomodify your existing runbooks with hello example code provided in hello section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="3e06e-128">Merhaba sertifika tabanlı hizmet sorumlusu kullanan Resource Manager kaynaklarına karşı kimlik doğrulamasını Hello farklı çalıştır hesabı içindir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-128">hello Run As account is for authentication against Resource Manager resources using hello certificate-based service principal.</span></span> <span data-ttu-id="3e06e-129">Merhaba Klasik farklı çalıştır hesabı, bir yönetim sertifikası ile Service Management kaynaklarına göre kimlik doğrulaması için ' dir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-129">hello Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-hello-azure-portal"></a><span data-ttu-id="3e06e-130">Azure portal hello Automation hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e06e-130">Create an Automation account from hello Azure portal</span></span>
<span data-ttu-id="3e06e-131">Bu bölümde, sırayla hem farklı çalıştır hesabı hem de klasik farklı çalıştır hesabı oluşturur Azure portal hello bir Azure Otomasyonu hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e06e-131">In this section, you create an Azure Automation account from hello Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="3e06e-132">bir Otomasyon hesabı toocreate, hello hizmet Yöneticileri rolünün üyesi ya da erişim toohello abonelik verme hello aboneliğinin ortak Yöneticisi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3e06e-132">toocreate an Automation account, you must be a member of hello Service Admins role or co-administrator of hello subscription that is granting access toohello subscription.</span></span> <span data-ttu-id="3e06e-133">Ayrıca bir kullanıcı toothat aboneliğin varsayılan Active Directory örneği olarak eklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-133">You must also be added as a user toothat subscription's default Active Directory instance.</span></span> <span data-ttu-id="3e06e-134">Merhaba hesap ayrıcalıklı bir role atanmış toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3e06e-134">hello account does not need toobe assigned a privileged role.</span></span>
>
><span data-ttu-id="3e06e-135">Merhaba abonelik toohello ortak Yönetici rolü eklenmeden önce hello aboneliğinin Active Directory örneğine üyesi değilseniz, bir konuk olarak tooActive dizin eklenir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-135">If you are not a member of hello subscription’s Active Directory instance before you are added toohello co-administrator role of hello subscription, you will be added tooActive Directory as a guest.</span></span> <span data-ttu-id="3e06e-136">Bu örnekte, bir "sahip olmadığınız izinleri toocreate..." alırsınız</span><span class="sxs-lookup"><span data-stu-id="3e06e-136">In this instance, you will receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="3e06e-137">Merhaba üzerinde uyarı **Automation hesabı Ekle** dikey.</span><span class="sxs-lookup"><span data-stu-id="3e06e-137">warning on hello **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="3e06e-138">Toohello ortak Yönetici rolü ilk hello aboneliğinin Active Directory örneğinden kaldırılabilir ve yeniden, toomake eklendi eklenen kullanıcılar bunları Active Directory'de tam bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="3e06e-138">Users who were added toohello co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="3e06e-139">tooverify hello bu durumdan **Azure Active Directory** hello seçerek Azure portal bölmesinde **kullanıcılar ve gruplar**, seçme **tüm kullanıcılar** ve siz seçtikten sonra Merhaba belirli bir kullanıcı, seçme **profil**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-139">tooverify this situation from hello **Azure Active Directory** pane in hello Azure portal by selecting **Users and groups**, selecting **All users** and, after you select hello specific user, selecting **Profile**.</span></span> <span data-ttu-id="3e06e-140">Merhaba hello değerini **kullanıcı türü** hello kullanıcı profili altındaki özniteliğini eşit değil **Konuk**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-140">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="3e06e-141">Toohello hello abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla Azure Portalı'nda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-141">Sign in toohello Azure portal with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>

2. <span data-ttu-id="3e06e-142">**Automation Hesapları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e06e-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="3e06e-143">Merhaba üzerinde **Automation hesapları** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-143">On hello **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="3e06e-144">Merhaba **Automation hesabı Ekle** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="3e06e-144">hello **Add Automation Account** blade opens.</span></span>

 ![Merhaba "Automation hesabı ekle" dikey penceresi](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="3e06e-146">Hesabınızı hello abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak Yöneticisi değilse, aşağıdaki uyarı hello hello üzerinde görüntülenir **Automation hesabı Ekle** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="3e06e-146">If your account is not a member of hello subscription administrators role and co-administrator of hello subscription, hello following warning is displayed on hello **Add Automation Account** blade:</span></span>
   >
   >![Automation Hesabı Uyarısı ekleme](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="3e06e-148">Merhaba üzerinde **Automation hesabı Ekle** dikey penceresinde hello **adı** kutusuna, yeni Automation hesabınız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-148">On hello **Add Automation Account** blade, in hello **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="3e06e-149">Birden fazla aboneliğiniz varsa, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3e06e-149">If you have more than one subscription, do hello following:</span></span>

    <span data-ttu-id="3e06e-150">a.</span><span class="sxs-lookup"><span data-stu-id="3e06e-150">a.</span></span> <span data-ttu-id="3e06e-151">Altında **abonelik**, hello yeni hesap için bir tane belirtin.</span><span class="sxs-lookup"><span data-stu-id="3e06e-151">Under **Subscription**, specify one for hello new account.</span></span>

    <span data-ttu-id="3e06e-152">b.</span><span class="sxs-lookup"><span data-stu-id="3e06e-152">b.</span></span> <span data-ttu-id="3e06e-153">**Kaynak Grubu** altında, **Yeni oluştur** veya **Var olanı kullan**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="3e06e-154">c.</span><span class="sxs-lookup"><span data-stu-id="3e06e-154">c.</span></span> <span data-ttu-id="3e06e-155">**Konum** altında bir Azure veri merkezi belirtin.</span><span class="sxs-lookup"><span data-stu-id="3e06e-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="3e06e-156">**Azure Farklı Çalıştır hesabı oluştur** altında **Evet**’i seçin ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3e06e-157">Seçerek toocreate hello farklı çalıştır hesabı değil seçerseniz **Hayır**, bir uyarı iletisi görüntülenir hello **Automation hesabı Ekle** dikey.</span><span class="sxs-lookup"><span data-stu-id="3e06e-157">If you choose not toocreate hello Run As account by selecting **No**, a warning message is displayed hello **Add Automation Account** blade.</span></span> <span data-ttu-id="3e06e-158">Merhaba hesap hello Azure portalında oluşturulur, ancak klasik veya Resource Manager Abonelik dizin hizmeti içinde karşılık gelen bir kimlik doğrulama kimliği yok.</span><span class="sxs-lookup"><span data-stu-id="3e06e-158">Although hello account is created in hello Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="3e06e-159">Sonuç olarak, hello hesap, aboneliğinizde hiçbir erişim tooresources sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-159">Consequently, hello account has no access tooresources in your subscription.</span></span> <span data-ttu-id="3e06e-160">Bu senaryo, ilgili dağıtım modellerindeki kaynaklara göre kimlik doğrulama ve görev gerçekleştirme işlemlerinden bu hesaba başvuran runbook’ları engeller.</span><span class="sxs-lookup"><span data-stu-id="3e06e-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Merhaba "Automation hesabı ekle" dikey uyarı iletisi](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="3e06e-162">Ayrıca, Hello hizmet sorumlusu oluşturulmadığında çünkü hello katkıda bulunan rolü atanmaz.</span><span class="sxs-lookup"><span data-stu-id="3e06e-162">Additionally, because hello service principal is not created, hello Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="3e06e-163">Azure hello Automation hesabını oluşturduğu sırada altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="3e06e-163">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="resources"></a><span data-ttu-id="3e06e-164">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3e06e-164">Resources</span></span>
<span data-ttu-id="3e06e-165">Hello Otomasyon hesabı başarıyla oluşturulduğunda bazı kaynaklar sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3e06e-165">When hello Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="3e06e-166">Merhaba kaynakları iki tablo aşağıdaki hello özetlenmiştir:</span><span class="sxs-lookup"><span data-stu-id="3e06e-166">hello resources are summarized in hello following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="3e06e-167">Farklı Çalıştır hesabının kaynakları</span><span class="sxs-lookup"><span data-stu-id="3e06e-167">Run As account resources</span></span>

| <span data-ttu-id="3e06e-168">Kaynak</span><span class="sxs-lookup"><span data-stu-id="3e06e-168">Resource</span></span> | <span data-ttu-id="3e06e-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3e06e-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e06e-170">AzureAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="3e06e-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="3e06e-171">Farklı Çalıştır hesabını kullanarak tooauthenticate hello nasıl gösteren ve tüm hello Resource Manager kaynaklarını alan örnek bir grafik runbook.</span><span class="sxs-lookup"><span data-stu-id="3e06e-171">An example graphical runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="3e06e-172">AzureAutomationTutorialScript Runbook</span><span class="sxs-lookup"><span data-stu-id="3e06e-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="3e06e-173">Farklı Çalıştır hesabını kullanarak tooauthenticate hello nasıl gösteren ve tüm hello Resource Manager kaynaklarını alan örnek bir PowerShell runbook.</span><span class="sxs-lookup"><span data-stu-id="3e06e-173">An example PowerShell runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="3e06e-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="3e06e-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="3e06e-175">Automation hesabı oluşturma veya var olan bir hesap için PowerShell Betiği aşağıdaki hello kullandığınızda, otomatik olarak oluşturulan hello sertifika varlığı.</span><span class="sxs-lookup"><span data-stu-id="3e06e-175">hello certificate asset that's automatically created when you create an Automation account or use hello following PowerShell script for an existing account.</span></span> <span data-ttu-id="3e06e-176">Merhaba sertifika Azure Resource Manager kaynaklarını runbook'lardan yönetebilmeniz için Azure ile tooauthenticate sağlar.</span><span class="sxs-lookup"><span data-stu-id="3e06e-176">hello certificate allows you tooauthenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="3e06e-177">Merhaba sertifikanın bir yıllık kullanım ömrü vardır.</span><span class="sxs-lookup"><span data-stu-id="3e06e-177">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="3e06e-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="3e06e-178">AzureRunAsConnection</span></span> | <span data-ttu-id="3e06e-179">bir Otomasyon hesabı oluşturduğunuzda ya da mevcut hesap için hello PowerShell Betiği kullanmak, otomatik olarak oluşturulan hello bağlantı varlığı.</span><span class="sxs-lookup"><span data-stu-id="3e06e-179">hello connection asset that's automatically created when you create an Automation account or use hello PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="3e06e-180">Klasik Farklı Çalıştır hesabının kaynakları</span><span class="sxs-lookup"><span data-stu-id="3e06e-180">Classic Run As account resources</span></span>

| <span data-ttu-id="3e06e-181">Kaynak</span><span class="sxs-lookup"><span data-stu-id="3e06e-181">Resource</span></span> | <span data-ttu-id="3e06e-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3e06e-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e06e-183">AzureClassicAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="3e06e-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="3e06e-184">Tüm hello sanal makineleri alan örnek bir grafik runbook hello Klasik farklı çalıştır hesabı (sertifika) kullanarak bir abonelikte hello Klasik dağıtım modeli kullanılarak oluşturulur ve hello VM adını ve durumunu yazar.</span><span class="sxs-lookup"><span data-stu-id="3e06e-184">An example graphical runbook that gets all hello VMs that are created using hello classic deployment model in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="3e06e-185">AzureClassicAutomationTutorial Script Runbook</span><span class="sxs-lookup"><span data-stu-id="3e06e-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="3e06e-186">Tüm alır örnek bir PowerShell runbook hello Klasik farklı çalıştır hesabı (sertifika) kullanarak bir abonelikte Klasik sanal makineleri hello ve ardından yazma VM adını ve durumunu hello.</span><span class="sxs-lookup"><span data-stu-id="3e06e-186">An example PowerShell runbook that gets all hello classic VMs in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="3e06e-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="3e06e-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="3e06e-188">Merhaba otomatik olarak oluşturulan sertifika varlığı Azure Klasik kaynaklarını runbook'lardan yönetebilmeniz için Azure ile tooauthenticate kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-188">hello automatically created certificate asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="3e06e-189">Merhaba sertifikanın bir yıllık kullanım ömrü vardır.</span><span class="sxs-lookup"><span data-stu-id="3e06e-189">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="3e06e-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="3e06e-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="3e06e-191">Merhaba otomatik olarak oluşturulan bağlantı varlığı Azure Klasik kaynaklarını runbook'lardan yönetebilmeniz için Azure ile tooauthenticate kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-191">hello automatically created connection asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="3e06e-192">Farklı Çalıştır kimlik doğrulamasını onaylama</span><span class="sxs-lookup"><span data-stu-id="3e06e-192">Verify Run As authentication</span></span>
<span data-ttu-id="3e06e-193">Başarıyla hello yeni farklı çalıştır hesabını kullanarak kimlik doğrulaması bir küçük test tooconfirm gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3e06e-193">Perform a small test tooconfirm that you can successfully authenticate by using hello new Run As account.</span></span>

1. <span data-ttu-id="3e06e-194">Hello Azure portal, daha önce oluşturduğunuz hello Automation hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-194">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="3e06e-195">Merhaba tıklatın **Runbook'lar** döşeme tooopen hello listesini.</span><span class="sxs-lookup"><span data-stu-id="3e06e-195">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="3e06e-196">Select hello **AzureAutomationTutorialScript** runbook ve ardından **Başlat** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="3e06e-196">Select hello **AzureAutomationTutorialScript** runbook, and then click **Start** toostart hello runbook.</span></span> <span data-ttu-id="3e06e-197">olayları aşağıdaki hello oluşur:</span><span class="sxs-lookup"><span data-stu-id="3e06e-197">hello following events occur:</span></span>
 * <span data-ttu-id="3e06e-198">A [runbook işi](automation-runbook-execution.md) hello oluşturulur, **iş** dikey penceresinde görüntülenir ve hello iş durumu hello görüntülenir **iş özeti** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3e06e-198">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="3e06e-199">Merhaba iş durumu başlar olarak **sıraya alınan**, bir runbook worker'hello bulut toobecome için bekleyen belirten.</span><span class="sxs-lookup"><span data-stu-id="3e06e-199">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="3e06e-200">Merhaba durumu olur **başlangıç** ne zaman bir çalışan talep hello işi.</span><span class="sxs-lookup"><span data-stu-id="3e06e-200">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="3e06e-201">Merhaba durumu olur **çalıştıran** hello runbook çalışmaya başladığında.</span><span class="sxs-lookup"><span data-stu-id="3e06e-201">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="3e06e-202">Çalışan Hello runbook işi tamamlandığında, durumunu görmelisiniz **tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-202">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="3e06e-203">toosee Merhaba hello runbook'un ayrıntılı sonuçlarını, hello tıklatın **çıkış** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3e06e-203">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="3e06e-204">Merhaba **çıkış** dikey penceresinde görüntülenir, o hello runbook doğrulamasının başarıyla yapıldığını ve hello kaynak grubunda mevcut tüm kaynakların bir listesini döndürülen gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="3e06e-204">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all resources available in hello resource group.</span></span>

5. <span data-ttu-id="3e06e-205">Kapat hello **çıkış** dikey tooreturn toohello **iş özeti** dikey.</span><span class="sxs-lookup"><span data-stu-id="3e06e-205">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="3e06e-206">Kapat hello **iş özeti** dikey ve hello karşılık gelen **AzureAutomationTutorialScript** runbook dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="3e06e-206">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="3e06e-207">Klasik Farklı Çalıştır kimlik doğrulamasını onaylama</span><span class="sxs-lookup"><span data-stu-id="3e06e-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="3e06e-208">Benzer küçük gerçekleştirmek, hello yeni Klasik farklı çalıştır hesabını kullanarak kimlik doğrulamasını başarıyla tooconfirm sınayın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-208">Perform a similar small test tooconfirm that you can successfully authenticate by using hello new Classic Run As account.</span></span>

1. <span data-ttu-id="3e06e-209">Hello Azure portal, daha önce oluşturduğunuz hello Automation hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-209">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="3e06e-210">Merhaba tıklatın **Runbook'lar** döşeme tooopen hello listesini.</span><span class="sxs-lookup"><span data-stu-id="3e06e-210">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="3e06e-211">Select hello **AzureClassicAutomationTutorialScript** runbook ve ardından **Başlat** çok hello runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-211">Select hello **AzureClassicAutomationTutorialScript** runbook, and then click **Start** too start hello runbook.</span></span> <span data-ttu-id="3e06e-212">olayları aşağıdaki hello oluşur:</span><span class="sxs-lookup"><span data-stu-id="3e06e-212">hello following events occur:</span></span>

 * <span data-ttu-id="3e06e-213">A [runbook işi](automation-runbook-execution.md) hello oluşturulur, **iş** dikey penceresinde görüntülenir ve hello iş durumu hello görüntülenir **iş özeti** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3e06e-213">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="3e06e-214">Merhaba iş durumu başlar olarak **sıraya alınan**, bir runbook worker'hello bulut toobecome için bekleyen belirten.</span><span class="sxs-lookup"><span data-stu-id="3e06e-214">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="3e06e-215">Merhaba durumu olur **başlangıç** ne zaman bir çalışan talep hello işi.</span><span class="sxs-lookup"><span data-stu-id="3e06e-215">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="3e06e-216">Merhaba durumu olur **çalıştıran** hello runbook çalışmaya başladığında.</span><span class="sxs-lookup"><span data-stu-id="3e06e-216">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="3e06e-217">Çalışan Hello runbook işi tamamlandığında, durumunu görmelisiniz **tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-217">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Güvenlik Sorumlusu Runbook Testi](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="3e06e-219">toosee Merhaba hello runbook'un ayrıntılı sonuçlarını, hello tıklatın **çıkış** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3e06e-219">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="3e06e-220">Merhaba **çıkış** dikey penceresinde görüntülenir, o hello runbook doğrulamasının başarıyla yapıldığını ve hello Abonelikteki tüm Klasik sanal makineleri listesini döndürülen gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="3e06e-220">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all classic VMs in hello subscription.</span></span>

5. <span data-ttu-id="3e06e-221">Kapat hello **çıkış** dikey tooreturn toohello **iş özeti** dikey.</span><span class="sxs-lookup"><span data-stu-id="3e06e-221">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="3e06e-222">Kapat hello **iş özeti** dikey ve hello karşılık gelen **AzureAutomationTutorialScript** runbook dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="3e06e-222">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="3e06e-223">Farklı Çalıştır hesabınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="3e06e-223">Managing your Run As account</span></span>
<span data-ttu-id="3e06e-224">Belirli bir noktada, Automation hesabınız süresi dolmadan önce toorenew hello sertifika gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-224">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="3e06e-225">Bu farklı çalıştır hesabı hello tehlikeye düşünüyorsanız, silin ve yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e06e-225">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="3e06e-226">Bu bölümde ele alınmaktadır nasıl tooperform bu işlemler.</span><span class="sxs-lookup"><span data-stu-id="3e06e-226">This section discusses how tooperform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="3e06e-227">Otomatik olarak imzalanan sertifika yenileme</span><span class="sxs-lookup"><span data-stu-id="3e06e-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="3e06e-228">hello farklı çalıştır hesabı için oluşturulan hello otomatik olarak imzalanan sertifika oluşturma başlangıç tarihinden itibaren bir yıl süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="3e06e-228">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="3e06e-229">Sertifikayı süresi dolmadan önce herhangi bir zamanda yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e06e-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="3e06e-230">Yenilediğinizde, yukarı veya etkin olarak çalışan sıraya ve bu farklı çalıştır hesabını hello ile kimlik doğrulaması runbook'ları olumsuz etkilenmez tutulan tooensure hello geçerli geçerli sertifika yok.</span><span class="sxs-lookup"><span data-stu-id="3e06e-230">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="3e06e-231">Merhaba sertifika sona erme tarihini kadar geçerli kalır.</span><span class="sxs-lookup"><span data-stu-id="3e06e-231">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="3e06e-232">Automation farklı çalıştır hesabı toouse, kuruluş sertifika yetkiliniz tarafından verilen bir sertifika yapılandırdıktan ve bu seçeneği kullanırsanız, hello Kurumsal Sertifika tarafından otomatik olarak imzalanan bir sertifika kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="3e06e-232">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="3e06e-233">toorenew hello sertifika, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3e06e-233">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="3e06e-234">Hello Azure portal, hello Automation hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-234">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="3e06e-235">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde hello **hesap özellikleri** bölmesi altında **hesap ayarlarını**seçin **farklı çalıştır hesapları**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-235">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Otomasyon hesabı özellikleri bölmesi](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="3e06e-237">Merhaba üzerinde **farklı çalıştır hesapları** ya da hello Çalıştır hesabı veya toorenew hello sertifika için istediğiniz hello Klasik farklı çalıştır hesabı olarak özellikleri dikey penceresinde, seçin.</span><span class="sxs-lookup"><span data-stu-id="3e06e-237">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="3e06e-238">Merhaba üzerinde **özellikleri** hello dikey penceresinde seçili hesabı'na tıklayın **yenileme sertifika**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-238">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Farklı Çalıştır hesabının sertifikasını yenileme](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="3e06e-240">Merhaba sertifika yenileme sırasında altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="3e06e-240">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="3e06e-241">Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını silme</span><span class="sxs-lookup"><span data-stu-id="3e06e-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="3e06e-242">Bu bölümde açıklanmıştır nasıl toodelete ve bir farklı çalıştır veya Klasik farklı çalıştır hesabını yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e06e-242">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="3e06e-243">Bu eylemi gerçekleştirdiğinizde, hello Otomasyon hesabı korunur.</span><span class="sxs-lookup"><span data-stu-id="3e06e-243">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="3e06e-244">Bir farklı çalıştır veya Klasik farklı çalıştır hesabını sildikten sonra hello Azure portalında yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e06e-244">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="3e06e-245">Hello Azure portal, hello Automation hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-245">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="3e06e-246">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde hello hesap Özellikler bölmesinde, **farklı çalıştır hesapları**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-246">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="3e06e-247">Merhaba üzerinde **farklı çalıştır hesapları** özellikleri dikey penceresinde, seçin ya da hello Çalıştır hesabı veya Klasik farklı çalıştır hesabı toodelete istiyor.</span><span class="sxs-lookup"><span data-stu-id="3e06e-247">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="3e06e-248">Ardından, hello **özellikleri** hello dikey penceresinde seçili hesabı'na tıklayın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-248">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Farklı Çalıştır hesabını silme](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="3e06e-250">Merhaba hesap silindi, ancak altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="3e06e-250">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="3e06e-251">Merhaba hesabı silindikten sonra bunu hello üzerinde yeniden oluşturabilirsiniz **farklı çalıştır hesapları** hello seçerek özellikler dikey penceresini oluşturma seçeneği **Azure farklı çalıştır hesabını**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-251">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Merhaba Automation farklı çalıştır hesabını yeniden oluşturun](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="3e06e-253">Yanlış yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3e06e-253">Misconfiguration</span></span>
<span data-ttu-id="3e06e-254">Merhaba Çalıştır veya Klasik farklı çalıştır hesabı toofunction için gereken bazı yapılandırma öğeleri düzgün silinmiş veya yanlış ilk kurulum sırasında oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="3e06e-254">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="3e06e-255">Merhaba öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="3e06e-255">hello items include:</span></span>

* <span data-ttu-id="3e06e-256">Sertifika varlığı</span><span class="sxs-lookup"><span data-stu-id="3e06e-256">Certificate asset</span></span>
* <span data-ttu-id="3e06e-257">Bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="3e06e-257">Connection asset</span></span>
* <span data-ttu-id="3e06e-258">Farklı Çalıştır hesabı hello katkıda bulunan rolü ' kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="3e06e-258">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="3e06e-259">Azure AD'de hizmet sorumlusu veya uygulama</span><span class="sxs-lookup"><span data-stu-id="3e06e-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="3e06e-260">Hello önceki ve diğer örnekleri yanlış hello Otomasyon hesabı hello değiştirir ve durumunu görüntüler algılar *tamamlanmamış* hello üzerinde **farklı çalıştır hesapları** hello özellikleri dikey penceresi hesabı.</span><span class="sxs-lookup"><span data-stu-id="3e06e-260">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Tamamlanmamış Farklı Çalıştır hesabı yapılandırma durumu](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="3e06e-262">Merhaba farklı çalıştır hesabı seçin, hesap hello **özellikleri** bölmesi hello aşağıdaki hata iletisini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="3e06e-262">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Tamamlanmamış Farklı Çalıştır yapılandırma uyarısı iletisi](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="3e06e-264">.</span><span class="sxs-lookup"><span data-stu-id="3e06e-264">.</span></span>

<span data-ttu-id="3e06e-265">Bu farklı çalıştır hesabı sorunları hızla, silme ve hello hesabını yeniden oluşturmayı da çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e06e-265">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="3e06e-266">PowerShell kullanarak Otomasyon hesabınızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3e06e-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="3e06e-267">Varsa, PowerShell tooupdate var olan Otomasyon hesabınızı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3e06e-267">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="3e06e-268">Automation hesabı oluşturma ancak toocreate hello farklı çalıştır hesabı reddedin.</span><span class="sxs-lookup"><span data-stu-id="3e06e-268">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="3e06e-269">Runbook kimlik doğrulaması için tooupdate hello tooinclude hello farklı çalıştır hesabı istediğiniz ve zaten bir Automation hesabı toomanage Resource Manager kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-269">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="3e06e-270">Zaten bir Automation hesabı toomanage Klasik kaynakları kullanır ve tooupdate isterseniz bunu toouse hello yeni bir hesap oluşturma ve runbook'ları ve varlıkları tooit geçirmek yerine Klasik farklı çalıştır hesabı.</span><span class="sxs-lookup"><span data-stu-id="3e06e-270">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="3e06e-271">Kuruluş sertifika yetkilisi (CA) tarafından verilen bir sertifikayı kullanarak toocreate bir farklı çalıştır ve klasik farklı çalıştır hesabı istiyor.</span><span class="sxs-lookup"><span data-stu-id="3e06e-271">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="3e06e-272">Merhaba komut dosyasında aşağıdaki önkoşullar hello vardır:</span><span class="sxs-lookup"><span data-stu-id="3e06e-272">hello script has hello following prerequisites:</span></span>

* <span data-ttu-id="3e06e-273">Hello betik yalnızca Windows 10 ve Windows Server 2016 ile Azure Resource Manager modüllerini 2.01 ve daha sonra çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-273">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="3e06e-274">Windows'un önceki sürümleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="3e06e-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="3e06e-275">Azure PowerShell 1.0 ve üzeri.</span><span class="sxs-lookup"><span data-stu-id="3e06e-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="3e06e-276">Hello PowerShell 1.0 sürümü hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e06e-276">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="3e06e-277">Merhaba hello değeri olarak başvurulan bir Otomasyon hesabı *– AutomationAccountName* ve *- ApplicationDisplayName* hello PowerShell Betiği aşağıdaki parametreleri.</span><span class="sxs-lookup"><span data-stu-id="3e06e-277">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="3e06e-278">tooget hello değerleri *Subscriptionıd*, *ResourceGroup*, ve *AutomationAccountName*hello komut dosyaları için gerekli parametreler olan, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3e06e-278">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="3e06e-279">İçinde Azure portal Merhaba, Automation hesabınızı hello üzerinde seçin **Otomasyon hesabı** dikey ve ardından **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-279">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="3e06e-280">Merhaba üzerinde **tüm ayarları** dikey altında **hesap ayarlarını**seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="3e06e-280">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="3e06e-281">Not hello hello değerlerine **özellikleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="3e06e-281">Note hello values on hello **Properties** blade.</span></span>

![Merhaba Otomasyon hesabı "Özellikler" dikey](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="3e06e-283">Farklı Çalıştır hesabı PowerShell betiği oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e06e-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="3e06e-284">Bu PowerShell Betiği yapılandırmaları aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="3e06e-284">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="3e06e-285">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e06e-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="3e06e-286">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e06e-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="3e06e-287">Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e06e-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="3e06e-288">Hello Azure Bulutu kendinden imzalı bir sertifika kullanarak bir farklı çalıştır hesabı ve klasik farklı çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e06e-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="3e06e-289">Seçtiğiniz hello yapılandırma seçeneğine bağlı olarak aşağıdaki öğelerindeki hello hello komut dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3e06e-289">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="3e06e-290">**Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="3e06e-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="3e06e-291">Bir Azure oluşturduğu AD uygulama toobe verilen kendinden imzalı ya da hello ile veya Kurumsal Sertifika genel anahtarı, Azure AD'de Merhaba uygulaması için bir hizmet sorumlusu hesabı oluşturur ve hello mevcut hello hesap için katılımcı rolü atar aboneliği.</span><span class="sxs-lookup"><span data-stu-id="3e06e-291">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="3e06e-292">Bu ayar tooOwner veya başka bir rolle değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e06e-292">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="3e06e-293">Daha fazla bilgi için bkz. [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="3e06e-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="3e06e-294">Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureRunAsCertificate* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="3e06e-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="3e06e-295">Merhaba sertifika varlığı hello Azure AD uygulama tarafından kullanılan hello sertifika özel anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-295">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="3e06e-296">Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureRunAsConnection* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="3e06e-296">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="3e06e-297">Merhaba bağlantı varlığı hello ApplicationId, Tenantıd, Subscriptionıd ve sertifika parmak izi tutar.</span><span class="sxs-lookup"><span data-stu-id="3e06e-297">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="3e06e-298">**Klasik Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="3e06e-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="3e06e-299">Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureClassicRunAsCertificate* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="3e06e-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="3e06e-300">Merhaba sertifika varlığı hello yönetim sertifikası tarafından kullanılan hello sertifika özel anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-300">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="3e06e-301">Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureClassicRunAsConnection* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="3e06e-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="3e06e-302">Merhaba bağlantı varlığı hello abonelik adı, Subscriptionıd ve sertifika varlık adı tutar.</span><span class="sxs-lookup"><span data-stu-id="3e06e-302">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="3e06e-303">Merhaba betik yürütüldükten sonra Klasik farklı çalıştır hesabı oluşturmak için her iki seçeneği seçerseniz, karşıya yükleme hello ortak sertifika (.cer dosya adı uzantısı) toohello yönetim deposu hello abonelik için bu hello Otomasyon hesabı içinde oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="3e06e-303">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

<span data-ttu-id="3e06e-304">tooexecute Merhaba komut dosyası ve hello sertifikasını karşıya yükleyin, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3e06e-304">tooexecute hello script and upload hello certificate, do hello following:</span></span>

1. <span data-ttu-id="3e06e-305">Komut dosyası, bilgisayarınızda aşağıdaki hello kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3e06e-305">Save hello following script on your computer.</span></span> <span data-ttu-id="3e06e-306">İsteğe bağlı olarak bu örnekte, hello dosya adıyla kaydedin *yeni RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="3e06e-306">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="3e06e-307">Bilgisayarınızda **Başlat**’a tıklayın ve yükseltilmiş kullanıcı haklarıyla **Windows PowerShell**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="3e06e-308">Merhaba PowerShell komut satırı kabuğundan, 1. adımda oluşturduğunuz hello betik içeren gidin toohello klasörü yükseltilmiş.</span><span class="sxs-lookup"><span data-stu-id="3e06e-308">From hello elevated PowerShell command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>

4. <span data-ttu-id="3e06e-309">İçin gerek duyduğunuz hello yapılandırma hello parametre değerlerini kullanarak Hello betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="3e06e-309">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="3e06e-310">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="3e06e-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="3e06e-311">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="3e06e-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="3e06e-312">**Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="3e06e-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="3e06e-313">**Hello Azure Bulutu kendinden imzalı bir sertifika kullanarak bir farklı çalıştır hesabı ve klasik farklı çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="3e06e-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="3e06e-314">Merhaba betiği yürüttükten sonra Azure ile istendiğinde tooauthenticate olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3e06e-314">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="3e06e-315">Merhaba abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-315">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="3e06e-316">Merhaba betiği başarıyla yürütüldü sonra hello aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="3e06e-316">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="3e06e-317">Otomatik olarak imzalanan bir PKI sertifikası (.cer dosyası) ile bir Klasik farklı çalıştır hesabını oluşturduysanız, hello komut dosyası oluşturur ve bilgisayarınızda hello kullanıcı profili altındaki toohello geçici dosyalar klasörüne kaydeder *%USERPROFILE%\AppData\Local\Temp*, tooexecute hello PowerShell oturumu kullanılan.</span><span class="sxs-lookup"><span data-stu-id="3e06e-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="3e06e-318">Kurumsal ortak sertifika (.cer file) ile bir Klasik Farklı Çalıştır hesabı oluşturduysanız bu sertifikayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e06e-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="3e06e-319">Merhaba yönergeleri izleyin [yönetim API sertifikası toohello Klasik Azure portalı karşıya](../azure-api-management-certs.md)ve ardından hello kullanarak Service Management kaynaklarıyla hello kimlik bilgisi yapılandırmasını doğrulamak [örnek kod Service Management kaynaklarıyla tooauthenticate](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="3e06e-319">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with Service Management resources by using hello [sample code tooauthenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="3e06e-320">Kaldırdıysanız *değil* Klasik farklı çalıştır hesabı oluşturma, Resource Manager kaynaklarıyla kimlik doğrulaması ve hello kullanarak hello kimlik bilgisi yapılandırmasını doğrulamak [örnek Hizmet Yönetimi ile kimlik doğrulaması için kod Kaynakları](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="3e06e-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a><span data-ttu-id="3e06e-321">Örnek kod tooauthenticate Resource Manager kaynaklarıyla</span><span class="sxs-lookup"><span data-stu-id="3e06e-321">Sample code tooauthenticate with Resource Manager resources</span></span>
<span data-ttu-id="3e06e-322">Güncelleştirilmiş hello aşağıdakileri kullanabilirsiniz örnek kod, hello gerçekleştirilecek *AzureAutomationTutorialScript* örnek runbook, runbook'larınızla hello farklı çalıştır hesabı toomanage Resource Manager kaynaklarını kullanarak tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="3e06e-322">You can use hello following updated sample code, taken from hello *AzureAutomationTutorialScript* example runbook, tooauthenticate by using hello Run As account toomanage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="3e06e-323">toohelp, tooeasily iş arasında birden fazla abonelik, abonelik bağlamına başvuruyu destekleyen iki ek kod satırı hello komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-323">toohelp you tooeasily work between multiple subscriptions, hello script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="3e06e-324">Adlı bir değişken varlığı *Subscriptionıd* hello hello abonelik Kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="3e06e-324">A variable asset named *SubscriptionId* contains hello ID of hello subscription.</span></span> <span data-ttu-id="3e06e-325">Merhaba sonra `Add-AzureRmAccount` cmdlet'i deyiminden hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet ile Merhaba parametre kümesi belirtilen *- Subscriptionıd*.</span><span class="sxs-lookup"><span data-stu-id="3e06e-325">After hello `Add-AzureRmAccount` cmdlet statement, hello [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with hello parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="3e06e-326">Merhaba değişken adı çok genelse, tooinclude bir önek düzeltmek veya başka bir adlandırma kuralı toomake kullanmak, daha kolay tooidentify.</span><span class="sxs-lookup"><span data-stu-id="3e06e-326">If hello variable name is too generic, you can revise it tooinclude a prefix or use another naming convention toomake it easier tooidentify.</span></span> <span data-ttu-id="3e06e-327">Alternatif olarak, hello parametre kümesini kullanabilirsiniz *varlığıyla - SubscriptionName* yerine *- Subscriptionıd* karşılık gelen bir değişken varlığı ile.</span><span class="sxs-lookup"><span data-stu-id="3e06e-327">Alternatively, you can use hello parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="3e06e-328">Merhaba runbook'ta kimlik doğrulaması için kullandığınız cmdlet'in hello `Add-AzureRmAccount`, kullandığı hello *ServicePrincipalCertificate* parametre kümesi.</span><span class="sxs-lookup"><span data-stu-id="3e06e-328">hello cmdlet that you use for authenticating in hello runbook, `Add-AzureRmAccount`, uses hello *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="3e06e-329">Merhaba hizmet asıl sertifikasını değil hello kullanıcı kimlik bilgilerini kullanarak kimlik doğrulamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="3e06e-329">It authenticates by using hello service principal certificate, not hello user credentials.</span></span>

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a><span data-ttu-id="3e06e-330">Örnek kod tooauthenticate Service Management kaynaklarıyla</span><span class="sxs-lookup"><span data-stu-id="3e06e-330">Sample code tooauthenticate with Service Management resources</span></span>
<span data-ttu-id="3e06e-331">Merhaba alınan güncelleştirilmiş örnek kodu aşağıdaki hello kullanabilirsiniz *AzureClassicAutomationTutorialScript* örnek runbook, Klasik farklı çalıştır toomanage Klasik kaynakları hesap hello kullanarak tooauthenticate, runbook'ları.</span><span class="sxs-lookup"><span data-stu-id="3e06e-331">You can use hello following updated sample code, which is taken from hello *AzureClassicAutomationTutorialScript* example runbook, tooauthenticate by using hello Classic Run As account toomanage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="3e06e-332">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e06e-332">Next steps</span></span>
* [<span data-ttu-id="3e06e-333">Azure AD’de uygulama ve hizmet sorumlusu nesneleri</span><span class="sxs-lookup"><span data-stu-id="3e06e-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="3e06e-334">Azure Otomasyonu’nda rol tabanlı erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="3e06e-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="3e06e-335">Azure Cloud Services’da sertifikalara genel bakış</span><span class="sxs-lookup"><span data-stu-id="3e06e-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
