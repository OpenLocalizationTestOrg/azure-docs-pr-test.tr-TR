---
title: "aaaOn içi veri ağ geçidi | Microsoft Docs"
description: "Bir şirket içi ağ geçidi, Azure Analysis Services sunucunuzun tooon içi veri kaynaklarına bağlanacak ise gereklidir."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="98117-103">Azure şirket içi veri ağ geçidi ile tooon içi veri kaynaklarına bağlanma</span><span class="sxs-lookup"><span data-stu-id="98117-103">Connecting tooon-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="98117-104">Merhaba şirket içi veri ağ geçidi, şirket içi veri kaynakları ve Azure Analysis Services sunucularınızı hello bulutta arasında güvenli veri aktarımını sağlayan bir köprü gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="98117-104">hello on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in hello cloud.</span></span> <span data-ttu-id="98117-105">Toplama tooworking hello birden çok Azure Analysis Services sunucusu ile aynı bölgede, hello hello ağ geçidinin en son sürümünü de Azure Logic Apps, Power BI, güç uygulamaları ve Microsoft Flow ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="98117-105">In addition tooworking with multiple Azure Analysis Services servers in hello same region, hello latest version of hello gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="98117-106">Birden çok Hizmetleri'nde hello ilişkilendirebilirsiniz tek bir ağ geçidi ile aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="98117-106">You can associate multiple services in hello same region with a single gateway.</span></span> 

 <span data-ttu-id="98117-107">Azure Analysis Services gerektiren bir ağ geçidi kaynağı hello aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="98117-107">Azure Analysis Services requires a gateway resource in hello same region.</span></span> <span data-ttu-id="98117-108">Örneğin, Azure Analysis Services sunucuları hello Doğu ABD 2 bölgede varsa, bir ağ geçidi kaynağı hello Doğu ABD 2 bölgesindeki gerekir.</span><span class="sxs-lookup"><span data-stu-id="98117-108">For example, if you have Azure Analysis Services servers in hello East US 2 region, you need a gateway resource in hello East US 2 region.</span></span> <span data-ttu-id="98117-109">Doğu ABD 2 birden çok sunucuya hello kullanabilirsiniz aynı ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="98117-109">Multiple servers in East US 2 can use hello same gateway.</span></span>

<span data-ttu-id="98117-110">İlk kez hello ağ geçidi hello ile kurulumun tamamlanmasında dört bölümden oluşan bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="98117-110">Getting setup with hello gateway hello first time is a four-part process:</span></span>

- <span data-ttu-id="98117-111">**Kurulumunu indirin ve çalıştırın** -Bu adım, kuruluşunuzdaki bir bilgisayarda bir ağ geçidi hizmeti yükler.</span><span class="sxs-lookup"><span data-stu-id="98117-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="98117-112">**Ağ geçidini kaydetmek** - Bu adımda, bir ad belirtin ve kurtarma anahtarı, ağ geçidiniz için ve ağ geçidiniz hello ağ geçidi bulut hizmeti ile kaydetme bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="98117-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with hello Gateway Cloud Service.</span></span>

- <span data-ttu-id="98117-113">**Bir ağ geçidi kaynağı oluşturma** -Bu adımda, Azure aboneliğinizde bir ağ geçidi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98117-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="98117-114">**Sunucuları tooyour ağ geçidi kaynağına bağlanmasına** -aboneliğinizde bir ağ geçidi kaynağına sahip olduğunda, sunucuları tooit bağlanma başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98117-114">**Connect your servers tooyour gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers tooit.</span></span>

