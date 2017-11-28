---
title: "Azure IOT paketi aaaCustomize bağlı Fabrika | Microsoft Docs"
description: "Merhaba toocustomize hello davranışını Fabrika nasıl bağlı bir açıklama önceden yapılandırılmış çözümü."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="9aed1-103">Merhaba Fabrika çözüm görüntüler veri OPC UA sunucularınızdan nasıl bağlanacağını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="9aed1-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="9aed1-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="9aed1-104">Introduction</span></span>

<span data-ttu-id="9aed1-105">Merhaba bağlı Fabrika çözüm toplar ve hello OPC UA sunucuları bağlı toohello çözüm verileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9aed1-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="9aed1-106">Göz atın ve komutları toohello OPC UA sunucuları çözümünüzde gönderir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="9aed1-107">Merhaba OPC UA hakkında daha fazla bilgi için bkz: [bağlı Fabrika SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="9aed1-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="9aed1-108">Merhaba çözümde toplanan veri örnekleri hello genel donanım verimliliği (OEE) ve başlangıç panosunda hello Fabrika, satır ve istasyon düzeylerinde görüntüleyebileceğiniz ana performans göstergelerini (KPI'lar) içerir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="9aed1-109">Merhaba aşağıdaki ekran görüntüsünde hello OEE KPI için ve değerleri hello gösterir **derleme** istasyon, üzerinde **üretim satırı 1**, hello içinde **Münih** Fabrika:</span><span class="sxs-lookup"><span data-stu-id="9aed1-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Merhaba çözümde OEE ve KPI değerleri örneği][img-oee-kpi]

<span data-ttu-id="9aed1-111">hello çözüm etkinleştirir, tooview belirli veri öğelerinden bilgilerinden ayrıntılı olarak bilinen OPC UA sunucuları hello *istasyonları*.</span><span class="sxs-lookup"><span data-stu-id="9aed1-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="9aed1-112">Merhaba aşağıdaki ekran görüntüsü hello sayının belirli bir istasyondan üretilen öğelerinin çizimleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="9aed1-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![Çizimler üretilen öğe sayısı][img-manufactured-items]

<span data-ttu-id="9aed1-114">Merhaba grafikleri birini tıklatın, daha fazla zaman serisi Öngörüler (TSI) kullanarak hello veri da gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9aed1-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![Zaman serisi Öngörüler kullanarak verileri keşfedin][img-tsi]

<span data-ttu-id="9aed1-116">Bu makalede açıklanır:</span><span class="sxs-lookup"><span data-stu-id="9aed1-116">This article describes:</span></span>

- <span data-ttu-id="9aed1-117">Nasıl hello veri kullanılabilir toohello çeşitli görünümleri hello çözümde yapılır.</span><span class="sxs-lookup"><span data-stu-id="9aed1-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="9aed1-118">Merhaba şekilde hello çözümü nasıl özelleştirebileceğiniz hello verilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9aed1-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="9aed1-119">Veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="9aed1-119">Data sources</span></span>

<span data-ttu-id="9aed1-120">Merhaba bağlı Fabrika çözüm hello OPC UA sunucuları bağlı toohello çözüm verileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9aed1-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="9aed1-121">Merhaba varsayılan yükleme Fabrika benzetimi birkaç OPC UA sunucuları içerir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="9aed1-122">Kendi OPC UA sunucuları ekleyebilirsiniz, [bir ağ geçidi üzerinden bağlanma] [ lnk-connect-cf] tooyour çözümü.</span><span class="sxs-lookup"><span data-stu-id="9aed1-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="9aed1-123">Bağlı bir OPC UA sunucuya hello panosunda tooyour çözüm gönderebilirsiniz hello veri öğeleri göz atabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9aed1-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="9aed1-124">Toohello gidin **OPC UA sunucuyu seçin** görünümü:</span><span class="sxs-lookup"><span data-stu-id="9aed1-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![Toohello seçin OPC UA sunucu görünümü gidin][img-select-server]

