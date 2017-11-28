---
title: "VPN verimlilik tooa Microsoft Azure sanal ağı doğrulama | Microsoft Docs"
description: "Merhaba bu belgenin amacı olan toohelp bir kullanıcı kendi şirket içi kaynakları tooan Azure sanal makinesi hello ağ akışından doğrulayın."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="c8919-103">Nasıl toovalidate VPN verimlilik tooa sanal ağ</span><span class="sxs-lookup"><span data-stu-id="c8919-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="c8919-104">Bir VPN gateway bağlantısı, sanal ağınız Azure içinde ve şirket içi arasında güvenli, şirket içi bağlantılar tooestablish sağlar BT altyapısı.</span><span class="sxs-lookup"><span data-stu-id="c8919-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="c8919-105">Bu makalede nasıl toovalidate ağ hello veri akışından kaynakları tooan Azure sanal makinesi şirket içi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c8919-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="c8919-106">Ayrıca, sorun giderme kılavuzu sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8919-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="c8919-107">Bu makale tasarlanmıştır toohelp tanılamak ve ortak sorunları giderin.</span><span class="sxs-lookup"><span data-stu-id="c8919-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="c8919-108">Bilgi, aşağıdaki hello kullanarak oluşturulamıyor toosolve hello sorun olduğunuzda [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="c8919-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="c8919-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c8919-109">Overview</span></span>

<span data-ttu-id="c8919-110">Merhaba VPN ağ geçidi bağlantısı hello aşağıdaki bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="c8919-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="c8919-111">Şirket içi VPN cihazı (bir listesini görüntülemek [doğrulanan VPN cihazları)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="c8919-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="c8919-112">Genel Internet</span><span class="sxs-lookup"><span data-stu-id="c8919-112">Public Internet</span></span>
- <span data-ttu-id="c8919-113">Azure VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="c8919-113">Azure VPN gateway</span></span>
- <span data-ttu-id="c8919-114">Azure sanal makinesi</span><span class="sxs-lookup"><span data-stu-id="c8919-114">Azure virtual machine</span></span>

