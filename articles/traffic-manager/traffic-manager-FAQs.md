---
title: "aaaAzure Traffic Manager - sık sorulan sorular | Microsoft Docs"
description: "Bu makalede yanıtlar sağlayan toofrequently trafik Yöneticisi hakkında sorular"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 5530d03b55bbf49a52002841e281e2cf5819c2b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>Trafik Yöneticisi sık sorulan sorular (SSS)

## <a name="traffic-manager-basics"></a>Trafik Yöneticisi temelleri

### <a name="what-ip-address-does-traffic-manager-use"></a>Hangi IP adresi trafik Yöneticisi kullanıyor mu?

İçinde anlatıldığı gibi [nasıl trafik Yöneticisi çalışır](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), trafik Yöneticisi DNS düzeyi hello çalışır. DNS yanıtları toodirect istemcileri toohello uygun hizmet gönderir uç noktası. İstemciler daha sonra toohello Hizmeti uç noktası doğrudan, trafik Yöneticisi ile bağlanır.

Bu nedenle, trafik Yöneticisi uç noktası veya IP adresi için istemcileri tooconnect sağlamaz. Hizmetiniz için statik IP adresi istiyorsanız, bu nedenle, hello hizmetine, değil trafik Yöneticisi'nde yapılandırılmış olması gerekir.

### <a name="does-traffic-manager-support-sticky-sessions"></a>Trafik Yöneticisi, 'Yapışkan' oturumları destekliyor mu?

İçinde anlatıldığı gibi [nasıl trafik Yöneticisi çalışır](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), trafik Yöneticisi DNS düzeyi hello çalışır. DNS yanıtları toodirect istemcileri toohello uygun hizmet uç noktası kullanır. İstemciler toohello Hizmeti uç noktası değil trafik Yöneticisi ile doğrudan bağlanır. Bu nedenle, trafik Yöneticisi hello istemci ile Merhaba sunucusu arasındaki hello HTTP trafiğini görmez.

Ayrıca, Traffic Manager tarafından alınan hello DNS sorgusu hello kaynak IP adresi toohello yinelemeli DNS hizmeti, istemci değil hello aittir. Bu nedenle, trafik Yöneticisi hiçbir şekilde tootrack tek tek istemci sahip ve 'Yapışkan' oturumları uygulayamaz. Bu sınırlama ortak tooall DNS tabanlı trafiği yönetim sistemleri ve belirli tooTraffic Yöneticisi değil.

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>Trafik Yöneticisi'ni kullanırken bir HTTP hata neden görüyorum?

İçinde anlatıldığı gibi [nasıl trafik Yöneticisi çalışır](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), trafik Yöneticisi DNS düzeyi hello çalışır. DNS yanıtları toodirect istemcileri toohello uygun hizmet uç noktası kullanır. İstemciler daha sonra toohello Hizmeti uç noktası doğrudan, trafik Yöneticisi ile bağlanır. Trafik Yöneticisi olmayan istemci ve sunucu arasındaki HTTP trafiğini bakın yapar. Bu nedenle, gördüğünüz herhangi bir HTTP hata uygulamanızdan gelen gerekir. Merhaba istemci tooconnect toohello uygulama için tüm DNS çözüm adımları tamamlandı. Trafik Yöneticisi hello uygulama trafik akışını sahip herhangi bir etkileşim dahildir.

Daha fazla araştırma, bu nedenle hello uygulaması üzerinde durmalısınız.