1. <span data-ttu-id="9aed1-126">Bir sunucu seçin ve tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="9aed1-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="9aed1-127">Tıklatın **İlerle** zaman hello güvenlik uyarısı görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="9aed1-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9aed1-128">Bu uyarı yalnızca bir kez her sunucu için görünür ve hello çözüm Panosu hello sunucu arasında bir güven ilişkisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9aed1-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="9aed1-129">Sunucu hello Gözat hello veri öğeleri toohello çözüm gönderebilirsiniz artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aed1-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="9aed1-130">Toohello Çözüm gönderilen öğeleri yeşil bir onay işareti vardır:</span><span class="sxs-lookup"><span data-stu-id="9aed1-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![Yayımlanan öğeler][img-published]

1. <span data-ttu-id="9aed1-132">Kullanıyorsanız bir *yönetici* hello çözümde, bir veri öğesi toomake toopublish seçebilirsiniz hello kullanılabilir bağlı Fabrika çözümü.</span><span class="sxs-lookup"><span data-stu-id="9aed1-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="9aed1-133">Yönetici olarak, veri öğeleri hello değerini değiştirin ve hello OPC UA server yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9aed1-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="9aed1-134">Merhaba verileri eşleme</span><span class="sxs-lookup"><span data-stu-id="9aed1-134">Map hello data</span></span>

<span data-ttu-id="9aed1-135">Fabrika çözüm eşlemeleri Hello bağlı ve toplamalar hello hello OPC UA sunucu toohello veri öğeleri çeşitli görünümleri hello çözümde yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="9aed1-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="9aed1-136">Merhaba çözüm sağladığınızda hello bağlı Fabrika çözüm tooyour Azure hesabı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="9aed1-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="9aed1-137">Merhaba bağlı Visual Studio Fabrika çözümü JSON dosyasında bu eşleme bilgilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="9aed1-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="9aed1-138">Görüntüleyin ve bu hello bağlı Fabrika Visual Studio çözümü JSON yapılandırma dosyasında değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9aed1-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="9aed1-139">Değişikliği yaptıktan sonra hello çözümü yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aed1-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="9aed1-140">Merhaba yapılandırma dosyasına kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9aed1-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="9aed1-141">Merhaba varolan sanal oluşturucuları, Üretim satırları ve istasyonları düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="9aed1-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="9aed1-142">Toohello çözümü bağlantı gerçek OPC UA sunuculardan verileri eşleyin.</span><span class="sxs-lookup"><span data-stu-id="9aed1-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="9aed1-143">tooclone hello bir kopyasını Fabrika Visual Studio çözümü, git komut aşağıdaki kullanım hello bağlı:</span><span class="sxs-lookup"><span data-stu-id="9aed1-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="9aed1-144">Merhaba dosya **ContosoTopologyDescription.json** OPC UA sunucu verilerini hello eşleme öğeleri toohello görünümleri hello bağlı Fabrika çözüm panosunda hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9aed1-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="9aed1-145">Bu yapılandırma dosyası hello bulabilirsiniz **Contoso\Topology** hello klasöründe **WebApp** hello Visual Studio çözümü projesinde.</span><span class="sxs-lookup"><span data-stu-id="9aed1-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="9aed1-146">Merhaba JSON dosyası Merhaba içeriğine hiyerarşisini Fabrika, üretim hattı ve istasyon düğümler düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="9aed1-147">Bu hiyerarşi hello Gezinti hiyerarşisinde hello bağlı Fabrika panosunda tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9aed1-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="9aed1-148">Her düğümde hello hiyerarşisinin değerler hello panosunda görüntülenen hello bilgileri belirler.</span><span class="sxs-lookup"><span data-stu-id="9aed1-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="9aed1-149">Örneğin, hello JSON dosyası hello Münih Fabrika için değerleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="9aed1-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

<span data-ttu-id="9aed1-150">Merhaba adını, açıklamasını ve konum bu hello Pano görünümünde görünür:</span><span class="sxs-lookup"><span data-stu-id="9aed1-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![Merhaba Pano Münih verileri][img-munich]

