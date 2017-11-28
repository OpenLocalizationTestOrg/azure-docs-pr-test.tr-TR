---
title: "aaa \"Azure uygulama hizmeti karma bağlantılar | Microsoft Docs\""
description: "Nasıl farklı ağlarda toocreate ve kullanım karma bağlantılar tooaccess kaynakları"
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
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a><span data-ttu-id="59ff6-103">Azure uygulama hizmeti karma bağlantılar</span><span class="sxs-lookup"><span data-stu-id="59ff6-103">Azure App Service Hybrid Connections</span></span> #

## <a name="overview"></a><span data-ttu-id="59ff6-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="59ff6-104">Overview</span></span> ##

<span data-ttu-id="59ff6-105">Karma bağlantılar hem Azure hizmetinde, hem de hello Azure App Service içinde bir özellik değil.</span><span class="sxs-lookup"><span data-stu-id="59ff6-105">Hybrid Connections is both a service in Azure as well as a feature in hello Azure App Service.</span></span>  <span data-ttu-id="59ff6-106">Bir hizmet olarak kullanın ve hello Azure App Service işlevden ötesinde özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="59ff6-106">As a service it has use and capabilities beyond those that are leveraged in hello Azure App Service.</span></span>  <span data-ttu-id="59ff6-107">Karma bağlantılar ve hello Azure App Service burada başlayabileceğini dışında kullanımı hakkında daha fazla toolearn [Azure geçişi karma bağlantılar][HCService]</span><span class="sxs-lookup"><span data-stu-id="59ff6-107">toolearn more about Hybrid Connections and their usage outside of hello Azure App Service you can start here, [Azure Relay Hybrid Connections][HCService]</span></span>

<span data-ttu-id="59ff6-108">Hello Azure App Service içinde karma bağlantılar diğer ağlarda kullanılan tooaccess uygulama kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-108">Within hello Azure App Service, hybrid connections can be used tooaccess application resources in other networks.</span></span> <span data-ttu-id="59ff6-109">Uygulama tooan uygulama uç NOKTASINDAN erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="59ff6-109">It provides access FROM your app tooan application endpoint.</span></span>  <span data-ttu-id="59ff6-110">Uygulamanızı bir alternatif yetenek tooaccess etkinleştirmez.</span><span class="sxs-lookup"><span data-stu-id="59ff6-110">It does not enable an alternative capability tooaccess your application.</span></span>  <span data-ttu-id="59ff6-111">Merhaba uygulama hizmeti kullanılan gibi her bir karma bağlantı tooa tek TCP ana bilgisayarı ve bağlantı noktası bileşimi hatalarla ilintilidir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-111">As used in hello App Service, each hybrid connection correlates tooa single TCP host and port combination.</span></span>  <span data-ttu-id="59ff6-112">Başka bir deyişle, bu hello karma bağlantı uç herhangi bir işletim sistemi ve herhangi bir uygulama üzerinde bir TCP dinleme bağlantı noktası devreyi sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-112">This means that hello hybrid connection endpoint can be on any operating system and any application provided you are hitting a TCP listening port.</span></span> <span data-ttu-id="59ff6-113">Karma bağlantılar, bilmiyorsanız veya hangi hello uygulama protokolü veya erişmeye çalıştığınız dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="59ff6-113">Hybrid connections does not know or care what hello application protocol is or what you are accessing.</span></span>  <span data-ttu-id="59ff6-114">Ayrıca, ağ erişimi yalnızca sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="59ff6-114">It is simply providing network access.</span></span>  


## <a name="how-it-works"></a><span data-ttu-id="59ff6-115">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="59ff6-115">How it works</span></span> ##
<span data-ttu-id="59ff6-116">Merhaba karma bağlantıları özelliği iki giden çağrıları tooService veri yolu geçişi oluşur.</span><span class="sxs-lookup"><span data-stu-id="59ff6-116">hello hybrid connections feature consists of two outbound calls tooService Bus Relay.</span></span>  <span data-ttu-id="59ff6-117">Burada, uygulamanızın hello app service içinde çalışan ve ardından hello karma bağlantı Manager(HCM) tooService veri yolu geçişi öğesinden bir bağlantı yoktur hello ana bilgisayardaki bir kitaplıktan bir bağlantı yok.</span><span class="sxs-lookup"><span data-stu-id="59ff6-117">There is a connection from a library on hello host where your app is running in hello app service and then there is a connection from hello Hybrid Connection Manager(HCM) tooService Bus relay.</span></span>  <span data-ttu-id="59ff6-118">Merhaba HCM hello ağ barındırma içinde dağıttığınız bir geçiş hizmetidir</span><span class="sxs-lookup"><span data-stu-id="59ff6-118">hello HCM is a relay service that you deploy within hello network hosting</span></span> 

