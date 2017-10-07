---
title: "Azure Ağ İzleyicisi ile aaaPacket denetleme | Microsoft Docs"
description: "Bir sanal makineden toouse Ağ İzleyicisi tooperform derin paket incelemesi nasıl toplanan bu makalede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="104c2-103">Azure Ağ İzleyicisi ile paket incelemesi</span><span class="sxs-lookup"><span data-stu-id="104c2-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="104c2-104">Ağ İzleyicisi Merhaba paket yakalama özelliğini kullanarak, Azure Vm'leriniz hello portalı, PowerShell CLI ve hello SDK aracılığıyla programlı olarak ve REST API yakalamaları oturumlarını yönetmesine ve başlatın.</span><span class="sxs-lookup"><span data-stu-id="104c2-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="104c2-105">Paket yakalama, paket düzeyinde veri kullanılabilir biçiminde hello bilgileri sağlayarak gerektiren tooaddress senaryolar sağlar.</span><span class="sxs-lookup"><span data-stu-id="104c2-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="104c2-106">Ücretsiz Araçlar tooinspect hello veri yararlanarak, Vm'leriniz iletişimler tooand inceleyin ve ağ trafiğinizi alın.</span><span class="sxs-lookup"><span data-stu-id="104c2-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="104c2-107">Paket yakalama veri bazı örnek kullanımları şunlardır: ağ veya uygulama sorunları incelemeye, ağ kötüye ve yetkisiz erişim girişimlerini algılama veya Mevzuat uyumluluğu bakımını yapma.</span><span class="sxs-lookup"><span data-stu-id="104c2-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="104c2-108">Bu makalede, nasıl tooopen bir paket yakalama dosyasını Ağ İzleyicisi tarafından popüler açık kaynak aracını kullanarak sağlanan gösterir.</span><span class="sxs-lookup"><span data-stu-id="104c2-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="104c2-109">Biz de nasıl toocalculate bağlantı gecikmesi anormal trafiği tanımlamak ve ağ istatistikleri inceleyin gösteren örnekler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="104c2-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="104c2-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="104c2-110">Before you begin</span></span>

