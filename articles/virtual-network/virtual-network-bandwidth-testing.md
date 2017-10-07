---
title: "aaaTesting Azure VM ağ verimliliği | Microsoft Docs"
description: "Nasıl tootest Azure sanal makine ağ verimliliği öğrenin."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="f4d63-103">Bant genişliği/işleme (NTTTCP) test etme</span><span class="sxs-lookup"><span data-stu-id="f4d63-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="f4d63-104">Azure'da ağ verimliliği performansından test ederken, en iyi toouse test hello ağ hedefler ve performansı etkileyen diğer kaynakları hello kullanımını en aza indirir bir araç olan.</span><span class="sxs-lookup"><span data-stu-id="f4d63-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="f4d63-105">NTTTCP önerilir.</span><span class="sxs-lookup"><span data-stu-id="f4d63-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="f4d63-106">Merhaba aracı tootwo hello Azure Vm'leri kopyalamak aynı boyutta.</span><span class="sxs-lookup"><span data-stu-id="f4d63-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="f4d63-107">Bir VM GÖNDERENİ ve ALICISI olarak diğer hello görür.</span><span class="sxs-lookup"><span data-stu-id="f4d63-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="f4d63-108">Test etmek için sanal makineleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="f4d63-108">Deploying VMs for testing</span></span>
<span data-ttu-id="f4d63-109">Bu test amacıyla Merhaba, iki VM bulunmalıdır hello aynı bulut hizmetine hello ya da aynı kullanılabilirlik kümesi, böylece biz kendi iç IP'leri kullanın ve hello yük dengeleyici hello testten hariç hello.</span><span class="sxs-lookup"><span data-stu-id="f4d63-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="f4d63-110">Merhaba VIP ile olası tootest, ancak bu tür sınama hello bu belgenin kapsamı dışında gelir.</span><span class="sxs-lookup"><span data-stu-id="f4d63-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="f4d63-111">Merhaba ALICININ IP adresini not edin.</span><span class="sxs-lookup"><span data-stu-id="f4d63-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="f4d63-112">Şimdi bu IP "a.b.c.r" çağırın</span><span class="sxs-lookup"><span data-stu-id="f4d63-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="f4d63-113">Merhaba VM üzerinde hello çekirdek sayısı not edin.</span><span class="sxs-lookup"><span data-stu-id="f4d63-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="f4d63-114">Şimdi bu çağırın "\#num\_çekirdek"</span><span class="sxs-lookup"><span data-stu-id="f4d63-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="f4d63-115">Hello NTTTCP 300 saniye (veya 5 dakika) test VM hello gönderici ve alıcı VM çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f4d63-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="f4d63-116">İpucu: Bu test hello için ilk kez ayarlarken, daha kısa bir test dönemi tooget geri bildirim er deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4d63-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="f4d63-117">Merhaba aracı beklendiği gibi çalıştığını sonra hello test dönemi too300 saniye hello en doğru sonuçlar için genişletir.</span><span class="sxs-lookup"><span data-stu-id="f4d63-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="f4d63-118">Merhaba gönderen **ve** alıcı belirtmelisiniz **aynı hello** süresi parametresi test (-t).</span><span class="sxs-lookup"><span data-stu-id="f4d63-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="f4d63-119">10 saniye için tek bir TCP akış tootest:</span><span class="sxs-lookup"><span data-stu-id="f4d63-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="f4d63-120">Alıcı parametreleri: ntttcp - r -t 10 - P 1</span><span class="sxs-lookup"><span data-stu-id="f4d63-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="f4d63-121">Gönderen parametreleri: ntttcp-s10.27.33.7 -t 10 - n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="f4d63-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="f4d63-122">Örnek önceki hello kullanılan tooconfirm yapılandırmanızı yalnızca olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f4d63-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="f4d63-123">Sınama geçerli örnekleri bu belgenin sonraki bölümlerinde ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f4d63-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="f4d63-124">WINDOWS çalıştıran VM'ler sınama:</span><span class="sxs-lookup"><span data-stu-id="f4d63-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="f4d63-125">NTTTCP VM'ler hello alın.</span><span class="sxs-lookup"><span data-stu-id="f4d63-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="f4d63-126">Merhaba en son sürümünü indirin: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="f4d63-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="f4d63-127">Ya da onu taşınsa arayın: <https://www.bing.com/search?q=ntttcp+download> \< --ilk isabet</span><span class="sxs-lookup"><span data-stu-id="f4d63-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="f4d63-128">C: gibi ayrı bir klasör içinde NTTTCP yerleştirmeyi düşünün\\araçları</span><span class="sxs-lookup"><span data-stu-id="f4d63-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="f4d63-129">NTTTCP hello Windows Güvenlik Duvarı aracılığıyla izin ver</span><span class="sxs-lookup"><span data-stu-id="f4d63-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="f4d63-130">Hello alıcı, NTTTCP trafiği tooarrive hello Windows Güvenlik Duvarı tooallow üzerinde izin verme kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4d63-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="f4d63-131">Tooallow belirli TCP bağlantı noktalarını gelen yerine onu kolay tooallow hello tüm NTTTCP ada göre programdır.</span><span class="sxs-lookup"><span data-stu-id="f4d63-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="f4d63-132">Bu gibi hello Windows Güvenlik Duvarı aracılığıyla ntttcp izin ver:</span><span class="sxs-lookup"><span data-stu-id="f4d63-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="f4d63-133">Netsh advfirewall güvenlik duvarı kuralı program Ekle =\<yolu\>\\ntttcp.exe adı "ntttcp" protocol = tüm dir = Action = etkinleştir izin yes profile = = ANY</span><span class="sxs-lookup"><span data-stu-id="f4d63-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="f4d63-134">Örneğin, ntttcp.exe toohello kopyaladıysanız "c:\\Araçları" klasörü, bu hello komutu olacaktır:</span><span class="sxs-lookup"><span data-stu-id="f4d63-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="f4d63-135">Netsh advfirewall güvenlik duvarı kuralı program Ekle = c:\\Araçları\\ntttcp.exe adı "ntttcp" protocol = tüm dir = eylemde = = etkinleştir izin yes profile = = ANY</span><span class="sxs-lookup"><span data-stu-id="f4d63-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="f4d63-136">NTTTCP testlerini çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f4d63-136">Running NTTTCP tests</span></span>

