---
title: "Ağ trafiği desenlerini Azure Ağ İzleyicisi'ni ve açık kaynaklı araçları ile Görselleştirme | Microsoft Docs"
description: "Bu sayfayı Ağ İzleyicisi paket yakalama ile Capanalysis Vm'leriniz gelen ve giden trafik düzenlerini görselleştirmek için nasıl kullanılacağını açıklar."
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
ms.openlocfilehash: e27bb694d0cbcf1ff7c9d8ca4682a79c8b5c5cb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-network-traffic-patterns-to-and-from-your-vms-using-open-source-tools"></a><span data-ttu-id="93f6f-103">Açık kaynaklı araçları kullanarak, Vm'lerde gelen ve giden ağ trafiği desenlerini Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="93f6f-103">Visualize network traffic patterns to and from your VMs using open source tools</span></span>

<span data-ttu-id="93f6f-104">Paket yakalama ağ hukuk ve derin paket incelemesi gerçekleştirmenize olanak sağlayan ağ verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="93f6f-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span></span> <span data-ttu-id="93f6f-105">Kaynak araç ağınız hakkında Öngörüler elde etmek için paket yakalamaları çözümlemek için kullanabileceğiniz birçok açılır vardır.</span><span class="sxs-lookup"><span data-stu-id="93f6f-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span></span> <span data-ttu-id="93f6f-106">Böyle bir araç CapAnalysis, bir açık kaynak paket yakalama görselleştirme Aracı ' dir.</span><span class="sxs-lookup"><span data-stu-id="93f6f-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="93f6f-107">Paket yakalama veri görselleştirme Öngörüler modelleri ve ağınızdaki anormallikleri hızlıca çıkarmaya değerli bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="93f6f-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="93f6f-108">Görselleştirmeleri de böyle Öngörüler apı'lerinizi bir şekilde paylaşma olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="93f6f-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="93f6f-109">Azure'nın Ağ İzleyicisi ağınızdaki paket yakalamaları gerçekleştirmenizi sağlayarak bu değerli verileri yakalama olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="93f6f-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span></span> <span data-ttu-id="93f6f-110">Bu makalede, görselleştirin ve paket ilişkin bilgiler elde etmek nasıl bir kılavuz CapAnalysis ile Ağ İzleyicisi kullanılarak yakalar sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="93f6f-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="93f6f-111">Senaryo</span><span class="sxs-lookup"><span data-stu-id="93f6f-111">Scenario</span></span>

<span data-ttu-id="93f6f-112">Akış desenleri ve tüm olası anormallikleri hızlı bir şekilde tanımlamak için ağ trafiğini görselleştirmek için açık kaynaklı araçları kullanmak istediğiniz bir Azure VM'de dağıtılan basit bir web uygulaması sahip.</span><span class="sxs-lookup"><span data-stu-id="93f6f-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="93f6f-113">Ağ İzleyicisi ile ağ ortamınızın bir paket yakalama elde ve doğrudan depolama hesabınıza saklayın.</span><span class="sxs-lookup"><span data-stu-id="93f6f-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="93f6f-114">CapAnalysis paket yakalama depolama blobda doğrudan alma ve içeriğini görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="93f6f-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span></span>

![senaryo][1]

## <a name="steps"></a><span data-ttu-id="93f6f-116">Adımlar</span><span class="sxs-lookup"><span data-stu-id="93f6f-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="93f6f-117">CapAnalysis yükleyin</span><span class="sxs-lookup"><span data-stu-id="93f6f-117">Install CapAnalysis</span></span>

<span data-ttu-id="93f6f-118">Bir sanal makineye CapAnalysis yükleme https://www.capanalysis.net/ca/how-to-install-capanalysis resmi yönergeleri için başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93f6f-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="93f6f-119">CapAnalysis uzaktan erişim, size yeni bir gelen güvenlik kuralı ekleyerek, VM 9877 noktasından açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93f6f-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="93f6f-120">Ağ güvenlik grupları kuralları oluşturma hakkında daha fazla bilgi için bkz [içinde varolan bir NSG kuralları oluşturma](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="93f6f-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="93f6f-121">Kural başarıyla eklendikten sonra gelen CapAnalysis erişebilir olmalıdır`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="93f6f-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-to-start-a-packet-capture-session"></a><span data-ttu-id="93f6f-122">Paket yakalama oturumunu başlatmak için Azure Ağ İzleyicisi'ni kullanma</span><span class="sxs-lookup"><span data-stu-id="93f6f-122">Use Azure Network Watcher to start a packet capture session</span></span>

<span data-ttu-id="93f6f-123">Ağ İzleyicisi, bir sanal makine ve trafiği izlemek için paketler yakalamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="93f6f-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="93f6f-124">Kısmındaki yönergeleri başvurabilirsiniz [Yönet paket yakalar Ağ İzleyicisi ile](network-watcher-packet-capture-manage-portal.md) paket yakalama oturumunu başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="93f6f-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span></span> <span data-ttu-id="93f6f-125">Bu paket yakalama CapAnalysis tarafından erişilecek bir depolama blob depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="93f6f-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-to-capanalysis"></a><span data-ttu-id="93f6f-126">Paket yakalama CapAnalysis için karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="93f6f-126">Upload a packet capture to CapAnalysis</span></span>
<span data-ttu-id="93f6f-127">Paket yakalama depolandığı "URL'den alma" sekmesini kullanarak ve depolama blobu bağlantı sağlayan Ağ İzleyicisi tarafından gerçekleştirilecek bir paket yakalama doğrudan yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93f6f-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span></span>

