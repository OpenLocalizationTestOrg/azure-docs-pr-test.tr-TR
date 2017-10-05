---
title: "Azure uygulama hizmeti karma bağlantılar | Microsoft Docs"
description: "Oluşturma ve farklı ağlarda kaynaklara erişmek için karma bağlantılar kullanın"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: fef9e7b280387934cb093f51b4c8aa134a3b87e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-hybrid-connections"></a><span data-ttu-id="5f734-103">Azure uygulama hizmeti karma bağlantılar</span><span class="sxs-lookup"><span data-stu-id="5f734-103">Azure App Service Hybrid Connections</span></span> #

## <a name="overview"></a><span data-ttu-id="5f734-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5f734-104">Overview</span></span> ##

<span data-ttu-id="5f734-105">Karma bağlantılar, hem Azure hizmetinde, hem de Azure App Service'te bir özellik değil.</span><span class="sxs-lookup"><span data-stu-id="5f734-105">Hybrid Connections is both a service in Azure as well as a feature in the Azure App Service.</span></span>  <span data-ttu-id="5f734-106">Bir hizmet olarak kullanın ve Azure App Service'te işlevden ötesinde özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="5f734-106">As a service it has use and capabilities beyond those that are leveraged in the Azure App Service.</span></span>  <span data-ttu-id="5f734-107">Karma bağlantılar ve burada başlayabileceğini Azure App Service dışında kullanımı hakkında daha fazla bilgi edinmek için [Azure geçişi karma bağlantılar][HCService]</span><span class="sxs-lookup"><span data-stu-id="5f734-107">To learn more about Hybrid Connections and their usage outside of the Azure App Service you can start here, [Azure Relay Hybrid Connections][HCService]</span></span>

<span data-ttu-id="5f734-108">Azure App Service içinde karma bağlantılar diğer ağlara uygulama kaynaklara erişim için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-108">Within the Azure App Service, hybrid connections can be used to access application resources in other networks.</span></span> <span data-ttu-id="5f734-109">Bir uygulama uç nokta UYGULAMANIZDAN erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5f734-109">It provides access FROM your app TO an application endpoint.</span></span>  <span data-ttu-id="5f734-110">Uygulamanızı erişmek bir alternatif özelliği sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="5f734-110">It does not enable an alternative capability to access your application.</span></span>  <span data-ttu-id="5f734-111">App Service içinde kullanılan gibi her bir karma bağlantı tek bir TCP ana bilgisayarı ve bağlantı noktası bileşimi hatalarla ilintilidir.</span><span class="sxs-lookup"><span data-stu-id="5f734-111">As used in the App Service, each hybrid connection correlates to a single TCP host and port combination.</span></span>  <span data-ttu-id="5f734-112">Bu karma bağlantı uç noktasının herhangi bir işletim sisteminde olabilir ve herhangi bir uygulama bir TCP dinleme bağlantı noktası devreyi sağlanan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5f734-112">This means that the hybrid connection endpoint can be on any operating system and any application provided you are hitting a TCP listening port.</span></span> <span data-ttu-id="5f734-113">Karma bağlantılar, bilmiyorsanız veya uygulama protokolü nedir veya erişmeye çalıştığınız dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5f734-113">Hybrid connections does not know or care what the application protocol is or what you are accessing.</span></span>  <span data-ttu-id="5f734-114">Ayrıca, ağ erişimi yalnızca sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="5f734-114">It is simply providing network access.</span></span>  


## <a name="how-it-works"></a><span data-ttu-id="5f734-115">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="5f734-115">How it works</span></span> ##
<span data-ttu-id="5f734-116">Karma bağlantılar özelliği Service Bus geçişi iki giden çağrıları oluşur.</span><span class="sxs-lookup"><span data-stu-id="5f734-116">The hybrid connections feature consists of two outbound calls to Service Bus Relay.</span></span>  <span data-ttu-id="5f734-117">Burada, uygulamanızın app service içinde çalışan ve sonra Service Bus geçişi karma bağlantı Manager(HCM) arasında bağlantı yok ana bilgisayardaki bir kitaplıktan bir bağlantı yok.</span><span class="sxs-lookup"><span data-stu-id="5f734-117">There is a connection from a library on the host where your app is running in the app service and then there is a connection from the Hybrid Connection Manager(HCM) to Service Bus relay.</span></span>  <span data-ttu-id="5f734-118">HCM ağ barındırma içinde dağıttığınız bir geçiş hizmetidir</span><span class="sxs-lookup"><span data-stu-id="5f734-118">The HCM is a relay service that you deploy within the network hosting</span></span> 