<span data-ttu-id="f4d63-137">Alıcı hello üzerinde NTTTCP Başlat (**CMD'den çalıştırmak**PowerShell dosyalardan değil):</span><span class="sxs-lookup"><span data-stu-id="f4d63-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="f4d63-138">ntttcp - r – m [2\*\#num\_çekirdek],\*, a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="f4d63-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="f4d63-139">Merhaba VM dört çekirdek ve 10.0.0.4 IP adresi varsa, onu şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="f4d63-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="f4d63-140">ntttcp - r – m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="f4d63-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="f4d63-141">GÖNDEREN hello üzerinde NTTTCP Başlat (**CMD'den çalıştırmak**PowerShell dosyalardan değil):</span><span class="sxs-lookup"><span data-stu-id="f4d63-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="f4d63-142">ntttcp -s-m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="f4d63-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="f4d63-143">Merhaba sonuçları için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="f4d63-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="f4d63-144">LINUX çalıştıran Vm'leri sınama:</span><span class="sxs-lookup"><span data-stu-id="f4d63-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="f4d63-145">Linux için nttcp kullanın.</span><span class="sxs-lookup"><span data-stu-id="f4d63-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="f4d63-146">Kullanılabilir <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="f4d63-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="f4d63-147">Hello Linux VM'ler (GÖNDERENİ ve ALICISI), ntttcp için linux Vm'lerinizi üzerinde hazırlamak için şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f4d63-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="f4d63-148">CentOS - yükleme Git:</span><span class="sxs-lookup"><span data-stu-id="f4d63-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="f4d63-149">Ubuntu - yükleme Git:</span><span class="sxs-lookup"><span data-stu-id="f4d63-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="f4d63-150">Olun ve hem de yükleyin:</span><span class="sxs-lookup"><span data-stu-id="f4d63-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="f4d63-151">Merhaba Windows örnekteki biz hello Linux ALICININ IP 10.0.0.4 olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="f4d63-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="f4d63-152">Linux için NTTTCP alıcı hello üzerinde başlatın:</span><span class="sxs-lookup"><span data-stu-id="f4d63-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="f4d63-153">Ve hello gönderen, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f4d63-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="f4d63-154">Test uzunluğu Varsayılanları too60 saniye hiçbir zaman parametresi, verilen</span><span class="sxs-lookup"><span data-stu-id="f4d63-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="f4d63-155">Windows ve LINUX çalıştıran VM'ler arasında sınama:</span><span class="sxs-lookup"><span data-stu-id="f4d63-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="f4d63-156">Merhaba test çalıştırabilmeniz için bu senaryoları biz hello eşitlemesi modu etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4d63-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="f4d63-157">Bu hello kullanarak yapılır **-N bayrağı** Linux için ve **-ns bayrağı** Windows için.</span><span class="sxs-lookup"><span data-stu-id="f4d63-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="f4d63-158">Linux tooWindows:</span><span class="sxs-lookup"><span data-stu-id="f4d63-158">From Linux tooWindows:</span></span>

<span data-ttu-id="f4d63-159">Alıcı <Windows>:</span><span class="sxs-lookup"><span data-stu-id="f4d63-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="f4d63-160">Gönderen <Linux> :</span><span class="sxs-lookup"><span data-stu-id="f4d63-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="f4d63-161">Windows tooLinux:</span><span class="sxs-lookup"><span data-stu-id="f4d63-161">From Windows tooLinux:</span></span>

<span data-ttu-id="f4d63-162">Alıcı <Linux>:</span><span class="sxs-lookup"><span data-stu-id="f4d63-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="f4d63-163">Gönderen <Windows>:</span><span class="sxs-lookup"><span data-stu-id="f4d63-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="f4d63-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f4d63-164">Next steps</span></span>
* <span data-ttu-id="f4d63-165">Sonuçlar bağlı olarak, olabilir oda çok[ağ verimliliği makineler en iyi duruma getirme](virtual-network-optimize-network-bandwidth.md) senaryonuz için.</span><span class="sxs-lookup"><span data-stu-id="f4d63-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="f4d63-166">Daha fazla bilgi edinin [Azure Virtual Network sık sorulan sorular (SSS)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="f4d63-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