Merhaba istemcinin tarayıcıdan gönderilen hello HTTP ana bilgisayar üstbilgisi hello en yaygın sorunları kaynağıdır. Merhaba uygulaması kullanmakta olduğunuz hello etki alanı adı için yapılandırılmış tooaccept hello doğru ana bilgisayar üstbilgisi olduğundan emin olun. Azure Uygulama Hizmeti uç noktalarını kullanarak hello için bkz: [trafik Yöneticisi'ni kullanarak Azure App Service içinde bir web uygulaması için bir özel etki alanı adı yapılandırma](../app-service-web/web-sites-traffic-manager-custom-domain-name.md).

### <a name="what-is-hello-performance-impact-of-using-traffic-manager"></a>Trafik Yöneticisi'ni kullanarak hello performans etkisi nedir?

İçinde anlatıldığı gibi [nasıl trafik Yöneticisi çalışır](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), trafik Yöneticisi DNS düzeyi hello çalışır. İstemcileri doğrudan tooyour hizmet uç noktalarına bağlanması hello bağlantı kurulduktan sonra trafik Yöneticisi'ni kullanırken ücrete performans üzerinde etkisi yoktur.

Trafik Yöneticisi hello DNS düzeyi uygulamaları ile tümleştirilir olduğundan, DNS çözümlemesi zinciri hello eklenen ek bir DNS Arama toobe gerektirir. DNS çözümleme süresi Hello etkisini trafik Yöneticisi'nin en az olur. Trafik Yöneticisi genel bir ağ ad sunucuları ve kullanır [her noktaya yayın](https://en.wikipedia.org/wiki/Anycast) ağ tooensure DNS sorgularını her zaman yönlendirilmiş toohello yakın kullanılabilir ad sunucusu. Ayrıca, DNS yanıtların önbelleğe alma trafik Yöneticisi'ni kullanarak ücrete hello ek DNS gecikme yalnızca tooa kesir oturumlarının uygulanacağı anlamına gelir.

Merhaba performans yöntemi yollar toohello yakın kullanılabilir uç nokta trafiği. Merhaba sonucunda olduğundan bu hello bu yöntemle ilişkili genel performans etkisi en az olmalıdır. DNS gecikme süresi içinde herhangi bir artış, alt ağ gecikmesi toohello bitiş noktası tarafından uzaklık.

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>Hangi uygulama protokolleri Traffic Manager ile kullanabilir miyim?

İçinde anlatıldığı gibi [nasıl trafik Yöneticisi çalışır](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), trafik Yöneticisi DNS düzeyi hello çalışır. Merhaba DNS araması tamamlandıktan sonra istemcileri toohello uygulama uç noktası değil trafik Yöneticisi ile doğrudan bağlanır. Bu nedenle, hello bağlantı herhangi bir uygulama protokolünü kullanabilirsiniz. İzleme protokolün, trafik Yöneticisi hello gibi TCP seçerseniz uç noktası durumunu izleme yapılabilir herhangi bir uygulama protokol kullanmadan. Uygulama protokolü kullanılarak doğrulandı toohave hello durumu seçerseniz, hello endpoint toobe mümkün toorespond tooeither HTTP veya HTTPS GET istekleri gerekir.

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>Trafik Yöneticisi 'naked' etki alanı adıyla kullanabilir miyim?

Hayır. Merhaba DNS standartlarında CNAME'ler tooco izin vermiyor-hello ile diğer DNS kayıtlarını aynı mevcut adı. Merhaba tepesinde (veya kök) bir DNS bölgesinin her zaman iki önceden var olan DNS kayıtlarını içerir; Merhaba SOA ve hello yetkili NS kayıtları. Başka bir deyişle, hello DNS standartlarında ihlal etmeden hello bölge tepesinde CNAME kaydı oluşturulamıyor.

Trafik Yöneticisi DNS CNAME kaydı toomap hello gösterim DNS adı gerektirir. Örneğin, www.contoso.com toohello trafik Yöneticisi profili DNS adı olan contoso.trafficmanager.NET'e eşleştirin. Ayrıca, hangi uç noktaya hello istemcinin bağlanması gereken ikinci bir DNS CNAME tooindicate hello trafik Yöneticisi profili döndürür.

Bu soruna geçici bir çözüm toowork, trafik Yöneticisi daha sonra kullanabileceğiniz hello naked etki alanı adı tooa farklı URL, bir HTTP yeniden yönlendirme toodirect trafiğinden kullanmanızı öneririz. Örneğin, hello çıplak "contoso.com" etki alanı kullanıcıları toohello CNAME 'toohello trafik Yöneticisi DNS adı işaret www.contoso.com' yönlendirebilirsiniz.

Naked etki alanı trafik Yöneticisi'nde için tam destek bizim özellik kapsamı izlenir. Bu özellik istekleri için destek kaydedebilirsiniz [için topluluk geri bildirim sitemizde oylama](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly).

### <a name="does-traffic-manager-consider-hello-client-subnet-address-when-handling-dns-queries"></a>Trafik Yöneticisi DNS sorguları işlerken hello istemci alt ağ adresi dikkate almaz? 
Trafik Yöneticisi yalnızca hello kaynak IP adresi, genellikle hello DNS Çözümleyicisi hello IP adresini aramaları için Geographic ve performans yönlendirme yöntemleri gerçekleştirirken aldığı, hello DNS sorgusunun göz önünde bulundurur Hayır, şu anda.  
Özellikle, [RFC 7871 – istemci alt ağdaki DNS sorgularını](https://tools.ietf.org/html/rfc7871) sağlayan bir [DNS (EDNS0) için uzantı mekanizması](https://tools.ietf.org/html/rfc2671) hangi iletebilir hello istemci alt ağ adresi tooDNS sunucuları destekler çözümleyiciler olduğu şu anda trafik Yöneticisi'nde desteklenmiyor. Bu özellik isteği için destek kaydedebilirsiniz bizim [topluluk geri bildirim sitesi](https://feedback.azure.com/forums/217313-networking).


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>DNS TTL nedir ve Kullanıcılarım nasıl etkiler?

Trafik Yöneticisi bir DNS sorgusu adlandırıldığını, yaşam süresi (TTL) olarak adlandırılan hello yanıt olarak bir değer ayarlar. Saniye cinsinden, birimidir, bu değer, bu yanıt tooDNS çözümleyiciler aşağı ne kadar süreyle toocache üzerinde gösterir. DNS Çözümleyicileri toocache garanti edilmez olurken, önbelleğe alma bu sonucu bunları toorespond tooany sonraki sorgular tooTraffic Yöneticisi DNS sunucuları olmaya yerine hello önbelleği devre dışı sağlar. Bu gibi hello yanıtları etkiler:
- daha yüksek bir TTL sunulan sorgu sayısı Faturalanabilir kullanım olduğundan, bir müşteri için hello maliyetini azaltabilir trafik Yöneticisi DNS sunucuları üzerinde hello güden sorguları hello sayısını azaltır.
- daha yüksek bir TTL olası toodo DNS araması hello süresini azaltabilir.
- daha yüksek bir TTL verilerinizi trafik Yöneticisi yoklama aracılarına elde edilen hello en son sistem durumu bilgileri yansıtmaz anlamına gelir.

### <a name="how-high-or-low-can-i-set-hello-ttl-for-traffic-manager-responses"></a>Trafik Yöneticisi yanıtlar için TTL Merhaba, nasıl yüksek veya düşük ayarlayabilir miyim?

Ayarlayabileceğiniz, adresindeki bir DNS TTL toobe 0 saniye olarak düşük ve yüksek 2.147.483.647 saniye olarak profili düzeyi hello (Merhaba üst aralık uyumlu [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt )). Aşağı Akış DNS Çözümleyicileri sorgu yanıtlarını önbelleğe alma ve tüm sorgular 0 anlamına gelir TTL tooreach hello trafik Yöneticisi DNS sunucuları çözümlemesi için bekleniyor.

## <a name="traffic-manager-geographic-traffic-routing-method"></a>Trafik Yöneticisi Geographic trafik yönlendirme yöntemi

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>Coğrafi yönlendirme yararlı olduğu bazı kullanım örnekleri nelerdir? 
Coğrafi yönlendirme türü burada Azure müşteri toodistinguish coğrafi bölgelerine bağlı kullanıcılarının gereken herhangi bir senaryoda kullanılabilir. Örneğin, hello coğrafi trafik yönlendirme yöntemini kullanarak, kullanıcıların belirli bölgelerdeki diğer bölgelerdeki olandan farklı bir kullanıcı deneyimi verebilirsiniz. Başka bir örnek, belirli bir bölgede kullanıcılardan yalnızca bu bölgede uç noktaları tarafından sunulması gerektiren yerel veri egemenliği gerektirir ile uymak.

### <a name="what-are-hello-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>Coğrafi yönlendirme için trafik Yöneticisi tarafından desteklenen hello bölgeleri nelerdir? 
Trafik Yöneticisi tarafından kullanılan hello ülke/bölge hiyerarşi bulunabilir [burada](traffic-manager-geographic-regions.md). Bu sayfayı tüm değişikliklerle güncel tutulur, ancak, program aracılığıyla da alabilirsiniz hello aynı bilgileri hello kullanarak [Azure Traffic Manager REST API'si](https://docs.microsoft.com/rest/api/trafficmanager/). 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>Trafik Yöneticisi gelen bir kullanıcı burada sorgulama nasıl belirler? 
Trafik Yöneticisi (büyük olasılıkla hello hello kullanıcı adına sorgulama yaparken yerel bir DNS Çözümleyicisi budur) hello sorgusunun hello kaynak IP bakar ve bir iç IP tooregion harita toodetermine hello konumu kullanır. Bu haritada hello değişiklikleri sürekli olarak tooaccount güncelleştirilmesi Internet. 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-hello-exact-geographic-location-of-hello-user-in-every-case"></a>Trafik Yöneticisi tam coğrafi konumu hello kullanıcı her durumda hello doğru belirleyebilirsiniz sağlanır?
Hayır, trafik Yöneticisi biz Infer hello kaynak IP adresinden bir DNS sorgusunun bu hello coğrafi bölge her zaman toohello aşağıdaki son toohello kullanıcının konumuna karşılık garanti edemez nedenler: 

- İlk olarak, hello önceki SSS bölümünde açıklandığı gibi hello kullanıcı adına hello arama yaparken bir DNS Çözümleyicisi olan bkz kaynak IP adresi hello. Merhaba DNS Çözümleyicisi coğrafi konumunu Hello hello kullanıcının hello coğrafi konum için iyi bir proxy olsa da, bu da farklı hello ayak izini hello DNS çözümleyicisi hizmeti ve bir müşteri seçtiği hello belirli DNS çözümleyicisini bağlı olarak olabilir toouse. Örnek olarak, Singapur, DNS sunucusu alabilirsiniz bir DNS çözümleyicisini toohandle hello sorgu çözümleri kullanıcı/cihaz için çekildi kendi cihazın ayarları kullanımda Malezya bulunan bir müşteri belirtebilirsiniz. Durumda, trafik Yöneticisi yalnızca hello Çözümleyicisi'nin IP adresini bakın, Singapur konumu toohello karşılık gelir. Ayrıca, bu sayfada önceki SSS istemci alt ağ adresi ile ilgili destek hello bakın.

- İkinci olarak, trafik Yöneticisi bir dahili harita toodo hello IP adresi toogeographic bölge çevirisi kullanır. Bu haritada doğrulandı ve güncelleştirilmiş bir sürekli olarak tooincrease doğruluğunu ve hesap yapısını gelişen hello için Internet Merhaba, hala bizim bilgi hello coğrafi konumunu tüm tam bir temsili olmadığından hello olasılığı olan Başlangıç IP adresi.


###  <a name="does-an-endpoint-need-toobe-physically-located-in-hello-same-region-as-hello-one-it-is-configured-with-for-geographic-routing"></a>Fiziksel olarak bulunan bir uç nokta gerek toobe hello aynı bölgede bir coğrafi yönlendirme için yapılandırılır hello mu? 
Hayır, hello endpoint hello konumunu bölgeler eşlenen tooit olabilen herhangi bir kısıtlama uygular. Örneğin, ABD-Orta Azure bölgesindeki bir uç nokta yönlendirilmiş Hindistan tooit tüm kullanıcıların sahip olabilir.

### <a name="can-i-assign-geographic-regions-tooendpoints-in-a-profile-that-is-not-configured-toodo-geographic-routing"></a>Coğrafi bölgeler atamak tooendpoints değil bir profilinde yapılandırılan toodo coğrafi yönlendirme? 

Evet, profil Hello yönlendirme yöntemini coğrafi değilse hello kullanabilirsiniz [Azure Traffic Manager REST API'si](https://docs.microsoft.com/rest/api/trafficmanager/) tooassign coğrafi bölgeler tooendpoints bu profilde. Coğrafi olmayan yönlendirme türü profillerine Hello durumda bu yapılandırmayı göz ardı edilir. Bu tür bir profil toogeographic yönlendirme türü daha sonra değiştirirseniz, trafik Yöneticisi bu eşlemeleri kullanabilirsiniz.


### <a name="why-am-i-getting-an-error-when-i-try-toochange-hello-routing-method-of-an-existing-profile-toogeographic"></a>Toochange hello yönlendirme yöntemini var olan bir profili tooGeographic çalıştığımda neden bir hata alıyorum?

Tüm hello uç noktaları coğrafi yönlendirme ile bir profil altında toohave gereken en az bir bölge tooit eşlenmiş. Mevcut bir profil toogeographic yönlendirme türü tooconvert, ilk ihtiyacınız tooassociate coğrafi bölgeler tooall hello kullanarak kendi uç noktaları [Azure Traffic Manager REST API'si](https://docs.microsoft.com/rest/api/trafficmanager/) hello değiştirmeden önce toogeographic yazın yönlendirme. Portalı kullanarak ilk silerseniz hello uç noktaları, hello profil toogeographic hello yönlendirme yöntemini değiştirmek ve bunların coğrafi bölge eşleme birlikte hello uç noktaları ekleyin. 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>Neden müşteriler coğrafi yönlendirme etkinleştirilmiş bir profil altında uç noktaları yerine iç içe profil oluşturmak önerilir? 

Bir bölge tooonly bir uç nokta bir profil içinde atanabilir kendi coğrafi yönlendirme türü kullanıyor. Sağlıksız, giderek bu uç nokta Traffic Manager toosend trafiği tooit tüm trafik herhangi daha iyi olmayan gönderme hello alternatif itibaren devam ederse, bu uç alt bağlı profili tooit ile iç içe geçmiş tür değilse. Atanan hello bölge "(örneğin, bölge İspanya sahip bir uç nokta şunlar olmayan yük devretme tooanother yapılacak sağlıksız kalırsa sağlıksız oluştu toohello uç nokta atanmış bir üst" Merhaba bölgesinin olduğunda bile trafik Yöneticisi yük devretme tooanother uç nokta yok mu "hello bölge Avrupa sahip uç nokta tooit atanır). Bu, bir müşterinin trafik Yöneticisi gizliliğinize hello coğrafi sınırlar kendi profilinde Kurulum tooensure gerçekleştirilir. başarısız bir uç nokta sağlıksız gittiğinde tooanother uç nokta üzerinden tooget hello avantajı, coğrafi bölge içindeki birden çok uç nokta tekil uç noktalarını yerine toonested profiller atanmış önerilir. Yük devretme tooanother endpoint hello içinde iç içe geçmiş hello alt profili başarısız olursa, trafiği bir uç yapabiliyorsanız, bu şekilde, aynı alt profili iç içe geçmiş.

### <a name="are-there-any-restrictions-on-hello-api-version-that-supports-this-routing-type"></a>Bu yönlendirme türü destekleyen hello API sürümünü kısıtlamaları var mı?

Evet, API sürümü 2017-03-01 ve daha yeni destekler coğrafi yönlendirme türü hello yalnızca. Herhangi bir eski API sürümü kullanılan toocreated profilleri coğrafi yönlendirme türü veya coğrafi bölgeler tooendpoints atayın. Eski bir API sürümü bir Azure aboneliği kullanılan tooretrieve profillerden ise, coğrafi yönlendirme türü herhangi bir profil döndürülmez. Üstelik, eski API sürümleri kullanırken, herhangi bir profil, uç nokta bir coğrafi bölge atama ile gösterilen coğrafi bölge atamasını yok döndürdü.



## <a name="traffic-manager-endpoints"></a>Traffic Manager uç noktaları

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>Trafik Yöneticisi uç noktaları birden çok abonelik kullanabilir?

Birden çok abonelik uç noktalarını kullanarak Azure Web Apps ile mümkün değildir. Azure Web uygulamaları, Web uygulamaları ile kullanılan bir özel etki alanı adı yalnızca tek bir abonelik içinde kullanılan gerektirir. Birden çok abonelik hello ile olası toouse Web uygulamaları olmadığı aynı etki alanı adı.

Diğer uç nokta türleri için olası toouse trafik Yöneticisi uç noktalarından birden fazla aboneliğiniz olur. Kaynak Yöneticisi'nde okuma erişimi toohello endpoint Hello trafik Yöneticisi profili yapılandırma hello kişinin sahip olduğu sürece herhangi bir abonelik uç noktalarının tooTraffic Yöneticisi, eklenebilir. Bu izinler kullanılarak verilebilir [Azure Resource Manager rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md).


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>Trafik Yöneticisi bulut hizmeti 'Staging' yuvası ile kullanabilir miyim?

Evet. Bulut hizmeti 'yuvası hazırlama' trafik Yöneticisi'nde dış uç noktalar olarak yapılandırılabilir. Sistem durumu denetimlerinin hala olması ücretlendirilirsiniz hello Azure uç noktaları oranı. Merhaba dış uç nokta türü kullanımda olduğundan, değişiklikleri toohello temel alınan hizmet değil toplanma otomatik olarak. Merhaba bulut hizmeti durdurulmuş veya silindiğinde dış uç noktalar ile trafik Yöneticisi algılayamıyor. Bu nedenle, Hello uç noktası devre dışı veya kadar hello Traffic Manager sistem durumu denetimleri için fatura devam eder.

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>Trafik Yöneticisi IPv6 uç noktaları destekliyor mu?

Trafik Yöneticisi IPv6 addressible ad sunucuları şu anda sağlamaz. Ancak, trafik Yöneticisi hala tooIPv6 uç noktaları bağlanan IPv6 istemciler tarafından kullanılabilir. Bir istemci kullanmayan DNS isteklerini doğrudan tooTraffic Yöneticisi. Bunun yerine, hello istemci yinelemeli DNS hizmeti kullanır. Bir yalnızca IPv6 istemci istekleri toohello yinelemeli DNS hizmeti IPv6 üzerinden gönderir. Ardından hello özyinelemeli hizmet IPv4 kullanarak mümkün toocontact hello trafik Yöneticisi ad sunucuları olmalıdır.

Trafik Yöneticisi hello DNS adı hello bitiş noktası ile yanıt verir. toosupport IPv6 uç noktası, DNS AAAA kaydı işaret hello uç nokta DNS adı toohello IPv6 adresi olması gerekir. Trafik Yöneticisi sistem durumu denetimlerini yalnızca IPv4 adreslerini destekler. Hello hizmeti gereken hello tooexpose bir IPv4 uç noktada aynı DNS adı.

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-hello-same-region"></a>Trafik Yöneticisi hello birden fazla Web uygulaması ile kullanabilirim aynı bölgede?

Genellikle, farklı bölgelerde dağıtılan kullanılan toodirect trafiği tooapplications trafiği yöneticisidir. Ancak, bu da bir uygulama birden fazla dağıtım hello sahip olduğu kullanılabilir aynı bölgede. Merhaba trafik Yöneticisi Azure uç noktaları birden fazla Web uygulaması uç hello izin vermediği aynı Azure bölgesinde toobe eklenen toohello aynı trafik Yöneticisi profili.

##  <a name="traffic-manager-endpoint-monitoring"></a>Trafik Yöneticisi uç nokta izleme

### <a name="is-traffic-manager-resilient-tooazure-region-failures"></a>Trafik Yöneticisi dayanıklı tooAzure bölgesini hataları mı?

Trafik Yöneticisi, yüksek oranda kullanılabilir uygulamalar azure'da hello teslimini anahtar bileşenidir.
toodeliver yüksek kullanılabilirlik, trafik Yöneticisi olağanüstü yüksek düzeyde kullanılabilirlik ve esnek tooregional hatası olması gerekir.

Tasarım gereği, trafik Yöneticisi herhangi bir Azure bölgesine tam başarısızlığını dayanıklı tooa bileşenleridir. Bu esneklik tooall trafik Yöneticisi bileşenleri geçerlidir: hello DNS ad sunucuları, hello API, hello depolama katmanı ve hello uç nokta izleme hizmeti.

Merhaba olası kesinti tüm Azure bölgesinin, trafik Yöneticisi beklenen toocontinue toofunction normalde olayıdır. Birden çok Azure bölgelerinde dağıtılan uygulamalar trafik Yöneticisi toodirect trafiği tooan kullanılabilir örneğinde kendi uygulama güvenebilirsiniz.

### <a name="how-does-hello-choice-of-resource-group-location-affect-traffic-manager"></a>Kaynak grubu konumu hello seçimine trafik Yöneticisi nasıl etkiler?

Trafik Yöneticisi tek, genel bir hizmettir. Bölgesel değil. kaynak grubu konumu Hello seçimine bu kaynak grubunda dağıtılan hiçbir fark tooTraffic Yöneticisi profilleri yapar.

Azure Resource Manager, tüm kaynak grupları toospecify hello varsayılan konumu, kaynak grubunda dağıtılan kaynakların belirleyen bir konum gerektirir. Trafik Yöneticisi profili oluşturduğunuzda, bir kaynak grubu oluşturulur. Tüm trafik Yöneticisi profilleri kullanmak **genel** hello kaynak grubu varsayılan geçersiz kılma konumlarına olarak.

### <a name="how-do-i-determine-hello-current-health-of-each-endpoint"></a>Her uç noktasının geçerli durumu hello nasıl belirlerim?

Merhaba geçerli her bitiş noktası durumunu izleme, toplama toohello genel profil görüntülenir hello Azure portalı. Bu bilgiler ayrıca trafiği İzleyicisi Merhaba kullanılabilir [REST API](https://msdn.microsoft.com/library/azure/mt163667.aspx), [PowerShell cmdlet'leri](https://msdn.microsoft.com/library/mt125941.aspx), ve [platformlar arası Azure CLI](../cli-install-nodejs.md).

Azure, sistem durumu veya hello özelliği tooraise uyarılar değişiklikleri tooendpoint sistem durumu hakkında geçmiş bitiş noktası ile ilgili geçmiş bilgileri sağlamaz.

### <a name="can-i-monitor-https-endpoints"></a>HTTPS uç noktalarının izleyebilir mi?

Evet. Trafik Yöneticisi HTTPS üzerinden yoklama destekler. Yapılandırma **HTTPS** hello izleme yapılandırmasında hello protokol olarak.

Trafik Yöneticisi tüm sertifika doğrulaması sağlayamazsınız dahil olmak üzere:

* Sunucu tarafı sertifikalar doğrulanmaz
* SNI sunucu tarafı sertifikalar desteklenmez
* İstemci sertifikalarını desteklenmez.

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>Uygulamam HTTP veya HTTPS desteği yoksa bile trafik Yöneticisi kullanabilir miyim?

Evet. Protokol ve trafik Yöneticisi izleme hello bir TCP bağlantı başlatmak ve hello uç noktasından bir yanıt beklerken TCP belirtebilirsiniz. Hello uç bağlantısı olan bir yanıt tooestablish hello toohello bağlantı isteği yanıtlarsa, hello zaman aşımı süresi içinde süre sonra Bu uç işaretlenmiş sağlıklı olarak.

### <a name="what-specific-responses-are-required-from-hello-endpoint-when-using-tcp-monitoring"></a>TCP izleme kullanırken hangi belirli yanıtları hello uç noktasından gereklidir?

TCP izleme kullanıldığında bir Eşitlemeye göndererek üç yönlü TCP anlaşması sırasında tooendpoint isteği trafik Yöneticisi'ni başlatır, belirtilen bağlantı noktası hello. Ardından (Merhaba zaman aşımı ayarları'nda belirtildiği gibi) bir süre için hello uç noktasından bir yanıt için bekler. Merhaba endpoint yanıtlarsa toohello Eşitlemeye izleme ayarlarını hello belirtilen hello zaman aşımı süresi içinde Eşitlemeye ACK yanıtta isteyebilir ve sonra Bu uç sağlıklı olarak kabul edilir. Merhaba Eşitlemeye ACK yanıt alınmazsa, hello trafik Yöneticisi geri RST ile yanıt vererek hello bağlantıyı sıfırlar.

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>Trafik Yöneticisi Kullanıcılarım sağlıksız bir uç nokta çıktığınızda ne kadar hızlı hareket?

Trafik Yöneticisi toocontrol hello yük devretme Traffic Manager profilinizin davranışını şu şekilde yardımcı olabilecek birden çok ayarları sağlar:
- daha sık olarak ayarlayarak hello trafik Yöneticisi araştırmalar hello uç noktaları yoklama aralığı 10 saniyede hello belirtebilirsiniz. Bu, sağlıksız giderek herhangi bir uç nokta mümkün olan en kısa sürede algılanabilir sağlar. 
- ne kadar süreyle toowait önce bir sistem durumu onay isteği zaman aşımına uğruyor belirtebilirsiniz (en düşük zaman aşımı değeri olan 5 saniye).
- Merhaba uç noktası olarak sağlıksız olarak işaretlenmiş önce kaç tane hataları oluşabilir belirtebilirsiniz. Bu değer 0 olarak düşük olabilir, hello başarısız hemen sonra hangi servis talebi hello endpoint sağlıksız işaretlenmiş içinde ilk sistem durumunu denetleyin. Ancak, izin hello sayısı için 0 en küçük değerini hello kullanarak tooendpoints döndürme algılanıyor hello sırasında oluşabilecek tooany geçici sorunlar nedeniyle dışı kalmasına yol açabilir.
- Merhaba DNS yanıtı toobe 0 olarak kadar düşük için hello yaşam süresi (TTL) belirtin. DNS Çözümleyicileri hello yanıt önbelleğe alamıyor ve her yeni bir sorgu o hello trafik Yöneticisi hello en güncel sistem durumu bilgilerini içeren bir yanıt alır anlamına gelir. nedenle yapılıyor.

Trafik Yöneticisi, bu ayarları kullanarak bir uç nokta sağlıksız gider ve bir DNS sorgusu karşılık gelen bir profili hello karşı yaptıktan sonra altında 10 saniye yerine sağlayabilir.

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>Nasıl t farklı uç noktalar için farklı izleme ayarları profilde belirtebilir miyim?

Trafik Yöneticisi izleme ayarlardır sırasında bir profil gerçekleştiriliyordu. Yalnızca bir uç noktası için farklı bir izleme ayarı toouse gerekiyorsa, o uç noktası olarak sağlayarak yapılabilir bir [iç içe profil](traffic-manager-nested-profiles.md) izleme ayarları olan hello üst profilinden farklı.

### <a name="what-host-header-do-endpoint-health-checks-use"></a>Hangi ana bilgisayar üstbilgisi uç nokta durumu kullanım denetler?

Trafik Yöneticisi ana bilgisayar üstbilgisi HTTP ve HTTPS sistem durumu denetimlerini kullanır. Trafik Yöneticisi tarafından kullanılan hello ana bilgisayar üstbilgisi hello profilinde yapılandırılan hello uç nokta hedef hello adıdır. Merhaba ana bilgisayar üstbilgisi için kullanılan hello değer hello hedef özelliğinden ayrı olarak belirtilemez.

### <a name="what-are-hello-ip-addresses-from-which-hello-health-checks-originate"></a>İçinden kaynaklanan hello durumu denetler hello IP adresleri nelerdir?

Merhaba aşağıdaki listede kaynaklanan, Traffic Manager sistem durumu denetler hello IP adreslerini içeriyor. Bu liste tooensure kullanabilir bu IP adreslerinden gelen bağlantıları sistem durumunun hello uç noktaları toocheck izin verilir.

* 40.68.30.66
* 40.68.31.178
* 137.135.80.149
* 137.135.82.249
* 23.96.236.252
* 65.52.217.19
* 40.87.147.10
* 40.87.151.34
* 13.75.124.254
* 13.75.127.63
* 52.172.155.168
* 52.172.158.37
* 104.215.91.84
* 13.75.153.124
* 13.84.222.37
* 23.101.191.199
* 23.96.213.12
* 137.135.46.163
* 137.135.47.215
* 191.232.208.52
* 191.232.214.62
* 13.75.152.253
* 104.41.187.209
* 104.41.190.203

### <a name="how-many-health-checks-toomy-endpoint-can-i-expect-from-traffic-manager"></a>Kaç tane sistem durumu denetimleri toomy endpoint trafik Yöneticisi'nden düşüklüğü görebilir?

uç noktanız ulaşmasını hello aşağıdakilere bağlıdır Traffic Manager sistem durumu Hello sayısını denetler:
- Merhaba hello izleme aralığı için ayarlamış olduğunuz değeri (küçük aralık, uç belirli bir dönemde giriş daha fazla isteği anlamına gelir).
- Burada hello durumu denetimleri (burada bu denetimleri SSS önceki hello listelenen bekleyebilirsiniz gelen IP adresleri hello) kaynaklanan gelen konumları Hello sayısı.

## <a name="traffic-manager-nested-profiles"></a>Trafik Yöneticisi profilleri iç içe geçmiş

### <a name="how-do-i-configure-nested-profiles"></a>İç içe profil nasıl yapılandırırım?

İç içe trafik Yöneticisi profillerine hem hello Azure Resource Manager kullanılarak yapılandırılabilir ve Azure PowerShell cmdlet'leri ve platformlar arası Azure CLI komutları Klasik Azure REST API'lerini hello. Bunlar ayrıca hello yeni Azure portalı üzerinden desteklenir. Merhaba Klasik Portalı'nda desteklenmez.

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>İç içe geçmiş mu trafik Yöneticisi kaç katmanları destekliyor?

Too10 düzey derinliğinde profilleri yerleştirebilirsiniz. 'Döngü' izin verilmez.

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-hello-same-traffic-manager-profile"></a>I diğer uç nokta türleri iç içe alt profilleriyle içinde karıştırabilirsiniz hello aynı trafik Yöneticisi profili?

Evet. Bir profili içindeki farklı türden uç noktaları nasıl birleştirmek üzerinde bir kısıtlama yoktur.

### <a name="how-does-hello-billing-model-apply-for-nested-profiles"></a>Merhaba faturalama modeli için iç içe profil nasıl uygulansın mı?

İç içe geçmiş profilleri kullanarak etkisi fiyatlandırma negatif yoktur.

Trafik Yöneticisi faturalama iki bileşeni vardır: uç noktası sistem durumu denetimlerinin ve DNS sorgularını milyonlarca

* Uç nokta durumu denetimleri: bir üst profilinde bir uç nokta olarak yapılandırıldığında alt profili için herhangi bir ücret alınmaz. Hello hello uç noktaları hello alt profildeki izleme faturalandırılan sayısı her zamanki gibi.
* DNS sorguları: her sorgu yalnızca bir kez sayılır. Bir sorgu alt profilden bir uç nokta döndüren bir üst profili yalnızca hello üst profili karşı sayılır.

Tüm Ayrıntılar için bkz: hello [trafik Yöneticisi fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/traffic-manager/).

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>İç içe profil için bir performans etkisi vardır?

Hayır. İç içe profil kullanılırken ücrete performans üzerinde etkisi yoktur.

Merhaba trafik Yöneticisi ad sunucuları hello profil hiyerarşi dahili olarak her DNS sorgusu işlenirken çapraz geçiş. Bir DNS sorgusu tooa üst profili bir uç nokta ile bir DNS yanıtı alt profilinden alabilir. Tek bir CNAME kaydı, tek bir profil veya iç içe profil kullanıp kullanmadığınızı kullanılır. Merhaba hiyerarşideki her profil için bir CNAME kaydı hiç gerek toocreate yoktur.

### <a name="how-does-traffic-manager-compute-hello-health-of-a-nested-endpoint-in-a-parent-profile"></a>Trafik Yöneticisi iç içe geçmiş bir uç noktası bir üst profilinde hello durumunu nasıl işlem?

Merhaba üst profil durumu denetimleri hello alt doğrudan gerçekleştirmez. Bunun yerine, hello alt profilinin uç noktaları hello durumunu olan kullanılan toocalculate hello hello alt profilinin genel sistem durumu. Bu bilgiler, iç içe geçmiş hello profili hiyerarşi toodetermine hello sistem durumu iç içe geçmiş hello uç noktasının yayılır. Merhaba trafik yönlendirilmiş toohello alt olabilir olup olmadığını hello üst profili bu toplanan sistem durumu toodetermine kullanır.

Merhaba aşağıdaki tabloda hello davranışı iç içe geçmiş bir uç noktası için sistem durumu denetler trafik Yöneticisi açıklanmaktadır.

| Alt profili izleme durumu | Üst uç nokta İzleyicisi durumu | Notlar |
| --- | --- | --- |
| Devre dışı. Merhaba alt profili devre dışı bırakıldı. |Durduruldu |devre dışı Hello üst uç nokta durumu durdurulur. Merhaba devre dışı durumunu hello üst profilinde hello uç noktası devre dışı bırakmış belirten için ayrılmıştır. |
| Düşürülmüş. En az bir alt profil uç Degraded durumda değil. |Çevrimiçi: hello çevrimiçi uç noktaları hello alt profilinde en az sayısıdır hello MinChildEndpoints değeri.<BR>CheckingEndpoint: hello çevrimiçi artı CheckingEndpoint uç noktaları hello alt profilinde en az sayısıdır hello MinChildEndpoints değeri.<BR>Düşürülmüş: Aksi takdirde. |Trafik CheckingEndpoint durumunun yönlendirilmiş tooan uç noktadır. MinChildEndpoints çok yüksek olarak ayarlanırsa, hello uç nokta her zaman düşer. |
| Çevrimiçi. En az bir alt profil uç noktası çevrimiçi bir durumdur. Uç nokta yok hello Degraded durumu ' dir. |Yukarıya bakın. | |
| CheckingEndpoints. En az bir alt profil uç noktası 'CheckingEndpoint' dir. Hiçbir noktalarıdır 'Çevrimiçi' veya 'Düşürülmüş' |Yukarıdaki ile aynı. | |
| Etkin değil. Tüm alt profili devre dışı veya durdurulmuş noktalarıdır veya bu profil hiçbir uç noktası vardır. |Durduruldu | |

## <a name="next-steps"></a>Sonraki adımlar:
- Trafik Yöneticisi hakkında daha fazla bilgi [uç nokta izleme ve otomatik yük devretme](../traffic-manager/traffic-manager-monitoring.md).
- Trafik Yöneticisi hakkında daha fazla bilgi [trafik yönlendirme yöntemleri](../traffic-manager/traffic-manager-routing-methods.md).