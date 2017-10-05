---
title: "Azure Traffic Manager ayarlarını doğrulayın | Microsoft Docs"
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
ms.openlocfilehash: aadff1806a7cb22347283143563467366e857569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="verify-traffic-manager-settings"></a><span data-ttu-id="5d30a-103">Trafik Yöneticisi ayarlarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="5d30a-103">Verify Traffic Manager settings</span></span>

<span data-ttu-id="5d30a-104">Trafik Yöneticisi ayarlarınızı sınamak için birden çok, çeşitli yerlerde testleri çalıştırma istemciniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-104">To test your Traffic Manager settings, you need to have multiple clients, in various locations, from which you can run your tests.</span></span> <span data-ttu-id="5d30a-105">Ardından, bir kerede aşağı Traffic Manager profilinize uç noktaları getirin.</span><span class="sxs-lookup"><span data-stu-id="5d30a-105">Then, bring the endpoints in your Traffic Manager profile down one at a time.</span></span>

* <span data-ttu-id="5d30a-106">Hızlı bir şekilde (örneğin, 30 saniye) değişiklikleri yaymak şekilde DNS TTL değeri düşük ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5d30a-106">Set the DNS TTL value low so that changes propagate quickly (for example, 30 seconds).</span></span>
* <span data-ttu-id="5d30a-107">Azure bulut hizmetlerinizi ve Web siteleri test ettiğiniz profilinde IP adreslerini bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d30a-107">Know the IP addresses of your Azure cloud services and websites in the profile you are testing.</span></span>
* <span data-ttu-id="5d30a-108">Bir IP adresi için DNS adını çözümlemek ve bu adresi görüntülemek olanak sağlayan araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="5d30a-108">Use tools that let you resolve a DNS name to an IP address and display that address.</span></span>

<span data-ttu-id="5d30a-109">DNS adlarını IP adreslerine profilinizde uç noktaları çözmek görmek için denetleniyor.</span><span class="sxs-lookup"><span data-stu-id="5d30a-109">You are checking to see that the DNS names resolve to IP addresses of the endpoints in your profile.</span></span> <span data-ttu-id="5d30a-110">Adları trafik Yöneticisi profilinde tanımlanmış trafik yönlendirme yöntemini ile tutarlı şekilde çözümlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-110">The names should resolve in a manner consistent with the traffic routing method defined in the Traffic Manager profile.</span></span> <span data-ttu-id="5d30a-111">Gibi araçları kullanabilirsiniz **nslookup** veya **derinliklerine** DNS adlarını çözümlemek için.</span><span class="sxs-lookup"><span data-stu-id="5d30a-111">You can use the tools like **nslookup** or **dig** to resolve DNS names.</span></span>

<span data-ttu-id="5d30a-112">Aşağıdaki örnekler, Traffic Manager profilinizin test yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5d30a-112">The following examples help you test your Traffic Manager profile.</span></span>

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a><span data-ttu-id="5d30a-113">Trafik Yöneticisi profili nslookup ve ipconfig Windows'da kullanma denetleyin</span><span class="sxs-lookup"><span data-stu-id="5d30a-113">Check Traffic Manager profile using nslookup and ipconfig in Windows</span></span>