<span data-ttu-id="59ff6-119">Merhaba uygulamanızı TCP tünel tooa sahip iki birleştirilmiş bağlantıları hello HCM diğer tarafını ana: bağlantı noktası bileşimi hello üzerinde sabit.</span><span class="sxs-lookup"><span data-stu-id="59ff6-119">Through hello two joined connections your app has a TCP tunnel tooa fixed host:port combination on hello other side of hello HCM.</span></span>  <span data-ttu-id="59ff6-120">Merhaba bağlantı TLS 1.2 güvenlik ve kimlik doğrulama/yetkilendirme için SAS anahtarları kullanır.</span><span class="sxs-lookup"><span data-stu-id="59ff6-120">hello connection uses TLS 1.2 for security and SAS keys for authentication/authorization.</span></span>    

![][1]

<span data-ttu-id="59ff6-121">Uygulamanızı bir DNS isteğinde bulunduğunda bir yapılandırma karma bağlantı uç noktası ile eşleşen sonra hello giden TCP trafiğine hello karma bağlantı yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-121">When your app makes a DNS request that matches a configure Hybrid Connection endpoint, then hello outbound TCP traffic will be redirected down hello hybrid connection.</span></span>  

> [!NOTE]
> <span data-ttu-id="59ff6-122">Bu karma bağlantınız için bir DNS adı tooalways kullanım denemelisiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-122">This means that you should try tooalways use a DNS name for your Hybrid Connection.</span></span>  <span data-ttu-id="59ff6-123">Hello uç noktası IP adresi yerine kullanıyorsa, bazı istemci yazılımı DNS araması yapın.</span><span class="sxs-lookup"><span data-stu-id="59ff6-123">Some client software does not do a DNS lookup if hello endpoint uses an IP address instead.</span></span>
>
>

<span data-ttu-id="59ff6-124">Karma bağlantılar, Azure geçiş altında bir hizmet olarak sunulan ve eski BizTalk karma bağlantılar hello hello yeni karma bağlantılar iki tür vardır.</span><span class="sxs-lookup"><span data-stu-id="59ff6-124">There are two types of hybrid connections, hello new hybrid connections that are offered as a service under Azure Relay and hello older BizTalk Hybrid Connections.</span></span>  <span data-ttu-id="59ff6-125">Merhaba eski BizTalk karma bağlantılar hello portalında başvurulan tooas Klasik karma bağlantılar ' dir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-125">hello older BizTalk Hybrid Connections are referred tooas Classic Hybrid Connections in hello portal.</span></span>  <span data-ttu-id="59ff6-126">Bu belgede daha sonra bunları hakkında daha fazla bilgi yoktur.</span><span class="sxs-lookup"><span data-stu-id="59ff6-126">There is more information later in this document about them.</span></span>

### <a name="app-service-hybrid-connection-benefits"></a><span data-ttu-id="59ff6-127">Uygulama hizmeti karma bağlantı avantajları</span><span class="sxs-lookup"><span data-stu-id="59ff6-127">App Service hybrid connection benefits</span></span> ###

<span data-ttu-id="59ff6-128">Avantajları toohello karma bağlantıları yeteneği dahil olmak üzere, birkaç vardır</span><span class="sxs-lookup"><span data-stu-id="59ff6-128">There are a number of benefits toohello hybrid connections capability including</span></span>

- <span data-ttu-id="59ff6-129">Uygulamaları güvenli bir şekilde şirket içi sistemleri ve Hizmetleri ile güvenli bir şekilde erişebilir</span><span class="sxs-lookup"><span data-stu-id="59ff6-129">Apps can securely access on premises systems and services securely</span></span>
- <span data-ttu-id="59ff6-130">Merhaba özelliği bir Internet erişilebilir uç nokta gerektirmez</span><span class="sxs-lookup"><span data-stu-id="59ff6-130">hello feature does not require an internet accessible endpoint</span></span>
- <span data-ttu-id="59ff6-131">hızlı ve kolay tooset ayarlama</span><span class="sxs-lookup"><span data-stu-id="59ff6-131">it is quick and easy tooset up</span></span>  
- <span data-ttu-id="59ff6-132">Her bir karma bağlantı bir mükemmel güvenlik durum olan tooa tek ana bilgisayar: bağlantı noktası birleşimi ile eşleşir</span><span class="sxs-lookup"><span data-stu-id="59ff6-132">each hybrid connection matches tooa single host:port combination which is an excellent security aspect</span></span>
- <span data-ttu-id="59ff6-133">Merhaba bağlantıları standart web bağlantı noktaları üzerinden giden tüm olduğu gibi normalde güvenlik duvarı delik gerektirmez</span><span class="sxs-lookup"><span data-stu-id="59ff6-133">it normally does not require firewall holes as hello connections are all outbound over standard web ports</span></span>
- <span data-ttu-id="59ff6-134">Merhaba özelliği anlamına da ağ düzeyi olduğundan hello bitiş noktası tarafından kullanılan uygulama ve hello teknoloji tarafından kullanılan belirsiz toohello dilini değildir</span><span class="sxs-lookup"><span data-stu-id="59ff6-134">because hello feature is network level that also means that it is agnostic toohello language used by your app and hello technology used by hello endpoint</span></span>
- <span data-ttu-id="59ff6-135">Bu olabilir tek bir uygulama birden çok ağlarda kullanılan tooprovide erişim</span><span class="sxs-lookup"><span data-stu-id="59ff6-135">it can be used tooprovide access in multiple networks from a single app</span></span> 

