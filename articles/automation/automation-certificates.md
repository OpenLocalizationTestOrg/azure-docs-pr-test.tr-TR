---
title: "Sertifika Azure automation'da varlıklar | Microsoft Docs"
description: "Runbook'ları veya Azure ve üçüncü taraf kaynaklarına karşı kimlik doğrulaması için DSC yapılandırması tarafından erişilebilecek şekilde sertifikaları güvenli bir şekilde Azure Otomasyonu'nda depolanabilir.  Bu makalede, sertifikalar ve bunlarla metinsel ve grafik yazma çalışma ayrıntılarını açıklanmaktadır."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: fd1737a420c132dace9307436bfea98a9bde94a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="d2465-104">Azure Otomasyonu sertifika varlıkları</span><span class="sxs-lookup"><span data-stu-id="d2465-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="d2465-105">Sertifikaları depolanabilir güvenli bir şekilde Azure Otomasyonu'nda runbook'lar veya kullanarak DSC yapılandırması tarafından erişilebilmeleri adına **Get-AzureRmAutomationRmCertificate** etkinlik Azure Resource Manager kaynakları için.</span><span class="sxs-lookup"><span data-stu-id="d2465-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="d2465-106">Bu runbook'ları ve kimlik doğrulaması için sertifikalar kullanmak DSC yapılandırmaları oluşturmanıza olanak tanıyan veya Azure veya üçüncü taraf kaynaklarına ekler.</span><span class="sxs-lookup"><span data-stu-id="d2465-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="d2465-107">Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir.</span><span class="sxs-lookup"><span data-stu-id="d2465-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="d2465-108">Bu varlıklar şifrelenir ve her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak Azure Automation depolanır.</span><span class="sxs-lookup"><span data-stu-id="d2465-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="d2465-109">Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır.</span><span class="sxs-lookup"><span data-stu-id="d2465-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="d2465-110">Güvenli bir varlık depolamak önce anahtar Otomasyon hesabı için sertifika aracılığıyla çözülür ve varlık şifrelemek için kullanılan.</span><span class="sxs-lookup"><span data-stu-id="d2465-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="d2465-111">Windows PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="d2465-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="d2465-112">Aşağıdaki tabloda yer alan cmdlet'ler oluşturmak ve Windows PowerShell ile automation sertifika varlıkları yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d2465-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="d2465-113">Bir parçası olarak sevk [Azure PowerShell Modülü](../powershell-install-configure.md) olduğu Automation runbook'ları ve DSC yapılandırmaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d2465-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="d2465-114">Cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="d2465-114">Cmdlets</span></span>|<span data-ttu-id="d2465-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d2465-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="d2465-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="d2465-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="d2465-117">Bir runbook veya DSC yapılandırması kullanmak için bir sertifikayla ilgili bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="d2465-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="d2465-118">Bu gibi durumlarda, sertifika yalnızca Get-AutomationCertificate etkinliğinden alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2465-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="d2465-119">AzureRmAutomationCertificate yeni</span><span class="sxs-lookup"><span data-stu-id="d2465-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="d2465-120">Yeni bir sertifika Azure Automation'a oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d2465-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="d2465-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="d2465-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="d2465-122">Bir sertifika Azure Otomasyon kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d2465-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="d2465-123">Yeni bir sertifika Azure Automation'a oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d2465-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="d2465-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="d2465-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="d2465-125">Sertifika dosyası karşıya yükleme ve bir .pfx için parolayı ayarlama da dahil olmak üzere var olan bir sertifikayı özelliklerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d2465-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="d2465-126">Ekleme AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="d2465-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="d2465-127">Belirtilen bulut hizmeti için hizmet sertifikası yükler.</span><span class="sxs-lookup"><span data-stu-id="d2465-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="d2465-128">Yeni bir sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2465-128">Creating a new certificate</span></span>

