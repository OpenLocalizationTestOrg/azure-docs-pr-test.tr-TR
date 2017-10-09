---
title: "aaaCreate Azure Automation farklı çalıştır hesapları | Microsoft Docs"
description: "Bu makalede nasıl tooupdate, Otomasyon hesabı ve PowerShell ile ya da hello Portalı'ndan farklı çalıştır hesapları oluşturun."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="30d3e-103">Farklı Çalıştır hesaplarıyla Otomasyon hesabı kimlik doğrulamasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="30d3e-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="30d3e-104">Merhaba portalından var olan Otomasyon hesabınızı güncelleştirmek veya PowerShell kullanın:</span><span class="sxs-lookup"><span data-stu-id="30d3e-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="30d3e-105">Automation hesabı oluşturma ancak toocreate hello farklı çalıştır hesabı reddedin.</span><span class="sxs-lookup"><span data-stu-id="30d3e-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="30d3e-106">Runbook kimlik doğrulaması için tooupdate hello tooinclude hello farklı çalıştır hesabı istediğiniz ve zaten bir Automation hesabı toomanage Resource Manager kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="30d3e-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="30d3e-107">Zaten bir Automation hesabı toomanage Klasik kaynakları kullanır ve tooupdate isterseniz bunu toouse hello yeni bir hesap oluşturma ve runbook'ları ve varlıkları tooit geçirmek yerine Klasik farklı çalıştır hesabı.</span><span class="sxs-lookup"><span data-stu-id="30d3e-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="30d3e-108">Kuruluş sertifika yetkilisi (CA) tarafından verilen bir sertifikayı kullanarak toocreate bir farklı çalıştır ve klasik farklı çalıştır hesabı istiyor.</span><span class="sxs-lookup"><span data-stu-id="30d3e-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30d3e-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="30d3e-109">Prerequisites</span></span>

