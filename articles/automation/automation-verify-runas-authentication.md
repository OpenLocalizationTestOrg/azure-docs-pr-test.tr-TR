---
title: "aaaValidate Azure Otomasyonu hesabı yapılandırması | Microsoft Docs"
description: "Bu makalede nasıl tooconfirm hello yapılandırma Otomasyon hesabınızın doğru şekilde kurulduğundan açıklanmaktadır."
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
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="93f82-103">Azure Otomasyonu Farklı Çalıştır hesabı kimlik doğrulamasını test etme</span><span class="sxs-lookup"><span data-stu-id="93f82-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="93f82-104">Bir Otomasyon hesabı başarıyla oluşturulduktan sonra mümkün basit bir sınama tooconfirm gerçekleştirebilirsiniz toosuccessfully kimlik doğrulaması Azure Kaynak Yöneticisi'nde veya yeni oluşturulmuş veya güncelleştirilmiş Automation farklı çalıştır hesabınızı kullanarak Azure Klasik dağıtım.</span><span class="sxs-lookup"><span data-stu-id="93f82-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="93f82-105">Otomasyon Farklı Çalıştır kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="93f82-105">Automation Run As authentication</span></span>
<span data-ttu-id="93f82-106">Aşağıdaki örnek kodu Hello çok kullanın[PowerShell runbook oluşturma](automation-creating-importing-runbook.md) hello kullanarak tooverify kimlik doğrulama hesabı olarak hem de özel runbook'lar tooauthenticate çalıştırın ve Otomasyon hesabınızda Resource Manager kaynaklarını yönetmek.</span><span class="sxs-lookup"><span data-stu-id="93f82-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
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

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

<span data-ttu-id="93f82-107">Kimlik doğrulaması için kullanılan cmdlet hello fark hello runbook'taki - **Add-AzureRmAccount**, kullandığı hello *ServicePrincipalCertificate* parametre kümesi.</span><span class="sxs-lookup"><span data-stu-id="93f82-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="93f82-108">Kimlik bilgilerini değil, hizmet asıl sertifikasını kullanarak kimlik doğrulamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="93f82-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="93f82-109">Olduğunda, [hello runbook'a](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate, farklı çalıştır hesabı bir [runbook işi](automation-runbook-execution.md) olan oluşturulan hello iş dikey penceresi görüntülenir ve hello iş durumu görüntülenen hello **iş özeti**döşeme.</span><span class="sxs-lookup"><span data-stu-id="93f82-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="93f82-110">Merhaba iş durumu olarak başlayacak *sıraya alınan* bir runbook worker'hello bulut toobecome için bekleyen belirten.</span><span class="sxs-lookup"><span data-stu-id="93f82-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="93f82-111">Ardından, çok taşınır*başlangıç* bir çalışan hello işi talep ettiğinde ve ardından *çalıştıran* hello runbook gerçekten çalışmaya başladığında.</span><span class="sxs-lookup"><span data-stu-id="93f82-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="93f82-112">Merhaba runbook işi tamamlandığında durumunu görmeliyiz **tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="93f82-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="93f82-113">toosee Merhaba hello runbook'un ayrıntılı sonuçlarını, üzerinde hello tıklatın **çıkış** döşeme.</span><span class="sxs-lookup"><span data-stu-id="93f82-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="93f82-114">Merhaba üzerinde **çıkış** dikey penceresinde görmeniz gerekir başarıyla doğrulaması ve tüm kaynak gruplarının, aboneliğinizdeki tüm kaynakların bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="93f82-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="93f82-115">Yalnızca tooremove hello hello açıklama ile başlayan kod bloğunu unutmayın `#Get all ARM resources from all resource groups` ne zaman yeniden hello kod runbook'lar için.</span><span class="sxs-lookup"><span data-stu-id="93f82-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="93f82-116">Klasik Farklı Çalıştır kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="93f82-116">Classic Run As authentication</span></span>
<span data-ttu-id="93f82-117">Aşağıdaki Hello örnek kodu çok kullanın[PowerShell runbook oluşturma](automation-creating-importing-runbook.md) tooverify kimlik doğrulaması kullanarak Klasik Merhaba hesabı olarak hem de özel runbook'lar tooauthenticate çalıştırın ve hello Klasik dağıtım modelinde kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="93f82-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

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
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="93f82-118">Olduğunda, [hello runbook'a](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate, farklı çalıştır hesabı bir [runbook işi](automation-runbook-execution.md) olan oluşturulan hello iş dikey penceresi görüntülenir ve hello iş durumu görüntülenen hello **iş özeti**döşeme.</span><span class="sxs-lookup"><span data-stu-id="93f82-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="93f82-119">Merhaba iş durumu olarak başlayacak *sıraya alınan* bir runbook worker'hello bulut toobecome için bekleyen belirten.</span><span class="sxs-lookup"><span data-stu-id="93f82-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="93f82-120">Ardından, çok taşınır*başlangıç* bir çalışan hello işi talep ettiğinde ve ardından *çalıştıran* hello runbook gerçekten çalışmaya başladığında.</span><span class="sxs-lookup"><span data-stu-id="93f82-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="93f82-121">Merhaba runbook işi tamamlandığında durumunu görmeliyiz **tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="93f82-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="93f82-122">toosee Merhaba hello runbook'un ayrıntılı sonuçlarını, üzerinde hello tıklatın **çıkış** döşeme.</span><span class="sxs-lookup"><span data-stu-id="93f82-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="93f82-123">Merhaba üzerinde **çıkış** dikey penceresinde görmeniz gerekir başarıyla doğrulaması ve aboneliğinizde dağıtılan VMName tarafından tüm Azure VM'ler listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="93f82-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="93f82-124">Yalnızca tooremove hello cmdlet unutmayın **Get-AzureVM** ne zaman yeniden hello kod runbook'lar için.</span><span class="sxs-lookup"><span data-stu-id="93f82-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93f82-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="93f82-125">Next steps</span></span>
* <span data-ttu-id="93f82-126">PowerShell runbook'ları ile çalışmaya tooget bkz [ilk PowerShell runbook'um](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="93f82-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="93f82-127">Grafik yazma hakkında daha fazla toolearn bkz [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="93f82-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