<span data-ttu-id="5f734-119">İki birleştirilmiş bağlantılarında uygulamanızı sabit ana: bağlantı noktası bileşimi için bir TCP tünel HCM diğer tarafta sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5f734-119">Through the two joined connections your app has a TCP tunnel to a fixed host:port combination on the other side of the HCM.</span></span>  <span data-ttu-id="5f734-120">Bağlantı TLS 1.2 güvenlik ve kimlik doğrulama/yetkilendirme için SAS anahtarları kullanır.</span><span class="sxs-lookup"><span data-stu-id="5f734-120">The connection uses TLS 1.2 for security and SAS keys for authentication/authorization.</span></span>    

![][1]

<span data-ttu-id="5f734-121">Uygulamanızı yapılandırma karma bağlantı uç noktayla eşleşen bir DNS isteğinde bulunduğunda, giden TCP trafiğine karma bağlantı yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-121">When your app makes a DNS request that matches a configure Hybrid Connection endpoint, then the outbound TCP traffic will be redirected down the hybrid connection.</span></span>  

> [!NOTE]
> <span data-ttu-id="5f734-122">Başka bir deyişle, her zaman karma bağlantınız için bir DNS adı kullanmayı denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f734-122">This means that you should try to always use a DNS name for your Hybrid Connection.</span></span>  <span data-ttu-id="5f734-123">Uç nokta bir IP adresi yerine kullanıyorsa, bazı istemci yazılımı bir DNS araması yapmaz.</span><span class="sxs-lookup"><span data-stu-id="5f734-123">Some client software does not do a DNS lookup if the endpoint uses an IP address instead.</span></span>
>
>

<span data-ttu-id="5f734-124">Karma bağlantılar, Azure geçiş altında bir hizmet olarak sunulan yeni karma bağlantılar ve eski BizTalk karma bağlantılar iki tür vardır.</span><span class="sxs-lookup"><span data-stu-id="5f734-124">There are two types of hybrid connections, the new hybrid connections that are offered as a service under Azure Relay and the older BizTalk Hybrid Connections.</span></span>  <span data-ttu-id="5f734-125">Eski BizTalk karma bağlantılar olarak Klasik karma bağlantılar portalda denir.</span><span class="sxs-lookup"><span data-stu-id="5f734-125">The older BizTalk Hybrid Connections are referred to as Classic Hybrid Connections in the portal.</span></span>  <span data-ttu-id="5f734-126">Bu belgede daha sonra bunları hakkında daha fazla bilgi yoktur.</span><span class="sxs-lookup"><span data-stu-id="5f734-126">There is more information later in this document about them.</span></span>

### <a name="app-service-hybrid-connection-benefits"></a><span data-ttu-id="5f734-127">Uygulama hizmeti karma bağlantı avantajları</span><span class="sxs-lookup"><span data-stu-id="5f734-127">App Service hybrid connection benefits</span></span> ###

<span data-ttu-id="5f734-128">Karma bağlantılar yeteneği dahil olmak üzere avantajları vardır</span><span class="sxs-lookup"><span data-stu-id="5f734-128">There are a number of benefits to the hybrid connections capability including</span></span>

- <span data-ttu-id="5f734-129">Uygulamaları güvenli bir şekilde şirket içi sistemleri ve Hizmetleri ile güvenli bir şekilde erişebilir</span><span class="sxs-lookup"><span data-stu-id="5f734-129">Apps can securely access on premises systems and services securely</span></span>
- <span data-ttu-id="5f734-130">Bu özellik Internet erişilebilir uç gerektirmez</span><span class="sxs-lookup"><span data-stu-id="5f734-130">the feature does not require an internet accessible endpoint</span></span>
- <span data-ttu-id="5f734-131">hızlı ve kolay ayarlamak</span><span class="sxs-lookup"><span data-stu-id="5f734-131">it is quick and easy to set up</span></span>  
- <span data-ttu-id="5f734-132">Her bir karma bağlantı bir mükemmel güvenlik durum olan tek ana bilgisayar: bağlantı noktası birleşimi ile eşleşir</span><span class="sxs-lookup"><span data-stu-id="5f734-132">each hybrid connection matches to a single host:port combination which is an excellent security aspect</span></span>
- <span data-ttu-id="5f734-133">Standart web bağlantı noktaları üzerinden giden tüm bağlantıları gibi normalde güvenlik duvarı delik gerektirmez</span><span class="sxs-lookup"><span data-stu-id="5f734-133">it normally does not require firewall holes as the connections are all outbound over standard web ports</span></span>
- <span data-ttu-id="5f734-134">özellik anlamına da ağ düzeyi olduğundan, uygulamanız tarafından kullanılan dil ve bitiş noktası tarafından kullanılan teknoloji bağımsızdır</span><span class="sxs-lookup"><span data-stu-id="5f734-134">because the feature is network level that also means that it is agnostic to the language used by your app and the technology used by the endpoint</span></span>
- <span data-ttu-id="5f734-135">tek bir uygulama birden çok ağ erişim sağlamak için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="5f734-135">it can be used to provide access in multiple networks from a single app</span></span> 

