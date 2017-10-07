---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - parçaları"
description: "Bilgi nasıl toocreate ve Azure Mobile Engagement kullanarak kullanıcıların tooidentify kullanım desenlerini kesimleri yönetme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a>Nasıl toocreate ve kullanıcıların tooidentify kullanım desenlerini kesimleri yönetme
Bu makalede hello **KESİMLERİ** hello sekmesinde **Mobile Engagement** portal. Merhaba kullandığınız **Mobile Engagement** portal toomonitor ve mobil uygulamalarınızı yönetin.

Merhaba kesimleri hello UI bölümünü hello farklı bir davranışı ve hello uygulamadan elde edebilirsiniz ve hello kesimleri API da erişebilirsiniz analytics göre kullanıcılarınızın kesimlere üzerinde toowork sağlar. Segment ilk 24 saat sonra oluşturuldukları ve bunlar her 24 saatte bir hello son analytics bilgilere göre yeniden hesaplanır. Kesimi hesaplanan sonra her gün bir "Günün tooday geçmişi" grafiğini görüntüler.

> [!NOTE]
> Merhaba birçok bölümlerini **Mobile Engagement** portal UI içeren hello **YARDIMINI Göster** düğmesi. Bu düğme tooget bir bölümü hakkında daha fazla kavramsal bilgi tuşuna basın.
> 
> 

## <a name="create-segments"></a>Kesimleri oluşturun
Üzerinde belirli bir dönem için hello too60 günde yukarı too10 ölçütlerini göre segment oluşturabilirsiniz hello analytics bölümünden geçmiş. Örneğin, belirli sayfalarını görüntülenebilir veya son 10 gün içinde Merhaba, uygulamanızın içinde belirli içerik arama hello kişiler üzerinde dayalı bir segment oluşturabilirsiniz. Bu bilgiler hello analytics bölümünde kullanılabilir. Bu nedenle, toocreate kesimi kullanın ve ardından bir anında iletme bildirimi tootarget kullanıcılar tooget bu kısmı ayarlayın bunları toocome geri toohello uygulama. 

> [!NOTE]
> Bir segment hesaplanan sonra olamaz düzenlenemez; Bunu yalnızca (kopyalanmış) kopyalanması veya (silinmiş) yok. Bir kesim içinde hello kopyalanıp aynı uygulamanın (ile aynı AppID hello), ve (ile farklı bir AppID) diğer uygulamalara da kopyalanabilir. 

 ![segments1][35] 

## <a name="examples-segments"></a>Örnekler parçaları
 ![segments2][36]

Segment toosegment hello son kullanıcılar, uygulamanızın izin verin.
Kullanıcılarınızın kesimlere bir önemli pazarlama stratejidir. Azure Mobile Engagement tooget geçmiş verileri sağlar ve özel kesimleri oluşturun. Bu güçlü bir araç uygulamanızda müşterilerinizin deneyimi hakkında toolearn sağlar. Kolayca segmentlerinizi çözümlemek ve segmentlerinizi itme hedefleri olarak kullanın.
Bir ortak kullanın-son kullanıcılar toorate toosend anında iletme bildirimi tooencourage istediğiniz durumdur hello deposu uygulamanızda. Bir bildirim tooall son kullanıcılarınızı göndermek yerine, yalnızca uygulamanız her gün Merhaba geçen ay kullandınız ve iyi kullanıcı deneyimini beklendiğinden kullanıcılar belirtirsiniz bir segment oluşturabilirsiniz. Daha az, hedeflenmiş anında iletme bildirimleri göndermek için daha iyi ROI alıyorum.

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a>Oluşturabileceğiniz kesimleri hello önemli Azure Mobile Engagement öğelere dayanmaktadır:
* Olay: hedefleri, bir belirli olay katından fazla bir hafta gerçekleşen hello uygulamasının bir segment oluşturun. 
* Oturumu: Merhaba uygulaması 5 defadan fazla geçen hafta kullanan kullanıcı kesimini oluşturun.
* Etkinliği: bir sayfa veya içeriği 10 saat geçen ay sayısından fazla veya az kullanılan kullanıcılar bir parçasını oluşturun.
* Proje: bir iş birden fazla günde tamamladınız kullanıcılar bir parçasını oluşturur.
* Kilitlenme: çökmeyle 10 kereden fazla geçen hafta beklendiğinden tüm hello kullanıcıların bir segment oluşturun. (Bu bir apology veya hatta kupon kesimle itme!)
* Hata: bir hata 100 kez birden fazla son 3 gün beklendiğinden tüm hello kullanıcıların bir segment oluşturun.
* Uygulama bilgileri: son 25 gün hello sırasında gerçekleşen özel bir uygulama bilgisi hedefleyen bir segment oluşturun.
  
  ![segments4][38]

