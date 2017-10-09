---
title: "aaaTroubleshooting durum üzerinde Azure Traffic Manager düşürülmüş"
description: "Nasıl olarak gösteriliyorsa tootroubleshoot Traffic Manager profillerini durumu düzeyi."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="d51f1-103">Durum üzerinde Azure Traffic Manager düşürülmüş sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="d51f1-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="d51f1-104">Bu makalede nasıl tootroubleshoot bir Azure Traffic Manager profilini düşürülmüş durumunu gösteren açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d51f1-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="d51f1-105">Bu senaryo için cloudapp.net barındırılan hizmetlerinizi toosome işaret eden bir Traffic Manager profilini yapılandırdığınız göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d51f1-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="d51f1-106">Merhaba sistem durumu, trafik Yöneticisi'nin görüntülerse bir **Degraded** durum sonra bir veya daha fazla uç noktaları hello durumunu olabilir **Degraded**:</span><span class="sxs-lookup"><span data-stu-id="d51f1-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![düzeyi düşürülmüş uç nokta durumu](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="d51f1-108">Merhaba sistem durumu, trafik Yöneticisi'nin görüntülerse bir **devre dışı** durum sonra her iki uç noktaları olabilir **devre dışı**:</span><span class="sxs-lookup"><span data-stu-id="d51f1-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Etkin olmayan trafik Yöneticisi durumu](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="d51f1-110">Trafik Yöneticisi anlama yoklamaları</span><span class="sxs-lookup"><span data-stu-id="d51f1-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="d51f1-111">Trafik Yöneticisi yalnızca hello araştırma bir HTTP 200 yanıtı aldığında çevrimiçi yedekleme hello araştırma yolundan bir uç nokta toobe göz önünde bulundurur.</span><span class="sxs-lookup"><span data-stu-id="d51f1-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="d51f1-112">Başka bir harici 200 yanıtı bir hatadır.</span><span class="sxs-lookup"><span data-stu-id="d51f1-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="d51f1-113">Merhaba URL döndürür bir 200 yeniden yönlendirilen olsa bile 30 x yeniden yönlendirme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d51f1-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="d51f1-114">HTTPs araştırmaları için sertifika hataları göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="d51f1-115">bir 200 döndürülen sürece hello araştırma yolunun hello gerçek içeriği önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="d51f1-116">Bir URL toosome statik içerik benzer yoklama "/ favicon.ico" ortak bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="d51f1-117">Merhaba uygulaması sağlıklı olsa bile hello ASP sayfalarının gibi dinamik içerik 200, her zaman döndürmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="d51f1-118">Tooset hello araştırma site hello yeterli mantığı toodetermine sahip yolu toosomething yukarı veya aşağı olan en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="d51f1-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="d51f1-119">"Hello önceki örnekte, ayarlayarak yolu too"/favicon.ico Hello ifadesini, yalnızca olduğunuz bu w3wp.exe sınama yanıt.</span><span class="sxs-lookup"><span data-stu-id="d51f1-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="d51f1-120">Bu araştırma, web uygulamanızın sağlıklı olduğunu göstermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="d51f1-121">Daha iyi bir seçenek tooset yolu tooa bir şey gibi olacaktır "/ Probe.aspx" Merhaba site mantığı toodetermine hello durumunu sahip.</span><span class="sxs-lookup"><span data-stu-id="d51f1-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="d51f1-122">Örneğin, performans sayaçları tooCPU kullanımı veya ölçü hello başarısız istek sayısı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d51f1-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="d51f1-123">Veya tooaccess veritabanı kaynakları veya oturum durumu toomake Merhaba web uygulaması çalıştığından emin çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="d51f1-124">Bir profildeki tüm uç noktaları düşürülmüş, trafik Yöneticisi tüm uç noktalar olarak sağlıklı değerlendirir sonra ve yolları tooall uç noktaları trafiği.</span><span class="sxs-lookup"><span data-stu-id="d51f1-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="d51f1-125">Bu davranış, mekanizması yoklama hello sorunları hizmetinizin tam bir kesinti içinde yol açmamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d51f1-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d51f1-126">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d51f1-126">Troubleshooting</span></span>

<span data-ttu-id="d51f1-127">bir araştırma hatası tootroubleshoot hello HTTP durum kodu hello araştırma URL'den dönüş gösteren bir aracı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="d51f1-128">Ham HTTP yanıtı hello gösteren birçok araçları vardır.</span><span class="sxs-lookup"><span data-stu-id="d51f1-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="d51f1-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="d51f1-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="d51f1-130">Curl</span><span class="sxs-lookup"><span data-stu-id="d51f1-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="d51f1-131">wget</span><span class="sxs-lookup"><span data-stu-id="d51f1-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="d51f1-132">Ayrıca, Internet Explorer tooview hello HTTP yanıtlarını hello F12 hata ayıklama araçlarını hello ağ sekmesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d51f1-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="d51f1-133">Bu örneğin toosee hello bizim araştırma URL'si yanıttan istiyoruz: http://watestsdp2008r2.cloudapp.net:80/araştırma.</span><span class="sxs-lookup"><span data-stu-id="d51f1-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="d51f1-134">Aşağıdaki PowerShell örneğine hello hello sorun gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="d51f1-135">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="d51f1-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="d51f1-136">Yeniden yönlendirme yanıtı aldık dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d51f1-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="d51f1-137">Daha önce tüm StatusCode dışında belirtildiği gibi 200 bir hata olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="d51f1-138">Trafik Yöneticisi değişiklikleri uç nokta durumu tooOffline hello.</span><span class="sxs-lookup"><span data-stu-id="d51f1-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="d51f1-139">tooresolve hello sorun uygun StatusCode hello onay hello Web sitesi yapılandırma tooensure hello araştırma yolundan döndürülebilir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="d51f1-140">Bir 200 döndüren hello trafik Yöneticisi araştırma toopoint tooa yolu yeniden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d51f1-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="d51f1-141">Araştırma hello HTTPS protokolünü kullanıyorsanız, test sırasında tooavoid SSL/TLS hataları denetleme toodisable sertifika gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d51f1-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="d51f1-142">Merhaba aşağıdaki PowerShell ifadeleri hello geçerli PowerShell oturumunda sertifika doğrulaması devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="d51f1-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="d51f1-143">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d51f1-143">Next Steps</span></span>

[<span data-ttu-id="d51f1-144">Traffic Manager trafik yönlendirme yöntemleri hakkında</span><span class="sxs-lookup"><span data-stu-id="d51f1-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="d51f1-145">Trafik Yöneticisi nedir</span><span class="sxs-lookup"><span data-stu-id="d51f1-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="d51f1-146">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d51f1-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="d51f1-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="d51f1-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="d51f1-148">Traffic Manager üzerindeki işlemler (REST API Başvurusu)</span><span class="sxs-lookup"><span data-stu-id="d51f1-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="d51f1-149">[Azure Traffic Manager cmdlet'leri][1]</span><span class="sxs-lookup"><span data-stu-id="d51f1-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