### <a name="things-you-cannot-do-with-hybrid-connections"></a><span data-ttu-id="5f734-136">Karma bağlantılar ile yapamayacağı noktalar</span><span class="sxs-lookup"><span data-stu-id="5f734-136">Things you cannot do with Hybrid Connections</span></span> ###

<span data-ttu-id="5f734-137">Karma bağlantılar ile yapamayacağınız birkaç şey vardır ve bunlar şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="5f734-137">There are a few things you cannot do with hybrid connections and they include:</span></span>

- <span data-ttu-id="5f734-138">bir sürücü bağlama</span><span class="sxs-lookup"><span data-stu-id="5f734-138">mounting a drive</span></span>
- <span data-ttu-id="5f734-139">UDP kullanma</span><span class="sxs-lookup"><span data-stu-id="5f734-139">using UDP</span></span>
- <span data-ttu-id="5f734-140">FTP Pasif modu veya genişletilmiş Pasif modu gibi dinamik bağlantı noktaları kullanan hizmetler dayalı TCP erişme</span><span class="sxs-lookup"><span data-stu-id="5f734-140">accessing TCP based services that use dynamic ports such as FTP Passive Mode or Extended Passive Mode</span></span>
- <span data-ttu-id="5f734-141">UDP şekliyle bazen LDAP desteği gerektirir</span><span class="sxs-lookup"><span data-stu-id="5f734-141">LDAP support, as it sometimes requires UDP</span></span>
- <span data-ttu-id="5f734-142">Active Directory desteği</span><span class="sxs-lookup"><span data-stu-id="5f734-142">Active Directory support</span></span>

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a><span data-ttu-id="5f734-143">Ekleme ve uygulamanızda karma bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f734-143">Adding and Creating a Hybrid Connection in your App</span></span> ##

<span data-ttu-id="5f734-144">Karma bağlantılar, uygulama portalı üzerinden veya karma bağlantı hizmet portalından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-144">Hybrid Connections can be created through the app portal or from the Hybrid Connection service portal.</span></span>  <span data-ttu-id="5f734-145">Uygulamanız ile kullanmak istediğiniz karma bağlantılar oluşturmak için uygulama portalını kullanma önerilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-145">It is highly recommended that you use the app portal to create the Hybrid Connections you wish to use with your app.</span></span>  <span data-ttu-id="5f734-146">Karma bir bağlantı oluşturmak için Git [Azure portal] [ portal] ve uygulamanız için kullanıcı Arabirimi uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="5f734-146">To create a Hybrid Connection go to the [Azure portal][portal] and go into the UI for your app.</span></span>  <span data-ttu-id="5f734-147">Seçin **Ağ > karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="5f734-147">Select **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="5f734-148">Buradan, uygulamanızı yapılandırılmış karma bağlantılar görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f734-148">From here you can see the Hybrid Connections that are configured with your app</span></span>  

![][2]

<span data-ttu-id="5f734-149">Yeni bir karma bağlantı eklemek için karma Bağlantı Ekle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5f734-149">To add a new Hybrid Connection, click Add Hybrid Connection.</span></span>  <span data-ttu-id="5f734-150">Açılan UI önceden oluşturduğunuz karma bağlantılar listeler.</span><span class="sxs-lookup"><span data-stu-id="5f734-150">The UI that opens up lists the Hybrid Connections that you have already created.</span></span>  <span data-ttu-id="5f734-151">Bir veya daha fazlası uygulamanıza eklemek için istediğiniz ve isabet olanları tıklatın **Ekle seçili karma bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="5f734-151">To add one or more of them to your app, click on the ones you want and hit **Add selected hybrid connection**.</span></span>  

![][3]

