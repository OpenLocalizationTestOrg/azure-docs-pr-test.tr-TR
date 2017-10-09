---
title: "aaaTroubleshoot koruma hataları VMware/fiziksel tooAzure | Microsoft Docs"
description: "Bu makalede hello ortak VMware makine çoğaltma hataları ve nasıl tootroubleshoot bunları"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="9cd56-103">Şirket içi VMware/fiziksel sunucu çoğaltma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="9cd56-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="9cd56-104">VMware sanal makineleri veya fiziksel sunucuları Azure Site RECOVERY'yi kullanarak korurken, belirli bir hata iletisi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9cd56-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="9cd56-105">Bazı hello karşılaşılan, sorun giderme adımları tooresolve yanı sıra daha sık karşılaşılan hata iletileri bu makale ayrıntıları bunları.</span><span class="sxs-lookup"><span data-stu-id="9cd56-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="9cd56-106">İlk çoğaltma %0 takıldı</span><span class="sxs-lookup"><span data-stu-id="9cd56-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="9cd56-107">Biz destek karşılaştığınız hello ilk çoğaltma hatalarını kaynak sunucu işlemi sunucu veya işlem sunucusu Azure arasında tooconnectivity sorunları nedeniyle çoğu.</span><span class="sxs-lookup"><span data-stu-id="9cd56-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="9cd56-108">Çoğu durumda, kendi kendini yapabilecekleriniz aşağıda listelenen hello adımları izleyerek bu sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="9cd56-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="9cd56-109">Kaynak makinede Hello aşağıdakileri denetleyin</span><span class="sxs-lookup"><span data-stu-id="9cd56-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="9cd56-110">Kaynak sunucu makine komut satırından Telnet tooping hello işlem sunucusu https bağlantı noktası (varsayılan 9443) ile ağ bağlantısı sorunları veya güvenlik duvarı bağlantı noktası engelleme sorunları varsa toosee gösterildiği gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="9cd56-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="9cd56-111">PING tootest bağlantı kullanmayın, Telnet kullanın.</span><span class="sxs-lookup"><span data-stu-id="9cd56-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="9cd56-112">Telnet yüklü değilse hello adımları listesini izleyen [burada](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="9cd56-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="9cd56-113">Sorun hala açamıyor tooconnect gelen bağlantı noktası 9443 hello işlem sunucusu izin ver ve hello olup olmadığını denetleyin çıkar.</span><span class="sxs-lookup"><span data-stu-id="9cd56-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="9cd56-114">İşlem sunucusu bu soruna neden olan DMZ olduğu bazı durumlarda açıldı.</span><span class="sxs-lookup"><span data-stu-id="9cd56-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="9cd56-115">Hizmetin Hello durumunu denetlemek `InMage Scout VX Agent – Sentinel/OutpostStart` hello sorun devam ederse çalıştığından ve onay değilse.</span><span class="sxs-lookup"><span data-stu-id="9cd56-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="9cd56-116">İŞLEM sunucusundaki Hello aşağıdakileri denetleyin</span><span class="sxs-lookup"><span data-stu-id="9cd56-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="9cd56-117">**İşlem sunucusu veri tooAzure etkin olarak gönderilmesi olmadığını denetleyin**</span><span class="sxs-lookup"><span data-stu-id="9cd56-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="9cd56-118">İşlem sunucusu makineden hello Görev Yöneticisi'ni (Ctrl-Shift-Esc tuşuna basın) açın.</span><span class="sxs-lookup"><span data-stu-id="9cd56-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="9cd56-119">Toohello performans sekmesine gidin ve 'Açık Kaynak İzleyicisi' bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9cd56-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="9cd56-120">Kaynak Yöneticisi'nden tooNetwork sekmesine gidin. Cbengine.exe 'Ağ etkinliği işlemlerle' ın büyük miktarda veri (MB) cinsinden etkin olarak gönderme olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="9cd56-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="9cd56-122">Aksi halde aşağıda listelenen hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="9cd56-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="9cd56-123">**İşlem sunucusu mümkün tooconnect Azure Blob olup olmadığını denetle**: seçin ve işlem sunucusu tooAzure depolama blob URL'si bağlantısını cbengine.exe tooview hello 'TCP bağlantılarını' toosee denetleyin.</span><span class="sxs-lookup"><span data-stu-id="9cd56-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="9cd56-125">Aksi halde tooControl Masası Git > Hizmetleri denetleyin Hizmetleri aşağıdaki hello hazır ve çalışır olup olmadığını:</span><span class="sxs-lookup"><span data-stu-id="9cd56-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="9cd56-126">(Re) Hangi çalışmıyor herhangi bir hizmeti başlatın ve hello sorun hala olup olmadığını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="9cd56-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="9cd56-127">**İşlem sunucusu bağlantı noktası 443 aracılığıyla mümkün tooconnect tooAzure genel IP adresi olup olmadığını denetleyin**</span><span class="sxs-lookup"><span data-stu-id="9cd56-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="9cd56-128">Açık gelen son CBEngineCurr.errlog hello `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` arayın ve: 443 ve bağlantı girişimi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="9cd56-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="9cd56-130">Sorun varsa, telnet tooping işlem sunucusu komut satırından kullanmak hello CBEngineCurr.currLog bulundu (içinde görüntünün üzerinde maskelenmiş) Azure genel IP adresinizin 443 numaralı bağlantı noktasını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9cd56-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="9cd56-131">%S tooconnect varsa, hello erişim sorununu son toofirewall veya sonraki adımda açıklandığı gibi Proxy sonra kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="9cd56-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="9cd56-132">**IP adresi tabanlı Güvenlik Duvarı'nı işlem sunucusu engellemediğini varsa erişimi denetleme**: hello sunucuda bir IP adresi tabanlı güvenlik duvarı kuralları kullanıyorsanız, hello tam listesi Microsoft Azure veri merkezi IP aralıkları indirme [burada ](https://www.microsoft.com/download/details.aspx?id=41653) ve iletişim tooAzure (ve hello HTTPS (443 numaralı) bağlantı noktası) sağlarlar tooyour güvenlik duvarı yapılandırması tooensure ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9cd56-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="9cd56-133">IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.</span><span class="sxs-lookup"><span data-stu-id="9cd56-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="9cd56-134">**İşlem sunucusu URL'si tabanlı güvenlik duvarının erişimi engellemediğini varsa denetleyin**: hello sunucuda temel URL güvenlik duvarı kuralları kullanıyorsanız, aşağıdaki URL'lere hello toofirewall yapılandırma eklenir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9cd56-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="9cd56-135">`*.accesscontrol.windows.net:` Erişim denetimi ve kimlik yönetimi için kullanılır</span><span class="sxs-lookup"><span data-stu-id="9cd56-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="9cd56-136">`*.backup.windowsazure.com:` Çoğaltma veri aktarımı ve düzenlemesi için kullanılır</span><span class="sxs-lookup"><span data-stu-id="9cd56-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="9cd56-137">`*.blob.core.windows.net:`Erişim toohello için kullanılan veri depolayan bir depolama hesabı çoğaltılan</span><span class="sxs-lookup"><span data-stu-id="9cd56-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="9cd56-138">`*.hypervrecoverymanager.windowsazure.com:` Çoğaltma yönetimi işlemleri ve düzenleme için kullanılır</span><span class="sxs-lookup"><span data-stu-id="9cd56-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="9cd56-139">`time.nist.gov`ve `time.windows.com`: toocheck zaman eşitleme sistem genel zaman arasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9cd56-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="9cd56-140">URL'ler için **Azure Bulutu**:</span><span class="sxs-lookup"><span data-stu-id="9cd56-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="9cd56-141">**İşlem sunucusundaki proxy ayarlarını erişim engellemediğinden varsa denetleyin**.</span><span class="sxs-lookup"><span data-stu-id="9cd56-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="9cd56-142">Bir Proxy sunucu kullanıyorsanız, hello DNS sunucusu tarafından hello proxy sunucu adı çözülürken emin olun.</span><span class="sxs-lookup"><span data-stu-id="9cd56-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="9cd56-143">toocheck yapılandırma sunucusu Kurulum hello sırasında sağlanan.</span><span class="sxs-lookup"><span data-stu-id="9cd56-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="9cd56-144">Tooregistry anahtar gidin</span><span class="sxs-lookup"><span data-stu-id="9cd56-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="9cd56-145">Şimdi aynı ayarları Azure Site Recovery aracı toosend verilerini tarafından kullanılmakta olan bu hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="9cd56-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="9cd56-146">Arama Microsoft Azure yedekleme</span><span class="sxs-lookup"><span data-stu-id="9cd56-146">Search Microsoft Azure  Backup</span></span> 

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="9cd56-148">Bunu açıp eylemini tıklatın > özelliklerini değiştir.</span><span class="sxs-lookup"><span data-stu-id="9cd56-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="9cd56-149">Proxy yapılandırma sekmesi altında hello kayıt defteri ayarları tarafından gösterildiği gibi aynı olması gerekir hello proxy adresi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cd56-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="9cd56-150">Aksi durumda, lütfen toohello değiştirin aynı adres.</span><span class="sxs-lookup"><span data-stu-id="9cd56-150">If not, please change it toohello same address.</span></span>

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="9cd56-152">**Bant genişliği azaltma işlemi sunucu üzerinde sınırlı değildir, denetleme**: hello bant genişliğini artırmak ve hello sorun hala olup olmadığını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="9cd56-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="9cd56-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9cd56-153">Next steps</span></span>
<span data-ttu-id="9cd56-154">Daha fazla yardıma gereksinim duyarsanız, sorgunuzu çok sonrası[ASR Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="9cd56-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="9cd56-155">Etkin bir topluluk sahibiz ve bizim mühendisleri birini mümkün tooassist olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9cd56-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
