---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - hesabım"
description: "Bilgi nasıl toomanage Azure Mobile Engagement hesabı profili ve test cihazlarınızı"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 22832678-3959-4b8c-9fb2-f2ff5974e5d1
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1d85f0e87c43605f59f6536ae42a7fb6a99ee36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-your-account-profile-and-test-devices"></a>Nasıl toomanage hesap profili ve test cihazları
Bu makalede hello **giriş** hello sayfasının **Mobile Engagement** portal. Merhaba kullandığınız **Mobile Engagement** portal toomonitor ve mobil uygulamalarınızı yönetin. 

tooget toohello **Hesabımı** sayfasında, hesabınızı hello sayfasının hello üstte tıklayın.

Merhaba UI nerede görüntüleyebilir ve profil ayarlarınızı dahil olmak üzere hesabınızla ilişkili hello ayarlarını değiştirin ve cihaz kimlikleri test olan hello hesabım bölümü. Bu ayarları hello aygıt API da erişilebilir öğeleri içerir.

![MyAccount1][7]  

## <a name="profile"></a>Profili:
Görüntüleyin veya aşağıda gösterilen hesap ayarlarınızı değiştirin. Başka bir kullanıcı izni toouse hello kendi e-posta adresinden göre uygulamanızın verebilirsiniz [giriş](mobile-engagement-user-interface-home.md).

![MyAccount2][8]  

## <a name="devices"></a>Aygıtlar:
Görüntülemek, ekleyebileceğiniz, kaldırmak veya aygıt ID tootest kullanabileceğiniz hello test aygıtların test, **ulaşmak** veya **itme** kampanyalar. Toofind hello cihaz kimliği her platform için aygıtların nasıl bağlamsal yönergeleri (iOS, Android, Windows Phone, vb.), "Yeni aygıt" tıklattığınızda görüntülenir. 

![MyAccount3][9]  

toouse anında API veya aygıt API tooknow kullanıcılarınızın benzersiz cihaz tanımlayıcısı (Merhaba DeviceID parametre) gerekir. Çeşitli yolları tooretrieve vardır:

1. Arka ucunuzdan, hello aygıt API tooget hello tam listesini cihaz tanımlayıcılarını hello "Get" özelliğini kullanabilirsiniz.
2. Uygulamanızdan hello SDK tooget kullanabilirsiniz. (Android, hello Aracısı sınıfı hello getDeviceID() işlevini çağırın ve hello Aracısı sınıfı hello DeviceID özelliği iOS üzerinde oku.)
3. Merhaba duyuru ile ilişkili hello eylem URL'si hello {DeviceID} düzeni içeriyorsa ulaşma duyurudan onu otomatik olarak hello cihazın tanımlayıcısı ile Merhaba eylemi tetikleyen hello tarafından değiştirilecek.
   http://<example>.com/registeruser? DeviceID {DeviceID} = & otherparam = myparamdata tarafından değiştirilecek: http://<example>.com/registeruser? DeviceID XXXXXXXXXXXXXXXX & otherparam = myparamdata = 
4. Merhaba hello duyuru HTML kodunun hello {DeviceID} düzeni içeriyorsa ulaşma web duyurudan onu otomatik olarak hello cihazın tanımlayıcısı ile Merhaba web duyuru görüntüleme hello tarafından değiştirilecek.
   My cihaz tanımlayıcısı şöyledir: {DeviceID} tarafından değiştirilecek: my cihaz tanımlayıcısı şöyledir: XXXXXXXXXXXXXXXX
5. Uygulamanız, Cihazınızda açın ve bir olay hangi etiketlendiği uygulamanızda gerçekleştirin.
   "UI - app - İzleyicisi - olaylarınızı - bilgilerinden" hello hello listesinde gerçekleştirilen olay bulur.
   Merhaba İzleyici toothis olay'ı tıklatın.
   Cihaz Kimliğinizi hello bu olay gerçekleştirmiş hello aygıtlar listesinde bulmanız gerekir.
   Ardından, bu cihaz Kimliğini kopyalayın ve "- yeni cihaz - kullanıcı Arabirimi - Hesabımı - cihazları cihaz platformu seçin" hello kaydedin.
   >(IDFA iOS için devre dışı bırakıldığında, kaldırın ve uygulamanızı yeniden yüklerseniz hello cihaz kimliği hello zaman içinde değişebilir olduğunu unutmayın.)

## <a name="troubleshooting-guide"></a>Sorun giderme kılavuzu
* [Sorun giderme kılavuzu - hizmet][Link 24]

## <a name="see-also"></a>Ayrıca bkz.
* [UI belgeleri - giriş][Link 13]

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




