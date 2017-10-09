---
title: "aaaTroubleshoot Windows sanal makine etkinleştirme sorunlarını azure'da | Microsoft Docs"
description: "Merhaba sağlar sorun giderme için Azure'da Windows sanal makine etkinleştirme sorunlarını giderme adımları"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="87dac-103">Azure Windows sanal makine etkinleştirme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="87dac-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="87dac-104">Özel bir görüntüden oluşturulan Azure Windows sanal makine (VM) etkinleştirirken sorun varsa, bu belge tootroubleshoot hello sayısındaki sağlanan hello bilgileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87dac-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use hello information provided in this document tootroubleshoot hello issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="87dac-105">Belirti</span><span class="sxs-lookup"><span data-stu-id="87dac-105">Symptom</span></span>

<span data-ttu-id="87dac-106">Bir Azure Windows VM tooactivate çalıştığınızda bir hata alıyorsunuz ileti örnek aşağıdaki hello benzer:</span><span class="sxs-lookup"><span data-stu-id="87dac-106">When you try tooactivate an Azure Windows VM, you receive an error message resembles hello following sample:</span></span>

<span data-ttu-id="87dac-107">**Hata: 0xC004F074 hello yazılım LicensingService o hello bilgisayarın etkinleştirilemediğini bildirdi. Hiçbir anahtar ManagementService (KMS) bağlantı kurulamadı. Lütfen ek bilgi için hello uygulama olay günlüğüne bakın.**</span><span class="sxs-lookup"><span data-stu-id="87dac-107">**Error: 0xC004F074 hello Software LicensingService reported that hello computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see hello Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="87dac-108">Nedeni</span><span class="sxs-lookup"><span data-stu-id="87dac-108">Cause</span></span>
<span data-ttu-id="87dac-109">Genellikle, Azure VM etkinleştirme sorunlar hello Windows VM tarafından yapılandırılmamışsa hello uygun KMS istemci kurulum anahtarı kullanarak veya bir bağlantı sorunu toohello Azure KMS hizmeti (kms.core.windows.net, bağlantı noktası 1668) hello Windows VM sahip oluşur.</span><span class="sxs-lookup"><span data-stu-id="87dac-109">Generally, Azure VM activation issues occur if hello Windows VM is not configured by using hello appropriate KMS client setup key, or hello Windows VM has a connectivity problem toohello Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="87dac-110">Çözüm</span><span class="sxs-lookup"><span data-stu-id="87dac-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="87dac-111">Siteden siteye VPN kullanıyorsanız ve zorlanan tünel, bkz: [kullanım Azure özel yönlendirir zorlamalı tünel ile tooenable KMS etkinleştirmesi](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="87dac-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes tooenable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="87dac-112">ExpressRoute kullanarak ve varsa varsayılan rota yayımlanan bkz [Azure VM ExpressRoute tooactivate başarısız olabilir](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="87dac-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail tooactivate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="87dac-113">1. adım yapılandırma hello uygun KMS istemci kurulum anahtarı (Windows Server 2016 ve Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="87dac-113">Step 1 Configure hello appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="87dac-114">Windows Server 2016 veya Windows Server 2012 R2 özel bir görüntüden oluşturulan VM Hello için hello uygun KMS istemci kurulum anahtarı hello VM için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="87dac-114">For hello VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure hello appropriate KMS client setup key for hello VM.</span></span>

<span data-ttu-id="87dac-115">Bu adım tooWindows 2012 veya Windows 2008 R2'in geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="87dac-115">This step does not apply tooWindows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="87dac-116">Yalnızca Windows Server 2016 ve Windows Server 2012 R2 tarafından desteklenen hello Otomasyon sanal makine etkinleştirme (AVMA) özelliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="87dac-116">It uses hello Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="87dac-117">Çalıştırma **slmgr.vbs/dlv** yükseltilmiş bir komut isteminde.</span><span class="sxs-lookup"><span data-stu-id="87dac-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="87dac-118">Merhaba hello çıktısında açıklama değeri denetleyin ve perakende (Perakende kanal) veya toplu (VOLUME_KMSCLIENT) lisans ortamdan oluşturulduğu olup olmadığını belirleyin:</span><span class="sxs-lookup"><span data-stu-id="87dac-118">Check hello Description value in hello output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="87dac-119">Varsa **slmgr.vbs/dlv** komutları tooset hello aşağıdaki hello çalıştırmak, perakende kanal gösterir [KMS istemci kurulum anahtarı](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) hello Windows Server sürümü için kullanılıyorsa ve tooretry etkinleştirme zorla:</span><span class="sxs-lookup"><span data-stu-id="87dac-119">If **slmgr.vbs /dlv** shows RETAIL channel, run hello following commands tooset hello [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for hello version of Windows Server being used, and force it tooretry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="87dac-120">Örneğin, Windows Server 2016 Datacenter için hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="87dac-120">For example, for Windows Server 2016 Datacenter, you would run hello following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a><span data-ttu-id="87dac-121">2. adım hello VM Azure KMS hizmeti arasındaki hello bağlantıyı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="87dac-121">Step 2 Verify hello connectivity between hello VM and Azure KMS service</span></span>

1. <span data-ttu-id="87dac-122">İndirmeyi ve ayıklamayı hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) aracı tooa yerel klasörde hello değil etkinleştirme VM.</span><span class="sxs-lookup"><span data-stu-id="87dac-122">Download and extract hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool tooa local folder in hello VM that does not activate.</span></span> 