### <a name="things-you-cannot-do-with-hybrid-connections"></a><span data-ttu-id="59ff6-136">Karma bağlantılar ile yapamayacağı noktalar</span><span class="sxs-lookup"><span data-stu-id="59ff6-136">Things you cannot do with Hybrid Connections</span></span> ###

<span data-ttu-id="59ff6-137">Karma bağlantılar ile yapamayacağınız birkaç şey vardır ve bunlar şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="59ff6-137">There are a few things you cannot do with hybrid connections and they include:</span></span>

- <span data-ttu-id="59ff6-138">bir sürücü bağlama</span><span class="sxs-lookup"><span data-stu-id="59ff6-138">mounting a drive</span></span>
- <span data-ttu-id="59ff6-139">UDP kullanma</span><span class="sxs-lookup"><span data-stu-id="59ff6-139">using UDP</span></span>
- <span data-ttu-id="59ff6-140">FTP Pasif modu veya genişletilmiş Pasif modu gibi dinamik bağlantı noktaları kullanan hizmetler dayalı TCP erişme</span><span class="sxs-lookup"><span data-stu-id="59ff6-140">accessing TCP based services that use dynamic ports such as FTP Passive Mode or Extended Passive Mode</span></span>
- <span data-ttu-id="59ff6-141">UDP şekliyle bazen LDAP desteği gerektirir</span><span class="sxs-lookup"><span data-stu-id="59ff6-141">LDAP support, as it sometimes requires UDP</span></span>
- <span data-ttu-id="59ff6-142">Active Directory desteği</span><span class="sxs-lookup"><span data-stu-id="59ff6-142">Active Directory support</span></span>

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a><span data-ttu-id="59ff6-143">Ekleme ve uygulamanızda karma bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="59ff6-143">Adding and Creating a Hybrid Connection in your App</span></span> ##

<span data-ttu-id="59ff6-144">Karma bağlantılar hello uygulama portalı üzerinden veya hello karma bağlantı hizmet portalından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-144">Hybrid Connections can be created through hello app portal or from hello Hybrid Connection service portal.</span></span>  <span data-ttu-id="59ff6-145">Merhaba uygulama portal toocreate hello karma bağlantılar, uygulamanızı toouse istediğiniz kullanmak önerilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-145">It is highly recommended that you use hello app portal toocreate hello Hybrid Connections you wish toouse with your app.</span></span>  <span data-ttu-id="59ff6-146">Karma bağlantı toocreate Git toohello [Azure portal] [ portal] ve uygulamanız için kullanıcı Arabirimi hello uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="59ff6-146">toocreate a Hybrid Connection go toohello [Azure portal][portal] and go into hello UI for your app.</span></span>  <span data-ttu-id="59ff6-147">Seçin **Ağ > karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="59ff6-147">Select **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="59ff6-148">Buradan, uygulamanızı yapılandırılmış hello karma bağlantılar görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59ff6-148">From here you can see hello Hybrid Connections that are configured with your app</span></span>  

![][2]

<span data-ttu-id="59ff6-149">Yeni bir karma bağlantı tooadd karma Bağlantı Ekle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="59ff6-149">tooadd a new Hybrid Connection, click Add Hybrid Connection.</span></span>  <span data-ttu-id="59ff6-150">Merhaba açılan UI hello karma bağlantılar'de, önceden oluşturduğunuz listeler.</span><span class="sxs-lookup"><span data-stu-id="59ff6-150">hello UI that opens up lists hello Hybrid Connections that you have already created.</span></span>  <span data-ttu-id="59ff6-151">bir veya daha fazla bunların tooadd tooyour uygulama, istediğiniz ve isabet hello olanları tıklatıldığında **Ekle seçili karma bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="59ff6-151">tooadd one or more of them tooyour app, click on hello ones you want and hit **Add selected hybrid connection**.</span></span>  

![][3]

