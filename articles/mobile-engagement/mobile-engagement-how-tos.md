---
title: "Mobile Engagement kullanıcı arabirimi - aaaAzure nasıl ulaşması"
description: "Azure Mobile Engagement için kullanıcı arabirimi genel bakış"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>Nasıl tooget kullanmaya ve tooreach tooyour son kullanıcılar çıkışı iter yönetme
Merhaba SDK tamamen uygulamanıza tümleşiktir sonra hello hello ulaşma hello UI tooPush bildirimleri toohello kullanıcılar, uygulamanızın bölümünü kullanmaya başlayabilirsiniz.  

## <a name="do-your-first-push-notification-campaign"></a>İlk anında iletme bildirimi kampanyanızı yapın
* Merhaba SDK'sı ile uygulamanızı elinizin tümleştirilmiş onaylayın. 
* Uygulamanızı seçin

![First1][1]

* Toohello "Reach" bölümü ve tıklatın "Yeni duyuru" gidin

![First2][2]

* Yeni bir kampanya oluşturun ve adlandırın
  
![First3][3]

* Nasıl hello bildirim, uygulama yalnızca gönderilmesi gereken seçin

![First4][4]

* Toopush istediğiniz hello iletisi oluşturun

![First5][5]

* Merhaba bildirim (isteğe bağlı) bir başlık yazabilir.
* Anında iletme iletisi içeriği yazma.
* Görüntüyü karşıya yükleyebilirsiniz. Merhaba hello dosyasının boyutunu 32.768 baytı aşamaz unutmayın.
* Seçenekleri daha fazla hello özelliği tooselect de, ancak bu öğreticide hello odağının, daha sonra göreceğiz.
* Yalnızca bildirim olarak Hello içerik türü seçin

![First6][6]

* Anında iletme kampanyanızı oluşturmak ve kampanya listenizde görüntülenir.

![First7][7]

## <a name="test-your-push-notification-campaign"></a>Anında iletme bildirimi kampanyanızı test
![Test1][8]

* Cihazınızı kaydedin.
* Tıklatın hello aygıt hello onay kutusunu toopush istiyor.
* Merhaba üzerinde "Test" düğmesine toosend hello itme toohello aygıt'ı tıklatın.

![Test2][9]

* Merhaba kampanyayı etkinleştirmek

![test3][10]

* Kampanyanızı oluşturduğunuza göre tooactivate yeterlidir tooyour kullanıcılar hello bildirim toobe için gönderilir.

## <a name="send-personalized-pushes"></a>Kişiselleştirilmiş bildirim gönder
* Bu örnek, bir özel indirim kodu hello anında iletme bildirimi girildiği push oluşturur.

![Personalize1][11]

Kişiselleştirme çalışır, böylece tarafından bir işaretçi bir uygulama bilgisi etiketinde değiştirerek toomake hello kullanıcının hello uygun app-info ilk tanımlı olduğundan emin sahip olacaksınız. Bu örnek hello hedeflenen kullanıcılara tanımlanan rebate_code adlı bir uygulama bilgisi etiketi sahip olur.
Yukarıda gördüğünüz gibi hello anında bildirim içeriği hello tarafından hello uygulama bilgisi etiketinin gerçek içerik yerine toobe olduğunu gösteren hello işaret ${rebate_code} içerir.

> [!WARNING]
> Merhaba uygulama bilgisi etiketi hello kullanıcıdan tanımlanmazsa hello kullanıcı hello itme alırsınız.

* Sonuç

