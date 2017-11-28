---
title: "aaaEnable erişim tooAzure DC/OS kapsayıcı uygulama | Microsoft Docs"
description: "Nasıl tooenable genel, Azure kapsayıcı hizmeti tooDC/OS kapsayıcılarında erişin."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a><span data-ttu-id="a788a-104">Genel erişim tooan Azure kapsayıcı hizmeti uygulamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a788a-104">Enable public access tooan Azure Container Service application</span></span>
<span data-ttu-id="a788a-105">Merhaba ACS herhangi bir DC/OS kapsayıcısına [ortak aracı havuzu](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) otomatik olarak sunulan toohello olan Internet.</span><span class="sxs-lookup"><span data-stu-id="a788a-105">Any DC/OS container in hello ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed toohello internet.</span></span> <span data-ttu-id="a788a-106">Varsayılan olarak, bağlantı noktaları **80**, **443**, **8080** açık olan ve bu bağlantı noktalarını dinler tüm (Genel) kapsayıcı erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a788a-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="a788a-107">Bu makale size nasıl tooopen daha uygulamalarınızı Azure kapsayıcı hizmeti için bağlantı noktalarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a788a-107">This article shows you how tooopen more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="a788a-108">Bağlantı noktası (portal) açın</span><span class="sxs-lookup"><span data-stu-id="a788a-108">Open a port (portal)</span></span>
<span data-ttu-id="a788a-109">İlk olarak, istiyoruz tooopen hello bağlantı noktası gerekir.</span><span class="sxs-lookup"><span data-stu-id="a788a-109">First, we need tooopen hello port we want.</span></span>

