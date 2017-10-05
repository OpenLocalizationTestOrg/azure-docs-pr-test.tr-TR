---
title: "Azure Ağ İzleyicisi ile paket incelemesi | Microsoft Docs"
description: "Bu makalede, bir VM'den toplanan derin paket incelemesi gerçekleştirmek için Ağ İzleyicisi'ni kullanmayı açıklar"
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
ms.openlocfilehash: 91c47bb8922a9be21dff72e7cf64b29b14a36e9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="8ffa4-103">Azure Ağ İzleyicisi ile paket incelemesi</span><span class="sxs-lookup"><span data-stu-id="8ffa4-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="8ffa4-104">Ağ İzleyicisi'nin paket yakalama özelliği kullanarak, Azure vm'lerinde portalı, PowerShell CLI ve SDK ve REST API aracılığıyla programlı olarak yakalamaları oturumlarını yönetmesine ve başlatın.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-104">Using the packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from the portal, PowerShell, CLI, and programmatically through the SDK and REST API.</span></span> <span data-ttu-id="8ffa4-105">Paket yakalama, paket düzeyinde veri kullanılabilir bir biçimde bilgileri sağlayarak gerektiren adresi senaryolar olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-105">Packet capture allows you to address scenarios that require packet level data by providing the information in a readily usable format.</span></span> <span data-ttu-id="8ffa4-106">Verileri incelemek için ücretsiz Araçlar yararlanarak, Vm'leriniz gelen ve giden iletişimler inceleyin ve ağ trafiğinizi alın.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-106">Leveraging freely available tools to inspect the data, you can examine communications sent to and from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="8ffa4-107">Paket yakalama veri bazı örnek kullanımları şunlardır: ağ veya uygulama sorunları incelemeye, ağ kötüye ve yetkisiz erişim girişimlerini algılama veya Mevzuat uyumluluğu bakımını yapma.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="8ffa4-108">Bu makalede, Ağ İzleyicisi tarafından sağlanan bir paket yakalama dosyasını açmak nasıl bir popüler açık kaynak aracını kullanarak gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-108">In this article, we show how to open a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="8ffa4-109">Biz de nasıl bir bağlantı gecikmesi hesaplamak, anormal trafiği tanımlamak ve ağ istatistikleri inceleyin gösteren örnekler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-109">We will also provide examples showing how to calculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8ffa4-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="8ffa4-110">Before you begin</span></span>

