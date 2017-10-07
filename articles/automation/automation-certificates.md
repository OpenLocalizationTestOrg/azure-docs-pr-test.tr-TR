---
title: "Azure Otomasyonu aaaCertificate varlıkları | Microsoft Docs"
description: "Runbook'ları veya DSC yapılandırmaları tooauthenticate Azure ve üçüncü taraf kaynakları karşı tarafından erişilebilecek şekilde sertifikaları güvenli bir şekilde Azure Otomasyonu'nda depolanabilir.  Bu makale, sertifikaları hello ayrıntılarını açıklar ve nasıl metinsel ve grafik yazma içinde toowork onlarla."
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
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="4a8b9-104">Azure Otomasyonu sertifika varlıkları</span><span class="sxs-lookup"><span data-stu-id="4a8b9-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="4a8b9-105">Sertifikaları depolanabilir güvenli bir şekilde Azure Otomasyonu'nda runbook'lar veya hello kullanarak DSC yapılandırması tarafından erişilebilmeleri adına **Get-AzureRmAutomationRmCertificate** etkinlik Azure Resource Manager kaynakları için.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="4a8b9-106">Bu toocreate runbook'ları ve kimlik doğrulaması için sertifikalar kullanmak DSC yapılandırmaları izin verir veya tooAzure veya üçüncü taraf kaynakları ekler.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="4a8b9-107">Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="4a8b9-108">Bu varlıklar şifrelenir ve hello Azure her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak otomasyon depolanır.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="4a8b9-109">Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="4a8b9-110">Güvenli bir varlık depolamak önce hello Otomasyon hesabının hello anahtarı hello ana sertifikayı kullanarak şifresi çözülür ve tooencrypt hello varlık kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="4a8b9-111">Windows PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="4a8b9-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="4a8b9-112">Aşağıdaki tablonun hello Hello cmdlet'leri kullanılan toocreate olan ve Otomasyon sertifika varlıklarını Windows PowerShell ile yönetme.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="4a8b9-113">Merhaba bir parçası olarak sevk [Azure PowerShell Modülü](../powershell-install-configure.md) olduğu Automation runbook'ları ve DSC yapılandırmaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="4a8b9-114">Cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="4a8b9-114">Cmdlets</span></span>|<span data-ttu-id="4a8b9-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4a8b9-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="4a8b9-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="4a8b9-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="4a8b9-117">Bir sertifika toouse bir runbook ya da DSC yapılandırma hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="4a8b9-118">Bu gibi durumlarda, hello sertifikanın kendisi yalnızca Get-AutomationCertificate etkinliğinden alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="4a8b9-119">AzureRmAutomationCertificate yeni</span><span class="sxs-lookup"><span data-stu-id="4a8b9-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="4a8b9-120">Yeni bir sertifika Azure Automation'a oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="4a8b9-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="4a8b9-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="4a8b9-122">Bir sertifika Azure Otomasyon kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="4a8b9-123">Yeni bir sertifika Azure Automation'a oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="4a8b9-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="4a8b9-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="4a8b9-125">Merhaba sertifika dosyası ve bir .pfx için hello parola ayarlama karşıya yüklenmesini de dahil olmak üzere var olan bir sertifikayı Hello özelliklerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="4a8b9-126">Ekleme AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="4a8b9-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="4a8b9-127">Bir hizmet sertifikası Merhaba yüklemeleri bulut hizmeti belirtilen.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="4a8b9-128">Yeni bir sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a8b9-128">Creating a new certificate</span></span>

<span data-ttu-id="4a8b9-129">Yeni bir sertifika oluşturduğunuzda, bir .cer veya .pfx dosyası tooAzure Otomasyon karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="4a8b9-130">Ardından, hello sertifikası dışarı aktarılabilir olarak işaretlerseniz, hello Azure Otomasyonu sertifika deposunu dışında aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="4a8b9-131">Dışarı aktarılabilir değilse, ardından bu yalnızca hello runbook veya DSC yapılandırması içinde imzalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="4a8b9-132">toocreate hello Azure portalı ile yeni bir sertifika</span><span class="sxs-lookup"><span data-stu-id="4a8b9-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="4a8b9-133">Otomasyon hesabınızdan hello tıklatın **varlıklar** döşeme tooopen hello **varlıklar** dikey.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="4a8b9-134">Merhaba tıklatın **sertifikaları** döşeme tooopen hello **sertifikaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="4a8b9-135">Tıklatın **bir sertifika eklemek** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="4a8b9-136">Hello hello sertifika için bir ad yazın **adı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="4a8b9-137">Tıklatın **bir dosya seçin** altında **bir sertifika dosyası karşıya** toobrowse bir .cer veya .pfx dosyası için.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="4a8b9-138">Bir .pfx dosyası seçerseniz, bir parola ve olup, dışa aktarılan toobe izin verilmesi gerektiğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="4a8b9-139">Tıklatın **oluşturma** toosave hello yeni sertifika varlığı.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="4a8b9-140">Windows PowerShell ile yeni bir sertifika toocreate</span><span class="sxs-lookup"><span data-stu-id="4a8b9-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="4a8b9-141">Merhaba aşağıdaki örnekte gösterilmiştir nasıl toocreate yeni bir Otomasyon sertifikası ve dışarı aktarılabilir olarak işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="4a8b9-142">Bu, var olan bir .pfx dosyasını içeri aktarır.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="4a8b9-143">Bir sertifika kullanma</span><span class="sxs-lookup"><span data-stu-id="4a8b9-143">Using a certificate</span></span>

<span data-ttu-id="4a8b9-144">Merhaba kullanmalısınız **Get-AutomationCertificate** etkinlik toouse bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="4a8b9-145">Merhaba kullanamazsınız [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) hello sertifika varlığı ancak hello sertifikanın kendisi değil hakkında bilgi döndürdüğünden cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="4a8b9-146">Metin biçiminde runbook örneği</span><span class="sxs-lookup"><span data-stu-id="4a8b9-146">Textual runbook sample</span></span>

<span data-ttu-id="4a8b9-147">Aşağıdaki örnek kod hello nasıl tooadd sertifika tooa bulut hizmeti bir runbook'ta gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="4a8b9-148">Bu örnekte, bir şifrelenmiş Otomasyon değişkeninden hello parola alınır.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="4a8b9-149">Grafik runbook örneği</span><span class="sxs-lookup"><span data-stu-id="4a8b9-149">Graphical runbook sample</span></span>

<span data-ttu-id="4a8b9-150">Eklediğiniz bir **Get-AutomationCertificate** sağ tıklayarak hello sertifika hello grafik Düzenleyicisi ve seçerek hello Kitaplık bölmesinde grafik runbook tooa **toocanvas eklemek**.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![Sertifika toohello tuvale Ekle](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="4a8b9-152">Merhaba aşağıdaki resimde bir grafik runbook'ta bir sertifika kullanarak bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="4a8b9-153">Merhaba budur metinsel bir runbook'tan bir sertifika tooa bulut hizmeti eklemek için yukarıda gösterilen aynı örneği.</span><span class="sxs-lookup"><span data-stu-id="4a8b9-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="4a8b9-154">Örnek grafik yazma</span><span class="sxs-lookup"><span data-stu-id="4a8b9-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="4a8b9-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a8b9-155">Next steps</span></span>

- <span data-ttu-id="4a8b9-156">runbook'unuzda bağlantıları toocontrol hello mantıksal akışı etkinlikleri ile çalışma hakkında daha fazla olan toolearn tasarlanmış tooperform bkz [grafik yazma içinde bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="4a8b9-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
