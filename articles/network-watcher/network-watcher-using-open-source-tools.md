---
title: "Azure Ağ İzleyicisi'ni ve açık kaynaklı araçları ile aaaVisualize ağ trafiği desenlerini | Microsoft Docs"
description: "Bu sayfa, vm'lerden Capanalysis toovisualize trafiği desenlerini tooand toouse Ağ İzleyicisi paket nasıl yakalama açıklar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="41dd7-103">Ağ trafiği desenlerini tooand açık kaynaklı araçları kullanarak, vm'lerden Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="41dd7-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="41dd7-104">Paket yakalama tooperform ağ hukuk ve derin paket incelemesi izin ağ verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="41dd7-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="41dd7-105">Kaynak araç ağınız hakkında tooanalyze paket yakalamaları toogain Öngörüler kullanabileceğiniz birçok açılır vardır.</span><span class="sxs-lookup"><span data-stu-id="41dd7-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="41dd7-106">Böyle bir araç CapAnalysis, bir açık kaynak paket yakalama görselleştirme Aracı ' dir.</span><span class="sxs-lookup"><span data-stu-id="41dd7-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="41dd7-107">Paket yakalama veri görselleştirme tooquickly türetilen Öngörüler modelleri ve anormallikleri ağınızdaki bir değerli yoludur.</span><span class="sxs-lookup"><span data-stu-id="41dd7-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="41dd7-108">Görselleştirmeleri de böyle Öngörüler apı'lerinizi bir şekilde paylaşma olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="41dd7-109">Ağınızda tooperform paket sağlayarak bu değerli verileri yakalar özelliği toocapture hello Azure'nın Ağ İzleyicisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="41dd7-110">Bu makalede, paket toovisualize ve kazanç bilgiler nasıl yakalar CapAnalysis ile Ağ İzleyicisi'ni kullanarak bir kılavuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="41dd7-111">Senaryo</span><span class="sxs-lookup"><span data-stu-id="41dd7-111">Scenario</span></span>

<span data-ttu-id="41dd7-112">Dağıtılan basit bir web uygulaması olan bir VM'de Azure istediğiniz toouse açık kaynaklı araçları toovisualize kendi ağ trafiği tooquickly tanımla akış desenleri ve tüm olası anormallikleri.</span><span class="sxs-lookup"><span data-stu-id="41dd7-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="41dd7-113">Ağ İzleyicisi ile ağ ortamınızın bir paket yakalama elde ve doğrudan depolama hesabınıza saklayın.</span><span class="sxs-lookup"><span data-stu-id="41dd7-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="41dd7-114">CapAnalysis hello paket yakalama doğrudan hello depolama blobu gelen alma ve içeriğini görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="41dd7-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![senaryo][1]

## <a name="steps"></a><span data-ttu-id="41dd7-116">Adımlar</span><span class="sxs-lookup"><span data-stu-id="41dd7-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="41dd7-117">CapAnalysis yükleyin</span><span class="sxs-lookup"><span data-stu-id="41dd7-117">Install CapAnalysis</span></span>

<span data-ttu-id="41dd7-118">tooinstall CapAnalysis bir sanal makinede toohello resmi yönergeleri başvurabilir burada https://www.capanalysis.net/ca/how-to-install-capanalysis.</span><span class="sxs-lookup"><span data-stu-id="41dd7-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="41dd7-119">CapAnalysis uzaktan erişim, yeni bir gelen güvenlik kuralı ekleyerek tooopen bağlantı noktası 9877 VM ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="41dd7-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="41dd7-120">Ağ güvenlik grupları kuralları oluşturma hakkında daha fazla bilgi için çok başvurmak[içinde varolan bir NSG kuralları oluşturma](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="41dd7-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="41dd7-121">Merhaba kural başarıyla eklendikten sonra mümkün tooaccess CapAnalysis olmalıdır gelen`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="41dd7-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="41dd7-122">Bir paket yakalama oturum Azure Ağ İzleyicisi toostart kullanın</span><span class="sxs-lookup"><span data-stu-id="41dd7-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="41dd7-123">Ağ İzleyicisi toocapture paketleri tootrack ve giden trafiği filtrelemek bir sanal makine sağlar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="41dd7-124">Toohello yönergeleri başvurabilir [Yönet paket yakalar Ağ İzleyicisi ile](network-watcher-packet-capture-manage-portal.md) bir paket yakalama oturumunu toostart.</span><span class="sxs-lookup"><span data-stu-id="41dd7-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="41dd7-125">Bu paket yakalama CapAnalysis tarafından erişilen bir depolama blob toobe depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="41dd7-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="41dd7-126">Paket yakalama tooCapAnalysis karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="41dd7-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="41dd7-127">Doğrudan hello paket yakalama depolandığı hello "URL'den alma" sekmesini kullanarak ve bir bağlantı toohello depolama blobu sağlayarak Ağ İzleyicisi tarafından gerçekleştirilen bir paket yakalama karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41dd7-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="41dd7-128">Bir bağlantı tooCapAnalysis sağlanırken emin tooappend bir SAS belirteci toohello depolama blob URL'si olun.</span><span class="sxs-lookup"><span data-stu-id="41dd7-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="41dd7-129">toodo Bu, tooShared erişim imzası hello depolama hesabından gidin, iznine hello atamak ve bir belirteç hello SAS Oluştur düğmesine toocreate tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="41dd7-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="41dd7-130">Ardından bu SAS belirteci toohello paket yakalama depolama blob URL'si ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41dd7-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="41dd7-131">Hello elde edilen URL şöyle görünecektir: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="41dd7-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="41dd7-132">Analiz etme paket yakalar</span><span class="sxs-lookup"><span data-stu-id="41dd7-132">Analyzing packet captures</span></span>