<span data-ttu-id="98117-115">Aboneliğiniz için yapılandırılmış bir ağ geçidi kaynağına sahip olduğunda, birden çok sunucu ve diğer hizmetleri tooit bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="98117-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services tooit.</span></span> <span data-ttu-id="98117-116">Yalnızca tooinstall faklı bir ağ geçidi gerekir ve farklı bir bölgede sunucuları veya diğer hizmetler varsa ek ağ geçidi kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98117-116">You only need tooinstall a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="98117-117">hemen kullanmaya tooget bkz [yüklemek ve şirket içi veri ağ geçidi yapılandırma](analysis-services-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="98117-117">tooget started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="98117-118"><a name="how-it-works"></a>Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="98117-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="98117-119">bir bilgisayara yüklemeniz, kuruluşunuzda hello ağ geçidi çalıştıran bir Windows hizmeti olarak **şirket içi veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="98117-119">hello gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="98117-120">Bu yerel hizmet hello Azure Service Bus aracılığıyla ağ geçidi bulut hizmetine kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="98117-120">This local service is registered with hello Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="98117-121">Ardından Azure aboneliğiniz için bir ağ geçidi kaynağı ağ geçidi bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98117-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="98117-122">Ardından sunuculardır, Azure Analysis Services tooyour ağ geçidi kaynağına bağlandı.</span><span class="sxs-lookup"><span data-stu-id="98117-122">Your Azure Analysis Services servers are then connected tooyour gateway resource.</span></span> <span data-ttu-id="98117-123">İçi sunucu ihtiyacını tooconnect tooyour modellerinde sorgular veya işlem için veri kaynakları, bir sorgu ve veri akış ilişkilerinden geçen hello ağ geçidi kaynağı, Azure Service Bus, yerel şirket içi veri ağ geçidi hizmeti ve veri kaynaklarınızı hello.</span><span class="sxs-lookup"><span data-stu-id="98117-123">When models on your server need tooconnect tooyour on-premises data sources for queries or processing, a query and data flow traverses hello gateway resource, Azure Service Bus, hello local on-premises data gateway service, and your data sources.</span></span> 

![Nasıl çalışır?](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="98117-125">Sorgular ve veri akış:</span><span class="sxs-lookup"><span data-stu-id="98117-125">Queries and data flow:</span></span>

1. <span data-ttu-id="98117-126">Bir sorgu hello şirket içi veri kaynağı için hello şifreli kimlik bilgileriyle hello bulut hizmeti tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="98117-126">A query is created by hello cloud service with hello encrypted credentials for hello on-premises data source.</span></span> <span data-ttu-id="98117-127">Ardından, tooa sıra hello ağ geçidi tooprocess için de gönderdi.</span><span class="sxs-lookup"><span data-stu-id="98117-127">It's then sent tooa queue for hello gateway tooprocess.</span></span>
2. <span data-ttu-id="98117-128">Merhaba ağ geçidi bulut Hizmeti'ne hello sorgu analiz eder ve hello isteği toohello iter [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="98117-128">hello gateway cloud service analyzes hello query and pushes hello request toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="98117-129">Merhaba şirket içi veri ağ geçidi hello Azure hizmet veri yolu için bekleyen istekler yoklar.</span><span class="sxs-lookup"><span data-stu-id="98117-129">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="98117-130">Hello ağ geçidi hello sorgu alır, hello kimlik şifresini çözer ve toohello veri kaynakları söz konusu kimlik bilgileriyle bağlanır.</span><span class="sxs-lookup"><span data-stu-id="98117-130">hello gateway gets hello query, decrypts hello credentials, and connects toohello data sources with those credentials.</span></span>
5. <span data-ttu-id="98117-131">Merhaba ağ geçidi hello sorgu toohello veri kaynağı için yürütme gönderir.</span><span class="sxs-lookup"><span data-stu-id="98117-131">hello gateway sends hello query toohello data source for execution.</span></span>
6. <span data-ttu-id="98117-132">Merhaba sonuçları hello veri kaynağından geri toohello ağ geçidi, ardından hello bulut hizmeti ve sunucunuz üzerine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="98117-132">hello results are sent from hello data source, back toohello gateway, and then onto hello cloud service and your server.</span></span>

## <span data-ttu-id="98117-133"><a name="windows-service-account"></a>Windows hizmet hesabı</span><span class="sxs-lookup"><span data-stu-id="98117-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="98117-134">Merhaba şirket içi veri ağ geçidi olduğu yapılandırılmış toouse *NT SERVICE\PBIEgwService* hello Windows hizmeti oturum açma kimlik bilgileri için.</span><span class="sxs-lookup"><span data-stu-id="98117-134">hello on-premises data gateway is configured toouse *NT SERVICE\PBIEgwService* for hello Windows service logon credential.</span></span> <span data-ttu-id="98117-135">Varsayılan olarak, bir hizmet olarak oturum açmada sağ hello sahiptir; Merhaba ağ geçidi yüklüyorsanız hello makine Hello bağlamında.</span><span class="sxs-lookup"><span data-stu-id="98117-135">By default, it has hello right of Logon as a service; in hello context of hello machine that you are installing hello gateway on.</span></span> <span data-ttu-id="98117-136">Bu kimlik bilgileri, aynı kullanılan hesap tooconnect tooon içi veri kaynakları veya Azure hesabınızda hello değil.</span><span class="sxs-lookup"><span data-stu-id="98117-136">This credential is not hello same account used tooconnect tooon-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="98117-137">Proxy sunucunuzu sorunlarla karşılaşırsanız tooauthentication, hello Windows hizmet hesabı tooa etki alanı kullanıcı ya da yönetilen toochange isteyebilir hizmet hesabı.</span><span class="sxs-lookup"><span data-stu-id="98117-137">If you encounter issues with your proxy server due tooauthentication, you may want toochange hello Windows service account tooa domain user or managed service account.</span></span>

## <span data-ttu-id="98117-138"><a name="ports"></a>Bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="98117-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="98117-139">Merhaba ağ geçidi giden bağlantı tooAzure hizmet veri yolu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="98117-139">hello gateway creates an outbound connection tooAzure Service Bus.</span></span> <span data-ttu-id="98117-140">Giden bağlantı noktaları iletişim kurar: TCP 443 (varsayılan), 5671, 5672, 9354 aracılığıyla 9350.</span><span class="sxs-lookup"><span data-stu-id="98117-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="98117-141">Merhaba ağ geçidi gelen bağlantı noktalarının gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="98117-141">hello gateway does not require inbound ports.</span></span>

<span data-ttu-id="98117-142">Beyaz liste hello IP adresleri, Güvenlik Duvarı'nda, veri bölgesinin öneririz.</span><span class="sxs-lookup"><span data-stu-id="98117-142">We recommend you whitelist hello IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="98117-143">Merhaba indirebilirsiniz [Microsoft Azure veri merkezi IP listesi](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="98117-143">You can download hello [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="98117-144">Bu liste haftalık güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="98117-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="98117-145">Merhaba IP hello Azure veri merkezi IP listesinde listelenen CIDR gösteriminde adresleridir.</span><span class="sxs-lookup"><span data-stu-id="98117-145">hello IP Addresses listed in hello Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="98117-146">Örneğin, 10.0.0.0/24 10.0.0.24 aracılığıyla 10.0.0.0 anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="98117-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="98117-147">Merhaba hakkında daha fazla bilgi [CIDR gösteriminde](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="98117-147">Learn more about hello [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="98117-148">Merhaba, hello ağ geçidi tarafından kullanılan hello tam olarak nitelenmiş etki alanı adlarını verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="98117-148">hello following are hello fully qualified domain names used by hello gateway.</span></span>

| <span data-ttu-id="98117-149">Etki alanı adları</span><span class="sxs-lookup"><span data-stu-id="98117-149">Domain names</span></span> | <span data-ttu-id="98117-150">Giden bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="98117-150">Outbound ports</span></span> | <span data-ttu-id="98117-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="98117-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98117-152">*. powerbı.com</span><span class="sxs-lookup"><span data-stu-id="98117-152">*.powerbi.com</span></span> |<span data-ttu-id="98117-153">80</span><span class="sxs-lookup"><span data-stu-id="98117-153">80</span></span> |<span data-ttu-id="98117-154">HTTP toodownload hello yükleyici kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98117-154">HTTP used toodownload hello installer.</span></span> |
| <span data-ttu-id="98117-155">*. powerbı.com</span><span class="sxs-lookup"><span data-stu-id="98117-155">*.powerbi.com</span></span> |<span data-ttu-id="98117-156">443</span><span class="sxs-lookup"><span data-stu-id="98117-156">443</span></span> |<span data-ttu-id="98117-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="98117-157">HTTPS</span></span> |
| <span data-ttu-id="98117-158">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="98117-158">*.analysis.windows.net</span></span> |<span data-ttu-id="98117-159">443</span><span class="sxs-lookup"><span data-stu-id="98117-159">443</span></span> |<span data-ttu-id="98117-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="98117-160">HTTPS</span></span> |
| <span data-ttu-id="98117-161">*. login.windows.net</span><span class="sxs-lookup"><span data-stu-id="98117-161">*.login.windows.net</span></span> |<span data-ttu-id="98117-162">443</span><span class="sxs-lookup"><span data-stu-id="98117-162">443</span></span> |<span data-ttu-id="98117-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="98117-163">HTTPS</span></span> |
| <span data-ttu-id="98117-164">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="98117-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="98117-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="98117-165">5671-5672</span></span> |<span data-ttu-id="98117-166">Gelişmiş Message Queuing Protokolü (AMQP)</span><span class="sxs-lookup"><span data-stu-id="98117-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="98117-167">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="98117-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="98117-168">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="98117-168">443, 9350-9354</span></span> |<span data-ttu-id="98117-169">Hizmet veri yolu geçişi (erişim denetimi belirteci alımı için 443'ü gerektirir) TCP üzerinden üzerindeki dinleyicileri</span><span class="sxs-lookup"><span data-stu-id="98117-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="98117-170">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="98117-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="98117-171">443</span><span class="sxs-lookup"><span data-stu-id="98117-171">443</span></span> |<span data-ttu-id="98117-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="98117-172">HTTPS</span></span> |
| <span data-ttu-id="98117-173">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="98117-173">*.core.windows.net</span></span> |<span data-ttu-id="98117-174">443</span><span class="sxs-lookup"><span data-stu-id="98117-174">443</span></span> |<span data-ttu-id="98117-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="98117-175">HTTPS</span></span> |
| <span data-ttu-id="98117-176">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="98117-176">login.microsoftonline.com</span></span> |<span data-ttu-id="98117-177">443</span><span class="sxs-lookup"><span data-stu-id="98117-177">443</span></span> |<span data-ttu-id="98117-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="98117-178">HTTPS</span></span> |
| <span data-ttu-id="98117-179">*. msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="98117-179">*.msftncsi.com</span></span> |<span data-ttu-id="98117-180">443</span><span class="sxs-lookup"><span data-stu-id="98117-180">443</span></span> |<span data-ttu-id="98117-181">Merhaba ağ geçidi hello Power BI hizmeti tarafından erişilemediğinde tootest internet bağlantısı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98117-181">Used tootest internet connectivity if hello gateway is unreachable by hello Power BI service.</span></span> |
| <span data-ttu-id="98117-182">*.microsoftonline p.com</span><span class="sxs-lookup"><span data-stu-id="98117-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="98117-183">443</span><span class="sxs-lookup"><span data-stu-id="98117-183">443</span></span> |<span data-ttu-id="98117-184">Yapılandırmasına bağlı olarak kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98117-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="98117-185"><a name="force-https"></a>Azure Service Bus ile HTTPS iletişimi zorlama</span><span class="sxs-lookup"><span data-stu-id="98117-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="98117-186">Doğrudan TCP yerine HTTPS kullanarak Azure Service Bus ile Merhaba ağ geçidi toocommunicate zorlayabilirsiniz; Ancak, bunun nedenle performansı büyük ölçüde düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="98117-186">You can force hello gateway toocommunicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="98117-187">Merhaba değiştirebileceğiniz *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* başlangıç değerinden değiştirerek dosya `AutoDetect` çok`Https`.</span><span class="sxs-lookup"><span data-stu-id="98117-187">You can modify hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing hello value from `AutoDetect` too`Https`.</span></span> <span data-ttu-id="98117-188">Bu genellikle bir dosyadır *C:\Program Files\On içi veri ağ geçidi*.</span><span class="sxs-lookup"><span data-stu-id="98117-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="98117-189"><a name="faq"></a>Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="98117-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="98117-190">Genel</span><span class="sxs-lookup"><span data-stu-id="98117-190">General</span></span>

<span data-ttu-id="98117-191">**Q**: bir ağ geçidi hello bulutta Azure SQL veritabanı gibi veri kaynakları için ihtiyacım var?</span><span class="sxs-lookup"><span data-stu-id="98117-191">**Q**: Do I need a gateway for data sources in hello cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="98117-192">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="98117-192">
**A**: No.</span></span> <span data-ttu-id="98117-193">Bir ağ geçidi tooon içi veri kaynakları yalnızca bağlanır.</span><span class="sxs-lookup"><span data-stu-id="98117-193">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="98117-194">**Q**: hello ağ geçidi aynı makine hello veri kaynağı olarak hello yüklü toobe sahip mi?</span><span class="sxs-lookup"><span data-stu-id="98117-194">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="98117-195">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="98117-195">
**A**: No.</span></span> <span data-ttu-id="98117-196">Merhaba ağ geçidi sağlanan hello bağlantı bilgilerini kullanarak toohello veri kaynağına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="98117-196">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="98117-197">Bu bağlamda bir istemci uygulaması olarak Hello ağ geçidi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="98117-197">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="98117-198">Merhaba ağ geçidi yalnızca, genellikle hello üzerinde aynı sağlanan hello yetenek tooconnect toohello sunucu adı gerekiyor ağ.</span><span class="sxs-lookup"><span data-stu-id="98117-198">hello gateway just needs hello capability tooconnect toohello server name that was provided, typically on hello same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="98117-199">**Q**: neden ı toouse bir iş gerekir veya Okul hesabı toosign?</span><span class="sxs-lookup"><span data-stu-id="98117-199">**Q**: Why do I need toouse a work or school account toosign in?</span></span> <br/><span data-ttu-id="98117-200">
**A**: yalnızca Azure bir iş veya Okul hesabınız hello şirket içi veri ağ geçidi yüklediğinizde.</span><span class="sxs-lookup"><span data-stu-id="98117-200">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="98117-201">Oturum açma hesabınızın Azure Active Directory (Azure AD) tarafından yönetilen bir kiracı depolanır.</span><span class="sxs-lookup"><span data-stu-id="98117-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="98117-202">Genellikle, Azure AD hesabınızın kullanıcı asıl adı (UPN) hello e-posta adresi ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="98117-202">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="98117-203">**Q**: kimlik bilgilerimi depolandığı?</span><span class="sxs-lookup"><span data-stu-id="98117-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="98117-204">
**A**: bir veri kaynağı için girdiğiniz hello kimlik bilgileri şifrelenir ve hello ağ geçidi bulut Hizmeti'ne depolanır.</span><span class="sxs-lookup"><span data-stu-id="98117-204">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello Gateway Cloud Service.</span></span> <span data-ttu-id="98117-205">Merhaba kimlik hello şirket içi veri ağ geçidi şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="98117-205">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="98117-206">**Q**: ağ bant genişliği için tüm gereksinimleri vardır?</span><span class="sxs-lookup"><span data-stu-id="98117-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="98117-207">
**A**: ağınızı öneririz sahip bağlantısı iyi verimlilik vardır.</span><span class="sxs-lookup"><span data-stu-id="98117-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="98117-208">Her ortam farklıdır ve gönderilen verilerin miktarını hello hello sonuçları etkiler.</span><span class="sxs-lookup"><span data-stu-id="98117-208">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="98117-209">ExpressRoute kullanarak şirket içi ve hello Azure veri merkezleri arasında işleme düzeyini tooguarantee yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="98117-209">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="98117-210">Merhaba üçüncü taraf aracı Azure hızı Test uygulama toohelp ölçer, üretilen iş kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98117-210">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="98117-211">**Q**: hello gecikmesi çalışan sorguları tooa veri kaynağından hello ağ geçidi nedir?</span><span class="sxs-lookup"><span data-stu-id="98117-211">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="98117-212">Merhaba en iyi mimarisi nedir?</span><span class="sxs-lookup"><span data-stu-id="98117-212">What is hello best architecture?</span></span> <br/><span data-ttu-id="98117-213">
**A**: tooreduce ağ gecikmesi, mümkün olduğunca yakın toohello veri kaynağı olarak yükleme hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="98117-213">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="98117-214">Merhaba gerçek veri kaynağında hello ağ geçidi yükleyebilirsiniz, bu yakınlık sunulan hello gecikme süresi en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="98117-214">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="98117-215">Merhaba veri merkezleri çok göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="98117-215">Consider hello datacenters too.</span></span> <span data-ttu-id="98117-216">Örneğin, hizmetiniz hello Batı ABD datacenter kullanır ve SQL Server'ın bir Azure VM ile barındırılan olması durumunda, Azure VM hello Batı ABD çok olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98117-216">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="98117-217">Bu yakınlık gecikme süresi en aza indirir ve çıkış ücretlerini hello Azure VM üzerinde önler.</span><span class="sxs-lookup"><span data-stu-id="98117-217">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="98117-218">**Q**: gönderilen sonuçları geri toohello bulut şeklini?</span><span class="sxs-lookup"><span data-stu-id="98117-218">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="98117-219">
**A**: sonuçları hello Azure Service Bus gönderilir.</span><span class="sxs-lookup"><span data-stu-id="98117-219">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="98117-220">**Q**: tüm gelen bağlantıları toohello ağ geçidi'nden hello bulut vardır?</span><span class="sxs-lookup"><span data-stu-id="98117-220">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="98117-221">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="98117-221">
**A**: No.</span></span> <span data-ttu-id="98117-222">Merhaba ağ geçidi giden bağlantılar tooAzure hizmet veri yolu kullanır.</span><span class="sxs-lookup"><span data-stu-id="98117-222">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="98117-223">**Q**: ne ı giden bağlantıları engelle?</span><span class="sxs-lookup"><span data-stu-id="98117-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="98117-224">Ne tooopen gerekir?</span><span class="sxs-lookup"><span data-stu-id="98117-224">What do I need tooopen?</span></span> <br/><span data-ttu-id="98117-225">
**A**: hello bağlantı noktaları ve ağ geçidi kullanan hello konakları bakın.</span><span class="sxs-lookup"><span data-stu-id="98117-225">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="98117-226">**Q**: ne hello gerçek Windows hizmeti adı verilir?</span><span class="sxs-lookup"><span data-stu-id="98117-226">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="98117-227">
**A**: Services'de hello ağ geçidi şirket içi veri ağ geçidi hizmeti olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="98117-227">
**A**: In Services, hello gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="98117-228">**Q**: ağ geçidi Windows hizmeti bir Azure Active Directory hesap ile çalıştırmak hello?</span><span class="sxs-lookup"><span data-stu-id="98117-228">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="98117-229">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="98117-229">
**A**: No.</span></span> <span data-ttu-id="98117-230">Merhaba Windows hizmeti geçerli bir Windows hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98117-230">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="98117-231">Varsayılan olarak, hello ile hizmet SID, NT SERVICE\PBIEgwService hello hizmeti çalışır.</span><span class="sxs-lookup"><span data-stu-id="98117-231">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="98117-232"><a name="high-availability"></a>Yüksek kullanılabilirlik ve olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="98117-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="98117-233">**Q**: olağanüstü durum kurtarma için kullanılabilir seçenekleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="98117-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="98117-234">
**A**: hello kurtarma anahtarı toorestore kullanın veya bir ağ geçidi taşıyın.</span><span class="sxs-lookup"><span data-stu-id="98117-234">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="98117-235">Merhaba ağ geçidi yüklediğinizde hello kurtarma anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="98117-235">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="98117-236">**Q**: hello kurtarma anahtarı hello avantajı nedir?</span><span class="sxs-lookup"><span data-stu-id="98117-236">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="98117-237">
**A**: hello kurtarma anahtarı bir şekilde toomigrate sağlar veya ağ geçidi ayarlarınızı sonra bir olağanüstü durum kurtarma.</span><span class="sxs-lookup"><span data-stu-id="98117-237">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="98117-238"><a name="troubleshooting"></a>Sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="98117-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="98117-239">**Q**: nasıl sorguları toohello şirket içi veri kaynağına gönderilen görebilir?</span><span class="sxs-lookup"><span data-stu-id="98117-239">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="98117-240">
**A**: gönderilen hello sorgular sorgu izlemeyi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98117-240">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="98117-241">Sorun giderme tamamlanınca toohello özgün değeri geri izleme toochange sorgu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="98117-241">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="98117-242">Sorgu izlemesi açık bırakarak daha büyük günlükleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="98117-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="98117-243">Ayrıca, izleme sorguları için veri kaynağınız olan araçlar da bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98117-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="98117-244">Örneğin, SQL Server ve Analysis Services için genişletilmiş olaylar veya SQL Profiler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98117-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="98117-245">**Q**: hello gateway günlükleri nerede?</span><span class="sxs-lookup"><span data-stu-id="98117-245">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="98117-246">
**A**: Bu konunun ilerleyen bölümlerinde günlüklere bakın.</span><span class="sxs-lookup"><span data-stu-id="98117-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="98117-247"><a name="update"></a>Güncelleştirme toohello en son sürümü</span><span class="sxs-lookup"><span data-stu-id="98117-247"><a name="update"></a>Update toohello latest version</span></span>

<span data-ttu-id="98117-248">Merhaba ağ geçidi sürümü güncel olmayan hale geldiğinde birçok sorunları ortaya.</span><span class="sxs-lookup"><span data-stu-id="98117-248">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="98117-249">Genel iyi uygulama olarak, hello en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="98117-249">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="98117-250">Merhaba ağ geçidi için ayda bir veya daha uzun güncelleştirmediyseniz hello hello ağ geçidinin en son sürümünü yüklemeyi göz önünde bulundurun ve hello sorunu yeniden bakın.</span><span class="sxs-lookup"><span data-stu-id="98117-250">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="98117-251">Hata: tooadd kullanıcı toogroup başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="98117-251">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="98117-252">(-2147463168 PBIEgwService performans günlük kullanıcılar)</span><span class="sxs-lookup"><span data-stu-id="98117-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="98117-253">Desteklenmeyen bir etki alanı denetleyicisinde tooinstall hello ağ geçidi çalışırsanız, bu hatayı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98117-253">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="98117-254">Bir etki alanı denetleyicisi olmayan bir makineyi hello geçidinde dağıttığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="98117-254">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="98117-255"><a name="logs"></a>Günlükleri</span><span class="sxs-lookup"><span data-stu-id="98117-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="98117-256">Günlük dosyaları bir önemli sorun giderirken kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="98117-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="98117-257">Kurumsal ağ geçidi hizmeti günlükleri</span><span class="sxs-lookup"><span data-stu-id="98117-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="98117-258">Yapılandırma günlükleri</span><span class="sxs-lookup"><span data-stu-id="98117-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="98117-259">Olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="98117-259">Event logs</span></span>

<span data-ttu-id="98117-260">Veri Yönetimi ağ geçidi ve PowerBIGateway günlüklerini altında hello bulabilirsiniz **uygulama ve hizmet günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="98117-260">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="98117-261"><a name="telemetry"></a>Telemetri</span><span class="sxs-lookup"><span data-stu-id="98117-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="98117-262">Telemetri, izleme ve sorun giderme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="98117-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="98117-263">Varsayılan olarak</span><span class="sxs-lookup"><span data-stu-id="98117-263">By default</span></span>

<span data-ttu-id="98117-264">**telemetri üzerinde tooturn**</span><span class="sxs-lookup"><span data-stu-id="98117-264">**tooturn on telemetry**</span></span>

1.  <span data-ttu-id="98117-265">Merhaba şirket içi veri ağ geçidi istemci dizini hello bilgisayarda denetleyin.</span><span class="sxs-lookup"><span data-stu-id="98117-265">Check hello On-premises data gateway client directory on hello computer.</span></span> <span data-ttu-id="98117-266">Genellikle,. **%SystemDrive%\Program Files\On içi veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="98117-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="98117-267">Veya, Hizmetler konsolunu açın ve hello yolu tooexecutable denetleyin: hello şirket içi veri ağ geçidi hizmeti bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="98117-267">Or, you can open a Services console and check hello Path tooexecutable: A property of hello On-premises data gateway service.</span></span>
2.  <span data-ttu-id="98117-268">Merhaba Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config dosyasında istemci dizininden.</span><span class="sxs-lookup"><span data-stu-id="98117-268">In hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="98117-269">Merhaba SendTelemetry ayarı tootrue değiştirin.</span><span class="sxs-lookup"><span data-stu-id="98117-269">Change hello SendTelemetry setting tootrue.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="98117-270">Yaptığınız değişiklikleri kaydedin ve hello Windows hizmetini yeniden başlatın: şirket içi veri ağ geçidi hizmeti.</span><span class="sxs-lookup"><span data-stu-id="98117-270">Save your changes and restart hello Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="98117-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98117-271">Next steps</span></span>
* [<span data-ttu-id="98117-272">Çözümleme Hizmetleri yönetme</span><span class="sxs-lookup"><span data-stu-id="98117-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="98117-273">Azure Analysis Services Veri Al</span><span class="sxs-lookup"><span data-stu-id="98117-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
