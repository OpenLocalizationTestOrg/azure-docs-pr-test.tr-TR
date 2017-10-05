---
title: "VMware/fiziksel Azure koruması hatalarını giderme | Microsoft Docs"
description: "Bu makalede ortak VMware makine çoğaltma hataları ve bunları ile ilgili sorunları giderme"
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
ms.openlocfilehash: 6ebec2e06566b1e2d6834fdd81c0d8b2801b80b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="826b9-103">Şirket içi VMware/fiziksel sunucu çoğaltma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="826b9-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="826b9-104">VMware sanal makineleri veya fiziksel sunucuları Azure Site RECOVERY'yi kullanarak korurken, belirli bir hata iletisi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="826b9-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="826b9-105">Bu makalede bazı karşılaştı, sorun giderme bunları gidermek için adımları yanı sıra daha sık karşılaşılan hata iletileri ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="826b9-105">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="826b9-106">İlk çoğaltma %0 takıldı</span><span class="sxs-lookup"><span data-stu-id="826b9-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="826b9-107">Kaynak sunucu işlemi sunucu veya işlem sunucusu Azure arasında bağlantı sorunları sizi desteğe karşılaştığınız ilk çoğaltma hataların çoğu kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="826b9-107">Most of the initial replication failures that we encounter at support are due to connectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="826b9-108">Çoğu durumda, kendi kendini yapabilecekleriniz aşağıda listelenen adımları izleyerek bu sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="826b9-108">For most cases, you can self troubleshoot these issues by following the steps listed below.</span></span>

