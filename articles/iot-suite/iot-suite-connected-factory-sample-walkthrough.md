---
title: "aaaConnected Fabrika Azure IOT paketi çözümünde gezinme | Microsoft Docs"
description: "Hello Azure IOT önceden yapılandırılmış çözüm açıklaması Fabrika ve mimarisinin bağlı."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="55369-103">Önceden yapılandırılmış bağlı fabrika çözüm kılavuzu</span><span class="sxs-lookup"><span data-stu-id="55369-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="55369-104">Merhaba IOT paketi bağlı Fabrika [önceden yapılandırılmış çözüm] [ lnk-preconfigured-solutions] uçtan uca endüstriyel çözümünü uygulamasıdır:</span><span class="sxs-lookup"><span data-stu-id="55369-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="55369-105">OPC UA sunucuları benzetimli Fabrika Üretim satırları ve gerçek OPC UA sunucu cihazlarda çalışan benzetimli tooboth endüstriyel aygıtlarını bağlar.</span><span class="sxs-lookup"><span data-stu-id="55369-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="55369-106">Merhaba OPC UA hakkında daha fazla bilgi için bkz: [bağlı Fabrika SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="55369-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="55369-107">Bu cihazların ve üretim hatlarının işlem KPI ve OEE değerlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="55369-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="55369-108">Bulut tabanlı bir uygulama OPC UA sunucu sistemleri ile kullanılan toointeract nasıl olabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="55369-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="55369-109">Tooconnect kendi OPC UA sunucusu aygıtları sağlar.</span><span class="sxs-lookup"><span data-stu-id="55369-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="55369-110">Toobrowse sağlar ve hello OPC UA sunucu verilerini değiştirme.</span><span class="sxs-lookup"><span data-stu-id="55369-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="55369-111">OPC UA sunucularınızdan hello veri özelleştirilmiş görünümleri Hello Azure zaman serisi Öngörüler (TSI) hizmeti tooprovide ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="55369-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="55369-112">Merhaba çözüm kendi uygulamanız için bir başlangıç noktası olarak kullanabilirsiniz ve [özelleştirme] [ lnk-customize] , toomeet kendi belirli iş gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="55369-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="55369-113">Bu makalede bazı temel öğeleri bağlı hello Fabrika çözüm tooenable hello anlatılmaktadır nasıl çalıştığını toounderstand.</span><span class="sxs-lookup"><span data-stu-id="55369-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="55369-114">Bu bilgiler şunları yapmanıza yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="55369-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="55369-115">Merhaba çözümde sorunları giderin.</span><span class="sxs-lookup"><span data-stu-id="55369-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="55369-116">Plan nasıl toocustomize toohello çözüm toomeet belirli gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="55369-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="55369-117">Azure hizmetlerini kullanan kendi IoT çözümünüzü tasarlama.</span><span class="sxs-lookup"><span data-stu-id="55369-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="55369-118">Daha fazla bilgi için bkz: Merhaba [bağlı Fabrika SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="55369-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="55369-119">Mantıksal mimari</span><span class="sxs-lookup"><span data-stu-id="55369-119">Logical architecture</span></span>

<span data-ttu-id="55369-120">Diyagram aşağıdaki hello hello hello önceden yapılandırılmış çözümün mantıksal bileşenlerinin ana hatların vermektedir:</span><span class="sxs-lookup"><span data-stu-id="55369-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Bağlı fabrika mantıksal mimarisi][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="55369-122">Kimlik doğrulaması desenleri</span><span class="sxs-lookup"><span data-stu-id="55369-122">Communication patterns</span></span>

