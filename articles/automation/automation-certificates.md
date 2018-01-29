---
title: "Sertifika Azure automation'da varlıklar | Microsoft Docs"
description: "Runbook'ları veya Azure ve üçüncü taraf kaynaklarına karşı kimlik doğrulaması için DSC yapılandırması tarafından erişilebilecek şekilde sertifikaları güvenli bir şekilde Azure Otomasyonu'nda depolanabilir.  Bu makalede, sertifikalar ve bunlarla metinsel ve grafik yazma çalışma ayrıntılarını açıklanmaktadır."
services: automation
documentationcenter: 
author: georgewallace
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: b6a5ff4fa3fd0084fd910968651c6ae0fefaf2cf
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Azure Otomasyonu sertifika varlıkları

Sertifikaları depolanabilir güvenli bir şekilde Azure Otomasyonu'nda runbook'lar veya kullanarak DSC yapılandırması tarafından erişilebilmeleri adına **Get-AzureRmAutomationCertificate** etkinlik Azure Resource Manager kaynakları için. Bu runbook'ları ve kimlik doğrulaması için sertifikalar kullanmak DSC yapılandırmaları oluşturmanıza olanak tanıyan veya Azure veya üçüncü taraf kaynakları ekler.

> [!NOTE] 
> Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir. Bu varlıklar şifrelenir ve her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak Azure Automation depolanır. Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır. Güvenli bir varlık depolamak önce anahtar Otomasyon hesabı için sertifika aracılığıyla çözülür ve varlık şifrelemek için kullanılan.
> 

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet'leri

Aşağıdaki tabloda yer alan cmdlet'ler oluşturmak ve Windows PowerShell ile automation sertifika varlıkları yönetmek için kullanılır. Bir parçası olarak sevk [Azure PowerShell Modülü](../powershell-install-configure.md) olduğu Automation runbook'ları ve DSC yapılandırmaları için kullanılabilir.

|Cmdlet'leri|Açıklama|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://docs.microsoft.com/powershell/module/azurerm.automation/get-azurermautomationcertificate?view=azurermps-4.3.1)|Bir runbook veya DSC yapılandırması kullanmak için bir sertifikayla ilgili bilgileri alır. Bu gibi durumlarda, sertifika yalnızca Get-AutomationCertificate etkinliğinden alabilirsiniz.|
|[AzureRmAutomationCertificate yeni](https://docs.microsoft.com/powershell/module/azurerm.automation/new-azurermautomationcertificate?view=azurermps-4.3.1)|Yeni bir sertifika Azure Automation'a oluşturur.|
[Remove-AzureRmAutomationCertificate](https://docs.microsoft.com/powershell/module/azurerm.automation/remove-azurermautomationcertificate?view=azurermps-4.3.1)|Bir sertifika Azure Otomasyon kaldırır.|Yeni bir sertifika Azure Automation'a oluşturur.
|[Set-AzureRmAutomationCertificate](https://docs.microsoft.com/powershell/module/azurerm.automation/set-azurermautomationcertificate?view=azurermps-4.3.1)|Sertifika dosyası karşıya yükleme ve bir .pfx için parolayı ayarlama da dahil olmak üzere var olan bir sertifikayı özelliklerini ayarlar.|
|[Ekleme AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Belirtilen bulut hizmeti için hizmet sertifikası yükler.|


## <a name="python2-functions"></a>Python2 işlevleri

Aşağıdaki tabloda işlevinde Python2 runbook sertifikalarda erişmek için kullanılır.

| İşlev | Açıklama |
|:---|:---|
| automationassets.get_automation_certificate | Bir sertifika varlığı ilgili bilgileri alır. |

> [!NOTE]
> İçeri aktarmanız gerekir **automationassets** varlık işlevleri erişmek için Python runbook'unuz başlangıcını modülünde.


## <a name="creating-a-new-certificate"></a>Yeni bir sertifika oluşturma

Yeni bir sertifika oluşturduğunuzda, Azure Automation .cer veya .pfx dosyasını karşıya yükleyin. Ardından sertifikası dışarı aktarılabilir olarak işaretlerseniz, bunu Azure Otomasyonu sertifika deposunu dışında aktarabilirsiniz. Dışarı aktarılabilir değilse, ardından bu yalnızca runbook veya DSC yapılandırması içinde imzalamak için kullanılabilir.


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a>Azure portalı ile yeni bir sertifika oluşturmak için

1. Otomasyon hesabınızdan tıklatın **varlıklar** açmak için kutucuğa **varlıklar** dikey.
1. Tıklatın **sertifikaları** açmak için kutucuğa **sertifikaları** dikey.
1. Tıklatın **bir sertifika eklemek** dikey pencerenin üstündeki.
2. Sertifika için bir ad yazın **adı** kutusu.
2. Tıklatın **bir dosya seçin** altında **bir sertifika dosyası karşıya** bir .cer veya .pfx dosyasını bulmak için.  Bir .pfx dosyası seçerseniz, bir parola ve olup, dışarı aktarılmasına izin verilmesi gerektiğini belirtin.
1. Tıklatın **oluşturma** yeni sertifika varlığı kaydetmek için.


### <a name="to-create-a-new-certificate-with-windows-powershell"></a>Windows PowerShell ile yeni bir sertifika oluşturmak için

Aşağıdaki örnek, yeni bir Otomasyon sertifikası oluşturun ve dışarı aktarılabilir olarak işaretleyin gösterilmiştir. Bu, var olan bir .pfx dosyasını içeri aktarır.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Bir sertifika kullanma

Kullanmalısınız **Get-AutomationCertificate** etkinliğini bir sertifika kullanın. Kullanamazsınız [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) sertifika varlığı ama sertifikanın kendisi hakkında bilgi döndürdüğünden cmdlet'i.

### <a name="textual-runbook-sample"></a>Metin biçiminde runbook örneği

Aşağıdaki örnek kod, bir runbook'ta bir bulut hizmeti için bir sertifika eklemek gösterilmiştir. Bu örnekte, parolayı bir şifrelenmiş Otomasyon değişkeninden alınır.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Grafik runbook örneği

Eklediğiniz bir **Get-AutomationCertificate** sağ tıklayarak grafik düzenleyicisini Kitaplık bölmesinde sertifika ve seçerek bir grafik runbook **tuvale Ekle**.

![Sertifika tuvale Ekle](media/automation-certificates/automation-certificate-add-to-canvas.png)

Aşağıdaki resimde bir grafik runbook'ta bir sertifika kullanarak bir örnek gösterilmektedir.  Bu, bir metinsel runbook'tan bir bulut hizmeti için bir sertifika eklemek için yukarıda gösterilen aynı örnektir.

![Örnek grafik yazma ](media/automation-certificates/graphical-runbook-add-certificate.png)

### <a name="python2-sample"></a>Python2 örnek
Aşağıdaki örnek, sertifikaları Python2 runbook'lardaki erişim gösterilmektedir.

    # get a reference to the Azure Automation certificate
    cert = automationassets.get_automation_certificate("AzureRunAsCertificate")
    
    # returns the binary cert content  
    print cert 

## <a name="next-steps"></a>Sonraki adımlar

- Runbook'unuzda gerçekleştirmek üzere tasarlanmıştır etkinliklerin mantıksal akışını denetlemek için bağlantılar ile çalışma hakkında daha fazla bilgi için bkz: [grafik yazma içinde bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow). 