<span data-ttu-id="104c2-111">Bu makalede önceden çalıştırılmış olan bir paket yakalama önceden yapılandırılmış bazı senaryolar üzerinden gider.</span><span class="sxs-lookup"><span data-stu-id="104c2-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="104c2-112">Bu senaryolar, bir paket yakalama gözden geçirerek erişilebilir özellikleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="104c2-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="104c2-113">Bu senaryo kullanır [WireShark](https://www.wireshark.org/) tooinspect hello paket yakalama.</span><span class="sxs-lookup"><span data-stu-id="104c2-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="104c2-114">Bu senaryo, bir sanal makinede bir paket yakalama zaten başlattıysanız varsayar.</span><span class="sxs-lookup"><span data-stu-id="104c2-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="104c2-115">nasıl toocreate paket yakalama ziyaret toolearn [Yönet paket yakalar hello portalıyla](network-watcher-packet-capture-manage-portal.md) veya REST şu adresi ziyaret ederek ile [REST API ile paket yakalar yönetme](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="104c2-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="104c2-116">Senaryo</span><span class="sxs-lookup"><span data-stu-id="104c2-116">Scenario</span></span>

<span data-ttu-id="104c2-117">Bu senaryoda:</span><span class="sxs-lookup"><span data-stu-id="104c2-117">In this scenario, you:</span></span>

* <span data-ttu-id="104c2-118">Paket yakalama gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="104c2-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="104c2-119">Ağ gecikmesi Hesapla</span><span class="sxs-lookup"><span data-stu-id="104c2-119">Calculate network latency</span></span>

<span data-ttu-id="104c2-120">Bu senaryoda, nasıl tooview hello iki uç noktaları arasında gerçekleşen İletim Denetimi Protokolü (TCP) konuşmanın ilk gidiş dönüş süresi (RTT) gösterir.</span><span class="sxs-lookup"><span data-stu-id="104c2-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="104c2-121">Bir TCP bağlantı kurulduğunda hello hello bağlantısında gönderilen ilk üç paketleri bir yaygın olarak ifade deseni tooas hello üç yönlü anlaşması izleyin.</span><span class="sxs-lookup"><span data-stu-id="104c2-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="104c2-122">Bu bağlantı oluşturulduğunda bu anlaşma, bir ilk isteği hello istemciden ve hello sunucusundan yanıt gönderilen hello ilk iki paket inceleyerek, biz hello gecikme hesaplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="104c2-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="104c2-123">Bu gecikme başvurulan tooas hello gidiş dönüş süresi (RTT) olur.</span><span class="sxs-lookup"><span data-stu-id="104c2-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="104c2-124">Merhaba TCP protokolü ve hello üç yönlü el sıkışma hakkında daha fazla bilgi için kaynak aşağıdaki toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="104c2-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="104c2-125">https://support.microsoft.com/en-US/Help/172983/Explanation-of-the-three-Way-Handshake-via-TCP-ip</span><span class="sxs-lookup"><span data-stu-id="104c2-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="104c2-126">1. Adım</span><span class="sxs-lookup"><span data-stu-id="104c2-126">Step 1</span></span>

<span data-ttu-id="104c2-127">WireShark başlatma</span><span class="sxs-lookup"><span data-stu-id="104c2-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="104c2-128">2. Adım</span><span class="sxs-lookup"><span data-stu-id="104c2-128">Step 2</span></span>

<span data-ttu-id="104c2-129">Yük hello **.cap** paket yakalama dosyasından.</span><span class="sxs-lookup"><span data-stu-id="104c2-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="104c2-130">Bu dosya, yerel olarak üzerinde hello sanal makine içinde kaydedildi hello blob bulunabilir nasıl yapılandırdığınıza bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="104c2-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="104c2-131">3. Adım</span><span class="sxs-lookup"><span data-stu-id="104c2-131">Step 3</span></span>

<span data-ttu-id="104c2-132">tooview Merhaba'TCP konuşmalarında ilk gidiş dönüş süresi (RTT), biz Karşılama ilk iki paketleri hello TCP anlaşması söz konusu adresindeki yalnızca arayacaktır.</span><span class="sxs-lookup"><span data-stu-id="104c2-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="104c2-133">Biz hello [Eşitlemeye] olan hello ilk iki paketlerinde hello üç yönlü el sıkışması, kullanacağınız [Eşitlemeye, ACK] paketler.</span><span class="sxs-lookup"><span data-stu-id="104c2-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="104c2-134">Merhaba TCP üstbilgisinde ayarlanan bayraklarının adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="104c2-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="104c2-135">Merhaba son hello el sıkışması, hello [ACK] paket pakette bu senaryoda kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="104c2-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="104c2-136">Merhaba [Eşitlemeye] paket hello istemci tarafından gönderilir.</span><span class="sxs-lookup"><span data-stu-id="104c2-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="104c2-137">Alındıktan sonra hello sunucu hello [ACK] paket hello Eşitlemeye hello istemciden alma, bir bildirim olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="104c2-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="104c2-138">Merhaba sunucu yanıtı çok az ek yük gerektirir hello olgu yararlanarak, biz hello [Eşitlemeye, ACK] paket hello zaman [Eşitlemeye] paket hello istemci tarafından alındı hello zaman çıkarılmasıyla tarafından RTT hello istemci tarafından gönderilen hello hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="104c2-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="104c2-139">WireShark kullanarak bu değeri bize hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="104c2-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="104c2-140">WireShark tarafından sağlanan yetenek filtreleme hello yararlanacak olan, toomore hello TCP üç yönlü anlaşması kolayca Karşılama ilk iki paketleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="104c2-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="104c2-141">tooapply hello WireShark, filtrede Merhaba, yakalama [Eşitlemeye] pakette "İletim Denetimi Protokolü" bölümünü genişletin ve hello TCP üstbilgisinde ayarlanan hello bayrakları inceleyin.</span><span class="sxs-lookup"><span data-stu-id="104c2-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="104c2-142">Tüm [Eşitlemeye] üzerinde toofilter arıyoruz beri ve [Eşitlemeye, ACK] bayrakları altında paketleri cofirm hello eşitlemeye bit too1 ayarlayın, sonra sağ tıklayarak hello eşitlemeye bit Filtre -> olarak seçili Uygula ->.</span><span class="sxs-lookup"><span data-stu-id="104c2-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![Şekil 7][7]

### <a name="step-4"></a><span data-ttu-id="104c2-144">4. Adım</span><span class="sxs-lookup"><span data-stu-id="104c2-144">Step 4</span></span>

<span data-ttu-id="104c2-145">Karşılama penceresi tooonly bakın paketleri ile filtrelenmiş göre hello [Eşitlemeye] biti ayarlanmamış, kolayca tooview ilginizi görüşmeleri hello ilk RTT.</span><span class="sxs-lookup"><span data-stu-id="104c2-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="104c2-146">Basit bir yol tooview hello WireShark RTT tıklamanız yeterlidir "SEQ/ACK" analiz işaretlenmiş hello açılır.</span><span class="sxs-lookup"><span data-stu-id="104c2-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="104c2-147">Ardından RTT görüntülenen hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="104c2-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="104c2-148">Bu durumda, hello RTT 0.0022114 saniye ya da 2.211 ms idi.</span><span class="sxs-lookup"><span data-stu-id="104c2-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![Şekil 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="104c2-150">İstenmeyen protokolleri</span><span class="sxs-lookup"><span data-stu-id="104c2-150">Unwanted protocols</span></span>

<span data-ttu-id="104c2-151">Azure üzerinde dağıtılan sanal makine örneği üzerinde çalışan birçok uygulamalar olabilir.</span><span class="sxs-lookup"><span data-stu-id="104c2-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="104c2-152">Bu uygulamaları birçoğu, belki de açık izniniz olmadan hello ağ üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="104c2-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="104c2-153">Paket yakalama toostore ağ iletişimi kullanarak, biz nasıl uygulama hello ağda varsayılır ve herhangi bir sorun için Ara araştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="104c2-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="104c2-154">Bu örnekte, sizi bir önceki gözden makinenizde çalışan bir uygulama yetkisiz iletişimi gösterebilir istenmeyen protokoller için paket yakalama çalıştı.</span><span class="sxs-lookup"><span data-stu-id="104c2-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="104c2-155">1. Adım</span><span class="sxs-lookup"><span data-stu-id="104c2-155">Step 1</span></span>

<span data-ttu-id="104c2-156">Merhaba hello önceki senaryo tıklatın aynı yakalama kullanarak **istatistikleri** > **Protokolü hiyerarşisi**</span><span class="sxs-lookup"><span data-stu-id="104c2-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![protokol hiyerarşi menüsü][2]

<span data-ttu-id="104c2-158">Merhaba Protokolü hiyerarşisi penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="104c2-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="104c2-159">Bu görünüm hello yakalama oturumu ve aktarılan ve hello protokolleri kullanılarak alınan paket sayısı hello sırasında kullanımda olan tüm hello protokollerin bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="104c2-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="104c2-160">Bu görünüm, sanal makine ya da ağ üzerindeki istenmeyen ağ trafiğini bulmak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="104c2-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![açılan iletişim kuralı hiyerarşisini][3]

<span data-ttu-id="104c2-162">Ekran yakalama aşağıdaki hello gördüğünüz eş toopeer dosya paylaşımı için kullanılan hello BitTorrent protokolünü kullanarak trafiği vardı.</span><span class="sxs-lookup"><span data-stu-id="104c2-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="104c2-163">Yönetici olarak toosee BitTorrent trafik bu belirli sanal makinelere beklediğiniz değil.</span><span class="sxs-lookup"><span data-stu-id="104c2-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="104c2-164">Şimdi, bu trafiğin kullanan, bu sanal makine ya da blok hello üzerinde yüklü hello eş toopeer yazılım kaldırabilirsiniz ağ güvenlik grupları veya bir Güvenlik Duvarı'nı kullanarak trafiği.</span><span class="sxs-lookup"><span data-stu-id="104c2-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="104c2-165">Ayrıca, hello protokolü kullanmak, sanal makinelere düzenli olarak gözden geçirebilirsiniz şekilde toorun paket yakalamaları bir zamanlamaya göre tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="104c2-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="104c2-166">Bir örneğin nasıl tooautomate ağ azure ziyaret edin görevler üzerinde [izlemek azure automation ile ağ kaynakları](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="104c2-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="104c2-167">En çok kullanılan hedefler ve bağlantı noktalarını bulma</span><span class="sxs-lookup"><span data-stu-id="104c2-167">Finding top destinations and ports</span></span>

<span data-ttu-id="104c2-168">Merhaba trafik türlerini anlama, uç noktaları hello ve hello bağlantı noktaları üzerinden iletişim önemlidir bir izleme veya uygulamaları ve ağınızdaki kaynaklara sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="104c2-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="104c2-169">Paket yakalama dosyası üstten yararlanarak, biz bizim VM ile iletişim kurduğu ve kullanılan bağlantı noktaları hello hello üst hedefleri hızlı bir şekilde öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="104c2-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="104c2-170">1. Adım</span><span class="sxs-lookup"><span data-stu-id="104c2-170">Step 1</span></span>

<span data-ttu-id="104c2-171">Merhaba hello önceki senaryo tıklatın aynı yakalama kullanarak **istatistikleri** > **IPv4 istatistikleri** > **hedefleri ve bağlantı noktaları**</span><span class="sxs-lookup"><span data-stu-id="104c2-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![Paket yakalama penceresi][4]

### <a name="step-2"></a><span data-ttu-id="104c2-173">2. Adım</span><span class="sxs-lookup"><span data-stu-id="104c2-173">Step 2</span></span>

<span data-ttu-id="104c2-174">Biz hello sonuçlar görünür olarak bir satır öne çıkması, birden çok bağlantı noktası bağlantı 111 vardı.</span><span class="sxs-lookup"><span data-stu-id="104c2-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="104c2-175">Uzak Masaüstü olduğu hello en sık kullanılan bağlantı noktası 3389, oluştu ve hello kalan RPC dinamik bağlantı noktalarının.</span><span class="sxs-lookup"><span data-stu-id="104c2-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="104c2-176">Bu trafik bir şey olabilir, ancak birçok bağlantıları için kullanılan ve bilinmeyen toohello yönetici haklarına sahip bir bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="104c2-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![Şekil 5][5]

### <a name="step-3"></a><span data-ttu-id="104c2-178">3. Adım</span><span class="sxs-lookup"><span data-stu-id="104c2-178">Step 3</span></span>

<span data-ttu-id="104c2-179">Göre Yerleştir bağlantı noktası başlangıç bağlantı noktasını temel alarak bizim yakalama filtre uygulayabilirsiniz yetersiz belirledik.</span><span class="sxs-lookup"><span data-stu-id="104c2-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="104c2-180">Bu senaryoda Hello filtresi şöyle olacaktır:</span><span class="sxs-lookup"><span data-stu-id="104c2-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="104c2-181">Biz hello filtre metni üstten hello filtre metin kutusuna girin ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="104c2-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![Şekil 6][6]

<span data-ttu-id="104c2-183">Merhaba sonuçlarından tüm hello trafiği üzerinde hello yerel bir sanal makineden gelen görebiliriz aynı alt ağ.</span><span class="sxs-lookup"><span data-stu-id="104c2-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="104c2-184">Biz bu trafiği neden oluştuğunu hala anlamadığınız, size daha fazla neden bu bağlantı noktası 111 çağrıları yapma hello paketleri toodetermine inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="104c2-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="104c2-185">Bu bilgiyle biz hello uygun eylemde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="104c2-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="104c2-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="104c2-186">Next steps</span></span>

<span data-ttu-id="104c2-187">Bilgi ziyaret ederek hello Ağ İzleyicisi'nin diğer tanılama özelliklerini hakkında [Azure ağ izlemeye genel bakış](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="104c2-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













