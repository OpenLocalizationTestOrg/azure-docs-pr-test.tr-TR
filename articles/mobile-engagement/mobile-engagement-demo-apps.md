---
title: "aaaAzure Mobile Engagement tanıtım uygulamasını | Microsoft Docs"
description: "Nerede tanımlar toodownload, nasıl toouse ve Azure Mobile Engagement kullanmanın yararları hello uygulama gösteri"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>Azure Mobile Engagement tanıtım uygulamasını
Bir Azure Mobile Engagement tanıtım uygulamasını için yayımlanan **iOS**, **Android**, ve **Windows** platformları toohelp, toofind kullanışlı kaynaklar ve mobil hakkında daha fazla bilgi edinin Katılım.

Merhaba uygulaması size yardımcı olur:

* Yararlı bağlantılar videoları, belgeleri, hello Destek Forumu gibi tooMobile katılım kaynaklarını kolayca bulmak ve burada toogo tooraise özelliği ister.
* Mobile Engagement tooget fikir mobil uygulamalarınız için tarafından desteklenen deneyimi örnek bildirimler.
* Bir başvuru uygulaması toostudy kullanma tooimplement Mobile Engagement kendi uygulamada. İçin bilgi alabilirsiniz:
  
  * Analytics veri toplar.
  * Uygulama bildirimi senaryolarını türleri gibi gelişmiş *tam ekran Interstitial* veya *açılır*.
  * Anketler ve anketler uygular.
  * Sessiz anında veri ve itme senaryolarında uygulayın.   

## <a name="app-installation"></a>Uygulama yükleme
Bu uygulama, uygulama mağazaları aşağıdaki hello edinilebilir:

* **Windows Evrensel tanıtım uygulamasını**:
  
  * Merhaba Hello uygulamaya karşıdan [Windows uygulama mağazası](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).
  * Merhaba uygulama Windows 10 Universal bir uygulama olarak geliştirilmiştir. Merhaba kaynak kodu edinilebilir [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).
* **iOS uygulama gösteri**:
  
  * Merhaba Hello uygulamaya karşıdan [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).
  * Merhaba uygulama iOS Swift geliştirilmiştir. Merhaba kaynak kodu edinilebilir [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).
* **Android tanıtım uygulamasını**:
  
  * Merhaba Hello uygulamaya karşıdan [Google Play mağazasına](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).
  * Merhaba kaynak kodu edinilebilir [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).

![Windows Evrensel tanıtım uygulamasını][1]

![iOS uygulama gösteri][2]
![Android tanıtım uygulamasını][3]

## <a name="usage"></a>Kullanım
Bu uygulama yolu şu hello kullanabilirsiniz:

**(Daha önce sağlanan) hello uygulama mağazası bağlantıları Cihazınızda Hello uygulamasını yükleyin:**

> [!IMPORTANT]
> Bir Azure hesabı gerekmez veya tooconnect hello uygulama tooa arka uç. Merhaba uygulaması bağımsız olarak çalışır.
> 
> 

