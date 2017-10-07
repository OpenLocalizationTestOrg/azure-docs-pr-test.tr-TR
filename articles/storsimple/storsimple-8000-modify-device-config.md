---
title: "aaaModify hello StorSimple 8000 serisi aygıt yapılandırması | Microsoft Docs"
description: "Nasıl toouse hello StorSimple cihaz Yöneticisi hizmeti tooreconfigure zaten dağıtılmış bir StorSimple cihazı açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a>StorSimple cihaz yapılandırmanızı Hello StorSimple cihaz Yöneticisi hizmeti toomodify kullanın

## <a name="overview"></a>Genel Bakış

Azure portal hello **aygıt ayarları** hello bölümünde **ayarları** dikey bir StorSimple cihaz Yöneticisi tarafından yönetilen bir StorSimple cihazda yapılandırabilirsiniz tüm hello aygıt parametreleri içerir hizmet. Bu öğretici hello nasıl kullanabileceğinizi açıklar **ayarları** cihaz düzeyinde görevleri aşağıdaki dikey tooperform hello:

* Cihaz kolay adı değiştir
* Aygıt saat ayarlarını değiştirme
* İkincil DNS atayın
* Ağ arabirimleri değiştirme
* Değiştirme veya IP'leri yeniden atama

## <a name="modify-device-friendly-name"></a>Cihaz kolay adı değiştir

Hello Azure portal toochange hello aygıt adı kullanabilir ve tercih ettiğiniz benzersiz bir kolay ad atayabilirsiniz. Kullanım hello **genel ayarları** dikey penceresinde, aygıt toomodify hello kolay adı. Merhaba kolay ad, herhangi bir karakter içerebilir ve en fazla 64 karakter uzunluğunda olabilir.

> [!NOTE] 
> Merhaba aygıt kurulum tamamlanmadan önce yalnızca hello Azure portal hello aygıt adını değiştirebilirsiniz. Merhaba en düşük cihaz kurulumu tamamlandıktan sonra hello aygıt adı değiştirilemiyor.

