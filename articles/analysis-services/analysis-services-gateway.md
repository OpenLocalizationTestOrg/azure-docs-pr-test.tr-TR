---
title: "Şirket içi veri ağ geçidi | Microsoft Docs"
description: "Analysis Services sunucunuzun azure'da şirket içi veri kaynağına bağlanır, bir şirket içi ağ geçidi gereklidir."
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
ms.openlocfilehash: 514b5404e8cbfa0baa657eb41736e20cad502638
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connecting-to-on-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="f1221-103">Azure şirket içi veri ağ geçidi ile şirket içi veri kaynaklarına bağlanma</span><span class="sxs-lookup"><span data-stu-id="f1221-103">Connecting to on-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="f1221-104">Şirket içi veri ağ geçidi, şirket içi veri kaynakları ve Azure Analysis Services sunucularınızı bulutta arasında güvenli veri aktarımını sağlayan bir köprü gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="f1221-104">The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in the cloud.</span></span> <span data-ttu-id="f1221-105">Aynı bölgede birden çok Azure Analysis Services sunucusu ile çalışma ek olarak, ağ geçidinin en son sürümünü de Azure Logic Apps, Power BI, güç uygulamaları ve Microsoft Flow ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="f1221-105">In addition to working with multiple Azure Analysis Services servers in the same region, the latest version of the gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="f1221-106">Tek bir ağ geçidi ile aynı bölgede birden çok hizmet ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-106">You can associate multiple services in the same region with a single gateway.</span></span> 

 <span data-ttu-id="f1221-107">Azure Analysis Services aynı bölgede bir ağ geçidi kaynağı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f1221-107">Azure Analysis Services requires a gateway resource in the same region.</span></span> <span data-ttu-id="f1221-108">Örneğin, Doğu ABD 2 bölgede Azure Analysis Services sunucuları varsa, bir ağ geçidi kaynağı Doğu ABD 2 bölgesindeki gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1221-108">For example, if you have Azure Analysis Services servers in the East US 2 region, you need a gateway resource in the East US 2 region.</span></span> <span data-ttu-id="f1221-109">Doğu ABD 2 birden çok sunucu, aynı ağ geçidi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-109">Multiple servers in East US 2 can use the same gateway.</span></span>

<span data-ttu-id="f1221-110">İlk kez ağ geçidi ile kurulumun tamamlanmasında dört bölümden oluşan bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="f1221-110">Getting setup with the gateway the first time is a four-part process:</span></span>

- <span data-ttu-id="f1221-111">**Kurulumunu indirin ve çalıştırın** -Bu adım, kuruluşunuzdaki bir bilgisayarda bir ağ geçidi hizmeti yükler.</span><span class="sxs-lookup"><span data-stu-id="f1221-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="f1221-112">**Ağ geçidini kaydetmek** - Bu adımda, bir ad belirtin ve kurtarma anahtarı, ağ geçidiniz için ve ağ geçidiniz ağ geçidi bulut hizmeti ile kaydetme bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="f1221-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with the Gateway Cloud Service.</span></span>

- <span data-ttu-id="f1221-113">**Bir ağ geçidi kaynağı oluşturma** -Bu adımda, Azure aboneliğinizde bir ağ geçidi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f1221-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="f1221-114">**Sunucularınız, ağ geçidi kaynağına bağlanma** -aboneliğinizde bir ağ geçidi kaynağına sahip olduktan sonra sunucularınız tarafından bağlanan başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-114">**Connect your servers to your gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers to it.</span></span>