Segment toouse en iyi şekilde, özelleştirilmiş bir hello SDK tümleştirilmesi "Uygulama bilgisini" etiketlerin etiketleme bir plan ile uygulamanızda yapmış olmanız gerekir.
Ardından, hello arabiriminin toohello giriş sayfasına gidin, istediğiniz ve hello "Kesimleri" bölümünü tıklatın Merhaba uygulaması seçin.

1. Merhaba "Kesimleri" bölümü seçin.
2. Yeni bir segment toocreate düğmesini hello "Yeni bir segment"'ı tıklatın.

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a>Gerçek yaşam örnek: "Oturum" bilgilerine dayalı basit bir segment oluşturma
Uygulamanızı hello geçen hafta en az 50 kez kullanmış tüm hello son kullanıcılar bir parçasını oluşturun. Buradan, en az 30 saniye uygulamanızda oturum başına harcanan hello son bulur. Bu uygulamayı olumlu bir deneyim sahibi tüm hello son kullanıcılar gösterir. Sonra oluşturulan hello segment kullanılan toopush bildirim toothese son kullanıcılar tooask olabilir bunları hello uygulamanızda toorate depolar.

 ![segments5][39]

1. Segmentinize sipariş toofind bir ad verin, hızlı bir şekilde hello "Segment" listesi içinde.
2. Merhaba üzerinde "Oluştur" düğmesine tıklayın.
   
   ![segments6][40]

Oturumu seçin.

 ![segments7][41]

1. "Geçen hafta" Merhaba süre seçin.
2. İleri'yi tıklatın.
   
   ![segments8][42]
3. Select hello hello liste arasında ilgili işleci: =; ≥, ≤.
4. Merhaba istediğiniz sayısı girin.
5. Merhaba istediğiniz örneği seçin. 
6. İleri'yi tıklatın.
   Bu örnekte, en az 50 oturumları yapmış olduğunuz kullanıcıları eşleştirmek geçen hafta bu üzerinden hello şekilde ayarlanır.
   
   ![segments9][43]

Hello oturum segment için bir ölçüt olarak oturumu başına hello uzunluğu seçebilirsiniz.

1. Merhaba işleci hello listeden seçin.
2. Oturum başına Hello uzunluğu belirtin.
3. İleri'ye tıklayın.
   Bu örnekte, tüm hello hello oluşumu bölümünde kesimli oturumları seçtiğinizden 30 saniyeden oturum başına harcanan hello kullanıcılar yazacaktır.
   
   ![segments10][44]

Ölçütünüzle hello içinde tamamlamak sipariş tooretrieve içinde ad Huni ve Son'u tıklatın.

 ![segments11][45]

Ölçütünüzle ayar tamamlandığında hello segment Huni içinde görüntülenir.
Bir segment çözümleme verilerini dayandığından, kesimleri günde bir kez hesaplanır.
Bu örnekte, 47,7 hello toplam son kullanıcılar % hello ölçüt eşleşti. İyi bir deneyim beklendiğinden hello kullanıcılar olmalıdır ve bunları bir bildirim gönderme varsa daha yüksek bir derecesinde olası tooprovide toorate hello uygulamayı hello Mağazası'nda yönergelerinin olması.

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

