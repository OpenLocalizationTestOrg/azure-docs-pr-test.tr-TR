---
title: "aaaModify hello StorSimple cihaz yapılandırma | Microsoft Docs"
description: "Nasıl toouse hello StorSimple Yöneticisi hizmet tooreconfigure zaten dağıtılmış bir StorSimple cihazı açıklar."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: bb679264-8d46-429c-9ef7-630dc3b4a423
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: v-sharos
ms.openlocfilehash: 10a54c191260bf1baba58d28cdbfa0ed72217f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomodify-your-storsimple-device-configuration"></a>StorSimple cihaz yapılandırmanızı Hello StorSimple Yöneticisi hizmet toomodify kullanın
## <a name="overview"></a>Genel Bakış
Klasik Azure portalı hello **yapılandırma** sayfası bir StorSimple Yöneticisi hizmeti tarafından yönetilen bir StorSimple cihazda yapılandırabilirsiniz tüm hello aygıt parametrelerini içerir. Bu öğretici hello nasıl kullanabileceğinizi açıklar **yapılandırma** cihaz düzeyinde görevleri aşağıdaki sayfayı tooperform hello:

* Cihaz ayarlarını değiştirme 
* Saat ayarlarını değiştirme 
* DNS ayarlarını değiştirme 
* Ağ arabirimleri değiştirme
* Değiştirme veya IP'leri yeniden atama

## <a name="modify-device-settings"></a>Cihaz ayarlarını değiştirme
Merhaba aygıt ayarları hello kolay adını hello cihaz ve hello aygıt açıklaması içerir.

> [!NOTE] 
> Merhaba Klasik Azure portalı hello aygıt adını değiştiremezsiniz. Merhaba aygıt yeniden adlandırma desteklenmiyor.

Bağlı toohello StorSimple Yöneticisi hizmeti bir StorSimple cihaz varsayılan ad atanır. Merhaba varsayılan adı genellikle hello aygıtının hello seri numarasını yansıtır. Örneğin, 15 karakter uzunluğunda 8600-SHX0991003G44HT gibi bir varsayılan cihaz adı hello şunları gösterir:

* **8600** – belirtir hello cihaz modeli.
* **SHX** – hello üretim sitesini belirtir.
* **0991003** -belirli bir ürün gösterir.
* **G44HT**- hello son 5 rakamlı olan artırılır toocreate benzersiz seri numaraları. Bu ardışık olmayabilir.

Aygıt açıklaması belirtebilirsiniz. Aygıt açıklaması genellikle hello sahibi ve hello aygıt fiziksel konumunu hello belirlemenize yardımcı olur. Hello açıklama alanı, 256'dan az karakter içermelidir.

## <a name="modify-time-settings"></a>Saat ayarlarını değiştirme
Cihazınızı sipariş tooauthenticate zamanında, bulut depolama hizmeti sağlayıcısı ile eşitlemeniz gerekir. Saat dilimini hello aşağı açılan listeden seçin ve tootwo ağ zaman Protokolü (NTP) sunucularını belirtin. Merhaba birincil NTP sunucusu gereklidir ve Cihazınızı StorSimple tooconfigure için Windows PowerShell kullanırsanız belirtilir. Merhaba varsayılan Windows Server belirtebilirsiniz **time.windows.com** NTP sunucusu olarak. Merhaba birincil NTP sunucusu yapılandırmasını hello Klasik Azure Portalı aracılığıyla görüntüleyebilirsiniz, ancak hello Windows PowerShell arabirimi toochange kullanmanız gerekir.

Merhaba ikincil NTP sunucusu yapılandırmasını isteğe bağlıdır. Merhaba Klasik portal tooconfigure ikincil NTP sunucusu kullanabilirsiniz. 

Merhaba NTP sunucusunu yapılandırırken, ağınızı hello NTP trafiğini toopass, veri merkezi toohello Internet gelen verdiğinden emin olun. Bir ortak NTP sunucusu belirtirken, ağ güvenlik duvarları ve diğer güvenlik aygıtlarını yapılandırılmış tooallow NTP trafiğini tootravel tooand hello Ağ dışından gelen olduğundan emin olmanız gerekir. Çift yönlü NTP trafiğini izin verilmiyor (Bu işlev bir Windows etki alanı denetleyicisi sunar) bir iç NTP sunucusu kullanmanız gerekir. Cihazınızı zaman eşitleyemez, bulut depolama sağlayıcısı ile mümkün toocommunicate olmayabilir.

