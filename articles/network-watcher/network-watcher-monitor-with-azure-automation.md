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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="ed51a-103">Ağ İzleyicisi sorun giderme VPN ağ geçitleri izleme</span><span class="sxs-lookup"><span data-stu-id="ed51a-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="ed51a-104">Ağ performansı ayrıntılı Öngörüler elde kritik tooprovide güvenilir hizmetler toocustomers olur.</span><span class="sxs-lookup"><span data-stu-id="ed51a-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="ed51a-105">Bu nedenle kritik toodetect ağ kesintisi koşulları hızla olduğundan ve düzeltme eylemi toomitigate hello kesinti koşul alın.</span><span class="sxs-lookup"><span data-stu-id="ed51a-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="ed51a-106">Azure Otomasyonu ve runbook'ları programlı bir şekilde bir görevi çalıştırmayı tooimplement sağlar.</span><span class="sxs-lookup"><span data-stu-id="ed51a-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="ed51a-107">Azure otomasyonu kullanarak, sürekli ve öngörülü ağ izleme ve uyarma gerçekleştirmek için mükemmel bir tarif oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ed51a-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="ed51a-108">Senaryo</span><span class="sxs-lookup"><span data-stu-id="ed51a-108">Scenario</span></span>

<span data-ttu-id="ed51a-109">Merhaba görüntü aşağıdaki hello içinde çok katmanlı bir uygulama ile bir VPN ağ geçidi ve tünel kullanılarak şirket içi bağlantısı senaryodur.</span><span class="sxs-lookup"><span data-stu-id="ed51a-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="ed51a-110">VPN ağ geçidi çalışıyor hello olduktan ve çalışan kritik toohello uygulamaları performansı gelir.</span><span class="sxs-lookup"><span data-stu-id="ed51a-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="ed51a-111">Bir runbook bir komut dosyası toocheck bağlantı durumu bağlantı tünel durumunun hello kaynak sorun giderme API toocheck kullanarak hello VPN tüneli için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ed51a-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="ed51a-112">Merhaba durumu sağlıklı değil, bir e-posta tetikleyicisi tooadministrators gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ed51a-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![Senaryo örneği][scenario]

<span data-ttu-id="ed51a-114">Bu senaryo aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="ed51a-114">This scenario will:</span></span>