<span data-ttu-id="c8919-115">Aşağıdaki diyagramda hello hello mantıksal bir şirket içi ağ tooan VPN aracılığıyla Azure sanal ağ bağlantısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c8919-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![Mantıksal müşteri ağ bağlantısı tooMSFT ağ VPN kullanarak](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="c8919-117">Merhaba maksimum beklenen giriş/çıkış Hesapla</span><span class="sxs-lookup"><span data-stu-id="c8919-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="c8919-118">Uygulamanızın temel üretilen iş gereksinimlerini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c8919-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="c8919-119">Azure VPN ağ geçidi işleme sınırları belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c8919-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="c8919-120">Yardım için hello "SKU ve VPN türüne göre toplam verimliliği" bölümüne bakın [planlama ve tasarım VPN ağ geçidi için](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="c8919-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="c8919-121">Merhaba belirlemek [Azure VM verimlilik Kılavuzu](../virtual-machines/virtual-machines-windows-sizes.md) VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="c8919-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="c8919-122">Internet servis sağlayıcısı (ISS) bant genişliğiniz belirler.</span><span class="sxs-lookup"><span data-stu-id="c8919-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="c8919-123">Beklenen Verimlilik - en az bant genişliği (VM, ağ geçidi, ISS) hesaplamak * 0,8.</span><span class="sxs-lookup"><span data-stu-id="c8919-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="c8919-124">Hesaplanan verimlilik, uygulamanızın temel üretilen iş gereksinimlerini karşılamıyorsa tooincrease hello bant genişliği hello performans sorunu tanımlanan hello kaynak gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8919-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="c8919-125">bir Azure VPN ağ geçidi tooresize bkz [bir ağ geçidi SKU'su değiştirme](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="c8919-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="c8919-126">bir sanal makine tooresize bkz [bir VM'yi yeniden boyutlandırın](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c8919-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="c8919-127">Beklenen Internet bant genişliği yaşıyorsanız değil, ISS toocontact da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8919-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="c8919-128">Performans araçları kullanarak ağ verimliliği doğrulama</span><span class="sxs-lookup"><span data-stu-id="c8919-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="c8919-129">Test sırasında VPN tüneli verimlilik Doygunluk doğru sonuçlar vermez gibi bu doğrulama yoğun olmayan saatlerde gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8919-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="c8919-130">Bu test için kullandığımız hello hem Windows hem de Linux üzerinde çalışır ve hem istemci hem de sunucu modları içeren iPerf aracıdır.</span><span class="sxs-lookup"><span data-stu-id="c8919-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="c8919-131">Windows VM'ler için sınırlı too3 Gbps olur.</span><span class="sxs-lookup"><span data-stu-id="c8919-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="c8919-132">Bu araç tüm okuma/yazma işlemleri toodisk gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="c8919-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="c8919-133">Bu yalnızca bir son toohello diğer kendinden oluşturulmuş TCP trafiği üretir.</span><span class="sxs-lookup"><span data-stu-id="c8919-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="c8919-134">İstemci ve sunucu düğümler arasında kullanılabilir bant hello ölçer deneme bağlı olarak istatistikleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c8919-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="c8919-135">İki düğüm arasında test edilirken bir hello sunucu ve istemci olarak diğer hello gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="c8919-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="c8919-136">Bu test tamamlandıktan sonra her ikisi de indirebileceğiniz ve her iki düğüm üzerinde üretilen işi hello rolleri tootest ters öneririz.</span><span class="sxs-lookup"><span data-stu-id="c8919-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="c8919-137">İPerf indirin</span><span class="sxs-lookup"><span data-stu-id="c8919-137">Download iPerf</span></span>
<span data-ttu-id="c8919-138">Karşıdan [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="c8919-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="c8919-139">Ayrıntılar için bkz [iPerf belgelerine](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="c8919-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="c8919-140">Bu makalede ele hello üçüncü taraf ürünler Microsoft'tan bağımsız şirketler tarafından üretilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c8919-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="c8919-141">Microsoft, zımni ya da aksi takdirde hello performans ya da bu ürünlerin hakkında hiçbir garanti vermez.</span><span class="sxs-lookup"><span data-stu-id="c8919-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="c8919-142">Çalışma iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="c8919-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="c8919-143">Merhaba trafiğinde (Azure VM sınama ortak IP adresi) izin veren bir NSG/ACL kuralı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c8919-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="c8919-144">Her iki düğüm üzerinde 5001 bağlantı noktası için güvenlik duvarı özel durumunu etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c8919-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="c8919-145">**Windows:** yönetici olarak çalıştır hello şu komutu:</span><span class="sxs-lookup"><span data-stu-id="c8919-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="c8919-146">test ederken tooremove hello kural bu komutu çalıştırmak, tamamlanır:</span><span class="sxs-lookup"><span data-stu-id="c8919-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="c8919-147">**Azure Linux:** Azure Linux görüntüleri olan izin veren güvenlik duvarları.</span><span class="sxs-lookup"><span data-stu-id="c8919-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="c8919-148">Bir bağlantı noktasını dinleyen bir uygulama olup olmadığını hello trafiğinin aracılığıyla izin verilir.</span><span class="sxs-lookup"><span data-stu-id="c8919-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="c8919-149">Güvenli hale getirilen özel resimler açıkça açılan bağlantı noktaları gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c8919-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="c8919-150">Ortak Linux işletim sistemi katmanlı güvenlik duvarları içeren `iptables`, `ufw`, veya `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="c8919-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="c8919-151">Merhaba sunucu düğümünde iperf3.exe ayıkladığınız toohello dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c8919-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="c8919-152">Ardından iPerf sunucu modunda çalıştırın ve toolisten 5001 bağlantı noktasında komutları aşağıdaki hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c8919-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="c8919-153">Merhaba istemci düğümde burada iperf aracı ayıkladığınız ve hello aşağıdaki komutu çalıştırın toohello dizini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c8919-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="c8919-154">Merhaba istemci bağlantı noktası 5001 toohello sunucuda trafiği 30 saniye inducing.</span><span class="sxs-lookup"><span data-stu-id="c8919-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="c8919-155">Merhaba bayrağı '-P ' 32 eşzamanlı bağlantı toohello sunucu düğümünü kullanarak size gösterir.</span><span class="sxs-lookup"><span data-stu-id="c8919-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="c8919-156">Merhaba aşağıdaki ekran bu örneğin hello çıktısını gösterir:</span><span class="sxs-lookup"><span data-stu-id="c8919-156">hello following screen shows hello output from this example:</span></span>

    ![Çıktı](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="c8919-158">(İsteğe bağlı) toopreserve hello sınama sonuçları, bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c8919-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="c8919-159">Merhaba sunucu düğümü şimdi hello istemci ve tam tersini böylece hello önceki adımları tamamladıktan sonra hello rolleri ile aynı adımları tersine, hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="c8919-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="c8919-160">Yavaş dosya kopyalama sorunlarını gidermek</span><span class="sxs-lookup"><span data-stu-id="c8919-160">Address slow file copy issues</span></span>
<span data-ttu-id="c8919-161">Windows Gezgini'ni kullanarak veya sürükleyip bir RDP oturumu aracılığıyla zaman kopyalamayı yavaş dosya karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8919-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="c8919-162">Bu sorun normalde tooone veya her ikisini Etkenler aşağıdaki hello oluşur:</span><span class="sxs-lookup"><span data-stu-id="c8919-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="c8919-163">Dosya kopyalama uygulamaları, Windows Gezgini ve RDP, gibi birden çok iş parçacığı dosya kopyalarken kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c8919-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="c8919-164">Çok iş parçacıklı dosya kopyalama uygulaması gibi daha iyi performans için kullandığınız [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy dosyaları 16 veya 32 iş parçacığı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c8919-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="c8919-165">toochange hello iş parçacığı numarasını Richcopy, dosya kopyalama için tıklatın **eylem** > **kopyalama seçenekleri** > **dosya kopyalama**.</span><span class="sxs-lookup"><span data-stu-id="c8919-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="c8919-166">
![Yavaş dosya kopyalama sorunları](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="c8919-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="c8919-167">Yetersiz VM disk okuma/yazma hızı.</span><span class="sxs-lookup"><span data-stu-id="c8919-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="c8919-168">Daha fazla bilgi için bkz: [Azure Storage sorunlarını giderme](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c8919-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="c8919-169">Şirket içi cihaz dış karşılıklı arabirimi</span><span class="sxs-lookup"><span data-stu-id="c8919-169">On-premises device external facing interface</span></span>
<span data-ttu-id="c8919-170">Merhaba içi bağlı VPN cihazı Internet'e yönelik IP adresi hello dahil değilse [yerel ağ](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) tanımı azure'da hello durumlarıyla VPN bağlantısını keser veya performans sorunları yaşamaktadır toobring karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8919-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="c8919-171">Gecikme olmadığı denetleniyor</span><span class="sxs-lookup"><span data-stu-id="c8919-171">Checking latency</span></span>
<span data-ttu-id="c8919-172">Atlama arasında 100 ms aşan gecikmeleri varsa tracert tootrace tooMicrosoft Azure kenar aygıt toodetermine kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8919-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="c8919-173">Merhaba şirket içi ağ üzerinden çalıştırılabilecek *tracert* toohello VIP hello Azure ağ geçidi ya da VM.</span><span class="sxs-lookup"><span data-stu-id="c8919-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="c8919-174">Yalnızca gördüğünüzde * döndürülen hello Azure kenar ulaştı, biliyor.</span><span class="sxs-lookup"><span data-stu-id="c8919-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="c8919-175">"Döndürülen MSN" içeren DNS adları gördüğünüzde hello Microsoft omurga ulaştınız bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8919-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="c8919-176">
![Gecikme olmadığı denetleniyor](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="c8919-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8919-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8919-177">Next steps</span></span>
<span data-ttu-id="c8919-178">Daha fazla bilgi veya Yardım için bağlantılar aşağıdaki hello denetleyin:</span><span class="sxs-lookup"><span data-stu-id="c8919-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="c8919-179">Azure sanal makineleri için ağ verimliliğini en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="c8919-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="c8919-180">Microsoft Destek</span><span class="sxs-lookup"><span data-stu-id="c8919-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
