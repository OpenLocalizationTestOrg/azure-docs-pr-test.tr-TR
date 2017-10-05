---
title: "Bir Microsoft Azure sanal ağı için VPN verimlilik doğrulama | Microsoft Docs"
description: "Bu belgenin amacı, bir kullanıcı, şirket içi kaynakları ağ akışından bir Azure sanal makinesi için doğrulama yardımcı olmaktır."
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
ms.openlocfilehash: 2e0347854b5d30c955a50a01d6f7ba08e24f94b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-validate-vpn-throughput-to-a-virtual-network"></a><span data-ttu-id="0b7bd-103">Nasıl bir sanal ağ VPN verimlilik doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="0b7bd-103">How to validate VPN throughput to a virtual network</span></span>

<span data-ttu-id="0b7bd-104">Bir VPN gateway bağlantısı güvenli kurmanızı sağlar, sanal ağınızı Azure içinde ve şirket içi arasında bağlantı şirket içi BT altyapısı.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-104">A VPN gateway connection enables you to establish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="0b7bd-105">Bu makalede, Azure sanal makinesi için ağ verimini şirket içi kaynaklardan doğrulamak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-105">This article shows how to validate network throughput from the on-premises resources to an Azure virtual machine.</span></span> <span data-ttu-id="0b7bd-106">Ayrıca, sorun giderme kılavuzu sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="0b7bd-107">Bu makale, tanılamanıza ve sık karşılaşılan sorunları gidermenize yardımcı olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-107">This article is intended to help diagnose and fix common issues.</span></span> <span data-ttu-id="0b7bd-108">Aşağıdaki bilgileri kullanarak sorunu çözmek yapamıyorsanız [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="0b7bd-108">If you're unable to solve the issue by using the following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="0b7bd-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0b7bd-109">Overview</span></span>

<span data-ttu-id="0b7bd-110">VPN ağ geçidi bağlantısı aşağıdaki bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="0b7bd-110">The VPN gateway connection involves the following components:</span></span>

