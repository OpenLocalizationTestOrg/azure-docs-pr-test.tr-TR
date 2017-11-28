---
title: "Azure'da Windows sanal makine etkinleştirme sorunlarını giderme | Microsoft Docs"
description: "Azure'da Windows sanal makine etkinleştirme sorunlarını düzeltmek için sorun giderme adımları sağlar"
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
ms.openlocfilehash: 77ef396e0bf75fab56bda2e76516b481d018c5b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="e2c6d-103">Azure Windows sanal makine etkinleştirme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e2c6d-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e2c6d-104">Özel bir görüntüden oluşturulan Azure Windows sanal makine (VM) etkinleştirirken konusunda sorun yaşıyorsanız, sorunu gidermek için bu belgede sağlanan bilgileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use the information provided in this document to troubleshoot the issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="e2c6d-105">Belirti</span><span class="sxs-lookup"><span data-stu-id="e2c6d-105">Symptom</span></span>

<span data-ttu-id="e2c6d-106">Bir Azure Windows VM etkinleştirmeye çalıştığınızda aldığınız hata iletisi aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="e2c6d-106">When you try to activate an Azure Windows VM, you receive an error message resembles the following sample:</span></span>

<span data-ttu-id="e2c6d-107">**Hata: 0xC004F074 yazılım LicensingService bilgisayarın etkinleştirilemediğini bildirdi. Hiçbir anahtar ManagementService (KMS) bağlantı kurulamadı. Lütfen ek bilgi için uygulama olay günlüğüne bakın.**</span><span class="sxs-lookup"><span data-stu-id="e2c6d-107">**Error: 0xC004F074 The Software LicensingService reported that the computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see the Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="e2c6d-108">Nedeni</span><span class="sxs-lookup"><span data-stu-id="e2c6d-108">Cause</span></span>
<span data-ttu-id="e2c6d-109">Genellikle, Azure VM etkinleştirme sorunlar uygun KMS istemci kurulum anahtarı'nı kullanarak Windows VM yapılandırılmamış veya Windows VM (kms.core.windows.net, bağlantı noktası 1668) Azure KMS hizmetine bir bağlantı sorunu olup olmadığını oluşur.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-109">Generally, Azure VM activation issues occur if the Windows VM is not configured by using the appropriate KMS client setup key, or the Windows VM has a connectivity problem to the Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="e2c6d-110">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e2c6d-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="e2c6d-111">Siteden siteye VPN kullanıyorsanız ve zorlanan tünel, bkz: [KMS etkinleştirme'yle etkinleştirmek için özel yollar kullanım Azure zorlamalı tünel](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2c6d-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="e2c6d-112">ExpressRoute kullanarak ve varsa varsayılan rota yayımlanan bkz [Azure VM ExpressRoute etkinleştirmek başarısız olabilir](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2c6d-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-the-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="e2c6d-113">1. adım yapılandırma uygun KMS istemci kurulum anahtarını (Windows Server 2016 ve Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="e2c6d-113">Step 1 Configure the appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="e2c6d-114">Windows Server 2016 veya Windows Server 2012 R2 özel bir görüntüden oluşturulan VM için VM için uygun KMS istemci kurulum anahtarı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-114">For the VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure the appropriate KMS client setup key for the VM.</span></span>

<span data-ttu-id="e2c6d-115">Bu adım Windows 2012 veya Windows 2008 R2 için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-115">This step does not apply to Windows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="e2c6d-116">Yalnızca Windows Server 2016 ve Windows Server 2012 R2 tarafından desteklenen Otomasyon sanal makine etkinleştirme (AVMA) özelliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-116">It uses the Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="e2c6d-117">Çalıştırma **slmgr.vbs/dlv** yükseltilmiş bir komut isteminde.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="e2c6d-118">Çıktıda açıklama değerini denetleyin ve perakende (Perakende kanal) veya toplu (VOLUME_KMSCLIENT) lisans ortamdan oluşturulduğu olup olmadığını belirleyin:</span><span class="sxs-lookup"><span data-stu-id="e2c6d-118">Check the Description value in the output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="e2c6d-119">Varsa **slmgr.vbs/dlv** ayarlamak için aşağıdaki komutları çalıştırın, perakende kanal gösterir [KMS istemci kurulum anahtarı](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) Windows Server sürümü için kullanılıyorsa ve etkinleştirmeyi yeniden deneyin zorla:</span><span class="sxs-lookup"><span data-stu-id="e2c6d-119">If **slmgr.vbs /dlv** shows RETAIL channel, run the following commands to set the [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for the version of Windows Server being used, and force it to retry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="e2c6d-120">Örneğin, Windows Server 2016 Datacenter için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2c6d-120">For example, for Windows Server 2016 Datacenter, you would run the following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-the-connectivity-between-the-vm-and-azure-kms-service"></a><span data-ttu-id="e2c6d-121">2. adım VM ve Azure KMS hizmeti arasındaki bağlantıyı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="e2c6d-121">Step 2 Verify the connectivity between the VM and Azure KMS service</span></span>

1. <span data-ttu-id="e2c6d-122">İndirmeyi ve ayıklamayı [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) değil etkinleştirme VM yerel bir klasöre aracı.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-122">Download and extract the [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool to a local folder in the VM that does not activate.</span></span> 

2. <span data-ttu-id="e2c6d-123">Başlat'a gidin, Windows PowerShell üzerinde arama, Windows PowerShell sağ tıklayın ve ardından yönetici olarak çalıştır'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-123">Go to Start, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="e2c6d-124">VM doğru Azure KMS sunucusunu kullanacak şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-124">Make sure that the VM is configured to use the correct Azure KMS server.</span></span> <span data-ttu-id="e2c6d-125">Bunu yapmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2c6d-125">To do this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="e2c6d-126">Komutun döndürmesi: anahtar yönetimi hizmeti makine adı için kms.core.windows.net:1688 başarılı bir şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-126">The command should return: Key Management Service machine name set to kms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="e2c6d-127">KMS sunucusu bağlantısı yoksa Psping kullanarak doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-127">Verify by using Psping that you have connectivity to the KMS server.</span></span> <span data-ttu-id="e2c6d-128">Pstools.zip indirme ayıkladığınız klasöre geçin ve ardından şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2c6d-128">Switch to the folder where you extracted the Pstools.zip download, and then run the following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="e2c6d-129">Çıktı ikinci son satırında gördüğünüz emin olun: gönderilen = 4, alınan = 4, kaybolan = 0 (%0 kayıp).</span><span class="sxs-lookup"><span data-stu-id="e2c6d-129">In the second-to-last line of the output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="e2c6d-130">Kayıp 0'dan (sıfır) büyük ise, VM KMS sunucusu bağlantısı yok.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-130">If Lost is greater than 0 (zero), the VM does not have connectivity to the KMS server.</span></span> <span data-ttu-id="e2c6d-131">Bu durumda, sanal bir ağa VM ise ve özel bir DNS sunucusu belirttiği, bu DNS sunucusuna emin olun kms.core.windows.net çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-131">In this situation, if the VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able to resolve kms.core.windows.net.</span></span> <span data-ttu-id="e2c6d-132">Veya DNS sunucusu kms.core.windows.net çözümlenmesi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-132">Or, change the DNS server to one that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="e2c6d-133">Sanal ağdan tüm DNS sunucularına kaldırırsanız, sanal makineleri Azure'nın iç DNS hizmeti kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="e2c6d-134">Bu hizmet kms.core.windows.net çözümleyebilir.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="e2c6d-135">Ayrıca, Konuk Güvenlik Duvarı'nı etkinleştirme girişimlerini engelleyebilecek bir biçimde yapılandırılmamış doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-135">Also verify that the guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="e2c6d-136">Kms.core.windows.net başarılı bağlantı doğruladıktan sonra o yükseltilmiş Windows PowerShell komut isteminde aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-136">After you verify successful connectivity to kms.core.windows.net, run the following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="e2c6d-137">Bu komut etkinleştirme birden çok kez çalışır.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="e2c6d-138">Başarılı bir etkinleştirme aşağıdakine benzer bilgiler verir:</span><span class="sxs-lookup"><span data-stu-id="e2c6d-138">A successful activation returns information that resembles the following:</span></span>

<span data-ttu-id="e2c6d-139">**Windows(R), Serverdatacentercore edition (12345678-1234-1234-1234-12345678) etkinleştiriliyor... Ürün başarıyla etkinleştirildi.**</span><span class="sxs-lookup"><span data-stu-id="e2c6d-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="e2c6d-140">SSS</span><span class="sxs-lookup"><span data-stu-id="e2c6d-140">FAQ</span></span> 

### <a name="i-created-the-windows-server-2016-from-azure-marketplace-do-i-need-to-configure-kms-key-for-activating-the-windows-server-2016"></a><span data-ttu-id="e2c6d-141">Windows Server 2016 Azure Marketi'nden oluşturdum.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-141">I created the Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="e2c6d-142">Windows Server 2016 etkinleştirme için KMS anahtarı yapılandırmanız gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="e2c6d-142">Do I need to configure KMS key for activating the Windows Server 2016?</span></span> 
 
<span data-ttu-id="e2c6d-143">Hayır.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-143">No.</span></span> <span data-ttu-id="e2c6d-144">Azure Market görüntüde zaten yapılandırılmış uygun KMS istemci kurulum anahtarı vardır.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-144">The image in Azure Marketplace has the appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-the-same-way-regardless-if-the-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="e2c6d-145">VM veya Azure karma kullanımı Avantajı (HUB) kullanıyorsa, Windows etkinleştirme bakılmaksızın aynı şekilde çalışır?</span><span class="sxs-lookup"><span data-stu-id="e2c6d-145">Does Windows activation work the same way regardless if the VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="e2c6d-146">Evet.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="e2c6d-147">Windows etkinleştirme süresi dolarsa ne olur?</span><span class="sxs-lookup"><span data-stu-id="e2c6d-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="e2c6d-148">Yetkisiz kullanım süresi dolmuştur ve Windows hala etkin olduğunda, Windows Server 2008 R2 ve sonraki Windows sürümlerini etkinleştirme hakkında ek bildirimleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-148">When the grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="e2c6d-149">Masaüstü duvar kağıdı siyah kalır ve Windows Update, güvenlik ve yalnızca kritik güncelleştirmeler, ancak isteğe bağlı değil güncelleştirmeleri yükler.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-149">The desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="e2c6d-150">Ekranın alt kısmındaki bildirimleri bölümüne bakın [lisans koşulları](http://technet.microsoft.com/en-us/library/ff793403.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-150">See  the Notifications section at the bottom of the [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="e2c6d-151">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="e2c6d-151">Need help?</span></span> <span data-ttu-id="e2c6d-152">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-152">Contact support.</span></span>
<span data-ttu-id="e2c6d-153">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için.</span><span class="sxs-lookup"><span data-stu-id="e2c6d-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>