<span data-ttu-id="55369-123">Merhaba çözüm kullanır hello [OPC UA Pub/alt belirtimi](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend JSON biçiminde OPC UA telemetri verileri tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="55369-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="55369-124">Merhaba çözüm kullanır hello [OPC yayımcı](https://github.com/Azure/iot-edge-opc-publisher) bu amaç için IOT kenar modülü.</span><span class="sxs-lookup"><span data-stu-id="55369-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="55369-125">Merhaba çözümü, ayrıca şirket içi OPC UA sunucuları ile bağlantı kurabilir bir web uygulaması tümleşik bir OPC UA istemcisi vardır.</span><span class="sxs-lookup"><span data-stu-id="55369-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="55369-126">Merhaba istemcinin kullandığı bir [ters proxy](https://wikipedia.org/wiki/Reverse_proxy) ve açık bağlantı noktalarını hello şirket içi Güvenlik Duvarı'nda gerek kalmadan IOT hub'ı toomake hello bağlantısından Yardım alır.</span><span class="sxs-lookup"><span data-stu-id="55369-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="55369-127">Bu iletişim deseni [hizmet destekli iletişim](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/) olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="55369-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="55369-128">Merhaba çözüm kullanır hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) bu amaç için IOT kenar modülü.</span><span class="sxs-lookup"><span data-stu-id="55369-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="55369-129">Benzetim</span><span class="sxs-lookup"><span data-stu-id="55369-129">Simulation</span></span>

<span data-ttu-id="55369-130">Sanal istasyonlar ve benzetimli hello üretim yürütme sistemleri (MES) bir Fabrika üretim hizalamak olun hello.</span><span class="sxs-lookup"><span data-stu-id="55369-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="55369-131">Merhaba sanal cihazlar ve hello OPC yayımcı modülü üzerinde hello dayalı [OPC UA .NET standart] [ lnk-OPC-UA-NET-Standard] hello OPC Foundation tarafından yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="55369-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="55369-132">Merhaba OPC Proxy ve OPC yayımcı modülleri dayalı olarak uygulanan [Azure IOT kenar][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="55369-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="55369-133">Her sanal üretim hattına bağlı, atanmış bir ağ geçidi bulunur.</span><span class="sxs-lookup"><span data-stu-id="55369-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="55369-134">Tüm benzetim bileşenleri bir Azure Linux VM’sinde barındırılan Docker kapsayıcıları içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="55369-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="55369-135">Merhaba benzetimi yapılandırılmış toorun sekiz sanal üretim varsayılan satırdır.</span><span class="sxs-lookup"><span data-stu-id="55369-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="55369-136">Sanal üretim hattı</span><span class="sxs-lookup"><span data-stu-id="55369-136">Simulated production line</span></span>

<span data-ttu-id="55369-137">Üretim hattı, parça üretir.</span><span class="sxs-lookup"><span data-stu-id="55369-137">A production line manufactures parts.</span></span> <span data-ttu-id="55369-138">Farklı istasyonlardan oluşur: derleme istasyonu, test istasyonu ve paketleme istasyonu.</span><span class="sxs-lookup"><span data-stu-id="55369-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="55369-139">Merhaba benzetimi çalışır ve hello OPC UA düğümleri kullanıma sunulan hello verileri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="55369-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="55369-140">Tüm sanal üretim hattı istasyonları, hello OPC UA aracılığıyla MES tarafından düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="55369-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="55369-141">Sanal üretim yürütme sistemi</span><span class="sxs-lookup"><span data-stu-id="55369-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="55369-142">Merhaba MES hello üretim satırı OPC UA toodetect istasyon durumu değiştiğinde aracılığıyla her istasyon izler.</span><span class="sxs-lookup"><span data-stu-id="55369-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="55369-143">OPC UA yöntemleri toocontrol hello istasyonları çağırır ve tamamlanıncaya kadar bir ürün bir istasyon toohello sonraki geçirir.</span><span class="sxs-lookup"><span data-stu-id="55369-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="55369-144">Ağ geçidi OPC yayımcı modülü</span><span class="sxs-lookup"><span data-stu-id="55369-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="55369-145">OPC yayımcı modülü toohello istasyon OPC UA sunucularını bağlar ve yayımlanan toohello OPC düğümleri toobe abone olur.</span><span class="sxs-lookup"><span data-stu-id="55369-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="55369-146">Merhaba modülü hello düğümü verileri JSON biçimine dönüştürür, onu şifreler ve tooIoT Hub OPC UA Pub/alt iletileri olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="55369-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="55369-147">Hello OPC yayımcı modülü yalnızca bir giden https bağlantı noktası (443) gerektirir ve var olan kuruluş altyapısı ile çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55369-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="55369-148">Ağ geçidi OPC proxy modülü</span><span class="sxs-lookup"><span data-stu-id="55369-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="55369-149">ağ geçidi OPC UA Proxy modülü Hello ikili OPC UA komut ve Denetim iletileri tünelleri ve yalnızca giden https bağlantı noktası (443) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="55369-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="55369-150">Web Proxy’leri dahil olmak üzere, mevcut kuruluş altyapısı ile birlikte çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="55369-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="55369-151">IOT Hub cihaz yöntemleri packetized tootransfer TCP/IP'yi veri hello uygulama katmanında kullanır ve böylece uç nokta güven, veri şifreleme ve SSL/TLS kullanarak bütünlüğü sağlar.</span><span class="sxs-lookup"><span data-stu-id="55369-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="55369-152">Merhaba OPC UA ikili Protokolü hello proxy üzerinden kendisini geçişli UA kimlik doğrulama ve şifreleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="55369-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="55369-153">Azure Zaman Serisi Görüşleri</span><span class="sxs-lookup"><span data-stu-id="55369-153">Azure Time Series Insights</span></span>

<span data-ttu-id="55369-154">ağ geçidi OPC yayımcı modülü Hello tooOPC UA server düğümleri toodetect değişiklik hello veri değerleri abone olur.</span><span class="sxs-lookup"><span data-stu-id="55369-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="55369-155">Bir veri değişikliği hello düğümlerinden biri algılanırsa, bu modül iletileri tooAzure IOT hub'ı sonra gönderir.</span><span class="sxs-lookup"><span data-stu-id="55369-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="55369-156">IOT hub'ı bir olay kaynağı tooAzure TSI sağlar.</span><span class="sxs-lookup"><span data-stu-id="55369-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="55369-157">TSI depoları veri damgalarının bağlı olarak 30 gün için toohello iletileri bağlı.</span><span class="sxs-lookup"><span data-stu-id="55369-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="55369-158">Bu veriler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="55369-158">This data includes:</span></span>

* <span data-ttu-id="55369-159">OPC UA ApplicationUri</span><span class="sxs-lookup"><span data-stu-id="55369-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="55369-160">OPC UA NodeId</span><span class="sxs-lookup"><span data-stu-id="55369-160">OPC UA NodeId</span></span>
* <span data-ttu-id="55369-161">Merhaba düğümünün değeri</span><span class="sxs-lookup"><span data-stu-id="55369-161">Value of hello node</span></span>
* <span data-ttu-id="55369-162">Kaynak zaman damgası</span><span class="sxs-lookup"><span data-stu-id="55369-162">Source timestamp</span></span>
* <span data-ttu-id="55369-163">OPC UA DisplayName</span><span class="sxs-lookup"><span data-stu-id="55369-163">OPC UA DisplayName</span></span>

<span data-ttu-id="55369-164">Şu anda TSI müşteriler izin vermiyor toocustomize ne kadar süreyle tookeep hello verilerini istedikleri.</span><span class="sxs-lookup"><span data-stu-id="55369-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="55369-165">TSI bir SearchSpan (Time.From, Time.To) kullanarak düğüme karşı sorgulama yapar ve OPC UA ApplicationUri ya da OPC UA NodeId veya OPC UA DisplayName’e göre toplar.</span><span class="sxs-lookup"><span data-stu-id="55369-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="55369-166">tooretrieve hello veri hello OEE ve KPI ölçerler ve hello zaman serisi grafikler, veriler için olayları, Sum, Avg, Min ve Max sayısına göre toplanır.</span><span class="sxs-lookup"><span data-stu-id="55369-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="55369-167">Merhaba zaman serisi, farklı bir işlem kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="55369-167">hello time series are built using a different process.</span></span> <span data-ttu-id="55369-168">OEE ve KPI'leri istasyon temel verilerinden hesaplanır ve hello topolojisi (Üretim satırları, oluşturucuları, Kurumsal) için hello uygulamada kabarcıklanma.</span><span class="sxs-lookup"><span data-stu-id="55369-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="55369-169">Buna ek olarak, görüntülenen bir timespan hazır olduğunda OEE ve KPI topolojisi için zaman serisi hello uygulamada hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="55369-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="55369-170">Örneğin, hello gün görünümü tam saatte bir güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="55369-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="55369-171">Merhaba zaman serisi düğümü verilerin görünümünü doğrudan bir toplama için timespan kullanarak TSI gelir.</span><span class="sxs-lookup"><span data-stu-id="55369-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="55369-172">IoT Hub’ı</span><span class="sxs-lookup"><span data-stu-id="55369-172">IoT Hub</span></span>
<span data-ttu-id="55369-173">Merhaba [IOT hub'ı] [ lnk-IoT Hub] hello OPC yayımcı modülü hello buluta gönderilen verileri alır ve kullanılabilir toohello Azure TSI hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="55369-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="55369-174">Merhaba IOT hub'ı hello çözümde de:</span><span class="sxs-lookup"><span data-stu-id="55369-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="55369-175">Tüm OPC yayımcı modülü ve tüm OPC Proxy modülleri için hello kimliklerini depolar kimlik kayıt defteri tutar.</span><span class="sxs-lookup"><span data-stu-id="55369-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="55369-176">Taşıma kanalını hello OPC Proxy modülü çift yönlü iletişimi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="55369-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="55369-177">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="55369-177">Azure Storage</span></span>
<span data-ttu-id="55369-178">Merhaba çözüm hello VM ve toostore veri dağıtımı için disk depolama alanı olarak Azure blob depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="55369-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="55369-179">Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="55369-179">Web app</span></span>
<span data-ttu-id="55369-180">bir tümleşik OPC UA istemci, işleme uyarıları ve telemetri görselleştirme oluşur hello önceden yapılandırılmış çözümün bir parçası olarak dağıtılan hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="55369-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55369-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="55369-181">Next steps</span></span>

<span data-ttu-id="55369-182">Makaleler hello okuyarak IOT paketi ile çalışmaya başlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="55369-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="55369-183">[Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="55369-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="55369-184">Windows veya Linux üzerinde bir ağ geçidi bağlı hello Fabrika önceden yapılandırılmış çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="55369-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
