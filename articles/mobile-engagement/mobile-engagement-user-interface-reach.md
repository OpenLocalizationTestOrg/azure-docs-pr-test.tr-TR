---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - ulaşma"
description: "Bilgi nasıl Azure Mobile Engagement kullanarak anında iletme bildirimleri ile uygulamanızın toohello kullanıcıları çıkışı tooreach"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a>Nasıl tooreach toohello kullanıcılara anında iletme bildirimleri ile uygulamanızın çıkışı
Bu makalede hello **ULAŞMAK** hello sekmesinde **Mobile Engagement** portal. Merhaba kullandığınız **Mobile Engagement** portal toomonitor ve mobil uygulamalarınızı yönetin. İlk ihtiyacınız toocreate hello portalını kullanarak bu toostart Not bir **Azure Mobile Engagement** hesabı. Daha fazla bilgi için bkz: [bir Azure Mobile Engagement hesabı oluşturma](mobile-engagement-create.md).

Merhaba UI hello bölümünü hello itme kampanya yönetim aracı oluşturma/düzenleme/etkinleştirmek/bitiş/İzleyici yapabileceğiniz ulaşmak ve anında iletme bildirimi kampanyaları ve ayrıca hello Reach API'sini (ve bazı öğelerini hello düşük erişilebilen özelliklere istatistikleri almak Düzey itme API). Merhaba API'leri veya hello UI kullanıp kullanmadığınızı toointegrate gerekeceğini unutmayın Azure Mobile Engagement ve Reach hello kullanabilmeniz için önce SDK ile her platform için uygulamanıza Reach kampanyaları.

> [!NOTE]
> Merhaba birçok bölümlerini **Mobile Engagement** portal UI içeren hello **YARDIMINI Göster** düğmesi. Bu düğme tooget bir bölümü hakkında daha fazla kavramsal bilgi tuşuna basın.
> 
> 

## <a name="four-types-of-push-notifications"></a>Dört tür anında iletme bildirimleri
1. Duyurular - uygulamanızı veya toosend içinde tooanother konum yönlendirmek toosend reklam iletileri toousers izin bunları tooa Web sayfası veya mağaza uygulamanızı dışında. 
2. Anketler - izin, son kullanıcılardan toogather bilgi sorular sorarak.
3. Veri gönderimleri - toosend bir ikili veya base64 veri dosyası sağlar. Veri gönderiminde yer alan hello bilgileri tooyour uygulama toomodify kullanıcılarınızın geçerli deneyimi uygulamanızda gönderilir. Veri gönderimi toobe mümkün tooprocess hello verileri uygulamanız gerekir.

## <a name="campaign-details"></a>Kampanya ayrıntıları
Düzenleme, kopyalama, silme veya henüz adlarını gelerek etkinleştirilmedi Kampanyalar etkinleştirmek veya tooopen tıklatabilirsiniz bunları. Adlarını gelerek zaten etkinleştirilmiş Kampanyalar kopyalayabilir veya tooopen tıklatabilirsiniz bunları. Ancak, etkinleştirildikten sonra bir kampanya değiştiremezsiniz.

![Reach1][18]

## <a name="reach-feedback"></a>Geri bildirim ulaşmak
Tıklayın **istatistikleri** Reach kampanya toosee hello ayrıntıları. Merhaba **basit** hello biçiminde bir kampanyanın etkinleştirildiği sonra ne hakkında bir sütun çubuk grafik görsel bir görünümünü sağlar. Merhaba **Gelişmiş** görünümü hello itme kampanyayla ilgili daha ayrıntılı ayrıntıları sağlar. Bir test kampanya bir itme gönderilen tooa test cihazı yani gönderiyorsanız, bu ayrıntıları kullanılamaz. Bu ayrıntılar nasıl yorumlanacağı aşağıda verilmiştir:

1. **Gönderilen** -bu hello toohello cihazlara gönderilen ileti sayısını belirtir. Bu sayı hello itme kampanya oluşturulurken belirtilen hello hedef kitle bağlıdır. Hiçbir hedef kitle belirtmezseniz, bu itme tooall hello kayıtlı cihazlar gönderilir. Diğer tüm itme Hizmetleri gibi biz hello anında iletme bildirimleri değil doğrudan toohello cihazlara ancak bunun yerine bunları toohello ilgili platformun gönderme belirli anında bildirim Hizmetleri (PNS - GCM/APNS/WNS) böylece toohello cihazların Merhaba bildirimleri sunabilir. 
2. **Teslim** -bu Mobile Engagement SDK'sı tarafından alınan olarak hello başarıyla hello PNS toohello aygıt tarafından sunulan ve onaylanan ileti sayısını belirtir. 
   
   *Teslim edildi nedenlerle basılmış sayısından daha az olan sayısı:*
   
   1. Merhaba kullanıcı hello uygulama hello CİHAZDAN kaldırdı. ancak hello PNS hakkında size hello itme toohello PNS göndereceğiz hello zamanında bilmiyor selamlama iletisine bırakılır.
   2. Merhaba uygulama Hello aygıt varsa ancak hello aygıtları kendilerini uzun bir süre için çevrimdışı, ardından hello PNS toodeliver hello ileti toohello aygıt başarısız olur. 
   3. Merhaba ileti toohello aygıt teslim ancak hello Mobile Engagement SDK'sı hello uygulamasında selamlama iletisine Merhaba içeriğine tanımıyor, sonra bu iletiyi bırakır. Merhaba bildirim hello uygulamasında Hello özelleştirmesini hello SDK ve açılan hello iletisinde, biz catch özel durum oluşturursa bu durum oluşabilir. Bu da hello cihaza hello uygulamanın ise hello platformundan hello mümkün toounderstand hello daha yeni sürümü hello anında iletme iletisi değil Mobile Engagement SDK'ın bir sürümü kullanılarak gönderilen ancak yalnızca hello uygulama hello bildirim sonra yükseltildiğinde bu oluşabilir Merhaba hizmet platformundan gönderildi. Merhaba **Gelişmiş** sekmesi, kaç tane iletileri bırakılan olmadığını bildirir. 
   4. İOS cihazlarda iletileri bazen ya da hello cihaz düşük pil gücüyle ise veya hello uygulama güç önemli miktarda uzak bildirimler işlerken kullanıp kullanmadığına teslim. Merhaba iOS cihazları kısıtlamasıdır.   
