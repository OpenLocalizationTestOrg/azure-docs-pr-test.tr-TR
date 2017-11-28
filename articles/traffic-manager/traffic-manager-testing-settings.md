---
title: "aaaVerify Azure Traffic Manager ayarları | Microsoft Docs"
description: "Bu makalede, trafik Yöneticisi ayarlarınızı doğrulamanıza yardımcı olur"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a><span data-ttu-id="f2e7c-103">Trafik Yöneticisi ayarlarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="f2e7c-103">Verify Traffic Manager settings</span></span>

<span data-ttu-id="f2e7c-104">tootest trafik Yöneticisi ayarlarınızı içinden çalıştırabilirsiniz testlerinizi çeşitli konumlarda birden çok istemci toohave gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-104">tootest your Traffic Manager settings, you need toohave multiple clients, in various locations, from which you can run your tests.</span></span> <span data-ttu-id="f2e7c-105">Ardından, bir kerede aşağı Traffic Manager profilinize hello uç noktaları getirin.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-105">Then, bring hello endpoints in your Traffic Manager profile down one at a time.</span></span>

* <span data-ttu-id="f2e7c-106">Hızlı bir şekilde (örneğin, 30 saniye) değişiklikleri yaymak şekilde hello DNS TTL değeri düşük ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-106">Set hello DNS TTL value low so that changes propagate quickly (for example, 30 seconds).</span></span>
* <span data-ttu-id="f2e7c-107">Hello Azure bulut hizmetlerine ve hello profilinde test ettiğiniz Web sitelerine IP adreslerini bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-107">Know hello IP addresses of your Azure cloud services and websites in hello profile you are testing.</span></span>
* <span data-ttu-id="f2e7c-108">Bir DNS adı tooan IP adresi çözmek ve bu adresi görüntülemek olanak sağlayan araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-108">Use tools that let you resolve a DNS name tooan IP address and display that address.</span></span>

<span data-ttu-id="f2e7c-109">Merhaba DNS adlarını hello uç noktaları profilinizde tooIP adresleri çözümleyecek toosee denetleniyor.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-109">You are checking toosee that hello DNS names resolve tooIP addresses of hello endpoints in your profile.</span></span> <span data-ttu-id="f2e7c-110">Merhaba adları hello trafik yönlendirme yöntemini hello trafik Yöneticisi profili tanımlanan ile tutarlı şekilde çözümlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-110">hello names should resolve in a manner consistent with hello traffic routing method defined in hello Traffic Manager profile.</span></span> <span data-ttu-id="f2e7c-111">Merhaba araçları gibi kullanabilirsiniz **nslookup** veya **derinliklerine** tooresolve DNS adları.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-111">You can use hello tools like **nslookup** or **dig** tooresolve DNS names.</span></span>

<span data-ttu-id="f2e7c-112">Merhaba aşağıdaki örneklerde, Traffic Manager profilinizin test yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-112">hello following examples help you test your Traffic Manager profile.</span></span>

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a><span data-ttu-id="f2e7c-113">Trafik Yöneticisi profili nslookup ve ipconfig Windows'da kullanma denetleyin</span><span class="sxs-lookup"><span data-stu-id="f2e7c-113">Check Traffic Manager profile using nslookup and ipconfig in Windows</span></span>

