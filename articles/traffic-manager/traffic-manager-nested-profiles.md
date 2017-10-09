---
title: "Trafik Yöneticisi profillerine aaaNested | Microsoft Docs"
description: "Bu makalede, hello 'İç içe geçmiş profiller' Özelliği Azure trafik Yöneticisi'nin açıklanmaktadır."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a>İç içe trafik Yöneticisi profilleri

Trafik Yöneticisi bir dizi trafik Yöneticisi nasıl seçtiği toocontrol hangi uç noktaya trafiği her son kullanıcıdan alması gereken izin trafik yönlendirme yöntemleri içerir. Daha fazla bilgi için bkz: [Traffic Manager trafik yönlendirme yöntemleri](traffic-manager-routing-methods.md).

Her trafik Yöneticisi profili, tek bir trafik yönlendirme yöntemini belirtir. Ancak, tek bir trafik Yöneticisi profili tarafından sağlanan hello yönlendirme çok daha karmaşık trafik yönlendirme gerektiren senaryolar vardır. Trafik Yöneticisi profilleri toocombine hello birden fazla trafik yönlendirme yöntemini yararları yerleştirebilirsiniz. İç içe profil toooverride hello varsayılan trafik Yöneticisi davranışı toosupport daha büyük ve daha karmaşık uygulama dağıtımları izin verir.

Örnek hello nasıl Traffic Manager profillerini çeşitli senaryolarda toouse iç içe geçmiş gösterilmektedir.

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a>Örnek 1: Birleştirme 'Performans' ve 'Weighted' trafik yönlendirme

Azure bölgeleri aşağıdaki hello uygulamada dağıtılan varsayalım: Batı ABD, Batı Avrupa ve Doğu Asya. Trafik Yöneticisi'nin 'Performans' trafik yönlendirme yöntemini toodistribute trafiği toohello bölge en yakın toohello kullanıcı kullanın.

![Tek trafik Yöneticisi profili][4]

Şimdi, bunu daha yaygın olarak çalışırken önce bir güncelleştirme tooyour hizmeti istediğiniz tootest varsayalım. Toouse hello 'ağırlıklı' trafik yönlendirme yöntemini toodirect trafiği tooyour sınama dağıtımı, küçük bir yüzdesi istiyor. Merhaba sınama dağıtımı hello var olan üretim dağıtımına yanında Batı Avrupa'da ayarlarsınız.

Hem 'Weighted' birleştiremez ve ' performans trafik yönlendirme tek bir profilde. toosupport bu senaryo, hello iki Batı Avrupa uç noktaları ve hello 'Weighted' trafik yönlendirme yöntemini kullanarak bir trafik Yöneticisi profili oluşturun. Ardından, bu 'alt' profili bir uç nokta toohello 'parent' profili olarak ekleyin. hala kullanır performans trafik yönlendirme yöntemini hello ve içerir hello üst profil uç noktalar olarak genel diğer dağıtımlar hello.

Aşağıdaki diyagramda hello Bu örnek gösterilmektedir:

![İç içe trafik Yöneticisi profilleri][2]

Bu yapılandırmada, hello üst profili yönlendirilen trafiği trafiği bölgeler arasında normal olarak dağıtır. Batı Avrupa içinde hello iç içe profil atanan toohello ağırlıklara göre trafiği toohello üretim ve test uç noktaları dağıtır.