2. <span data-ttu-id="87dac-123">TooStart gidin, Windows PowerShell üzerinde arama, Windows PowerShell sağ tıklayın ve ardından yönetici olarak çalıştır'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="87dac-123">Go tooStart, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="87dac-124">Sanal makine bu hello toouse hello doğru Azure KMS sunucusunda yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="87dac-124">Make sure that hello VM is configured toouse hello correct Azure KMS server.</span></span> <span data-ttu-id="87dac-125">toodo Bu, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="87dac-125">toodo this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="87dac-126">Merhaba komutu döndürmelidir: anahtar yönetimi hizmeti makine adı tookms.core.windows.net:1688 başarılı bir şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="87dac-126">hello command should return: Key Management Service machine name set tookms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="87dac-127">Bağlantı toohello KMS sunucusuna sahip olmanızı Psping kullanarak doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="87dac-127">Verify by using Psping that you have connectivity toohello KMS server.</span></span> <span data-ttu-id="87dac-128">Merhaba Pstools.zip indirme ayıkladığınız toohello klasöre geçin ve hello aşağıdakini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="87dac-128">Switch toohello folder where you extracted hello Pstools.zip download, and then run hello following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="87dac-129">Merhaba ikinci son satırında hello çıktı, gördüğünüz emin olun: gönderilen = 4, alınan = 4, kaybolan = 0 (%0 kayıp).</span><span class="sxs-lookup"><span data-stu-id="87dac-129">In hello second-to-last line of hello output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="87dac-130">Kayıp 0'dan (sıfır) büyük olursa hello VM bağlantı toohello KMS sunucusunda yok.</span><span class="sxs-lookup"><span data-stu-id="87dac-130">If Lost is greater than 0 (zero), hello VM does not have connectivity toohello KMS server.</span></span> <span data-ttu-id="87dac-131">Bu durumda, hello VM olan bir sanal ağ ve özel bir DNS sunucusu belirttiği, bu DNS sunucusuna emin olun mümkün tooresolve kms.core.windows.net olur.</span><span class="sxs-lookup"><span data-stu-id="87dac-131">In this situation, if hello VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able tooresolve kms.core.windows.net.</span></span> <span data-ttu-id="87dac-132">Veya kms.core.windows.net gidermek hello DNS sunucusu tooone değiştirin.</span><span class="sxs-lookup"><span data-stu-id="87dac-132">Or, change hello DNS server tooone that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="87dac-133">Sanal ağdan tüm DNS sunucularına kaldırırsanız, sanal makineleri Azure'nın iç DNS hizmeti kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="87dac-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="87dac-134">Bu hizmet kms.core.windows.net çözümleyebilir.</span><span class="sxs-lookup"><span data-stu-id="87dac-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="87dac-135">Ayrıca bu hello Konuk Güvenlik Duvarı'nı etkinleştirme girişimlerini engelleyebilecek bir biçimde yapılandırılmamış doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="87dac-135">Also verify that hello guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="87dac-136">Başarılı bağlantı tookms.core.windows.net doğruladıktan sonra o yükseltilmiş Windows PowerShell isteminde komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="87dac-136">After you verify successful connectivity tookms.core.windows.net, run hello following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="87dac-137">Bu komut etkinleştirme birden çok kez çalışır.</span><span class="sxs-lookup"><span data-stu-id="87dac-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="87dac-138">Başarılı bir etkinleştirme hello aşağıdakine benzer bilgiler verir:</span><span class="sxs-lookup"><span data-stu-id="87dac-138">A successful activation returns information that resembles hello following:</span></span>