1. <span data-ttu-id="f2e7c-114">Bir komut veya Windows PowerShell komut istemini yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-114">Open a command or Windows PowerShell prompt as an administrator.</span></span>
2. <span data-ttu-id="f2e7c-115">Tür `ipconfig /flushdns` tooflush hello DNS çözümleyicisi önbelleği.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-115">Type `ipconfig /flushdns` tooflush hello DNS resolver cache.</span></span>
3. <span data-ttu-id="f2e7c-116">`nslookup <your Traffic Manager domain name>` yazın.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-116">Type `nslookup <your Traffic Manager domain name>`.</span></span> <span data-ttu-id="f2e7c-117">Örneğin, denetimleri hello hello önek etki alanı adıyla komutu aşağıdaki hello *myapp.contoso*</span><span class="sxs-lookup"><span data-stu-id="f2e7c-117">For example, hello following command checks hello domain name with hello prefix *myapp.contoso*</span></span>

        nslookup myapp.contoso.trafficmanager.net

    <span data-ttu-id="f2e7c-118">Tipik bir sonuç bilgisinden hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="f2e7c-118">A typical result shows hello following information:</span></span>

    + <span data-ttu-id="f2e7c-119">Merhaba DNS adı ve IP adresi hello DNS sunucusu olma tooresolve Bu trafik yöneticisi etki alanı adı erişilir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-119">hello DNS name and IP address of hello DNS server being accessed tooresolve this Traffic Manager domain name.</span></span>
    + <span data-ttu-id="f2e7c-120">Merhaba trafik yöneticisi etki alanı adı "nslookup sonra" Merhaba komut satırında yazılan ve başlangıç IP adresi toowhich hello trafik yöneticisi etki alanı giderir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-120">hello Traffic Manager domain name you typed on hello command line after "nslookup" and hello IP address toowhich hello Traffic Manager domain resolves.</span></span> <span data-ttu-id="f2e7c-121">Merhaba önemli bir toocheck Hello ikinci IP adresi değil.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-121">hello second IP address is hello important one toocheck.</span></span> <span data-ttu-id="f2e7c-122">Merhaba bulut Hizmetleri veya hello trafik Yöneticisi profili test ettiğiniz Web sitelerinde biri için bir genel sanal IP (VIP) adresi eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-122">It should match a public virtual IP (VIP) address for one of hello cloud services or websites in hello Traffic Manager profile you are testing.</span></span>

## <a name="how-tootest-hello-failover-traffic-routing-method"></a><span data-ttu-id="f2e7c-123">Nasıl tootest hello yük devretme trafik yönlendirme yöntemi</span><span class="sxs-lookup"><span data-stu-id="f2e7c-123">How tootest hello failover traffic routing method</span></span>

1. <span data-ttu-id="f2e7c-124">Yukarı tüm uç noktaları bırakın.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-124">Leave all endpoints up.</span></span>
2. <span data-ttu-id="f2e7c-125">Tek bir istemci kullanarak, DNS çözümlemesi nslookup veya benzer bir yardımcı programını kullanarak, şirketinizin etki alanı adı isteyin.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-125">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="f2e7c-126">IP adresi hello birincil uç noktayla eşleşen bu hello çözülmüş emin olun.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-126">Ensure that hello resolved IP address matches hello primary endpoint.</span></span>
4. <span data-ttu-id="f2e7c-127">Kapalı olduğu, uygulama Merhaba trafik Yöneticisi düşündüğü böylece dosya izleme hello kaldırın veya birincil uç noktanızı getirin.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-127">Bring down your primary endpoint or remove hello monitoring file so that Traffic Manager thinks that hello application is down.</span></span>
5. <span data-ttu-id="f2e7c-128">Merhaba DNS için-yaşam süresi (TTL) hello trafik Yöneticisi profilinin artı iki dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-128">Wait for hello DNS Time-to-Live (TTL) of hello Traffic Manager profile plus an additional two minutes.</span></span> <span data-ttu-id="f2e7c-129">Örneğin, DNS TTL 300 saniye (5 dakika) ise, yedi dakika beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-129">For example, if your DNS TTL is 300 seconds (5 minutes), you must wait for seven minutes.</span></span>
6. <span data-ttu-id="f2e7c-130">Nslookup kullanarak DNS istemci önbelleği ve istek DNS çözümlemenizin temizlenir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-130">Flush your DNS client cache and request DNS resolution using nslookup.</span></span> <span data-ttu-id="f2e7c-131">Windows hello ipconfig/flushdns komutuyla, DNS önbelleğini boşaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-131">In Windows, you can flush your DNS cache with hello ipconfig /flushdns command.</span></span>
7. <span data-ttu-id="f2e7c-132">IP adresi, ikincil uç noktayla eşleşen bu hello çözülmüş emin olun.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-132">Ensure that hello resolved IP address matches your secondary endpoint.</span></span>
8. <span data-ttu-id="f2e7c-133">Her uç noktası sırayla getiren hello işlemi yineleyin.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-133">Repeat hello process, bringing down each endpoint in turn.</span></span> <span data-ttu-id="f2e7c-134">Bu hello DNS hello IP adresi hello sonraki uç noktasının hello listesinde döndürür doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-134">Verify that hello DNS returns hello IP address of hello next endpoint in hello list.</span></span> <span data-ttu-id="f2e7c-135">Tüm uç noktaları kapalı olduğunda, başlangıç IP adresi hello birincil uç noktasının yeniden edinmelidir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-135">When all endpoints are down, you should obtain hello IP address of hello primary endpoint again.</span></span>

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a><span data-ttu-id="f2e7c-136">Trafik yönlendirme yöntemini nasıl tootest hello ağırlıklı</span><span class="sxs-lookup"><span data-stu-id="f2e7c-136">How tootest hello weighted traffic routing method</span></span>

