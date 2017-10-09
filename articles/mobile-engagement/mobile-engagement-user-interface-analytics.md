---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - Analytics'i"
description: "Bilgi nasıl Azure Mobile Engagement kullanarak uygulamanız hakkındaki geçmiş verilerini tooanalyze"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a>Nasıl uygulamanız hakkındaki geçmiş verilerini tooanalyze
Bu makalede hello **ANALYTICS** hello sekmesinde **Mobile Engagement** portal. Merhaba kullandığınız **Mobile Engagement** portal toomonitor ve mobil uygulamalarınızı yönetin. İlk ihtiyacınız toocreate hello portalını kullanarak bu toostart Not bir **Azure Mobile Engagement** hesabı.

Hello hello UI Analytics bölümünü, 24 saatte bir güncelleştirilir geçmiş verilere dayanan uygulamanız hakkında toplanan bilgiler sağlar. Merhaba bilgi çubuğu/satır/pasta grafikler, kılavuzları ve haritalar oluşan farklı panolarda görüntülenir. Merhaba verileri de .csv dosyaları olarak indirilebilir. Bu aynı bilgilerin çoğunu hello hello UI İzleyici bölümünü gerçek zamanda kullanılabilir ve hello Analytics API ' da erişilebilir.

> [!NOTE]
> Merhaba birçok bölümlerini **Mobile Engagement** portal UI içeren hello **YARDIMINI Göster** düğmesi. Bu düğme tooget bir bölümü hakkında daha fazla kavramsal bilgi tuşuna basın.

## <a name="standard-and-custom-analytics"></a>Standart ve özel analizi
Azure Mobile Engagement uygulamanız hello SDK'sı ile tümleştirme hemen çizilebilir, uygulamalar ile ilgili temel, standart analitik bilgileri kümesi sağlar. Azure Mobile Engagement ayrıca istediğiniz hello özelliği toogather ek özel analytics hakkında bilgi, son kullanıcılarınızın davranış sağlar. Bir etiket planı "oluşturulan özel etiketler (uygulama bilgisi)", oluşturarak bunu yapabilirsiniz **ayarları** böylece Azure Mobile Engagement, bu ek verileri toplayın.

## <a name="analytics"></a>Analiz
* Pano: yeni ve Etkinleri kullanıcılarınıza ve onların eğilimleri hakkında genel bilgileri gösterir.
* Kullanıcılar: Kullanıcılar, cihaz tanımlayıcılarına göre tanımlanır: Bu tanımlayıcı her cihaz için benzersizdir (yeni bir kullanıcı olduğundan gerçekte bir yeni aygıt). İlk oturumunu bu zaman aralığında gerçekleştirdiyse bir kullanıcı yeni bir belirli bir zaman aralığında kabul edilir. Kullanıcı en az bir oturum sırasında hello son 7 gün gerçekleştirdiyse elde tutulmuş kabul edilir. Etkin kullanıcılar en az bir oturum belirli bir süre boyunca yapılan kullanıcılardır. Göre aylık, haftalık, günlük veya saatlik zaman dönemi sıralama yapabilirsiniz. Tüm hello grafikleri şuna benzer ancak toofilter hello sürümü, uygulama ve ardından toosort gibi farklı özellikleri tarafından bir zaman aralığında izin verir. Merhaba hello SDK ile tümleştirerek toplanan standart bilgileri hello aşağıdakileri içerir: etkin kullanıcılar, yeni bir kullanıcı, oturum sayısı, her oturum, hello ülke, yerel öğeler, konum, dil taşıyıcı, aygıtlar, bellenimi hakkında teknik bilgi uzunluğu Ağ (WIFI) hello uygulama ve müşterileri tarafından kullanılan SDK sürümleri. Bu bilgi, gerçek zamanlı hello İzleyici bölümünden görüntülenebilir.

> [!NOTE]
> Başlangıç tarihi yanlış ayarlanmış olan telefon sahip bir kullanıcı hello süre yanlış gösterilebileceği şekilde hello hello kullanıcıların cihaz ayarları, başlangıç tarihinden süre dayanır.

