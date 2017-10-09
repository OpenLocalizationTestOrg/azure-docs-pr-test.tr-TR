---
title: "Active Directory çoğaltma durumunu Azure günlük analizi ile aaaMonitor | Microsoft Docs"
description: "Merhaba Active Directory çoğaltma durumunu çözüm paketi düzenli olarak çoğaltma hatalar için Active Directory ortamınızı izler ve OMS Panonuzda hello sonuçları raporlar."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>Günlük analizi ile Active Directory çoğaltma durumunu izleme

![AD çoğaltma durumu simgesi](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

Active Directory kuruluş BT ortamında anahtar bir bileşenidir. tooensure yüksek kullanılabilirlik ve yüksek performans, her etki alanı denetleyicisi hello Active Directory veritabanının kopyasını sahiptir. Etki alanı denetleyicileri birbirleri ile Merhaba kuruluş genelinde sipariş toopropagate değişiklikler çoğaltılır. Bu çoğaltma işlemi hatalarına çeşitli sorunlar hello kuruluş genelinde neden olabilir.

Merhaba AD çoğaltma durumunu çözüm paketi düzenli olarak çoğaltma hatalar için Active Directory ortamınızı izler ve OMS Panonuzda hello sonuçları raporlar.

## <a name="installing-and-configuring-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.

* Merhaba etki alanı toobe hesaplanan üyeleri olan etki alanı denetleyicilerinde aracıları yüklemeniz gerekir. Veya üye sunuculara aracıları yükleyene ve hello aracıları toosend AD çoğaltma verileri tooOMS yapılandırmanız gerekir. Windows bilgisayarları tooOMS tooconnect nasıl görürüm toounderstand [bağlanmak Windows bilgisayarları tooLog Analytics](log-analytics-windows-agents.md). Etki alanı denetleyicinizi zaten tooconnect tooOMS istediğiniz mevcut bir System Center Operations Manager ortamının bir parçası olup olmadığını [Operations Manager bağlanmak tooLog Analytics](log-analytics-om-agents.md).
* Merhaba işlemi kullanarak OMS çalışma açıklanan hello Active Directory çoğaltma durumunu çözüm tooyour eklemek [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).  Başka bir yapılandırma işlemi gerekmez.

## <a name="ad-replication-status-data-collection-details"></a>AD çoğaltma durumu verileri toplama ayrıntıları
Merhaba aşağıdaki tabloda veri toplama yöntemleri ve veri AD çoğaltma durumunun nasıl toplandığını ilgili diğer ayrıntıları gösterir.

| Platform | Doğrudan Aracısı | SCOM Aracısı | Azure Storage | SCOM gerekli? | Yönetim grubu gönderilen SCOM Aracısı verileri | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |beş günde |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a>İsteğe bağlı olarak, bir etki alanı dışı denetleyicisi toosend AD veri tooOMS etkinleştir
TooOMS, diğer bir OMS bağlı bilgisayar hello AD çoğaltma durumunu çözüm için veri paketi ve sahip hello veri gönderme, etki alanı toocollect içinde kullanabilir doğrudan tooconnect herhangi bir etki alanı denetleyicileriniz istemiyorsanız.

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a>tooenable olmayan etki alanı denetleyicisi toosend AD veri tooOMS
1. Bu hello bilgisayar hello AD çoğaltma durumunu çözümünü kullanarak toomonitor istediğiniz hello etki alanının bir üyesi olduğunu doğrulayın.
2. [Merhaba Windows bilgisayar tooOMS bağlanmak](log-analytics-windows-agents.md) veya [, var olan Operations Manager ortamı tooOMS kullanarak bağlanmak](log-analytics-om-agents.md), zaten bağlı değilse.
3. Bu bilgisayarda, kayıt defteri anahtarını aşağıdaki hello ayarlayın:

   * Anahtar: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management grupları\<ManagementGroupName > \Solutions\ADReplication**
   * Değer: **IsTarget**
   * Değer verisi: **true**

   > [!NOTE]
   > Bu değişiklikler, yeniden başlatma hello Microsoft İzleme Aracısı hizmeti (HealthService.exe) kadar etkili olmaz.
   >
   >

## <a name="understanding-replication-errors"></a>Çoğaltma hataları anlama
AD çoğaltma durumu verilerinin tooOMS gönderilen sahip olduğunda, görüntü şu anda kaç çoğaltma hataları belirten hello OMS Panoda izleyen bir kutucuğu benzer toohello bakın.  
![AD çoğaltma durumu kutucuğu](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

**Kritik çoğaltma hataları** veya üstü hello %75 hatalarını olan [ömründen](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) , Active Directory ormanı için.

Merhaba kutucuğa tıkladığınızda hello hatalar hakkında daha fazla bilgi görüntüleyebilirsiniz.
![AD çoğaltma durumu Panosu](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>Hedef sunucu durumu ve kaynak sunucu durumu
Bu sütunlarda hedef sunucular ve çoğaltma hataları yaşıyor kaynak sunucular hello durumu görüntülenir. Her etki alanı denetleyicisi adı Hello numarasıyla o etki alanı denetleyicisindeki çoğaltma hataları hello sayısını gösterir.

Bazı sorunlar hello kaynak sunucu açısından daha kolay tootroubleshoot ve diğerleri hello hedef sunucu açısından olduğundan hello hataları hedef sunucuları ve kaynak sunucular için gösterilir.

Bu örnekte, birçok hedef sunucusu yaklaşık sahip görebilirsiniz hello aynı hata sayısı, ancak diğer tüm hello daha pek çok daha fazla hata sahip bir kaynak sunucu (ADDC35) yok. Toofail toosend veri tooits ortakları neden ADDC35 üzerinde bazı sorun olduğunu olasıdır. Üzerinde ADDC35 Hello sorunlarını giderme hello hedef sunucu alanında görünen hello hataları çoğunu çözebilir.

### <a name="replication-error-types"></a>Çoğaltma hata türleri
Bu alan, kuruluşunuza algılanan hatalar hello türleri hakkında bilgi sağlar. Her hata benzersiz bir sayısal kod ve hello kök hello hatanın nedenini belirlemenize yardımcı olacak bir ileti vardır.

Merhaba halka hello üstünde daha fazla ve ortamınızdaki sık hangi hatalar görüntülenir hakkında bir fikir verir.

Bu, birden çok etki alanı denetleyicileri hello kullanırken gösterir aynı çoğaltma hatası. Bu durumda, olabilir mümkün toodiscover veya bir etki alanı denetleyicisinde bir çözümü belirlemek tıklatıp, diğer etki alanı denetleyicilerinde etkilenen hello tarafından aynı yineleyin hata.

### <a name="tombstone-lifetime"></a>Silinmiş Öğe işareti yaşam süresi
Merhaba ömründen ne kadar süreyle olduğu silinmiş bir nesneyi belirler, tooas bir ilan başvurulan, hello Active Directory veritabanında tutulur. Silinen nesnenin geçişleri hello kullanım ömrü tıklattığınızda, bir atık toplama işlemi hello Active Directory veritabanından otomatik olarak kaldırır.

Merhaba varsayılan kullanım ömrü 180 gün Windows, en son sürümleri ancak 60 gün eski sürümlerinde olduğu ve açıkça bir Active Directory Yöneticisi tarafından değiştirilebilir.

Merhaba kullanım ömrü yaklaştığı ya da çoğaltma hatalarının yaşıyorsanız, önemli tooknow var. İki etki alanı denetleyicisi hello kullanım ömrü devam ederse çoğaltma hata ile karşılaşırsanız, çoğaltma bir çoğaltma hatası için temel alınan hello sabit olsa bile bu iki etki alanı denetleyicileri arasında devre dışı bırakılmış.

Merhaba ömründen alanı devre dışı çoğaltma oluşmasını tehlike içinde olduğu yerlerde belirlemenize yardımcı olur. Her hata hello **% 100'den TSL** kategorisini hello orman için en az hello kullanım ömrü için kendi kaynak ve hedef sunucuda arasında çoğaltılmamış bir bölümünü temsil eder.

Bu durumda, yalnızca hello çoğaltma hatanın düzeltilmesi yeterli olmaz. En azından toomanually gerek tooidentify araştırın ve çoğaltma yeniden başlatmadan önce nesneleri kalan yukarı Temizle. Bir etki alanı denetleyicisi toodecommission bile gerekebilir.

Toplama tooidentifying hello kullanım ömrü kalıcı çoğaltma hatalarını da hello dönmeden toopay dikkat tooany hataları istediğiniz **% 50-75 TSL** veya **75-%100 TSL** Kategoriler.

Bu büyük olasılıkla ihtiyaç duydukları araya tooresolve böylece açıkça kalan, değil geçici hatalardır. Merhaba müjde, bunlar henüz hello ömründen ulaştığınızı değil ' dir. Kısa süre içinde bu sorunları düzeltmek varsa ve *önce* hello ömründen ulaşmak, çoğaltma ile en az el ile müdahale yeniden başlatın.

Daha önce belirtildiği gibi hello Panosu kutucuğu hello AD çoğaltma durumunu çözüm için hello sayısını gösterir. *kritik* (dahil olmak üzere kullanım ömrü % 75'üzerindeki hatalarını tanımlanır, ortamınızdaki çoğaltma hataları üzerinde % 100'tsl hatalarını). Tookeep 0 bu numaradan çalışmalar yapılmaktadır.

> [!NOTE]
> Bir özel silinmiş öğe işareti yaşam süresi değeri ayarlanmış olsa bile bu yüzdeleri doğru güven şekilde hello silinmiş öğe işareti yaşam süresi yüzdesini hesaplamalarının hello gerçek kullanım ömrü, Active Directory ormanı için temel alır.
>
>

### <a name="ad-replication-status-details"></a>AD çoğaltma durumu ayrıntıları
Hello listelerinden birinde herhangi bir öğeyi tıklatın, günlük arama kullanarak hakkında ek ayrıntılar bakın. Merhaba sonuçlar filtrelenmiş tooshow yalnızca hello hatalarla ilgili toothat öğe olur. Tıklayarak, örneğin, hello ilk etki alanı denetleyicisi altında listelenen **hedef sunucu durumu (ADDC02)**, arama sonuçlarını filtre tooshow hataları hello hedef sunucu olarak listelenen etki alanı denetleyicisi ile bakın:

![Arama sonuçlarında AD çoğaltma durumu hataları](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

Buradan, daha fazla filtrelemek, hello arama sorguyu değiştirin ve benzeri. Merhaba günlük arama kullanma hakkında daha fazla bilgi için bkz: [oturum aramaları](log-analytics-log-searches.md).

Merhaba **HelpLink** alan belirli hata hakkında daha ayrıntılı bilgi içeren bir TechNet sayfa hello URL'sini gösterir. Kopyalayın ve sorun giderme ve hello hatanın düzeltilmesi hakkında tarayıcı penceresini toosee bilgilerinizi bu bağlantıyı yapıştırın.

Tıklatarak **dışarı** tooexport hello tooExcel sonuçlanır. Merhaba verileri dışarı aktarma çoğaltma hata verileri istediğiniz herhangi bir şekilde görselleştirmenize yardımcı olabilir.

![Excel'de verilen AD çoğaltma durumu hataları](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>AD çoğaltma durumu hakkında SSS
**S: ne sıklıkta AD çoğaltma durumu verilerinin güncelleştirildi mi?**
Y: hello bilgiler beş günde bir güncelleştirilir.

**S: Bu verilerin ne sıklıkla güncelleştirilme biçimini tooconfigure var mı?**
Şu anda A:.

**S: tooadd ihtiyacım tüm etki alanı denetleyicileri toomy OMS çalışma Alanım sipariş toosee çoğaltma durumu?**
Y: Hayır, yalnızca bir tek etki alanı denetleyicisi eklenmelidir. OMS çalışma alanınızda birden çok etki alanı denetleyicisi varsa, bunların tümünün verilerden tooOMS gönderilir.

**S: tooadd herhangi bir etki alanı denetleyicileri toomy OMS çalışma istemiyorum. Merhaba AD çoğaltma durumunu çözüm kullanabilir miyim?**
Y: Evet. Kayıt defteri anahtarı tooenable hello değerini ayarlayabilir. Bkz: [tooenable olmayan etki alanı denetleyicisi toosend AD veri tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

**S: veri toplama hello hello işlemin hello adı nedir?**
Y: AdvisorAssessment.exe

**S: ne kadar süreyle için toplanan verileri toobe sürer?**
Y: veri toplama zamanı hello hello Active Directory ortamında boyutuna bağlıdır, ancak genellikle 15 dakikadan kısa sürer.

**S: hangi türde veri toplanır?**
Y: çoğaltma bilgilerini LDAP toplanır.

**S: bir şekilde tooconfigure verileri toplandığında var mı?**
Şu anda A:.

**S: izinleri ne toocollect verilerinin gerekiyor?**
Y: normal kullanıcı izinleri tooActive dizin yeterli.

## <a name="troubleshoot-data-collection-problems"></a>Veri toplama sorunlarını giderme
Sipariş toocollect verilerin en az bir etki alanı denetleyicisine bağlı toobe tooyour OMS çalışma hello AD çoğaltma durumunu çözüm paketi gerektirir. Bir etki alanı denetleyicisine bağlanmak kadar belirten bir ileti görüntülenir **veri devam toplanır**.

Etki alanı denetleyicilerinden biri bağlama konusunda yardıma ihtiyacınız varsa, belgeleri görüntüleyebilirsiniz [bağlanmak Windows bilgisayarları tooLog Analytics](log-analytics-windows-agents.md). Alternatif olarak, etki alanı denetleyicinizi zaten bağlı tooan mevcut System Center Operations Manager ortamında ise, belgeleri görüntüleyebilirsiniz [System Center Operations Manager bağlanmak tooLog Analytics](log-analytics-om-agents.md).

Bkz: tooOMS veya tooSCOM, doğrudan tooconnect herhangi bir etki alanı denetleyicileriniz istemiyorsanız [tooenable olmayan etki alanı denetleyicisi toosend AD veri tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı Active Directory çoğaltma durumu verileri.