3. **Görüntülenen** -bu hello başarıyla toohello uygulama kullanıcı bir sistem itme/çıkış-in-uygulama bildirimi hello bildirim merkezinde veya bir uygulama bildirimi hello içinde hello biçiminde hello aygıtta Mobil gösterilen iletilerinin sayısını belirtir uygulama.  Merhaba **Gelişmiş** sekmesini söyleyin, sistem bildirimleri kaç tane ve uygulama içi bildirimler kaç tane. 
   
   *Görüntülenen nedenlerle (bekleme toobe görüntülenen) teslim edildi sayısından daha az olan Say*
   
   1. Hello bildirimi kampanyası hello bildirim teslim edildi ancak zaman hello zaman tooopen gelen mümkündür sonra bir bitiş tarihi üzerinde var ve toohello uygulama kullanıcı görüntülemek, hiçbir zaman gösterilen şekilde zaten dolmuştur.   
   2. Ardından Hello bildirim bir uygulama bildirimi ise hello uygulama hello uygulama kullanıcı oturum açtığında hello bildirim yalnızca görüntülenir. Merhaba uygulama kullanıcı hello uygulama burada açmadığını durumlarda hello SDK hello bildirim teslim ancak hello uygulama açılıncaya kadar henüz görüntülenen rapor eder. 
   3. Merhaba bildirim bir uygulama bildirimi ise ve ayrıca hello bildirim teslim olarak bildirilir sonra belirli bir etkinlik/ekranda gösterilen toobe yapılandırılmış ancak kadar teslim edilmedi hello kullanıcı belirli bir ekranda hello uygulama açar. 
4. **Kullanıcı etkileşimleri** -bu hello hangi hello uygulama kullanıcı ile etkileşime ve eylem yapılan veya Çıkılan hello iletileri içerecektir iletilerinin sayısını belirtir. 
   
   * *Merhaba uygulama kullanıcı, yolu izleyerek hello birindeki bir bildirim işlem yapabilir:*
     
     1. Merhaba, bir sistem/çıkış-in-uygulama bildirimi bildirimidir veya bir uygulama bildirimi yalnızca bildirim olarak gönderilen sonra hello uygulama kullanıcı hello bildirim.
     2. Merhaba bildirim metin ya da web görünümü içeren bir uygulama bildirimi ya yoklamalar sonra uygulama kullanıcı hello ise üzerinde hello hello bildirim eylem düğmesine tıklar.
     3. Bir web görünümü içeren bir uygulama bildirimi ardından Hello bildirim ise, uygulama kullanıcı tıklar hello web [Android yalnızca görüntüleme] bir URL'de hello
   * *Merhaba uygulama kullanıcı, yolu izleyerek hello birindeki bir bildirim çıkabilirsiniz:*
     
     1. Merhaba bildirim Hello Kapat düğmesini doğrudan tıklatarak. 
     2. Hemen geçirmeyi veya hello bildirim siliniyor. 
     3. Metin/web içeriği ve anketler ile uygulama bildirimleri genellikle görüntülenen toohello uygulama kullanıcı iki adımlı bir işlem var. Bir bildirim ilk görür ve üzerinde'ı tıklattığınızda hello sonraki metin/web/yoklama içeriğin görürler. Merhaba uygulama kullanıcı ya da bu adımları bildiriminde çıkabilirsiniz ve hello Gelişmiş görünümde hello ayrıntılar bu yakalar. 
5. **İşleme alınan** -bu hello hello uygulama kullanıcı tarafından açıkça işleme alınan iletilerin sayısını belirtir. Bu, hello bildiriminde gönderilen selamlama iletisine tarafından kaç uygulama kullanıcıların ilgileniyor söylerken bu hello en ilginç numarasıdır. 

> [!NOTE]
> Merhaba kullanıcının hello uygulamasını açın ve hello kampanya varsa dışında uygulama ve uygulama içi bildirimler hem de başlangıç görüntülenir mümkündür iOS & Windows platformları, "Her zaman" kampanya olduğu aynı anda. Bu teslim edildi hello yüksek bir görüntülenen sayısı neden olabilir. Merhaba kullanıcı etkileşim isterseniz Eylemler hello bildirim sonra bile hello kullanıcı etkileşimleri/Actioned sayısı teslim edildi büyük olabilir. 
> 
> 

![Reach2][19]

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

