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
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Durum üzerinde Azure Traffic Manager düşürülmüş sorunlarını giderme

Bu makalede nasıl tootroubleshoot bir Azure Traffic Manager profilini düşürülmüş durumunu gösteren açıklanmaktadır. Bu senaryo için cloudapp.net barındırılan hizmetlerinizi toosome işaret eden bir Traffic Manager profilini yapılandırdığınız göz önünde bulundurun. Merhaba sistem durumu, trafik Yöneticisi'nin görüntülerse bir **Degraded** durum sonra bir veya daha fazla uç noktaları hello durumunu olabilir **Degraded**:

![düzeyi düşürülmüş uç nokta durumu](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Merhaba sistem durumu, trafik Yöneticisi'nin görüntülerse bir **devre dışı** durum sonra her iki uç noktaları olabilir **devre dışı**:

![Etkin olmayan trafik Yöneticisi durumu](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Trafik Yöneticisi anlama yoklamaları

* Trafik Yöneticisi yalnızca hello araştırma bir HTTP 200 yanıtı aldığında çevrimiçi yedekleme hello araştırma yolundan bir uç nokta toobe göz önünde bulundurur. Başka bir harici 200 yanıtı bir hatadır.
* Merhaba URL döndürür bir 200 yeniden yönlendirilen olsa bile 30 x yeniden yönlendirme başarısız olur.
* HTTPs araştırmaları için sertifika hataları göz ardı edilir.
* bir 200 döndürülen sürece hello araştırma yolunun hello gerçek içeriği önemli değildir. Bir URL toosome statik içerik benzer yoklama "/ favicon.ico" ortak bir tekniktir. Merhaba uygulaması sağlıklı olsa bile hello ASP sayfalarının gibi dinamik içerik 200, her zaman döndürmeyebilir.
* Tooset hello araştırma site hello yeterli mantığı toodetermine sahip yolu toosomething yukarı veya aşağı olan en iyi uygulamadır. "Hello önceki örnekte, ayarlayarak yolu too"/favicon.ico Hello ifadesini, yalnızca olduğunuz bu w3wp.exe sınama yanıt. Bu araştırma, web uygulamanızın sağlıklı olduğunu göstermeyebilir. Daha iyi bir seçenek tooset yolu tooa bir şey gibi olacaktır "/ Probe.aspx" Merhaba site mantığı toodetermine hello durumunu sahip. Örneğin, performans sayaçları tooCPU kullanımı veya ölçü hello başarısız istek sayısı kullanabilirsiniz. Veya tooaccess veritabanı kaynakları veya oturum durumu toomake Merhaba web uygulaması çalıştığından emin çalışabilir.
* Bir profildeki tüm uç noktaları düşürülmüş, trafik Yöneticisi tüm uç noktalar olarak sağlıklı değerlendirir sonra ve yolları tooall uç noktaları trafiği. Bu davranış, mekanizması yoklama hello sorunları hizmetinizin tam bir kesinti içinde yol açmamasını sağlar.

## <a name="troubleshooting"></a>Sorun giderme

bir araştırma hatası tootroubleshoot hello HTTP durum kodu hello araştırma URL'den dönüş gösteren bir aracı gerekir. Ham HTTP yanıtı hello gösteren birçok araçları vardır.

* [Fiddler](http://www.telerik.com/fiddler)
* [Curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

Ayrıca, Internet Explorer tooview hello HTTP yanıtlarını hello F12 hata ayıklama araçlarını hello ağ sekmesini kullanabilirsiniz.

Bu örneğin toosee hello bizim araştırma URL'si yanıttan istiyoruz: http://watestsdp2008r2.cloudapp.net:80/araştırma. Aşağıdaki PowerShell örneğine hello hello sorun gösterilmektedir.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

Örnek çıktı:

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

Yeniden yönlendirme yanıtı aldık dikkat edin. Daha önce tüm StatusCode dışında belirtildiği gibi 200 bir hata olarak kabul edilir. Trafik Yöneticisi değişiklikleri uç nokta durumu tooOffline hello. tooresolve hello sorun uygun StatusCode hello onay hello Web sitesi yapılandırma tooensure hello araştırma yolundan döndürülebilir. Bir 200 döndüren hello trafik Yöneticisi araştırma toopoint tooa yolu yeniden yapılandırın.

Araştırma hello HTTPS protokolünü kullanıyorsanız, test sırasında tooavoid SSL/TLS hataları denetleme toodisable sertifika gerekebilir. Merhaba aşağıdaki PowerShell ifadeleri hello geçerli PowerShell oturumunda sertifika doğrulaması devre dışı bırakın:

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

## <a name="next-steps"></a>Sonraki Adımlar

[Traffic Manager trafik yönlendirme yöntemleri hakkında](traffic-manager-routing-methods.md)

[Trafik Yöneticisi nedir](traffic-manager-overview.md)

[Cloud Services](http://go.microsoft.com/fwlink/?LinkId=314074)

[Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/)

[Traffic Manager üzerindeki işlemler (REST API Başvurusu)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Azure Traffic Manager cmdlet'leri][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
