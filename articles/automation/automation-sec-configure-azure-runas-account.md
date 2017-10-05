---
title: "Azure Farklı Çalıştır Hesabını Yapılandırma | Microsoft Docs"
description: "Bu öğretici, Azure Otomasyonu’nda güvenlik temel elemanı kimlik doğrulaması oluşturulması, test edilmesi ve örneklerinde size yol göstermektedir."
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
redirect_document_id: TRUE
ms.openlocfilehash: f88c775eba19bb227d0e206d6420c08b57305b92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="be17e-104">Azure Farklı Çalıştır hesabıyla kimlik doğrulaması runbook’ları</span><span class="sxs-lookup"><span data-stu-id="be17e-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="be17e-105">Bu makalede, Azure portalında bir Azure Otomasyonu hesabını yapılandırma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="be17e-105">This article shows you how to configure an Azure Automation account in the Azure portal.</span></span> <span data-ttu-id="be17e-106">Bunu yapmak için, Farklı Çalıştır hesabı özelliğini kullanarak Azure Resource Manager veya Azure Service Management’ta kaynakları yöneten runbook’ların kimliğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-106">To do so, you use the Run As account feature to authenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="be17e-107">Azure portalında bir Otomasyon hesabı oluşturduğunuzda otomatik olarak iki hesap oluşturursunuz:</span><span class="sxs-lookup"><span data-stu-id="be17e-107">When you create an Automation account in the Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="be17e-108">Bir Farklı Çalıştır hesabı.</span><span class="sxs-lookup"><span data-stu-id="be17e-108">A Run As account.</span></span> <span data-ttu-id="be17e-109">Bu hesap, Azure Active Directory'de (Azure AD) bir hizmet sorumlusu ve bir sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be17e-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="be17e-110">Ayrıca, runbook kullanarak Resource Manager kaynaklarını yöneten Katkıda Bulunan rol tabanlı erişim denetimi (RBAC) iznini atar.</span><span class="sxs-lookup"><span data-stu-id="be17e-110">It also assigns the Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="be17e-111">Klasik Farklı Çalıştır hesabı.</span><span class="sxs-lookup"><span data-stu-id="be17e-111">A Classic Run As account.</span></span> <span data-ttu-id="be17e-112">Bu hesap, runbook kullanarak Service Management’ı ya da klasik kaynakları yönetmek için kullanılan bir yönetim sertifikasını karşıya yükler.</span><span class="sxs-lookup"><span data-stu-id="be17e-112">This account uploads a management certificate, which is used to manage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="be17e-113">Bir Otomasyon hesabının oluşturulması, işlemi sizin için basitleştirir ve otomasyon gerekliliklerini desteklemek için runbook’ları oluşturmaya ve dağıtmaya hemen başlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="be17e-113">Creating an Automation account simplifies the process for you and helps you quickly start building and deploying runbooks to support your automation needs.</span></span>

<span data-ttu-id="be17e-114">Farklı Çalıştır ve Klasik Farklı Çalıştır hesapları ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be17e-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="be17e-115">Azure portalındaki runbook’lardan Resource Manager veya Service Management kaynakları yönetilirken Azure ile kimlik doğrulaması için standartlaştırılmış bir yol sağlama.</span><span class="sxs-lookup"><span data-stu-id="be17e-115">Provide a standardized way to authenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in the Azure portal.</span></span>
* <span data-ttu-id="be17e-116">Azure Uyarıları’nda yapılandırabileceğiniz genel runbook'ların kullanımını otomatikleştirme.</span><span class="sxs-lookup"><span data-stu-id="be17e-116">Automate the use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="be17e-117">Otomasyon genel runbook’larına sahip Azure [Uyarı tümleştirme özelliği](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) için Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabıyla yapılandırılmış bir Otomasyon hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="be17e-117">The [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="be17e-118">Farklı Çalıştır ve Klasik Farklı Çalıştır hesabı zaten tanımlanmış bir Otomasyon hesabı seçebilir ya da yeni bir Otomasyon hesabı oluşturmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose to create a new Automation account.</span></span>
>  

<span data-ttu-id="be17e-119">Bu makalede, Otomasyon hesabının Azure portalından oluşturulması, bir Otomasyon hesabının Azure PowerShell kullanılarak güncelleştirilmesi, hesap yapılandırmasının yönetilmesi ve runbook’larınızda kimlik doğrulamasının nasıl yapılacağı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="be17e-119">This article shows how to create an Automation account from the Azure portal, update an Automation account by using Azure PowerShell, manage the account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="be17e-120">Bir Otomasyon hesabı oluşturmaya başlamadan önce aşağıdakileri anlayın ve göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="be17e-120">Before you begin creating an Automation account, it's a good idea to understand and consider the following:</span></span>

