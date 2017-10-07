---
title: "Azure Otomasyon karma Runbook çalışanı aaaRun runbook'larda | Microsoft Docs"
description: "Bu makalede, yerel veri merkezinde veya Bulut sağlayıcısı hello karma Runbook çalışanı rolü ile makinelerde çalışan runbook'ları hakkında bilgi sağlar."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Bir karma Runbook çalışanı üzerinde çalışan runbook'ları 
Azure Automation ve karma Runbook çalışanı üzerinde çalışacak çalışan runbook'ların hello yapısındaki arasında fark yoktur. Her ile kullandığınız runbook'ları kaynakları hello yerel bilgisayarda kendisini veya dağıtıldığı, runbook'ları sırasında hello yerel ortamında kaynaklara karşı bir karma Runbook çalışanı genellikle hedefleyen runbook'ları yönetmek beri büyük olasılıkla ancak önemli ölçüde farklı Azure Otomasyonu'nda genellikle hello Azure bulut kaynakları yönetin.

Azure Otomasyon karma Runbook çalışanı için bir runbook düzenleyebilirsiniz ancak tootest hello runbook hello düzenleyicisinde çalışırsanız ilgili sorunlar olabilir.  Merhaba yerel kaynakları Azure Otomasyonu ortamınızda; bu durumda yüklenmeyebilir erişen hello PowerShell modülleri hello test başarısız olur.  Yüklerseniz hello modülleri, gerekli sonra hello runbook çalışır, ancak tam bir test için yerel kaynak mümkün tooaccess olmaz.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>Karma Runbook çalışanını runbook başlatma
[Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md) bir runbook'u başlatmak için farklı yöntemleri açıklar.  Karma Runbook çalışanı ekler bir **RunOn** bir karma Runbook çalışan grubu hello adını belirtebileceğiniz seçeneği.  Bir grubu belirtilirse, ardından hello runbook alınır ve tarafından o gruptaki hello çalışanı çalıştırın.  Bu seçenek belirtilmezse, ardından onu Azure Otomasyonu'nda normal olarak çalıştırılır.

Hello Azure portalında bir runbook'u başlattığınızda ile sunulan bir **çalıştıracağınız** seçebileceğiniz seçeneği **Azure** veya **karma çalışanı**.  Seçerseniz **karma çalışanı**, hello Grup aşağı açılır listeden seçin, sonra.

Kullanım hello **RunOn** parametresi.  Komut toostart Windows PowerShell kullanarak MyHybridGroup adlı bir karma Runbook çalışan grubu üzerinde Test-Runbook adlı bir runbook aşağıdaki hello kullanabilirsiniz.

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> Merhaba **RunOn** parametresi toohello eklenen **başlangıç AzureAutomationRunbook** 0.9.1 sürümünde Microsoft Azure PowerShell cmdlet'i.  Yapmanız gerekenler [hello en son sürümü karşıdan](https://azure.microsoft.com/downloads/) yüklü daha önceki bir varsa.  Yalnızca bu sürümü, Windows Powershell'den hello runbook başlatılıyor bir iş istasyonunda tooinstall gerekir.  Tooinstall gerekmez hello çalışan bilgisayar üzerinde toostart runbook'lar o bilgisayardan düşünmüyorsanız.  Bu Otomasyon hesabınızda yüklü Azure Powershell toobe en son sürümünü hello gerektiren bu yana bir runbook şu anda başka bir runbook'tan bir karma Runbook çalışanı üzerinde başlatılamıyor.  Merhaba en son sürümü Azure Otomasyonu'nda otomatik olarak güncelleştirilir ve toohello çalışanları en kısa sürede otomatik olarak gönderilir.
>
>

## <a name="runbook-permissions"></a>Runbook izinleri
Bir karma Runbook çalışanı üzerinde çalışan runbook'ları kullanmak aynı hello olamaz genelde runbook'ları Azure dışında kaynaklara erişmesi beri tooAzure kaynakları kimlik doğrulaması için kullanılan yöntem.  Merhaba runbook toolocal kaynakları ya da kendi kimlik doğrulaması sağlayabilir veya bir RunAs hesabı tooprovide tüm runbook'lar için bir kullanıcı bağlamı belirtebilirsiniz.

### <a name="runbook-authentication"></a>Runbook kimlik doğrulaması
Bunlar erişecek kendi kimlik doğrulama tooresources sağlamanız gerekir varsayılan olarak, runbook'ları hello şirket içi bilgisayardaki yerel sistem hesabı hello hello bağlamında çalıştırın.  