<span data-ttu-id="41dd7-133">CapAnalysis çeşitli seçenekler toovisualize paket yakalama, farklı açısından sağlayan her analizi sunar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="41dd7-134">Bu görsel özetler ile ağ trafiği eğilimleri anlamak ve hızlı bir şekilde tüm olağandışı nokta.</span><span class="sxs-lookup"><span data-stu-id="41dd7-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="41dd7-135">Bu özelliklerden bazılarını listesi aşağıdaki hello gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="41dd7-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="41dd7-136">Akış tabloları</span><span class="sxs-lookup"><span data-stu-id="41dd7-136">Flow Tables</span></span>

    <span data-ttu-id="41dd7-137">Bu tablo, hello paket veri akışlarında listesi Merhaba, zaman damgası başlangıç akışları ile ilişkili hello ve hello akış yanı sıra ile kaynak ve hedef IP ilişkili çeşitli protokoller hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![capanalysis akış sayfası][5]

1. <span data-ttu-id="41dd7-139">Protokolü'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="41dd7-139">Protocol Overview</span></span>

    <span data-ttu-id="41dd7-140">Bu bölme sağlar tooquickly çeşitli protokolleri ve coğrafyalara bu hello dağıtım ağ trafiği hello bakın.</span><span class="sxs-lookup"><span data-stu-id="41dd7-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![capanalysis Protokolü'ne genel bakış][6]

1. <span data-ttu-id="41dd7-142">İstatistikler</span><span class="sxs-lookup"><span data-stu-id="41dd7-142">Statistics</span></span>

    <span data-ttu-id="41dd7-143">Bu bölme, tooview ağ trafiği istatistikleri – bayt gönderildi ve kaynak ve hedef IP, Akışlar hello kaynak ve hedef IP, her birinin için alınan Protokolü çeşitli akışları ve hello süre akışları için kullanılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![capanalysis istatistikleri][7]

1. <span data-ttu-id="41dd7-145">geomap</span><span class="sxs-lookup"><span data-stu-id="41dd7-145">Geomap</span></span>

    <span data-ttu-id="41dd7-146">Bu bölme toohello hacimli trafik her ülkedeki ölçeklendirme renkler, ağ trafiğinizi olan bir harita görünümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="41dd7-147">Gönderilen ve bu ülkede IP'leri alınan veriler hello oranını gibi vurgulanan ülkelerde tooview ek akış istatistikleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41dd7-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="41dd7-149">Filtreler</span><span class="sxs-lookup"><span data-stu-id="41dd7-149">Filters</span></span>

    <span data-ttu-id="41dd7-150">CapAnalysis belirli paketlerin hızlı çözümleme için bir filtre kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="41dd7-151">Örneğin, bu alt trafik üzerinde Protokolü toogain belirli Öngörüler tarafından toofilter hello veri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41dd7-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filtreleri][11]

    <span data-ttu-id="41dd7-153">Ziyaret [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn tüm CapAnalysis özellikleri hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="41dd7-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="41dd7-154">Sonuç</span><span class="sxs-lookup"><span data-stu-id="41dd7-154">Conclusion</span></span>

<span data-ttu-id="41dd7-155">Ağ İzleyicisi'nin paket yakalama özelliği, ağ trafiğinizi daha iyi anlamak ve toocapture hello veri gerekli tooperform ağ hukuk sağlar.</span><span class="sxs-lookup"><span data-stu-id="41dd7-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="41dd7-156">Bu senaryoda, nasıl Ağ İzleyicisi paket görüntüleri kolayca açık kaynak görselleştirme araçları ile tümleştirilebilir gösterdi.</span><span class="sxs-lookup"><span data-stu-id="41dd7-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="41dd7-157">CapAnalysis toovisualize paketleri yakalar gibi açık kaynaklı araçları kullanarak, ayrıntılı paket incelemesi gerçekleştiren ve hızlı bir şekilde ağ trafiğinizi içinde eğilimleri belirlemek.</span><span class="sxs-lookup"><span data-stu-id="41dd7-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41dd7-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41dd7-158">Next steps</span></span>

<span data-ttu-id="41dd7-159">NSG akış günlükleri, hakkında daha fazla toolearn ziyaret [NSG akış günlükleri](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="41dd7-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="41dd7-160">Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="41dd7-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