- <span data-ttu-id="ed51a-115">Bir runbook çağırma hello oluşturmak `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot bağlantı durumu</span><span class="sxs-lookup"><span data-stu-id="ed51a-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="ed51a-116">Bir zamanlama toohello runbook Bağla</span><span class="sxs-lookup"><span data-stu-id="ed51a-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ed51a-117">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ed51a-117">Before you begin</span></span>

<span data-ttu-id="ed51a-118">Bu senaryo başlamadan önce aşağıdaki ön koşullar hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ed51a-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="ed51a-119">Bir Azure Otomasyonu hesabı Azure.</span><span class="sxs-lookup"><span data-stu-id="ed51a-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="ed51a-120">Merhaba Otomasyon hesabı hello son modülleri sahip ve aynı zamanda hello AzureRM.Network modülü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ed51a-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="ed51a-121">Merhaba AzureRM.Network modülü kullanılabilir hello modülü Galerisi'nde tooadd ihtiyacınız varsa onu tooyour automation hesabı.</span><span class="sxs-lookup"><span data-stu-id="ed51a-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="ed51a-122">Azure Otomasyonu'nda yapılandırma kimlik bilgileri kümesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed51a-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="ed51a-123">Hakkında daha fazla bilgi edinin [Azure Automation güvenliği](../automation/automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ed51a-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="ed51a-124">Geçerli bir SMTP sunucusu (Office 365, şirket içi e-posta veya başka bir) ve Azure Automation'da tanımlanan kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="ed51a-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="ed51a-125">Yapılandırılmış bir sanal ağ ağ geçidi azure'da.</span><span class="sxs-lookup"><span data-stu-id="ed51a-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="ed51a-126">Mevcut bir kapsayıcı toostore hello varolan bir depolama hesabıyla oturum açtığında.</span><span class="sxs-lookup"><span data-stu-id="ed51a-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="ed51a-127">Görüntü önceki hello gösterilen hello altyapı çizim amaçlıdır ve bu makalenin içerdiği hello adımlara oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="ed51a-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="ed51a-128">Merhaba runbook oluşturma</span><span class="sxs-lookup"><span data-stu-id="ed51a-128">Create hello runbook</span></span>

<span data-ttu-id="ed51a-129">Merhaba ilk adım tooconfiguring hello toocreate hello runbook örnektir.</span><span class="sxs-lookup"><span data-stu-id="ed51a-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="ed51a-130">Bu örnek, bir farklı çalıştır hesabını kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed51a-130">This example uses a run-as account.</span></span> <span data-ttu-id="ed51a-131">toolearn Çalıştır hesaplarıyla ilgili ziyaret [kimlik doğrulaması runbook'larına sahip Azure farklı çalıştır hesabı](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="ed51a-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="ed51a-132">1. Adım</span><span class="sxs-lookup"><span data-stu-id="ed51a-132">Step 1</span></span>

<span data-ttu-id="ed51a-133">TooAzure Otomasyon hello içinde gezinmek [Azure portal](https://portal.azure.com) tıklatıp **runbook'ları**</span><span class="sxs-lookup"><span data-stu-id="ed51a-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Automation hesabına genel bakış][1]

### <a name="step-2"></a><span data-ttu-id="ed51a-135">2. Adım</span><span class="sxs-lookup"><span data-stu-id="ed51a-135">Step 2</span></span>

<span data-ttu-id="ed51a-136">Tıklatın **runbook Ekle** hello runbook'un toostart hello oluşturma işlemi.</span><span class="sxs-lookup"><span data-stu-id="ed51a-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![runbook'ları dikey penceresi][2]

### <a name="step-3"></a><span data-ttu-id="ed51a-138">3. Adım</span><span class="sxs-lookup"><span data-stu-id="ed51a-138">Step 3</span></span>

<span data-ttu-id="ed51a-139">Altında **hızlı Oluştur**, tıklatın **yeni bir runbook oluşturmak** toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="ed51a-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![bir runbook dikey penceresinde ekleme][3]

### <a name="step-4"></a><span data-ttu-id="ed51a-141">4. Adım</span><span class="sxs-lookup"><span data-stu-id="ed51a-141">Step 4</span></span>

<span data-ttu-id="ed51a-142">Bu adımda, biz hello runbook bir ad verin, hello örnekte adlı **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="ed51a-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="ed51a-143">Önemli toogive hello runbook açıklayıcı bir addır ve PowerShell standart adlandırma standartlarını takip eden bir ad verip önerilir.</span><span class="sxs-lookup"><span data-stu-id="ed51a-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="ed51a-144">Bu örneğin Hello runbook türü **PowerShell**, hello diğer grafik, PowerShell iş akışı, seçeneklerdir ve grafik PowerShell iş akışı.</span><span class="sxs-lookup"><span data-stu-id="ed51a-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![runbook dikey penceresi][4]

### <a name="step-5"></a><span data-ttu-id="ed51a-146">5. Adım</span><span class="sxs-lookup"><span data-stu-id="ed51a-146">Step 5</span></span>

<span data-ttu-id="ed51a-147">Bu adımda hello runbook oluşturulur, aşağıdaki kod örneğine hello tüm hello örnek için gereken kod hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="ed51a-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="ed51a-148">Merhaba içeren öğelerini hello kodda \<değeri\> aboneliğiniz hello değerlerle yerini toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed51a-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="ed51a-149">Kullanım hello aşağıdaki kod tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="ed51a-149">Use hello following code as click **Save**</span></span>

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

### <a name="step-6"></a><span data-ttu-id="ed51a-150">6. Adım</span><span class="sxs-lookup"><span data-stu-id="ed51a-150">Step 6</span></span>

<span data-ttu-id="ed51a-151">Merhaba runbook kaydedildikten sonra bir zamanlama olmalıdır bağlı tooit tooautomate hello hello runbook başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="ed51a-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="ed51a-152">toostart hello işlem tıklatın **zamanlama**.</span><span class="sxs-lookup"><span data-stu-id="ed51a-152">toostart hello process, click **Schedule**.</span></span>

![6. Adım][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="ed51a-154">Bir zamanlama toohello runbook Bağla</span><span class="sxs-lookup"><span data-stu-id="ed51a-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="ed51a-155">Yeni bir zamanlama oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed51a-155">A new schedule must be created.</span></span> <span data-ttu-id="ed51a-156">Tıklatın **bir zamanlama tooyour runbook bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="ed51a-156">Click **Link a schedule tooyour runbook**.</span></span>

![7. Adım][7]

### <a name="step-1"></a><span data-ttu-id="ed51a-158">1. Adım</span><span class="sxs-lookup"><span data-stu-id="ed51a-158">Step 1</span></span>

<span data-ttu-id="ed51a-159">Merhaba üzerinde **zamanlama** dikey penceresinde tıklatın **yeni bir zamanlama oluşturun**</span><span class="sxs-lookup"><span data-stu-id="ed51a-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![8. Adım][8]

### <a name="step-2"></a><span data-ttu-id="ed51a-161">2. Adım</span><span class="sxs-lookup"><span data-stu-id="ed51a-161">Step 2</span></span>

<span data-ttu-id="ed51a-162">Merhaba üzerinde **yeni zamanlama** hello zamanlama bilgilerini dikey doldururken.</span><span class="sxs-lookup"><span data-stu-id="ed51a-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="ed51a-163">ayarlanabilir hello değerler listesi aşağıdaki hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ed51a-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="ed51a-164">**Ad** -hello zamanlama hello kolay adı.</span><span class="sxs-lookup"><span data-stu-id="ed51a-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="ed51a-165">**Açıklama** -hello zamanlama açıklaması.</span><span class="sxs-lookup"><span data-stu-id="ed51a-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="ed51a-166">**Başlatır** -bu değer tarih, saat ve hello zaman hello zamanlama Tetikleyicileri olun saat dilimi bir birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="ed51a-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="ed51a-167">**Yineleme** -bu değer hello zamanlamaları yineleme belirler.</span><span class="sxs-lookup"><span data-stu-id="ed51a-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="ed51a-168">Geçerli değerler **kez** veya **yinelenen**.</span><span class="sxs-lookup"><span data-stu-id="ed51a-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="ed51a-169">**Tekrarlamayı her** -hello zamanlama saat, gün, hafta veya ay içinde hello yineleme aralığı.</span><span class="sxs-lookup"><span data-stu-id="ed51a-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="ed51a-170">**Sona erme süresini ayarlamanıza** -hello değerini belirleyen hello zamanlama veya sona durumunda.</span><span class="sxs-lookup"><span data-stu-id="ed51a-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="ed51a-171">Çok ayarlanabilir**Evet** veya **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="ed51a-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="ed51a-172">Geçerli tarih ve saat Evet seçilirse sağlanan toobe var.</span><span class="sxs-lookup"><span data-stu-id="ed51a-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="ed51a-173">(Diğer bir deyişle, 15, 30, 45 dakika hello saat sonra) farklı aralıklarla saatte daha sık çalışacak bir runbook'tan toohave ihtiyacınız varsa, birden çok zamanlama oluşturulmalıdır</span><span class="sxs-lookup"><span data-stu-id="ed51a-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![9. Adım][9]

### <a name="step-3"></a><span data-ttu-id="ed51a-175">3. Adım</span><span class="sxs-lookup"><span data-stu-id="ed51a-175">Step 3</span></span>

<span data-ttu-id="ed51a-176">Toosave hello zamanlama toohello runbook tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ed51a-176">Click Save toosave hello schedule toohello runbook.</span></span>

![10. adım][10]

## <a name="next-steps"></a><span data-ttu-id="ed51a-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ed51a-178">Next steps</span></span>

<span data-ttu-id="ed51a-179">Nasıl bir anlama sahip olduğunuza toointegrate Azure Automation ile Ağ İzleyicisi sorun gidermeyi öğrenme nasıl tootrigger paket VM uyarılar ziyaret ederek yakalar [bir uyarı tetiklenen paket yakalama Azure Ağ İzleyicisioluşturma](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="ed51a-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