Kullanabileceğiniz [kimlik bilgisi](http://msdn.microsoft.com/library/dn940015.aspx) ve [sertifika](http://msdn.microsoft.com/library/dn940013.aspx) runbook'unuzda toodifferent kaynakları doğrulanabilir şekilde toospecify kimlik bilgilerine izin ver cmdlet'leri ile varlıklar.  Merhaba aşağıdaki örnek bir bilgisayarı yeniden başlatır bir runbook bir kısmı gösterir.  Kimlik bilgileri bir değişken varlığı hello bilgisayardan kimlik bilgisi varlığı ve hello adını alır ve ardından bu değerleri hello Restart-Computer cmdlet'iyle kullanır.

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

Ayrıca yararlanabilirsiniz [Inlinescript](automation-powershell-workflow.md#inlinescript), olanak sağlayan kod toorun blokları başka bir bilgisayarda hello tarafından belirtilen kimlik bilgileriyle [PSCredential ortak parametresi](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="runas-account"></a>RunAs hesabı
Belirleyebileceğiniz toolocal kaynakları kendi kimlik doğrulaması sağlamak runbook'lar sahip olmak yerine bir **RunAs** hesap için bir karma çalışanı grubu.  Belirttiğiniz bir [kimlik bilgisi varlığı](automation-credentials.md) toolocal erişimine sahip ve hello grubundaki bir karma Runbook çalışanı üzerinde çalışan tüm runbook'ları bu kimlik bilgileri altında çalıştırın.  

Merhaba kimlik bilgisi için Hello kullanıcı adı biçimleri aşağıdaki hello biri olmalıdır:

* etki alanı\kullanıcı adı
* username@domain
* Kullanıcı adı (için yerel toohello şirket içi bilgisayar hesapları)

Aşağıdaki yordam toospecify karma çalışanı grubu için bir RunAs hesabı hello kullan:

1. Oluşturma bir [kimlik bilgisi varlığı](automation-credentials.md) erişim toolocal kaynaklara sahip.
2. Hello Azure portal Hello Automation hesabını açın.
3. Select hello **karma çalışan grupları** döşeme ve hello grubu seçin.
4. Seçin **tüm ayarları** ve ardından **karma çalışanı grubu ayarları**.
5. Değişiklik **Çalıştır** gelen **varsayılan** çok**özel**.
6. Merhaba kimlik bilgisi seçip tıklatın **kaydetmek**.

### <a name="automation-run-as-account"></a>Automation farklı çalıştır hesabı
Azure'daki kaynakların dağıtımı için otomatik yapı işleminizin bir parçası olarak, erişim tooon içi sistemleri toosupport bir görev veya grup adımı, dağıtım sırası gerektirebilir.  Merhaba farklı çalıştır hesabını kullanarak Azure karşı kimlik doğrulamasını toosupport, tooinstall hello farklı çalıştır hesabı sertifikası gerekir.  

PowerShell runbook aşağıdaki hello *verme RunAsCertificateToHybridWorker*, Azure Otomasyonu hesabınızı hello Çalıştır sertifika verir ve indirir ve bunu hello yerel makine sertifika deposuna aktarır bir Karma çalışanı bağlı toohello aynı hesabı.  Bu adım tamamlandıktan sonra hello çalışan tooAzure hello farklı çalıştır hesabını kullanarak kimlik doğrulamasını başarıyla doğrular.

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

Merhaba Kaydet *verme RunAsCertificateToHybridWorker* runbook tooyour bilgisayarla bir `.ps1` uzantısı.  Otomasyon hesabınızda içeri aktarın ve hello hello değişkeninin değerini değiştirme hello runbook düzenleme `$Password` kendi parolanızı ile.  Yayımlama ve çalıştıran ve runbook'ları hello farklı çalıştır hesabını kullanarak kimlik doğrulaması hello karma çalışanı grubu hedefleme hello runbook çalıştırın.  Merhaba iş akışı raporları hello girişimi tooimport hello sertifika hello yerel makine deposunu ve kaç tane Automation hesapları aboneliğinizde tanımlanır ve kimlik doğrulaması başarılı olup olmadığını bağlı olarak birden fazla satır ile aşağıdaki.  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>Karma Runbook çalışanı runbook'larda sorun giderme
Günlükleri yerel olarak her karma çalışanı C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes konumunda depolanır.  Karma çalışanı de kaydeder hatalarını ve olaylarını hello Windows olay günlüğünde altında **uygulama ve Hizmetleri Logs\Microsoft-SMA\Operational**.  Olaylar ilgili hello çalışan üzerinde yürütülen toorunbooks çok yazılır**uygulama ve Hizmetleri Logs\Microsoft-Automation\Operational**.  Merhaba **Microsoft SMA** günlük pek çok daha fazla olayları ilgili toohello runbook işi basılmış toohello çalışan ve hello işlenmesini hello runbook içerir.  Merhaba sırasında **Microsoft Otomasyon** olay günlüğü sahip değil birçok olay runbook yürütülmesi hello sorun giderme konusunda yardımcı ayrıntılarla ve hello sonuçları hello runbook işi, en az bulacaksınız.  

[Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md) karma çalışanları yalnızca Otomasyon gibi hello bulutta çalışan runbook işleri tooAzure gönderilir.  Merhaba ayrıntılı de etkinleştirebilir ve ilerleme akışları hello aynı diğer runbook'lar için oluşturursunuz.  

Runbook'larınızın başarıyla tamamlanamamasının ve Özet hello iş durumunu gösterir **askıya alındı**, lütfen sorun giderme makalesi hello gözden [karma Runbook çalışanı: durum koduyla bir runbook işi sonlandırır Askıya](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).   

## <a name="next-steps"></a>Sonraki adımlar
* toolearn kullanılan toostart bir runbook olabilecek daha hello farklı yöntemler hakkında bkz [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md).  
* PowerShell ve PowerShell iş akışı runbook'ları hello metin düzenleyicisi kullanarak Azure Automation ile çalışma toounderstand hello farklı yordamlara bakın [Azure Otomasyon Runbook'u düzenleme](automation-edit-textual-runbook.md)