toosee gidin toohello ortak NTP sunucularının bir listesini [NTP sunucuları Web](http://support.ntp.org/bin/view/Servers/WebHome). 

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Farklı bir saat diliminde Hello aygıt dağıtılırsa ne olur?
Merhaba aygıtı farklı bir saat diliminde dağıtılırsa hello aygıt saat dilimini değiştirir. Tüm hello yedekleme ilkeleri hello aygıt saat dilimi kullanmasını görevinden hello yedekleme ilkeleri hello yeni saat dilimine göre otomatik olarak ayarlayın. Kullanıcı müdahalesi gerekli değildir.

## <a name="modify-dns-settings"></a>DNS ayarlarını değiştirme
Bulut depolama hizmeti sağlayıcınızla toocommunicate Cihazınızı girişiminde bulunduğunda bir DNS sunucusu kullanılır. Yüksek kullanılabilirlik için iki hello birincil gerekli tooconfigure olan ve ikincil DNS sunucuları hello ilk cihaz dağıtımı sırasında hello. tooreconfigure hello birincil DNS sunucusu, StorSimple Cihazınızda toouse hello Windows PowerShell arabirimi gerekir.

toomodify hello ikincil DNS sunucusu, hello Klasik Azure portalını kullanabilirsiniz.

## <a name="modify-network-interfaces"></a>Ağ arabirimleri değiştirme
Cihazınızı dört biri 1 GbE ve ikisi de 10 GbE altı aygıt, ağ arabirimleri vardır. Bu arabirimleri 0 – veri 5 verileri olarak etiketlenir. Veri 2 ve veri 3 10 GbE ağ arabirimleri ise 0, 1 DATA, veri 4 ve verileri 5 1 GbE verilerdir.

Yapılandırma **ağ arabirimi ayarları** her hello arabirimleri toobe kullanılır. tooensure yüksek kullanılabilirlik, Cihazınızda en az iki iSCSI arabirimleri ve iki bulut etkin arabirimlere sahip öneririz. Size önerilir ancak kullanılmayan arabirimleri devre dışı bırakılmasını gerektirmez.

Merhaba ağ arabirimlerinin yapılandırdığınızda, sanal IP (VIP) yapılandırmanız gerekir.

Veri 0 bulut varsayılan olarak etkindir. Veri 0 yapılandırırken, ayrıca gerekli tooconfigure iki sabit IP adresleri, her denetleyici için bir tane değildir. Bu sabit IP adresleri kullanılan tooaccess hello aygıt denetleyicileri doğrudan olabilir ve hello cihazında veya hello denetleyicileri hello amacı sorun giderme için eriştiğinizde güncelleştirmeleri yüklediğinizde yararlıdır.

StorSimple 8000 serisi güncelleştirme 1'de toohello hello yönlendirme ölçüm verilerinin 0 en düşük olarak ayarlanır; Bu nedenle, Cihazınızı StorSimple 8000 serisi güncelleştirme 1 çalışıyorsa, tüm hello bulut trafiği veri 0 yönlendirilir. StorSimple Cihazınızda birden fazla bulut etkin ağ arabirimi varsa, bu not edin.

> [!NOTE]
> Sabit hello denetleyicisi için IP adresleri hello hello güncelleştirmeleri toohello aygıt bakım için kullanılır. Bu nedenle, hello sabit IP'ler yönlendirilebilir ve mümkün tooconnect toohello Internet olması gerekir.
> 
> 

Her ağ arabirimi için şu parametreler hello görüntülenir:

* **Hızı** – kullanıcı tarafından yapılandırılabilir bir parametre değil. Veri 2 ve veri 3 10 GbE arabirimleri ise 0, 1 DATA, veri 4 ve verileri 5 her zaman 1 GbE verilerdir.
  
  > [!NOTE]
  > Hız ve çift yönlü her zaman otomatik-belirlenir. Jumbo çerçeveler desteklenmez.
  > 
  > 
* **Arabirim durumu** – bir arabirim etkin veya devre dışı. Etkinleştirilirse, hello aygıt toouse hello arabirimi deneyecek. Bağlı toohello ağ ve kullanılan arabirimleri etkinleştirilmesi önerilir. Kullanmadığınız arabirimleri devre dışı bırakın.
* **Arabirim türü** – Bu parametre, bulut depolama trafiği gelen tooisolate iSCSI trafiğine izin verir. Bu parametre hello aşağıdakilerden biri olabilir:
  
  * **Bulut etkin** – etkin olduğunda, hello aygıt ile Merhaba bulut bu arabirimi toocommunicate kullanın.
  * **iSCSI etkin** – etkin olduğunda, hello aygıt hello iSCSI konak ile bu arabirimi toocommunicate kullanın.
    
    Bulut depolama trafiğinden iSCSI trafiğini yalıtmak öneririz. Ayrıca, ana bilgisayarınız hello içinde olup olmadığını unutmayın aynı alt ağda Cihazınızı tooassign bir ağ geçidi; gerekmez Ancak, Cihazınızı daha farklı bir alt ağ ana bilgisayarınız olması durumunda tooassign bir ağ geçidi gerekir.
* **IP adresi** – bu IPv4 veya IPv6 veya her ikisi de olabilir. Başlangıç IPv4 ve IPv6 adres ailelerinin hello cihaz ağ arabirimleri için desteklenir. IPv4 kullanırken, bir 32 bit IP adresi belirtin (*xxx.xxx.xxx.xxx*) noktalı ondalık gösterimde. IPv6 kullanırken, yalnızca 4 basamaklı önek sağlayın ve 128-bit adres bu ön ekini temel alarak, aygıt ağ arabirimi için otomatik olarak oluşturulur.
* **Alt ağ** – bu toohello alt ağ maskesi başvuruyor ve hello Windows PowerShell arabirimi yapılandırılır.
* **Ağ geçidi** – toocommunicate hello içinde olmayan düğüm ile çalıştığında bu arabirim tarafından kullanılması gereken hello varsayılan ağ geçidi budur aynı IP adresi alanını (alt ağ). Merhaba varsayılan ağ geçidi olmalıdır hello aynı (alt ağ) hello arabirimi IP adresi olarak hello alt ağ maskesi kullanılarak belirlenen adres alanı.
* **IP adresi sabit** – yalnızca hello veri 0 yapılandırması sırasında bu alan kullanılabilir arabirimi. Güncelleştirmeleri veya sorun giderme hello cihazı gibi işlemleri için tooconnect gerekebilir doğrudan toohello aygıt denetleyicisi. IP adresi sabit hello kullanılan tooaccess olabilir hello etkin ve hello pasif denetleyiciyi Cihazınızda.

Denetleyici 0 ve denetleyici 1 hello Klasik Azure portalı yeniden yapılandırabilirsiniz.

> [!NOTE]
> * tooensure düzgün çalışmasını hello arabirim hızı ve çift yönlü her aygıt arabirimi bağlı hello anahtardaki doğrulayın. Anahtar arabirimleri ile ya da anlaşması gereken veya Gigabit Ethernet için yapılandırılması (1000 MB/sn) ve tam çift yönlü. İşletim yavaş hızlarda veya yarı çift yönlü arabirimleri performans sorunlarına neden olur.
> * toominimize kesintilerini ve kapalı kalma süresi, her iSCSI ağ arabiriminin Cihazınızı hello bağlantı noktalarını bağlanma hello anahtar portfast etkinleştirmenizi öneririz. Bu, ağ bağlantısı hızlı bir şekilde bir yük devretme hello olayda kurulması güvence altına alır.
> 
> 

## <a name="swap-or-reassign-ips"></a>Değiştirme veya IP'leri yeniden atama
Şu anda, herhangi bir arabirim ağ hello denetleyicisi kullanımda olan bir VIP atanır (Merhaba tarafından aynı veya başka bir aygıtı hello ağındaki), hello denetleyicisi üzerinden başarısız olur. Bu nedenle, hello aygıt ağ arabirimi için VIP'ler takas, yinelenen bir IP durum oluşturacağından toofollow hello uygun yordamı sahip.

Aşağıdaki adımları tooswap hello gerçekleştirmek veya herhangi bir hello ağ arabirimleri için hello VIP'ler yeniden ata:

#### <a name="tooreassign-ips"></a>tooreassign IP'leri
1. Her iki arabirimde Temizle hello IP adresi.
2. Başlangıç IP adresi temizlendikten sonra toohello ilgili arabirimleri hello yeni IP adresleri atayın.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[StorSimple cihazınız için MPIO yapılandırma](storsimple-configure-mpio-windows-server.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

