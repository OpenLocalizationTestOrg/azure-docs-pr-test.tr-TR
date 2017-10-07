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
# <a name="how-toomanage-your-account-profile-and-test-devices"></a><span data-ttu-id="91c44-103">Nasıl toomanage hesap profili ve test cihazları</span><span class="sxs-lookup"><span data-stu-id="91c44-103">How toomanage your account profile and test devices</span></span>
<span data-ttu-id="91c44-104">Bu makalede hello **giriş** hello sayfasının **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="91c44-104">This article describes hello **Home** page of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="91c44-105">Merhaba kullandığınız **Mobile Engagement** portal toomonitor ve mobil uygulamalarınızı yönetin.</span><span class="sxs-lookup"><span data-stu-id="91c44-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> 

<span data-ttu-id="91c44-106">tooget toohello **Hesabımı** sayfasında, hesabınızı hello sayfasının hello üstte tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91c44-106">tooget toohello **my account** page, click on your account on hello top of hello page.</span></span>

<span data-ttu-id="91c44-107">Merhaba UI nerede görüntüleyebilir ve profil ayarlarınızı dahil olmak üzere hesabınızla ilişkili hello ayarlarını değiştirin ve cihaz kimlikleri test olan hello hesabım bölümü.</span><span class="sxs-lookup"><span data-stu-id="91c44-107">hello My Account section of hello UI is where you can view and change hello settings associated with your account, including your Profile settings and test Device IDs.</span></span> <span data-ttu-id="91c44-108">Bu ayarları hello aygıt API da erişilebilir öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="91c44-108">These settings contain items that can also be accessed via hello Device API.</span></span>

![MyAccount1][7]  

## <a name="profile"></a><span data-ttu-id="91c44-110">Profili:</span><span class="sxs-lookup"><span data-stu-id="91c44-110">Profile:</span></span>
<span data-ttu-id="91c44-111">Görüntüleyin veya aşağıda gösterilen hesap ayarlarınızı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="91c44-111">You can view or change any of your account settings shown below.</span></span> <span data-ttu-id="91c44-112">Başka bir kullanıcı izni toouse hello kendi e-posta adresinden göre uygulamanızın verebilirsiniz [giriş](mobile-engagement-user-interface-home.md).</span><span class="sxs-lookup"><span data-stu-id="91c44-112">You can also give another user permission toouse your application based on their e-mail address from hello [Home](mobile-engagement-user-interface-home.md).</span></span>

![MyAccount2][8]  

## <a name="devices"></a><span data-ttu-id="91c44-114">Aygıtlar:</span><span class="sxs-lookup"><span data-stu-id="91c44-114">Devices:</span></span>
<span data-ttu-id="91c44-115">Görüntülemek, ekleyebileceğiniz, kaldırmak veya aygıt ID tootest kullanabileceğiniz hello test aygıtların test, **ulaşmak** veya **itme** kampanyalar.</span><span class="sxs-lookup"><span data-stu-id="91c44-115">You can view, add, or remove test Device ID's of hello test devices that you can use tootest your **reach** or **push** campaigns.</span></span> <span data-ttu-id="91c44-116">Toofind hello cihaz kimliği her platform için aygıtların nasıl bağlamsal yönergeleri (iOS, Android, Windows Phone, vb.), "Yeni aygıt" tıklattığınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="91c44-116">Contextual instructions for how toofind hello Device ID of devices for each platform (iOS, Android, Windows Phone, etc.) are displayed when you click "New Device".</span></span> 

![MyAccount3][9]  

<span data-ttu-id="91c44-118">toouse anında API veya aygıt API tooknow kullanıcılarınızın benzersiz cihaz tanımlayıcısı (Merhaba DeviceID parametre) gerekir.</span><span class="sxs-lookup"><span data-stu-id="91c44-118">toouse Push API or Device API you need tooknow your users' unique device identifier (hello deviceid parameter).</span></span> <span data-ttu-id="91c44-119">Çeşitli yolları tooretrieve vardır:</span><span class="sxs-lookup"><span data-stu-id="91c44-119">There are several ways tooretrieve it:</span></span>