<span data-ttu-id="59ff6-152">Yeni bir karma bağlantı toocreate istiyorsanız, **yeni karma bağlantı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="59ff6-152">If you want toocreate a new Hybrid Connection, click **Create new hybrid connection**.</span></span>  <span data-ttu-id="59ff6-153">Buradan belirtin:</span><span class="sxs-lookup"><span data-stu-id="59ff6-153">From here you specify the:</span></span> 

- <span data-ttu-id="59ff6-154">uç nokta adı</span><span class="sxs-lookup"><span data-stu-id="59ff6-154">endpoint name</span></span>
- <span data-ttu-id="59ff6-155">uç noktası ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="59ff6-155">endpoint hostname</span></span>
- <span data-ttu-id="59ff6-156">uç nokta bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="59ff6-156">endpoint port</span></span>
- <span data-ttu-id="59ff6-157">servicebus ad alanı toouse istiyor</span><span class="sxs-lookup"><span data-stu-id="59ff6-157">servicebus namespace you wish toouse</span></span>

![][4]

<span data-ttu-id="59ff6-158">Her karma bağlantı bağlı tooa hizmet veri yolu ad alanıdır ve her hizmet veri yolu ad alanı bir Azure bölgesinde.</span><span class="sxs-lookup"><span data-stu-id="59ff6-158">Every hybrid connection is tied tooa service bus namespace and each service bus namespace is in an Azure region.</span></span>  <span data-ttu-id="59ff6-159">Tootry ve bir hizmet veri yolu ad alanında kullanım uygulamanızı aynı bölgede tooavoid kopyaladığınızda ağ gecikmesi olarak şekilde hello önemlidir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-159">It is important tootry and use a service bus namespace in hello same region as your app so as tooavoid network induced latency.</span></span>

<span data-ttu-id="59ff6-160">Uygulamanızdan karma bağlantınız tooremove istiyorsanız, sağ tıklayın ve seçin **Bağlantıyı Kes**.</span><span class="sxs-lookup"><span data-stu-id="59ff6-160">If you want tooremove your hybrid connection from your app, right click on it and select **Disconnect**.</span></span>  

<span data-ttu-id="59ff6-161">Karma bağlantı tooyour web uygulaması eklendikten sonra Ayrıntılar üzerinde yalnızca tıklayarak görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59ff6-161">Once a hybrid connection is added tooyour web app, you can see details on it by simply clicking on it.</span></span>  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a><span data-ttu-id="59ff6-162">Karma bağlantılar ve uygulama hizmeti planları</span><span class="sxs-lookup"><span data-stu-id="59ff6-162">Hybrid Connections and App Service Plans</span></span> ##

<span data-ttu-id="59ff6-163">Şimdi yapabileceğiniz hello yalnızca karma bağlantılar hello yeni karma bağlantılar ' dir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-163">hello only hybrid connections you can now make are hello new hybrid connections.</span></span>  <span data-ttu-id="59ff6-164">Yalnızca temel, standart, Premium ve SKU'ları fiyatlandırması Isolated kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-164">They are only available in Basic, Standard, Premium and Isolated pricing SKUs.</span></span>  <span data-ttu-id="59ff6-165">Plan fiyatlandırması bağlı sınırları toohello vardır.</span><span class="sxs-lookup"><span data-stu-id="59ff6-165">There are limits tied toohello pricing plan.</span></span>  

| <span data-ttu-id="59ff6-166">Plan fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="59ff6-166">Pricing Plan</span></span> | <span data-ttu-id="59ff6-167">Karma bağlantılar hello planında kullanılabilir sayısı</span><span class="sxs-lookup"><span data-stu-id="59ff6-167">Number of hybrid connections usable in hello plan</span></span> |
|----|----|
| <span data-ttu-id="59ff6-168">Temel</span><span class="sxs-lookup"><span data-stu-id="59ff6-168">Basic</span></span> | <span data-ttu-id="59ff6-169">5</span><span class="sxs-lookup"><span data-stu-id="59ff6-169">5</span></span> |
| <span data-ttu-id="59ff6-170">Standart</span><span class="sxs-lookup"><span data-stu-id="59ff6-170">Standard</span></span> | <span data-ttu-id="59ff6-171">25</span><span class="sxs-lookup"><span data-stu-id="59ff6-171">25</span></span> |
| <span data-ttu-id="59ff6-172">Premium</span><span class="sxs-lookup"><span data-stu-id="59ff6-172">Premium</span></span> | <span data-ttu-id="59ff6-173">200</span><span class="sxs-lookup"><span data-stu-id="59ff6-173">200</span></span> |
| <span data-ttu-id="59ff6-174">Yalıtılmış</span><span class="sxs-lookup"><span data-stu-id="59ff6-174">Isolated</span></span> | <span data-ttu-id="59ff6-175">200</span><span class="sxs-lookup"><span data-stu-id="59ff6-175">200</span></span> |