<span data-ttu-id="5f734-152">Yeni bir karma bağlantı oluşturmak istiyorsanız, tıklatın **yeni karma bağlantı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="5f734-152">If you want to create a new Hybrid Connection, click **Create new hybrid connection**.</span></span>  <span data-ttu-id="5f734-153">Buradan belirtin:</span><span class="sxs-lookup"><span data-stu-id="5f734-153">From here you specify the:</span></span> 

- <span data-ttu-id="5f734-154">uç nokta adı</span><span class="sxs-lookup"><span data-stu-id="5f734-154">endpoint name</span></span>
- <span data-ttu-id="5f734-155">uç noktası ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="5f734-155">endpoint hostname</span></span>
- <span data-ttu-id="5f734-156">uç nokta bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="5f734-156">endpoint port</span></span>
- <span data-ttu-id="5f734-157">kullanmak istediğiniz servicebus ad alanı</span><span class="sxs-lookup"><span data-stu-id="5f734-157">servicebus namespace you wish to use</span></span>

![][4]

<span data-ttu-id="5f734-158">Her karma bağlantı için hizmet veri yolu ad alanı bağlıdır ve bir Azure bölgesinde her hizmet veri yolu ad alanıdır.</span><span class="sxs-lookup"><span data-stu-id="5f734-158">Every hybrid connection is tied to a service bus namespace and each service bus namespace is in an Azure region.</span></span>  <span data-ttu-id="5f734-159">Deneyin ve kopyaladığınızda ağ gecikmesi önlemek amacıyla, uygulamanız ile aynı bölgede bir hizmet veri yolu ad alanı kullanmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="5f734-159">It is important to try and use a service bus namespace in the same region as your app so as to avoid network induced latency.</span></span>

<span data-ttu-id="5f734-160">Karma bağlantınız uygulamanızdan kaldırmak istiyorsanız, sağ tıklayın ve seçin **Bağlantıyı Kes**.</span><span class="sxs-lookup"><span data-stu-id="5f734-160">If you want to remove your hybrid connection from your app, right click on it and select **Disconnect**.</span></span>  

<span data-ttu-id="5f734-161">Karma bağlantı, web uygulamanızın eklendikten sonra Ayrıntılar üzerinde yalnızca tıklayarak görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f734-161">Once a hybrid connection is added to your web app, you can see details on it by simply clicking on it.</span></span>  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a><span data-ttu-id="5f734-162">Karma bağlantılar ve uygulama hizmeti planları</span><span class="sxs-lookup"><span data-stu-id="5f734-162">Hybrid Connections and App Service Plans</span></span> ##

<span data-ttu-id="5f734-163">Şimdi yapabileceğiniz yalnızca karma bağlantılar, yeni karma bağlantılar gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-163">The only hybrid connections you can now make are the new hybrid connections.</span></span>  <span data-ttu-id="5f734-164">Yalnızca temel, standart, Premium ve SKU'ları fiyatlandırması Isolated kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-164">They are only available in Basic, Standard, Premium and Isolated pricing SKUs.</span></span>  <span data-ttu-id="5f734-165">Fiyatlandırma plana bağlı sınırları vardır.</span><span class="sxs-lookup"><span data-stu-id="5f734-165">There are limits tied to the pricing plan.</span></span>  

| <span data-ttu-id="5f734-166">Plan fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="5f734-166">Pricing Plan</span></span> | <span data-ttu-id="5f734-167">Karma bağlantılar planda kullanılabilir sayısı</span><span class="sxs-lookup"><span data-stu-id="5f734-167">Number of hybrid connections usable in the plan</span></span> |
|----|----|
| <span data-ttu-id="5f734-168">Temel</span><span class="sxs-lookup"><span data-stu-id="5f734-168">Basic</span></span> | <span data-ttu-id="5f734-169">5</span><span class="sxs-lookup"><span data-stu-id="5f734-169">5</span></span> |
| <span data-ttu-id="5f734-170">Standart</span><span class="sxs-lookup"><span data-stu-id="5f734-170">Standard</span></span> | <span data-ttu-id="5f734-171">25</span><span class="sxs-lookup"><span data-stu-id="5f734-171">25</span></span> |
| <span data-ttu-id="5f734-172">Premium</span><span class="sxs-lookup"><span data-stu-id="5f734-172">Premium</span></span> | <span data-ttu-id="5f734-173">200</span><span class="sxs-lookup"><span data-stu-id="5f734-173">200</span></span> |
| <span data-ttu-id="5f734-174">Yalıtılmış</span><span class="sxs-lookup"><span data-stu-id="5f734-174">Isolated</span></span> | <span data-ttu-id="5f734-175">200</span><span class="sxs-lookup"><span data-stu-id="5f734-175">200</span></span> |