* Cihazınızda hello uygulamanız sonra hello sol taraftaki menü toofind hello kullanışlı kaynaklar hakkında Mobile Engagement hello bağlantılar yoluyla gidebilirsiniz.
* Merhaba ekledik [hizmetin RSS akışı](https://aka.ms/azmerssfeed) bu uygulamaya böylece her zaman hello en son ürün güncelleştirmelerini hakkında güncelleştirilmiş.
* Mobile Engagement tarafından desteklenen her platform için bildirimler hello örnek bildirim senaryoları tooexperience hello türü aracılığıyla gidebilirsiniz. Bu bildirimler olabilir deneyimli yerel olarak--diğer bir deyişle, tıklayabilirsiniz hello ekranlar tooshow hello düğmeleri, aynı toosending hello bildirimleri hello Mobile Engagement platformu olan bildirimler deneyimini hello.

![Windows için uygulama menüsü][4]

![İOS için uygulama menüsünden][5]
![Android için uygulama menüsü][6]

**Merhaba kaynak kodu (daha önce sağlanan) GitHub bağlantılarını hello yükleyin:**

* Merhaba kaynak kodu indirdikten sonra hello ilgili geliştirme ortamında--XCode iOS, Android ve Windows için Visual Studio için Android Studio açın.
* Sonraki izlemeniz gereken bizim [Temel SDK tümleştirme adımları](mobile-engagement-windows-store-dotnet-get-started.md) mümkün tooconnect kodlarla bu uygulama tooits kendi Mobile Engagement arka uç örneği.
  * Tooconfigure hello uygulamasında bir bağlantı dizesi gerekir.
  * Ayrıca tooconfigure hello anında iletme bildirimi platform uygulamanız için gerekir.
* Bu hello uygulaması ile Mobile Engagement izlenmiş olan fark edeceksiniz. Toohello arka uç bağlandıktan sonra hello uygulamasını açın, bu nedenle, hello üzerinde mümkün toosee hello kullanıcı oturumunu, etkinlikleri, olayları vb. olması **İzleyici** sekmesi.
* Yerel bildirimler kullanmak yerine kendi Mobile Engagement örneğinden mümkün toosend bildirimleri toothis uygulama de.
  
  * Bir test cihazı hello kullanarak Cihazınızı buraya ekleyebilirsiniz **Get hello cihaz kimliği** hello uygulamasında menü öğesi. Bu platform arka uç örneğinizle ardından bir test cihazı kaydetmek bir cihaz kimliği verir.
    
    ![Windows aygıt kimliği][7]
    
    ![İOS cihaz kimliği][8]
    ![Android cihaz kimliği][9]

## <a name="key-features-of-hello-demo-app"></a>Merhaba tanıtım uygulamasını temel özellikleri
* Bu uygulama ile daha önce belirtildiği gibi tüm hello anahtar kaynaklar, el ile Mobile Engagement için sahiptir. Merhaba soldaki menüden hello bağlantılar aracılığıyla gidebilirsiniz.
* Her platform için uygulama bildirimler yaşayabilirsiniz. Bu bildirimler olarak teslim edilebilir **yalnızca bildirim**, burada hello bildirim tıklatılması yalnızca yerel bir hello uygulama ekran yukarı açar (kullanarak **derin bağlama**)--ya da farklı bir **Web Duyuru**, burada, ek HTML içeriğini Mobile Engagement bitiş hello hello bildirim tıklatıldığında görüntülenen toobe sunabilir.
  
    ![App bildirimler][29]
* İos'ta, tooclose hello uygulama toosee hello uygulama ya da sistem anında iletme bildirimleri sahip. Eklemek için buraya hello uygulama bakabilir **eylem düğmeleri**uygulama bildirim için eklenen toothis olan olanları hello gibi *geri bildirim* ve *paylaşımı* (böylece "Hello kullanıcı hello bildirim kendisini eylem sağdan sürebilir).
  
    ![İOS uygulama bildirimler][11] ![İOS uygulama bildirim görüntüleme][14]
* Android, desteklenen hello seçenekleri çok satırlı metin eklemekte olduğunuz (**büyük metin**) veya bir bildirim görüntüsü (**büyük resmi**) hello birlikte toohello bildirim **eylem düğmeleri** (iOS tarafından desteklenen gibi).
  
    ![Android uygulama bildirimlerini][12] ![Android uygulama bildirim ekranı][15]
* Windows 10'hello bildirimleri PC hello üzerinde nasıl göründüğünü görebilirsiniz. Bu bildirim ayrıca hello Windows 10 görüntülenir **bildirim Merkezi**. Ekleme desteği yoktur **eylem düğmeleri** hello anda hello Windows SDK.
  
    ![Windows uygulama bildirimler][10] ![Windows uygulama görüntüleme][13]
* Her platform için varsayılan "uygulama" bildirimleri yaşayabilirsiniz. Bu iki adımlı bir deneyimdir burada bir **bildirim** penceresi ilk görüntülenir. Tıklattığınızda, bir tam ekran yukarı açılır **duyuru**, ekran aşağıdaki hello görüntülendiği gibi. Bu duyuru Merhaba içeriğine, Mobile Engagement arka uç örneğinden gelir. Merhaba SDK bildirimler ve duyuruları için hello şablon yok. Bunları, hello ayrıca bizim logo ve renklendirme olan bu tanıtım uygulamasını gösterildiği gibi kolaylıkla özelleştirebilirsiniz.  
  
    ![Windows uygulama bildirimleri][16]
  
    ![İOS uygulama bildirimleri][17]  ![Android'daki uygulama bildirimleri][18]
  
    **iOS**, **Android**
* Merhaba de kullanabilirsiniz **kategori** Mobile Engagement toocustomize özelliği bu varsayılan deneyimi. Hello demo uygulamada, biz iki genel yolu toochange hello deneyimi hello bildirimler gösterilen. Merhaba kategori özellik hello Windows SDK henüz desteklenmeyen unutmayın.
  
    **Tam ekran Interstitial:**
  
    ![Uygulama içi bildirim - Interstitial kategorisi][30]
  
    ![İOS Interstitial kategorisi][21]     ![Android'de Interstitial kategorisi][22]
  
    **Açılır bildirimi:**
  
    ![Uygulama içi bildirim - açılır kategorisi][31]
  
    ![İOS açılır bildirim][19]    ![Android açılır bildirimi][20]

**iOS**, **Android**

* Mobile Engagement Ayrıca, uygulama içi bildirim olarak adlandırılan uzmanlaşmış bir türü destekler **yoklamalar**. Bu, hızlı anketler kesimli tooyour uygulama kullanıcılarınızın çıkışı toosend sağlar. Sorular ve ekran aşağıdaki hello olduğu gibi her bir soru için seçenekleri ekleyebilirsiniz. Bu daha sonra bir uygulama içi bildirim toohello uygulama kullanıcısı olarak görüntülenen.   
  
    ![Yoklama bildirimleri][32]
  
    ![Windows'da anket][26]
  
    ![İos'ta anket][27]   ![Android'de anket][28]

**iOS**, **Android**

* Mobile Engagement ayrıca destekler sessiz gönderme **veri gönderme** bildirimleri. Bu bildirimler ile hizmetinizden (gibi hello JSON verileri aşağıdaki örneğine hello), veri gönderebilir uygulamanızda işlemek ve bazı adımları uygulayın. Nasıl biz hello fiyat öğenin seçmeli olarak veri anında iletme bildirimleri kullanarak değiştirirsiniz bir örnektir.
  
    ![Veri anında iletme bildirimi][33]
  
    ![Windows üzerinde veri anında iletme bildirimi][23]
  
    ![İOS veri anında iletme bildirimi][24]  ![Android veri anında iletme bildirimi][25]

**iOS**, **Android**

> [!NOTE]
> Ayrıntılı adım adım yönergeler için bu bildirimler hiçbirini tıklatarak görüntüleyebileceğiniz **hakkında yönergeler için buraya tıklayın toosend Mobile Engagement platformu Bu bildirimler** herhangi örnek bildirim ekranında.
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
