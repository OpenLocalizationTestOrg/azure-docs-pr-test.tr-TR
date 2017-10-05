---
title: "Azure DC/OS kapsayıcı uygulama erişimi etkinleştir | Microsoft Docs"
description: "Azure kapsayıcı hizmeti DC/OS kapsayıcılarında genel erişimi etkinleştirmek nasıl."
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
ms.openlocfilehash: c9ef5913859cf3a55a2de2107a9304f1d28a4829
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-public-access-to-an-azure-container-service-application"></a><span data-ttu-id="7fd64-104">Azure kapsayıcı hizmeti uygulamanın genel erişimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="7fd64-104">Enable public access to an Azure Container Service application</span></span>
<span data-ttu-id="7fd64-105">ACS herhangi bir DC/OS kapsayıcısına [ortak aracı havuzu](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) otomatik olarak internet erişimine açıktır.</span><span class="sxs-lookup"><span data-stu-id="7fd64-105">Any DC/OS container in the ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed to the internet.</span></span> <span data-ttu-id="7fd64-106">Varsayılan olarak, bağlantı noktaları **80**, **443**, **8080** açık olan ve bu bağlantı noktalarını dinler tüm (Genel) kapsayıcı erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="7fd64-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="7fd64-107">Bu makalede daha fazla bağlantı noktalarının, uygulamalarınız için Azure kapsayıcı Hizmeti'nde nasıl açılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7fd64-107">This article shows you how to open more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="7fd64-108">Bağlantı noktası (portal) açın</span><span class="sxs-lookup"><span data-stu-id="7fd64-108">Open a port (portal)</span></span>
<span data-ttu-id="7fd64-109">İlk olarak, biz biz istediğiniz bağlantı noktasını açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fd64-109">First, we need to open the port we want.</span></span>