- <span data-ttu-id="0b7bd-111">Şirket içi VPN cihazı (bir listesini görüntülemek [doğrulanan VPN cihazları)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="0b7bd-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="0b7bd-112">Genel Internet</span><span class="sxs-lookup"><span data-stu-id="0b7bd-112">Public Internet</span></span>
- <span data-ttu-id="0b7bd-113">Azure VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="0b7bd-113">Azure VPN gateway</span></span>
- <span data-ttu-id="0b7bd-114">Azure sanal makinesi</span><span class="sxs-lookup"><span data-stu-id="0b7bd-114">Azure virtual machine</span></span>

<span data-ttu-id="0b7bd-115">Aşağıdaki diyagramda bir şirket içi ağ VPN aracılığıyla Azure sanal ağını mantıksal bağlantısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-115">The following diagram shows the logical connectivity of an on-premises network to an Azure virtual network through VPN.</span></span>

![Mantıksal bağlantı, müşteri ağa MSFT VPN kullanarak ağ](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-the-maximum-expected-ingressegress"></a><span data-ttu-id="0b7bd-117">En fazla beklenen giriş/çıkış Hesapla</span><span class="sxs-lookup"><span data-stu-id="0b7bd-117">Calculate the maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="0b7bd-118">Uygulamanızın temel üretilen iş gereksinimlerini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="0b7bd-119">Azure VPN ağ geçidi işleme sınırları belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="0b7bd-120">Yardım için "SKU ve VPN türüne göre toplam verimliliği" bölümüne bakın [planlama ve tasarım VPN ağ geçidi için](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="0b7bd-120">For help, see the "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="0b7bd-121">Belirlemek [Azure VM verimlilik Kılavuzu](../virtual-machines/virtual-machines-windows-sizes.md) VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-121">Determine the [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="0b7bd-122">Internet servis sağlayıcısı (ISS) bant genişliğiniz belirler.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="0b7bd-123">Beklenen Verimlilik - en az bant genişliği (VM, ağ geçidi, ISS) hesaplamak * 0,8.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="0b7bd-124">Hesaplanan verimlilik, uygulamanızın temel üretilen iş gereksinimlerini karşılamıyorsa, bant genişliği performans sorunu tanımlanan kaynağın artırmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need to increase the bandwidth of the resource that you identified as the bottleneck.</span></span> <span data-ttu-id="0b7bd-125">Bir Azure VPN ağ geçidi yeniden boyutlandırmak için bkz: [bir ağ geçidi SKU'su değiştirme](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="0b7bd-125">To resize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="0b7bd-126">Bir sanal makine yeniden boyutlandırmak için bkz: [bir VM'yi yeniden boyutlandırın](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="0b7bd-126">To resize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="0b7bd-127">Beklenen Internet bant genişliği yaşıyorsanız değil, ISS'ye başvurun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-127">If you are not experiencing expected Internet bandwidth, you may also want to contact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="0b7bd-128">Performans araçları kullanarak ağ verimliliği doğrulama</span><span class="sxs-lookup"><span data-stu-id="0b7bd-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="0b7bd-129">Test sırasında VPN tüneli verimlilik Doygunluk doğru sonuçlar vermez gibi bu doğrulama yoğun olmayan saatlerde gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="0b7bd-130">Bu test için kullandığımız hem Windows hem de Linux üzerinde çalışır ve hem istemci hem de sunucu modları içeren iPerf aracıdır.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-130">The tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="0b7bd-131">3 GB/sn için Windows VM için sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-131">It is limited to 3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="0b7bd-132">Bu araç, disk okuma/yazma işlemleri gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-132">This tool does not perform any read/write operations to disk.</span></span> <span data-ttu-id="0b7bd-133">Bu yalnızca bir ucu kendinden oluşturulmuş TCP trafiği diğer üretir.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-133">It solely produces self-generated TCP traffic from one end to the other.</span></span> <span data-ttu-id="0b7bd-134">İstemci ve sunucu düğümler arasında kullanılabilir bant genişliğini ölçer deneme bağlı olarak istatistikleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-134">It generated statistics based on experimentation that measures the bandwidth available between client and server nodes.</span></span> <span data-ttu-id="0b7bd-135">İki düğüm arasında test edilirken bir sunucunun ve diğer istemci olarak görür.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-135">When testing between two nodes, one acts as the server and the other as a client.</span></span> <span data-ttu-id="0b7bd-136">Bu test tamamlandıktan sonra her iki karşıya yükleme test ve her iki düğüm üzerinde üretilen işi indirmek için rolleri ters öneririz.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-136">Once this test is completed, we recommend that you reverse the roles to test both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="0b7bd-137">İPerf indirin</span><span class="sxs-lookup"><span data-stu-id="0b7bd-137">Download iPerf</span></span>
<span data-ttu-id="0b7bd-138">Karşıdan [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="0b7bd-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="0b7bd-139">Ayrıntılar için bkz [iPerf belgelerine](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="0b7bd-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="0b7bd-140">Bu makalede ele alınan üçüncü taraf ürünler Microsoft'tan bağımsız şirketler tarafından üretilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-140">The third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="0b7bd-141">Microsoft, zımni ya da aksi takdirde performans veya bu ürünlerin hakkında hiçbir garanti vermez.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-141">Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="0b7bd-142">Çalışma iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="0b7bd-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="0b7bd-143">(Azure VM sınama ortak IP adresi için) trafiğe izin bir NSG/ACL kuralını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-143">Enable an NSG/ACL rule allowing the traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="0b7bd-144">Her iki düğüm üzerinde 5001 bağlantı noktası için güvenlik duvarı özel durumunu etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="0b7bd-145">**Windows:** yönetici olarak aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0b7bd-145">**Windows:** Run the following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="0b7bd-146">Test ederken kuralı kaldırmak için bu komutu çalıştırmak, tamamlanır:</span><span class="sxs-lookup"><span data-stu-id="0b7bd-146">To remove the rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="0b7bd-147">**Azure Linux:** Azure Linux görüntüleri olan izin veren güvenlik duvarları.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="0b7bd-148">Bir bağlantı noktasını dinleyen bir uygulama olduğunda trafiği aracılığıyla izin verilir.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-148">If there is an application listening on a port, the traffic is allowed through.</span></span> <span data-ttu-id="0b7bd-149">Güvenli hale getirilen özel resimler açıkça açılan bağlantı noktaları gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="0b7bd-150">Ortak Linux işletim sistemi katmanlı güvenlik duvarları içeren `iptables`, `ufw`, veya `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="0b7bd-151">Sunucu düğümünde iperf3.exe ayıkladığınız dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-151">On the server node, change to the directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="0b7bd-152">Ardından iPerf sunucu modunda çalıştırın ve aşağıdaki komutları olarak 5001 bağlantı noktasında dinleyecek şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="0b7bd-152">Then run iPerf in server mode and set it to listen on port 5001 as the following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="0b7bd-153">İstemci düğümde burada iperf aracı ayıkladığınız ve aşağıdaki komutu çalıştırın dizinine değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0b7bd-153">On the client node, change to the directory where iperf tool is extracted and then run the following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of the iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="0b7bd-154">İstemci sunucuya 5001 numaralı bağlantı noktasında trafik 30 saniye inducing.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-154">The client is inducing traffic on port 5001 to the server for 30 seconds.</span></span> <span data-ttu-id="0b7bd-155">Bayrağı '-P ' belirten 32 eşzamanlı bağlantıların sunucu düğümünü kullanarak biz.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-155">The flag '-P ' that indicates we are using 32 simultaneous connections to the server node.</span></span>

    <span data-ttu-id="0b7bd-156">Aşağıdaki ekran bu örneğin çıktısını gösterir:</span><span class="sxs-lookup"><span data-stu-id="0b7bd-156">The following screen shows the output from this example:</span></span>

    ![Çıktı](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="0b7bd-158">(İSTEĞE BAĞLI) Test sonuçlarını korumak için bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0b7bd-158">(OPTIONAL) To preserve the testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="0b7bd-159">Sunucu düğümü şimdi istemci ve tam tersini olmayacaktır önceki adımları tamamladıktan sonra tersine, rolleri ile aynı adımları yürütün.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-159">After completing the previous steps, execute the same steps with the roles reversed, so that the server node will now be the client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="0b7bd-160">Yavaş dosya kopyalama sorunlarını gidermek</span><span class="sxs-lookup"><span data-stu-id="0b7bd-160">Address slow file copy issues</span></span>
<span data-ttu-id="0b7bd-161">Windows Gezgini'ni kullanarak veya sürükleyip bir RDP oturumu aracılığıyla zaman kopyalamayı yavaş dosya karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="0b7bd-162">Bu sorun, normalde birini veya her ikisini aşağıdaki etmenlere nedeniyle oluşur:</span><span class="sxs-lookup"><span data-stu-id="0b7bd-162">This problem is normally due to one or both of the following factors:</span></span>

- <span data-ttu-id="0b7bd-163">Dosya kopyalama uygulamaları, Windows Gezgini ve RDP, gibi birden çok iş parçacığı dosya kopyalarken kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="0b7bd-164">Çok iş parçacıklı dosya kopyalama uygulaması gibi daha iyi performans için kullandığınız [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) 16 veya 32 iş parçacığı kullanarak dosyaları kopyalamak için.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) to copy files by using 16 or 32 threads.</span></span> <span data-ttu-id="0b7bd-165">Dosya kopyalama Richcopy içindeki iş parçacığı sayısını değiştirmek için tıklatın **eylem** > **kopyalama seçenekleri** > **dosya kopyalama**.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-165">To change the thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="0b7bd-166">
![Yavaş dosya kopyalama sorunları](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="0b7bd-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="0b7bd-167">Yetersiz VM disk okuma/yazma hızı.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="0b7bd-168">Daha fazla bilgi için bkz: [Azure Storage sorunlarını giderme](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0b7bd-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="0b7bd-169">Şirket içi cihaz dış karşılıklı arabirimi</span><span class="sxs-lookup"><span data-stu-id="0b7bd-169">On-premises device external facing interface</span></span>
<span data-ttu-id="0b7bd-170">Şirket içi VPN cihazı Internet'e yönelik IP adresini de dahil edilmişse [yerel ağ](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) Azure tanımında durumlarıyla VPN bağlantısını keser yukarı getirmek için bağlanamama ya da performans sorunları yaşayabilir.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-170">If the on-premises VPN device Internet-facing IP address is included in the [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability to bring up the VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="0b7bd-171">Gecikme olmadığı denetleniyor</span><span class="sxs-lookup"><span data-stu-id="0b7bd-171">Checking latency</span></span>
<span data-ttu-id="0b7bd-172">Microsoft Azure sınır cihazı izlemek için tracert atlama arasında 100 ms aşan gecikmeleri olup olmadığını belirlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-172">Use tracert to trace to Microsoft Azure Edge device to determine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="0b7bd-173">Şirket içi ağ üzerinden çalıştırılabilecek *tracert* Azure ağ geçidi veya VM VIP için.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-173">From the on-premises network, run *tracert* to the VIP of the Azure Gateway or VM.</span></span> <span data-ttu-id="0b7bd-174">Yalnızca gördüğünüzde * döndürdü, Azure kenar ulaştı, biliyor.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-174">Once you see only * returned, you know you have reached the Azure edge.</span></span> <span data-ttu-id="0b7bd-175">"Döndürülen MSN" içeren DNS adları gördüğünüzde Microsoft omurga ulaştınız bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b7bd-175">When you see DNS names that include "MSN" returned, you know you have reached the Microsoft backbone.</span></span><br><br><span data-ttu-id="0b7bd-176">
![Gecikme olmadığı denetleniyor](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="0b7bd-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b7bd-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0b7bd-177">Next steps</span></span>
<span data-ttu-id="0b7bd-178">Daha fazla bilgi veya Yardım için aşağıdaki bağlantıları kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="0b7bd-178">For more information or help, check out the following links:</span></span>

- [<span data-ttu-id="0b7bd-179">Azure sanal makineleri için ağ verimliliğini en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="0b7bd-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="0b7bd-180">Microsoft Destek</span><span class="sxs-lookup"><span data-stu-id="0b7bd-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