* <span data-ttu-id="be17e-121">Bir Otomasyon hesabının oluşturulması, klasik veya Resource Manager dağıtım modelinde daha önce oluşturmuş olabileceğiniz Otomasyon hesaplarını etkilemez.</span><span class="sxs-lookup"><span data-stu-id="be17e-121">Creating an Automation account does not affect Automation accounts you might have already created in either the classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="be17e-122">İşlem yalnızca Azure portalında oluşturduğunuz Otomasyon hesapları için geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="be17e-122">The process works only for Automation accounts that you create in the Azure portal.</span></span> <span data-ttu-id="be17e-123">Klasik Azure portalından bir hesap oluşturulmaya çalışıldığında Farklı Çalıştır hesabının yapılandırması çoğaltılmaz.</span><span class="sxs-lookup"><span data-stu-id="be17e-123">Attempting to create an account from the Azure classic portal does not replicate the Run As account configuration.</span></span>
* <span data-ttu-id="be17e-124">Klasik kaynakları yönetmek için kullandığınız runbook’lar ve varlıklar (zamanlamalar veya değişkenler) zaten varsa ve yeni Klasik Farklı Çalıştır hesabında runbook’ların kimliğini doğrulamak istiyorsanız, aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="be17e-124">If you already have runbooks and assets (such as schedules or variables) in place to manage classic resources, and you want runbooks to authenticate with the new Classic Run As account, do either of the following:</span></span>

  * <span data-ttu-id="be17e-125">Klasik Farklı Çalıştır hesabı oluşturmak için "Farklı Çalıştır hesabınızı yönetme" bölümünde yer alan yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="be17e-125">To create a Classic Run As account, follow the instructions in the "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="be17e-126">Var olan hesabınızı güncelleştirmek için "PowerShell kullanarak Otomasyon hesabınızı güncelleştirme" bölümündeki PowerShell betiğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="be17e-126">To update your existing account, use the PowerShell script in the "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="be17e-127">Yeni Farklı Çalıştır hesabını ve Klasik Farklı Çalıştır Otomasyon hesabını kullanarak kimlik doğrulamak için mevcut runbook’larınızı [Kimlik doğrulaması kod örnekleri](#authentication-code-examples) bölümünde sağlanan örnek kod ile değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be17e-127">To authenticate by using the new Run As account and Classic Run As Automation account, you  need to modify your existing runbooks with the example code provided in the section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="be17e-128">Farklı Çalıştır hesabı, sertifika tabanlı hizmet sorumlusu kullanarak Resource Manager kaynaklarına göre kimlik doğrulaması içindir.</span><span class="sxs-lookup"><span data-stu-id="be17e-128">The Run As account is for authentication against Resource Manager resources using the certificate-based service principal.</span></span> <span data-ttu-id="be17e-129">Klasik Farklı Çalıştır hesabı ise bir yönetim sertifikası ile Service Management kaynaklarına göre kimlik doğrulaması içindir.</span><span class="sxs-lookup"><span data-stu-id="be17e-129">The Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-the-azure-portal"></a><span data-ttu-id="be17e-130">Azure portalından Otomasyon hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="be17e-130">Create an Automation account from the Azure portal</span></span>
<span data-ttu-id="be17e-131">Bu bölümde, Azure portalından hem bir Farklı Çalıştır hesabı hem de bir Klasik Farklı Çalıştır hesabı oluşturan Azure Otomasyonu hesabı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="be17e-131">In this section, you create an Azure Automation account from the Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="be17e-132">Bir Otomasyon hesabı oluşturmak için, Hizmet Yöneticileri rolünün bir üyesi veya aboneliğe erişim veren aboneliğin ortak yöneticisi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be17e-132">To create an Automation account, you must be a member of the Service Admins role or co-administrator of the subscription that is granting access to the subscription.</span></span> <span data-ttu-id="be17e-133">Ayrıca, bu aboneliğin varsayılan Active Directory örneğine kullanıcı olarak eklenmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be17e-133">You must also be added as a user to that subscription's default Active Directory instance.</span></span> <span data-ttu-id="be17e-134">Hesabın ayrıcalıklı bir role atanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="be17e-134">The account does not need to be assigned a privileged role.</span></span>
>
><span data-ttu-id="be17e-135">Aboneliğin ortak yönetici rolüne eklenmeden önce aboneliğin Active Directory örneğine üye değilseniz, Active Directory’ye konuk olarak eklenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-135">If you are not a member of the subscription’s Active Directory instance before you are added to the co-administrator role of the subscription, you will be added to Active Directory as a guest.</span></span> <span data-ttu-id="be17e-136">Bu örnekte, “Oluşturma izniniz yok…”</span><span class="sxs-lookup"><span data-stu-id="be17e-136">In this instance, you will receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="be17e-137">uyarısını **Otomasyon Hesabı Ekle** dikey penceresinde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="be17e-137">warning on the **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="be17e-138">İlk olarak ortak yönetici rolüne eklenen kullanıcılar aboneliğin Active Directory örneğinden kaldırılabilir ve tekrar eklenerek Active Directory’de tam bir Kullanıcı haline getirilebilir.</span><span class="sxs-lookup"><span data-stu-id="be17e-138">Users who were added to the co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="be17e-139">Bu durumu Azure portalındaki **Azure Active Directory** bölmesinde **Kullanıcılar ve gruplar**’ı ve **Tüm kullanıcılar**’ı seçtikten sonra gerekli kullanıcıyı belirleyip **Profil**’i seçerek doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-139">To verify this situation from the **Azure Active Directory** pane in the Azure portal by selecting **Users and groups**, selecting **All users** and, after you select the specific user, selecting **Profile**.</span></span> <span data-ttu-id="be17e-140">Kullanıcı profili altındaki **Kullanıcı türü** özniteliğinin **Konuk** olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be17e-140">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="be17e-141">Azure portalında abonelik yöneticileri rolünün üyesi ve aboneliğin ortak yöneticisi olan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="be17e-141">Sign in to the Azure portal with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>

2. <span data-ttu-id="be17e-142">**Automation Hesapları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="be17e-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="be17e-143">**Otomasyon Hesapları** dikey penceresinde **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-143">On the **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="be17e-144">**Otomasyon Hesabı Ekle** dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="be17e-144">The **Add Automation Account** blade opens.</span></span>

 ![“Otomasyon Hesabı Ekle” dikey penceresi](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="be17e-146">Hesabınız aboneliğin yönetici rolüne üye değilse veya aboneliğin ortak yöneticisi değilse, **Otomasyon Hesabı Ekle** dikey penceresinde şu uyarı gösterilir:</span><span class="sxs-lookup"><span data-stu-id="be17e-146">If your account is not a member of the subscription administrators role and co-administrator of the subscription, the following warning is displayed on the **Add Automation Account** blade:</span></span>
   >
   >![Automation Hesabı Uyarısı ekleme](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="be17e-148">**Otomasyon Hesabı Ekle** dikey penceresindeki **Ad** kutusuna yeni Otomasyon hesabınız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="be17e-148">On the **Add Automation Account** blade, in the **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="be17e-149">Birden fazla aboneliğiniz varsa aşağıdaki işlemleri yapın:</span><span class="sxs-lookup"><span data-stu-id="be17e-149">If you have more than one subscription, do the following:</span></span>

    <span data-ttu-id="be17e-150">a.</span><span class="sxs-lookup"><span data-stu-id="be17e-150">a.</span></span> <span data-ttu-id="be17e-151">**Abonelik** altında yeni hesap için bir abonelik belirtin.</span><span class="sxs-lookup"><span data-stu-id="be17e-151">Under **Subscription**, specify one for the new account.</span></span>

    <span data-ttu-id="be17e-152">b.</span><span class="sxs-lookup"><span data-stu-id="be17e-152">b.</span></span> <span data-ttu-id="be17e-153">**Kaynak Grubu** altında, **Yeni oluştur** veya **Var olanı kullan**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="be17e-154">c.</span><span class="sxs-lookup"><span data-stu-id="be17e-154">c.</span></span> <span data-ttu-id="be17e-155">**Konum** altında bir Azure veri merkezi belirtin.</span><span class="sxs-lookup"><span data-stu-id="be17e-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="be17e-156">**Azure Farklı Çalıştır hesabı oluştur** altında **Evet**’i seçin ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="be17e-157">**Hayır**’ı seçerek Farklı Çalıştır hesabı oluşturmamayı tercih ederseniz, **Otomasyon Hesabı Ekle** dikey penceresinde bir uyarı iletisi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="be17e-157">If you choose not to create the Run As account by selecting **No**, a warning message is displayed the **Add Automation Account** blade.</span></span> <span data-ttu-id="be17e-158">Hesap Azure portalında oluşturulsa da, klasik veya Resource Manager aboneliğinin dizin hizmetinde ona karşılık gelen bir kimlik doğrulama kimliği yoktur.</span><span class="sxs-lookup"><span data-stu-id="be17e-158">Although the account is created in the Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="be17e-159">Sonuç olarak hesap, aboneliğinizdeki kaynaklara erişemez.</span><span class="sxs-lookup"><span data-stu-id="be17e-159">Consequently, the account has no access to resources in your subscription.</span></span> <span data-ttu-id="be17e-160">Bu senaryo, ilgili dağıtım modellerindeki kaynaklara göre kimlik doğrulama ve görev gerçekleştirme işlemlerinden bu hesaba başvuran runbook’ları engeller.</span><span class="sxs-lookup"><span data-stu-id="be17e-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > !["Otomasyon Hesabı Ekle" dikey penceresindeki uyarı iletisi](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="be17e-162">Ayrıca, hizmet sorumlusu oluşturulmadığı için Katkıda Bulunan rolü atanmaz.</span><span class="sxs-lookup"><span data-stu-id="be17e-162">Additionally, because the service principal is not created, the Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="be17e-163">Azure Automation hesabını oluşturduğu sırada menünün **Bildirimler** öğesi altında ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-163">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="resources"></a><span data-ttu-id="be17e-164">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="be17e-164">Resources</span></span>
<span data-ttu-id="be17e-165">Otomasyon hesabı başarıyla oluşturulduğunda bazı kaynaklar sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="be17e-165">When the Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="be17e-166">Kaynaklar aşağıdaki iki tabloda özetlenmiştir:</span><span class="sxs-lookup"><span data-stu-id="be17e-166">The resources are summarized in the following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="be17e-167">Farklı Çalıştır hesabının kaynakları</span><span class="sxs-lookup"><span data-stu-id="be17e-167">Run As account resources</span></span>

| <span data-ttu-id="be17e-168">Kaynak</span><span class="sxs-lookup"><span data-stu-id="be17e-168">Resource</span></span> | <span data-ttu-id="be17e-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be17e-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="be17e-170">AzureAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="be17e-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="be17e-171">Farklı Çalıştır hesabını kullanarak kimlik doğrulaması yapmayı gösteren ve tüm Resource Manager kaynaklarını alan örnek bir grafik runbook.</span><span class="sxs-lookup"><span data-stu-id="be17e-171">An example graphical runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="be17e-172">AzureAutomationTutorialScript Runbook</span><span class="sxs-lookup"><span data-stu-id="be17e-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="be17e-173">Farklı Çalıştır hesabını kullanarak kimlik doğrulaması yapmayı gösteren ve tüm Resource Manager kaynaklarını alan örnek bir PowerShell runbook.</span><span class="sxs-lookup"><span data-stu-id="be17e-173">An example PowerShell runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="be17e-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="be17e-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="be17e-175">Bir Otomasyon hesabı oluşturduğunuzda veya var olan bir hesap için aşağıdaki PowerShell betiğini kullandığınızda otomatik olarak oluşturulan sertifika varlığı.</span><span class="sxs-lookup"><span data-stu-id="be17e-175">The certificate asset that's automatically created when you create an Automation account or use the following PowerShell script for an existing account.</span></span> <span data-ttu-id="be17e-176">Sertifika, Azure Resource Manager kaynaklarını runbook’lardan yönetebilmeniz için Azure kimlik doğrulaması yapmanıza imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="be17e-176">The certificate allows you to authenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="be17e-177">Bu sertifikanın bir yıllık kullanım ömrü vardır.</span><span class="sxs-lookup"><span data-stu-id="be17e-177">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="be17e-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="be17e-178">AzureRunAsConnection</span></span> | <span data-ttu-id="be17e-179">Bir Otomasyon hesabı oluşturduğunuzda veya var olan bir hesap için PowerShell betiğini kullandığınızda otomatik olarak oluşturulan bağlantı varlığı.</span><span class="sxs-lookup"><span data-stu-id="be17e-179">The connection asset that's automatically created when you create an Automation account or use the PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="be17e-180">Klasik Farklı Çalıştır hesabının kaynakları</span><span class="sxs-lookup"><span data-stu-id="be17e-180">Classic Run As account resources</span></span>

| <span data-ttu-id="be17e-181">Kaynak</span><span class="sxs-lookup"><span data-stu-id="be17e-181">Resource</span></span> | <span data-ttu-id="be17e-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be17e-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="be17e-183">AzureClassicAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="be17e-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="be17e-184">Klasik Farklı Çalıştır hesabı (sertifika) kullanarak, bir abonelikte klasik dağıtım modeli ile oluşturulan tüm VM’leri alan ve sonra VM adı ile durumunu yazan, örnek grafik runbook.</span><span class="sxs-lookup"><span data-stu-id="be17e-184">An example graphical runbook that gets all the VMs that are created using the classic deployment model in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="be17e-185">AzureClassicAutomationTutorial Script Runbook</span><span class="sxs-lookup"><span data-stu-id="be17e-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="be17e-186">Klasik Farklı Çalıştır hesabı (sertifika) kullanarak bir abonelikteki tüm klasik VM'leri alan ve sonra VM adını ve durumunu yazan, örnek PowerShell runbook.</span><span class="sxs-lookup"><span data-stu-id="be17e-186">An example PowerShell runbook that gets all the classic VMs in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="be17e-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="be17e-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="be17e-188">Otomatik olarak oluşturulan ve Azure klasik kaynaklarını runbook’lardan yönetebilmeniz için Azure kimlik doğrulaması yapmak üzere kullandığınız sertifika varlığı.</span><span class="sxs-lookup"><span data-stu-id="be17e-188">The automatically created certificate asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="be17e-189">Bu sertifikanın bir yıllık kullanım ömrü vardır.</span><span class="sxs-lookup"><span data-stu-id="be17e-189">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="be17e-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="be17e-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="be17e-191">Otomatik olarak oluşturulan ve Azure klasik kaynaklarını runbook’lardan yönetebilmeniz için Azure kimlik doğrulaması yapmak üzere kullandığınız bağlantı varlığı.</span><span class="sxs-lookup"><span data-stu-id="be17e-191">The automatically created connection asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="be17e-192">Farklı Çalıştır kimlik doğrulamasını onaylama</span><span class="sxs-lookup"><span data-stu-id="be17e-192">Verify Run As authentication</span></span>
<span data-ttu-id="be17e-193">Yeni Farklı Çalıştır hesabını kullanarak kimlik doğrulamasını sorunsuz yapabildiğinizi doğrulamak için küçük bir test gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="be17e-193">Perform a small test to confirm that you can successfully authenticate by using the new Run As account.</span></span>

1. <span data-ttu-id="be17e-194">Azure portalında, daha önce oluşturduğunuz Otomasyon hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="be17e-194">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="be17e-195">Runbook'ların listesini açmak için **Runbook'lar** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-195">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="be17e-196">**AzureAutomationTutorialScript** runbook’unu seçin ve ardından **Başlat**’a tıklayarak runbook’u başlatın.</span><span class="sxs-lookup"><span data-stu-id="be17e-196">Select the **AzureAutomationTutorialScript** runbook, and then click **Start** to start the runbook.</span></span> <span data-ttu-id="be17e-197">Aşağıdaki olaylar gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="be17e-197">The following events occur:</span></span>
 * <span data-ttu-id="be17e-198">Bir [runbook işi](automation-runbook-execution.md) oluşturulur, **İş** dikey penceresi gösterilir ve iş durumu **İş Özeti** kutucuğunda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="be17e-198">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="be17e-199">İş durumu, bulutta bir runbook çalışanının kullanılabilir hale gelmesinin beklendiğini gösteren şekilde **Sırada** olarak başlar.</span><span class="sxs-lookup"><span data-stu-id="be17e-199">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="be17e-200">Bir çalışan işi talep ettiğinde durum **Başlıyor** olur.</span><span class="sxs-lookup"><span data-stu-id="be17e-200">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="be17e-201">Runbook çalışmaya başladığında durum **Çalışıyor** olur.</span><span class="sxs-lookup"><span data-stu-id="be17e-201">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="be17e-202">Runbook işi tamamlandığında **Tamamlandı** durumunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be17e-202">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="be17e-203">Runbook’un ayrıntılı sonuçlarını görmek için **Çıktı** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-203">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="be17e-204">Runbook kimlik doğrulamasının başarıyla yapıldığını ve kaynak grubunda mevcut olan tüm kaynakların bir listesini döndürdüğünü gösteren **Çıktı** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="be17e-204">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all resources available in the resource group.</span></span>

5. <span data-ttu-id="be17e-205">**Çıktı** dikey penceresini kapatarak **İş Özeti** dikey penceresine geri dönün.</span><span class="sxs-lookup"><span data-stu-id="be17e-205">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="be17e-206">**İş Özeti** dikey penceresini ve karşılık gelen **AzureAutomationTutorialScript** runbook dikey penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="be17e-206">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="be17e-207">Klasik Farklı Çalıştır kimlik doğrulamasını onaylama</span><span class="sxs-lookup"><span data-stu-id="be17e-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="be17e-208">Yeni Klasik Farklı Çalıştır hesabını kullanarak kimlik doğrulamasını sorunsuz yapabildiğinizi doğrulamak için benzer bir küçük test gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="be17e-208">Perform a similar small test to confirm that you can successfully authenticate by using the new Classic Run As account.</span></span>

1. <span data-ttu-id="be17e-209">Azure portalında, daha önce oluşturduğunuz Otomasyon hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="be17e-209">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="be17e-210">Runbook'ların listesini açmak için **Runbook'lar** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-210">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="be17e-211">**AzureClassicAutomationTutorialScript** runbook’unu seçin ve ardından **Başlat**’a tıklayarak runbook’u başlatın.</span><span class="sxs-lookup"><span data-stu-id="be17e-211">Select the **AzureClassicAutomationTutorialScript** runbook, and then click **Start** to  start the runbook.</span></span> <span data-ttu-id="be17e-212">Aşağıdaki olaylar gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="be17e-212">The following events occur:</span></span>

 * <span data-ttu-id="be17e-213">Bir [runbook işi](automation-runbook-execution.md) oluşturulur, **İş** dikey penceresi gösterilir ve iş durumu **İş Özeti** kutucuğunda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="be17e-213">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="be17e-214">İş durumu, bulutta bir runbook çalışanının kullanılabilir hale gelmesinin beklendiğini gösteren şekilde **Sırada** olarak başlar.</span><span class="sxs-lookup"><span data-stu-id="be17e-214">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="be17e-215">Bir çalışan işi talep ettiğinde durum **Başlıyor** olur.</span><span class="sxs-lookup"><span data-stu-id="be17e-215">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="be17e-216">Runbook çalışmaya başladığında durum **Çalışıyor** olur.</span><span class="sxs-lookup"><span data-stu-id="be17e-216">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="be17e-217">Runbook işi tamamlandığında **Tamamlandı** durumunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be17e-217">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Güvenlik Sorumlusu Runbook Testi](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="be17e-219">Runbook’un ayrıntılı sonuçlarını görmek için **Çıktı** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-219">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="be17e-220">Runbook kimlik doğrulamasının başarıyla yapıldığını ve abonelikteki tüm klasik VM’lerin bir listesini döndürdüğünü gösteren **Çıktı** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="be17e-220">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all classic VMs in the subscription.</span></span>

5. <span data-ttu-id="be17e-221">**Çıktı** dikey penceresini kapatarak **İş Özeti** dikey penceresine geri dönün.</span><span class="sxs-lookup"><span data-stu-id="be17e-221">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="be17e-222">**İş Özeti** dikey penceresini ve karşılık gelen **AzureAutomationTutorialScript** runbook dikey penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="be17e-222">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="be17e-223">Farklı Çalıştır hesabınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="be17e-223">Managing your Run As account</span></span>
<span data-ttu-id="be17e-224">Otomasyon hesabınızın süresi dolmadan önce sertifikayı yenilemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be17e-224">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="be17e-225">Farklı Çalıştır hesabının tehlikede olduğunu düşünüyorsanız, hesabı silip yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-225">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="be17e-226">Bu bölümde bu işlemlerin nasıl gerçekleştirileceği ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="be17e-226">This section discusses how to perform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="be17e-227">Otomatik olarak imzalanan sertifika yenileme</span><span class="sxs-lookup"><span data-stu-id="be17e-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="be17e-228">Farklı Çalıştır hesabı için oluşturduğunuz otomatik olarak imzalanan sertifikanın süresi, oluşturulduktan bir yıl sonra dolar.</span><span class="sxs-lookup"><span data-stu-id="be17e-228">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="be17e-229">Sertifikayı süresi dolmadan önce herhangi bir zamanda yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="be17e-230">Sertifikayı yenilediğinizde, sıraya alınmış ya da o anda çalışan ve Farklı Çalıştır hesabı ile kimliği doğrulanmış runbook’ların olumsuz yönde etkilenmemesi için geçerli sertifika saklanır.</span><span class="sxs-lookup"><span data-stu-id="be17e-230">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="be17e-231">Sertifika, sona erme tarihine kadar geçerliliğini sürdürür.</span><span class="sxs-lookup"><span data-stu-id="be17e-231">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="be17e-232">Otomasyon Farklı Çalıştır hesabınızı, kuruluş sertifika yetkiliniz tarafından yayınlanan bir sertifika kullanmak üzere yapılandırdıysanız ve bu seçeneği kullanırsanız, kurumsal sertifika otomatik olarak imzalanan bir sertifikayla değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="be17e-232">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="be17e-233">Sertifikayı yenilemek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="be17e-233">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="be17e-234">Azure portalında Otomasyon hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="be17e-234">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="be17e-235">**Otomasyon Hesabı** dikey penceresindeki **Hesap özellikleri** bölmesinin **Hesap Ayarları** altında **Farklı Çalıştır Hesapları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="be17e-235">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Otomasyon hesabı özellikleri bölmesi](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="be17e-237">**Farklı Çalıştır Hesapları** özellikleri dikey penceresinde sertifikasını yenilemek istediğiniz Farklı Çalıştır Hesabını veya Klasik Farklı Çalıştır Hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="be17e-237">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="be17e-238">Seçili hesabın **Özellikler** dikey penceresinde **Sertifikayı yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-238">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Farklı Çalıştır hesabının sertifikasını yenileme](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="be17e-240">Sertifika yenilenirken menünün **Bildirimler** öğesi altında ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-240">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="be17e-241">Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını silme</span><span class="sxs-lookup"><span data-stu-id="be17e-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="be17e-242">Bu bölümde bir Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını silip yeniden oluşturma işlemi açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="be17e-242">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="be17e-243">Bu eylemi gerçekleştirdiğinizde Otomasyon hesabı korunur.</span><span class="sxs-lookup"><span data-stu-id="be17e-243">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="be17e-244">Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını sildikten sonra Azure portalında yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-244">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="be17e-245">Azure portalında Otomasyon hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="be17e-245">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="be17e-246">**Otomasyon Hesabı** dikey penceresindeki hesap özellikleri bölmesinde **Farklı Çalıştır Hesapları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="be17e-246">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="be17e-247">**Farklı Çalıştır Hesapları** özellikleri dikey penceresinde silmek istediğiniz Farklı Çalıştır Hesabını veya Klasik Farklı Çalıştır Hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="be17e-247">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="be17e-248">Ardından, seçili hesabın **Özellikler** dikey penceresinde **Sil**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-248">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Farklı Çalıştır hesabını silme](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="be17e-250">Hesap silinirken menünün **Bildirimler** öğesi altında ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-250">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="be17e-251">Hesap silindikten sonra **Farklı Çalıştır Hesapları** özellikler dikey penceresinde **Azure Farklı Çalıştır Hesabı** seçeneğini belirleyerek hesabı yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-251">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Otomasyon Farklı Çalıştır hesabını yeniden oluşturma](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="be17e-253">Yanlış yapılandırma</span><span class="sxs-lookup"><span data-stu-id="be17e-253">Misconfiguration</span></span>
<span data-ttu-id="be17e-254">İlk kurulum sırasında, Farklı Çalıştır veya Klasik Farklı Çalıştır hesabının düzgün çalışması için gerekli olan bazıları silinmiş veya düzgün oluşturulmamış olabilir.</span><span class="sxs-lookup"><span data-stu-id="be17e-254">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="be17e-255">Bu öğeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="be17e-255">The items include:</span></span>

* <span data-ttu-id="be17e-256">Sertifika varlığı</span><span class="sxs-lookup"><span data-stu-id="be17e-256">Certificate asset</span></span>
* <span data-ttu-id="be17e-257">Bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="be17e-257">Connection asset</span></span>
* <span data-ttu-id="be17e-258">Farklı Çalıştır hesabının katkıda bulunan rolünden kaldırılması</span><span class="sxs-lookup"><span data-stu-id="be17e-258">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="be17e-259">Azure AD'de hizmet sorumlusu veya uygulama</span><span class="sxs-lookup"><span data-stu-id="be17e-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="be17e-260">Yanlış yapılandırmanın önceki ve diğer örneklerinde, Otomasyon hesabı değişiklikleri algılar ve hesabın **Farklı Çalıştır Hesapları** özellikleri dikey penceresinde *Tamamlanmadı* durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="be17e-260">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Tamamlanmamış Farklı Çalıştır hesabı yapılandırma durumu](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="be17e-262">Farklı Çalıştır hesabını seçtiğinizde hesabın **Özellikler** bölmesinde aşağıdaki hata iletisi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="be17e-262">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Tamamlanmamış Farklı Çalıştır yapılandırma uyarısı iletisi](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="be17e-264">.</span><span class="sxs-lookup"><span data-stu-id="be17e-264">.</span></span>

<span data-ttu-id="be17e-265">Hesabı silip yeniden oluşturarak Farklı Çalıştır hesabıyla ilgili bu sorunları hızlı bir şekilde çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-265">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="be17e-266">PowerShell kullanarak Otomasyon hesabınızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="be17e-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="be17e-267">Aşağıdaki durumlarda var olan Otomasyon hesabınızı güncelleştirmek için PowerShell kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be17e-267">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="be17e-268">Bir Otomasyon hesabı oluşturdunuz, ancak Farklı Çalıştır hesabı oluşturmayı reddettiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-268">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="be17e-269">Resource Manager kaynaklarını yönetmek için bir Otomasyon hesabı zaten kullanıyorsunuz ve runbook kimlik doğrulaması için Farklı Çalıştır hesabını içerecek şekilde güncelleştirmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="be17e-269">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="be17e-270">Klasik kaynakları yönetmek için bir Otomasyon hesabı zaten kullanıyorsunuz ve yeni bir hesap oluşturup runbook’larınızı ve varlıklarınızı ona geçirmek yerine Klasik Farklı Çalıştır hesabını kullanacak şekilde güncelleştirmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="be17e-270">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="be17e-271">Kuruluş sertifika yetkiliniz (CA) tarafından verilen bir sertifika kullanarak bir Farklı Çalıştır ve Klasik Farklı Çalıştır hesabı oluşturmak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="be17e-271">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="be17e-272">Betiğin aşağıdaki önkoşulları vardır:</span><span class="sxs-lookup"><span data-stu-id="be17e-272">The script has the following prerequisites:</span></span>

* <span data-ttu-id="be17e-273">Betik yalnızca Azure Resource Manager 2.01 veya sonrasındaki modülleri içeren Windows 10 ve Windows Server 2016 işletim sistemlerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="be17e-273">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="be17e-274">Windows'un önceki sürümleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="be17e-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="be17e-275">Azure PowerShell 1.0 ve üzeri.</span><span class="sxs-lookup"><span data-stu-id="be17e-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="be17e-276">PowerShell 1.0 sürümü hakkında bilgi için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="be17e-276">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="be17e-277">Aşağıdaki PowerShell betiğinde *–AutomationAccountName* ve *-ApplicationDisplayName* parametrelerinin değeri olarak başvurulan bir Otomasyon hesabı.</span><span class="sxs-lookup"><span data-stu-id="be17e-277">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="be17e-278">Betiklerin parametreleri için gerekli olan *SubscriptionID*, *ResourceGroup* ve *AutomationAccountName* değerlerini almak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="be17e-278">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="be17e-279">Azure portalında, **Otomasyon hesabı** dikey penceresinden Otomasyon hesabınızı ve ardından **Tüm ayarlar** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="be17e-279">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="be17e-280">**Tüm ayarlar** dikey penceresindeki **Hesap Ayarları** altında **Özellikler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="be17e-280">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="be17e-281">**Özellikler** dikey penceresindeki değerleri not alın.</span><span class="sxs-lookup"><span data-stu-id="be17e-281">Note the values on the **Properties** blade.</span></span>

![Otomasyon hesabı "Özellikler" dikey penceresi](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="be17e-283">Farklı Çalıştır hesabı PowerShell betiği oluşturma</span><span class="sxs-lookup"><span data-stu-id="be17e-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="be17e-284">Bu PowerShell betiği aşağıdaki yapılandırmalar için destek içerir:</span><span class="sxs-lookup"><span data-stu-id="be17e-284">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="be17e-285">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be17e-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="be17e-286">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be17e-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="be17e-287">Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be17e-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="be17e-288">Azure Kamu bulutunda otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be17e-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="be17e-289">Seçtiğiniz yapılandırma seçeneğine bağlı olarak, betik aşağıdaki öğeleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be17e-289">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="be17e-290">**Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="be17e-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="be17e-291">Otomatik olarak imzalanan sertifika veya kurumsal sertifika ortak anahtarıyla dışarı aktarılacak bir Azure AD uygulaması oluşturur, Azure AD’de bu uygulama için bir hizmet sorumlusu hesabı oluşturur ve geçerli aboneliğinizde hesap için Katkıda Bulunan rolünü atar.</span><span class="sxs-lookup"><span data-stu-id="be17e-291">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="be17e-292">Bu ayarı Sahip veya başka bir rolle değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-292">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="be17e-293">Daha fazla bilgi için bkz. [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="be17e-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="be17e-294">Belirtilen Otomasyon hesabında *AzureRunAsCertificate* adlı bir Otomasyon sertifikası varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be17e-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="be17e-295">Sertifika varlıkları, Azure AD uygulaması tarafından kullanılan sertifika özel anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="be17e-295">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="be17e-296">Belirtilen Otomasyon hesabında *AzureRunAsConnection* adlı bir Otomasyon bağlantı varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be17e-296">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="be17e-297">Bağlantı varlığı applicationId, tenantId, subscriptionId ve sertifika parmak izini içerir.</span><span class="sxs-lookup"><span data-stu-id="be17e-297">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="be17e-298">**Klasik Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="be17e-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="be17e-299">Belirtilen Otomasyon hesabında *AzureClassicRunAsCertificate* adlı bir Otomasyon sertifikası varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be17e-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="be17e-300">Sertifika varlığı, yönetim sertifikası tarafından kullanılan sertifika özel anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="be17e-300">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="be17e-301">Belirtilen Otomasyon hesabında *AzureClassicRunAsConnection* adlı bir Otomasyon bağlantı varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be17e-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="be17e-302">Bağlantı varlığı; abonelik adı, subscriptionId ve sertifika varlık adını içerir.</span><span class="sxs-lookup"><span data-stu-id="be17e-302">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="be17e-303">Klasik Farklı Çalıştır hesabı oluşturma seçeneğini belirlerseniz, betik yürütüldükten sonra Otomasyon hesabının oluşturulduğu abonelik için yönetim deposuna ortak sertifikayı (.cer dosya adı uzantısı) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="be17e-303">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

<span data-ttu-id="be17e-304">Betiği yürütüp sertifikayı karşıya yüklemek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="be17e-304">To execute the script and upload the certificate, do the following:</span></span>

1. <span data-ttu-id="be17e-305">Aşağıdaki betiği bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="be17e-305">Save the following script on your computer.</span></span> <span data-ttu-id="be17e-306">Bu örnekte *New-RunAsAccount.ps1* dosya adıyla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="be17e-306">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                    "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="be17e-307">Bilgisayarınızda **Başlat**’a tıklayın ve yükseltilmiş kullanıcı haklarıyla **Windows PowerShell**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="be17e-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="be17e-308">Yükseltilmiş PowerShell komut satırı kabuğundan, 1. adımda oluşturduğunuz komut dosyasını içeren klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="be17e-308">From the elevated PowerShell command-line shell, go to the folder that contains the script you created in step 1.</span></span>

4. <span data-ttu-id="be17e-309">İstediğiniz yapılandırmanın parametre değerlerini kullanarak betiği yürütün.</span><span class="sxs-lookup"><span data-stu-id="be17e-309">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="be17e-310">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="be17e-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="be17e-311">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="be17e-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="be17e-312">**Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="be17e-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="be17e-313">**Azure Kamu bulutunda otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="be17e-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="be17e-314">Betik yürütüldükten sonra Azure kimlik doğrulamasını yapmanız istenecektir.</span><span class="sxs-lookup"><span data-stu-id="be17e-314">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="be17e-315">Aboneliğin yöneticiler rolünün üyesi ve aboneliğin ortak yöneticisi olan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="be17e-315">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="be17e-316">Betik başarıyla yürütüldükten sonra aşağıdakilere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="be17e-316">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="be17e-317">Otomatik olarak imzalanan bir ortak sertifika (.cer dosyası) ile Klasik Farklı Çalıştır hesabı oluşturduysanız, betik bu hesabı oluşturup bilgisayarınızdaki geçici dosya klasörüne, PowerShell oturumunu yürütmek için kullandığınız *%USERPROFILE%\AppData\Local\Temp* kullanıcı profili altında kaydeder.</span><span class="sxs-lookup"><span data-stu-id="be17e-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="be17e-318">Kurumsal ortak sertifika (.cer file) ile bir Klasik Farklı Çalıştır hesabı oluşturduysanız bu sertifikayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="be17e-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="be17e-319">[Klasik Azure portalında yönetim API sertifikayı yükleme](../azure-api-management-certs.md) yönergelerini izleyin ve ardından [Service Management Kaynakları ile kimlik doğrulamaya yönelik örnek kodu](#sample-code-to-authenticate-with-service-management-resources) kullanarak Service Management kaynakları ile kimlik bilgisi yapılandırmasını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="be17e-319">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with Service Management resources by using the [sample code to authenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="be17e-320">Klasik Farklı Çalıştır hesabı *oluşturmadıysanız*, Resource Manager kaynakları kimlik doğrulaması yapmak ve kimlik bilgisi yapılandırmasını doğrulamak için [Service Management kaynakları ile kimlik doğrulamaya yönelik örnek kodu](#sample-code-to-authenticate-with-resource-manager-resources) kullanın.</span><span class="sxs-lookup"><span data-stu-id="be17e-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-to-authenticate-with-resource-manager-resources"></a><span data-ttu-id="be17e-321">Resource Manager kaynaklarıyla kimlik doğrulaması için örnek kod</span><span class="sxs-lookup"><span data-stu-id="be17e-321">Sample code to authenticate with Resource Manager resources</span></span>
<span data-ttu-id="be17e-322">Runbook’larınızla Resource Manager kaynaklarını yönetecek Farklı Çalıştır hesabını kullanarak kimlik doğrulaması yapmak için *AzureAutomationTutorialScript* örnek runbook’undan alınan aşağıdaki güncelleştirilmiş örnek kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-322">You can use the following updated sample code, taken from the *AzureAutomationTutorialScript* example runbook, to authenticate by using the Run As account to manage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get the connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in to Azure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context to a specific subscription"     
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

<span data-ttu-id="be17e-323">Bu betikte, birden fazla abonelik arasında kolayca çalışmanıza yardımcı olmak üzere abonelik bağlamına başvuruyu destekleyen iki ek kod satırı bulunur.</span><span class="sxs-lookup"><span data-stu-id="be17e-323">To help you to easily work between multiple subscriptions, the script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="be17e-324">*SubscriptionId* adlı değişken varlık, aboneliğin kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="be17e-324">A variable asset named *SubscriptionId* contains the ID of the subscription.</span></span> <span data-ttu-id="be17e-325">`Add-AzureRmAccount` cmdlet’i belirtildikten sonra *-SubscriptionId* parametre kümesi ile [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet’i belirtilir.</span><span class="sxs-lookup"><span data-stu-id="be17e-325">After the `Add-AzureRmAccount` cmdlet statement, the [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with the parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="be17e-326">Değişken adı çok genelse, tanımlanmasını kolaylaştırmak amacıyla bir ön ek veya başka diğer adlandırma kuralı kullanmak için değişken adını gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-326">If the variable name is too generic, you can revise it to include a prefix or use another naming convention to make it easier to identify.</span></span> <span data-ttu-id="be17e-327">Alternatif olarak, ilgili değişken varlığıyla *-SubscriptionId* yerine *-SubscriptionName* parametre kümesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-327">Alternatively, you can use the parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="be17e-328">Runbook’ta kimlik doğrulaması için kullandığınız cmdlet `Add-AzureRmAccount`, *ServicePrincipalCertificate* parametre kümesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="be17e-328">The cmdlet that you use for authenticating in the runbook, `Add-AzureRmAccount`, uses the *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="be17e-329">Kullanıcı kimlik bilgilerini değil, hizmet sorumlusu sertifikasını kullanarak kimlik doğrulaması yapar.</span><span class="sxs-lookup"><span data-stu-id="be17e-329">It authenticates by using the service principal certificate, not the user credentials.</span></span>

## <a name="sample-code-to-authenticate-with-service-management-resources"></a><span data-ttu-id="be17e-330">Service Management kaynaklarıyla kimlik doğrulaması için örnek kod</span><span class="sxs-lookup"><span data-stu-id="be17e-330">Sample code to authenticate with Service Management resources</span></span>
<span data-ttu-id="be17e-331">Runbook’larınızla klasik kaynakları yönetecek Klasik Farklı Çalıştır hesabını kullanarak kimlik doğrulaması yapmak için *AzureClassicAutomationTutorialScript* örnek runbook’undan alınan aşağıdaki güncelleştirilmiş örnek kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be17e-331">You can use the following updated sample code, which is taken from the *AzureClassicAutomationTutorialScript* example runbook, to authenticate by using the Classic Run As account to manage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="be17e-332">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be17e-332">Next steps</span></span>
* [<span data-ttu-id="be17e-333">Azure AD’de uygulama ve hizmet sorumlusu nesneleri</span><span class="sxs-lookup"><span data-stu-id="be17e-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="be17e-334">Azure Otomasyonu’nda rol tabanlı erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="be17e-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="be17e-335">Azure Cloud Services’da sertifikalara genel bakış</span><span class="sxs-lookup"><span data-stu-id="be17e-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