1. <span data-ttu-id="7fd64-110">Portalda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7fd64-110">Log in to the portal.</span></span>
2. <span data-ttu-id="7fd64-111">Azure kapsayıcı hizmeti için dağıttığınız kaynak grubunu bulun.</span><span class="sxs-lookup"><span data-stu-id="7fd64-111">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="7fd64-112">Aracı yük dengeleyicinin seçin (adlandırılmış benzer **XXXX-aracı-lb-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="7fd64-112">Select the agent load balancer (which is named similar to **XXXX-agent-lb-XXXX**).</span></span>
   
    ![Azure kapsayıcı hizmeti yük dengeleyici](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="7fd64-114">Tıklatın **yoklamaları** ve ardından **eklemek**.</span><span class="sxs-lookup"><span data-stu-id="7fd64-114">Click **Probes** and then **Add**.</span></span>
   
    ![Azure kapsayıcı hizmeti yük dengeleyici yoklamaları](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="7fd64-116">Araştırma formu doldurun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7fd64-116">Fill out the probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="7fd64-117">Alan</span><span class="sxs-lookup"><span data-stu-id="7fd64-117">Field</span></span> | <span data-ttu-id="7fd64-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7fd64-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="7fd64-119">Ad</span><span class="sxs-lookup"><span data-stu-id="7fd64-119">Name</span></span> |<span data-ttu-id="7fd64-120">Yoklama, açıklayıcı bir ad.</span><span class="sxs-lookup"><span data-stu-id="7fd64-120">A descriptive name of the probe.</span></span> |
   | <span data-ttu-id="7fd64-121">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="7fd64-121">Port</span></span> |<span data-ttu-id="7fd64-122">Test etmek için kapsayıcı bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="7fd64-122">The port of the container to test.</span></span> |
   | <span data-ttu-id="7fd64-123">Yol</span><span class="sxs-lookup"><span data-stu-id="7fd64-123">Path</span></span> |<span data-ttu-id="7fd64-124">(HTTP modunda olduğunda) Araştırma göreli Web sitesi yolu.</span><span class="sxs-lookup"><span data-stu-id="7fd64-124">(When in HTTP mode) The relative website path to probe.</span></span> <span data-ttu-id="7fd64-125">HTTPS desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="7fd64-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="7fd64-126">aralığı</span><span class="sxs-lookup"><span data-stu-id="7fd64-126">Interval</span></span> |<span data-ttu-id="7fd64-127">Araştırma arasındaki süreyi saniye cinsinden çalışır.</span><span class="sxs-lookup"><span data-stu-id="7fd64-127">The amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="7fd64-128">Sağlıksız durum eşiği.</span><span class="sxs-lookup"><span data-stu-id="7fd64-128">Unhealthy threshold</span></span> |<span data-ttu-id="7fd64-129">Arka arkaya araştırma sayısı kapsayıcı sağlıksız olduğunu düşünmeden önce çalışır.</span><span class="sxs-lookup"><span data-stu-id="7fd64-129">Number of consecutive probe attempts before considering the container unhealthy.</span></span> |
6. <span data-ttu-id="7fd64-130">Geri aracı yük dengeleyicinin, Özellikler **Yük Dengeleme kuralları** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7fd64-130">Back at the properties of the agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Azure kapsayıcı hizmeti yük dengeleyici kuralları](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="7fd64-132">Yük Dengeleyici formu doldurun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7fd64-132">Fill out the load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="7fd64-133">Alan</span><span class="sxs-lookup"><span data-stu-id="7fd64-133">Field</span></span> | <span data-ttu-id="7fd64-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7fd64-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="7fd64-135">Ad</span><span class="sxs-lookup"><span data-stu-id="7fd64-135">Name</span></span> |<span data-ttu-id="7fd64-136">Yük dengeleyicinin açıklayıcı bir ad.</span><span class="sxs-lookup"><span data-stu-id="7fd64-136">A descriptive name of the load balancer.</span></span> |
   | <span data-ttu-id="7fd64-137">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="7fd64-137">Port</span></span> |<span data-ttu-id="7fd64-138">Genel gelen bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="7fd64-138">The public incoming port.</span></span> |
   | <span data-ttu-id="7fd64-139">Arka uç bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="7fd64-139">Backend port</span></span> |<span data-ttu-id="7fd64-140">Kapsayıcı trafiği yönlendirmek için ortak iç bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="7fd64-140">The internal-public port of the container to route traffic to.</span></span> |
   | <span data-ttu-id="7fd64-141">Arka uç havuzu</span><span class="sxs-lookup"><span data-stu-id="7fd64-141">Backend pool</span></span> |<span data-ttu-id="7fd64-142">Bu havuz kapsayıcılarında Bu yük dengeleyici için hedef olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7fd64-142">The containers in this pool will be the target for this load balancer.</span></span> |
   | <span data-ttu-id="7fd64-143">Araştırma</span><span class="sxs-lookup"><span data-stu-id="7fd64-143">Probe</span></span> |<span data-ttu-id="7fd64-144">Bir hedef belirlemek için kullanılan araştırma **arka uç havuzu** iyi değil.</span><span class="sxs-lookup"><span data-stu-id="7fd64-144">The probe used to determine if a target in the **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="7fd64-145">Oturum kalıcılığı</span><span class="sxs-lookup"><span data-stu-id="7fd64-145">Session persistence</span></span> |<span data-ttu-id="7fd64-146">İstemciden gelen trafiğin oturum boyunca nasıl işleneceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="7fd64-146">Determines how traffic from a client should be handled for the duration of the session.</span></span><br><br><span data-ttu-id="7fd64-147">**Hiçbiri**: aynı istemciden art arda gelen istekleri tüm kapsayıcı tarafından işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="7fd64-147">**None**: Successive requests from the same client can be handled by any container.</span></span><br><span data-ttu-id="7fd64-148">**İstemci IP**: aynı istemci IP adresinden art arda gelen istekleri aynı kapsayıcı tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="7fd64-148">**Client IP**: Successive requests from the same client IP are handled by the same container.</span></span><br><span data-ttu-id="7fd64-149">**İstemci IP ve Protokolü**: aynı istemci IP'si ve protokolü bileşiminden art arda gelen istekleri aynı kapsayıcı tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="7fd64-149">**Client IP and protocol**: Successive requests from the same client IP and protocol combination are handled by the same container.</span></span> |
   | <span data-ttu-id="7fd64-150">Boşta kalma zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="7fd64-150">Idle timeout</span></span> |<span data-ttu-id="7fd64-151">(Yalnızca TCP) Dakika cinsinden bir TCP/HTTP istemci saklama süresi açmak öğesine bağlı kalmadan *tutma* iletileri.</span><span class="sxs-lookup"><span data-stu-id="7fd64-151">(TCP only) In minutes, the time to keep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="7fd64-152">Güvenlik Kuralı (portal) Ekle</span><span class="sxs-lookup"><span data-stu-id="7fd64-152">Add a security rule (portal)</span></span>
<span data-ttu-id="7fd64-153">Ardından, şu güvenlik duvarı aracılığıyla bizim açılmış bağlantı noktasından trafiğini yönlendiren bir güvenlik kuralı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fd64-153">Next, we need to add a security rule that routes traffic from our opened port through the firewall.</span></span>

1. <span data-ttu-id="7fd64-154">Portalda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7fd64-154">Log in to the portal.</span></span>
2. <span data-ttu-id="7fd64-155">Azure kapsayıcı hizmeti için dağıttığınız kaynak grubunu bulun.</span><span class="sxs-lookup"><span data-stu-id="7fd64-155">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="7fd64-156">Seçin **ortak** Aracısı ağ güvenlik grubu (adlandırılmış benzer **XXXX-aracı-genel-nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="7fd64-156">Select the **public** agent network security group (which is named similar to **XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Azure kapsayıcı hizmeti ağ güvenlik grubu](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="7fd64-158">Seçin **gelen güvenlik kuralları** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7fd64-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Azure kapsayıcı hizmeti ağ güvenlik grubu kuralları](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="7fd64-160">' I tıklatın ve genel bağlantı noktanızın izin vermek güvenlik duvarı kuralı dolgu **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7fd64-160">Fill out the firewall rule to allow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="7fd64-161">Alan</span><span class="sxs-lookup"><span data-stu-id="7fd64-161">Field</span></span> | <span data-ttu-id="7fd64-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7fd64-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="7fd64-163">Ad</span><span class="sxs-lookup"><span data-stu-id="7fd64-163">Name</span></span> |<span data-ttu-id="7fd64-164">Güvenlik duvarı kuralı, açıklayıcı bir ad.</span><span class="sxs-lookup"><span data-stu-id="7fd64-164">A descriptive name of the firewall rule.</span></span> |
   | <span data-ttu-id="7fd64-165">Öncelik</span><span class="sxs-lookup"><span data-stu-id="7fd64-165">Priority</span></span> |<span data-ttu-id="7fd64-166">Kural için öncelik derecesi.</span><span class="sxs-lookup"><span data-stu-id="7fd64-166">Priority rank for the rule.</span></span> <span data-ttu-id="7fd64-167">Düşük sayı öncelik o kadar yüksektir.</span><span class="sxs-lookup"><span data-stu-id="7fd64-167">The lower the number the higher the priority.</span></span> |
   | <span data-ttu-id="7fd64-168">Kaynak</span><span class="sxs-lookup"><span data-stu-id="7fd64-168">Source</span></span> |<span data-ttu-id="7fd64-169">Bu kural tarafından izin verilecek ve reddedilecek şekilde gelen IP adres aralığını kısıtlayın.</span><span class="sxs-lookup"><span data-stu-id="7fd64-169">Restrict the incoming IP address range to be allowed or denied by this rule.</span></span> <span data-ttu-id="7fd64-170">Kullanım **herhangi** bir kısıtlama belirtmemek için.</span><span class="sxs-lookup"><span data-stu-id="7fd64-170">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="7fd64-171">Hizmet</span><span class="sxs-lookup"><span data-stu-id="7fd64-171">Service</span></span> |<span data-ttu-id="7fd64-172">Bu güvenlik kuralı içindir önceden tanımlanmış Hizmetleri kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="7fd64-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="7fd64-173">Aksi takdirde kullanmak **özel** kendi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7fd64-173">Otherwise use **Custom** to create your own.</span></span> |
   | <span data-ttu-id="7fd64-174">Protokol</span><span class="sxs-lookup"><span data-stu-id="7fd64-174">Protocol</span></span> |<span data-ttu-id="7fd64-175">Temel trafiği kısıtlamak **TCP** veya **UDP**.</span><span class="sxs-lookup"><span data-stu-id="7fd64-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="7fd64-176">Kullanım **herhangi** bir kısıtlama belirtmemek için.</span><span class="sxs-lookup"><span data-stu-id="7fd64-176">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="7fd64-177">Bağlantı noktası aralığı</span><span class="sxs-lookup"><span data-stu-id="7fd64-177">Port range</span></span> |<span data-ttu-id="7fd64-178">Zaman **hizmet** olan **özel**, bu kural etkileyen bağlantı noktası aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7fd64-178">When **Service** is **Custom**, specifies the range of ports that this rule affects.</span></span> <span data-ttu-id="7fd64-179">Tek bir bağlantı noktası gibi kullanabilir **80**, veya bir aralık **1024 1500**.</span><span class="sxs-lookup"><span data-stu-id="7fd64-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="7fd64-180">Eylem</span><span class="sxs-lookup"><span data-stu-id="7fd64-180">Action</span></span> |<span data-ttu-id="7fd64-181">İzin ver veya Reddet ölçütleri karşılayan trafiği.</span><span class="sxs-lookup"><span data-stu-id="7fd64-181">Allow or deny traffic that meets the criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7fd64-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7fd64-182">Next steps</span></span>
<span data-ttu-id="7fd64-183">Arasındaki farklar hakkında bilgi edinin [ortak ve özel DC/OS aracıları](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="7fd64-183">Learn about the difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="7fd64-184">Hakkında daha fazla bilgi okuyun [DC/OS kapsayıcılarınızı yönetme](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="7fd64-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