<span data-ttu-id="5f734-176">Uygulama hizmeti planı kısıtlamaları olduğundan UI kaç karma bağlantılar kullanıldığını gösterir App Service planı ve hangi uygulamalar tarafından bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5f734-176">Since there are App Service Plan restrictions there is also UI in the App Service Plan that shows you how many hybrid connections are being used and by what apps.</span></span>  

![][6]

<span data-ttu-id="5f734-177">Gibi uygulama görünümüyle ayrıntıları karma bağlantınız tıklayarak görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f734-177">Just as with the app view, you can see details on your hybrid connection by clicking on it.</span></span>  <span data-ttu-id="5f734-178">Burada gösterilen özellikleri'nde uygulama görünüme sahip tüm bilgileri görebilirsiniz ancak de aynı uygulama hizmeti planında kaç diğer uygulamalar bu karma bağlantı kullandığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f734-178">In the properties shown here you can see all the information you had at the app view but can also see how many other apps in the same App Service Plan are using that hybrid connection.</span></span>

![][7]

<span data-ttu-id="5f734-179">Bir uygulama hizmeti planı'nda kullanılabilir karma bağlantı uç sayısına bir sınır olsa da, bu uygulama hizmeti planı uygulamalarda herhangi bir sayıda genelinde kullanılan her karma bağlantı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-179">While there is a limit on the number of hybrid connection endpoints that can be used in an App Service Plan, each hybrid connection used can be used across any number of apps in that App Service Plan.</span></span>  <span data-ttu-id="5f734-180">My uygulama hizmeti planı'nda 5 ayrı uygulamalarında kullandım 1 karma bağlantı varsa, yine yalnızca 1 karma bağlantı olduğunu söylemek için olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="5f734-180">That is to say that if I had 1 hybrid connection that I used in 5 separate apps in my App Service Plan, that is still just 1 hybrid connection.</span></span>

<span data-ttu-id="5f734-181">Karma bağlantılar'yalnızca temel, standart, Premium veya yalıtılmış SKU içinde kullanılabilir olan ötesinde ek bir maliyet yoktur.</span><span class="sxs-lookup"><span data-stu-id="5f734-181">There is an additional cost to hybrid connections beyond being only usable in a Basic, Standard, Premium or Isolated SKU.</span></span>  <span data-ttu-id="5f734-182">Karma bağlantı fiyatlandırma hakkında ayrıntılar lütfen buraya gidin: [Service Bus fiyatlandırma][sbpricing].</span><span class="sxs-lookup"><span data-stu-id="5f734-182">For details on hybrid connection pricing please go here: [Service Bus pricing][sbpricing].</span></span>

## <a name="hybrid-connection-manager"></a><span data-ttu-id="5f734-183">Karma Bağlantı Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="5f734-183">Hybrid Connection Manager</span></span> ##

