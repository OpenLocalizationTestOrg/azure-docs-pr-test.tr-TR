---
title: "Azure Otomasyonu hesap yapılandırmasını doğrulama | Microsoft Docs"
description: "Bu makalede Otomasyon hesabınızın doğru şekilde ayarlandığını onaylama işlemi açıklanmaktadır."
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
ms.openlocfilehash: 804e05f596e1d6d5f650e4c94a18eff6b7c3ba4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="95340-103">Azure Otomasyonu Farklı Çalıştır hesabı kimlik doğrulamasını test etme</span><span class="sxs-lookup"><span data-stu-id="95340-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="95340-104">Bir Otomasyon hesabı başarıyla oluşturulduktan sonra, yeni oluşturduğunuz veya güncelleştirdiğiniz Azure Farklı Çalıştır hesabını kullanarak Azure Resource Manager veya Azure klasik dağıtımında kimlik doğrulamasını başarıyla yapabildiğinizi onaylamak üzere basit bir test gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95340-104">After an Automation account is successfully created, you can perform a simple test to confirm you are able to successfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="95340-105">Otomasyon Farklı Çalıştır kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="95340-105">Automation Run As authentication</span></span>
<span data-ttu-id="95340-106">Aşağıdaki örnek kodları Farklı Çalıştır hesabını kullanarak kimlik doğrulamayı denetlemek için bir [PowerShell runbook’u oluşturmak](automation-creating-importing-runbook.md) ve özel runbook’larınızda Otomasyon hesabınızda kimlik doğrulamak ve Resource Manager kaynaklarınızı yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95340-106">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Run As account and also in your custom runbooks to authenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get the connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in to Azure..."
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

<span data-ttu-id="95340-107">Runbook’ta kimlik doğrulaması için kullanılan cmdlet’in (**Add-AzureRmAccount**) *ServicePrincipalCertificate* parametre kümesini kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="95340-107">Notice the cmdlet used for authenticating in the runbook - **Add-AzureRmAccount**, uses the *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="95340-108">Kimlik bilgilerini değil, hizmet asıl sertifikasını kullanarak kimlik doğrulamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="95340-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="95340-109">Farklı Çalıştır hesabınızı doğrulamak için bir [runbook’u çalıştırdığınızda](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) bir [runbook işi](automation-runbook-execution.md) oluşturulur, İş dikey penceresi gösterilir ve iş durumu **İş Özeti** kutucuğunda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="95340-109">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="95340-110">İş durumu, bulutta bir runbook çalışanının kullanılabilir hale gelmesinin beklendiğini gösteren şekilde *Sırada* olarak başlar.</span><span class="sxs-lookup"><span data-stu-id="95340-110">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="95340-111">Ardından, bir çalışan işi talep ettiğinde *Başlatılıyor* olarak ve runbook gerçekten çalışmaya başladığında *Çalışıyor* olarak değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="95340-111">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="95340-112">Runbook işi tamamlandığında **Tamamlandı** durumunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="95340-112">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="95340-113">Runbook’un ayrıntılı sonuçlarını görmek için **Çıktı** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="95340-113">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="95340-114">**Çıktı** dikey penceresinde kimlik doğrulamasının başarıyla yapıldığını ve aboneliğinizde olan tüm kaynak gruplarındaki kaynakların bir listesinin döndürüldüğünü görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="95340-114">On the **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="95340-115">Runbook’larınız için kodları kullanırken `#Get all ARM resources from all resource groups` açıklaması ile başlayan kod bloğunu kaldırmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="95340-115">Just remember to remove the block of code starting with the comment `#Get all ARM resources from all resource groups` when you reuse the code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="95340-116">Klasik Farklı Çalıştır kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="95340-116">Classic Run As authentication</span></span>
<span data-ttu-id="95340-117">Aşağıdaki örnek kodları Klasik Farklı Çalıştır hesabını kullanarak kimlik doğrulamayı denetlemek için bir [PowerShell runbook’u oluşturmak](automation-creating-importing-runbook.md) ve özel runbook’larınızda kimlik doğrulamak ve klasik dağıtım modelinde kaynaklarınızı yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95340-117">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Classic Run As account and also in your custom runbooks to authenticate and manage resources in the classic deployment model.</span></span>  

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
    
    #Get all VMs in the subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="95340-118">Farklı Çalıştır hesabınızı doğrulamak için bir [runbook’u çalıştırdığınızda](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) bir [runbook işi](automation-runbook-execution.md) oluşturulur, İş dikey penceresi gösterilir ve iş durumu **İş Özeti** kutucuğunda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="95340-118">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="95340-119">İş durumu, bulutta bir runbook çalışanının kullanılabilir hale gelmesinin beklendiğini gösteren şekilde *Sırada* olarak başlar.</span><span class="sxs-lookup"><span data-stu-id="95340-119">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="95340-120">Ardından, bir çalışan işi talep ettiğinde *Başlatılıyor* olarak ve runbook gerçekten çalışmaya başladığında *Çalışıyor* olarak değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="95340-120">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="95340-121">Runbook işi tamamlandığında **Tamamlandı** durumunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="95340-121">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="95340-122">Runbook’un ayrıntılı sonuçlarını görmek için **Çıktı** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="95340-122">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="95340-123">**Çıktı** dikey penceresinde kimlik doğrulamasının başarıyla yapıldığını ve aboneliğinizde olan Azure VM’lerinin VMName’lerini içeren bir listesinin döndürüldüğünü görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="95340-123">On the **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="95340-124">Runbook’larınız için kodları kullanırken **Get-AzureVM** cmdlet’ini kaldırmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="95340-124">Just remember to remove the cmdlet **Get-AzureVM** when you reuse the code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95340-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95340-125">Next steps</span></span>
* <span data-ttu-id="95340-126">PowerShell runbook'ları kullanmaya başlamak için bkz. [İlk PowerShell runbook’um](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="95340-126">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="95340-127">Grafik Yazma hakkında daha fazla bilgi için bkz. [Azure Otomasyonu’nda grafik yazma](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="95340-127">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