![Aygıt adı genel ayarları](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

Bağlı toohello StorSimple cihaz Yöneticisi hizmeti bir StorSimple cihaz varsayılan ad atanır. Merhaba varsayılan adı genellikle hello aygıtının hello seri numarasını yansıtır. Örneğin, 15 karakter uzunluğunda 8600-SHX0991003G44HT gibi bir varsayılan cihaz adı hello şunları gösterir:

* **8600** – belirtir hello cihaz modeli.
* **SHX** – hello üretim sitesini belirtir.
* **0991003** -belirli bir ürün gösterir.
* **G44HT**- hello son 5 rakamlı olan artırılır toocreate benzersiz seri numaraları. Bu ardışık olmayabilir.

## <a name="modify-device-description"></a>Aygıt açıklaması değiştirme

Kullanım hello **genel ayarları** dikey penceresinde, aygıt toomodify hello aygıt açıklaması.

![Genel Ayarları'nda Aygıt açıklaması](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

Aygıt açıklaması genellikle hello sahibi ve hello aygıt fiziksel konumunu hello belirlemenize yardımcı olur. Hello açıklama alanı, 256'dan az karakter içermelidir.

## <a name="modify-time-settings"></a>Saat ayarlarını değiştirme

Cihazınızı sipariş tooauthenticate zamanında, bulut depolama hizmeti sağlayıcısı ile eşitlemeniz gerekir. Kullanım hello **genel ayarları** aygıt toomodify hello aygıt saat ayarlarını dikey penceresinde.

![Genel Ayarları'nda Aygıt açıklaması](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 Saat dilimini hello aşağı açılan listeden seçin. Tootwo ağ zaman Protokolü (NTP) sunucularını belirtebilirsiniz:

 - **Birincil NTP sunucusu** -hello yapılandırması gereklidir ve Cihazınızı StorSimple tooconfigure için Windows PowerShell kullanırsanız belirtilir. Merhaba varsayılan Windows Server belirtebilirsiniz **time.windows.com** NTP sunucusu olarak. Merhaba birincil NTP sunucusu yapılandırmasını hello Azure portal aracılığıyla görüntüleyebilirsiniz, ancak hello Windows PowerShell arabirimi toochange kullanmanız gerekir. Kullanım hello `Set-HcsNTPClientServerAddress` cmdlet toomodify hello birincil NTP sunucusu aygıtınızın. Daha fazla bilgi için [Set-HcsNTPClientServerAddress] (https://technet.microsoft.com/library/dn688138.aspx) cmdlet toosynxtax gidin.

- **İkincil NTP sunucusu** -hello yapılandırmadır isteğe bağlıdır. Merhaba portal tooconfigure ikincil NTP sunucusu kullanabilirsiniz.

Merhaba NTP sunucusunu yapılandırırken, ağınızı hello NTP trafiğini toopass, veri merkezi toohello Internet gelen verdiğinden emin olun. Bir ortak NTP sunucusu belirtirken, ağ güvenlik duvarları ve diğer güvenlik aygıtlarını yapılandırılmış tooallow NTP trafiğini tootravel tooand hello Ağ dışından gelen olduğundan emin olmanız gerekir. Çift yönlü NTP trafiğini izin verilmiyor (Bu işlev bir Windows etki alanı denetleyicisi sunar) bir iç NTP sunucusu kullanmanız gerekir. Cihazınızı zaman eşitleyemez, bulut depolama sağlayıcısı ile mümkün toocommunicate olmayabilir.

toosee gidin toohello ortak NTP sunucularının bir listesini [NTP sunucuları Web](http://support.ntp.org/bin/view/Servers/WebHome).

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Farklı bir saat diliminde Hello aygıt dağıtılırsa ne olur?

Merhaba aygıtı farklı bir saat diliminde dağıtılırsa hello aygıt saat dilimini değiştirir. Tüm hello yedekleme ilkeleri hello aygıt saat dilimi kullanmasını görevinden hello yedekleme ilkeleri hello yeni saat dilimine göre otomatik olarak ayarlayın. Kullanıcı müdahalesi gerekli değildir.

## <a name="modify-dns-settings"></a>DNS ayarlarını değiştirme

Bulut depolama hizmeti sağlayıcınızla toocommunicate Cihazınızı girişiminde bulunduğunda bir DNS sunucusu kullanılır. Kullanım hello **ağ ayarlarını** aygıt tooview dikey penceresinde ve yapılandırılmış hello DNS ayarlarını değiştirin. 

![Ağ Ayarları'nda DNS ayarları](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

Yüksek kullanılabilirlik için iki hello birincil gerekli tooconfigure olan ve ikincil DNS sunucuları hello ilk cihaz dağıtımı sırasında hello.

**Birincil DNS sunucusu** -hello ilk kurulum sırasında hello birincil DNS sunucusu için StorSimple toofirst belirtin hello Windows PowerShell kullanın. Merhaba birincil DNS sunucusunu yalnızca hello Windows PowerShell arabirimi üzerinden yeniden yapılandırabilirsiniz. Kullanım hello `Set-HcsDNSClientServerAddress` cmdlet toomodify hello birincil DNS sunucusu cihazınızın. Daha fazla bilgi için toosynxtax gitmek [kümesi HcsDNSClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet'i.

**İkincil DNS sunucusu** -toomodify hello ikincil DNS sunucusu, kullanım hello `Set-HcsDNSClientServerAddress` hello cihazın hello Windows PowerShell arabiriminde cmdlet'ini veya **ağ ayarlarını** hello Azure StorSimple Cihazınızı dikey Portal.

toomodify hello ikincil DNS sunucusu Azure portalında hello aşağıdaki adımları gerçekleştirin.

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin. Cihaz hello listesini seçin ve aygıtınızı tıklatın.

2. Merhaba, **ayarları** dikey penceresinde çok Git**Aygıt Ayarları > Ağ**. Merhaba açılır **ağ ayarlarını** dikey. Tıklatın **DNS ayarlarını** döşeme. Merhaba ikincil DNS sunucusu IP adresini değiştirin.

    ![İkincil DNS sunucusu IP adderss değiştirme](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. Merhaba Komut çubuğundaki **kaydetmek** tıklatıp onaylamanız istendiğinde, **Tamam**.

    ![Kaydet ve değişiklikleri onaylayın](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a>Ağ arabirimleri değiştirme

Cihazınızı dört biri 1 GbE ve ikisi de 10 GbE altı aygıt, ağ arabirimleri vardır. Bu arabirimleri 0 – veri 5 verileri olarak etiketlenir. Veri 2 ve veri 3 10 GbE ağ arabirimleri ise 0, 1 DATA, veri 4 ve verileri 5 1 GbE verilerdir.

Kullanım hello **ağ ayarlarını** dikey tooconfigure her Merhaba, kullanılan toobe arabirimleri.

![Ağ arabirimleri aracılığıyla ağ ayarlarını yapılandırma](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

tooensure yüksek kullanılabilirlik, Cihazınızda en az iki iSCSI arabirimleri ve iki bulut etkin arabirimlere sahip öneririz. Size önerilir ancak kullanılmayan arabirimleri devre dışı bırakılmasını gerektirmez.

Her ağ arabirimi için şu parametreler hello görüntülenir:

* **Hızı** – kullanıcı tarafından yapılandırılabilir bir parametre değil. Veri 2 ve veri 3 10 GbE arabirimleri ise 0, 1 DATA, veri 4 ve verileri 5 her zaman 1 GbE verilerdir.
  
  > [!NOTE]
  > Hız ve çift yönlü her zaman otomatik-belirlenir. Jumbo çerçeveler desteklenmez.
  
* **Arabirim durumu** – bir arabirim etkin veya devre dışı. Etkinleştirilirse, hello aygıt toouse hello arabirimi deneyecek. Bağlı toohello ağ ve kullanılan arabirimleri etkinleştirilmesi önerilir. Kullanmadığınız arabirimleri devre dışı bırakın.
* **Arabirim türü** – Bu parametre, bulut depolama trafiği gelen tooisolate iSCSI trafiğine izin verir. Bu parametre hello aşağıdakilerden biri olabilir:
  
  * **Bulut etkin** – etkin olduğunda, hello aygıt ile Merhaba bulut bu arabirimi toocommunicate kullanın.
  * **iSCSI etkin** – etkin olduğunda, hello aygıt hello iSCSI konak ile bu arabirimi toocommunicate kullanın.
    
    Bulut depolama trafiğinden iSCSI trafiğini yalıtmak öneririz. Ayrıca, ana bilgisayarınız hello içinde olup olmadığını unutmayın aynı alt ağda Cihazınızı tooassign bir ağ geçidi; gerekmez Ancak, Cihazınızı daha farklı bir alt ağ ana bilgisayarınız olması durumunda tooassign bir ağ geçidi gerekir.
* **IP adresi** – hello ağ arabirimlerinin yapılandırdığınızda, sanal IP (VIP) yapılandırmanız gerekir. Bu, IPv4 veya IPv6 ya da her ikisini de olabilir. Başlangıç IPv4 ve IPv6 adres ailelerinin hello cihaz ağ arabirimleri için desteklenir. IPv4 kullanırken, bir 32 bit IP adresi belirtin (*xxx.xxx.xxx.xxx*) noktalı ondalık gösterimde. IPv6 kullanırken, yalnızca 4 basamaklı önek sağlayın ve 128-bit adres bu ön ekini temel alarak, aygıt ağ arabirimi için otomatik olarak oluşturulur.
* **Alt ağ** – bu toohello alt ağ maskesi başvuruyor ve hello Windows PowerShell arabirimi yapılandırılır.
* **Ağ geçidi** – toocommunicate hello içinde olmayan düğüm ile çalıştığında bu arabirim tarafından kullanılması gereken hello varsayılan ağ geçidi budur aynı IP adresi alanını (alt ağ). Merhaba varsayılan ağ geçidi olmalıdır hello aynı (alt ağ) hello arabirimi IP adresi olarak hello alt ağ maskesi kullanılarak belirlenen adres alanı.
* **IP adresi sabit** – yalnızca hello veri 0 yapılandırması sırasında bu alan kullanılabilir arabirimi. Güncelleştirmeleri veya sorun giderme hello cihazı gibi işlemleri için tooconnect gerekebilir doğrudan toohello aygıt denetleyicisi. IP adresi sabit hello kullanılan tooaccess olabilir hello etkin ve hello pasif denetleyiciyi Cihazınızda.

> [!NOTE]
> * tooensure düzgün çalışmasını hello arabirim hızı ve çift yönlü her aygıt arabirimi bağlı hello anahtardaki doğrulayın. Anahtar arabirimleri ile ya da anlaşması gereken veya Gigabit Ethernet için yapılandırılması (1000 MB/sn) ve tam çift yönlü. İşletim yavaş hızlarda veya yarı çift yönlü arabirimleri performans sorunlarına neden olur.
> * toominimize kesintilerini ve kapalı kalma süresi, her iSCSI ağ arabiriminin Cihazınızı hello bağlantı noktalarını bağlanma hello anahtar portfast etkinleştirmenizi öneririz. Bu, ağ bağlantısı hızlı bir şekilde bir yük devretme hello olayda kurulması güvence altına alır.

### <a name="configure-data-0"></a>Veri 0 yapılandırın

Veri 0 bulut varsayılan olarak etkindir. Veri 0 yapılandırırken, ayrıca gerekli tooconfigure iki sabit IP adresleri, her denetleyici için bir tane değildir. Bu sabit IP adresleri kullanılan tooaccess hello aygıt denetleyicileri doğrudan olabilir ve hello cihazında veya hello denetleyicileri hello amacı sorun giderme için eriştiğinizde güncelleştirmeleri yüklediğinizde yararlıdır.

IP denetleyicileri hello veri 0 ayarları dikey penceresi aracılığıyla sabit hello yeniden yapılandırabilirsiniz.

![Ağ arabirimi - DATA 0 için yapılandırın](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> Sabit hello denetleyicisi için IP adresleri hello hello güncelleştirmeleri toohello aygıt bakım için kullanılır. Bu nedenle, hello sabit IP'ler yönlendirilebilir ve mümkün tooconnect toohello Internet olması gerekir.

### <a name="configure-data-1---data-5"></a>VERİLERİ 1 - 5 veri yapılandırma

VERİ için 1 - veri 5 ağ arabirimleri, hello ekran aşağıdaki gösterildiği gibi tüm hello ağ ayarlarını yapılandırabilirsiniz:

![Ağ arabirimleri veri 1 - veri 5 yapılandırın](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a>Değiştirme veya IP'leri yeniden atama

Şu anda, herhangi bir arabirim ağ hello denetleyicisi kullanımda olan bir VIP atanır (Merhaba tarafından aynı veya başka bir aygıtı hello ağındaki), hello denetleyicisi üzerinden başarısız olur. Değiştirme veya bir aygıt ağ arabirimi için VIP'ler yeniden atadığınızda, yinelenen bir IP durum oluşturabilirsiniz gibi uygun bir yordamı izlemeniz gerekir.

Aşağıdaki adımları tooswap hello gerçekleştirmek veya herhangi bir hello ağ arabirimleri için hello VIP'ler yeniden ata:

#### <a name="tooreassign-ips"></a>tooreassign IP'leri

1. Her iki arabirimde Temizle hello IP adresi.
2. Başlangıç IP adresi temizlendikten sonra toohello ilgili arabirimleri hello yeni IP adresleri atayın.

## <a name="next-steps"></a>Sonraki adımlar

* Nasıl çok öğrenin[StorSimple cihazınız için MPIO yapılandırma](storsimple-8000-configure-mpio-windows-server.md).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