1. <span data-ttu-id="5d30a-114">Bir komut veya Windows PowerShell komut istemini yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="5d30a-114">Open a command or Windows PowerShell prompt as an administrator.</span></span>
2. <span data-ttu-id="5d30a-115">Tür `ipconfig /flushdns` DNS çözümleyicisi önbelleğini temizlemek için.</span><span class="sxs-lookup"><span data-stu-id="5d30a-115">Type `ipconfig /flushdns` to flush the DNS resolver cache.</span></span>
3. <span data-ttu-id="5d30a-116">`nslookup <your Traffic Manager domain name>` yazın.</span><span class="sxs-lookup"><span data-stu-id="5d30a-116">Type `nslookup <your Traffic Manager domain name>`.</span></span> <span data-ttu-id="5d30a-117">Örneğin, aşağıdaki komutu ön ek etki alanı adıyla denetler *myapp.contoso*</span><span class="sxs-lookup"><span data-stu-id="5d30a-117">For example, the following command checks the domain name with the prefix *myapp.contoso*</span></span>

        nslookup myapp.contoso.trafficmanager.net

    <span data-ttu-id="5d30a-118">Normal sonuç, aşağıdaki bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="5d30a-118">A typical result shows the following information:</span></span>

    + <span data-ttu-id="5d30a-119">Bu trafik yöneticisi etki alanı adı çözümlemek için erişilen DNS sunucusunun IP adresini ve DNS adı.</span><span class="sxs-lookup"><span data-stu-id="5d30a-119">The DNS name and IP address of the DNS server being accessed to resolve this Traffic Manager domain name.</span></span>
    + <span data-ttu-id="5d30a-120">Trafik yöneticisi etki alanı adı komut satırında, trafik yöneticisi etki alanı çözümler IP adresi ve "nslookup" sonra yazdığınız.</span><span class="sxs-lookup"><span data-stu-id="5d30a-120">The Traffic Manager domain name you typed on the command line after "nslookup" and the IP address to which the Traffic Manager domain resolves.</span></span> <span data-ttu-id="5d30a-121">İkinci IP adresi denetlemek için önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-121">The second IP address is the important one to check.</span></span> <span data-ttu-id="5d30a-122">Bulut Hizmetleri veya test ettiğiniz trafik Yöneticisi profili Web sitelerinde biri için bir genel sanal IP (VIP) adresi eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-122">It should match a public virtual IP (VIP) address for one of the cloud services or websites in the Traffic Manager profile you are testing.</span></span>

## <a name="how-to-test-the-failover-traffic-routing-method"></a><span data-ttu-id="5d30a-123">Yük devretme trafik yönlendirme yöntemini test etme</span><span class="sxs-lookup"><span data-stu-id="5d30a-123">How to test the failover traffic routing method</span></span>

1. <span data-ttu-id="5d30a-124">Yukarı tüm uç noktaları bırakın.</span><span class="sxs-lookup"><span data-stu-id="5d30a-124">Leave all endpoints up.</span></span>
2. <span data-ttu-id="5d30a-125">Tek bir istemci kullanarak, DNS çözümlemesi nslookup veya benzer bir yardımcı programını kullanarak, şirketinizin etki alanı adı isteyin.</span><span class="sxs-lookup"><span data-stu-id="5d30a-125">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="5d30a-126">Çözümlenen IP adresini birincil endpoint eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5d30a-126">Ensure that the resolved IP address matches the primary endpoint.</span></span>
4. <span data-ttu-id="5d30a-127">Bu trafik Yöneticisi uygulama kapalı olduğunu düşündüğü izleme dosyayı kaldırın veya birincil uç noktanızı getirin.</span><span class="sxs-lookup"><span data-stu-id="5d30a-127">Bring down your primary endpoint or remove the monitoring file so that Traffic Manager thinks that the application is down.</span></span>
5. <span data-ttu-id="5d30a-128">DNS zaman yaşam için (TTL) trafik Yöneticisi profili ve iki dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5d30a-128">Wait for the DNS Time-to-Live (TTL) of the Traffic Manager profile plus an additional two minutes.</span></span> <span data-ttu-id="5d30a-129">Örneğin, DNS TTL 300 saniye (5 dakika) ise, yedi dakika beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-129">For example, if your DNS TTL is 300 seconds (5 minutes), you must wait for seven minutes.</span></span>
6. <span data-ttu-id="5d30a-130">Nslookup kullanarak DNS istemci önbelleği ve istek DNS çözümlemenizin temizlenir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-130">Flush your DNS client cache and request DNS resolution using nslookup.</span></span> <span data-ttu-id="5d30a-131">Windows'da ipconfig/flushdns komutuyla, DNS önbelleğini boşaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d30a-131">In Windows, you can flush your DNS cache with the ipconfig /flushdns command.</span></span>
7. <span data-ttu-id="5d30a-132">Çözümlenen IP adresini ikincil uç noktanız eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5d30a-132">Ensure that the resolved IP address matches your secondary endpoint.</span></span>
8. <span data-ttu-id="5d30a-133">Her uç noktası sırayla hale getirme işlemi yineleyin.</span><span class="sxs-lookup"><span data-stu-id="5d30a-133">Repeat the process, bringing down each endpoint in turn.</span></span> <span data-ttu-id="5d30a-134">DNS sonraki uç noktası IP adresi listesinde döndürdüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5d30a-134">Verify that the DNS returns the IP address of the next endpoint in the list.</span></span> <span data-ttu-id="5d30a-135">Tüm uç noktaları kapalı olduğunda, birincil uç noktası IP adresi yeniden edinmelidir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-135">When all endpoints are down, you should obtain the IP address of the primary endpoint again.</span></span>