<span data-ttu-id="9aed1-152">Her fabrika, üretim hattı ve istasyon bir görüntü özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="9aed1-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="9aed1-153">Bu JPEG dosyaları hello bulabilirsiniz **Content\img** hello klasöründe **WebApp** projesi.</span><span class="sxs-lookup"><span data-stu-id="9aed1-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="9aed1-154">Bu görüntü dosyalar hello bağlı Fabrika panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="9aed1-155">Her istasyon OPC UA hello veri öğeleri eşleme hello tanımlayan çeşitli ayrıntılı özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="9aed1-156">Bu özellikleri hello aşağıdaki bölümlerde açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="9aed1-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="9aed1-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="9aed1-157">OpcUri</span></span>

<span data-ttu-id="9aed1-158">Merhaba **OpcUri** hello OPC UA uygulama URI'hello OPC UA sunucu benzersiz olarak tanıtan bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="9aed1-159">Örneğin, hello **OpcUri** hello derleme istasyon Münih 1 satırda üretim hello şuna benzeyen için bir değer: **urn: scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="9aed1-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="9aed1-160">Merhaba çözüm panosunda hello bağlı hello OPC UA sunucularının URI'ler görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9aed1-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![OPC UA sunucusu URI görüntülemek][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="9aed1-162">Benzetim</span><span class="sxs-lookup"><span data-stu-id="9aed1-162">Simulation</span></span>

<span data-ttu-id="9aed1-163">Merhaba hello bilgilerinde **benzetimi** belirli toohello hello varsayılan olarak sağlanan OPC UA sunucuları çalıştıran OPC UA benzetimi düğümdür.</span><span class="sxs-lookup"><span data-stu-id="9aed1-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="9aed1-164">Gerçek bir OPC UA sunucusu için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="9aed1-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="9aed1-165">Kpi1 ve kpı2</span><span class="sxs-lookup"><span data-stu-id="9aed1-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="9aed1-166">Bu düğümler hello istasyon verilerden toohello iki KPI değerleri hello panosunda nasıl katkıda açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9aed1-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="9aed1-167">Varsayılan dağıtımında, bu KPI saat başına birim ve saatte kWh değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="9aed1-168">Merhaba çözüm KPI değerlerinde bir istasyonun hello düzeyinde hesaplar ve bunları hello üretim hattı ve Fabrika düzeylerinde toplar.</span><span class="sxs-lookup"><span data-stu-id="9aed1-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="9aed1-169">Her KPI minimum, maksimum ve hedef değer vardır.</span><span class="sxs-lookup"><span data-stu-id="9aed1-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="9aed1-170">Her bir KPI değeri bağlı hello Fabrika çözüm tooperform için uyarı eylemleri de tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aed1-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="9aed1-171">Merhaba aşağıdaki kod parçacığında hello KPI hello derleme istasyon tanımlarında satırdaki üretim Münih 1 gösterir:</span><span class="sxs-lookup"><span data-stu-id="9aed1-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

<span data-ttu-id="9aed1-172">Merhaba aşağıdaki ekran görüntüsünde hello KPI verileri hello panosunda gösterir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![KPI bilgilerini hello panosunda][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="9aed1-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="9aed1-174">OpcNodes</span></span>

<span data-ttu-id="9aed1-175">Merhaba **OpcNodes** düğümleri tanımlamak hello OPC UA sunucu yayımlanan veri öğeleri hello ve belirtin nasıl tooprocess verileri.</span><span class="sxs-lookup"><span data-stu-id="9aed1-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="9aed1-176">Merhaba **nodeId** değeri tanımlar hello hello OPC UA sunucu gelen belirli OPC UA nodeId.</span><span class="sxs-lookup"><span data-stu-id="9aed1-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="9aed1-177">Merhaba ilk düğüm hello derleme istasyon üretim satırının Münih 1 değerine sahip **ns = 2; ı 385 =**.</span><span class="sxs-lookup"><span data-stu-id="9aed1-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="9aed1-178">A **nodeId** değeri belirten hello veri öğesi tooread hello OPC UA sunucu ve hello **SymbolicName** bu veriler için bir kolay ad toouse hello panosunda sağlar.</span><span class="sxs-lookup"><span data-stu-id="9aed1-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="9aed1-179">Her düğüm ile ilişkili diğer değerler, aşağıdaki tablonun hello özetlenmiştir:</span><span class="sxs-lookup"><span data-stu-id="9aed1-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="9aed1-180">Değer</span><span class="sxs-lookup"><span data-stu-id="9aed1-180">Value</span></span> | <span data-ttu-id="9aed1-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9aed1-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9aed1-182">İlgi Düzeyi</span><span class="sxs-lookup"><span data-stu-id="9aed1-182">Relevance</span></span>  | <span data-ttu-id="9aed1-183">Merhaba KPI'yı ve OEE değerleri için bu verileri katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="9aed1-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="9aed1-184">İşlem kodu</span><span class="sxs-lookup"><span data-stu-id="9aed1-184">OpCode</span></span>     | <span data-ttu-id="9aed1-185">Merhaba verileri nasıl toplanır.</span><span class="sxs-lookup"><span data-stu-id="9aed1-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="9aed1-186">Birimler</span><span class="sxs-lookup"><span data-stu-id="9aed1-186">Units</span></span>      | <span data-ttu-id="9aed1-187">Merhaba birimleri toouse hello panosunda.</span><span class="sxs-lookup"><span data-stu-id="9aed1-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="9aed1-188">Görünür</span><span class="sxs-lookup"><span data-stu-id="9aed1-188">Visible</span></span>    | <span data-ttu-id="9aed1-189">Toodisplay bu değer olup olmadığını hello Pano.</span><span class="sxs-lookup"><span data-stu-id="9aed1-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="9aed1-190">Bazı değerler hesaplamalarında kullanılır ancak görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="9aed1-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="9aed1-191">Maksimum</span><span class="sxs-lookup"><span data-stu-id="9aed1-191">Maximum</span></span>    | <span data-ttu-id="9aed1-192">Merhaba panosunda uyarıyı tetikleyen hello en büyük değer.</span><span class="sxs-lookup"><span data-stu-id="9aed1-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="9aed1-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="9aed1-193">MaximumAlertActions</span></span> | <span data-ttu-id="9aed1-194">Bir eylem tootake yanıt tooan uyarısında.</span><span class="sxs-lookup"><span data-stu-id="9aed1-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="9aed1-195">Örneğin, bir komut tooa istasyon gönderir.</span><span class="sxs-lookup"><span data-stu-id="9aed1-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="9aed1-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="9aed1-196">ConstValue</span></span> | <span data-ttu-id="9aed1-197">Bir hesaplanmasında kullanılan sabit bir değer.</span><span class="sxs-lookup"><span data-stu-id="9aed1-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="9aed1-198">Merhaba değişiklikleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="9aed1-198">Deploy hello changes</span></span>

<span data-ttu-id="9aed1-199">Değişiklikleri toohello yapmadan tamamladığınızda **ContosoTopologyDescription.json** gerekir dağıtmanız dosyası hello bağlı Fabrika çözüm tooyour Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="9aed1-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="9aed1-200">Merhaba **azure-IOT-bağlı-Fabrika** deposu içeren bir **build.ps1** toorebuild kullanın ve hello çözümü dağıtmak PowerShell komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="9aed1-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9aed1-201">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9aed1-201">Next Steps</span></span>

<span data-ttu-id="9aed1-202">Bağlı hello Fabrika önceden yapılandırılmış çözüm hakkında daha fazla tarafından okuma hello makaleleri aşağıdaki bilgi:</span><span class="sxs-lookup"><span data-stu-id="9aed1-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="9aed1-203">[Önceden yapılandırılmış bağlı fabrika çözümü yönergeleri][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="9aed1-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="9aed1-204">[Bağlı üreteci için bir ağ geçidi dağıtma][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="9aed1-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="9aed1-205">[Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="9aed1-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="9aed1-206">Bağlı fabrika hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="9aed1-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="9aed1-207">[SSS][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="9aed1-207">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md