1. <span data-ttu-id="a788a-110">Toohello Portalı'nda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a788a-110">Log in toohello portal.</span></span>
2. <span data-ttu-id="a788a-111">Dağıttığınız Bul hello kaynak grubu hello Azure kapsayıcı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a788a-111">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="a788a-112">Merhaba aracı yük dengeleyicinin seçin (adlandırılmış benzer çok**XXXX-aracı-lb-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="a788a-112">Select hello agent load balancer (which is named similar too**XXXX-agent-lb-XXXX**).</span></span>
   
    ![Azure kapsayıcı hizmeti yük dengeleyici](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="a788a-114">Tıklatın **yoklamaları** ve ardından **eklemek**.</span><span class="sxs-lookup"><span data-stu-id="a788a-114">Click **Probes** and then **Add**.</span></span>
   
    ![Azure kapsayıcı hizmeti yük dengeleyici yoklamaları](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="a788a-116">Merhaba araştırma formu doldurun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a788a-116">Fill out hello probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="a788a-117">Alan</span><span class="sxs-lookup"><span data-stu-id="a788a-117">Field</span></span> | <span data-ttu-id="a788a-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a788a-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="a788a-119">Ad</span><span class="sxs-lookup"><span data-stu-id="a788a-119">Name</span></span> |<span data-ttu-id="a788a-120">Merhaba araştırma, açıklayıcı bir ad.</span><span class="sxs-lookup"><span data-stu-id="a788a-120">A descriptive name of hello probe.</span></span> |
   | <span data-ttu-id="a788a-121">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="a788a-121">Port</span></span> |<span data-ttu-id="a788a-122">Merhaba kapsayıcı tootest Hello bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="a788a-122">hello port of hello container tootest.</span></span> |
   | <span data-ttu-id="a788a-123">Yol</span><span class="sxs-lookup"><span data-stu-id="a788a-123">Path</span></span> |<span data-ttu-id="a788a-124">(HTTP modunda olduğunda) göreli Web sitesi yolu tooprobe hello.</span><span class="sxs-lookup"><span data-stu-id="a788a-124">(When in HTTP mode) hello relative website path tooprobe.</span></span> <span data-ttu-id="a788a-125">HTTPS desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a788a-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="a788a-126">aralığı</span><span class="sxs-lookup"><span data-stu-id="a788a-126">Interval</span></span> |<span data-ttu-id="a788a-127">saniye cinsinden araştırma arasındaki süre miktarı Hello çalışır.</span><span class="sxs-lookup"><span data-stu-id="a788a-127">hello amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="a788a-128">Sağlıksız durum eşiği.</span><span class="sxs-lookup"><span data-stu-id="a788a-128">Unhealthy threshold</span></span> |<span data-ttu-id="a788a-129">Arka arkaya araştırma sayısı hello kapsayıcı sağlıksız olduğunu düşünmeden önce çalışır.</span><span class="sxs-lookup"><span data-stu-id="a788a-129">Number of consecutive probe attempts before considering hello container unhealthy.</span></span> |
6. <span data-ttu-id="a788a-130">Geri hello hello aracı yük dengeleyicinin, Özellikler **Yük Dengeleme kuralları** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a788a-130">Back at hello properties of hello agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Azure kapsayıcı hizmeti yük dengeleyici kuralları](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="a788a-132">Merhaba yük dengeleyici formu doldurun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a788a-132">Fill out hello load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="a788a-133">Alan</span><span class="sxs-lookup"><span data-stu-id="a788a-133">Field</span></span> | <span data-ttu-id="a788a-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a788a-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="a788a-135">Ad</span><span class="sxs-lookup"><span data-stu-id="a788a-135">Name</span></span> |<span data-ttu-id="a788a-136">Merhaba yük dengeleyicinin açıklayıcı bir ad.</span><span class="sxs-lookup"><span data-stu-id="a788a-136">A descriptive name of hello load balancer.</span></span> |
   | <span data-ttu-id="a788a-137">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="a788a-137">Port</span></span> |<span data-ttu-id="a788a-138">Merhaba genel gelen bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="a788a-138">hello public incoming port.</span></span> |
   | <span data-ttu-id="a788a-139">Arka uç bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="a788a-139">Backend port</span></span> |<span data-ttu-id="a788a-140">Merhaba ortak iç hello kapsayıcı tooroute trafik için bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="a788a-140">hello internal-public port of hello container tooroute traffic to.</span></span> |
   | <span data-ttu-id="a788a-141">Arka uç havuzu</span><span class="sxs-lookup"><span data-stu-id="a788a-141">Backend pool</span></span> |<span data-ttu-id="a788a-142">Bu havuz Merhaba kapsayıcılara Bu yük dengeleyici için hello hedef olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a788a-142">hello containers in this pool will be hello target for this load balancer.</span></span> |
   | <span data-ttu-id="a788a-143">Araştırma</span><span class="sxs-lookup"><span data-stu-id="a788a-143">Probe</span></span> |<span data-ttu-id="a788a-144">bir hedef durumunda hello araştırma toodetermine hello **arka uç havuzu** iyi değil.</span><span class="sxs-lookup"><span data-stu-id="a788a-144">hello probe used toodetermine if a target in hello **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="a788a-145">Oturum kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="a788a-145">Session persistence</span></span> |<span data-ttu-id="a788a-146">Merhaba hello oturumu süresince bir istemciden gelen trafiğin nasıl işleneceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="a788a-146">Determines how traffic from a client should be handled for hello duration of hello session.</span></span><br><br><span data-ttu-id="a788a-147">**Hiçbiri**: aynı istemci tüm kapsayıcı tarafından işlenebilir hello gelen art arda gelen istekleri.</span><span class="sxs-lookup"><span data-stu-id="a788a-147">**None**: Successive requests from hello same client can be handled by any container.</span></span><br><span data-ttu-id="a788a-148">**İstemci IP**: aynı istemci IP tarafından işlenmesini hello gelen art arda gelen istekleri hello aynı kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="a788a-148">**Client IP**: Successive requests from hello same client IP are handled by hello same container.</span></span><br><span data-ttu-id="a788a-149">**İstemci IP ve Protokolü**: aynı istemci IP ve protokol birleşimi tarafından işlenmesini hello gelen art arda gelen istekleri hello aynı kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="a788a-149">**Client IP and protocol**: Successive requests from hello same client IP and protocol combination are handled by hello same container.</span></span> |
   | <span data-ttu-id="a788a-150">Boşta kalma zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="a788a-150">Idle timeout</span></span> |<span data-ttu-id="a788a-151">(Yalnızca TCP) Dakika cinsinden süre tookeep TCP/HTTP İstemcisi'ni açmak öğesine bağlı kalmadan hello *tutma* iletileri.</span><span class="sxs-lookup"><span data-stu-id="a788a-151">(TCP only) In minutes, hello time tookeep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="a788a-152">Güvenlik Kuralı (portal) Ekle</span><span class="sxs-lookup"><span data-stu-id="a788a-152">Add a security rule (portal)</span></span>
<span data-ttu-id="a788a-153">Ardından, tooadd hello güvenlik duvarı üzerinden bizim açılmış bağlantı noktasından trafiğini yönlendiren bir güvenlik kuralı gerekir.</span><span class="sxs-lookup"><span data-stu-id="a788a-153">Next, we need tooadd a security rule that routes traffic from our opened port through hello firewall.</span></span>

1. <span data-ttu-id="a788a-154">Toohello Portalı'nda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a788a-154">Log in toohello portal.</span></span>
2. <span data-ttu-id="a788a-155">Dağıttığınız Bul hello kaynak grubu hello Azure kapsayıcı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a788a-155">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="a788a-156">Select hello **ortak** Aracısı ağ güvenlik grubu (adlandırılmış benzer çok**XXXX-aracı-genel-nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="a788a-156">Select hello **public** agent network security group (which is named similar too**XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Azure kapsayıcı hizmeti ağ güvenlik grubu](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="a788a-158">Seçin **gelen güvenlik kuralları** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a788a-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Azure kapsayıcı hizmeti ağ güvenlik grubu kuralları](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="a788a-160">Genel bağlantı noktanızın Hello güvenlik duvarı kuralı tooallow doldurun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a788a-160">Fill out hello firewall rule tooallow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="a788a-161">Alan</span><span class="sxs-lookup"><span data-stu-id="a788a-161">Field</span></span> | <span data-ttu-id="a788a-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a788a-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="a788a-163">Ad</span><span class="sxs-lookup"><span data-stu-id="a788a-163">Name</span></span> |<span data-ttu-id="a788a-164">Merhaba güvenlik duvarı kuralı, açıklayıcı bir ad.</span><span class="sxs-lookup"><span data-stu-id="a788a-164">A descriptive name of hello firewall rule.</span></span> |
   | <span data-ttu-id="a788a-165">Öncelik</span><span class="sxs-lookup"><span data-stu-id="a788a-165">Priority</span></span> |<span data-ttu-id="a788a-166">Öncelik derecesi hello kuralı için.</span><span class="sxs-lookup"><span data-stu-id="a788a-166">Priority rank for hello rule.</span></span> <span data-ttu-id="a788a-167">Merhaba alt hello sayı hello yüksek hello önceliği.</span><span class="sxs-lookup"><span data-stu-id="a788a-167">hello lower hello number hello higher hello priority.</span></span> |
   | <span data-ttu-id="a788a-168">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a788a-168">Source</span></span> |<span data-ttu-id="a788a-169">İzin verilen veya reddedilen bu kural tarafından hello gelen IP adresi aralığı toobe kısıtlayın.</span><span class="sxs-lookup"><span data-stu-id="a788a-169">Restrict hello incoming IP address range toobe allowed or denied by this rule.</span></span> <span data-ttu-id="a788a-170">Kullanım **herhangi** toonot bir kısıtlama belirtin.</span><span class="sxs-lookup"><span data-stu-id="a788a-170">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="a788a-171">Hizmet</span><span class="sxs-lookup"><span data-stu-id="a788a-171">Service</span></span> |<span data-ttu-id="a788a-172">Bu güvenlik kuralı içindir önceden tanımlanmış Hizmetleri kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="a788a-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="a788a-173">Aksi takdirde kullanmak **özel** toocreate kendi.</span><span class="sxs-lookup"><span data-stu-id="a788a-173">Otherwise use **Custom** toocreate your own.</span></span> |
   | <span data-ttu-id="a788a-174">Protokol</span><span class="sxs-lookup"><span data-stu-id="a788a-174">Protocol</span></span> |<span data-ttu-id="a788a-175">Temel trafiği kısıtlamak **TCP** veya **UDP**.</span><span class="sxs-lookup"><span data-stu-id="a788a-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="a788a-176">Kullanım **herhangi** toonot bir kısıtlama belirtin.</span><span class="sxs-lookup"><span data-stu-id="a788a-176">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="a788a-177">Bağlantı noktası aralığı</span><span class="sxs-lookup"><span data-stu-id="a788a-177">Port range</span></span> |<span data-ttu-id="a788a-178">Zaman **hizmet** olan **özel**, bu kural etkileyen bağlantı noktalarının hello aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a788a-178">When **Service** is **Custom**, specifies hello range of ports that this rule affects.</span></span> <span data-ttu-id="a788a-179">Tek bir bağlantı noktası gibi kullanabilir **80**, veya bir aralık **1024 1500**.</span><span class="sxs-lookup"><span data-stu-id="a788a-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="a788a-180">Eylem</span><span class="sxs-lookup"><span data-stu-id="a788a-180">Action</span></span> |<span data-ttu-id="a788a-181">İzin ver veya Reddet hello ölçütleri karşılayan trafiği.</span><span class="sxs-lookup"><span data-stu-id="a788a-181">Allow or deny traffic that meets hello criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a788a-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a788a-182">Next steps</span></span>
<span data-ttu-id="a788a-183">Merhaba birbirinden hakkında bilgi edinin [ortak ve özel DC/OS aracıları](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="a788a-183">Learn about hello difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="a788a-184">Hakkında daha fazla bilgi okuyun [DC/OS kapsayıcılarınızı yönetme](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="a788a-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

