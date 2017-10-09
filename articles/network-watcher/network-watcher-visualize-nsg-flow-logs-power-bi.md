---
title: "aaaVisualizing Azure ağ güvenlik grubu akış günlükleri Power BI ile | Microsoft Docs"
description: "Bu sayfa toovisualize NSG akış Power BI ile nasıl günlüğe yazacağını açıklar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="3d2eb-103">Power BI ile visualizing ağ güvenlik grubu akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="3d2eb-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="3d2eb-104">Ağ güvenlik grubu akış günlükleri, ağ güvenlik grupları hakkında giriş ve çıkış IP trafiği tooview bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="3d2eb-105">Bu akış günlükleri giden Göster ve gelen akış kuralı başına temelinde hello NIC hello akış, 5-tanımlama grubu ve hakkında bilgi hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, protokol) hello trafiğine izin verilen veya reddedilen varsa uygular.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="3d2eb-106">Merhaba günlük dosyalarını el ile arama yaparak veri günlüğü akış zor toogain fikir olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="3d2eb-107">Bu makalede, bir çözüm toovisualize en son akışınız günlüğe kaydeder ve ağınızdaki trafiği hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="3d2eb-108">Senaryo</span><span class="sxs-lookup"><span data-stu-id="3d2eb-108">Scenario</span></span>

<span data-ttu-id="3d2eb-109">Senaryo aşağıdaki hello hello havuzu olarak bizim akış NSG günlüğü verilerini yapılandırdıktan Power BI Masaüstü toohello depolama hesabı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="3d2eb-110">Biz tooour depolama hesabı bağlandıktan sonra Power BI indirir ve hello günlükleri tooprovide görsel bir ağ güvenlik grupları tarafından günlüğe hello trafiği ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="3d2eb-111">Merhaba görselleri inceleyebilirsiniz hello şablonunda sağlanan kullanma:</span><span class="sxs-lookup"><span data-stu-id="3d2eb-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="3d2eb-112">Üst Talkers</span><span class="sxs-lookup"><span data-stu-id="3d2eb-112">Top Talkers</span></span>
* <span data-ttu-id="3d2eb-113">Akış zaman serisi veri yönü ve kural karar tarafından</span><span class="sxs-lookup"><span data-stu-id="3d2eb-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="3d2eb-114">Ağ arabirimi MAC adresiyle akışlar</span><span class="sxs-lookup"><span data-stu-id="3d2eb-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="3d2eb-115">NSG ve kural tarafından akışlar</span><span class="sxs-lookup"><span data-stu-id="3d2eb-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="3d2eb-116">Hedef bağlantı noktası tarafından akışlar</span><span class="sxs-lookup"><span data-stu-id="3d2eb-116">Flows by Destination Port</span></span>

<span data-ttu-id="3d2eb-117">tooadd yeni veri, görselleri, değiştirin ya da sorgular toosuit gereksinimlerinizi Düzenle sağlanan hello düzenlenebilir şablonudur.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="3d2eb-118">Kurulum</span><span class="sxs-lookup"><span data-stu-id="3d2eb-118">Setup</span></span>

<span data-ttu-id="3d2eb-119">Başlamadan önce ağ güvenlik grubu akış hesabınızda bir veya daha çok ağ güvenlik grupları etkin günlüğü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="3d2eb-120">Akış günlükleri ağ güvenliği etkinleştirme yönergeleri için aşağıdaki makaleye bakın toohello bakın: [ağ güvenlik grupları için giriş tooflow günlüğü](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d2eb-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="3d2eb-121">Ayrıca boş alanı, depolama hesabınız var, makine toodownload ve yük hello günlüğü verilerini makinenizde ve yeterli hello Power BI Desktop istemcisinin yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Visio diyagramı][1]

### <a name="steps"></a><span data-ttu-id="3d2eb-123">Adımlar</span><span class="sxs-lookup"><span data-stu-id="3d2eb-123">Steps</span></span>

