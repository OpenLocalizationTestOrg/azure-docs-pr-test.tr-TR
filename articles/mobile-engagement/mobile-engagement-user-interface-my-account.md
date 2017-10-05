---
title: "Azure Mobile Engagement kullanıcı arabirimi - hesabım"
description: "Azure Mobile Engagement hesabı profili ve test cihazlarınızı yönetmeyi öğrenin"
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
ms.openlocfilehash: 4e463e973dcfa1faa7b08e4738192161980b3aa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-your-account-profile-and-test-devices"></a><span data-ttu-id="12339-103">Hesap profili ve test cihazları yönetme</span><span class="sxs-lookup"><span data-stu-id="12339-103">How to manage your account profile and test devices</span></span>
<span data-ttu-id="12339-104">Bu makalede **giriş** sayfasında **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="12339-104">This article describes the **Home** page of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="12339-105">Kullandığınız **Mobile Engagement** izlemek ve mobil uygulamalarınızı yönetmek için portal.</span><span class="sxs-lookup"><span data-stu-id="12339-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> 

<span data-ttu-id="12339-106">Almak için **Hesabımı** sayfasında, sayfanın üst kısmında, hesabınızı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12339-106">To get to the **my account** page, click on your account on the top of the page.</span></span>

<span data-ttu-id="12339-107">Hesabımı UI nerede görüntüleyebilir ve profil ayarlarınızı dahil olmak üzere hesabınızla ilişkili ayarlarını değiştirin ve cihaz kimlikleri test bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="12339-107">The My Account section of the UI is where you can view and change the settings associated with your account, including your Profile settings and test Device IDs.</span></span> <span data-ttu-id="12339-108">Bu ayarları da aygıt API üzerinden erişilebilen öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="12339-108">These settings contain items that can also be accessed via the Device API.</span></span>

![MyAccount1][7]  

## <a name="profile"></a><span data-ttu-id="12339-110">Profili:</span><span class="sxs-lookup"><span data-stu-id="12339-110">Profile:</span></span>
<span data-ttu-id="12339-111">Görüntüleyin veya aşağıda gösterilen hesap ayarlarınızı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="12339-111">You can view or change any of your account settings shown below.</span></span> <span data-ttu-id="12339-112">Ayrıca kendi e-posta adresinden göre uygulamanızın kullanmak üzere başka bir kullanıcı izni verebilirsiniz [giriş](mobile-engagement-user-interface-home.md).</span><span class="sxs-lookup"><span data-stu-id="12339-112">You can also give another user permission to use your application based on their e-mail address from the [Home](mobile-engagement-user-interface-home.md).</span></span>

![MyAccount2][8]  

## <a name="devices"></a><span data-ttu-id="12339-114">Aygıtlar:</span><span class="sxs-lookup"><span data-stu-id="12339-114">Devices:</span></span>
<span data-ttu-id="12339-115">Görüntülemek, ekleyebileceğiniz, kaldırmak veya test etmek için kullanabileceğiniz test cihazların cihaz ID test, **ulaşmak** veya **itme** kampanyalar.</span><span class="sxs-lookup"><span data-stu-id="12339-115">You can view, add, or remove test Device ID's of the test devices that you can use to test your **reach** or **push** campaigns.</span></span> <span data-ttu-id="12339-116">Her platform için cihazları cihaz Kimliğini bulmak nasıl bağlamsal yönergeler (iOS, Android, Windows Phone, vb.), "Yeni aygıt" tıklattığınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="12339-116">Contextual instructions for how to find the Device ID of devices for each platform (iOS, Android, Windows Phone, etc.) are displayed when you click "New Device".</span></span> 

![MyAccount3][9]  

<span data-ttu-id="12339-118">Anında iletme API'si veya Device API'sini kullanmak için kullanıcılarınızın benzersiz cihaz tanımlayıcısı (DeviceID parametre) bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="12339-118">To use Push API or Device API you need to know your users' unique device identifier (the deviceid parameter).</span></span> <span data-ttu-id="12339-119">Bunu almak için birkaç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="12339-119">There are several ways to retrieve it:</span></span>