![Personalize2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>Daha fazla hello metin bildiriminizin kişiselleştirebilirsiniz
![Personalize3][13]

* Merhaba bildirim Hello başlığı dahil olmak üzere,
* Ve selamlama iletisine Merhaba içeriğine.
* Duyuru (metin görünümü veya Web görünümü) Hello türünü seçin

![Personalize4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>Duyuru Hello gövdesi ile de kişiselleştirilmiş:
* Giriş sayfasında toocustomize hello Hello eylem URL'si, istediğiniz
* Merhaba başlığı
* Merhaba hello ileti gövdesi.

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>Bilgisayarınızı anında iletilen bildirim (içeri veya uygulama dışında) ayırt
* Anında iletme, uygulamanızı seçin, toohello "Reach" bölümüne gidin, seçin veya bir anında iletme kampanya oluşturacak ve toohello "Bildirim" bölümüne gidin bildirim Hello türünü seçin.
* ' I tıklatın, "teslimat" Merhaba üzerinde istediğiniz.
* Belirli etkinlikleri (ekranları) hello bildirim istediğinizde "Kısıtlamak etkinlikler" onay kutusunu oluşur hello tıklayın.

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a>"Yalnızca uygulama dışında" teslimat
![Differentiate2][16]

"Yalnızca uygulama dışında" teslimat hello uygulama kapatıldığında anında iletme bildirimi sağlar. Merhaba standart anında iletme bildirimi budur.
"Yalnızca uygulama dışı" seçtiğinizde, zaten uygulamanız (APNS veya GCM) oluşturuyor hello platform hello sertifikalardan sağlamış olmanız gerekiyor.

### <a name="see-also"></a>Ayrıca bkz.
* [Apple anında bildirim hizmeti – sertifikaları](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google bulut Mesajlaşma – sertifika](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>"uygulama yalnızca" teslimat
![Differentiate3][17]

Merhaba uygulama çalışırken "Uygulama yalnızca" teslimat anında iletme bildirimi sağlar.
Bu bildirim için hello APNS aracılığıyla toogo ve GCM sistem gerekmez.
Kullanıcılarınıza hello uygulama teslim sistemi tooreach kullanabilirsiniz.
Tam olarak hello bildirim özelleştirmek ve hangi etkinliğin (ekran) hello bildirim görünür karar verebilirsiniz.

### <a name="anytime-delivery-mode"></a>"Dilediğiniz zaman" teslimat
Bir "Her zaman" teslimat seçebilirsiniz, son olup hello tooreach sağlar veya uygulama çalıştıran.
"Dilediğiniz zaman" seçtiğinizde, zaten uygulamanız (APNS veya GCM) oluşturuyor hello platform hello sertifikalardan sağlamış olmanız gerekiyor. 

## <a name="schedule-a-push-campaign"></a>Anında iletme kampanya zamanlama
### <a name="plan-toostart-a-campaign"></a>TooStart bir kampanya planlama
![Shedule1][18]

Mart 21st hello olduğundan ve bir duyuru toomake sahip Merhaba Mart 22nd gece yarısı planlanmış. Merhaba arabirimi toodo push önünde toostay yok! Bildirim gönderilir önceden hello tam dakika planlayabilirsiniz.

* Kaldırma onay hello "Hiçbiri" onay kutusunu ve bir başlangıç saati seçin 
* Başlangıç tarihi ve toostart hello itme kampanya hello saatini seçin.

### <a name="plan-tooend-a-campaign"></a>Tooend bir kampanya planlama
![Shedule2][19]

Hello üzerinde kampanya toostop Mart 25 3:00 pm istediğiniz ancak, olmayacak var. toodo biliyorsanız.
Merhaba arabirimi toopush önünde toostay yok! Kampanyanızı durdurur önceden hello tam dakika planlayabilirsiniz.

* "Hiçbiri" Merhaba üzerinde tıklatın onay kutusu veya bir bitiş saati seçin
* Başlangıç tarihi ve toofinish hello itme kampanya hello saatini seçin.

### <a name="end-a-campaign-manually"></a>Bir kampanya el ile bitmelidir
![Shedule3][20]

Varsayılan olarak, "None" onay kutularının seçili hello.
Hello etkinleştirdikten hemen hello kampanya başlar deyişle bölüm ulaşmak ve üzerinde hello durdurulacak zaman son bölümü ulaşabileceği.

> [!NOTE]
> Bitiş tarihi oluşturulan Kampanyalar hello itme hello cihazda yerel olarak depolamak ve hello kampanya el ile sona erdi olsa bile hello uygulama açıldığında hello göster.

## <a name="enhance-a-push-notification-with-a-text-view"></a>Metin görünümü ile anında iletme bildirimi geliştirin
### <a name="what-is-a-text-view"></a>Metin Görünümü nedir?
![TextView1][21]

Metni metin içeriği içeren bir açılır pencere görülmektedir. Merhaba son kullanıcı hello anında iletme bildirimine tıklamıştır sonra bu açılır pencere görünür.
Metin görünümü toopresent sağlar. daha fazla içerik tooyour son kullanıcı. Bu aynı zamanda hello fırsat toopresent tooa bir web sayfasını açarak deposu başlatma, coğrafi olarak yerelleştirilmiş arama, vb. bir e-posta gönderme, yeniden yönlendirme, uygulamanızın tooa sayfa atlama gibi bir çağrı tooaction olup...

### <a name="example-text-view"></a>Örnek: Metin görünümü
* Merhaba "Ulaşmak" bölümünde anında iletme bildirimi kampanyanızı oluşturmak ve kampanyanızı adlandırın

![TextView2][22]

* Görünür selamlama iletisine hello bildirim yazma.
* Merhaba duyuru "metin" içerik türü seçin

![TextView3][23]

> [!NOTE]
> Metin görünümü bastığınızda, her zaman içeren bir bildirim önce gelir. 

* Merhaba metni (Merhaba metin duyuru içeriği hello alt bölümünün görünür, görüntülenen toobe toodefine hello metin izin vererek seçtikten sonra.) tanımlayın

![TextView4][24]

* Merhaba selamlama iletisine üstünde görünür hello başlık yazın.
* Merhaba ana hello metin görünümü içeriğini yazma.
* Merhaba eylem düğmesine (eylem düğmesi hello uygulama toomake tooan App store veya herhangi bir tür, sağlayabilirsiniz kaynakları yönlendirme hello uygulama sayfasını açarak gibi belirli bir eylemi sağlar) görünür hello içerik yazma.
* Merhaba çıkış düğmesinde görünür yazma hello içeriği (Merhaba çıkış düğmesini tıklatarak hello metin görünümü kaybolur.)
* Anında iletme bildirimi kampanyanızı oluşturmak ve hello kampanya listede görüntülenir.

![TextView5][25]

* Anında iletme bildirimi kampanya toosend hello metin görünümü tooyour kullanıcılarınızın etkinleştirin.

![TextView6][26]

* Sonuç

![TextView7][27]

* Merhaba kullanıcı hello bildirim ve onu tıklatıldığında alır.
* Merhaba metin görünümü, bir açılır izin hello kullanıcı toointeract onunla olarak görünür.

## <a name="enhance-a-push-notification-with-a-web-view"></a>Bir Web görünümü ile anında iletme bildirimi geliştirin
### <a name="what-is-a-web-view"></a>Bir Web Görünümü nedir?
![WebView1][28]

Bir web görünümü web içeriği içeren bir açılır pencere ' dir. Merhaba son kullanıcı hello anında iletme bildirimine tıkladığında bu açılır pencere görünür.
Web görünümü toohave sağlar hello son kullanıcı ile daha fazla etkileşimi.
Bu aynı zamanda hello fırsat toopresent çağrısı tooaction yeniden yönlendirme tooApp bir web sayfasını açarak başlatma, coğrafi olarak yerelleştirilmiş arama, vb. bir e-posta gönderme deposu gibi olup...

### <a name="example-web-view"></a>Örnek: Web görünümü
* Merhaba "Ulaşmak" bölümünde anında iletme kampanyanızı oluşturmak ve kampanyanızı adlandırın.

![WebView2][29]

* Görünür selamlama iletisine hello bildirim yazma.
* "Web" Merhaba duyuru içerik türü seçin

![WebView3][30]

### <a name="about-announcement-types"></a>Duyuru türleri hakkında:
* Yalnızca bildirim: Basit standart bir bildirim değil. Kullanıcı üzerinde tıklatır, ek görünüm yok görünür, ancak yalnızca hello eylem ilişkili tooit ortaya çıkar anlamına gelir.
* Metin duyuru: hello kullanıcı toohave metin görünümü göz prosese bir bildirimidir.
* Web duyuru: hello kullanıcı toohave bir web görünümü göz prosese bir bildirimidir.
  Merhaba "Web duyuru" içerik seçin.

> [!NOTE]
> Bir web görünümü bastığınızda, her zaman içeren bir bildirim önce gelir.

* (Merhaba duyuru, web içeriği hello alt bölümde görünür, görüntülenen toobe istediğiniz toodefine hello web görünümü içeriğini izin vererek seçtikten sonra.) Hello web içeriğini tanımlayın

![WebView4][31]

* (İsteğe bağlı) selamlama iletisine hello üstünde görünür hello başlık yazın.
* HTML kodunuzu buraya yazın.
* Hello kaynağında düzenleme modu düğmesi tooswitch edition'ı tıklatın ve nasıl gibi göründüğünü görebilirsiniz.
* Merhaba eylem düğmesine (eylem düğmesi hello uygulama toomake tooa deposu veya herhangi bir tür, sağlayabilirsiniz kaynakları yönlendirme hello uygulama sayfasını açarak gibi belirli bir eylemi sağlar) görünür hello içerik yazma.
* Merhaba çıkış düğmesinde görünür yazma hello içeriği (Merhaba çıkış düğmesini tıklatarak hello web görünümü kaybolur).
* Sonuç

![WebView5][32]

* Merhaba kullanıcı hello bildirim almak ve tıklayın.
* Merhaba metin görünümü, bir açılır izin hello kullanıcı toointeract onunla olarak görünür.

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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