## <a name="how-to-test-the-weighted-traffic-routing-method"></a><span data-ttu-id="5d30a-136">Ağırlıklı trafik yönlendirme yöntemini test etme</span><span class="sxs-lookup"><span data-stu-id="5d30a-136">How to test the weighted traffic routing method</span></span>

1. <span data-ttu-id="5d30a-137">Yukarı tüm uç noktaları bırakın.</span><span class="sxs-lookup"><span data-stu-id="5d30a-137">Leave all endpoints up.</span></span>
2. <span data-ttu-id="5d30a-138">Tek bir istemci kullanarak, DNS çözümlemesi nslookup veya benzer bir yardımcı programını kullanarak, şirketinizin etki alanı adı isteyin.</span><span class="sxs-lookup"><span data-stu-id="5d30a-138">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="5d30a-139">Çözümlenen IP adresini noktalarınızı birini eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5d30a-139">Ensure that the resolved IP address matches one of your endpoints.</span></span>
4. <span data-ttu-id="5d30a-140">DNS istemci önbelleğini temizlemek ve her uç noktası için 2 ve 3. adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="5d30a-140">Flush your DNS client cache and repeat steps 2 and 3 for each endpoint.</span></span> <span data-ttu-id="5d30a-141">Her uç noktalarınızı için döndürülen farklı IP adreslerini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-141">You should see different IP addresses returned for each of your endpoints.</span></span>

## <a name="how-to-test-the-performance-traffic-routing-method"></a><span data-ttu-id="5d30a-142">Performans trafik yönlendirme yöntemini test etme</span><span class="sxs-lookup"><span data-stu-id="5d30a-142">How to test the performance traffic routing method</span></span>

<span data-ttu-id="5d30a-143">Etkili bir şekilde performans trafik yönlendirme yöntemini sınamak için dünyanın farklı bölümlerinde bulunan istemciler olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-143">To effectively test a performance traffic routing method, you must have clients located in different parts of the world.</span></span> <span data-ttu-id="5d30a-144">İstemcileri hizmetlerinizi test etmek için kullanılan farklı Azure bölgelerinde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d30a-144">You can create clients in different Azure regions that can be used to test your services.</span></span> <span data-ttu-id="5d30a-145">Genel bir ağ varsa, uzaktan dünya diğer bölümlerinde istemciler için oturum açın ve buradan testleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5d30a-145">If you have a global network, you can remotely sign in to clients in other parts of the world and run your tests from there.</span></span>

<span data-ttu-id="5d30a-146">Alternatif olarak, ücretsiz web tabanlı DNS araması ve vardır kullanılabilir hizmetler derinliklerine.</span><span class="sxs-lookup"><span data-stu-id="5d30a-146">Alternatively, there are free web-based DNS lookup and dig services available.</span></span> <span data-ttu-id="5d30a-147">Bu araçlardan bazıları dünyanın çeşitli konumlardan DNS adı çözümlemesini denetleyin olanağı verir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-147">Some of these tools give you the ability to check DNS name resolution from various locations around the world.</span></span> <span data-ttu-id="5d30a-148">Örnekler "DNS aramalarında" araması yapın.</span><span class="sxs-lookup"><span data-stu-id="5d30a-148">Do a search on "DNS lookup" for examples.</span></span> <span data-ttu-id="5d30a-149">Gomez veya açılış konuşması gibi üçüncü taraf hizmetleri profillerinizi trafiği beklendiği gibi dağıtıyorsanız onaylamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5d30a-149">Third-party services like Gomez or Keynote can be used to confirm that your profiles are distributing traffic as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d30a-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5d30a-150">Next steps</span></span>

* [<span data-ttu-id="5d30a-151">Traffic Manager trafik yönlendirme yöntemleri hakkında</span><span class="sxs-lookup"><span data-stu-id="5d30a-151">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="5d30a-152">Traffic Manager için performans konuları</span><span class="sxs-lookup"><span data-stu-id="5d30a-152">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="5d30a-153">Düzeyi düşürülmüş Traffic Manager durumu için sorun giderme</span><span class="sxs-lookup"><span data-stu-id="5d30a-153">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
