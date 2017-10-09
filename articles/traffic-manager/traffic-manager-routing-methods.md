---
title: "aaaAzure Traffic Manager - trafik yönlendirme yöntemleri | Microsoft Docs"
description: "Bu trafik Yöneticisi tarafından kullanılan hello farklı trafik yönlendirme yöntemleri anlamanıza yardımcı makaleler"
services: traffic-manager
documentationcenter: 
author: KumudD
manager: timlt
editor: 
ms.assetid: db1efbf6-6762-4c7a-ac99-675d4eeb54d0
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: kumud
ms.openlocfilehash: b3eeca63ab5f2b9cd4a3a6b6a8fd3e40059e32b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-routing-methods"></a>Traffic Manager yönlendirme yöntemleri

Azure Traffic Manager destekler dört trafik yönlendirme yöntemleri toodetermine nasıl tooroute ağ trafiği toohello çeşitli hizmet uç noktaları. Trafik Yöneticisi aldığı hello trafik yönlendirme yöntemini tooeach DNS sorgusunu uygular. Merhaba DNS yanıtında hangi uç noktaya Hello trafik yönlendirme yöntemini belirler.

Trafik Yöneticisi'nde dört trafik yönlendirme yöntemleri vardır:

* **[Öncelik](#priority):** seçin **öncelik** zaman toouse birincil hizmet uç noktası için tüm trafiği isterseniz ve hello birincil veya hello yedekleme uç noktaların kullanılamaz durumda yedeklemeler sağlar.
* **[Weighted](#weighted):** seçin **Weighted** toodistribute trafiği bir uç nokta kümesi boyunca ya da eşit istediğinizde ya da tanımladığınız according tooweights.
* **[Performans](#performance):** seçin **performans** ne zaman farklı coğrafi konumlarda uç noktaları varsa ve son kullanıcıların toouse hello "en yakın" uç nokta hello en düşük ağ gecikmesini bakımından istiyorsanız.
* **[Coğrafi](#geographic):** seçin **coğrafi** kullanıcıların hangi coğrafi konum temelinde yönlendirilmiş toospecific uç noktaları (Azure, dış veya iç içe); böylece kendi DNS sorgusu kaynaklandığı. Bu, bir kullanıcının coğrafi bölge bilerek ve bunları oturum tabanlı yönlendirme önemli olduğu trafik Yöneticisi müşteriler tooenable senaryolar güçlendirir. Örnek veri egemenliği gerektirir, içerik & kullanıcı deneyiminin yerelleştirme uymaktan ve farklı bölgelerdeki trafiğini ölçme verilebilir.

Tüm trafik Yöneticisi Profil uç noktası durumu ve otomatik uç nokta yük devretme izlemeyi içerir. Daha fazla bilgi için bkz: [trafik Yöneticisi uç noktası izleme](traffic-manager-monitoring.md). Tek bir Traffic Manager profilini yalnızca bir trafik yönlendirme yöntemini kullanabilirsiniz. Profiliniz için herhangi bir zamanda farklı trafik yönlendirme yöntemini seçebilirsiniz. Bir dakika içinde değişiklikler uygulanır ve kapalı kalma süresi olmadan oluşur. Trafik yönlendirme yöntemleri, iç içe trafik Yöneticisi profilleri kullanılarak birleştirilebilir. İç içe geçme daha büyük ve karmaşık uygulamaları hello ihtiyaçlarını karşılayan karmaşık ve esnek trafik yönlendirme yapılandırmaları sağlar. Daha fazla bilgi için bkz: [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md).

## <a name = "priority"></a>Öncelik trafik yönlendirme yöntemi

Genellikle bir kuruluşun kendi birincil hizmet arıza durumunda bir veya daha fazla yedekleme hizmetleri dağıtarak hizmetlerinin tooprovide güvenilirliği istemektedir. Merhaba 'Priority' trafik yönlendirme yöntemini sağlayan Azure müşterilerin tooeasily Bu yük devretme desen uygulamak.

![Azure trafik Yöneticisi 'Priority' trafik yönlendirme yöntemi][1]

Merhaba trafik Yöneticisi profili hizmet uç noktaları öncelikli listesi içerir. Varsayılan olarak, tüm trafik toohello birincil (en yüksek öncelik) uç trafik Yöneticisi gönderir. Merhaba birincil uç noktası kullanılabilir durumda değilse, trafik Yöneticisi yollar trafiği toohello ikinci uç nokta hello. Her iki hello birincil ve ikincil uç noktaları mevcut değilse hello trafiği toohello gider üçüncü, vb.. (Etkin veya devre dışı) yapılandırılmış hello durumuna göre hello uç noktasının kullanılabilirliğini ve devam eden uç nokta izleme hello.

### <a name="configuring-endpoints"></a>Uç noktalarını yapılandırma

Azure Resource Manager ile Merhaba 'priority' özelliği için her bir uç nokta kullanılarak açıkça hello uç nokta önceliği yapılandırın. Bu özellik, 1 ile 1000 arasında bir değerdir. Daha düşük değerler daha yüksek önceliği temsil eder. Uç noktaları öncelik değerleri paylaşamaz. Merhaba özelliğinin ayarlanması isteğe bağlıdır. Atlanmış hello uç nokta sırasına göre varsayılan öncelik kullanılır.

##<a name = "weighted"></a>Ağırlıklı trafik yönlendirme yöntemi
Merhaba 'Weighted' trafik yönlendirme yöntemini verir toodistribute trafiği eşit veya toouse önceden tanımlanmış ağırlığı.

![Azure trafik Yöneticisi 'Ağırlıklı' trafik yönlendirme yöntemi][2]

Merhaba ağırlıklı trafik yönlendirme yöntemini, bir ağırlık tooeach uç noktası hello trafik Yöneticisi profili yapılandırması atayın. Merhaba ağırlığı 1 too1000 arasında bir tamsayıdır. Bu parametre isteğe bağlıdır. Belirtilmezse, trafiği yöneticileri varsayılan ağırlık '1' olarak kullanır.

Alınan her DNS sorgusu için trafik Yöneticisi kullanılabilir uç nokta rastgele seçer. bir uç noktasını hello olasılığını tooall kullanılabilir uç noktaları atanan hello ağırlıklarını temel alır. Hello kullanarak aynı bir bile trafik dağılımı tüm uç noktaları sonuçlarında arasında ağırlık. Daha yüksek veya düşük ağırlıkları üzerinde belirli uç noktalarını kullanarak fazla veya az sık hello DNS yanıtları döndürülen bu uç noktaları toobe neden olur.

Ağırlıklı hello yöntemi bazı yararlı senaryolarına olanak sağlar:

* Aşamalı uygulama yükseltme: trafiği tooroute tooa yeni uç nokta yüzdesi ayırmak ve hello trafiği saati too100% aşamalı olarak artırmak.
* Uygulama geçiş tooAzure: hem Azure hem de dış uç noktalar ile bir profili oluşturun. Merhaba ağırlık hello uç noktaları tooprefer hello yeni uç nokta olarak ayarlayın.
* Ek kapasite için bulut emniyeti: bir Traffic Manager profilini koyarak bir şirket içi dağıtım hello buluta hızlı bir şekilde genişletin. Merhaba bulut ek kapasite gerektiğinde, ekleyin veya daha fazla uç noktaları etkinleştirin ve hangi trafik bölümünü tooeach endpoint gider belirtin.

Merhaba Resource Manager Azure portal ağırlıklı trafik yönlendirme hello yapılandırmasını destekler.  Azure PowerShell'i, CLI ve hello REST API sürümleri hello Resource Manager kullanarak ağırlıkları yapılandırabilirsiniz.

DNS yanıtları istemciler tarafından önbelleğe alınır ve istemcilerin hello hello yinelemeli DNS sunucuları tarafından tooresolve DNS adlarını kullanın önemli toounderstand olur. Bu önbelleğe alma ağırlıklı trafiği dağıtımları üzerinde bir etkisi olabilir. Merhaba sayıda istemci ve yinelemeli DNS sunucuları büyük olduğunda trafik dağılımı beklendiği gibi çalışır. İstemcileri veya yinelemeli DNS sunucuları Hello sayısı az olduğunda ancak, önbelleğe alma önemli ölçüde hello trafik dağılımı eğme.

Ortak kullanım durumları şunlardır:

* Geliştirme ve test ortamları
* Uygulama uygulama iletişimleri
* Uygulamalar bir dar kullanıcı ortak bir yinelemeli DNS altyapısı (örneğin, bir proxy üzerinden bağlanma şirket çalışanlarının) paylaşan temel yönelik

Bu DNS önbelleğe alma etkileri ortak tooall DNS tabanlı trafik yönlendirme, yalnızca Azure Traffic Manager sistemleridir. Bazı durumlarda, açıkça hello DNS önbelleği temizleme geçici bir çözüm sağlayabilir. Diğer durumlarda, alternatif bir trafik yönlendirme yöntemi daha uygun olabilir.

## <a name = "performance"></a>Performans trafik yönlendirme yöntemi

İki veya daha fazla konumlarda uç noktaları Merhaba Dünya çapında dağıtma hello uygulamalarının yanıtlama hızını birçok 'en yakın' tooyou olan Yönlendirme trafiği toohello konuma göre artırabilir. Merhaba 'Performans' trafik yönlendirme yöntemini bu yeteneği sağlar.

![Azure trafik Yöneticisi 'Performans' trafik yönlendirme yöntemi][3]

Merhaba 'en yakın' bitiş noktası tarafından coğrafi uzaklığı ölçülen mutlaka yakın değil. Bunun yerine, ağ gecikmesi ölçerek hello en yakın endpoint hello 'Performans' trafik yönlendirme yöntemini belirler. Trafik Yöneticisi Internet gecikme tablosu bir tootrack hello gidiş dönüş süresi IP adresi aralıkları ve her Azure veri merkezi arasında tutar.

Trafik Yöneticisi hello gelen DNS istekte hello Internet gecikme tablosu hello kaynak IP adresi arar. Trafik Yöneticisi kullanılabilir uç nokta hello hello IP adres aralığı için en düşük gecikme süresine sahiptir ve ardından bu uç hello DNS yanıtı döndürür Azure veri merkezi içinde seçer.

İçinde anlatıldığı gibi [nasıl trafik Yöneticisi çalışır](traffic-manager-overview.md#how-traffic-manager-works), trafik Yöneticisi DNS sorgularını doğrudan istemcilerden almaz. Bunun yerine, DNS sorgularını hello istemcileri yapılandırılmış toouse olduğunu hello yinelemeli DNS hizmetinden gelen. Bu nedenle, hello IP adresi kullanılan toodetermine hello 'en yakın' uç noktası hello istemcinin IP adresi değil ancak hello yinelemeli DNS hizmeti başlangıç IP adresi olacak. Uygulamada, hello istemci için iyi bir proxy bu IP adresidir.


Trafik güncelleştirmeleri Internet gecikme tablosu tooaccount değişiklikleri hello Yöneticisi düzenli olarak genel Internet ve yeni Azure bölgeleri hello. Ancak, uygulama performansı göre yük gerçek zamanlı Çeşitlemeler Internet hello arasında değişir. Performans trafik yönlendirme verilen hizmet uç noktası üzerindeki yük izlemez. Bir uç nokta kullanılamaz duruma gelirse, ancak, trafik Yöneticisi, DNS sorgu yanıtlarında içermeyecek.


Noktaları toonote:

* Profilinizi içinde birden fazla uç noktası içeriyorsa, Traffic Manager trafik hello bu bölgede kullanılabilir uç noktaları arasında dağıtır sonra aynı Azure bölgesinde hello. Bir bölge içinde farklı trafik dağılımı tercih ederseniz, kullanabileceğiniz [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md).
* Tüm hello en yakın uç noktalarını etkin olduğunda Azure bölgesi düzeyi düşürülmüş, Traffic Manager trafik toohello uç noktaları hello sonraki en yakın Azure bölgesinde taşır. Toodefine tercih edilen yük devretme sırası istiyorsanız kullanın [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md).
* Merhaba performans trafik yönlendirme yöntemini dış uç noktalar veya iç içe geçmiş uç noktaları ile kullanırken bu uç toospecify hello konumunu gerekir. Hello Azure bölgesi en yakın tooyour dağıtımı seçin. Konumların hello Internet gecikme tablosu tarafından desteklenen hello değerlerdir.
* Merhaba uç noktası seçtiği hello belirleyici algoritmasıdır. DNS sorgularından aynı istemci hello yönlendirilmiş toohello yinelenen aynı uç noktası. Genellikle, istemcilerin seyahat halindeyken farklı yinelemeli DNS sunucusu kullanın. Merhaba istemci yönlendirilmiş tooa farklı uç noktası olabilir. Yönlendirme güncelleştirmeleri toohello Internet gecikme tablosu tarafından etkilenebilir. Bu nedenle, hello trafik yönlendirme yöntemini garanti etmez bir istemci her zaman olduğunu performans toohello yönlendirilen aynı uç noktası.
* Merhaba Internet gecikme tablosu değiştiğinde bazı istemciler yönlendirilmiş tooa farklı uç noktası olduğunu fark edebilirsiniz. Bu yönlendirme değişiklik geçerli gecikme verilere göre daha doğru olur. Bu temel toomaintain hello doğruluğunu performans trafik yönlendirme Internet sürekli dönüşmesi hello olarak güncelleştirmelerdir.

## <a name = "geographic"></a>Coğrafi trafik yönlendirme yöntemi

Trafik Yöneticisi profilleri, böylece kullanıcılar toospecific uç noktaları (Azure, dış veya iç içe) hangi coğrafi konum kendi DNS sorgusu temelinde yönlendirilir yönlendirme yöntemini Geographic kaynaklandığı yapılandırılmış toouse hello olabilir. Bu, bir kullanıcının coğrafi bölge bilerek ve bunları oturum tabanlı yönlendirme önemli olduğu trafik Yöneticisi müşteriler tooenable senaryolar güçlendirir. Örnek veri egemenliği gerektirir, içerik & kullanıcı deneyiminin yerelleştirme uymaktan ve farklı bölgelerdeki trafiğini ölçme verilebilir.
Bir profili coğrafi yönlendirme için yapılandırıldığında, her bitiş profili toohave atanan coğrafi bölgeler tooit kümesi gerektiğini ilişkili. Coğrafi bir bölgenin ayrıntı düzeyi aşağıdaki düzeylerde olabilir 
- Dünya – herhangi bir bölgeyi
- Bölgesel gruplandırma – Örneğin, Afrika, Orta Doğu, Avustralya/Pasifik vs. 
- Ülke/bölge – Örneğin, İrlanda, Peru, Hong Kong ÖİB vs. 
- Bölge – Örneğin, ABD California, Avustralya-Queensland, Kanada Alberta vb. (Not: Bu ayrıntı düzeyi yalnızca durumları için desteklenen / il Avustralya, Kanada, İngiltere ve ABD).

Bir bölge veya bölge kümesi tooan uç noktası atandığında, bu bölgeler gelen tüm isteklerin yönlendirilmiş yalnızca toothat uç noktası alır. Trafik Yöneticisi gelen bir kullanıcı sorgulama – genellikle bu hello IP hello sorgu hello kullanıcı adına yapılması hello yerel DNS Çözümleyicisi adresidir hello DNS sorgu toodetermine hello bölge hello kaynak IP adresini kullanır.  

![Azure trafik Yöneticisi 'Coğrafi' trafik yönlendirme yöntemi](./media/traffic-manager-routing-methods/geographic.png)

Trafik Yöneticisi hello DNS sorgusu hello kaynak IP adresi bilgilerini okur ve veritabanından kaynaklanan hangi coğrafi bölge karar verir. Bu eşlenen coğrafi bölge tooit sahip bir uç nokta ise ardından toosee arar. Bu arama hello düşük ayrıntı düzeyinde (burada, desteklenir, aksi takdirde hello ülke/bölge düzeyinde bölge) başlar ve tüm hello yolu olan toohello yüksek düzey girer **World**. Bu geçişi kullanarak hello uç nokta tooreturn hello sorgu yanıt olarak tasarlanmış Hello ilk eşleşme bulunamadı. Bir uç nokta, alt profilindeki bir iç içe türü uç noktasıyla eşleşen döndürüldüğünde, kendi yönlendirme yöntemini esas alarak. Başlangıç noktaları aşağıdaki geçerli toothis davranışı şunlardır:

- Merhaba yönlendirme türü coğrafi yönlendirme olduğunda coğrafi bir bölgenin bir Traffic Manager profilini yalnızca eşlenen tooone uç olabilir. Bu kullanıcıları yönlendirme belirleyici ve müşteriler anlaşılır coğrafi sınırları gerektiren senaryolar etkinleştirebilirsiniz sağlar.
- Bir kullanıcının bölge altında iki farklı uç noktalar coğrafi eşleme geliyorsa, trafik Yöneticisi hello en düşük ayrıntı hello uç noktası seçer ve bu bölge toohello yönlendirme isteklerinden diğer uç nokta dikkate almaz. Örneğin, coğrafi yönlendirme türü profili iki uç noktaları - bitiş noktası 1 ve Endpoint2 göz önünde bulundurun. Bitiş noktası 1 yapılandırılmış İrlanda ve Endpoint2 tooreceive trafiği yapılandırılmış Avrupa tooreceive trafiği. İrlanda'dan bir isteğin kaynaklandığı, her zaman yönlendirilmiş tooEndpoint1 olur.
- Bir bölge eşlenen yalnızca tooone uç nokta olabileceği için trafik Yöneticisi bunu hello endpoint sağlıklı olup olmamasına bakılmaksızın döndürür.

    >[!IMPORTANT]
    >Merhaba coğrafi yönlendirme yöntemini kullanan müşteriler, her içinde en az iki uç nokta içeren alt profilleri sahip hello iç içe türü uç noktaları ilişkilendirme önerilir.
- Bir uç nokta eşleşme bulundu ve bu uç hello olup olmadığını **durduruldu** durumunda, trafik Yöneticisi NODATA yanıt verir. Bu durumda, başka bir arama yapılır yukarıya hello coğrafi bölge hiyerarşisinde. Bu davranış da Hello alt profili hello olduğunda iç içe geçmiş uç nokta türleri için geçerli olur. **durduruldu** veya **devre dışı** durumu.
- Bir uç nokta görüntülerse bir **devre dışı** durumu, işlem eşleştirme hello bölgede eklenmeyecek. Bu davranış da Hello endpoint hello olduğunda iç içe geçmiş uç nokta türleri için geçerli olur. **devre dışı** durumu.
- Bir sorgu, bu profilde eşleme olan coğrafi bölgedeki geliyorsa, trafik Yöneticisi NODATA yanıtı döndürür. Bu nedenle, müşterilerin ideal türünde, iç içe hello bölgesiyle hello alt profilinde en az iki uç nokta bir uç nokta ile coğrafi yönlendirme kullandığı önerilir **World** tooit atanmış. Bu, aynı zamanda tooa bölge eşlemediğinden herhangi bir IP adresi işlenmesini sağlar.

İçinde anlatıldığı gibi [nasıl trafik Yöneticisi çalışır](traffic-manager-how-traffic-manager-works.md), trafik Yöneticisi DNS sorgularını doğrudan istemcilerden almaz. Bunun yerine, DNS sorgularını hello istemcileri yapılandırılmış toouse olduğunu hello yinelemeli DNS hizmetinden gelen. Bu nedenle, başlangıç IP adresi kullanılan toodetermine hello bölge istemcinin IP adresi Merhaba, ancak bunu hello yinelemeli DNS hizmeti başlangıç IP adresi değil. Uygulamada, hello istemci için iyi bir proxy bu IP adresidir.


## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl kullanarak toodevelop yüksek kullanılabilirlik uygulamaları [trafik Yöneticisi uç nokta izleme](traffic-manager-monitoring.md)

Nasıl çok öğrenin[trafik Yöneticisi profili oluştur](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-routing-methods/priority.png
[2]: ./media/traffic-manager-routing-methods/weighted.png
[3]: ./media/traffic-manager-routing-methods/performance.png