<span data-ttu-id="93f6f-128">Bir bağlantı için CapAnalysis sağlarken, depolama blob URL'si için bir SAS belirteci eklenecek emin olun.</span><span class="sxs-lookup"><span data-stu-id="93f6f-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span></span>  <span data-ttu-id="93f6f-129">Bunu yapmak için paylaşılan erişim imzası depolama hesabından gidin, izin verilen izinleri atamak ve bir belirteç oluşturmak için SAS Oluştur düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="93f6f-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span></span> <span data-ttu-id="93f6f-130">Paket yakalama depolama blob URL'si bu SAS belirteci sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93f6f-130">You can then append this SAS token to the packet capture storage blob URL.</span></span>

<span data-ttu-id="93f6f-131">Sonuçta elde edilen URL şöyle görünür: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="93f6f-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="93f6f-132">Analiz etme paket yakalar</span><span class="sxs-lookup"><span data-stu-id="93f6f-132">Analyzing packet captures</span></span>

<span data-ttu-id="93f6f-133">CapAnalysis paket yakalama, farklı açısından sağlayan her analizi görselleştirmek için çeşitli seçenekler sunar.</span><span class="sxs-lookup"><span data-stu-id="93f6f-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="93f6f-134">Bu görsel özetler ile ağ trafiği eğilimleri anlamak ve hızlı bir şekilde tüm olağandışı nokta.</span><span class="sxs-lookup"><span data-stu-id="93f6f-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="93f6f-135">Bu özelliklerden bazılarını aşağıdaki listede gösterilir:</span><span class="sxs-lookup"><span data-stu-id="93f6f-135">A few of these features are shown in the following list:</span></span>

1. <span data-ttu-id="93f6f-136">Akış tabloları</span><span class="sxs-lookup"><span data-stu-id="93f6f-136">Flow Tables</span></span>

    <span data-ttu-id="93f6f-137">Bu tabloda paket verileri, akışları ile ilişkili zaman damgası ve akış yanı sıra ile kaynak ve hedef IP ilişkili çeşitli protokoller akışlarında listesi verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="93f6f-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span></span>

    ![capanalysis akış sayfası][5]

1. <span data-ttu-id="93f6f-139">Protokolü'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="93f6f-139">Protocol Overview</span></span>

    <span data-ttu-id="93f6f-140">Bu bölme, ağ trafiğinin dağıtımını çeşitli protokolleri ve coğrafi hızlı bir şekilde görmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="93f6f-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span></span>

    ![capanalysis Protokolü'ne genel bakış][6]

1. <span data-ttu-id="93f6f-142">İstatistikler</span><span class="sxs-lookup"><span data-stu-id="93f6f-142">Statistics</span></span>

    <span data-ttu-id="93f6f-143">Bu bölme, ağ trafiğini istatistikleri – bayt görüntülemek için gönderilen ve kaynak ve hedef IP, Akışlar için her kaynak ve hedef IP, alınan Protokolü çeşitli akışları ve süre akışları için kullanılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="93f6f-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span></span>

    ![capanalysis istatistikleri][7]

1. <span data-ttu-id="93f6f-145">geomap</span><span class="sxs-lookup"><span data-stu-id="93f6f-145">Geomap</span></span>

    <span data-ttu-id="93f6f-146">Bu bölme her ülkeden trafik hacmi ölçeklendirme renkler, ağ trafiğinizi olan bir harita görünümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="93f6f-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span></span> <span data-ttu-id="93f6f-147">Gönderilen ve bu ülkede IP'leri alınan veriler oranını gibi ek akış istatistiklerini görüntülemek için vurgulanan ülkelerde seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93f6f-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="93f6f-149">Filtreler</span><span class="sxs-lookup"><span data-stu-id="93f6f-149">Filters</span></span>

    <span data-ttu-id="93f6f-150">CapAnalysis belirli paketlerin hızlı çözümleme için bir filtre kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="93f6f-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="93f6f-151">Örneğin, bu alt trafik üzerinde belirli serisidir protokolü tarafından verilerini filtrelemek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93f6f-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span></span>

    ![filtreleri][11]

    <span data-ttu-id="93f6f-153">Ziyaret [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) tüm CapAnalysis özellikleri hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="93f6f-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="93f6f-154">Sonuç</span><span class="sxs-lookup"><span data-stu-id="93f6f-154">Conclusion</span></span>

<span data-ttu-id="93f6f-155">Ağ İzleyicisi'nin paket yakalama özelliği, ağ hukuk gerçekleştirmek ve ağ trafiğinizi daha iyi anlamak gereken verileri yakalamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="93f6f-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="93f6f-156">Bu senaryoda, nasıl Ağ İzleyicisi paket görüntüleri kolayca açık kaynak görselleştirme araçları ile tümleştirilebilir gösterdi.</span><span class="sxs-lookup"><span data-stu-id="93f6f-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="93f6f-157">Paket yakalamaları görselleştirmek için CapAnalysis gibi açık kaynaklı araçları kullanarak, derin paket incelemesi gerçekleştiren ve hızlı bir şekilde ağ trafiğinizi içinde eğilimleri belirlemek.</span><span class="sxs-lookup"><span data-stu-id="93f6f-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93f6f-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="93f6f-158">Next steps</span></span>

<span data-ttu-id="93f6f-159">NSG akış günlükleri hakkında daha fazla bilgi için [NSG akış günlükleri](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="93f6f-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="93f6f-160">Ziyaret ederek NSG akış günlüklerinizi Power BI ile görselleştirme öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="93f6f-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
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