<span data-ttu-id="59ff6-176">Uygulama hizmeti planı kısıtlamaları bulunmaktadır UI hello kaç karma bağlantılar kullanıldığını gösterir App Service planı ve hangi uygulamaların bu yana.</span><span class="sxs-lookup"><span data-stu-id="59ff6-176">Since there are App Service Plan restrictions there is also UI in hello App Service Plan that shows you how many hybrid connections are being used and by what apps.</span></span>  

![][6]

<span data-ttu-id="59ff6-177">Gibi hello uygulama görünümüyle ayrıntıları karma bağlantınız tıklayarak görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59ff6-177">Just as with hello app view, you can see details on your hybrid connection by clicking on it.</span></span>  <span data-ttu-id="59ff6-178">Merhaba uygulama Sergi sahip tüm hello bilgileri görebilir, ancak kaç hello uygulamalarında da görebilirsiniz burada gösterilen hello özelliklerinde aynı App Service planı kullandığınız Bu karma bağlantı.</span><span class="sxs-lookup"><span data-stu-id="59ff6-178">In hello properties shown here you can see all hello information you had at hello app view but can also see how many other apps in hello same App Service Plan are using that hybrid connection.</span></span>

![][7]

<span data-ttu-id="59ff6-179">Bir uygulama hizmeti planı'nda kullanılabilir karma bağlantı uç hello sayısına bir sınır olsa da, bu uygulama hizmeti planı uygulamalarda herhangi bir sayıda genelinde kullanılan her karma bağlantı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-179">While there is a limit on hello number of hybrid connection endpoints that can be used in an App Service Plan, each hybrid connection used can be used across any number of apps in that App Service Plan.</span></span>  <span data-ttu-id="59ff6-180">My uygulama hizmeti planı'nda 5 ayrı uygulamalarında kullandım 1 karma bağlantı varsa, yine yalnızca 1 karma bağlantı olduğunu toosay olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="59ff6-180">That is toosay that if I had 1 hybrid connection that I used in 5 separate apps in my App Service Plan, that is still just 1 hybrid connection.</span></span>

<span data-ttu-id="59ff6-181">Yalnızca temel, standart, Premium veya yalıtılmış SKU içinde kullanılabilir olan ötesinde ek maliyet toohybrid bağlantıları yoktur.</span><span class="sxs-lookup"><span data-stu-id="59ff6-181">There is an additional cost toohybrid connections beyond being only usable in a Basic, Standard, Premium or Isolated SKU.</span></span>  <span data-ttu-id="59ff6-182">Karma bağlantı fiyatlandırma hakkında ayrıntılar lütfen buraya gidin: [Service Bus fiyatlandırma][sbpricing].</span><span class="sxs-lookup"><span data-stu-id="59ff6-182">For details on hybrid connection pricing please go here: [Service Bus pricing][sbpricing].</span></span>

## <a name="hybrid-connection-manager"></a><span data-ttu-id="59ff6-183">Karma Bağlantı Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="59ff6-183">Hybrid Connection Manager</span></span> ##

