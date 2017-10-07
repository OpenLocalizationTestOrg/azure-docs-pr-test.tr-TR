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
# <a name="certificate-assets-in-azure-automation"></a>Azure Otomasyonu sertifika varlıkları

Sertifikaları depolanabilir güvenli bir şekilde Azure Otomasyonu'nda runbook'lar veya hello kullanarak DSC yapılandırması tarafından erişilebilmeleri adına **Get-AzureRmAutomationRmCertificate** etkinlik Azure Resource Manager kaynakları için. Bu toocreate runbook'ları ve kimlik doğrulaması için sertifikalar kullanmak DSC yapılandırmaları izin verir veya tooAzure veya üçüncü taraf kaynakları ekler.

> [!NOTE] 
> Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir. Bu varlıklar şifrelenir ve hello Azure her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak otomasyon depolanır. Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır. Güvenli bir varlık depolamak önce hello Otomasyon hesabının hello anahtarı hello ana sertifikayı kullanarak şifresi çözülür ve tooencrypt hello varlık kullanılır.
> 

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet'leri

Aşağıdaki tablonun hello Hello cmdlet'leri kullanılan toocreate olan ve Otomasyon sertifika varlıklarını Windows PowerShell ile yönetme. Merhaba bir parçası olarak sevk [Azure PowerShell Modülü](../powershell-install-configure.md) olduğu Automation runbook'ları ve DSC yapılandırmaları için kullanılabilir.

|Cmdlet'leri|Açıklama|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Bir sertifika toouse bir runbook ya da DSC yapılandırma hakkında bilgi alır. Bu gibi durumlarda, hello sertifikanın kendisi yalnızca Get-AutomationCertificate etkinliğinden alabilirsiniz.|
|[AzureRmAutomationCertificate yeni](https://msdn.microsoft.com/library/mt603604.aspx)|Yeni bir sertifika Azure Automation'a oluşturur.|
[Remove-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Bir sertifika Azure Otomasyon kaldırır.|Yeni bir sertifika Azure Automation'a oluşturur.
|[Set-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|Merhaba sertifika dosyası ve bir .pfx için hello parola ayarlama karşıya yüklenmesini de dahil olmak üzere var olan bir sertifikayı Hello özelliklerini ayarlar.|
|[Ekleme AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Bir hizmet sertifikası Merhaba yüklemeleri bulut hizmeti belirtilen.|


## <a name="creating-a-new-certificate"></a>Yeni bir sertifika oluşturma

Yeni bir sertifika oluşturduğunuzda, bir .cer veya .pfx dosyası tooAzure Otomasyon karşıya yükleyin. Ardından, hello sertifikası dışarı aktarılabilir olarak işaretlerseniz, hello Azure Otomasyonu sertifika deposunu dışında aktarabilirsiniz. Dışarı aktarılabilir değilse, ardından bu yalnızca hello runbook veya DSC yapılandırması içinde imzalamak için kullanılabilir.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate hello Azure portalı ile yeni bir sertifika

1. Otomasyon hesabınızdan hello tıklatın **varlıklar** döşeme tooopen hello **varlıklar** dikey.
1. Merhaba tıklatın **sertifikaları** döşeme tooopen hello **sertifikaları** dikey.
1. Tıklatın **bir sertifika eklemek** hello dikey penceresinde hello üstünde.
2. Hello hello sertifika için bir ad yazın **adı** kutusu.
2. Tıklatın **bir dosya seçin** altında **bir sertifika dosyası karşıya** toobrowse bir .cer veya .pfx dosyası için.  Bir .pfx dosyası seçerseniz, bir parola ve olup, dışa aktarılan toobe izin verilmesi gerektiğini belirtin.
1. Tıklatın **oluşturma** toosave hello yeni sertifika varlığı.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>Windows PowerShell ile yeni bir sertifika toocreate

Merhaba aşağıdaki örnekte gösterilmiştir nasıl toocreate yeni bir Otomasyon sertifikası ve dışarı aktarılabilir olarak işaretleyin. Bu, var olan bir .pfx dosyasını içeri aktarır.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Bir sertifika kullanma

Merhaba kullanmalısınız **Get-AutomationCertificate** etkinlik toouse bir sertifika. Merhaba kullanamazsınız [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) hello sertifika varlığı ancak hello sertifikanın kendisi değil hakkında bilgi döndürdüğünden cmdlet'i.

### <a name="textual-runbook-sample"></a>Metin biçiminde runbook örneği

Aşağıdaki örnek kod hello nasıl tooadd sertifika tooa bulut hizmeti bir runbook'ta gösterir. Bu örnekte, bir şifrelenmiş Otomasyon değişkeninden hello parola alınır.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Grafik runbook örneği

Eklediğiniz bir **Get-AutomationCertificate** sağ tıklayarak hello sertifika hello grafik Düzenleyicisi ve seçerek hello Kitaplık bölmesinde grafik runbook tooa **toocanvas eklemek**.

![Sertifika toohello tuvale Ekle](media/automation-certificates/automation-certificate-add-to-canvas.png)

Merhaba aşağıdaki resimde bir grafik runbook'ta bir sertifika kullanarak bir örnek gösterilmektedir.  Merhaba budur metinsel bir runbook'tan bir sertifika tooa bulut hizmeti eklemek için yukarıda gösterilen aynı örneği.

![Örnek grafik yazma ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>Sonraki adımlar

- runbook'unuzda bağlantıları toocontrol hello mantıksal akışı etkinlikleri ile çalışma hakkında daha fazla olan toolearn tasarlanmış tooperform bkz [grafik yazma içinde bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow). 
