---
title: "Azure Otomasyonu Farklı Çalıştır Hesapları oluşturma | Microsoft Docs"
description: "Bu makalede, Otomasyon hesabınızı güncelleştirme ve PowerShell ile ya da portaldan Farklı Çalıştır hesapları oluşturma işlemi açıklanmaktadır."
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
ms.openlocfilehash: eaf6eb49bbfe4572827fcc101d1f552b48ab91e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="453fc-103">Farklı Çalıştır hesaplarıyla Otomasyon hesabı kimlik doğrulamasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="453fc-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="453fc-104">Mevcut Otomasyon hesabınızı portaldan güncelleştirebilir veya aşağıdaki durumlarda PowerShell kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="453fc-104">You can update your existing Automation account from the portal or use PowerShell if:</span></span>

* <span data-ttu-id="453fc-105">Bir Otomasyon hesabı oluşturdunuz, ancak Farklı Çalıştır hesabı oluşturmayı reddettiniz.</span><span class="sxs-lookup"><span data-stu-id="453fc-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="453fc-106">Resource Manager kaynaklarını yönetmek için bir Otomasyon hesabı zaten kullanıyorsunuz ve runbook kimlik doğrulaması için Farklı Çalıştır hesabını içerecek şekilde güncelleştirmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="453fc-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="453fc-107">Klasik kaynakları yönetmek için bir Otomasyon hesabı zaten kullanıyorsunuz ve yeni bir hesap oluşturup runbook’larınızı ve varlıklarınızı ona geçirmek yerine Klasik Farklı Çalıştır hesabını kullanacak şekilde güncelleştirmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="453fc-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="453fc-108">Kuruluş sertifika yetkiliniz (CA) tarafından verilen bir sertifika kullanarak bir Farklı Çalıştır ve Klasik Farklı Çalıştır hesabı oluşturmak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="453fc-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="453fc-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="453fc-109">Prerequisites</span></span>

* <span data-ttu-id="453fc-110">Betik yalnızca Azure Resource Manager 3.0.0 veya sonrasındaki modülleri içeren Windows 10 ve Windows Server 2016 işletim sistemlerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="453fc-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="453fc-111">Windows'un önceki sürümleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="453fc-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="453fc-112">Azure PowerShell 1.0 ve üzeri.</span><span class="sxs-lookup"><span data-stu-id="453fc-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="453fc-113">PowerShell 1.0 sürümü hakkında bilgi için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="453fc-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="453fc-114">Aşağıdaki PowerShell betiğinde *–AutomationAccountName* ve *-ApplicationDisplayName* parametrelerinin değeri olarak başvurulan bir Otomasyon hesabı.</span><span class="sxs-lookup"><span data-stu-id="453fc-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="453fc-115">Betik parametreleri için gerekli olan *SubscriptionID*, *ResourceGroup* ve *AutomationAccountName* değerlerini almak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="453fc-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the script, do the following:</span></span>