1. <span data-ttu-id="12339-120">Arka ucunuzdan, cihaz tanımlayıcılarını tam listesini almak için cihaz API "Get" özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12339-120">From your backend, you can use the "Get" feature of the Device API to get the full list of device identifiers.</span></span>
2. <span data-ttu-id="12339-121">Uygulamanızdan almak için SDK'yı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12339-121">From your app, you can use the SDK to get it.</span></span> <span data-ttu-id="12339-122">(Android, aracı sınıfının ve iOS, getDeviceID() işlevini çağırın Aracısı sınıfın DeviceID özelliği okuyun.)</span><span class="sxs-lookup"><span data-stu-id="12339-122">(On Android, call the getDeviceID() function of the Agent class, and on iOS, read the deviceid property of the Agent class.)</span></span>
3. <span data-ttu-id="12339-123">Duyuru ile ilişkili eylem URL'si {DeviceID} desenini içeriyorsa ulaşma duyurudan, otomatik olarak eylemi tetikleyen cihazın tanımlayıcısı ile değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="12339-123">From a Reach announcement, if the action URL associated with the announcement contains the {deviceid} pattern, it will be automatically replaced by the identifier of the device triggering the action.</span></span>
   <span data-ttu-id="12339-124">http://<example>.com/registeruser? DeviceID {DeviceID} = & otherparam = myparamdata tarafından değiştirilecek: http://<example>.com/registeruser? DeviceID XXXXXXXXXXXXXXXX & otherparam = myparamdata =</span><span class="sxs-lookup"><span data-stu-id="12339-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata will be replaced by: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span></span> 
4. <span data-ttu-id="12339-125">Duyurunun HTML kodu {DeviceID} desenini içeriyorsa ulaşma web duyurudan onu otomatik olarak web duyuruyu görüntüleyen cihazın tanımlayıcısı ile değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="12339-125">From a Reach web announcement, if the HTML code of the announcement contains the {deviceid} pattern, it will be automatically replaced by the identifier of the device displaying the web announcement.</span></span>
   <span data-ttu-id="12339-126">My cihaz tanımlayıcısı şöyledir: {DeviceID} tarafından değiştirilecek: my cihaz tanımlayıcısı şöyledir: XXXXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="12339-126">Here is my device identifier: {deviceid} will be replaced by: Here is my device identifier: XXXXXXXXXXXXXXXX</span></span>
5. <span data-ttu-id="12339-127">Uygulamanız, Cihazınızda açın ve bir olay hangi etiketlendiği uygulamanızda gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="12339-127">Open your application on your device and perform an Event in your app which has been tagged.</span></span>
   <span data-ttu-id="12339-128">"UI - app - İzleyicisi - olaylarınızı - Ayrıntılar" listesinde gerçekleştirilen olayı bulun.</span><span class="sxs-lookup"><span data-stu-id="12339-128">From "UI - your app - Monitor - Events - Details", find the Event you performed in the list.</span></span>
   <span data-ttu-id="12339-129">Bu olay İzleyicisi'nde için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="12339-129">Click to this event in the Monitor.</span></span>
   <span data-ttu-id="12339-130">Bu olay gerçekleştirmiş aygıtlar listesinde cihaz Kimliğinizi bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="12339-130">You should find your Device ID in the list of the devices that have performed this event.</span></span>
   <span data-ttu-id="12339-131">Ardından, bu cihaz Kimliğini kopyalayın ve "- yeni cihaz - kullanıcı Arabirimi - Hesabımı - cihazları seçin, cihaz platformu" kaydedin.</span><span class="sxs-lookup"><span data-stu-id="12339-131">Then, you can copy this Device ID and register it in the "UI - My Account - Devices - New Device - Select your device platform".</span></span>
   ><span data-ttu-id="12339-132">(IDFA iOS için devre dışı bırakıldığında, uygulamanızı kaldırıp, cihaz kimliği zaman içinde değişebilir olduğunu unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="12339-132">(Be aware that when IDFA is disabled for iOS, the Device ID may change over the time if you uninstall and reinstall your app.)</span></span>

## <a name="troubleshooting-guide"></a><span data-ttu-id="12339-133">Sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="12339-133">Troubleshooting Guide</span></span>
* <span data-ttu-id="12339-134">[Sorun giderme kılavuzu - hizmet][Link 24]</span><span class="sxs-lookup"><span data-stu-id="12339-134">[Troubleshooting Guide - Service][Link 24]</span></span>

## <a name="see-also"></a><span data-ttu-id="12339-135">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="12339-135">See also</span></span>
* <span data-ttu-id="12339-136">[UI belgeleri - giriş][Link 13]</span><span class="sxs-lookup"><span data-stu-id="12339-136">[UI Documentation - Home][Link 13]</span></span>

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