* <span data-ttu-id="30d3e-110">Merhaba komut dosyası çalıştırma yalnızca Windows 10 ve Windows Server 2016 ile Azure Resource Manager modüllerini 3.0.0 ve daha sonra olabilir.</span><span class="sxs-lookup"><span data-stu-id="30d3e-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="30d3e-111">Windows'un önceki sürümleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="30d3e-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="30d3e-112">Azure PowerShell 1.0 ve üzeri.</span><span class="sxs-lookup"><span data-stu-id="30d3e-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="30d3e-113">Hello PowerShell 1.0 sürümü hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="30d3e-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="30d3e-114">Merhaba hello değeri olarak başvurulan bir Otomasyon hesabı *– AutomationAccountName* ve *- ApplicationDisplayName* hello PowerShell Betiği aşağıdaki parametreleri.</span><span class="sxs-lookup"><span data-stu-id="30d3e-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="30d3e-115">tooget hello değerleri *Subscriptionıd*, *ResourceGroup*, ve *AutomationAccountName*hello komut dosyası için gerekli parametreler olan, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="30d3e-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="30d3e-116">İçinde Azure portal Merhaba, Automation hesabınızı hello üzerinde seçin **Otomasyon hesabı** dikey ve ardından **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="30d3e-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="30d3e-117">Merhaba üzerinde **tüm ayarları** dikey altında **hesap ayarlarını**seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="30d3e-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="30d3e-118">Not hello hello değerlerine **özellikleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="30d3e-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="30d3e-119">![Merhaba Otomasyon hesabı "Özellikler" dikey](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="30d3e-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="30d3e-120">Otomasyon hesabınızı izinleri tooupdate gerekli</span><span class="sxs-lookup"><span data-stu-id="30d3e-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="30d3e-121">Bu konuda toocomplete gereken izinler ve tooupdate bir Otomasyon hesabı, belirli ayrıcalıkları aşağıdaki hello sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="30d3e-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="30d3e-122">AD kullanıcı hesabınızın makalesinde ana hatlarıyla toobe eklenen tooa rolü izinleri eşdeğer toohello katkıda bulunan rolü ile Microsoft.Automation kaynaklar için gereken [Azure automation'da rol tabanlı erişim denetimi](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="30d3e-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="30d3e-123">Azure AD kiracınızda yönetici olmayan kullanıcılar [AD uygulamaları kaydetmek](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) hello uygulama kayıtlar ayarı ayarlarsanız çok**Evet**.</span><span class="sxs-lookup"><span data-stu-id="30d3e-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="30d3e-124">Merhaba uygulama kayıtlar ayarı ayarlarsanız çok**Hayır**, hello kullanıcının bu eylemi gerçekleştirmeden Azure AD genel yönetici olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="30d3e-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="30d3e-125">Toohello genel yönetici/co-administrator rolüne hello abonelik eklenmeden önce hello aboneliğinin Active Directory örneğine üyesi değilseniz, tooActive dizinine konuk olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="30d3e-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="30d3e-126">Bu durumda, bir "sahip olmadığınız izinleri toocreate..." alırsınız.</span><span class="sxs-lookup"><span data-stu-id="30d3e-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="30d3e-127">Merhaba üzerinde uyarı **Automation hesabı Ekle** dikey.</span><span class="sxs-lookup"><span data-stu-id="30d3e-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="30d3e-128">Toohello genel yönetici/co-administrator rolüne ilk hello aboneliğinin Active Directory örneğinden kaldırılabilir ve yeniden, toomake eklendi eklenen kullanıcılar bunları Active Directory'de tam bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="30d3e-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="30d3e-129">tooverify bu durumdan hello **Azure Active Directory** hello Azure portal, select bölmesinde **kullanıcılar ve gruplar**seçin **tüm kullanıcılar** ve hello seçtikten sonra belirli bir kullanıcı, select **profil**.</span><span class="sxs-lookup"><span data-stu-id="30d3e-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="30d3e-130">Merhaba hello değerini **kullanıcı türü** hello kullanıcı profili altındaki özniteliğini eşit değil **Konuk**.</span><span class="sxs-lookup"><span data-stu-id="30d3e-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="30d3e-131">Merhaba Portalı'ndan farklı çalıştır hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="30d3e-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="30d3e-132">Bu bölümde, aşağıdaki adımları tooupdate hello hello Azure portal ' Azure Otomasyonu hesabınızı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="30d3e-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="30d3e-133">Merhaba farklı çalıştır ve klasik farklı çalıştır hesapları ayrı ayrı oluşturduğunuz ve toomanage kaynakları hello Klasik Azure portalında gerekmiyorsa, yalnızca hello Azure farklı çalıştır hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30d3e-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="30d3e-134">Merhaba işlemi aşağıdaki Otomasyon hesabınızda öğelerindeki hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="30d3e-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="30d3e-135">**Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="30d3e-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="30d3e-136">Otomatik olarak imzalanan bir sertifika ile Azure AD uygulaması oluşturur, Azure AD'de Merhaba uygulaması için bir hizmet sorumlusu hesabı oluşturur ve hello geçerli aboneliğinizde hello hesap için katılımcı rolü atar.</span><span class="sxs-lookup"><span data-stu-id="30d3e-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="30d3e-137">Bu ayar tooOwner veya başka bir rolle değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30d3e-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="30d3e-138">Daha fazla bilgi için bkz. [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="30d3e-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="30d3e-139">Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureRunAsCertificate* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="30d3e-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="30d3e-140">Merhaba sertifika varlığı hello Azure AD uygulama tarafından kullanılan hello sertifika özel anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="30d3e-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="30d3e-141">Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureRunAsConnection* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="30d3e-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="30d3e-142">Merhaba bağlantı varlığı hello ApplicationId, Tenantıd, Subscriptionıd ve sertifika parmak izi tutar.</span><span class="sxs-lookup"><span data-stu-id="30d3e-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="30d3e-143">**Klasik Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="30d3e-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="30d3e-144">Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureClassicRunAsCertificate* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="30d3e-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="30d3e-145">Merhaba sertifika varlığı hello yönetim sertifikası tarafından kullanılan hello sertifika özel anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="30d3e-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="30d3e-146">Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureClassicRunAsConnection* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="30d3e-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="30d3e-147">Merhaba bağlantı varlığı hello abonelik adı, Subscriptionıd ve sertifika varlık adı tutar.</span><span class="sxs-lookup"><span data-stu-id="30d3e-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="30d3e-148">Toohello Azure portal hello abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="30d3e-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="30d3e-149">Merhaba Otomasyon hesabı dikey penceresinden seçin **farklı çalıştır hesapları** hello bölümünde **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="30d3e-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="30d3e-150">Gereken hesaba bağlı olarak **Azure Farklı Çalıştır Hesabı**’nı veya **Azure Klasik Farklı Çalıştır Hesabı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="30d3e-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="30d3e-151">Ya da hello seçtikten sonra **eklemek Azure Farklı Çalıştır** veya **eklemek Azure Klasik farklı çalıştır hesabı** dikey penceresinde görüntülenir ve hello genel bakış bilgileri gözden geçirdikten sonra tıklatın **oluşturma** Farklı Çalıştır hesabı oluşturma ile tooproceed.</span><span class="sxs-lookup"><span data-stu-id="30d3e-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="30d3e-152">Azure hello farklı çalıştır hesabını oluşturduğu sırada altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menü ve bir başlık görüntülenir belirten hello hesabı oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="30d3e-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="30d3e-153">Bu işlem birkaç dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="30d3e-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="30d3e-154">PowerShell betiği ile Farklı Çalıştır hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="30d3e-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="30d3e-155">Bu PowerShell Betiği yapılandırmaları aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="30d3e-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="30d3e-156">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="30d3e-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="30d3e-157">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="30d3e-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="30d3e-158">Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="30d3e-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="30d3e-159">Hello Azure Bulutu kendinden imzalı bir sertifika kullanarak bir farklı çalıştır hesabı ve klasik farklı çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="30d3e-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="30d3e-160">Seçtiğiniz hello yapılandırma seçeneğine bağlı olarak aşağıdaki öğelerindeki hello hello komut dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="30d3e-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="30d3e-161">**Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="30d3e-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="30d3e-162">Bir Azure oluşturduğu AD uygulama toobe verilen kendinden imzalı ya da hello ile veya Kurumsal Sertifika genel anahtarı, Azure AD'de Merhaba uygulaması için bir hizmet sorumlusu hesabı oluşturur ve hello mevcut hello hesap için katılımcı rolü atar aboneliği.</span><span class="sxs-lookup"><span data-stu-id="30d3e-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="30d3e-163">Bu ayar tooOwner veya başka bir rolle değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30d3e-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="30d3e-164">Daha fazla bilgi için bkz. [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="30d3e-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="30d3e-165">Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureRunAsCertificate* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="30d3e-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="30d3e-166">Merhaba sertifika varlığı hello Azure AD uygulama tarafından kullanılan hello sertifika özel anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="30d3e-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="30d3e-167">Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureRunAsConnection* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="30d3e-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="30d3e-168">Merhaba bağlantı varlığı hello ApplicationId, Tenantıd, Subscriptionıd ve sertifika parmak izi tutar.</span><span class="sxs-lookup"><span data-stu-id="30d3e-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="30d3e-169">**Klasik Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="30d3e-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="30d3e-170">Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureClassicRunAsCertificate* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="30d3e-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="30d3e-171">Merhaba sertifika varlığı hello yönetim sertifikası tarafından kullanılan hello sertifika özel anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="30d3e-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="30d3e-172">Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureClassicRunAsConnection* hello Otomasyon hesabı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="30d3e-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="30d3e-173">Merhaba bağlantı varlığı hello abonelik adı, Subscriptionıd ve sertifika varlık adı tutar.</span><span class="sxs-lookup"><span data-stu-id="30d3e-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="30d3e-174">Merhaba betik yürütüldükten sonra Klasik farklı çalıştır hesabı oluşturmak için her iki seçeneği seçerseniz, karşıya yükleme hello ortak sertifika (.cer dosya adı uzantısı) toohello yönetim deposu hello abonelik için bu hello Otomasyon hesabı içinde oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="30d3e-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="30d3e-175">Komut dosyası, bilgisayarınızda aşağıdaki hello kaydedin.</span><span class="sxs-lookup"><span data-stu-id="30d3e-175">Save hello following script on your computer.</span></span> <span data-ttu-id="30d3e-176">İsteğe bağlı olarak bu örnekte, hello dosya adıyla kaydedin *yeni RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="30d3e-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
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
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="30d3e-177">Bilgisayarınızda Başlat **Windows PowerShell** hello gelen **Başlat** yükseltilmiş kullanıcı haklarıyla ekran.</span><span class="sxs-lookup"><span data-stu-id="30d3e-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="30d3e-178">Hello komut satırı kabuğundan, 1. adımda oluşturduğunuz hello betik içeren gidin toohello klasörü yükseltilmiş.</span><span class="sxs-lookup"><span data-stu-id="30d3e-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="30d3e-179">İçin gerek duyduğunuz hello yapılandırma hello parametre değerlerini kullanarak Hello betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="30d3e-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="30d3e-180">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="30d3e-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="30d3e-181">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="30d3e-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="30d3e-182">**Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="30d3e-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="30d3e-183">**Hello Azure Bulutu kendinden imzalı bir sertifika kullanarak bir farklı çalıştır hesabı ve klasik farklı çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="30d3e-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="30d3e-184">Merhaba betiği yürüttükten sonra Azure ile istendiğinde tooauthenticate olacaktır.</span><span class="sxs-lookup"><span data-stu-id="30d3e-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="30d3e-185">Merhaba abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="30d3e-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="30d3e-186">Merhaba betiği başarıyla yürütüldü sonra hello aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="30d3e-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="30d3e-187">Otomatik olarak imzalanan bir PKI sertifikası (.cer dosyası) ile bir Klasik farklı çalıştır hesabını oluşturduysanız, hello komut dosyası oluşturur ve bilgisayarınızda hello kullanıcı profili altındaki toohello geçici dosyalar klasörüne kaydeder *%USERPROFILE%\AppData\Local\Temp*, tooexecute hello PowerShell oturumu kullanılan.</span><span class="sxs-lookup"><span data-stu-id="30d3e-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="30d3e-188">Kurumsal ortak sertifika (.cer file) ile bir Klasik Farklı Çalıştır hesabı oluşturduysanız bu sertifikayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="30d3e-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="30d3e-189">Merhaba yönergeleri izleyin [yönetim API sertifikası toohello Klasik Azure portalı karşıya](../azure-api-management-certs.md)ve ardından hello kullanarak Klasik dağıtım kaynaklarla hello kimlik bilgisi yapılandırmasını doğrulamak [örnek kod Azure Klasik dağıtım kaynaklarla tooauthenticate](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="30d3e-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="30d3e-190">Kaldırdıysanız *değil* Klasik farklı çalıştır hesabı oluşturma, Resource Manager kaynaklarıyla kimlik doğrulaması ve hello kullanarak hello kimlik bilgisi yapılandırmasını doğrulamak [örnek Hizmet Yönetimi ile kimlik doğrulaması için kod Kaynakları](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="30d3e-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="30d3e-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="30d3e-191">Next steps</span></span>
* <span data-ttu-id="30d3e-192">Hizmet sorumluları hakkında daha fazla bilgi için çok başvuran[uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="30d3e-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="30d3e-193">Sertifikalar ve Azure hizmetleri hakkında daha fazla bilgi için çok başvuran[Azure Cloud Services sertifikalarına genel bakış](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="30d3e-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