<span data-ttu-id="8ffa4-111">Bu makalede önceden çalıştırılmış olan bir paket yakalama önceden yapılandırılmış bazı senaryolar üzerinden gider.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="8ffa4-112">Bu senaryolar, bir paket yakalama gözden geçirerek erişilebilir özellikleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="8ffa4-113">Bu senaryo kullanır [WireShark](https://www.wireshark.org/) paket yakalama incelemek için.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-113">This scenario uses [WireShark](https://www.wireshark.org/) to inspect the packet capture.</span></span>

<span data-ttu-id="8ffa4-114">Bu senaryo, bir sanal makinede bir paket yakalama zaten başlattıysanız varsayar.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="8ffa4-115">Bir paket yakalama ziyaret oluşturmayı öğrenmek için [Yönet paket yakalar portal ile](network-watcher-packet-capture-manage-portal.md) veya REST şu adresi ziyaret ederek ile [REST API ile paket yakalar yönetme](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="8ffa4-115">To learn how to create a packet capture visit [Manage packet captures with the portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="8ffa4-116">Senaryo</span><span class="sxs-lookup"><span data-stu-id="8ffa4-116">Scenario</span></span>

<span data-ttu-id="8ffa4-117">Bu senaryoda:</span><span class="sxs-lookup"><span data-stu-id="8ffa4-117">In this scenario, you:</span></span>

* <span data-ttu-id="8ffa4-118">Paket yakalama gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="8ffa4-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="8ffa4-119">Ağ gecikmesi Hesapla</span><span class="sxs-lookup"><span data-stu-id="8ffa4-119">Calculate network latency</span></span>

<span data-ttu-id="8ffa4-120">Bu senaryoda, iki uç noktaları arasında gerçekleşen bir İletim Denetimi Protokolü (TCP) konuşma ilk gidiş dönüş süresi (RTT) görüntülemek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-120">In this scenario, we show how to view the initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="8ffa4-121">Bir TCP bağlantı kurulduğunda bağlantı gönderilen ilk üç paketleri genellikle üç yönlü el sıkışması olarak adlandırılan bir yol izler.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-121">When a TCP connection is established, the first three packets sent in the connection follow a pattern commonly referred to as the three-way handshake.</span></span> <span data-ttu-id="8ffa4-122">Bu bağlantı kuruldu, istemci bir ilk istek ve yanıt sunucudan bu el sıkışma gönderilen ilk iki paketleri inceleyerek biz gecikme hesaplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-122">By examining the first two packets sent in this handshake, an initial request from the client and a response from the server, we can calculate the latency when this connection was established.</span></span> <span data-ttu-id="8ffa4-123">Bu gecikme gidiş dönüş süresi (RTT) olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-123">This latency is referred to as the Round Trip Time (RTT).</span></span> <span data-ttu-id="8ffa4-124">TCP protokolü ve üç yönlü el sıkışma hakkında daha fazla bilgi için aşağıdaki kaynağa bakın.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-124">For more information on the TCP protocol and the three-way handshake refer to the following resource.</span></span> <span data-ttu-id="8ffa4-125">https://support.microsoft.com/en-US/Help/172983/Explanation-of-the-three-Way-Handshake-via-TCP-ip</span><span class="sxs-lookup"><span data-stu-id="8ffa4-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="8ffa4-126">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8ffa4-126">Step 1</span></span>

<span data-ttu-id="8ffa4-127">WireShark başlatma</span><span class="sxs-lookup"><span data-stu-id="8ffa4-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="8ffa4-128">2. Adım</span><span class="sxs-lookup"><span data-stu-id="8ffa4-128">Step 2</span></span>

<span data-ttu-id="8ffa4-129">Yük **.cap** paket yakalama dosyasından.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-129">Load the **.cap** file from your packet capture.</span></span> <span data-ttu-id="8ffa4-130">Bu dosya içinde kaydedildi blob bulunabilir bizim nasıl yapılandırdığınıza bağlı olarak sanal makinenin yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-130">This file can be found in the blob it was saved in our locally on the virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="8ffa4-131">3. Adım</span><span class="sxs-lookup"><span data-stu-id="8ffa4-131">Step 3</span></span>

<span data-ttu-id="8ffa4-132">TCP görüşmeleri ilk gidiş dönüş süresi (RTT) görüntülemek için biz yalnızca TCP anlaşma söz konusu ilk iki paket adresindeki arayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-132">To view the initial Round Trip Time (RTT) in TCP conversations, we will only be looking at the first two packets involved in the TCP handshake.</span></span> <span data-ttu-id="8ffa4-133">Biz [Eşitlemeye] olan üç yönlü el sıkışma ilk iki paketlerinde kullanacağınız [Eşitlemeye, ACK] paketler.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-133">We will be using the first two packets in the three-way handshake, which are the [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="8ffa4-134">TCP üstbilgisinde ayarlanan bayraklarının adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-134">They are named for flags set in the TCP header.</span></span> <span data-ttu-id="8ffa4-135">Son paket [ACK] paket el sıkışma içinde bu senaryoda kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-135">The last packet in the handshake, the [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="8ffa4-136">İstemci tarafından gönderilen [Eşitlemeye] paket.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-136">The [SYN] packet is sent by the client.</span></span> <span data-ttu-id="8ffa4-137">Alındıktan sonra sunucu [ACK] paket Eşitlemeye istemciden alma onay olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-137">Once it is received the server sends the [ACK] packet as an acknowledgement of receiving the SYN from the client.</span></span> <span data-ttu-id="8ffa4-138">Sunucu yanıtı çok az ek yük gerektirdiğini yararlanarak, biz RTT zamanını çıkararak [Eşitlemeye, ACK] hesaplamak paket alındı [Eşitlemeye] zamana göre istemci tarafından paket istemci tarafından gönderildi.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-138">Leveraging the fact that the server’s response requires very little overhead, we calculate the RTT by subtracting the time the [SYN, ACK] packet was received by the client by the time [SYN] packet was sent by the client.</span></span>

<span data-ttu-id="8ffa4-139">WireShark kullanarak bu değeri bize hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="8ffa4-140">Daha kolay TCP üç yönlü anlaşma ilk iki paketlerini görüntülemek için biz WireShark tarafından sağlanan filtreleme özellik yararlanacak olan.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-140">To more easily view the first two packets in the TCP three-way handshake, we will utilize the filtering capability provided by WireShark.</span></span>

<span data-ttu-id="8ffa4-141">WireShark filtre uygulamak için yakalama [Eşitlemeye] pakette "İletim Denetimi Protokolü" kesimi genişletin ve TCP üstbilgisinde ayarlanan bayraklar inceleyin.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-141">To apply the filter in WireShark, expand the “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine the flags set in the TCP header.</span></span>

<span data-ttu-id="8ffa4-142">Tüm [Eşitlemeye] üzerinde filtrelemek için arıyoruz beri ve [Eşitlemeye, ACK] bayrakları altında paketleri cofirm eşitlemeye biti 1 olarak ayarlayın, sonra sağ tıklayarak eşitlemeye bit Filtre -> olarak seçili Uygula ->.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-142">Since we are looking to filter on all [SYN] and [SYN, ACK] packets, under flags cofirm that the Syn bit is set to 1, then right click on the Syn bit -> Apply as Filter -> Selected.</span></span>

![Şekil 7][7]

### <a name="step-4"></a><span data-ttu-id="8ffa4-144">4. Adım</span><span class="sxs-lookup"><span data-stu-id="8ffa4-144">Step 4</span></span>

<span data-ttu-id="8ffa4-145">Yalnızca [Eşitlemeye] bit kümesiyle paketleri görmek için penceresini filtre, ilk RTT görüntülemek ilgilendiğiniz görüşmeleri kolayca seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-145">Now that you have filtered the window to only see packets with the [SYN] bit set, you can easily select conversations you are interested in to view the initial RTT.</span></span> <span data-ttu-id="8ffa4-146">RTT WireShark içinde görüntülemek için basit bir yol tıklamanız yeterlidir "SEQ/ACK" analiz işaretlenmiş açılır.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-146">A simple way to view the RTT in WireShark simply click the dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="8ffa4-147">Ardından görüntülenen RTT görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-147">You will then see the RTT displayed.</span></span> <span data-ttu-id="8ffa4-148">Bu durumda, RTT 0.0022114 saniye ya da 2.211 ms idi.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-148">In this case, the RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![Şekil 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="8ffa4-150">İstenmeyen protokolleri</span><span class="sxs-lookup"><span data-stu-id="8ffa4-150">Unwanted protocols</span></span>

<span data-ttu-id="8ffa4-151">Azure üzerinde dağıtılan sanal makine örneği üzerinde çalışan birçok uygulamalar olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="8ffa4-152">Bu uygulamalar çoğunu ağ üzerinden belki de açık izniniz olmadan iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-152">Many of these applications communicate over the network, perhaps without your explicit permission.</span></span> <span data-ttu-id="8ffa4-153">Paket yakalama ağ iletişimi depolamak için kullanarak, biz nasıl uygulama ağ üzerinde varsayılır ve herhangi bir sorun için Ara araştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-153">Using packet capture to store network communication, we can investigate how application are talking on the network and look for any issues.</span></span>

<span data-ttu-id="8ffa4-154">Bu örnekte, sizi bir önceki gözden makinenizde çalışan bir uygulama yetkisiz iletişimi gösterebilir istenmeyen protokoller için paket yakalama çalıştı.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="8ffa4-155">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8ffa4-155">Step 1</span></span>

<span data-ttu-id="8ffa4-156">Önceki senaryoda aynı yakalama kullanarak **istatistikleri** > **Protokolü hiyerarşisi**</span><span class="sxs-lookup"><span data-stu-id="8ffa4-156">Using the same capture in the previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![protokol hiyerarşi menüsü][2]

<span data-ttu-id="8ffa4-158">Protokol hiyerarşisi penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-158">The protocol hierarchy window appears.</span></span> <span data-ttu-id="8ffa4-159">Bu görünüm yakalama oturumunu ve aktarılan ve protokoller kullanılarak alınan paket sayısı sırasında kullanımda olan tüm protokollerin bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-159">This view provides a list of all the protocols that were in use during the capture session and the number of packets transmitted and received using the protocols.</span></span> <span data-ttu-id="8ffa4-160">Bu görünüm, sanal makine ya da ağ üzerindeki istenmeyen ağ trafiğini bulmak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![açılan iletişim kuralı hiyerarşisini][3]

<span data-ttu-id="8ffa4-162">Aşağıdaki ekran görüntüsünde gördüğünüz gibi eşler arası dosya paylaşımı için kullanılan BitTorrent protokolünü kullanarak trafiği vardı.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-162">As you can see in the following screen capture, there was traffic using the BitTorrent protocol, which is used for peer to peer file sharing.</span></span> <span data-ttu-id="8ffa4-163">Yönetici olarak BitTorrent görmeyi beklediğiniz değil Bu belirli sanal makinelerde trafiği.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-163">As an administrator you do not expect to see BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="8ffa4-164">Şimdi, bu trafiğin kullanan, bu sanal makinede yüklü eşler arası yazılım kaldırabilir, veya ağ güvenlik grupları veya bir Güvenlik Duvarı'nı kullanarak trafiği engelle.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-164">Now you aware of this traffic, you can remove the peer to peer software that installed on this virtual machine, or block the traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="8ffa4-165">Ayrıca, Protokolü kullanımı, sanal makinelere düzenli olarak gözden geçirebilirsiniz şekilde paket yakalamaları bir zamanlamaya göre çalışmasını tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-165">Additionally, you may elect to run packet captures on a schedule, so you can review the protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="8ffa4-166">Azure ağ görevleri otomatik hale getirme konusunda bir örnek ziyaret [izlemek azure automation ile ağ kaynakları](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="8ffa4-166">For an example on how to automate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="8ffa4-167">En çok kullanılan hedefler ve bağlantı noktalarını bulma</span><span class="sxs-lookup"><span data-stu-id="8ffa4-167">Finding top destinations and ports</span></span>

<span data-ttu-id="8ffa4-168">Üzerinden iletilen bağlantı noktalarını, uç noktalarını ve trafik türlerini anlama bir izleme veya sorun giderme uygulamaları ve ağınızdaki kaynaklara önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-168">Understanding the types of traffic, the endpoints, and the ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="8ffa4-169">Paket yakalama dosyası üstten yararlanarak, biz bizim VM ile iletişim kurduğu üst hedefler ve kullanılan bağlantı noktaları hızla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-169">Utilizing a packet capture file from above, we can quickly learn the top destinations our VM is communicating with and the ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="8ffa4-170">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8ffa4-170">Step 1</span></span>

<span data-ttu-id="8ffa4-171">Önceki senaryoda aynı yakalama kullanarak **istatistikleri** > **IPv4 istatistikleri** > **hedefleri ve bağlantı noktaları**</span><span class="sxs-lookup"><span data-stu-id="8ffa4-171">Using the same capture in the previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![Paket yakalama penceresi][4]

### <a name="step-2"></a><span data-ttu-id="8ffa4-173">2. Adım</span><span class="sxs-lookup"><span data-stu-id="8ffa4-173">Step 2</span></span>

<span data-ttu-id="8ffa4-174">Bir satır öne çıkması sonuçları göz biz gibi birden çok bağlantı noktası bağlantı 111 vardı.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-174">As we look through the results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="8ffa4-175">En fazla kullanılan bağlantı noktası 3389, Uzak Masaüstü olduğu idi ve kalan RPC dinamik bağlantı noktalarının.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-175">The most used port was 3389, which is remote desktop, and the remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="8ffa4-176">Bu trafik bir şey olabilir, ancak birçok bağlantıları için kullanılan ve yönetici için bilinmeyen bir bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown to the administrator.</span></span>

![Şekil 5][5]

### <a name="step-3"></a><span data-ttu-id="8ffa4-178">3. Adım</span><span class="sxs-lookup"><span data-stu-id="8ffa4-178">Step 3</span></span>

<span data-ttu-id="8ffa4-179">Yerleştir bağlantı noktası dışı belirledik şimdi biz bağlantı noktasını temel alarak bizim yakalama filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-179">Now that we have determined an out of place port we can filter our capture based on the port.</span></span>

<span data-ttu-id="8ffa4-180">Bu senaryoda filtresi şöyle olacaktır:</span><span class="sxs-lookup"><span data-stu-id="8ffa4-180">The filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="8ffa4-181">Biz üstten filtre metni filtre metin kutusuna girin ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-181">We enter the filter text from above in the filter textbox and hit enter.</span></span>

![Şekil 6][6]

<span data-ttu-id="8ffa4-183">Tüm trafiğin aynı alt ağda yerel bir sanal makineden gelen sonuçlarından görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-183">From the results, we can see all the traffic is coming from a local virtual machine on the same subnet.</span></span> <span data-ttu-id="8ffa4-184">Biz bu trafiği neden oluştuğunu hala anlamadığınız, size daha fazla neden bu bağlantı noktası 111 çağrıları yapma belirlemek için paket inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-184">If we still don’t understand why this traffic is occurring, we can further inspect the packets to determine why it is making these calls on port 111.</span></span> <span data-ttu-id="8ffa4-185">Bu bilgileri size uygun eylemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8ffa4-185">With this information we can take the appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ffa4-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ffa4-186">Next steps</span></span>

<span data-ttu-id="8ffa4-187">Ağ İzleyicisi, diğer tanılama özellikleri hakkında bilgi edinin ziyaret ederek [Azure ağ izlemeye genel bakış](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8ffa4-187">Learn about the other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