1. <span data-ttu-id="453fc-116">Azure portalında, **Otomasyon hesabı** dikey penceresinden Otomasyon hesabınızı ve ardından **Tüm ayarlar** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="453fc-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="453fc-117">**Tüm ayarlar** dikey penceresindeki **Hesap Ayarları** altında **Özellikler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="453fc-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="453fc-118">**Özellikler** dikey penceresindeki değerleri not alın.</span><span class="sxs-lookup"><span data-stu-id="453fc-118">Note the values on the **Properties** blade.</span></span><br><br> <span data-ttu-id="453fc-119">![Otomasyon hesabı "Özellikler" dikey penceresi](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="453fc-119">![The Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-to-update-your-automation-account"></a><span data-ttu-id="453fc-120">Otomasyon hesabınızı güncelleştirmek için gereken izinler</span><span class="sxs-lookup"><span data-stu-id="453fc-120">Required permissions to update your Automation account</span></span>
<span data-ttu-id="453fc-121">Otomasyon hesabını güncelleştirmek isterseniz bu konuyu tamamlamak için gereken aşağıdaki özel ayrıcalıklara ve izinlere sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="453fc-121">To update an Automation account, you must have the following specific privileges and permissions required to complete this topic.</span></span>   
 
* <span data-ttu-id="453fc-122">AD kullanıcı hesabınızın, [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md#contributor-role-permissions) makalesinde açıklandığı gibi Microsoft.Automation kaynaklarındaki Katkıda Bulunan rolüne eşdeğer izinlere sahip bir role eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="453fc-122">Your AD user account needs to be added to a role with permissions equivalent to the Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="453fc-123">Azure AD kiracınızdaki yönetici olmayan kullanıcılar, Uygulama kayıtları ayarı **Evet** olarak ayarlanırsa [AD uygulamalarını kaydedebilir](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="453fc-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if the App registrations setting is set to **Yes**.</span></span>  <span data-ttu-id="453fc-124">Uygulama kayıtları ayarı **Hayır** olarak ayarlanırsa bu işlemi gerçekleştiren kullanıcının, Azure AD’de genel yönetici olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="453fc-124">If the app registrations setting is set to **No**, the user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="453fc-125">Aboneliğin genel yönetici/ortak yönetici rolüne eklenmeden önce aboneliğin Active Directory örneğine üye değilseniz Active Directory’ye konuk olarak eklenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="453fc-125">If you are not a member of the subscription’s Active Directory instance before you are added to the global administrator/co-administrator role of the subscription, you are added to Active Directory as a guest.</span></span> <span data-ttu-id="453fc-126">Bu durumda, “Oluşturma izniniz yok…” iletisini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="453fc-126">In this situation, you receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="453fc-127">uyarısını **Otomasyon Hesabı Ekle** dikey penceresinde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="453fc-127">warning on the **Add Automation Account** blade.</span></span> <span data-ttu-id="453fc-128">İlk olarak genel yönetici/ortak yönetici rolüne eklenen kullanıcılar aboneliğin Active Directory örneğinden kaldırılabilir ve tekrar eklenerek Active Directory’de tam bir Kullanıcı haline getirilebilir.</span><span class="sxs-lookup"><span data-stu-id="453fc-128">Users who were added to the global administrator/co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="453fc-129">Bu durumu doğrulamak için Azure portalındaki **Azure Active Directory** bölmesinde **Kullanıcılar ve gruplar**’ı, **Tüm kullanıcılar**’ı seçin ve belirli bir kullanıcıyı seçtikten sonra **Profil**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="453fc-129">To verify this situation, from the **Azure Active Directory** pane in the Azure portal, select **Users and groups**, select **All users** and, after you select the specific user, select **Profile**.</span></span> <span data-ttu-id="453fc-130">Kullanıcı profili altındaki **Kullanıcı türü** özniteliğinin **Konuk** olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="453fc-130">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-the-portal"></a><span data-ttu-id="453fc-131">Portaldan Farklı Çalıştır hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="453fc-131">Create Run As account from the portal</span></span>
<span data-ttu-id="453fc-132">Bu bölümde, Azure portalından Azure Otomasyonu hesabınızı güncelleştirmek için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="453fc-132">In this section, perform the following steps to update your Azure Automation account from  the Azure portal.</span></span>  <span data-ttu-id="453fc-133">Farklı Çalıştır ve Klasik Farklı Çalıştır hesaplarını tek tek oluşturursunuz. Klasik Azure portalında kaynakları yönetmeniz gerekmiyorsa yalnızca Azure Farklı Çalıştır hesabını oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="453fc-133">You create the Run As and Classic Run As accounts individually, and if you don't need to manage resources in the classic Azure portal, you can just create the Azure Run As account.</span></span>  

<span data-ttu-id="453fc-134">İşlem, Otomasyon hesabınızda aşağıdaki öğeleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-134">The process creates the following items in your Automation account.</span></span>

<span data-ttu-id="453fc-135">**Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="453fc-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="453fc-136">Otomatik olarak imzalanan bir sertifika ile Azure AD uygulaması oluşturur, Azure AD’de bu uygulama için bir hizmet sorumlusu hesabı oluşturur ve geçerli aboneliğinizde hesap için Katkıda Bulunan rolünü atar.</span><span class="sxs-lookup"><span data-stu-id="453fc-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="453fc-137">Bu ayarı Sahip veya başka bir rolle değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="453fc-137">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="453fc-138">Daha fazla bilgi için bkz. [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="453fc-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="453fc-139">Belirtilen Otomasyon hesabında *AzureRunAsCertificate* adlı bir Otomasyon sertifikası varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="453fc-140">Sertifika varlıkları, Azure AD uygulaması tarafından kullanılan sertifika özel anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="453fc-140">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="453fc-141">Belirtilen Otomasyon hesabında *AzureRunAsConnection* adlı bir Otomasyon bağlantı varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-141">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="453fc-142">Bağlantı varlığı applicationId, tenantId, subscriptionId ve sertifika parmak izini içerir.</span><span class="sxs-lookup"><span data-stu-id="453fc-142">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="453fc-143">**Klasik Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="453fc-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="453fc-144">Belirtilen Otomasyon hesabında *AzureClassicRunAsCertificate* adlı bir Otomasyon sertifikası varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="453fc-145">Sertifika varlığı, yönetim sertifikası tarafından kullanılan sertifika özel anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="453fc-145">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="453fc-146">Belirtilen Otomasyon hesabında *AzureClassicRunAsConnection* adlı bir Otomasyon bağlantı varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="453fc-147">Bağlantı varlığı; abonelik adı, subscriptionId ve sertifika varlık adını içerir.</span><span class="sxs-lookup"><span data-stu-id="453fc-147">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="453fc-148">Azure portalında Abonelik Yöneticileri rolünün üyesi ve aboneliğin ortak yöneticisi olan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="453fc-148">Sign in to the Azure portal with an account that is a member of the Subscription Admins role and co-administrator of the subscription.</span></span>
2. <span data-ttu-id="453fc-149">Otomasyon hesabı dikey penceresinin **Hesap Ayarları** bölümünde **Farklı Çalıştır Hesapları**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="453fc-149">From the Automation account blade, select **Run As Accounts** under the section **Account Settings**.</span></span>  
3. <span data-ttu-id="453fc-150">Gereken hesaba bağlı olarak **Azure Farklı Çalıştır Hesabı**’nı veya **Azure Klasik Farklı Çalıştır Hesabı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="453fc-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="453fc-151">Seçim sonrasında **Azure Farklı Çalıştır Ekle** veya **Azure Klasik Farklı Çalıştır Hesabı Ekle** dikey penceresi görüntülenir ve genel bakış bilgilerini gözden geçirdikten sonra Farklı Çalıştır hesabı oluşturma işlemine devam etmek için **Oluştur**’a tıklamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="453fc-151">After selecting either the **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing the overview information, click **Create** to proceed with Run As account creation.</span></span>  
4. <span data-ttu-id="453fc-152">Farklı Çalıştır hesabı Azure tarafından oluşturulurken ilerleme durumunu menüdeki **Bildirimler** altında izleyebilirsiniz; hesabın oluşturulmakta olduğunu belirten bir başlık görünür.</span><span class="sxs-lookup"><span data-stu-id="453fc-152">While Azure creates the Run As account, you can track the progress under **Notifications** from the menu and a banner is displayed stating the account is being created.</span></span>  <span data-ttu-id="453fc-153">Bu işlemin tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="453fc-153">This process can take a few minutes to complete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="453fc-154">PowerShell betiği ile Farklı Çalıştır hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="453fc-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="453fc-155">Bu PowerShell betiği aşağıdaki yapılandırmalar için destek içerir:</span><span class="sxs-lookup"><span data-stu-id="453fc-155">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="453fc-156">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="453fc-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="453fc-157">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="453fc-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="453fc-158">Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="453fc-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="453fc-159">Azure Kamu bulutunda otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="453fc-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="453fc-160">Seçtiğiniz yapılandırma seçeneğine bağlı olarak, betik aşağıdaki öğeleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-160">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="453fc-161">**Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="453fc-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="453fc-162">Otomatik olarak imzalanan sertifika veya kurumsal sertifika ortak anahtarıyla dışarı aktarılacak bir Azure AD uygulaması oluşturur, Azure AD’de bu uygulama için bir hizmet sorumlusu hesabı oluşturur ve geçerli aboneliğinizde hesap için Katkıda Bulunan rolünü atar.</span><span class="sxs-lookup"><span data-stu-id="453fc-162">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="453fc-163">Bu ayarı Sahip veya başka bir rolle değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="453fc-163">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="453fc-164">Daha fazla bilgi için bkz. [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="453fc-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="453fc-165">Belirtilen Otomasyon hesabında *AzureRunAsCertificate* adlı bir Otomasyon sertifikası varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="453fc-166">Sertifika varlıkları, Azure AD uygulaması tarafından kullanılan sertifika özel anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="453fc-166">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="453fc-167">Belirtilen Otomasyon hesabında *AzureRunAsConnection* adlı bir Otomasyon bağlantı varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-167">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="453fc-168">Bağlantı varlığı applicationId, tenantId, subscriptionId ve sertifika parmak izini içerir.</span><span class="sxs-lookup"><span data-stu-id="453fc-168">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="453fc-169">**Klasik Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="453fc-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="453fc-170">Belirtilen Otomasyon hesabında *AzureClassicRunAsCertificate* adlı bir Otomasyon sertifikası varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="453fc-171">Sertifika varlığı, yönetim sertifikası tarafından kullanılan sertifika özel anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="453fc-171">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="453fc-172">Belirtilen Otomasyon hesabında *AzureClassicRunAsConnection* adlı bir Otomasyon bağlantı varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="453fc-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="453fc-173">Bağlantı varlığı; abonelik adı, subscriptionId ve sertifika varlık adını içerir.</span><span class="sxs-lookup"><span data-stu-id="453fc-173">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="453fc-174">Klasik Farklı Çalıştır hesabı oluşturma seçeneğini belirlerseniz, betik yürütüldükten sonra Otomasyon hesabının oluşturulduğu abonelik için yönetim deposuna ortak sertifikayı (.cer dosya adı uzantısı) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="453fc-174">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="453fc-175">Aşağıdaki betiği bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="453fc-175">Save the following script on your computer.</span></span> <span data-ttu-id="453fc-176">Bu örnekte *New-RunAsAccount.ps1* dosya adıyla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="453fc-176">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="453fc-177">Bilgisayarınızda **Windows PowerShell**’i yükseltilmiş kullanıcı haklarına sahip **Başlat** ekranından başlatın.</span><span class="sxs-lookup"><span data-stu-id="453fc-177">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="453fc-178">Yükseltilmiş komut satırı kabuğundan, 1. adımda oluşturduğunuz komut dosyasını içeren klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="453fc-178">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="453fc-179">İstediğiniz yapılandırmanın parametre değerlerini kullanarak betiği yürütün.</span><span class="sxs-lookup"><span data-stu-id="453fc-179">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="453fc-180">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="453fc-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="453fc-181">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="453fc-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="453fc-182">**Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="453fc-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="453fc-183">**Azure Kamu bulutunda otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="453fc-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="453fc-184">Betik yürütüldükten sonra Azure kimlik doğrulamasını yapmanız istenecektir.</span><span class="sxs-lookup"><span data-stu-id="453fc-184">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="453fc-185">Aboneliğin yöneticiler rolünün üyesi ve aboneliğin ortak yöneticisi olan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="453fc-185">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="453fc-186">Betik başarıyla yürütüldükten sonra aşağıdakilere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="453fc-186">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="453fc-187">Otomatik olarak imzalanan bir ortak sertifika (.cer dosyası) ile Klasik Farklı Çalıştır hesabı oluşturduysanız, betik bu hesabı oluşturup bilgisayarınızdaki geçici dosya klasörüne, PowerShell oturumunu yürütmek için kullandığınız *%USERPROFILE%\AppData\Local\Temp* kullanıcı profili altında kaydeder.</span><span class="sxs-lookup"><span data-stu-id="453fc-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="453fc-188">Kurumsal ortak sertifika (.cer file) ile bir Klasik Farklı Çalıştır hesabı oluşturduysanız bu sertifikayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="453fc-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="453fc-189">[Klasik Azure portalında yönetim API sertifikasını yükleme](../azure-api-management-certs.md) yönergelerini izleyin ve ardından [Azure Klasik Dağıtım Kaynakları ile kimlik doğrulamaya yönelik örnek kodunu](automation-verify-runas-authentication.md#classic-run-as-authentication) kullanarak klasik dağıtım kaynakları ile kimlik bilgisi yapılandırmasını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="453fc-189">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="453fc-190">Klasik Farklı Çalıştır hesabı *oluşturmadıysanız*, Resource Manager kaynakları kimlik doğrulaması yapmak ve kimlik bilgisi yapılandırmasını doğrulamak için [Service Management kaynakları ile kimlik doğrulamaya yönelik örnek kodu](automation-verify-runas-authentication.md#automation-run-as-authentication) kullanın.</span><span class="sxs-lookup"><span data-stu-id="453fc-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="453fc-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="453fc-191">Next steps</span></span>
* <span data-ttu-id="453fc-192">Hizmet Sorumluları hakkında daha fazla bilgi için bkz. [Uygulama Nesneleri ve Hizmet Sorumlusu Nesneleri](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="453fc-192">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="453fc-193">Sertifikalar ve Azure hizmetleri hakkında daha fazla bilgi için bkz. [Azure Cloud Services sertifikalarına genel bakış](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="453fc-193">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>