<span data-ttu-id="f1221-115">Aboneliğiniz için yapılandırılmış bir ağ geçidi kaynağına sahip olduğunda, birden çok sunucu ve diğer hizmetler için bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services to it.</span></span> <span data-ttu-id="f1221-116">Faklı bir ağ geçidi yükleyin ve farklı bir bölgede sunucuları veya diğer hizmetler varsa ek ağ geçidi kaynakları oluşturun yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="f1221-116">You only need to install a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="f1221-117">Hemen kullanmaya başlamak için bkz: [yüklemek ve şirket içi veri ağ geçidi yapılandırma](analysis-services-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="f1221-117">To get started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="f1221-118"><a name="how-it-works"></a>Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="f1221-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="f1221-119">Bir bilgisayara yüklemeniz, kuruluşunuzda ağ geçidi Windows hizmeti olarak çalışan **şirket içi veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="f1221-119">The gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="f1221-120">Bu yerel hizmet Azure Service Bus aracılığıyla ağ geçidi bulut hizmetine kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="f1221-120">This local service is registered with the Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="f1221-121">Ardından Azure aboneliğiniz için bir ağ geçidi kaynağı ağ geçidi bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f1221-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="f1221-122">Azure Analysis Services sunucuları, ağ geçidi kaynağı bağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f1221-122">Your Azure Analysis Services servers are then connected to your gateway resource.</span></span> <span data-ttu-id="f1221-123">Sunucunuzdaki modelleri kaynakları sorgular veya işleme için şirket içi verilerinize bağlanın gerektiğinde, bir sorgu ve veri akışı ağ geçidi kaynağı, Azure Service Bus, yerel şirket içi veri ağ geçidi hizmeti ve veri kaynaklarınızı erişir.</span><span class="sxs-lookup"><span data-stu-id="f1221-123">When models on your server need to connect to your on-premises data sources for queries or processing, a query and data flow traverses the gateway resource, Azure Service Bus, the local on-premises data gateway service, and your data sources.</span></span> 

![Nasıl çalışır?](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="f1221-125">Sorgular ve veri akış:</span><span class="sxs-lookup"><span data-stu-id="f1221-125">Queries and data flow:</span></span>

1. <span data-ttu-id="f1221-126">Bir sorgu tarafından şifrelenmiş kimlik bilgileri bulut hizmetiyle şirket içi veri kaynağı için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f1221-126">A query is created by the cloud service with the encrypted credentials for the on-premises data source.</span></span> <span data-ttu-id="f1221-127">Daha sonra işlemek ağ geçidi için bir sırasına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f1221-127">It's then sent to a queue for the gateway to process.</span></span>
2. <span data-ttu-id="f1221-128">Ağ geçidi bulut Hizmeti'ne sorgu analiz eder ve isteği iter [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="f1221-128">The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="f1221-129">Şirket içi veri ağ geçidi bekleyen istekler için Azure Service Bus yoklar.</span><span class="sxs-lookup"><span data-stu-id="f1221-129">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="f1221-130">Ağ geçidi sorgu alır, kimlik bilgileri şifresini çözer ve veri kaynağı bu kimlik bilgileri ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f1221-130">The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.</span></span>
5. <span data-ttu-id="f1221-131">Ağ geçidi yürütme için veri kaynağı sorgusu gönderir.</span><span class="sxs-lookup"><span data-stu-id="f1221-131">The gateway sends the query to the data source for execution.</span></span>
6. <span data-ttu-id="f1221-132">Sonuçları, ağ geçidi dönün ve bulut hizmeti ve sunucunuz üzerine veri kaynağından gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f1221-132">The results are sent from the data source, back to the gateway, and then onto the cloud service and your server.</span></span>

## <span data-ttu-id="f1221-133"><a name="windows-service-account"></a>Windows hizmet hesabı</span><span class="sxs-lookup"><span data-stu-id="f1221-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="f1221-134">Şirket içi veri ağ geçidi kullanacak şekilde yapılandırılmış *NT SERVICE\PBIEgwService* Windows hizmeti oturum açma kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f1221-134">The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential.</span></span> <span data-ttu-id="f1221-135">Varsayılan olarak, bir hizmet olarak oturum açma hakkı vardır; ağ geçidi yüklüyorsanız makine bağlamında.</span><span class="sxs-lookup"><span data-stu-id="f1221-135">By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on.</span></span> <span data-ttu-id="f1221-136">Bu kimlik bilgileri, şirket içi veri kaynaklarına bağlanmak için kullanılan aynı hesap ya da Azure hesabınızda değil.</span><span class="sxs-lookup"><span data-stu-id="f1221-136">This credential is not the same account used to connect to on-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="f1221-137">Proxy sunucunuz kimlik doğrulaması nedeniyle ile sorunlarla karşılaşırsanız, Windows hizmet hesabı etki alanı kullanıcısına değiştirmek isteyebilirsiniz veya yönetilen hizmet hesabı.</span><span class="sxs-lookup"><span data-stu-id="f1221-137">If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.</span></span>

## <span data-ttu-id="f1221-138"><a name="ports"></a>Bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="f1221-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="f1221-139">Ağ geçidi, Azure Service Bus giden bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f1221-139">The gateway creates an outbound connection to Azure Service Bus.</span></span> <span data-ttu-id="f1221-140">Giden bağlantı noktaları iletişim kurar: TCP 443 (varsayılan), 5671, 5672, 9354 aracılığıyla 9350.</span><span class="sxs-lookup"><span data-stu-id="f1221-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="f1221-141">Ağ geçidi gelen bağlantı noktalarının gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="f1221-141">The gateway does not require inbound ports.</span></span>

<span data-ttu-id="f1221-142">Güvenlik Duvarı'nda, veri bölgesinin IP adreslerini güvenilir listeye öneririz.</span><span class="sxs-lookup"><span data-stu-id="f1221-142">We recommend you whitelist the IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="f1221-143">İndirebilirsiniz [Microsoft Azure veri merkezi IP listesi](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="f1221-143">You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="f1221-144">Bu liste haftalık güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f1221-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="f1221-145">Azure veri merkezi IP listesinde listelenen IP adresleri CIDR gösteriminde değil.</span><span class="sxs-lookup"><span data-stu-id="f1221-145">The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="f1221-146">Örneğin, 10.0.0.0/24 10.0.0.24 aracılığıyla 10.0.0.0 anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="f1221-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="f1221-147">Daha fazla bilgi edinmek [CIDR gösteriminde](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="f1221-147">Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="f1221-148">Ağ Geçidi tarafından kullanılan tam etki alanı adları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f1221-148">The following are the fully qualified domain names used by the gateway.</span></span>

| <span data-ttu-id="f1221-149">Etki alanı adları</span><span class="sxs-lookup"><span data-stu-id="f1221-149">Domain names</span></span> | <span data-ttu-id="f1221-150">Giden bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="f1221-150">Outbound ports</span></span> | <span data-ttu-id="f1221-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f1221-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1221-152">*. powerbı.com</span><span class="sxs-lookup"><span data-stu-id="f1221-152">*.powerbi.com</span></span> |<span data-ttu-id="f1221-153">80</span><span class="sxs-lookup"><span data-stu-id="f1221-153">80</span></span> |<span data-ttu-id="f1221-154">Yükleyici indirmek için kullanılan HTTP.</span><span class="sxs-lookup"><span data-stu-id="f1221-154">HTTP used to download the installer.</span></span> |
| <span data-ttu-id="f1221-155">*. powerbı.com</span><span class="sxs-lookup"><span data-stu-id="f1221-155">*.powerbi.com</span></span> |<span data-ttu-id="f1221-156">443</span><span class="sxs-lookup"><span data-stu-id="f1221-156">443</span></span> |<span data-ttu-id="f1221-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f1221-157">HTTPS</span></span> |
| <span data-ttu-id="f1221-158">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="f1221-158">*.analysis.windows.net</span></span> |<span data-ttu-id="f1221-159">443</span><span class="sxs-lookup"><span data-stu-id="f1221-159">443</span></span> |<span data-ttu-id="f1221-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f1221-160">HTTPS</span></span> |
| <span data-ttu-id="f1221-161">*. login.windows.net</span><span class="sxs-lookup"><span data-stu-id="f1221-161">*.login.windows.net</span></span> |<span data-ttu-id="f1221-162">443</span><span class="sxs-lookup"><span data-stu-id="f1221-162">443</span></span> |<span data-ttu-id="f1221-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f1221-163">HTTPS</span></span> |
| <span data-ttu-id="f1221-164">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="f1221-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="f1221-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="f1221-165">5671-5672</span></span> |<span data-ttu-id="f1221-166">Gelişmiş Message Queuing Protokolü (AMQP)</span><span class="sxs-lookup"><span data-stu-id="f1221-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="f1221-167">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="f1221-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="f1221-168">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="f1221-168">443, 9350-9354</span></span> |<span data-ttu-id="f1221-169">Hizmet veri yolu geçişi (erişim denetimi belirteci alımı için 443'ü gerektirir) TCP üzerinden üzerindeki dinleyicileri</span><span class="sxs-lookup"><span data-stu-id="f1221-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="f1221-170">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="f1221-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="f1221-171">443</span><span class="sxs-lookup"><span data-stu-id="f1221-171">443</span></span> |<span data-ttu-id="f1221-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f1221-172">HTTPS</span></span> |
| <span data-ttu-id="f1221-173">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f1221-173">*.core.windows.net</span></span> |<span data-ttu-id="f1221-174">443</span><span class="sxs-lookup"><span data-stu-id="f1221-174">443</span></span> |<span data-ttu-id="f1221-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f1221-175">HTTPS</span></span> |
| <span data-ttu-id="f1221-176">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="f1221-176">login.microsoftonline.com</span></span> |<span data-ttu-id="f1221-177">443</span><span class="sxs-lookup"><span data-stu-id="f1221-177">443</span></span> |<span data-ttu-id="f1221-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f1221-178">HTTPS</span></span> |
| <span data-ttu-id="f1221-179">*. msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="f1221-179">*.msftncsi.com</span></span> |<span data-ttu-id="f1221-180">443</span><span class="sxs-lookup"><span data-stu-id="f1221-180">443</span></span> |<span data-ttu-id="f1221-181">Ağ geçidi Power BI hizmeti tarafından erişilemediğinde internet bağlantısı test etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f1221-181">Used to test internet connectivity if the gateway is unreachable by the Power BI service.</span></span> |
| <span data-ttu-id="f1221-182">*.microsoftonline p.com</span><span class="sxs-lookup"><span data-stu-id="f1221-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="f1221-183">443</span><span class="sxs-lookup"><span data-stu-id="f1221-183">443</span></span> |<span data-ttu-id="f1221-184">Yapılandırmasına bağlı olarak kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f1221-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="f1221-185"><a name="force-https"></a>Azure Service Bus ile HTTPS iletişimi zorlama</span><span class="sxs-lookup"><span data-stu-id="f1221-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="f1221-186">Doğrudan TCP yerine HTTPS kullanarak Azure Service Bus ile iletişim kurmak için ağ geçidi zorlayabilirsiniz; Ancak, bunun nedenle performansı büyük ölçüde düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="f1221-186">You can force the gateway to communicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="f1221-187">Değiştirebileceğiniz *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* değerini değiştirerek dosya `AutoDetect` için `Https`.</span><span class="sxs-lookup"><span data-stu-id="f1221-187">You can modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing the value from `AutoDetect` to `Https`.</span></span> <span data-ttu-id="f1221-188">Bu genellikle bir dosyadır *C:\Program Files\On içi veri ağ geçidi*.</span><span class="sxs-lookup"><span data-stu-id="f1221-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="f1221-189"><a name="faq"></a>Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="f1221-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="f1221-190">Genel</span><span class="sxs-lookup"><span data-stu-id="f1221-190">General</span></span>

<span data-ttu-id="f1221-191">**Q**: bir ağ geçidi bulutta Azure SQL veritabanı gibi veri kaynakları için ihtiyacım var?</span><span class="sxs-lookup"><span data-stu-id="f1221-191">**Q**: Do I need a gateway for data sources in the cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="f1221-192">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="f1221-192">
**A**: No.</span></span> <span data-ttu-id="f1221-193">Bir ağ geçidi yalnızca şirket içi veri kaynağına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f1221-193">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="f1221-194">**Q**: ağ geçidi veri kaynağı ile aynı makinede yüklü olması gerekmez?</span><span class="sxs-lookup"><span data-stu-id="f1221-194">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="f1221-195">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="f1221-195">
**A**: No.</span></span> <span data-ttu-id="f1221-196">Ağ geçidi sağlanan bağlantı bilgilerini kullanarak veri kaynağına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f1221-196">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="f1221-197">Bu bağlamda bir istemci uygulaması olarak, ağ geçidi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="f1221-197">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="f1221-198">Ağ geçidi yalnızca, genellikle aynı ağ üzerinde sağlanan sunucu adı bağlanmak için özellik gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="f1221-198">The gateway just needs the capability to connect to the server name that was provided, typically on the same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="f1221-199">**Q**: neden gerekiyor mu oturum açmak için bir iş veya Okul hesabı kullanmanız?</span><span class="sxs-lookup"><span data-stu-id="f1221-199">**Q**: Why do I need to use a work or school account to sign in?</span></span> <br/><span data-ttu-id="f1221-200">
**A**: yalnızca Azure bir iş veya Okul hesabınız, şirket içi veri ağ geçidi yüklediğinizde.</span><span class="sxs-lookup"><span data-stu-id="f1221-200">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="f1221-201">Oturum açma hesabınızın Azure Active Directory (Azure AD) tarafından yönetilen bir kiracı depolanır.</span><span class="sxs-lookup"><span data-stu-id="f1221-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f1221-202">Genellikle, Azure AD hesabınızın kullanıcı asıl adı (UPN) e-posta adresi ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="f1221-202">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="f1221-203">**Q**: kimlik bilgilerimi depolandığı?</span><span class="sxs-lookup"><span data-stu-id="f1221-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="f1221-204">
**A**: bir veri kaynağı için girdiğiniz kimlik bilgileri şifrelenir ve ağ geçidi bulut hizmetinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="f1221-204">
**A**: The credentials that you enter for a data source are encrypted and stored in the Gateway Cloud Service.</span></span> <span data-ttu-id="f1221-205">Kimlik bilgileri şirket içi veri ağ geçidi şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="f1221-205">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="f1221-206">**Q**: ağ bant genişliği için tüm gereksinimleri vardır?</span><span class="sxs-lookup"><span data-stu-id="f1221-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="f1221-207">
**A**: ağınızı öneririz sahip bağlantısı iyi verimlilik vardır.</span><span class="sxs-lookup"><span data-stu-id="f1221-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="f1221-208">Her ortam farklıdır ve gönderilen verilerin miktarını sonuçları etkiler.</span><span class="sxs-lookup"><span data-stu-id="f1221-208">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="f1221-209">ExpressRoute kullanarak şirket içi ve Azure veri merkezleri arasında işleme düzeyini güvence altına almak için yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f1221-209">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="f1221-210">Üçüncü taraf aracı Azure hızı Test uygulaması, üretilen iş ölçer yardımcı olmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-210">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="f1221-211">**Q**: bir veri kaynağına ağ geçidi'nden sorguları çalıştırmak için gecikme süresi nedir?</span><span class="sxs-lookup"><span data-stu-id="f1221-211">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="f1221-212">En iyi mimarisi nedir?</span><span class="sxs-lookup"><span data-stu-id="f1221-212">What is the best architecture?</span></span> <br/><span data-ttu-id="f1221-213">
**A**: ağ gecikmesini azaltmak için veri kaynağı olarak mümkün olduğunca yakın ağ geçidini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f1221-213">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="f1221-214">Gerçek veri kaynağı üzerinde ağ geçidi yükleyebilirsiniz, bu yakınlık sunulan gecikme süresi en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="f1221-214">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="f1221-215">Veri merkezleri çok göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="f1221-215">Consider the datacenters too.</span></span> <span data-ttu-id="f1221-216">Örneğin, Batı ABD datacenter hizmetinizi kullanır ve SQL Server bir Azure VM ile barındırılan varsa, Azure VM Batı ABD çok olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1221-216">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="f1221-217">Bu yakınlık gecikme süresi en aza indirir ve çıkış ücretlerini Azure VM'de önler.</span><span class="sxs-lookup"><span data-stu-id="f1221-217">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="f1221-218">**Q**: nasıl sonuçları gönderilir bulut için?</span><span class="sxs-lookup"><span data-stu-id="f1221-218">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="f1221-219">
**A**: sonuçları, Azure Service Bus gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f1221-219">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="f1221-220">**Q**: tüm gelen bağlantıları buluttan ağ geçidine vardır?</span><span class="sxs-lookup"><span data-stu-id="f1221-220">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="f1221-221">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="f1221-221">
**A**: No.</span></span> <span data-ttu-id="f1221-222">Ağ geçidi, Azure Service Bus giden bağlantılara kullanır.</span><span class="sxs-lookup"><span data-stu-id="f1221-222">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="f1221-223">**Q**: ne ı giden bağlantıları engelle?</span><span class="sxs-lookup"><span data-stu-id="f1221-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="f1221-224">Açmak neler gerekir?</span><span class="sxs-lookup"><span data-stu-id="f1221-224">What do I need to open?</span></span> <br/><span data-ttu-id="f1221-225">
**A**: bağlantı noktaları ve ağ geçidini kullanan konakları bakın.</span><span class="sxs-lookup"><span data-stu-id="f1221-225">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="f1221-226">**Q**: ne gerçek Windows hizmeti adı verilir?</span><span class="sxs-lookup"><span data-stu-id="f1221-226">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="f1221-227">
**A**: içinde Hizmetleri, ağ geçidi şirket içi veri ağ geçidi hizmeti çağrılır.</span><span class="sxs-lookup"><span data-stu-id="f1221-227">
**A**: In Services, the gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="f1221-228">**Q**: ağ geçidi Windows hizmeti bir Azure Active Directory hesabıyla çalıştırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="f1221-228">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="f1221-229">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="f1221-229">
**A**: No.</span></span> <span data-ttu-id="f1221-230">Windows hizmeti geçerli bir Windows hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1221-230">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="f1221-231">Varsayılan olarak, hizmet hizmet SID, NT SERVICE\PBIEgwService çalışır.</span><span class="sxs-lookup"><span data-stu-id="f1221-231">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="f1221-232"><a name="high-availability"></a>Yüksek kullanılabilirlik ve olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="f1221-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="f1221-233">**Q**: olağanüstü durum kurtarma için kullanılabilir seçenekleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="f1221-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="f1221-234">
**A**: Kurtarma anahtarını geri yüklemek veya bir ağ geçidi taşımak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-234">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="f1221-235">Ağ geçidi yüklediğinizde, Kurtarma anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="f1221-235">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="f1221-236">**Q**: Kurtarma anahtarı avantajı nedir?</span><span class="sxs-lookup"><span data-stu-id="f1221-236">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="f1221-237">
**A**: Kurtarma anahtarı geçirmek veya ağ geçidi ayarlarınızı sonra bir olağanüstü durum kurtarma için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="f1221-237">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="f1221-238"><a name="troubleshooting"></a>Sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="f1221-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="f1221-239">**Q**: nasıl ı görebilir ne sorguları yükleniyor şirket içi veri kaynağına gönderilen?</span><span class="sxs-lookup"><span data-stu-id="f1221-239">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="f1221-240">
**A**: gönderilen sorgular sorgu izlemeyi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-240">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="f1221-241">Sorgu geri sorun giderme tamamlanınca özgün değeri izleme değiştirmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f1221-241">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="f1221-242">Sorgu izlemesi açık bırakarak daha büyük günlükleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f1221-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="f1221-243">Ayrıca, izleme sorguları için veri kaynağınız olan araçlar da bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="f1221-244">Örneğin, SQL Server ve Analysis Services için genişletilmiş olaylar veya SQL Profiler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="f1221-245">**Q**: ağ geçidi günlüklerini nerede?</span><span class="sxs-lookup"><span data-stu-id="f1221-245">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="f1221-246">
**A**: Bu konunun ilerleyen bölümlerinde günlüklere bakın.</span><span class="sxs-lookup"><span data-stu-id="f1221-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="f1221-247"><a name="update"></a>En son sürüme güncelleştir</span><span class="sxs-lookup"><span data-stu-id="f1221-247"><a name="update"></a>Update to the latest version</span></span>

<span data-ttu-id="f1221-248">Ağ geçidi sürümü güncel olmayan hale geldiğinde birçok sorunları ortaya.</span><span class="sxs-lookup"><span data-stu-id="f1221-248">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="f1221-249">Genel iyi uygulama olarak, en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f1221-249">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="f1221-250">Ağ geçidi, bir veya daha uzun bir ay için güncelleştirmediyseniz, ağ geçidinin en son sürümünü yüklemeyi göz önünde bulundurun ve sorunu yeniden bakın.</span><span class="sxs-lookup"><span data-stu-id="f1221-250">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="f1221-251">Hata: kullanıcı gruba eklenemedi.</span><span class="sxs-lookup"><span data-stu-id="f1221-251">Error: Failed to add user to group.</span></span> <span data-ttu-id="f1221-252">(-2147463168 PBIEgwService performans günlük kullanıcılar)</span><span class="sxs-lookup"><span data-stu-id="f1221-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="f1221-253">Desteklenmeyen bir etki alanı denetleyicisinde ağ geçidini yüklemeye çalıştığınızda bu hatayı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1221-253">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="f1221-254">Bir etki alanı denetleyicisi olmayan bir makineye ağ geçidi dağıttığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f1221-254">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="f1221-255"><a name="logs"></a>Günlükleri</span><span class="sxs-lookup"><span data-stu-id="f1221-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="f1221-256">Günlük dosyaları bir önemli sorun giderirken kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="f1221-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="f1221-257">Kurumsal ağ geçidi hizmeti günlükleri</span><span class="sxs-lookup"><span data-stu-id="f1221-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="f1221-258">Yapılandırma günlükleri</span><span class="sxs-lookup"><span data-stu-id="f1221-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="f1221-259">Olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="f1221-259">Event logs</span></span>

<span data-ttu-id="f1221-260">Veri Yönetimi ağ geçidi ve PowerBIGateway logs altında bulabilirsiniz **uygulama ve hizmet günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="f1221-260">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="f1221-261"><a name="telemetry"></a>Telemetri</span><span class="sxs-lookup"><span data-stu-id="f1221-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="f1221-262">Telemetri, izleme ve sorun giderme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f1221-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="f1221-263">Varsayılan olarak</span><span class="sxs-lookup"><span data-stu-id="f1221-263">By default</span></span>

<span data-ttu-id="f1221-264">**Telemetriyi etkinleştirmek için**</span><span class="sxs-lookup"><span data-stu-id="f1221-264">**To turn on telemetry**</span></span>

1.  <span data-ttu-id="f1221-265">Şirket içi veri ağ geçidi istemci dizini bilgisayarda denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f1221-265">Check the On-premises data gateway client directory on the computer.</span></span> <span data-ttu-id="f1221-266">Genellikle,. **%SystemDrive%\Program Files\On içi veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="f1221-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="f1221-267">Veya, Hizmetler konsolunu açın ve yürütülebilir dosya yolunu denetleyin: şirket içi veri ağ geçidi hizmeti bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="f1221-267">Or, you can open a Services console and check the Path to executable: A property of the On-premises data gateway service.</span></span>
2.  <span data-ttu-id="f1221-268">İstemci dizininden Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config dosyasında.</span><span class="sxs-lookup"><span data-stu-id="f1221-268">In the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="f1221-269">SendTelemetry ayarı true olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f1221-269">Change the SendTelemetry setting to true.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="f1221-270">Yaptığınız değişiklikleri kaydedin ve Windows hizmetini yeniden başlatın: şirket içi veri ağ geçidi hizmeti.</span><span class="sxs-lookup"><span data-stu-id="f1221-270">Save your changes and restart the Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="f1221-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f1221-271">Next steps</span></span>
* [<span data-ttu-id="f1221-272">Çözümleme Hizmetleri yönetme</span><span class="sxs-lookup"><span data-stu-id="f1221-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="f1221-273">Azure Analysis Services Veri Al</span><span class="sxs-lookup"><span data-stu-id="f1221-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
