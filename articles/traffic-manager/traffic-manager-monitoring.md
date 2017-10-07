---
title: "aaaAzure trafik Yöneticisi uç nokta izleme | Microsoft Docs"
description: "Bu makalede, uç nokta izleme ve otomatik uç nokta yük devretme toohelp Azure trafik Yöneticisi nasıl kullandığını anlamanıza yardımcı olabilir müşterilerin, yüksek kullanılabilirlik uygulamaları dağıtma"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: fff25ac3-d13a-4af9-8916-7c72e3d64bc7
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/22/2017
ms.author: kumud
ms.openlocfilehash: b4862499c88bdb1951833d06199b034a07ac7576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>Trafik Yöneticisi uç nokta izleme

Azure Traffic Manager yerleşik uç nokta izleme ve otomatik uç nokta yük devretme içerir. Bu özellik dayanıklı tooendpoint hatası Azure bölgesi hatalar dahil olmak üzere, yüksek kullanılabilirlik uygulamaları sunmanıza yardımcı olur.

## <a name="configure-endpoint-monitoring"></a>Uç nokta izlemeyi yapılandırma

tooconfigure uç nokta izleme, Traffic Manager profilinize ayarları aşağıdaki hello belirtmeniz gerekir:

* **Protokol**. Trafik Yöneticisi uç noktası toocheck yoklama zaman kullanan hello protokolü olarak HTTP, HTTPS veya TCP, sistem durumunu seçin. HTTPS izleme doğrulamaz, SSL sertifikası geçerli--olup, yalnızca denetler bu hello sertifika varsa.
* **Bağlantı noktası**. Merhaba istek için kullanılan başlangıç bağlantı noktası seçin.
* **Yol**. Bu yapılandırma ayarının belirten hello yolu ayar gereklidir yalnızca hello HTTP ve HTTPS protokolleri için geçerli değil. Bu ayar hello TCP hata izleme Protokolü sonuçlar için sağlama. TCP protokolü için erişimleri izleme bu hello hello göreli yol ve hello hello Web sayfası veya hello dosyanın adını verin. Eğik çizgi (/) hello göreli yolu geçerli bir giriştir. Bu değer hello kök dizininde (varsayılan) bu hello dosyasıdır anlamına gelir.
* **Yoklama aralığı**. Bu değer, ne sıklıkta bir uç nokta Traffic Manager yoklama aracısından sistem durumu denetlenme belirtir. Burada iki değerleri belirtebilirsiniz: 30 (normal yoklama) saniye ile 10 saniye (Hızlı Yoklama). Hiçbir değer sağlanmamışsa hello profil tooa varsayılan değer 30 saniye cinsinden ayarlar. Merhaba ziyaret [trafik Yöneticisi fiyatlandırma](https://azure.microsoft.com/pricing/details/traffic-manager) sayfa toolearn Hızlı Yoklama fiyatlandırma hakkında daha fazla bilgi.
* **Hatalarının sayısı izin**. Bu değer, o uç noktası sağlıksız olarak işaretleme önce bir trafik Yöneticisi yoklama Aracısı göstereceği kaç hataları belirtir. Değeri 0 ile 9 arasında değişebilir. Bir değeri 0 anlamına gelir sorunlu olarak bu uç nokta toobe tek bir izleme başarısız olmasına neden olabilir. Herhangi bir değer belirtilirse, varsayılan değeri 3'hello kullanır.
* **Zaman aşımı izleme**. Bu özellik zaman hello trafik yoklama Aracısı olduğunu düşünmeden önce beklemesi gereken bir sistem durumu denetimi araştırma toohello endpoint gönderildiğinde, bir hatası kontrol Yöneticisi hello miktarını belirtir. Yoklama aralığı too30 saniye sonra ayarlanır hello hello zaman aşımı değeri 5 ve 10 saniye arasında bir değer ayarlarsanız. Herhangi bir değer belirtilirse, varsayılan değer 10 saniye olarak kullanır. Yoklama aralığı too10 saniye sonra ayarlanır hello hello zaman aşımı değeri 5-9 saniye arasında bir değer ayarlarsanız. Hiçbir zaman aşımı değeri belirtilirse, varsayılan değer 9 saniye olarak kullanır.

![Trafik Yöneticisi uç nokta izleme](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**Şekil 1: Trafik Yöneticisi uç nokta izleme**

## <a name="how-endpoint-monitoring-works"></a>Uç nokta izleme nasıl çalışır

İzleme Protokolü hello HTTP veya HTTPS ayarlanırsa, hello trafik Yöneticisi yoklama Aracısı hello protokolü, bağlantı noktası ve verilen göreli bir yol kullanarak bir GET isteği toohello uç noktası sağlar. 200 Tamam yanıt geri alır, bu uç sağlıklı olarak değerlendirilir. Merhaba yanıt farklı bir değer ise veya, belirtilen hello zaman aşımı süresi içinde yanıt alınmazsa, ardından hello Traffic Manager Aracısı yoklama toohello izin numarası, hataları ayarı (Bu ayar 0 ise hiçbir yeniden dener yapılır) according yeniden dener . Ardışık sayısı Hello hello izin numarası, hataları ayarından daha yüksek ise, bu uç sorunlu olarak işaretlenir. 

İzleme Protokolü hello TCP ise, belirtilen başlangıç bağlantı noktası kullanarak bir TCP bağlantısı isteği hello trafik Yöneticisi araştırma aracı başlatır. Sistem durumu denetimi başarılı işaretlenmiş ve hello trafik Yöneticisi yoklama Aracısı hello TCP bağlantısı sıfırlar bir bağlantıyla yanıt tooestablish hello toohello isteği Hello uç noktası yanıt verirse. Merhaba yanıt farklı bir değer ise veya içinde hiçbir yanıt alınmazsa hello zaman aşımı süresi, belirtilen hello Traffic Manager Aracısı yoklama toohello izin numarası, hataları ayarı (Bu ayar 0 hiçbir yeniden çalışır hale getirilir) according yeniden dener. Ardışık sayısı Hello hello izin numarası, hataları ayarından daha yüksek ise, bu uç sağlıksız olarak işaretlenmiş.

Tüm durumlarda trafik Yöneticisi birden çok konumlardan araştırmaları ve her bölge içinde hello ardışık hatası belirleme olur. Bu aynı zamanda uç noktaları sistem durumu araştırmalarının trafik Yöneticisi'nden yoklama aralığı için kullanılan hello ayarından daha yüksek bir sıklıkta almadığı anlamına gelir.

>[!NOTE]
>HTTP veya HTTPS protokolü izleme için yaygın bir hello uç nokta tarafında tooimplement özel bir sayfa, uygulamanızda - Örneğin, /health.aspx uygulamadır. Bu yolu, izleme için kullanarak, uygulamaya özgü denetimleri, performans sayaçları denetleme veya veritabanı kullanılabilirlik doğrulama gibi gerçekleştirebilirsiniz. Bu özel denetimler bağlı olarak, uygun bir HTTP durum kodu hello sayfasını döndürür.

Trafik Yöneticisi profili içindeki tüm uç noktaları izleme ayarlarını paylaşır. Toouse farklı izleme ayarlarını farklı uç noktalar için gerekiyorsa, oluşturabileceğiniz [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings).

## <a name="endpoint-and-profile-status"></a>Uç nokta ve profil durumu

Etkinleştirme ve trafik Yöneticisi profillerinizi ve uç noktaları devre dışı bırakabilirsiniz. Ancak, bir sonuç trafik Yöneticisi'nin ayarlarını ve işlemleri otomatik olarak bir uç nokta durumu değişikliği de oluşabilir.

### <a name="endpoint-status"></a>Uç nokta durumu

Etkinleştirmek veya belirli bir uç noktası devre dışı bırakabilirsiniz. hala sağlıklı olabilir, hello temel alınan hizmet etkilenmez. Değişen hello uç nokta durumu denetimleri hello trafik Yöneticisi Profil uç noktasını hello kullanılabilirliğini hello. Bir uç nokta durumu devre dışı bırakıldığında, trafik Yöneticisi, sistem durumunu denetlemez ve hello uç noktası bir DNS yanıtına dahil edilmez.

### <a name="profile-status"></a>Profil durumu

Hello profil durumu ayarı kullanarak, etkinleştirebilir veya belirli bir profili devre dışı bırakın. Uç nokta durumu tek bir uç nokta etkiler, profil durumu tüm uç noktalar dahil hello tüm profil etkiler. Bir profili devre dışı bıraktığınızda, hello uç noktaları için sistem durumu denetlenmez ve uç nokta bir DNS yanıtına dahil edilir. Bir [NXDOMAIN](https://tools.ietf.org/html/rfc2308) hello DNS sorgusu için yanıt kodunu döndürdü.

### <a name="endpoint-monitor-status"></a>Uç nokta izleme durumu

Uç nokta izleme durumu hello endpoint hello durumunu gösteren bir trafik Yöneticisi tarafından oluşturulan bir değerdir. Bu ayarı el ile değiştirilemiyor. uç nokta izleme sonuçlarını hello birleşimidir ve yapılandırılmış uç noktası durumu hello Hello uç noktası durumunu izleyin. uç nokta izleme durumunu Hello olası değerler aşağıdaki tablonun hello gösterilmektedir:

| Profil durumu | Uç nokta durumu | Uç nokta izleme durumu | Notlar |
| --- | --- | --- | --- |
| Devre dışı |Etkin |Etkin olmayan |Hello profili devre dışı bırakıldı. Merhaba uç nokta durumu etkindir ancak hello profil durumu (devre dışı) önceliklidir. Devre dışı profilleri uç noktalarını izlenmeyen. Bir NXDOMAIN yanıt kodu hello DNS sorgusu için döndürülür. |
| &lt;tüm&gt; |Devre dışı |Devre dışı |Merhaba uç noktası devre dışı bırakıldı. Devre dışı uç noktaları izlenmeyen. Merhaba endpoint DNS yanıtları bulunmaz, bu nedenle, trafiği almaz. |
| Etkin |Etkin |Çevrimiçi |Merhaba uç noktası izlenir ve iyi durumda. DNS yanıtları bulunur ve trafik alabilir. |
| Etkin |Etkin |Düşürülmüş |Uç nokta izleme sistem durumu denetimi başarısız oluyor. Merhaba uç noktası DNS yanıtları bulunmaz ve trafik almaz. <br>Bir özel durum toothis; bu durumda tüm uç noktaları bozulduğunu varsa, bunların tümünün hello sorgu yanıtında toobe değerlendirilir olur).</br>|
| Etkin |Etkin |CheckingEndpoint |Merhaba endpoint izlenen ancak hello ilk araştırmasını hello sonuçlarını henüz alınamadı. CheckingEndpoint genellikle ekleyerek veya bir uç nokta hello profilinde etkinleştirme hemen sonra oluşan geçici bir durumdur. Bu durumdaki bir uç nokta DNS yanıtları bulunur ve trafik alabilir. |
| Etkin |Etkin |Durduruldu |uç noktaları çalışmıyor toois hello hello bulut hizmeti veya web uygulaması. Merhaba bulut hizmeti veya web uygulaması ayarlarını kontrol edin. İç içe geçmiş endpoint yazın ve hello alt profili devre dışı bırakılmış veya etkin değil, Hello uç nokta ise, bu da meydana gelebilir. <br>Bir uç nokta durduruldu durumu olan izlenmiyor. DNS yanıtları bulunmaz ve trafik almaz. Bir özel durum toothis tüm uç noktaları bozulduğunu varsa; bu durumda bunların tümünün hello sorgu yanıtında toobe olarak kabul edilir olduğunu.</br>|

Uç nokta izleme durumu iç içe geçmiş uç noktaları için nasıl hesaplandığını hakkında daha fazla bilgi için bkz [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md).

### <a name="profile-monitor-status"></a>Profil İzleyici durumu

Hello profil İzleyici durumu, yapılandırılmış hello profil durumu ve hello uç nokta İzleyici durum değerleri tüm uç noktalar için birleşimidir. Merhaba olası değerler aşağıdaki tablonun hello açıklanmaktadır:

| (Yapılandırıldığı gibi) profil durumu | Uç nokta izleme durumu | Profil İzleyici durumu | Notlar |
| --- | --- | --- | --- |
| Devre dışı |&lt;tüm&gt; veya bir profille tanımlanmış uç nokta yok. |Devre dışı |Hello profili devre dışı bırakıldı. |
| Etkin |en az bir uç nokta Hello durumunu düşer. |Düşürülmüş |Merhaba tek tek uç nokta durum değerleri toodetermine hangi uç noktaları daha fazla ilgilenilmesi gözden geçirin. |
| Etkin |en az bir uç nokta Hello durumunu çevrimiçi olur. Uç nokta yok Degraded durumuna sahip. |Çevrimiçi |Merhaba hizmeti trafiğini kabul ediyor. Başka bir eylem gerekli değildir. |
| Etkin |Merhaba en az bir uç nokta CheckingEndpoint durumudur. Çevrimiçi veya Degraded durumunu hiçbir noktalarıdır. |CheckingEndpoints |Bu geçiş durumu oluşturduysanız veya etkin bir profili oluşur. Merhaba uç nokta durumu hello için ilk kez olup olmadığı denetleniyor. |
| Etkin |devre dışı veya durdurulmuş Hello durum hello profildeki tüm uç noktalar şunlardır ya da tanımlanmış uç nokta hello profiline sahip. |Etkin olmayan |Uç nokta yok etkindir, ancak hello profili hala etkin. |

## <a name="endpoint-failover-and-recovery"></a>Uç nokta yük devretme ve kurtarma

Trafik Yöneticisi düzenli aralıklarla sağlıksız uç noktalar dahil tüm uç hello durumunu denetler. Trafik Yöneticisi bir uç nokta iyi olur ve geri dönüş getirir algılar.

Olayları aşağıdaki hello hiçbirini oluştuğunda bir uç nokta sağlam değil:
- İzleme Protokolü hello HTTP veya HTTPS ise:
    - (Farklı 2xx kodu veya bir 301/302 yeniden yönlendirme dahil) 200 olmayan yanıt aldı.
- İzleme Protokolü hello TCP ise: 
    - ACK veya Eşitlemeye ACK yanıt toohello eşitleme isteğinde alınan dışında bir yanıt tarafından trafik Yöneticisi tooattempt bağlantı kurma gönderdi.
- Zaman aşımı. 
- Merhaba uç nokta erişilebilir olmaması kaynaklanan herhangi diğer bağlantı sorunu.

Sorun giderme başarısız denetimleri hakkında daha fazla bilgi için bkz: [sorun giderme düşürülmüş durumu Azure Traffic Manager üzerindeki](traffic-manager-troubleshooting-degraded.md). 

Merhaba aşağıdaki zaman çizelgesi Şekil 2'olan ayarları aşağıdaki hello sahip trafik Yöneticisi uç noktası işlemin izlenmesi hello ayrıntılı bir açıklaması: olan HTTP protokolü izleme, yoklama aralığı 30 saniye, toleranslı sayısı 3, zaman aşımı değeri 10 saniye ve DNS TTL 30 saniyedir.

![Trafik Yöneticisi uç nokta yük devretme ve yeniden çalışma dizisi](./media/traffic-manager-monitoring/timeline.png)

**Şekil 2: Yük devretme ve kurtarma trafik Yöneticisi uç noktası sırası**

1. **ALMA**. Her uç noktası için hello trafik Yöneticisi izleme sistemi izleme ayarlarını hello belirtilen hello yolunda bir GET isteği gerçekleştirir.
2. **200 TAMAM**. Sistem izleme hello 10 saniye içinde döndürülen bir HTTP 200 Tamam ileti toobe bekliyor. Bu yanıt aldığında, hello hizmetinin kullanılabilir olduğunu algılar.
3. **Denetimler arasındaki 30 saniye**. Merhaba uç noktası sistem durumu denetimi, her 30 saniyede yinelenir.
4. **Hizmet kullanılamıyor**. Merhaba hizmeti kullanılamaz duruma gelir. Trafik Yöneticisi hello sonraki sistem durumu denetimi kadar bilmez.
5. **Yol izleme denemeleri tooaccess hello**. Sistem izleme hello GET isteği yapar, ancak hello zaman aşımı süresi 10 saniye içinde bir yanıt almaz (Alternatif olarak, 200 yanıt alınması). 30 saniyelik aralıklarda üç kez daha, daha sonra çalışır. Merhaba çalıştığında biri başarılı olursa, deneme sayısını hello sıfırlanır.
6. **Durumu ayarla tooDegraded**. Dördüncü ardışık hatasından sonra sistem izleme hello hello kullanılabilir uç nokta durumu Degraded işaretler.
7. **Trafiğidir yolu saptırabilir tooother uç noktaları**. Merhaba trafik Yöneticisi DNS ad sunucuları güncelleştirilir ve trafik Yöneticisi yanıt tooDNS sorgularda artık hello endpoint döndürür. Yönlendirilmiş tooother, kullanılabilir uç noktaları yeni bağlantılardır. Ancak, bu bitiş noktası içeren önceki DNS yanıtları hala yinelemeli DNS sunucuları ve DNS istemcileri tarafından önbelleğe alınmış olabilir. Merhaba DNS Önbellek süresi doluncaya kadar istemciler toouse hello endpoint devam eder. Merhaba DNS Önbellek süresi gibi istemciler yeni DNS sorguları yapmak ve yönlendirilmiş toodifferent noktalarıdır. Merhaba önbellek süresi hello trafik Yöneticisi profili, örneğin, 30 saniye hello TTL ayarı tarafından denetlenir.
8. **Sistem durumu denetler devam**. Trafik Yöneticisi Degraded durum sahipken toocheck hello durumu hello uç noktasının devam eder. Trafik Yöneticisi Hello endpoint toohealth döndürdüğünde algılar.
9. **Hizmet gelen tekrar çevrimiçi**. Merhaba hizmet kullanılabilir hale gelir. Sistem izleme hello sonraki kendi sistem durumu denetimi gerçekleştirir kadar Degraded durumunu trafik Yöneticisi'nde hello endpoint korur.
10. **Trafik tooservice sürdürür**. Trafik Yöneticisi bir GET isteği gönderir ve 200 Tamam durumu yanıtı alır. Merhaba hizmet tooa iyi duruma döndürüldü. Merhaba trafik Yöneticisi ad sunucuları güncelleştirilir ve DNS yanıtları hello hizmetin DNS adı çıkışı toohand başlayın. Diğer uç noktaları dönüş önbelleğe alınan DNS yanıtları süresinin dolmasını ve varolan bağlantılar olarak tooother uç noktaları sonlandırılır trafiği toohello endpoint döndürür.

    > [!NOTE]
    > Trafik Yöneticisi DNS düzeyi hello çalıştığından, mevcut bağlantıları tooany uç etkilemek olamaz. Trafik Yöneticisi uç noktaları (veya değiştirilen profili ayarları, yük devretme veya yeniden çalışma sırasında) arasındaki trafiği yönlendirir, yeni bağlantıları tooavailable uç nokta yönlendirir. Ancak, bu oturumlar durduruluncaya kadar diğer uç noktaları tooreceive trafiği varolan bağlantılar yoluyla devam edebilir. tooenable trafiği toodrain varolan bağlantılardan uygulamalar her bitiş noktası ile kullanılan bir oturum süresi hello sınırlamanız gerekir.

## <a name="traffic-routing-methods"></a>Trafik yönlendirme yöntemleri

Bir uç nokta Degraded durum olduğunda, artık yanıt tooDNS sorgularda döndürülür. Bunun yerine, alternatif bir uç nokta seçilen döndürülen ve. Merhaba alternatif uç nokta nasıl seçilir Hello profilinde yapılandırılan hello trafik yönlendirme yöntemini belirler.

* **Öncelik**. Uç noktaları öncelikli listesi oluşturur. Merhaba ilk kullanılabilir uç nokta hello listesinde her zaman döndürülür. Bir uç nokta durumu düşürülmüş, hello sonraki kullanılabilir uç nokta döndürülür.
* **Ağırlıklı**. Herhangi bir kullanılabilir uç nokta rastgele atanan ağırlıkları göre seçilir ve diğer kullanılabilir uç noktaları hello ağırlıkları hello.
* **Performans**. Merhaba endpoint en yakın toohello son kullanıcı döndürülür. Bu uç kullanılamıyorsa, bir uç nokta gelen rastgele seçilir tüm kullanılabilir diğer uç noktaları hello. Rastgele bir uç noktasını hello sonraki en yakın endpoint aşırı yüklü olduğunda oluşabilecek basamaklı bir hata önler. Kullanarak performans trafik yönlendirme için diğer yük devretme planlarını yapılandırabilirsiniz [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region).
* **Coğrafi**. Merhaba endpoint tooserve hello coğrafi konum IP'ın döndürülen hello sorgu isteği temel alarak eşlenmiş. Bu uç kullanılamıyorsa, coğrafi konum profilde yalnızca eşlenen tooone uç nokta olabileceği için başka bir uç nokta için seçilen toofailover olmaz (daha fazla ayrıntı hello olan [SSS](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method)). En iyisi, coğrafi yönlendirme kullanırken, müşterilerin birden fazla uç noktası ile iç içe geçmiş toouse Traffic Manager profillerini hello profil hello uç noktalar olarak öneririz.

Daha fazla bilgi için bkz: [Traffic Manager trafik yönlendirme yöntemleri](traffic-manager-routing-methods.md).

> [!NOTE]
> Tüm uygun uç noktaları düşürülmüş durumuna sahip bir özel durum toonormal trafik yönlendirme davranış oluşur. "En iyi çaba" denemesi trafik Yöneticisi yapar ve *tüm hello Degraded durumu bitiş gerçekte çevrimiçi bir durumda ise gibi yanıt*. Bu davranış olabilecek tercih toohello alternatifi: toonot herhangi bir uç nokta hello DNS yanıtı döndürür. Devre dışı veya durdurulmuş uç noktaları izlenmez, bu nedenle, bunlar trafiği için uygun olarak kabul edilmez.
>
> Bu durum genellikle gibi hello hizmeti, hatalı yapılandırma tarafından kaynaklanır:
>
> * Merhaba Traffic Manager sistem durumu denetimini engelleyen bir erişim denetim listesi [ACL].
> * Bağlantı noktası veya hello trafik Yöneticisi profili protokolünde izleme hello hatalı bir yapılandırma.
>
> Merhaba Bu davranış sonucu Traffic Manager sistem durumu denetimlerinin doğru yapılandırılmamışsa, bu trafik Yöneticisi olarak ancak Yönlendirme hello trafiğinden görünür olan *olan* düzgün çalışmıyor. Ancak, bu durumda, uç nokta yük devretme genel uygulama kullanılabilirliği etkiler meydana olamaz. Hello profili Degraded durumu çevrimiçi bir durumu gösterir önemli toocheck olur. Çevrimiçi durumu bu hello trafik Yöneticisi sistem beklendiği gibi çalıştığını denetler gösterir.

Sorun giderme hakkında daha fazla bilgi için sistem durumu denetimi başarısız oldu bkz [sorun giderme düşürülmüş durumu Azure Traffic Manager üzerindeki](traffic-manager-troubleshooting-degraded.md).



## <a name="next-steps"></a>Sonraki adımlar

Bilgi [trafik Yöneticisi nasıl çalışır?](traffic-manager-how-traffic-manager-works.md)

Merhaba hakkında daha fazla bilgi [trafik yönlendirme yöntemleri](traffic-manager-routing-methods.md) Traffic Manager tarafından desteklenen

Nasıl çok öğrenin[trafik Yöneticisi profili oluştur](traffic-manager-manage-profiles.md)

[Degraded durumu sorun giderme](traffic-manager-troubleshooting-degraded.md) trafik Yöneticisi uç noktada