<span data-ttu-id="5f734-184">Sırayla çalışması karma bağlantılar için bir geçiş aracısı, karma bağlantı uç noktasını barındıran ağdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f734-184">In order for hybrid connections to work you need a relay agent in the network that hosts your hybrid connection endpoint.</span></span>  <span data-ttu-id="5f734-185">Bu geçiş aracısı karma Bağlantı Yöneticisi (HCM) adı verilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-185">That relay agent is called the Hybrid Connection Manager (HCM).</span></span>  <span data-ttu-id="5f734-186">Bu araç şu adresten yüklenebilir: **Ağ > karma bağlantı uç noktalarınızı yapılandırın** UI içinde uygulamanızdan kullanılabilir [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="5f734-186">This tool can be downloaded from the **Networking > Configure your hybrid connection endpoints** UI available from your app in the [Azure portal][portal].</span></span>  

<span data-ttu-id="5f734-187">Bu araç, Windows server 2008 R2 ve Windows'un sonraki sürümlerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5f734-187">This tool runs on Windows server 2008 R2 and later versions of Windows.</span></span>  <span data-ttu-id="5f734-188">HCM çalışır bir hizmet olarak bir kez yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5f734-188">Once installed the HCM runs as a service.</span></span>  <span data-ttu-id="5f734-189">Bu hizmet üzerinde yapılandırılmış uç tabanlı Azure servicebus geçiş bağlanır.</span><span class="sxs-lookup"><span data-stu-id="5f734-189">This service connects to Azure servicebus relay based on the configured endpoints.</span></span>  <span data-ttu-id="5f734-190">HCM bağlantılarından 80 ve 443 numaralı bağlantı noktalarına giden.</span><span class="sxs-lookup"><span data-stu-id="5f734-190">The connections from the HCM are outbound to ports 80 and 443.</span></span>    

<span data-ttu-id="5f734-191">HCM yapılandırmak için bir kullanıcı Arabirimi vardır.</span><span class="sxs-lookup"><span data-stu-id="5f734-191">The HCM has a UI to configure it.</span></span>  <span data-ttu-id="5f734-192">HCM yüklendikten sonra karma Bağlantı Yöneticisi'ni yükleme dizininde bulunur HybridConnectionManagerUi.exe çalıştırarak UI'yi kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f734-192">After the HCM is installed you can bring up the UI by running the HybridConnectionManagerUi.exe that sits in the Hybrid Connection Manager installation directory.</span></span>  <span data-ttu-id="5f734-193">Yazarak Windows 10'da kolayca ulaşıldığında *karma Bağlantı Yöneticisi kullanıcı Arabirimi* , arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="5f734-193">It is also easily reached on Windows 10 by typing *Hybrid Connection Manager UI* in your search box.</span></span>  

<span data-ttu-id="5f734-194">HCM kullanıcı Arabirimi başlatıldığında, gördüğünüz ilk tüm HCM'ın bu örneğinin yapılandırılmış karma bağlantıları listeleyen bir tablo şeydir.</span><span class="sxs-lookup"><span data-stu-id="5f734-194">When the HCM UI is started, the first thing you see is a table that lists all of the hybrid connections that are configured with this instance of the HCM.</span></span>  <span data-ttu-id="5f734-195">Herhangi bir değişiklik yapmak istiyorsanız Azure kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f734-195">If you wish to make any changes you will need to authenticate with Azure.</span></span> 

<span data-ttu-id="5f734-196">Bir veya daha fazla karma bağlantılar, HCM eklemek için:</span><span class="sxs-lookup"><span data-stu-id="5f734-196">To add one or more Hybrid Connections to your HCM:</span></span>

1. <span data-ttu-id="5f734-197">HCM kullanıcı arabirimini Başlat</span><span class="sxs-lookup"><span data-stu-id="5f734-197">Start the HCM UI</span></span>
1. <span data-ttu-id="5f734-198">Başka bir karma bağlantı yapılandırmak tıklayın![][8]</span><span class="sxs-lookup"><span data-stu-id="5f734-198">Click Configure another hybrid connection ![][8]</span></span>

1. <span data-ttu-id="5f734-199">Azure hesabınızla oturum açın</span><span class="sxs-lookup"><span data-stu-id="5f734-199">Sign in with your Azure account</span></span>
1. <span data-ttu-id="5f734-200">Bir abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="5f734-200">Choose a subscription</span></span>
1. <span data-ttu-id="5f734-201">Geçiş için bu HCM istediğiniz karma bağlantılar'ı tıklatın![][9]</span><span class="sxs-lookup"><span data-stu-id="5f734-201">Click on the hybrid connections you want this HCM to relay ![][9]</span></span>

1. <span data-ttu-id="5f734-202">Kaydet’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5f734-202">Click Save</span></span>

<span data-ttu-id="5f734-203">Bu noktada eklediğiniz karma bağlantılar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5f734-203">At this point you will see the hybrid connections you added.</span></span>  <span data-ttu-id="5f734-204">Ayrıca yapılandırılmış karma bağlantısında tıklatın ve bağlantı ayrıntılarını bakın.</span><span class="sxs-lookup"><span data-stu-id="5f734-204">You can also click on the configured hybrid connection and see details about the connection.</span></span>

![][10]

<span data-ttu-id="5f734-205">HCM ile yapılandırılmış karma bağlantılar destekleyebilmesi, onu gerekir:</span><span class="sxs-lookup"><span data-stu-id="5f734-205">For your HCM to be able to support the hybrid connections it is configured with, it needs:</span></span>

- <span data-ttu-id="5f734-206">TCP bağlantı noktaları 80 ve 443 üzerinden Azure erişimi</span><span class="sxs-lookup"><span data-stu-id="5f734-206">TCP access to Azure over ports 80 and 443</span></span>
- <span data-ttu-id="5f734-207">Karma bağlantı uç noktasının TCP erişimi</span><span class="sxs-lookup"><span data-stu-id="5f734-207">TCP access to the hybrid connection endpoint</span></span>
- <span data-ttu-id="5f734-208">DNS yapılabilmesi aramalarına uç noktası ana bilgisayar ve azure servicebus ad alanı</span><span class="sxs-lookup"><span data-stu-id="5f734-208">ability to do DNS look ups on the endpoint host and the azure servicebus namespace</span></span>

<span data-ttu-id="5f734-209">HCM, hem yeni karma bağlantılar, hem de eski BizTalk karma bağlantılar destekler.</span><span class="sxs-lookup"><span data-stu-id="5f734-209">The HCM supports both new hybrid connections as well as the older BizTalk hybrid connections.</span></span>

### <a name="redundancy"></a><span data-ttu-id="5f734-210">Yedeklilik</span><span class="sxs-lookup"><span data-stu-id="5f734-210">Redundancy</span></span> ###

<span data-ttu-id="5f734-211">Her HCM, birden çok karma bağlantılar destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-211">Each HCM can support multiple hybrid connections.</span></span>  <span data-ttu-id="5f734-212">Ayrıca, herhangi bir belirtilen karma bağlantıyı birden çok HCMs tarafından desteklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5f734-212">Also, any given hybrid connection can be supported by multiple HCMs.</span></span>  <span data-ttu-id="5f734-213">Varsayılan davranış hepsini bir kez trafiği verilen herhangi bir uç nokta için yapılandırılmış HCMs arasında değil.</span><span class="sxs-lookup"><span data-stu-id="5f734-213">The default behavior is to round robin traffic across the configured HCMs for any given endpoint.</span></span>  <span data-ttu-id="5f734-214">Yüksek kullanılabilirlik, karma bağlantılar ağınızdan isterseniz, yalnızca birden çok HCMs ayrı makinelerde örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5f734-214">If you want high availability on your hybrid connections from your network, simply instantiate multiple HCMs on separate machines.</span></span> 

### <a name="manually-adding-a-hybrid-connection"></a><span data-ttu-id="5f734-215">El ile karma bağlantı ekleme</span><span class="sxs-lookup"><span data-stu-id="5f734-215">Manually adding a hybrid connection</span></span> ###

<span data-ttu-id="5f734-216">Birisi verilen karma bağlantı için bir HCM örneği barındırmak için aboneliğinizi dışında istiyorsanız, bunları ile karma bağlantı için ağ geçidi bağlantı dizesi paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f734-216">If you wish somebody outside of your subscription to host an HCM instance for a given hybrid connection, you can share with them the gateway connection string for the hybrid connection.</span></span>  <span data-ttu-id="5f734-217">Bu karma bir bağlantı özelliklerinde görebilirsiniz [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="5f734-217">You can see this in the properties for a hybrid connection in the [Azure portal][portal].</span></span> <span data-ttu-id="5f734-218">Bu dizeyi kullanmak için tıklatın **el ile yapılandırmanız** HCM düğmesine tıklayın ve ağ geçidi bağlantı dizesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="5f734-218">To use that string, click the **Configure manually** button in the HCM and paste in the gateway connection string.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="5f734-219">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="5f734-219">Troubleshooting</span></span> ##

<span data-ttu-id="5f734-220">Ne zaman karma bağlantınız ile çalışan bir uygulama ayarlanır ve yapılandırılmış Bu karma bağlantısı olan en az bir HCM yoktur ardından durum söyleyin **bağlı** Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="5f734-220">When your hybrid connection is set up with a running application and there is at least one HCM that has that hybrid connection configured, then the status will say **Connected** in the portal.</span></span>  <span data-ttu-id="5f734-221">Değil dediği varsa **bağlı** uygulamanızı çalışmıyor veya sizin HCM Azure 80 veya 443 bağlantı noktalarında giden bağlanamıyor anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5f734-221">If it does not say **Connected** then it means that either your app is down or your HCM cannot connect out to Azure on ports 80 or 443.</span></span>  

<span data-ttu-id="5f734-222">Uç nokta bir DNS adı yerine bir IP adresi kullanarak belirtilmediğinden, istemciler kendi uç noktasına bağlanamıyor birincil nedenidir.</span><span class="sxs-lookup"><span data-stu-id="5f734-222">The primary reason that clients cannot connect to their endpoint is because the endpoint was specified using an IP address instead of a DNS name.</span></span>  <span data-ttu-id="5f734-223">Uygulamanızı istenen endpoint ulaşamıyor ve bir IP adresi kullandıysanız HCM'ın çalıştırıldığı konak üzerinde geçerli bir DNS adı kullanmaya geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="5f734-223">If your app cannot reach the desired endpoint and you used an IP address, switch to using a DNS name that is valid on the host where the HCM is running.</span></span>  <span data-ttu-id="5f734-224">Denetlenecek diğer DNS adını düzgün HCM çalıştığı konakta çözümler ve HCM karma bağlantı uç noktasına çalıştığı ana bilgisayardan bağlantısı olduğunu noktalardır.</span><span class="sxs-lookup"><span data-stu-id="5f734-224">Other things to check are that the DNS name resolves properly on the host where the HCM is running and that there is connectivity from the host where the HCM is running to the hybrid connection endpoint.</span></span>  

<span data-ttu-id="5f734-225">App Service'te tcpping adlı Konsolu'ndan çağrılan bir aracı yoktur.</span><span class="sxs-lookup"><span data-stu-id="5f734-225">There is a tool in the App Service that can be invoked from the console called tcpping.</span></span>  <span data-ttu-id="5f734-226">Bu araç TCP uç noktası erişimi ancak bir karma bağlantı uç noktasının erişiminiz varsa söylemez anlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f734-226">This tool can tell you if you have access to a TCP endpoint but does not tell you if you have access to a hybrid connection endpoint.</span></span>  <span data-ttu-id="5f734-227">Karma bağlantı uç noktasının karşı konsolunda kullanıldığında, başarılı bir ping işlemi yalnızca bu ana bilgisayar: bağlantı noktası bileşimi kullanan uygulamanız için yapılandırılmış karma bağlantı olduğunu söyler.</span><span class="sxs-lookup"><span data-stu-id="5f734-227">When used in the console against a hybrid connection endpoint, a successful ping will only tell you that you have a hybrid connection configured for your app that uses that host:port combination.</span></span>  

## <a name="biztalk-hybrid-connections"></a><span data-ttu-id="5f734-228">BizTalk Karma Bağlantıları</span><span class="sxs-lookup"><span data-stu-id="5f734-228">BizTalk Hybrid Connections</span></span> ##

<span data-ttu-id="5f734-229">Eski BizTalk karma bağlantılar özelliği devre dışı başka BizTalk karma bağlantı oluşturmaları kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="5f734-229">The older BizTalk Hybrid Connections capability has been closed off to further BizTalk Hybrid Connection creations.</span></span>  <span data-ttu-id="5f734-230">Önceden var olan BizTalk karma bağlantılarınızı uygulamalarınızı ile kullanmaya devam edebilirsiniz ancak yeni hizmet geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f734-230">You can continue using your preexisting BizTalk Hybrid Connections with your apps but should migrate to the new service.</span></span>  <span data-ttu-id="5f734-231">Yeni hizmet BizTalk sürüm üzerinden avantajları arasında şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5f734-231">Among the benefits in the new service over the BizTalk version are:</span></span>

- <span data-ttu-id="5f734-232">hiçbir ek BizTalk hesabı gereklidir</span><span class="sxs-lookup"><span data-stu-id="5f734-232">no additional BizTalk account is required</span></span>
- <span data-ttu-id="5f734-233">TLS 1.2 BizTalk karma bağlantılar olduğu gibi 1.0 yerine olduğu</span><span class="sxs-lookup"><span data-stu-id="5f734-233">TLS is 1.2 instead of 1.0 as in BizTalk Hybrid Connections</span></span>
- <span data-ttu-id="5f734-234">Bağlantı noktaları 80 ve 443 numaralı IP adresleri yerine Azure ve bir dizi ek diğer ulaşmak için bir DNS adını kullanarak bağlantı noktaları üzerinden iletişim önemlidir.</span><span class="sxs-lookup"><span data-stu-id="5f734-234">Communication is over ports 80 and 443 using a DNS name to reach Azure instead of IP addresses and a range of additional other ports.</span></span>  

<span data-ttu-id="5f734-235">Uygulamanızı Git BizTalk karma bağlantı uygulamanıza eklemek için [Azure portal] [ portal] tıklatıp **Ağ > karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="5f734-235">To add a BizTalk hybrid connection to your app, go to your app in the [Azure portal][portal] and click **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="5f734-236">Klasik karma bağlantıları tabloda tıklatın **Klasik karma Bağlantı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5f734-236">In the Classic hybrid connections table click **Add classic hybrid connection**.</span></span>  <span data-ttu-id="5f734-237">Buradan, BizTalk karma bağlantılar listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5f734-237">From here you will see a list of your BizTalk hybrid connections.</span></span>  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