<span data-ttu-id="d2465-129">Yeni bir sertifika oluşturduğunuzda, Azure Automation .cer veya .pfx dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d2465-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="d2465-130">Ardından sertifikası dışarı aktarılabilir olarak işaretlerseniz, bunu Azure Otomasyonu sertifika deposunu dışında aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2465-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="d2465-131">Dışarı aktarılabilir değilse, ardından bu yalnızca runbook veya DSC yapılandırması içinde imzalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d2465-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="d2465-132">Azure portalı ile yeni bir sertifika oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="d2465-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="d2465-133">Otomasyon hesabınızdan tıklatın **varlıklar** açmak için kutucuğa **varlıklar** dikey.</span><span class="sxs-lookup"><span data-stu-id="d2465-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="d2465-134">Tıklatın **sertifikaları** açmak için kutucuğa **sertifikaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d2465-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="d2465-135">Tıklatın **bir sertifika eklemek** dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="d2465-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="d2465-136">Sertifika için bir ad yazın **adı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="d2465-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="d2465-137">Tıklatın **bir dosya seçin** altında **bir sertifika dosyası karşıya** bir .cer veya .pfx dosyasını bulmak için.</span><span class="sxs-lookup"><span data-stu-id="d2465-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="d2465-138">Bir .pfx dosyası seçerseniz, bir parola ve olup, dışarı aktarılmasına izin verilmesi gerektiğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d2465-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="d2465-139">Tıklatın **oluşturma** yeni sertifika varlığı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="d2465-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="d2465-140">Windows PowerShell ile yeni bir sertifika oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="d2465-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="d2465-141">Aşağıdaki örnek, yeni bir Otomasyon sertifikası oluşturun ve dışarı aktarılabilir olarak işaretleyin gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d2465-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="d2465-142">Bu, var olan bir .pfx dosyasını içeri aktarır.</span><span class="sxs-lookup"><span data-stu-id="d2465-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="d2465-143">Bir sertifika kullanma</span><span class="sxs-lookup"><span data-stu-id="d2465-143">Using a certificate</span></span>

<span data-ttu-id="d2465-144">Kullanmalısınız **Get-AutomationCertificate** etkinliğini bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2465-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="d2465-145">Kullanamazsınız [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) sertifika varlığı ama sertifikanın kendisi hakkında bilgi döndürdüğünden cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="d2465-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="d2465-146">Metin biçiminde runbook örneği</span><span class="sxs-lookup"><span data-stu-id="d2465-146">Textual runbook sample</span></span>

<span data-ttu-id="d2465-147">Aşağıdaki örnek kod, bir runbook'ta bir bulut hizmeti için bir sertifika eklemek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d2465-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="d2465-148">Bu örnekte, parolayı bir şifrelenmiş Otomasyon değişkeninden alınır.</span><span class="sxs-lookup"><span data-stu-id="d2465-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="d2465-149">Grafik runbook örneği</span><span class="sxs-lookup"><span data-stu-id="d2465-149">Graphical runbook sample</span></span>

<span data-ttu-id="d2465-150">Eklediğiniz bir **Get-AutomationCertificate** sağ tıklayarak grafik düzenleyicisini Kitaplık bölmesinde sertifika ve seçerek bir grafik runbook **tuvale Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d2465-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![Sertifika tuvale Ekle](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="d2465-152">Aşağıdaki resimde bir grafik runbook'ta bir sertifika kullanarak bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d2465-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="d2465-153">Bu, bir metinsel runbook'tan bir bulut hizmeti için bir sertifika eklemek için yukarıda gösterilen aynı örnektir.</span><span class="sxs-lookup"><span data-stu-id="d2465-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="d2465-154">Örnek grafik yazma</span><span class="sxs-lookup"><span data-stu-id="d2465-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="d2465-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d2465-155">Next steps</span></span>

- <span data-ttu-id="d2465-156">Runbook'unuzda gerçekleştirmek üzere tasarlanmıştır etkinliklerin mantıksal akışını denetlemek için bağlantılar ile çalışma hakkında daha fazla bilgi için bkz: [grafik yazma içinde bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="d2465-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