<span data-ttu-id="87dac-139">**Windows(R), Serverdatacentercore edition (12345678-1234-1234-1234-12345678) etkinleştiriliyor... Ürün başarıyla etkinleştirildi.**</span><span class="sxs-lookup"><span data-stu-id="87dac-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="87dac-140">SSS</span><span class="sxs-lookup"><span data-stu-id="87dac-140">FAQ</span></span> 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a><span data-ttu-id="87dac-141">Azure Marketi'nden hello Windows Server 2016 oluşturdum.</span><span class="sxs-lookup"><span data-stu-id="87dac-141">I created hello Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="87dac-142">Tooconfigure KMS anahtarı hello Windows Server 2016 etkinleştirmek için gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="87dac-142">Do I need tooconfigure KMS key for activating hello Windows Server 2016?</span></span> 
 
<span data-ttu-id="87dac-143">Hayır.</span><span class="sxs-lookup"><span data-stu-id="87dac-143">No.</span></span> <span data-ttu-id="87dac-144">Azure Market Hello görüntüde hello uygun KMS istemci kurulum anahtarı zaten yapılandırılmış sahiptir.</span><span class="sxs-lookup"><span data-stu-id="87dac-144">hello image in Azure Marketplace has hello appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="87dac-145">Merhaba VM veya Azure karma kullanımı Avantajı (HUB) kullanıyorsa, Windows etkinleştirme iş aynı şekilde bakılmaksızın hello mu?</span><span class="sxs-lookup"><span data-stu-id="87dac-145">Does Windows activation work hello same way regardless if hello VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="87dac-146">Evet.</span><span class="sxs-lookup"><span data-stu-id="87dac-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="87dac-147">Windows etkinleştirme süresi dolarsa ne olur?</span><span class="sxs-lookup"><span data-stu-id="87dac-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="87dac-148">Hello yetkisiz kullanım süresi dolmuştur ve Windows hala etkin olduğunda, Windows Server 2008 R2 ve sonraki Windows sürümlerini etkinleştirme hakkında ek bildirimleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="87dac-148">When hello grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="87dac-149">Merhaba masaüstü duvar kağıdı siyah kalır ve Windows Update, güvenlik ve yalnızca kritik güncelleştirmeler, ancak isteğe bağlı değil güncelleştirmeleri yükler.</span><span class="sxs-lookup"><span data-stu-id="87dac-149">hello desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="87dac-150">Merhaba bildirimleri bkz hello hello alt kısmına [lisans koşulları](http://technet.microsoft.com/en-us/library/ff793403.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="87dac-150">See  hello Notifications section at hello bottom of hello [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="87dac-151">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="87dac-151">Need help?</span></span> <span data-ttu-id="87dac-152">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="87dac-152">Contact support.</span></span>
<span data-ttu-id="87dac-153">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.</span><span class="sxs-lookup"><span data-stu-id="87dac-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