1. <span data-ttu-id="3d2eb-124">Karşıdan yükleme ve hello Power BI Desktop uygulamasını Power BI şablonda aşağıdaki açık hello [Ağ İzleyicisi Powerbı akış günlükleri şablonu](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="3d2eb-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="3d2eb-125">Gerekli hello sorgu parametrelerini girin</span><span class="sxs-lookup"><span data-stu-id="3d2eb-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="3d2eb-126">**StorageAccountName** – belirtir toohello içeren hello NSG akış günlükleri hello depolama hesabının adını ve gibi tooload görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="3d2eb-127">**NumberOfLogFiles** – Merhaba, gibi toodownload ve Power BI'da görselleştirin, günlük dosyası sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="3d2eb-128">Örneğin, 50 belirtilirse, en son 50 günlük dosyalarını hello.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="3d2eb-129">2 Nsg'ler sahibiz ff etkin ve toosend NSG akış günlükleri toothis hesabı yapılandırılmış sonra hello günlüklerinin son 25 saat görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![Power BI ana][2]

1. <span data-ttu-id="3d2eb-131">Merhaba, depolama hesabının erişim anahtarı girin.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="3d2eb-132">Geçerli erişim tuşları hello Azure portal ve seçme tooyour depolama hesabında giderek bulabileceğiniz **erişim tuşları** hello ayarları menüsünden.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="3d2eb-133">Tıklatın **Bağlan** değişiklikler uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-133">Click **Connect** then apply changes.</span></span>

    ![Erişim tuşları][3]

    ![erişim tuşu 2][4]

4.  <span data-ttu-id="3d2eb-136">Günlüklerinizi indirmek durumda, ayrıştırılmış ve şimdi hello önceden oluşturulmuş görselleri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="3d2eb-137">Merhaba görselleri anlama</span><span class="sxs-lookup"><span data-stu-id="3d2eb-137">Understanding hello visuals</span></span>

<span data-ttu-id="3d2eb-138">Şablon Hello olması koşuluyla Yardım görselleri kümesi hello NSG akış günlük verilerini duygusu olun.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="3d2eb-139">Merhaba aşağıdaki görüntüleri hangi hello Pano verilerle doldurmuş zaman benzer, bir örnek göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="3d2eb-140">Daha ayrıntılı her görsel aşağıda inceleyeceğiz</span><span class="sxs-lookup"><span data-stu-id="3d2eb-140">Below we examine each visual in greater detail</span></span> 

![powerbı][5]
 
<span data-ttu-id="3d2eb-142">Merhaba üst visual gösterir IP'leri hello başlatılan Talkers çoğu bağlantı belirtilen dönem hello hello.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="3d2eb-143">Merhaba kutuları Hello boyutunu toohello göreli bağlantıları sayısına karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="3d2eb-145">Merhaba aşağıdaki zaman serisi grafikleri hello süre boyunca akışları hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="3d2eb-146">Merhaba üst grafik hello akış yönü tarafından ayrılmış ve hello alt (izin verme veya reddetme) yapılan hello karar tarafından ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="3d2eb-147">Bu görsel ile trafiği eğilimleri zaman içinde inceleyin ve herhangi bir anormal ani nokta veya trafiği veya trafiği segmentasyonunun reddedin.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="3d2eb-149">Merhaba aşağıdaki grafikleri hello akışları akış yönü tarafından kesimli hello üst ve alt hello tarafından yapılan karar bölümlenmiş sahip ağ arabirimi başına gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="3d2eb-150">Bu bilgiyle iletilen Vm'leriniz hangisinin çoğu göreli tooothers hello ve trafik tooa belirli VM yüklenmekte olan kazanmadan izin verilen veya reddedilen.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="3d2eb-152">Halka tekerleği grafiği aşağıdaki hello hedef bağlantı noktası tarafından akışları dökümünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="3d2eb-153">Bu bilgi ile belirtilen hello içinde kullanılan en yaygın olarak kullanılan hello hedef bağlantı noktaları görüntüleyebilirsiniz Süresi.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![Halka][9]

<span data-ttu-id="3d2eb-155">Merhaba aşağıdaki çubuk grafik hello akış NSG ve kural tarafından gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="3d2eb-156">Bu bilgiyle, hello Nsg'ler Merhaba sorumlu çoğu trafiği ve trafik hello dökümünü üzerinde bir NSG kural tarafından görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="3d2eb-158">Merhaba aşağıdaki bilgi grafikler hakkında bilgi görüntüler hello Nsg'ler hello günlüklerinde sunmak, hello dönemi ve yakalanan hello erken günlük hello tarihi yakalanan akışlarının sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="3d2eb-159">Bu bilgiler, hangi Nsg'ler hakkında bir fikir günlüğe kaydedilen ve akışlar tarih aralığını hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="3d2eb-162">Bu şablon içerir dilimleyiciler tooallow en ilgi tooview hello veriler yalnızca hello.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="3d2eb-163">Kaynak grupları, Nsg'ler ve kuralları filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="3d2eb-164">Ayrıca, 5-tanımlama bilgileri, karar ve hello günlük yazıldığı hello zaman filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![dilimleyicileri][13]

## <a name="conclusion"></a><span data-ttu-id="3d2eb-166">Sonuç</span><span class="sxs-lookup"><span data-stu-id="3d2eb-166">Conclusion</span></span>

<span data-ttu-id="3d2eb-167">Bu senaryoda Ağ İzleyicisi'ni ve Power BI tarafından sağlanan ağ güvenlik grubu akış günlükleri'ni kullanarak, biz mümkün toovisualize ve hello trafiği anlamak olduğundan gösterdi.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="3d2eb-168">Sağlanan hello şablonunu kullanarak, Power BI hello günlükleri doğrudan depolama biriminden yükler ve yerel olarak işler.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="3d2eb-169">Geçen süre tooload hello şablon istenen dosyaları hello sayısına bağlı olarak değişir ve dosyaların toplam boyutu yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="3d2eb-170">Bu şablon, gereksinimleriniz için ücretsiz toocustomize eşitleyerek.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="3d2eb-171">Ağ güvenlik grubu akış günlükleri ile Power BI kullanabileceğiniz birçok pek çok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="3d2eb-172">Notlar</span><span class="sxs-lookup"><span data-stu-id="3d2eb-172">Notes</span></span>

* <span data-ttu-id="3d2eb-173">Günlükler varsayılan olarak depolanır`https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="3d2eb-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="3d2eb-174">Diğer verileri başka bir dizinde olup olmadığını sorgular toopull hello ve işlem hello verileri değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="3d2eb-175">sağlanan hello şablonu 1 GB'den fazla günlükleri ile kullanım için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="3d2eb-176">Günlükleri, büyük bir miktarını varsa, Data Lake veya SQL server gibi başka bir veri deposunu kullanan bir çözüm araştırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="3d2eb-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d2eb-177">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3d2eb-177">Next Steps</span></span>

<span data-ttu-id="3d2eb-178">Toovisualize NSG akışınız hello Elastick yığını ile ziyaret ederek nasıl oturum öğrenin [açık kaynaklı araçları kullanarak, Vm'lerden gelen ağ trafiği desenlerini tooand Görselleştirme](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="3d2eb-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
