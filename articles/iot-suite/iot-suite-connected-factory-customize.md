---
title: "Azure IOT paketi bağlı Fabrika özelleştirme | Microsoft Docs"
description: "Bağlı Fabrika önceden yapılandırılmış çözümün davranışını özelleştirmek nasıl açıklaması."
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
ms.openlocfilehash: 90a6172dbd887ecda5a9f5d9082a4e136092bc10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="311a5-103">Bağlı Fabrika çözüm OPC UA sunucularınızdan veri biçimini Özelleştir</span><span class="sxs-lookup"><span data-stu-id="311a5-103">Customize how the connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="311a5-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="311a5-104">Introduction</span></span>

<span data-ttu-id="311a5-105">Bağlı Fabrika çözüm toplar ve çözüme bağlı OPC UA sunuculardan verileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="311a5-105">The connected factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="311a5-106">Göz atın ve komutları OPC UA sunucularına çözümünüzde gönderir.</span><span class="sxs-lookup"><span data-stu-id="311a5-106">You can browse and send commands to the OPC UA servers in your solution.</span></span> <span data-ttu-id="311a5-107">OPC UA hakkında daha fazla bilgi için bkz. [Connected factory SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="311a5-107">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="311a5-108">Genel donanım verimliliği (OEE) ve Fabrika, satır ve istasyon düzeylerinde panosunda görüntüleyebileceğiniz ana performans göstergelerini (KPI'lar) çözümüne toplanan veri örneklerindendir.</span><span class="sxs-lookup"><span data-stu-id="311a5-108">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span></span> <span data-ttu-id="311a5-109">Aşağıdaki ekran görüntüsü için OEE ve KPI değerleri gösterir **derleme** istasyon, üzerinde **üretim satırı 1**, **Münih** Fabrika:</span><span class="sxs-lookup"><span data-stu-id="311a5-109">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span></span>

![OEE ve KPI değerleri çözümde örneği][img-oee-kpi]

<span data-ttu-id="311a5-111">Çözüm, belirli veri öğeleri olarak adlandırılan OPC UA sunucularından alınan ayrıntılı bilgileri görüntülemenize olanak tanır *istasyonları*.</span><span class="sxs-lookup"><span data-stu-id="311a5-111">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span></span> <span data-ttu-id="311a5-112">Aşağıdaki ekran çizimleri belirli bir istasyonu üretilen öğelerinden sayısının gösterir:</span><span class="sxs-lookup"><span data-stu-id="311a5-112">The following screenshot shows plots of the number of manufactured items from a specific station:</span></span>

![Çizimler üretilen öğe sayısı][img-manufactured-items]

<span data-ttu-id="311a5-114">Aşağıdakilerden grafikleri tıklarsanız, verileri daha fazla zaman serisi Öngörüler (TSI) kullanarak da gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="311a5-114">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span></span>

![Zaman serisi Öngörüler kullanarak verileri keşfedin][img-tsi]

<span data-ttu-id="311a5-116">Bu makalede açıklanır:</span><span class="sxs-lookup"><span data-stu-id="311a5-116">This article describes:</span></span>

- <span data-ttu-id="311a5-117">Nasıl veri çözümde çeşitli görünümleri için kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="311a5-117">How the data is made available to the various views in the solution.</span></span>
- <span data-ttu-id="311a5-118">Çözüm şekilde nasıl özelleştirebileceğiniz verileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="311a5-118">How you can customize the way the solution displays the data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="311a5-119">Veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="311a5-119">Data sources</span></span>

<span data-ttu-id="311a5-120">Bağlı Fabrika çözüm çözüme bağlı OPC UA sunuculardan verileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="311a5-120">The connected factory solution displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="311a5-121">Varsayılan yükleme Fabrika benzetimi birkaç OPC UA sunucuları içerir.</span><span class="sxs-lookup"><span data-stu-id="311a5-121">The default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="311a5-122">Kendi OPC UA sunucuları ekleyebilirsiniz, [bir ağ geçidi üzerinden bağlanma] [ lnk-connect-cf] çözümünüze.</span><span class="sxs-lookup"><span data-stu-id="311a5-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span></span>

<span data-ttu-id="311a5-123">Pano çözümünüzde bağlı OPC UA sunucu gönderebilir veri öğelerini göz atabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="311a5-123">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span></span>

1. <span data-ttu-id="311a5-124">Gidin **OPC UA sunucuyu seçin** görünümü:</span><span class="sxs-lookup"><span data-stu-id="311a5-124">Navigate to the **Select an OPC UA server** view:</span></span>

    ![OPC UA sunucu görünümü seçin gidin][img-select-server]

1. <span data-ttu-id="311a5-126">Bir sunucu seçin ve tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="311a5-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="311a5-127">Tıklatın **İlerle** zaman güvenlik uyarısı görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="311a5-127">Click **Proceed** when the security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="311a5-128">Bu uyarı yalnızca bir kez her sunucu için görünür ve çözüm panosu ve sunucu arasında bir güven ilişkisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="311a5-128">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span></span>

1. <span data-ttu-id="311a5-129">Sunucu çözüme gönderebilirsiniz veri öğelerini gözatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="311a5-129">You can now browse the data items that the server can send to the solution.</span></span> <span data-ttu-id="311a5-130">Çözüme gönderilen öğeleri yeşil bir onay işareti vardır:</span><span class="sxs-lookup"><span data-stu-id="311a5-130">Items that are being sent to the solution have a green check mark:</span></span>

    ![Yayımlanan öğeler][img-published]

1. <span data-ttu-id="311a5-132">Kullanıyorsanız bir *yönetici* çözümde bağlı Fabrika çözümde kullanılabilir hale getirmek için bir veri öğesi yayımlamayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="311a5-132">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the connected factory solution.</span></span> <span data-ttu-id="311a5-133">Yönetici olarak, veri öğeleri değerini değiştirin ve OPC UA Server'da yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="311a5-133">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span></span>

## <a name="map-the-data"></a><span data-ttu-id="311a5-134">Verileri eşleme</span><span class="sxs-lookup"><span data-stu-id="311a5-134">Map the data</span></span>

<span data-ttu-id="311a5-135">Bağlı Fabrika çözüm eşler ve çeşitli görünümlere çözümdeki OPC UA sunucudan yayımlanan veri öğelerini toplar.</span><span class="sxs-lookup"><span data-stu-id="311a5-135">The connected factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span></span> <span data-ttu-id="311a5-136">Bir çözüm sağladığınızda Azure hesabınıza bağlı Fabrika çözümü dağıtır.</span><span class="sxs-lookup"><span data-stu-id="311a5-136">The connected factory solution deploys to your Azure account when you provision the solution.</span></span> <span data-ttu-id="311a5-137">Visual Studio bağlı Fabrika çözümü JSON dosyasında bu eşleme bilgilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="311a5-137">A JSON file in the Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="311a5-138">Görüntüleyin ve bu bağlantılı Fabrika Visual Studio çözümü JSON yapılandırma dosyasında değiştirin.</span><span class="sxs-lookup"><span data-stu-id="311a5-138">You can view and modify this JSON configuration file in the connected factory Visual Studio solution.</span></span> <span data-ttu-id="311a5-139">Değişikliği yaptıktan sonra çözümü yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="311a5-139">You can redeploy the solution after you make a change.</span></span>

<span data-ttu-id="311a5-140">Yapılandırma dosyası kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="311a5-140">You can use the configuration file to:</span></span>

- <span data-ttu-id="311a5-141">Varolan sanal oluşturucuları, Üretim satırları ve istasyonları düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="311a5-141">Edit the existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="311a5-142">Çözümü arasında bağlantı gerçek OPC UA sunuculardan verileri eşleyin.</span><span class="sxs-lookup"><span data-stu-id="311a5-142">Map data from real OPC UA servers that you connect to the solution.</span></span>

<span data-ttu-id="311a5-143">Visual Studio çözümü bağlı Fabrika kopyasını kopyalamak için aşağıdaki git komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="311a5-143">To clone a copy of the connected factory Visual Studio solution, use the following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="311a5-144">Dosya **ContosoTopologyDescription.json** bağlı Fabrika çözüm panosunda OPC UA sunucu veri öğeleri eşleme görünümleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="311a5-144">The file **ContosoTopologyDescription.json** defines the mapping from the OPC UA server data items to the views in the connected factory solution dashboard.</span></span> <span data-ttu-id="311a5-145">Bu yapılandırma dosyasında bulabilirsiniz **Contoso\Topology** klasöründe **WebApp** Visual Studio çözümü projesinde.</span><span class="sxs-lookup"><span data-stu-id="311a5-145">You can find this configuration file in the **Contoso\Topology** folder in the **WebApp** project in the Visual Studio solution.</span></span>

<span data-ttu-id="311a5-146">JSON dosyasının içeriği Fabrika, üretim hattı ve istasyon düğümleri hiyerarşi olarak düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="311a5-146">The content of the JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="311a5-147">Bu hiyerarşi Gezinti hiyerarşisinde bağlı Fabrika panosunda tanımlar.</span><span class="sxs-lookup"><span data-stu-id="311a5-147">This hierarchy defines the navigation hierarchy in the connected factory dashboard.</span></span> <span data-ttu-id="311a5-148">Hiyerarşinin her düğümde değerler panosunda görüntülenen bilgileri belirler.</span><span class="sxs-lookup"><span data-stu-id="311a5-148">Values at each node of the hierarchy determine the information displayed in the dashboard.</span></span> <span data-ttu-id="311a5-149">Örneğin, JSON dosyası Münih Fabrika için aşağıdaki değerleri içerir:</span><span class="sxs-lookup"><span data-stu-id="311a5-149">For example, the JSON file contains the following values for the Munich factory:</span></span>

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

<span data-ttu-id="311a5-150">Adını, açıklamasını ve konum bu Pano görünümünde görünür:</span><span class="sxs-lookup"><span data-stu-id="311a5-150">The name, description, and location appear on this view in the dashboard:</span></span>

![Pano Münih verileri][img-munich]

<span data-ttu-id="311a5-152">Her fabrika, üretim hattı ve istasyon bir görüntü özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="311a5-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="311a5-153">Bu JPEG dosyaları bulabilirsiniz **Content\img** klasöründe **WebApp** projesi.</span><span class="sxs-lookup"><span data-stu-id="311a5-153">You can find these JPEG files in the **Content\img** folder in the **WebApp** project.</span></span> <span data-ttu-id="311a5-154">Bu görüntü dosyalar bağlı Fabrika panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="311a5-154">These image files display in the connected factory dashboard.</span></span>

<span data-ttu-id="311a5-155">Her istasyon OPC UA veri öğeleri eşlemesinden tanımlayan çeşitli ayrıntılı özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="311a5-155">Each station includes several detailed properties that define the mapping from the OPC UA data items.</span></span> <span data-ttu-id="311a5-156">Bu özellikler aşağıdaki bölümlerde açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="311a5-156">These properties are described in the following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="311a5-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="311a5-157">OpcUri</span></span>

<span data-ttu-id="311a5-158">**OpcUri** OPC UA sunucunun benzersiz olarak tanıtan OPC UA uygulama URI bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="311a5-158">The **OpcUri** value is the OPC UA Application URI that uniquely identifies the OPC UA server.</span></span> <span data-ttu-id="311a5-159">Örneğin, **OpcUri** değeri 1 üretim satırında Münih derleme istasyon aşağıdaki gibi görünür: **urn: scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="311a5-159">For example, the **OpcUri** value for the assembly station on production line 1 in Munich looks like the following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="311a5-160">Çözüm panosunda URI'ler bağlı OPC UA sunucuları görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="311a5-160">You can view the URIs of the connected OPC UA servers in the solution dashboard:</span></span>

![OPC UA sunucusu URI görüntülemek][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="311a5-162">Benzetim</span><span class="sxs-lookup"><span data-stu-id="311a5-162">Simulation</span></span>

<span data-ttu-id="311a5-163">Bilgileri **benzetimi** düğümü, varsayılan olarak sağlanan OPC UA sunucularında çalışan OPC UA benzetimi için özeldir.</span><span class="sxs-lookup"><span data-stu-id="311a5-163">The information in the **Simulation** node is specific to the OPC UA simulation that runs in the OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="311a5-164">Gerçek bir OPC UA sunucusu için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="311a5-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="311a5-165">Kpi1 ve kpı2</span><span class="sxs-lookup"><span data-stu-id="311a5-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="311a5-166">Bu düğümler Pano iki KPI değerler istasyon verileri nasıl katkıda bulunan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="311a5-166">These nodes describe how data from the station contributes to the two KPI values in the dashboard.</span></span> <span data-ttu-id="311a5-167">Varsayılan dağıtımında, bu KPI saat başına birim ve saatte kWh değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="311a5-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="311a5-168">Çözüm KPI değerlerinde bir istasyon düzeyinde hesaplar ve bunları üretim hattı ve Fabrika düzeylerinde toplar.</span><span class="sxs-lookup"><span data-stu-id="311a5-168">The solution calculates KPI vales at the level of a station and aggregates them at the production line and factory levels.</span></span>

<span data-ttu-id="311a5-169">Her KPI minimum, maksimum ve hedef değer vardır.</span><span class="sxs-lookup"><span data-stu-id="311a5-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="311a5-170">Her bir KPI değeri Uyarı eylemleri gerçekleştirmek bağlı Fabrika çözüm için de tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="311a5-170">Each KPI value can also define alert actions for the connected factory solution to perform.</span></span> <span data-ttu-id="311a5-171">Aşağıdaki kod parçacığında derleme istasyon KPI tanımlarında Münih 1 üretim satırdaki gösterir:</span><span class="sxs-lookup"><span data-stu-id="311a5-171">The following snippet shows the KPI definitions for the assembly station on production line 1 in Munich:</span></span>

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

<span data-ttu-id="311a5-172">Aşağıdaki ekran görüntüsünde KPI verileri Panoda gösterir.</span><span class="sxs-lookup"><span data-stu-id="311a5-172">The following screenshot shows the KPI data in the dashboard.</span></span>

![KPI bilgilerini panosunda][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="311a5-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="311a5-174">OpcNodes</span></span>

<span data-ttu-id="311a5-175">**OpcNodes** düğümleri OPC UA sunucusundan yayımlanan veri öğelerini tanımlamak ve bu verileri işlemek nasıl belirtin.</span><span class="sxs-lookup"><span data-stu-id="311a5-175">The **OpcNodes** nodes identify the published data items from the OPC UA server and specify how to process that data.</span></span>

<span data-ttu-id="311a5-176">**NodeId** değer OPC UA sunucusundan belirli OPC UA nodeId tanımlar.</span><span class="sxs-lookup"><span data-stu-id="311a5-176">The **NodeId** value identifies the specific OPC UA NodeID from the OPC UA server.</span></span> <span data-ttu-id="311a5-177">Derleme istasyon üretim hattı Münih 1 için ilk düğüm bir değere sahip **ns = 2; ı 385 =**.</span><span class="sxs-lookup"><span data-stu-id="311a5-177">The first node in the assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="311a5-178">A **nodeId** değeri OPC UA sunucusundan okumak için veri öğesi belirtir ve **SymbolicName** bu verileri Panoda kullanmak için kullanıcı dostu bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="311a5-178">A **NodeId** value specifies the data item to read from the OPC UA server, and the **SymbolicName** provides a user-friendly name to use in the dashboard for that data.</span></span>

<span data-ttu-id="311a5-179">Her düğüm ile ilişkili diğer değerler aşağıdaki tabloda özetlenmiştir:</span><span class="sxs-lookup"><span data-stu-id="311a5-179">Other values associated with each node are summarized in the following table:</span></span>

| <span data-ttu-id="311a5-180">Değer</span><span class="sxs-lookup"><span data-stu-id="311a5-180">Value</span></span> | <span data-ttu-id="311a5-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="311a5-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="311a5-182">İlgi Düzeyi</span><span class="sxs-lookup"><span data-stu-id="311a5-182">Relevance</span></span>  | <span data-ttu-id="311a5-183">KPI'yı ve OEE değerleri için bu verileri katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="311a5-183">The KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="311a5-184">İşlem kodu</span><span class="sxs-lookup"><span data-stu-id="311a5-184">OpCode</span></span>     | <span data-ttu-id="311a5-185">Verileri nasıl toplanır.</span><span class="sxs-lookup"><span data-stu-id="311a5-185">How the data is aggregated.</span></span> |
| <span data-ttu-id="311a5-186">Birimler</span><span class="sxs-lookup"><span data-stu-id="311a5-186">Units</span></span>      | <span data-ttu-id="311a5-187">Panoda kullanılacak birim.</span><span class="sxs-lookup"><span data-stu-id="311a5-187">The units to use in the dashboard.</span></span>  |
| <span data-ttu-id="311a5-188">Görünür</span><span class="sxs-lookup"><span data-stu-id="311a5-188">Visible</span></span>    | <span data-ttu-id="311a5-189">Bu değer panosunda görüntülenip görüntülenmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="311a5-189">Whether to display this value in the dashboard.</span></span> <span data-ttu-id="311a5-190">Bazı değerler hesaplamalarında kullanılır ancak görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="311a5-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="311a5-191">Maksimum</span><span class="sxs-lookup"><span data-stu-id="311a5-191">Maximum</span></span>    | <span data-ttu-id="311a5-192">Panodaki bir uyarıyı tetikleyen en yüksek değer.</span><span class="sxs-lookup"><span data-stu-id="311a5-192">The maximum value that triggers an alert in the dashboard.</span></span> |
| <span data-ttu-id="311a5-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="311a5-193">MaximumAlertActions</span></span> | <span data-ttu-id="311a5-194">Yanıt bir uyarı olarak gerçekleştirilecek bir eylem.</span><span class="sxs-lookup"><span data-stu-id="311a5-194">An action to take in response to an alert.</span></span> <span data-ttu-id="311a5-195">Örneğin, bir komut istasyona gönderir.</span><span class="sxs-lookup"><span data-stu-id="311a5-195">For example, send a command to a station.</span></span> |
| <span data-ttu-id="311a5-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="311a5-196">ConstValue</span></span> | <span data-ttu-id="311a5-197">Bir hesaplanmasında kullanılan sabit bir değer.</span><span class="sxs-lookup"><span data-stu-id="311a5-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-the-changes"></a><span data-ttu-id="311a5-198">Değişiklikleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="311a5-198">Deploy the changes</span></span>

<span data-ttu-id="311a5-199">Değişiklikler yapma tamamladığınızda **ContosoTopologyDescription.json** dosyası, Azure hesabınıza bağlı Fabrika çözümü yeniden dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="311a5-199">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the connected factory solution to your Azure account.</span></span>

<span data-ttu-id="311a5-200">**Azure-IOT-bağlı-Fabrika** deposu içeren bir **build.ps1** PowerShell komut dosyasını yeniden oluşturun ve çözümü dağıtmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="311a5-200">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="311a5-201">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="311a5-201">Next Steps</span></span>

<span data-ttu-id="311a5-202">Aşağıdaki makaleleri okuyarak bağlı Fabrika önceden yapılandırılmış çözüm hakkında daha fazla bilgi:</span><span class="sxs-lookup"><span data-stu-id="311a5-202">Learn more about the connected factory preconfigured solution by reading the following articles:</span></span>

* <span data-ttu-id="311a5-203">[Önceden yapılandırılmış bağlı fabrika çözümü yönergeleri][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="311a5-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="311a5-204">[Bağlı üreteci için bir ağ geçidi dağıtma][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="311a5-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="311a5-205">[azureiotsuite.com sitesindeki izinler][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="311a5-205">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="311a5-206">Bağlı fabrika hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="311a5-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="311a5-207">[SSS][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="311a5-207">[FAQ][lnk-faq]</span></span>


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