<span data-ttu-id="59ff6-184">Karma bağlantılar toowork sırayla geçiş aracısı, karma bağlantı uç noktasını barındıran hello ağdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-184">In order for hybrid connections toowork you need a relay agent in hello network that hosts your hybrid connection endpoint.</span></span>  <span data-ttu-id="59ff6-185">Bu geçiş aracısı hello karma Bağlantı Yöneticisi (HCM) adı verilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-185">That relay agent is called hello Hybrid Connection Manager (HCM).</span></span>  <span data-ttu-id="59ff6-186">Bu araç hello indirilebilir **Ağ > karma bağlantı uç noktalarınızı yapılandırın** UI hello uygulamanızda kullanılabilir [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="59ff6-186">This tool can be downloaded from hello **Networking > Configure your hybrid connection endpoints** UI available from your app in hello [Azure portal][portal].</span></span>  

<span data-ttu-id="59ff6-187">Bu araç, Windows server 2008 R2 ve Windows'un sonraki sürümlerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="59ff6-187">This tool runs on Windows server 2008 R2 and later versions of Windows.</span></span>  <span data-ttu-id="59ff6-188">Bir kez yüklendikten sonra hello HCM bir hizmet olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="59ff6-188">Once installed hello HCM runs as a service.</span></span>  <span data-ttu-id="59ff6-189">Bu hizmet yapılandırılmış hello uç noktalarda dayalı tooAzure servicebus geçiş bağlanır.</span><span class="sxs-lookup"><span data-stu-id="59ff6-189">This service connects tooAzure servicebus relay based on hello configured endpoints.</span></span>  <span data-ttu-id="59ff6-190">Merhaba HCM Hello bağlantılarından 80 ve 443 giden tooports ' dir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-190">hello connections from hello HCM are outbound tooports 80 and 443.</span></span>    

<span data-ttu-id="59ff6-191">Merhaba HCM sahip bir kullanıcı Arabirimi tooconfigure onu.</span><span class="sxs-lookup"><span data-stu-id="59ff6-191">hello HCM has a UI tooconfigure it.</span></span>  <span data-ttu-id="59ff6-192">HCM yüklü hello sonra hello karma Bağlantı Yöneticisi'ni yükleme dizininde bulunur HybridConnectionManagerUi.exe hello çalıştırarak UI hello kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59ff6-192">After hello HCM is installed you can bring up hello UI by running hello HybridConnectionManagerUi.exe that sits in hello Hybrid Connection Manager installation directory.</span></span>  <span data-ttu-id="59ff6-193">Yazarak Windows 10'da kolayca ulaşıldığında *karma Bağlantı Yöneticisi kullanıcı Arabirimi* , arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="59ff6-193">It is also easily reached on Windows 10 by typing *Hybrid Connection Manager UI* in your search box.</span></span>  

<span data-ttu-id="59ff6-194">HCM kullanıcı Arabirimi başlatıldığında, hello hello ilk şey, bkz: Merhaba HCM'ın bu örneğinin yapılandırılmış hello karma bağlantılar tümünün listeleyen bir tablo durumdur.</span><span class="sxs-lookup"><span data-stu-id="59ff6-194">When hello HCM UI is started, hello first thing you see is a table that lists all of hello hybrid connections that are configured with this instance of hello HCM.</span></span>  <span data-ttu-id="59ff6-195">Herhangi bir değişiklik toomake isterseniz Azure ile tooauthenticate gerekir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-195">If you wish toomake any changes you will need tooauthenticate with Azure.</span></span> 

<span data-ttu-id="59ff6-196">tooadd bir veya daha fazla karma bağlantılar tooyour HCM:</span><span class="sxs-lookup"><span data-stu-id="59ff6-196">tooadd one or more Hybrid Connections tooyour HCM:</span></span>

1. <span data-ttu-id="59ff6-197">Merhaba HCM UI Başlat</span><span class="sxs-lookup"><span data-stu-id="59ff6-197">Start hello HCM UI</span></span>
1. <span data-ttu-id="59ff6-198">Başka bir karma bağlantı yapılandırmak tıklayın![][8]</span><span class="sxs-lookup"><span data-stu-id="59ff6-198">Click Configure another hybrid connection ![][8]</span></span>

1. <span data-ttu-id="59ff6-199">Azure hesabınızla oturum açın</span><span class="sxs-lookup"><span data-stu-id="59ff6-199">Sign in with your Azure account</span></span>
1. <span data-ttu-id="59ff6-200">Bir abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="59ff6-200">Choose a subscription</span></span>
1. <span data-ttu-id="59ff6-201">' I tıklatın Bu HCM toorelay istediğiniz hello karma bağlantıları![][9]</span><span class="sxs-lookup"><span data-stu-id="59ff6-201">Click on hello hybrid connections you want this HCM toorelay ![][9]</span></span>

1. <span data-ttu-id="59ff6-202">Kaydet’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="59ff6-202">Click Save</span></span>

<span data-ttu-id="59ff6-203">Bu noktada eklediğiniz hello karma bağlantılar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="59ff6-203">At this point you will see hello hybrid connections you added.</span></span>  <span data-ttu-id="59ff6-204">Ayrıca, yapılandırılmış hello karma bağlantıda tıklatın ve hello bağlantı ayrıntılarını bakın.</span><span class="sxs-lookup"><span data-stu-id="59ff6-204">You can also click on hello configured hybrid connection and see details about hello connection.</span></span>

![][10]

<span data-ttu-id="59ff6-205">İle yapılandırılmış HCM toobe mümkün toosupport hello karma bağlantılarınız için onu gerekir:</span><span class="sxs-lookup"><span data-stu-id="59ff6-205">For your HCM toobe able toosupport hello hybrid connections it is configured with, it needs:</span></span>

- <span data-ttu-id="59ff6-206">TCP bağlantı noktaları 80 ve 443 üzerinden erişim tooAzure</span><span class="sxs-lookup"><span data-stu-id="59ff6-206">TCP access tooAzure over ports 80 and 443</span></span>
- <span data-ttu-id="59ff6-207">TCP erişim toohello karma bağlantı uç noktasının</span><span class="sxs-lookup"><span data-stu-id="59ff6-207">TCP access toohello hybrid connection endpoint</span></span>
- <span data-ttu-id="59ff6-208">özelliği toodo DNS aramalarına hello uç noktası ana bilgisayar ve hello azure servicebus ad alanı</span><span class="sxs-lookup"><span data-stu-id="59ff6-208">ability toodo DNS look ups on hello endpoint host and hello azure servicebus namespace</span></span>

<span data-ttu-id="59ff6-209">Merhaba HCM, hem yeni karma bağlantılar, hem de hello eski BizTalk karma bağlantılar destekler.</span><span class="sxs-lookup"><span data-stu-id="59ff6-209">hello HCM supports both new hybrid connections as well as hello older BizTalk hybrid connections.</span></span>

### <a name="redundancy"></a><span data-ttu-id="59ff6-210">Yedeklilik</span><span class="sxs-lookup"><span data-stu-id="59ff6-210">Redundancy</span></span> ###

<span data-ttu-id="59ff6-211">Her HCM, birden çok karma bağlantılar destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-211">Each HCM can support multiple hybrid connections.</span></span>  <span data-ttu-id="59ff6-212">Ayrıca, herhangi bir belirtilen karma bağlantıyı birden çok HCMs tarafından desteklenebilir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-212">Also, any given hybrid connection can be supported by multiple HCMs.</span></span>  <span data-ttu-id="59ff6-213">Merhaba varsayılan davranışı tooround bir kez deneme trafik hello arasında HCMs herhangi belirli bir uç nokta için yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="59ff6-213">hello default behavior is tooround robin traffic across hello configured HCMs for any given endpoint.</span></span>  <span data-ttu-id="59ff6-214">Yüksek kullanılabilirlik, karma bağlantılar ağınızdan isterseniz, yalnızca birden çok HCMs ayrı makinelerde örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="59ff6-214">If you want high availability on your hybrid connections from your network, simply instantiate multiple HCMs on separate machines.</span></span> 

### <a name="manually-adding-a-hybrid-connection"></a><span data-ttu-id="59ff6-215">El ile karma bağlantı ekleme</span><span class="sxs-lookup"><span data-stu-id="59ff6-215">Manually adding a hybrid connection</span></span> ###

<span data-ttu-id="59ff6-216">Birisi, abonelik toohost dışında verilen karma bağlantı için bir HCM örneği istiyorsanız, bunları paylaşabilirsiniz hello hello karma bağlantı için ağ geçidi bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="59ff6-216">If you wish somebody outside of your subscription toohost an HCM instance for a given hybrid connection, you can share with them hello gateway connection string for hello hybrid connection.</span></span>  <span data-ttu-id="59ff6-217">Bu hello içinde karma bağlantı hello özelliklerinde görebilirsiniz [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="59ff6-217">You can see this in hello properties for a hybrid connection in hello [Azure portal][portal].</span></span> <span data-ttu-id="59ff6-218">dize, toouse tıklatın hello **el ile yapılandırmanız** düğmesini hello HCM ve hello ağ geçidi bağlantı dizesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="59ff6-218">toouse that string, click hello **Configure manually** button in hello HCM and paste in hello gateway connection string.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="59ff6-219">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="59ff6-219">Troubleshooting</span></span> ##

<span data-ttu-id="59ff6-220">Ne zaman karma bağlantınız ile çalışan bir uygulama ayarlanır ve yapılandırılmış Bu karma bağlantısı olan en az bir HCM yoktur sonra hello durum söyleyin **bağlı** hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="59ff6-220">When your hybrid connection is set up with a running application and there is at least one HCM that has that hybrid connection configured, then hello status will say **Connected** in hello portal.</span></span>  <span data-ttu-id="59ff6-221">Değil dediği varsa **bağlı** uygulamanızı çalışmıyor veya, HCM tooAzure 80 veya 443 bağlantı noktalarında giden bağlanamıyor anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-221">If it does not say **Connected** then it means that either your app is down or your HCM cannot connect out tooAzure on ports 80 or 443.</span></span>  

<span data-ttu-id="59ff6-222">Merhaba uç noktası bir DNS adı yerine bir IP adresi kullanarak belirtilmediğinden istemciler tootheir endpoint bağlanamıyor hello birincil nedenidir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-222">hello primary reason that clients cannot connect tootheir endpoint is because hello endpoint was specified using an IP address instead of a DNS name.</span></span>  <span data-ttu-id="59ff6-223">Uygulamanızı istenen hello endpoint ulaşamıyor ve bir IP adresi kullandıysanız toousing hello HCM çalıştığı hello konakta geçerli bir DNS adı geçin.</span><span class="sxs-lookup"><span data-stu-id="59ff6-223">If your app cannot reach hello desired endpoint and you used an IP address, switch toousing a DNS name that is valid on hello host where hello HCM is running.</span></span>  <span data-ttu-id="59ff6-224">Diğer şeyleri toocheck olduğunuz nerede hello HCM çalıştıran sunucunun ve hello HCM toohello karma bağlantı uç noktasının çalıştığı hello ana bilgisayardan bağlantısı yok hello ana bilgisayarda bu hello DNS adı düzgün çözümler.</span><span class="sxs-lookup"><span data-stu-id="59ff6-224">Other things toocheck are that hello DNS name resolves properly on hello host where hello HCM is running and that there is connectivity from hello host where hello HCM is running toohello hybrid connection endpoint.</span></span>  

<span data-ttu-id="59ff6-225">Merhaba tcpping adlı hello konsolundan etkinleştirilebilir uygulama hizmeti bir aracı yoktur.</span><span class="sxs-lookup"><span data-stu-id="59ff6-225">There is a tool in hello App Service that can be invoked from hello console called tcpping.</span></span>  <span data-ttu-id="59ff6-226">Bu araç erişim tooa TCP uç noktası sahip ancak erişim tooa karma bağlantı uç noktasının varsa söylemez anlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59ff6-226">This tool can tell you if you have access tooa TCP endpoint but does not tell you if you have access tooa hybrid connection endpoint.</span></span>  <span data-ttu-id="59ff6-227">Karma bağlantı uç noktasının karşı hello konsolunda kullanıldığında, başarılı bir ping işlemi yalnızca bu ana bilgisayar: bağlantı noktası bileşimi kullanan uygulamanız için yapılandırılmış karma bağlantı olduğunu söyler.</span><span class="sxs-lookup"><span data-stu-id="59ff6-227">When used in hello console against a hybrid connection endpoint, a successful ping will only tell you that you have a hybrid connection configured for your app that uses that host:port combination.</span></span>  

## <a name="biztalk-hybrid-connections"></a><span data-ttu-id="59ff6-228">BizTalk Karma Bağlantıları</span><span class="sxs-lookup"><span data-stu-id="59ff6-228">BizTalk Hybrid Connections</span></span> ##

<span data-ttu-id="59ff6-229">Merhaba eski BizTalk karma bağlantılar özelliği devre dışı toofurther BizTalk karma bağlantı oluşturmaları kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="59ff6-229">hello older BizTalk Hybrid Connections capability has been closed off toofurther BizTalk Hybrid Connection creations.</span></span>  <span data-ttu-id="59ff6-230">Önceden var olan BizTalk karma bağlantılarınızı uygulamalarınızı ile kullanmaya devam edebilirsiniz ancak toohello yeni hizmet geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-230">You can continue using your preexisting BizTalk Hybrid Connections with your apps but should migrate toohello new service.</span></span>  <span data-ttu-id="59ff6-231">Merhaba arasında hello BizTalk sürüm üzerinden hello yeni hizmetindeki yararlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="59ff6-231">Among hello benefits in hello new service over hello BizTalk version are:</span></span>

- <span data-ttu-id="59ff6-232">hiçbir ek BizTalk hesabı gereklidir</span><span class="sxs-lookup"><span data-stu-id="59ff6-232">no additional BizTalk account is required</span></span>
- <span data-ttu-id="59ff6-233">TLS 1.2 BizTalk karma bağlantılar olduğu gibi 1.0 yerine olduğu</span><span class="sxs-lookup"><span data-stu-id="59ff6-233">TLS is 1.2 instead of 1.0 as in BizTalk Hybrid Connections</span></span>
- <span data-ttu-id="59ff6-234">İletişim diğer bağlantı noktaları 80 ve 443 bir IP adresi yerine Azure DNS ad tooreach ve bir dizi ek kullanarak bağlantı noktaları üzerinden önemlidir.</span><span class="sxs-lookup"><span data-stu-id="59ff6-234">Communication is over ports 80 and 443 using a DNS name tooreach Azure instead of IP addresses and a range of additional other ports.</span></span>  

<span data-ttu-id="59ff6-235">tooadd bir BizTalk karma bağlantı tooyour uygulaması hello gidin tooyour uygulamada [Azure portal] [ portal] tıklatıp **Ağ > karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="59ff6-235">tooadd a BizTalk hybrid connection tooyour app, go tooyour app in hello [Azure portal][portal] and click **Networking > Configure your hybrid connection endpoints**.</span></span>  <span data-ttu-id="59ff6-236">Merhaba Klasik karma bağlantıları tabloda tıklatın **Klasik karma Bağlantı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="59ff6-236">In hello Classic hybrid connections table click **Add classic hybrid connection**.</span></span>  <span data-ttu-id="59ff6-237">Buradan, BizTalk karma bağlantılar listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="59ff6-237">From here you will see a list of your BizTalk hybrid connections.</span></span>  


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