1. <span data-ttu-id="91c44-120">Arka ucunuzdan, hello aygıt API tooget hello tam listesini cihaz tanımlayıcılarını hello "Get" özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91c44-120">From your backend, you can use hello "Get" feature of hello Device API tooget hello full list of device identifiers.</span></span>
2. <span data-ttu-id="91c44-121">Uygulamanızdan hello SDK tooget kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91c44-121">From your app, you can use hello SDK tooget it.</span></span> <span data-ttu-id="91c44-122">(Android, hello Aracısı sınıfı hello getDeviceID() işlevini çağırın ve hello Aracısı sınıfı hello DeviceID özelliği iOS üzerinde oku.)</span><span class="sxs-lookup"><span data-stu-id="91c44-122">(On Android, call hello getDeviceID() function of hello Agent class, and on iOS, read hello deviceid property of hello Agent class.)</span></span>
3. <span data-ttu-id="91c44-123">Merhaba duyuru ile ilişkili hello eylem URL'si hello {DeviceID} düzeni içeriyorsa ulaşma duyurudan onu otomatik olarak hello cihazın tanımlayıcısı ile Merhaba eylemi tetikleyen hello tarafından değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="91c44-123">From a Reach announcement, if hello action URL associated with hello announcement contains hello {deviceid} pattern, it will be automatically replaced by hello identifier of hello device triggering hello action.</span></span>
   <span data-ttu-id="91c44-124">http://<example>.com/registeruser? DeviceID {DeviceID} = & otherparam = myparamdata tarafından değiştirilecek: http://<example>.com/registeruser? DeviceID XXXXXXXXXXXXXXXX & otherparam = myparamdata =</span><span class="sxs-lookup"><span data-stu-id="91c44-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata will be replaced by: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span></span> 
4. <span data-ttu-id="91c44-125">Merhaba hello duyuru HTML kodunun hello {DeviceID} düzeni içeriyorsa ulaşma web duyurudan onu otomatik olarak hello cihazın tanımlayıcısı ile Merhaba web duyuru görüntüleme hello tarafından değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="91c44-125">From a Reach web announcement, if hello HTML code of hello announcement contains hello {deviceid} pattern, it will be automatically replaced by hello identifier of hello device displaying hello web announcement.</span></span>
   <span data-ttu-id="91c44-126">My cihaz tanımlayıcısı şöyledir: {DeviceID} tarafından değiştirilecek: my cihaz tanımlayıcısı şöyledir: XXXXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="91c44-126">Here is my device identifier: {deviceid} will be replaced by: Here is my device identifier: XXXXXXXXXXXXXXXX</span></span>
5. <span data-ttu-id="91c44-127">Uygulamanız, Cihazınızda açın ve bir olay hangi etiketlendiği uygulamanızda gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="91c44-127">Open your application on your device and perform an Event in your app which has been tagged.</span></span>
   <span data-ttu-id="91c44-128">"UI - app - İzleyicisi - olaylarınızı - bilgilerinden" hello hello listesinde gerçekleştirilen olay bulur.</span><span class="sxs-lookup"><span data-stu-id="91c44-128">From "UI - your app - Monitor - Events - Details", find hello Event you performed in hello list.</span></span>
   <span data-ttu-id="91c44-129">Merhaba İzleyici toothis olay'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="91c44-129">Click toothis event in hello Monitor.</span></span>
   <span data-ttu-id="91c44-130">Cihaz Kimliğinizi hello bu olay gerçekleştirmiş hello aygıtlar listesinde bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="91c44-130">You should find your Device ID in hello list of hello devices that have performed this event.</span></span>
   <span data-ttu-id="91c44-131">Ardından, bu cihaz Kimliğini kopyalayın ve "- yeni cihaz - kullanıcı Arabirimi - Hesabımı - cihazları cihaz platformu seçin" hello kaydedin.</span><span class="sxs-lookup"><span data-stu-id="91c44-131">Then, you can copy this Device ID and register it in hello "UI - My Account - Devices - New Device - Select your device platform".</span></span>
   ><span data-ttu-id="91c44-132">(IDFA iOS için devre dışı bırakıldığında, kaldırın ve uygulamanızı yeniden yüklerseniz hello cihaz kimliği hello zaman içinde değişebilir olduğunu unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="91c44-132">(Be aware that when IDFA is disabled for iOS, hello Device ID may change over hello time if you uninstall and reinstall your app.)</span></span>

## <a name="troubleshooting-guide"></a><span data-ttu-id="91c44-133">Sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="91c44-133">Troubleshooting Guide</span></span>
* <span data-ttu-id="91c44-134">[Sorun giderme kılavuzu - hizmet][Link 24]</span><span class="sxs-lookup"><span data-stu-id="91c44-134">[Troubleshooting Guide - Service][Link 24]</span></span>

## <a name="see-also"></a><span data-ttu-id="91c44-135">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="91c44-135">See also</span></span>
* <span data-ttu-id="91c44-136">[UI belgeleri - giriş][Link 13]</span><span class="sxs-lookup"><span data-stu-id="91c44-136">[UI Documentation - Home][Link 13]</span></span>

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