1. <span data-ttu-id="f2e7c-137">Yukarı tüm uç noktaları bırakın.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-137">Leave all endpoints up.</span></span>
2. <span data-ttu-id="f2e7c-138">Tek bir istemci kullanarak, DNS çözümlemesi nslookup veya benzer bir yardımcı programını kullanarak, şirketinizin etki alanı adı isteyin.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-138">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="f2e7c-139">IP adresi noktalarınızı biriyle eşleşen bu hello çözülmüş emin olun.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-139">Ensure that hello resolved IP address matches one of your endpoints.</span></span>
4. <span data-ttu-id="f2e7c-140">DNS istemci önbelleğini temizlemek ve her uç noktası için 2 ve 3. adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-140">Flush your DNS client cache and repeat steps 2 and 3 for each endpoint.</span></span> <span data-ttu-id="f2e7c-141">Her uç noktalarınızı için döndürülen farklı IP adreslerini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-141">You should see different IP addresses returned for each of your endpoints.</span></span>

## <a name="how-tootest-hello-performance-traffic-routing-method"></a><span data-ttu-id="f2e7c-142">Nasıl tootest hello performans trafik yönlendirme yöntemi</span><span class="sxs-lookup"><span data-stu-id="f2e7c-142">How tootest hello performance traffic routing method</span></span>

<span data-ttu-id="f2e7c-143">tooeffectively test performans trafik yönlendirme yöntemini, hello world farklı bölümlerinde bulunan istemciler olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-143">tooeffectively test a performance traffic routing method, you must have clients located in different parts of hello world.</span></span> <span data-ttu-id="f2e7c-144">İstemcileri hizmetlerinizi kullanılan tootest olabilir farklı Azure bölgelerinde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-144">You can create clients in different Azure regions that can be used tootest your services.</span></span> <span data-ttu-id="f2e7c-145">Genel bir ağ varsa, uzaktan oturum açma tooclients Merhaba Dünya diğer bölümlerinde ve buradan testleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-145">If you have a global network, you can remotely sign in tooclients in other parts of hello world and run your tests from there.</span></span>

<span data-ttu-id="f2e7c-146">Alternatif olarak, ücretsiz web tabanlı DNS araması ve vardır kullanılabilir hizmetler derinliklerine.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-146">Alternatively, there are free web-based DNS lookup and dig services available.</span></span> <span data-ttu-id="f2e7c-147">Bunlardan bazıları özelliği toocheck DNS ad çözümlemesi Merhaba Dünya çeşitli konumlardan hello verin araçları.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-147">Some of these tools give you hello ability toocheck DNS name resolution from various locations around hello world.</span></span> <span data-ttu-id="f2e7c-148">Örnekler "DNS aramalarında" araması yapın.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-148">Do a search on "DNS lookup" for examples.</span></span> <span data-ttu-id="f2e7c-149">Gomez veya açılış konuşması gibi üçüncü taraf hizmetleri profillerinizi trafiği beklendiği gibi dağıtıyorsanız kullanılan tooconfirm olabilir.</span><span class="sxs-lookup"><span data-stu-id="f2e7c-149">Third-party services like Gomez or Keynote can be used tooconfirm that your profiles are distributing traffic as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2e7c-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f2e7c-150">Next steps</span></span>

* [<span data-ttu-id="f2e7c-151">Traffic Manager trafik yönlendirme yöntemleri hakkında</span><span class="sxs-lookup"><span data-stu-id="f2e7c-151">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="f2e7c-152">Traffic Manager için performans konuları</span><span class="sxs-lookup"><span data-stu-id="f2e7c-152">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="f2e7c-153">Düzeyi düşürülmüş Traffic Manager durumu için sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f2e7c-153">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
