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
# <a name="test-azure-automation-run-as-account-authentication"></a>Azure Otomasyonu Farklı Çalıştır hesabı kimlik doğrulamasını test etme
Bir Otomasyon hesabı başarıyla oluşturulduktan sonra mümkün basit bir sınama tooconfirm gerçekleştirebilirsiniz toosuccessfully kimlik doğrulaması Azure Kaynak Yöneticisi'nde veya yeni oluşturulmuş veya güncelleştirilmiş Automation farklı çalıştır hesabınızı kullanarak Azure Klasik dağıtım.    

## <a name="automation-run-as-authentication"></a>Otomasyon Farklı Çalıştır kimlik doğrulaması
Aşağıdaki örnek kodu Hello çok kullanın[PowerShell runbook oluşturma](automation-creating-importing-runbook.md) hello kullanarak tooverify kimlik doğrulama hesabı olarak hem de özel runbook'lar tooauthenticate çalıştırın ve Otomasyon hesabınızda Resource Manager kaynaklarını yönetmek.   

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

Kimlik doğrulaması için kullanılan cmdlet hello fark hello runbook'taki - **Add-AzureRmAccount**, kullandığı hello *ServicePrincipalCertificate* parametre kümesi.  Kimlik bilgilerini değil, hizmet asıl sertifikasını kullanarak kimlik doğrulamasını yapar.  

Olduğunda, [hello runbook'a](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate, farklı çalıştır hesabı bir [runbook işi](automation-runbook-execution.md) olan oluşturulan hello iş dikey penceresi görüntülenir ve hello iş durumu görüntülenen hello **iş özeti**döşeme. Merhaba iş durumu olarak başlayacak *sıraya alınan* bir runbook worker'hello bulut toobecome için bekleyen belirten. Ardından, çok taşınır*başlangıç* bir çalışan hello işi talep ettiğinde ve ardından *çalıştıran* hello runbook gerçekten çalışmaya başladığında.  Merhaba runbook işi tamamlandığında durumunu görmeliyiz **tamamlandı**.

toosee Merhaba hello runbook'un ayrıntılı sonuçlarını, üzerinde hello tıklatın **çıkış** döşeme.  Merhaba üzerinde **çıkış** dikey penceresinde görmeniz gerekir başarıyla doğrulaması ve tüm kaynak gruplarının, aboneliğinizdeki tüm kaynakların bir listesini döndürür.  

Yalnızca tooremove hello hello açıklama ile başlayan kod bloğunu unutmayın `#Get all ARM resources from all resource groups` ne zaman yeniden hello kod runbook'lar için.

## <a name="classic-run-as-authentication"></a>Klasik Farklı Çalıştır kimlik doğrulaması
Aşağıdaki Hello örnek kodu çok kullanın[PowerShell runbook oluşturma](automation-creating-importing-runbook.md) tooverify kimlik doğrulaması kullanarak Klasik Merhaba hesabı olarak hem de özel runbook'lar tooauthenticate çalıştırın ve hello Klasik dağıtım modelinde kaynaklarını yönetme.  

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

Olduğunda, [hello runbook'a](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate, farklı çalıştır hesabı bir [runbook işi](automation-runbook-execution.md) olan oluşturulan hello iş dikey penceresi görüntülenir ve hello iş durumu görüntülenen hello **iş özeti**döşeme. Merhaba iş durumu olarak başlayacak *sıraya alınan* bir runbook worker'hello bulut toobecome için bekleyen belirten. Ardından, çok taşınır*başlangıç* bir çalışan hello işi talep ettiğinde ve ardından *çalıştıran* hello runbook gerçekten çalışmaya başladığında.  Merhaba runbook işi tamamlandığında durumunu görmeliyiz **tamamlandı**.

toosee Merhaba hello runbook'un ayrıntılı sonuçlarını, üzerinde hello tıklatın **çıkış** döşeme.  Merhaba üzerinde **çıkış** dikey penceresinde görmeniz gerekir başarıyla doğrulaması ve aboneliğinizde dağıtılan VMName tarafından tüm Azure VM'ler listesini döndürür.  

Yalnızca tooremove hello cmdlet unutmayın **Get-AzureVM** ne zaman yeniden hello kod runbook'lar için.

## <a name="next-steps"></a>Sonraki adımlar
* PowerShell runbook'ları ile çalışmaya tooget bkz [ilk PowerShell runbook'um](automation-first-runbook-textual-powershell.md).
* Grafik yazma hakkında daha fazla toolearn bkz [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md).
