---
title: "Azure Ağ İzleyicisi sorun giderme aaaMonitor VPN ağ geçitleri | Microsoft Docs"
description: "Bu makalede Azure Automation ve Ağ İzleyicisi ile şirket içi bağlantı nasıl Tanılama"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Ağ İzleyicisi sorun giderme VPN ağ geçitleri izleme

Ağ performansı ayrıntılı Öngörüler elde kritik tooprovide güvenilir hizmetler toocustomers olur. Bu nedenle kritik toodetect ağ kesintisi koşulları hızla olduğundan ve düzeltme eylemi toomitigate hello kesinti koşul alın. Azure Otomasyonu ve runbook'ları programlı bir şekilde bir görevi çalıştırmayı tooimplement sağlar. Azure otomasyonu kullanarak, sürekli ve öngörülü ağ izleme ve uyarma gerçekleştirmek için mükemmel bir tarif oluşturur.

## <a name="scenario"></a>Senaryo

Merhaba görüntü aşağıdaki hello içinde çok katmanlı bir uygulama ile bir VPN ağ geçidi ve tünel kullanılarak şirket içi bağlantısı senaryodur. VPN ağ geçidi çalışıyor hello olduktan ve çalışan kritik toohello uygulamaları performansı gelir.

Bir runbook bir komut dosyası toocheck bağlantı durumu bağlantı tünel durumunun hello kaynak sorun giderme API toocheck kullanarak hello VPN tüneli için oluşturulur. Merhaba durumu sağlıklı değil, bir e-posta tetikleyicisi tooadministrators gönderilir.

![Senaryo örneği][scenario]

Bu senaryo aşağıdakileri yapar:

- Bir runbook çağırma hello oluşturmak `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot bağlantı durumu
- Bir zamanlama toohello runbook Bağla

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo başlamadan önce aşağıdaki ön koşullar hello sahip olmanız gerekir:

- Bir Azure Otomasyonu hesabı Azure. Merhaba Otomasyon hesabı hello son modülleri sahip ve aynı zamanda hello AzureRM.Network modülü olduğundan emin olun. Merhaba AzureRM.Network modülü kullanılabilir hello modülü Galerisi'nde tooadd ihtiyacınız varsa onu tooyour automation hesabı.
- Azure Otomasyonu'nda yapılandırma kimlik bilgileri kümesi olması gerekir. Hakkında daha fazla bilgi edinin [Azure Automation güvenliği](../automation/automation-security-overview.md)
- Geçerli bir SMTP sunucusu (Office 365, şirket içi e-posta veya başka bir) ve Azure Automation'da tanımlanan kimlik bilgileri
- Yapılandırılmış bir sanal ağ ağ geçidi azure'da.
- Mevcut bir kapsayıcı toostore hello varolan bir depolama hesabıyla oturum açtığında.

> [!NOTE]
> Görüntü önceki hello gösterilen hello altyapı çizim amaçlıdır ve bu makalenin içerdiği hello adımlara oluşturulmaz.

### <a name="create-hello-runbook"></a>Merhaba runbook oluşturma

Merhaba ilk adım tooconfiguring hello toocreate hello runbook örnektir. Bu örnek, bir farklı çalıştır hesabını kullanır. toolearn Çalıştır hesaplarıyla ilgili ziyaret [kimlik doğrulaması runbook'larına sahip Azure farklı çalıştır hesabı](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>1. Adım

TooAzure Otomasyon hello içinde gezinmek [Azure portal](https://portal.azure.com) tıklatıp **runbook'ları**

![Automation hesabına genel bakış][1]

### <a name="step-2"></a>2. Adım

Tıklatın **runbook Ekle** hello runbook'un toostart hello oluşturma işlemi.

![runbook'ları dikey penceresi][2]

### <a name="step-3"></a>3. Adım

Altında **hızlı Oluştur**, tıklatın **yeni bir runbook oluşturmak** toocreate hello runbook.

![bir runbook dikey penceresinde ekleme][3]

### <a name="step-4"></a>4. Adım

Bu adımda, biz hello runbook bir ad verin, hello örnekte adlı **Get-VPNGatewayStatus**. Önemli toogive hello runbook açıklayıcı bir addır ve PowerShell standart adlandırma standartlarını takip eden bir ad verip önerilir. Bu örneğin Hello runbook türü **PowerShell**, hello diğer grafik, PowerShell iş akışı, seçeneklerdir ve grafik PowerShell iş akışı.

![runbook dikey penceresi][4]

### <a name="step-5"></a>5. Adım

Bu adımda hello runbook oluşturulur, aşağıdaki kod örneğine hello tüm hello örnek için gereken kod hello sağlar. Merhaba içeren öğelerini hello kodda \<değeri\> aboneliğiniz hello değerlerle yerini toobe gerekir.

Kullanım hello aşağıdaki kod tıklatın **Kaydet**

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a>6. Adım

Merhaba runbook kaydedildikten sonra bir zamanlama olmalıdır bağlı tooit tooautomate hello hello runbook başlangıcı. toostart hello işlem tıklatın **zamanlama**.

![6. Adım][6]

## <a name="link-a-schedule-toohello-runbook"></a>Bir zamanlama toohello runbook Bağla

Yeni bir zamanlama oluşturulması gerekir. Tıklatın **bir zamanlama tooyour runbook bağlantı**.

![7. Adım][7]

### <a name="step-1"></a>1. Adım

Merhaba üzerinde **zamanlama** dikey penceresinde tıklatın **yeni bir zamanlama oluşturun**

![8. Adım][8]

### <a name="step-2"></a>2. Adım

Merhaba üzerinde **yeni zamanlama** hello zamanlama bilgilerini dikey doldururken. ayarlanabilir hello değerler listesi aşağıdaki hello şunlardır:

- **Ad** -hello zamanlama hello kolay adı.
- **Açıklama** -hello zamanlama açıklaması.
- **Başlatır** -bu değer tarih, saat ve hello zaman hello zamanlama Tetikleyicileri olun saat dilimi bir birleşimidir.
- **Yineleme** -bu değer hello zamanlamaları yineleme belirler.  Geçerli değerler **kez** veya **yinelenen**.
- **Tekrarlamayı her** -hello zamanlama saat, gün, hafta veya ay içinde hello yineleme aralığı.
- **Sona erme süresini ayarlamanıza** -hello değerini belirleyen hello zamanlama veya sona durumunda. Çok ayarlanabilir**Evet** veya **Hayır**. Geçerli tarih ve saat Evet seçilirse sağlanan toobe var.

> [!NOTE]
> (Diğer bir deyişle, 15, 30, 45 dakika hello saat sonra) farklı aralıklarla saatte daha sık çalışacak bir runbook'tan toohave ihtiyacınız varsa, birden çok zamanlama oluşturulmalıdır

![9. Adım][9]

### <a name="step-3"></a>3. Adım

Toosave hello zamanlama toohello runbook tıklatın.

![10. adım][10]

## <a name="next-steps"></a>Sonraki adımlar

Nasıl bir anlama sahip olduğunuza toointegrate Azure Automation ile Ağ İzleyicisi sorun gidermeyi öğrenme nasıl tootrigger paket VM uyarılar ziyaret ederek yakalar [bir uyarı tetiklenen paket yakalama Azure Ağ İzleyicisioluşturma](network-watcher-alert-triggered-packet-capture.md).

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