###<a name="check-the-following-on-source-machine"></a><span data-ttu-id="826b9-109">Kaynak makinede aşağıdakileri denetleyin</span><span class="sxs-lookup"><span data-stu-id="826b9-109">Check the following on SOURCE MACHINE</span></span>
* <span data-ttu-id="826b9-110">Kaynak sunucu makine komut satırından Telnet https bağlantı noktası (varsayılan 9443) işlem sunucusuyla herhangi bir ağ bağlantısı sorunları veya güvenlik duvarı bağlantı noktası engelleme sorunları olup olmadığını görmek için aşağıda gösterildiği gibi ping işlemi yapmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="826b9-110">From Source Server machine command line, use Telnet to ping the Process Server with https port (default 9443) as shown below to see if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="826b9-111">Telnet kullanın, PING bağlantısını test etme için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="826b9-111">Use Telnet, don’t use PING to test connectivity.</span></span>  <span data-ttu-id="826b9-112">Telnet yüklü değilse, adımları listesini izleyen [burada](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="826b9-112">If Telnet is not installed, follow the steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="826b9-113">Alınamazsa bağlanmak, bağlantı noktasının 9443 işlem sunucusundaki izin ve sorun hala çıkar olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="826b9-113">If unable to connect, allow inbound port 9443 on the Process Server and check if the problem still exits.</span></span> <span data-ttu-id="826b9-114">İşlem sunucusu bu soruna neden olan DMZ olduğu bazı durumlarda açıldı.</span><span class="sxs-lookup"><span data-stu-id="826b9-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="826b9-115">Hizmetinin durumunu denetlemek `InMage Scout VX Agent – Sentinel/OutpostStart` sorun devam ederse çalıştığından ve onay değilse.</span><span class="sxs-lookup"><span data-stu-id="826b9-115">Check the status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if the problem still exists.</span></span>   
 
###<a name="check-the-following-on-process-server"></a><span data-ttu-id="826b9-116">İŞLEM sunucusunda aşağıdakileri denetleyin</span><span class="sxs-lookup"><span data-stu-id="826b9-116">Check the following on PROCESS SERVER</span></span>

* <span data-ttu-id="826b9-117">**İşlem sunucusu etkin olarak veri Azure'a dağıtmaya olmadığını denetleyin**</span><span class="sxs-lookup"><span data-stu-id="826b9-117">**Check if process server is actively pushing data to Azure**</span></span> 

<span data-ttu-id="826b9-118">İşlem sunucusu makineden Görev Yöneticisi'ni (Ctrl-Shift-Esc tuşuna basın) açın.</span><span class="sxs-lookup"><span data-stu-id="826b9-118">From Process Server machine, open the Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="826b9-119">Performans sekmesine gidin ve 'Açık Kaynak İzleyicisi' bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="826b9-119">Go to the Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="826b9-120">Kaynak Yöneticisi'nden ağ sekmesine gidin.</span><span class="sxs-lookup"><span data-stu-id="826b9-120">From Resource Manager, go to Network tab.</span></span> <span data-ttu-id="826b9-121">Cbengine.exe 'Ağ etkinliği işlemlerle' ın büyük miktarda veri (MB) cinsinden etkin olarak gönderme olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="826b9-121">Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="826b9-123">Aksi halde aşağıda listelenen adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="826b9-123">If not follow the steps listed below:</span></span>

* <span data-ttu-id="826b9-124">**İşlem sunucusu Azure Blob bağlanabiliyor olup olmadığını denetle**: seçin ve 'TCP Azure Storage blobu URL işlem sunucusu bağlantısını olup olmadığını görmek için bağlantıları' görüntülemek için cbengine.exe denetleyin.</span><span class="sxs-lookup"><span data-stu-id="826b9-124">**Check if Process server is able to connect Azure Blob**: Select and check cbengine.exe to view the ‘TCP Connections’ to see if there is connectivity from Process server to Azure Storage blob URL.</span></span>

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="826b9-126">Ardından gidin, Denetim Masası'na > Hizmetleri, aşağıdaki hizmetleri hazır ve çalışır olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="826b9-126">If not then go to Control Panel > Services, check if the following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="826b9-127">(Re) Hangi çalışmıyor herhangi bir hizmeti başlatın ve sorunu hala olup olmadığını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="826b9-127">(Re)Start any service which is not running and check if the problem still exists.</span></span>

* <span data-ttu-id="826b9-128">**İşlem sunucusu bağlantı noktası 443 aracılığıyla Azure genel IP adresine bağlanabiliyor olup olmadığını denetleyin**</span><span class="sxs-lookup"><span data-stu-id="826b9-128">**Check if Process server is able to connect to Azure Public IP address using port 443**</span></span>

<span data-ttu-id="826b9-129">En son CBEngineCurr.errlog gelen açmak `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` arayın ve: 443 ve bağlantı girişimi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="826b9-129">Open the latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="826b9-131">Sorun varsa, işlem sunucusunu komut satırından 443 numaralı bağlantı noktasını kullanarak CBEngineCurr.currLog içinde bulundu (içinde görüntünün üzerinde maskelenmiş), Azure genel IP adresine ping işlemi telnet kullanın.</span><span class="sxs-lookup"><span data-stu-id="826b9-131">If there are issues, then from Process Server command line, use telnet to ping your Azure Public IP address (masked in above image) found in the CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="826b9-132">Bağlanma sorunu, güvenlik duvarı veya bir sonraki adımda açıklandığı gibi Proxy nedeniyle erişim sorunu olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="826b9-132">If you are unable to connect, then check if the access issue is due to firewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="826b9-133">**IP adresi tabanlı Güvenlik Duvarı'nı işlem sunucusu engellemediğini varsa erişimi denetleme**: sunucu üzerinde bir IP adresi tabanlı güvenlik duvarı kuralları kullanıyorsanız, Microsoft Azure veri merkezi IP aralıkları tam listesi karşıdan [burada](https://www.microsoft.com/download/details.aspx?id=41653) ve bunları Azure (ve HTTPS (443 numaralı) bağlantı noktası) iletişimi sağlarlar emin olmak için güvenlik duvarı yapılandırmanızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="826b9-133">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on the server, then download the complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them to your firewall configuration to ensure they allow communication to Azure (and the HTTPS (443) port).</span></span>  <span data-ttu-id="826b9-134">Aboneliğinizin Azure bölgesi ve Batı ABD (Access Control ve Identity Management için kullanılır) için IP adresi aralıklarına izin verin.</span><span class="sxs-lookup"><span data-stu-id="826b9-134">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="826b9-135">**İşlem sunucusu URL'si tabanlı güvenlik duvarının erişimi engellemediğini varsa denetleyin**: sunucu üzerinde temel URL güvenlik duvarı kuralları kullanıyorsanız, aşağıdaki URL'ler için güvenlik duvarı yapılandırmasını eklenir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="826b9-135">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on the server, ensure the following URLs are added to firewall configuration.</span></span> 
     
  <span data-ttu-id="826b9-136">`*.accesscontrol.windows.net:` Erişim denetimi ve kimlik yönetimi için kullanılır</span><span class="sxs-lookup"><span data-stu-id="826b9-136">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="826b9-137">`*.backup.windowsazure.com:` Çoğaltma veri aktarımı ve düzenlemesi için kullanılır</span><span class="sxs-lookup"><span data-stu-id="826b9-137">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="826b9-138">`*.blob.core.windows.net:`Erişim depoları veri kopyalandığı depolama hesabı için kullanılan</span><span class="sxs-lookup"><span data-stu-id="826b9-138">`*.blob.core.windows.net:` Used for access to the storage account that stores replicated data</span></span>

  <span data-ttu-id="826b9-139">`*.hypervrecoverymanager.windowsazure.com:` Çoğaltma yönetimi işlemleri ve düzenleme için kullanılır</span><span class="sxs-lookup"><span data-stu-id="826b9-139">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="826b9-140">`time.nist.gov`ve `time.windows.com`: Sistem ve genel saat arasındaki zaman eşitlemesini denetlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="826b9-140">`time.nist.gov` and `time.windows.com`: Used to check time synchronization between system and global time.</span></span>

<span data-ttu-id="826b9-141">URL'ler için **Azure Bulutu**:</span><span class="sxs-lookup"><span data-stu-id="826b9-141">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="826b9-142">**İşlem sunucusundaki proxy ayarlarını erişim engellemediğinden varsa denetleyin**.</span><span class="sxs-lookup"><span data-stu-id="826b9-142">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="826b9-143">Bir Proxy sunucu kullanıyorsanız, proxy sunucu adı DNS sunucusu tarafından çözülürken emin olun.</span><span class="sxs-lookup"><span data-stu-id="826b9-143">If you are using a Proxy Server, ensure the proxy server name is resolving by the DNS server.</span></span>
<span data-ttu-id="826b9-144">Yapılandırma sunucusu Kurulum sırasında sağlanan denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="826b9-144">To check what you have provided at the time of Configuration Server setup.</span></span> <span data-ttu-id="826b9-145">Kayıt defteri anahtarına gidin</span><span class="sxs-lookup"><span data-stu-id="826b9-145">Go to registry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="826b9-146">Şimdi aynı ayarları Azure Site Recovery aracısı tarafından veri göndermek için kullanıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="826b9-146">Now ensure that the same settings are being used by Azure Site Recovery agent to send data.</span></span>
<span data-ttu-id="826b9-147">Arama Microsoft Azure yedekleme</span><span class="sxs-lookup"><span data-stu-id="826b9-147">Search Microsoft Azure  Backup</span></span> 

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="826b9-149">Bunu açıp eylemini tıklatın > özelliklerini değiştir.</span><span class="sxs-lookup"><span data-stu-id="826b9-149">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="826b9-150">Proxy Yapılandırması sekmesinde, kayıt defteri ayarları tarafından gösterildiği gibi aynı olması gerekir proxy adresi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="826b9-150">Under Proxy Configuration tab, you should see the proxy address, which should be same as shown by the registry settings.</span></span> <span data-ttu-id="826b9-151">Aksi durumda, lütfen aynı adrese değiştirin.</span><span class="sxs-lookup"><span data-stu-id="826b9-151">If not, please change it to the same address.</span></span>

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="826b9-153">**Bant genişliği azaltma işlemi sunucu üzerinde sınırlı değildir, denetleme**: bant genişliğini artırmak ve sorunu hala olup olmadığını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="826b9-153">**Check if Throttle bandwidth is not constrained on Process server**:  Increase the bandwidth  and check if the problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="826b9-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="826b9-154">Next steps</span></span>
<span data-ttu-id="826b9-155">Daha fazla yardıma gereksinim duyarsanız, sorgunuza sonrası [ASR Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="826b9-155">If you need more help, then post your query to [ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="826b9-156">Etkin bir topluluk sahibiz ve bizim mühendisleri biri size yardımcı olmak mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="826b9-156">We have an active community and one of our engineers will be able to assist you.</span></span>