* Bekletme: Bir kullanıcı ilk oturumunu bu zaman aralığında gerçekleştirdiyse bir belirli bir zaman aralığında elde tutulmuş kabul edilir. Elde tutulmuş kullanıcıların (ve yeni kullanıcıların) toohours, gün, hafta veya ay sayıldığı zaman aralıklarını hello değiştirebilirsiniz. Merhaba kullanıcı bekletme analytics cohorts üzerinde oluşturulmuştur. Bir kohort hello (yani, bu süre boyunca ilk oturumuna gerçekleştirme kullanıcılar hello kümesi) belirli bir dönem için algılanan tüm hello yeni kullanıcılar kümesidir. 1 gün, 2 gün, 4 gün, 7 gün veya 1 aylık cohorts kullanırız. Kohort, her gün 1, 2 gün, 4 gün, 7 gün veya 1 aylık Azure Mobile Engagement hesaplar hello kümesi tüm kullanıcılara kimin toohello kohort ve hala etkin olan (yani, hello kümesi hello dönemde en az bir oturum sırasında gerçekleştirilen kullanıcılar) ait. Bu kullanıcı kümesi kohort sürüm adı verilir. (Azure Mobile Engagement, kullanıcılarınızın kaç uygulamanızı kullanmaya devam gösterebilir, ancak yalnızca hello platform belirli deposu kullanıcılarınızın kaç Windows mağazası, app - Örneğin, GooglePlay, iTunes kaldırılması öğrenebilirsiniz vs.).
* Oturumlar: Tek bir kullanıcı tarafından Merhaba uygulaması kullanımı. Oturumlar, kullanıcılar tarafından gerçekleştirilen etkinliklerin hello serisinden oluşturulur (bir etkinlik hello uygulamanın bir ekran genellikle ilişkili toohello kullanımını bağlıdır, ancak bu SDK hello uygulamada bütünleştirilmiştir hello şekilde hello bağlı olarak değişebilir). Bir kullanıcı aynı anda yalnızca bir etkinlik gerçekleştirebilirsiniz: hello kullanıcı ilk etkinliğini başlar ve kendisine son etkinliğini bitirdiğinde durur hemen bir oturumu başlatır. Bir kullanıcı birden fazla birkaç saniye herhangi bir etkinlik yapmadan kalırsa, kendi etkinlik dizisini iki ayrı oturumlara ayrılır.
* Etkinlikler: her ekranda, uygulamanızdaki her ekran hello adlarını ve kullanıcılar hello uzunluğu ayırın. Etkinlikler kendi uygulamanız için ayarladığınız toohello "uygulama bilgisini" etiketleri karşılık gelir özel bir analitik seçeneği şunlardır:
* Kullanıcı yolu: kullanıcılarınızın uygulama etkinlikleri (ekranları) içinde nasıl gezindiğini gösterir. Merhaba kaydırıcı tooadjust hello ayrıntı düzeyini taşıyabilirsiniz. Mavi düğümler uygulamanızın etkinliklerini ifade eder. Kendi boyuttur orantılı toohello zaman kullanıcıların bunlar içinde geçirdiği. Beyaz düğümler oturum başlangıcını ve bitişini ifade eder. Kırmızı düğümler çökme (Crash) ifade eder. Bağlantılar uygulamanızın etkinlikleri arasındaki (veya etkinlikler ile çökmeler arasındaki) geçişleri ifade eder. Bir düğüm veya bağlantı toodisplay verileriniz hakkında daha fazla bilgi içeren bir araç ipucunu tıklatın: hello için harcanan süre belirli bir ekranda hello geçiş sayısı ve hello kaynak etkinliği toohello hedef etkinliğinden geçiş hello yüzdesi. (Bir---60%---> B anlamına gelir bir gelecek tooactivity B başlangıç saati % 60 etkinliğindeki kullanıcıların.) Merhaba grafik tooclarify istediğiniz şekilde yeniden düzenleyebilirsiniz; Her bir değişiklik yaptığınızda konumu kaydedilir. Gösterebilir veya hello kilitlenme toolighten hello grafik gizleyebilirsiniz.
* Olayları: hello uygulamada bir kullanıcı tarafından yapılan belirli eylemler. olayların Hello dağıtım hello olayları kullanıcı başına oturum sayısı olarak gösterilir. Bir olay anlık bir eylemi, örneğin, bir bildirim düğmesini veya hello alımını tıklama temsil eder. (olayların anlamı hello hello SDK hello uygulamada nasıl tümleştirildiğine üzerinde bağlıdır.) Bir olay bir oturum ya da iş sırasında oluşabilir veya tek başına olabilir.
* İşlerini: hello eylemin hello uzunluğu odak dışında benzer tooevents. Örneğin, işleri içerik tooload veya çağrı tooweb hizmet süreyi hakkında teknik bilgiler söyleyebilirsiniz. Bunu Ayrıca kullanıcı toofill form süreyi gösterir, bir hesap oluşturun veya satın alma. Bir işi hello bir görevin süresini temsil eder, örneğin, hello bir indirme görevinin süresi veya hello bir başlık süre Merhaba ekranında görüntülenir. (işlerin anlamı hello hello SDK hello uygulamada nasıl tümleştirildiğine üzerinde bağlıdır.) İşlerini genellikle bir oturumun (yani, herhangi bir kullanıcı etkinliği olmadan) hello kapsamı dışında gerçekleştirilen arka plan görevleri ile ilişkilendirilir.
* Technicals: Hakkında teknik bilgiler hello cihazların Merhaba kullanıcıların uygulamanızın, hello hello kullanıcıların cihazlarına yerel ayar, taşıyıcı, ağ, aygıt, bellenim ve ekran boyutunu ve hello hello kullanılan SDK sürümü ve uygulama sürümü gibi uygulamanızda izleyebilirsiniz.
* Hatalar: Merhaba uygulaması içinde hello uygulama toocrash neden olmaz teknik hatalarla ilgili bilgi. Bir hata, bir ağ hatası veya hatalı işleme gibi anlık bir sorunu temsil eder. (olayların anlamı hello hello SDK hello uygulamada nasıl tümleştirildiğine üzerinde bağlıdır.) Hata bir oturum ya da iş sırasında oluşabilir veya tek başına olabilir.
* Çökme (Crash): Uygulama toocrash neden hatalar hakkında bilgi. Bir kilitlenme burada hello uygulamanın beklenen işlevlerini gerçekleştirmeyi durdurduğu ve durdurulması gerektiği beklenmeyen bir durumdur. Bir çökme genellikle Merhaba uygulaması tooa hata nedeniyle kaynaklanır.