Merhaba üst profili hello 'Performans' trafik yönlendirme yöntemini kullandığında, her bitiş konumu atanması gerekir. Merhaba endpoint yapılandırdığınızda hello konumu atanır. Hello Azure bölgesi en yakın tooyour dağıtımı seçin. Hello Azure bölgeleri hello Internet gecikme tablosu tarafından desteklenen hello konumu değerlerdir. Daha fazla bilgi için bkz: ['Performans' Traffic Manager trafik yönlendirme yöntemini](traffic-manager-routing-methods.md#performance).

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a>Örnek 2: İç içe geçmiş profillerinde uç nokta izleme

Trafik Yöneticisi etkin olarak her hizmet uç noktası hello durumunu izler. Bir uç nokta sağlıksız durumda, trafik Yöneticisi kullanıcıları tooalternative uç noktaları toopreserve hello kullanılabilirlik hizmetinizin yönlendirir. Bu uç nokta izleme ve yük devretme davranış tooall trafik yönlendirme yöntemleri geçerlidir. Daha fazla bilgi için bkz: [trafik Yöneticisi uç noktası izleme](traffic-manager-monitoring.md). Uç nokta izleme iç içe profil için farklı şekilde çalışır. İç içe geçmiş profilleriyle hello üst profil durumu denetimleri hello alt doğrudan gerçekleştirmez. Bunun yerine, kullanılan toocalculate hello alt profilinin uç noktaları hello durumunu olduğu hello hello alt profilinin genel sistem durumu. Bu sistem durumu bilgileri, iç içe geçmiş hello profil hiyerarşisini yayılır. Merhaba üst profili bu toplanan sistem durumu toodetermine kullanıp kullanmadığını toodirect trafik toohello alt profili. Merhaba bkz [SSS](traffic-manager-FAQs.md#traffic-manager-nested-profiles) iç içe profil sistem durumu izleme hakkında ayrıntılar için.

Toohello önceki örnek döndüren, Batı Avrupa hello üretim dağıtımında başarısız varsayalım. Varsayılan olarak, tüm trafik toohello sınama dağıtımı hello 'alt' profili yönlendirir. Merhaba sınama dağıtımı de başarısız olursa, tüm alt uç noktaları sağlıksız olduğundan hello alt profilinin trafik alması gerektiğini değil hello üst profil belirler. Ardından, hello üst profili trafiği toohello başka bölgelerde dağıtır.

![İç içe profil yük devretme (varsayılan davranış)][3]

Bu düzenleme ile mutluluk olabilir. Veya tüm trafiği Batı Avrupa için şimdi toohello sınama dağıtımı sınırlı alt trafik yerine geçiyor ilgili olabilir. Merhaba Hello durumunu bağımsız olarak dağıtımı test etme, Batı Avrupa'da hello Üretim dağıtımı başarısız olduğunda toofail toohello diğer bölgelerdeki istiyor. tooenable Bu yük devretme hello 'MinChildEndpoints' parametresi hello alt profili hello üst profilindeki bir uç nokta olarak yapılandırırken belirtebilirsiniz. Merhaba parametre hello minimum hello alt profildeki kullanılabilir uç noktaları sayısını belirler. Merhaba varsayılan değer, '1' dir. Bu senaryo için hello MinChildEndpoints değeri too2 ayarlayın. Bu eşiğin altına hello üst profili hello tüm alt profili toobe kullanılamaz olarak değerlendirir ve diğer uç noktaları trafiği toohello yönlendirir.

Merhaba aşağıdaki şekilde bu yapılandırma gösterilmektedir:

!['MinChildEndpoints' ile profil yük devretme iç içe geçmiş = 2][4]

> [!NOTE]
> Merhaba 'Priority' trafik yönlendirme yöntemini tüm trafiği tooa tek uç dağıtır. Bu nedenle bulunmaktadır az amacı '1' dışında bir MinChildEndpoints ayarı için bir alt profili.

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a>Örnek 3: trafiği 'Performans' akışındaki öncelikli yük devretme bölgeleri

Merhaba varsayılan hello 'Performans' trafik yönlendirme yöntemi için aşırı, sonraki yüklenirken en yakın bitiş hello ve basamaklı bir dizi hata neden tasarlanmış tooavoid davranıştır. Bir uç nokta başarısız olduğunda, toothat endpoint eşit yönlendirilir tüm trafiği toohello diğer uç noktalar tüm bölgeler arasında dağıtılmış.

!['Performans' trafiği ile varsayılan yük devretme yönlendirme][5]

Ancak, BİZE hello Batı Avrupa trafik yük devretme tooWest tercih ve yalnızca her iki uç noktaları kullanılamadığında trafiği tooother bölgeleri doğrudan varsayalım. Bir alt profili ile Merhaba 'Priority' trafik yönlendirme yöntemini kullanarak bu çözüm oluşturabilirsiniz.

!['Performans' trafiğine tercihe bağlı yük devretme kümelemesiyle yönlendirme][6]

Hello Batı Avrupa endpoint hello Batı ABD endpoint daha yüksek önceliğe sahip olduğundan, her iki uç noktaları çevrimiçi olduğunda tüm trafiği toohello Batı Avrupa endpoint gönderilir. Batı Avrupa başarısız olursa, yönlendirilmiş tooWest ABD trafiğidir. Batı Avrupa ve Batı ABD yalnızca başarısız olduğunda iç içe geçmiş hello profiliyle yönlendirilmiş tooEast Asya trafiğidir.

Tüm bölgeler için bu deseni yineleyebilirsiniz. Merhaba üst profilindeki tüm üç uç noktaları her bir öncelikli yük devretme sırası sağlayan üç alt profilleriyle değiştirin.

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a>Örnek 4: hello içinde birden çok uç noktalar arasında aynı yönlendirme 'Performans' trafiğini denetleme bölge

Merhaba 'birden fazla uç belirli bir bölgede bulunan bir profilde trafik yönlendirme yöntemini kullanılan performans' varsayalım. Varsayılan olarak, trafiği toothat bölge bu bölgedeki tüm kullanılabilir uç noktaları arasında eşit olarak dağıtılır yönlendirilmiş.

!['Performans' Yönlendirme bölge trafik dağılımı (varsayılan davranış) trafiği][7]

Birden çok uç nokta Batı Avrupa'da eklemek yerine, bu uç ayrı alt profilinde iliştirilir. Merhaba alt profili toohello üst hello Batı Avrupa'da yalnızca uç noktası olarak eklenir. Merhaba alt profilinde Hello ayarlarını, o bölge içinde öncelik tabanlı veya ağırlıklı trafik yönlendirme etkinleştirerek Batı Avrupa ile Merhaba trafik dağılımı kontrol edebilirsiniz.

!['Performans' trafiği özel bölge trafik dağılımı ile yönlendirme][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a>Örnek 5: Her uç nokta izleme ayarları

Kullanmakta olduğunuz varsayalım trafik Yöneticisi toosmoothly geçiş trafiği Azure üzerinde barındırılan bir eski şirket içi web sitesi tooa yeni bulut tabanlı sürümü. Merhaba eski site için toouse hello giriş sayfası URI toomonitor site durumu istiyor. Ancak hello yeni bulut tabanlı sürümü için özel bir izleme sayfası uyguluyorsanız (yol ' / monitor.aspx'), ek denetimleri içerir.

![Trafik Yöneticisi uç noktası (varsayılan davranış) izleme][9]

Trafik Yöneticisi profili İzleme ayarlarında Hello tooall uç noktaları tek bir profili içinde geçerlidir. İç içe geçmiş profilleriyle site toodefine izleme ayarlarını farklı her farklı alt profili kullanın.

![Trafik Yöneticisi uç noktası uç nokta başına ayarlarla izleme][10]

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [trafik Yöneticisi profilleri](traffic-manager-overview.md)

Nasıl çok öğrenin[trafik Yöneticisi profili oluştur](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png
