---
title: "Durum üzerinde Azure Traffic Manager düşürülmüş sorunlarını giderme"
description: "Traffic Manager profillerini olarak gösteriliyorsa ile ilgili sorunları giderme durumu düzeyi."
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
ms.openlocfilehash: b1d00fb84695d2289f37647f55a7c56cf28c8c96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="9ae23-103">Durum üzerinde Azure Traffic Manager düşürülmüş sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="9ae23-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="9ae23-104">Bu makalede, düzeyi düşürülmüş durumunu gösteren bir Azure Traffic Manager profilini sorun giderme açıklar.</span><span class="sxs-lookup"><span data-stu-id="9ae23-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="9ae23-105">Bu senaryo için bazı cloudapp.net barındırılan hizmetlerinizi işaret eden bir Traffic Manager profilini yapılandırdığınız göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9ae23-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span></span> <span data-ttu-id="9ae23-106">Sistem durumu, trafik Yöneticisi'nin görüntülerse bir **Degraded** durum sonra bir veya daha fazla uç noktaları durumunu olabilir **Degraded**:</span><span class="sxs-lookup"><span data-stu-id="9ae23-106">If the health of your Traffic Manager displays a **Degraded** status, then the status of one or more endpoints may be **Degraded**:</span></span>

![düzeyi düşürülmüş uç nokta durumu](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="9ae23-108">Sistem durumu, trafik Yöneticisi'nin görüntülerse bir **devre dışı** durum sonra her iki uç noktaları olabilir **devre dışı**:</span><span class="sxs-lookup"><span data-stu-id="9ae23-108">If the health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Etkin olmayan trafik Yöneticisi durumu](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="9ae23-110">Trafik Yöneticisi anlama yoklamaları</span><span class="sxs-lookup"><span data-stu-id="9ae23-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="9ae23-111">Trafik Yöneticisi yalnızca araştırma araştırma yolundan bir HTTP 200 yanıtı aldığında çevrimiçi olması için bir uç nokta göz önünde bulundurur.</span><span class="sxs-lookup"><span data-stu-id="9ae23-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span></span> <span data-ttu-id="9ae23-112">Başka bir harici 200 yanıtı bir hatadır.</span><span class="sxs-lookup"><span data-stu-id="9ae23-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="9ae23-113">Yeniden yönlendirilen URL bir 200 döndürürse bile 30 x yeniden yönlendirme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="9ae23-113">A 30x redirect fails, even if the redirected URL returns a 200.</span></span>
* <span data-ttu-id="9ae23-114">HTTPs araştırmaları için sertifika hataları göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="9ae23-115">Bir 200 döndürülen sürece araştırma yolu gerçek içeriği önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="9ae23-116">Yoklama gibi bazı statik içerik için bir URL "/ favicon.ico" ortak bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="9ae23-117">Uygulama sağlıklı olsa bile ASP sayfalarının gibi dinamik içerik 200, her zaman döndürmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span></span>
* <span data-ttu-id="9ae23-118">Sitenin yukarı veya aşağı olduğunu belirlemek için yeterli mantığı içeren bir araştırma yolunu ayarlama en iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="9ae23-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span></span> <span data-ttu-id="9ae23-119">Yolun ayarlayarak önceki örnekte, "/ favicon.ico", yalnızca olduğunuz bu w3wp.exe sınama yanıt.</span><span class="sxs-lookup"><span data-stu-id="9ae23-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="9ae23-120">Bu araştırma, web uygulamanızın sağlıklı olduğunu göstermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="9ae23-121">Bir yol gibi bir şeye ayarlamak için daha iyi bir seçenek olacaktır "/ Probe.aspx" sitenin durumunu belirlemek için mantığı vardır.</span><span class="sxs-lookup"><span data-stu-id="9ae23-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span></span> <span data-ttu-id="9ae23-122">Örneğin, CPU kullanımı için performans sayaçları kullanın veya başarısız istek sayısı ölçün.</span><span class="sxs-lookup"><span data-stu-id="9ae23-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span></span> <span data-ttu-id="9ae23-123">Veya veritabanı kaynakları veya web uygulamasının çalıştığından emin olmak için oturum durumu erişme girişimi.</span><span class="sxs-lookup"><span data-stu-id="9ae23-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span></span>
* <span data-ttu-id="9ae23-124">Bir profildeki tüm uç noktaları düşürülmüş, ardından trafik Yöneticisi tüm uç noktalar olarak sağlıklı ve yollar trafiğini tüm uç noktalara değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span></span> <span data-ttu-id="9ae23-125">Bu davranış, araştırma mekanizması sorunları hizmetinizin tam bir kesinti içinde yol açmamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ae23-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9ae23-126">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="9ae23-126">Troubleshooting</span></span>

<span data-ttu-id="9ae23-127">Bir araştırma hatası gidermek için HTTP durum kodu araştırma URL'den dönüş gösteren bir aracı gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span></span> <span data-ttu-id="9ae23-128">Kullanılabilir ham HTTP yanıtı gösteren birçok araç vardır.</span><span class="sxs-lookup"><span data-stu-id="9ae23-128">There are many tools available that show you the raw HTTP response.</span></span>

* [<span data-ttu-id="9ae23-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="9ae23-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="9ae23-130">Curl</span><span class="sxs-lookup"><span data-stu-id="9ae23-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="9ae23-131">wget</span><span class="sxs-lookup"><span data-stu-id="9ae23-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="9ae23-132">Ayrıca, HTTP yanıtları görüntülemek için Internet Explorer'da F12 hata ayıklama araçları'nın Ağ sekmesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae23-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span></span>

<span data-ttu-id="9ae23-133">Bizim araştırma URL'si yanıttan görmeyi istiyoruz Bu, örneğin: http://watestsdp2008r2.cloudapp.net:80/araştırma.</span><span class="sxs-lookup"><span data-stu-id="9ae23-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="9ae23-134">Aşağıdaki PowerShell örneğinde sorun gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-134">The following PowerShell example illustrates the problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="9ae23-135">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="9ae23-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="9ae23-136">Yeniden yönlendirme yanıtı aldık dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9ae23-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="9ae23-137">Daha önce tüm StatusCode dışında belirtildiği gibi 200 bir hata olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="9ae23-138">Trafik Yöneticisi uç noktası durumu çevrimdışı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-138">Traffic Manager changes the endpoint status to Offline.</span></span> <span data-ttu-id="9ae23-139">Sorunu gidermek için uygun StatusCode araştırma yolundan döndürüldüğünden emin olunması için Web sitesi yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae23-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span></span> <span data-ttu-id="9ae23-140">Trafik Yöneticisi araştırma bir 200 döndüren bir yolunu işaret edecek şekilde yeniden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9ae23-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span></span>

<span data-ttu-id="9ae23-141">Araştırma HTTPS protokolünü kullanıyorsanız, sertifika, test sırasında SSL/TLS hatalarını önlemek için denetlemeyi devre dışı bırakmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="9ae23-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="9ae23-142">Aşağıdaki PowerShell ifadeleri geçerli PowerShell oturumunda sertifika doğrulaması devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="9ae23-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9ae23-143">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9ae23-143">Next Steps</span></span>

[<span data-ttu-id="9ae23-144">Traffic Manager trafik yönlendirme yöntemleri hakkında</span><span class="sxs-lookup"><span data-stu-id="9ae23-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="9ae23-145">Trafik Yöneticisi nedir</span><span class="sxs-lookup"><span data-stu-id="9ae23-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="9ae23-146">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="9ae23-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="9ae23-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="9ae23-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="9ae23-148">Traffic Manager üzerindeki işlemler (REST API Başvurusu)</span><span class="sxs-lookup"><span data-stu-id="9ae23-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="9ae23-149">[Azure Traffic Manager cmdlet'leri][1]</span><span class="sxs-lookup"><span data-stu-id="9ae23-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