![Analytics2][11]

## <a name="accessing-hello-retention-overview"></a>Merhaba bekletme genel bakış erişme
![Analytics3][12]

Merhaba bekletme genel bakış ayrılmıştır hello Orta birkaç kartları içine, belirli bir bekletme dönemi için her gösteren hello genel bakış. Merhaba 2 gün Bekletme dönemi hello örnekte görülür. Merhaba diğer kartlar hello 4 gün ve 7 gün bekletme süreleri gösterir.

## <a name="understanding-hello-retention-overview-cards"></a>Merhaba bekletme genel bakış kartları anlama
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a>Her bir kart 3 ana bölümden oluşur:
1. 1: Merhaba kohort ve hello süresi kabul
2. 2-4: Merhaba bekletme hello için geçerli dönem
3. 5: bir mini hello geçmişi

### <a name="here-is-detailed-information-about-each-element"></a>Her öğe hakkında ayrıntılı bilgiler aşağıdadır:
1. Kohort ve süresi: Bu başlık kohort hello türü sağlar. Burada "2 günlük süre" anlamına kullanıcıların hello davranış üzerinde 2 gün görüneceğini 2 gün bloklarını aşağıdaki hello bağlandıklarında gün ve olup olmadığını 2 döneminde gelen kullanıcılar. Yukarıdaki örnekte Merhaba, kullanıcılar hello arasında hello etkinliğini göz önünde bulundurur 21 ve Kasım, 22.
2. Bu hello bekletme oranı 21 ve Kasım 22 hello 19 ve Kasım 20 ulaşan hello kullanıcılar için sağlar. Burada size Merhaba 21st ve 22nd, üzerinde yeni kullanıcılar arasında olan 3 hello 1 etkin kullanıcı arasında vardı hello 19 ve 20.
3. Yukarıdaki aynı bilgileri grafik temsil bu görsel gösterge verir hello. (Merhaba üçüncü Merhaba daire hello % 33 sayıdır.) Merhaba renk ek bilgiler verir: yeşil gösterir bu numarayı hello önceki hesaplama artmaktadır. Sarı azalan kararlı ve kırmızı anlamına gelir.
4. Merhaba hesaplama için kullanılan hello değerleri gösterir.
5. Merhaba bekletme değerlerin hello geçmişinin bir mini budur. Toosee hello değerleri izin verir, toohave nasıl gelişen bir geniş görünümünü hello.

## <a name="see-also"></a>Ayrıca bkz.
* [Kavramları][Link 6]
* [Sorun giderme kılavuzu hizmeti][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md
