---
title: "Herhangi bir aygıttan uygulamalarınıza erişme | Microsoft Docs"
description: "Hangi istemcilerin Azure RemoteApp için desteklenir ve uygulamalarınıza erişmek nasıl öğrenin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 10a5be6251765b59fac92a33120cedcf8091a677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a>Azure RemoteApp içindeki uygulamalarınıza erişim
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp beauties herhangi aygıtlarınızın uygulamaları erişebilir biridir. Bile daha iyi bir cihazda çalışmaya başlamak ve ikinci bir cihaz sorunsuz geçiş ve kullanabilirsiniz kaldığınız yerden yukarı sola çekme. Başlamak için cihazınız için uygun istemci yükleme ve hizmete oturum açmak gerekir.

Bu konuda, sizi şu anda desteklenen istemciler ve ı RemoteApp her istemcilerin oturum açma göstermeden önce bunları indirmek nasıl gözden geçirin.

## <a name="supported-clients"></a>Desteklenen istemciler
RemoteApp Cihazınızı bu işletim sistemlerinden birini çalıştıran, aşağıdaki adımları kullanarak erişebilirsiniz:

* Windows 10 
* Windows 8.1
* Windows 8
* Windows 7 Service Pack 1
* Windows Phone 8.1
* iOS
* Mac OS X
* Android

 Küçük boyutlu istemciler hakkında neler? Aşağıdaki Windows Embedded ince istemciler desteklenir:

* Windows Embedded Standard 7
* Windows Embedded 8 Standard
* Windows Embedded 8.1 Industry Pro
* Windows 10 IoT Enterprise

## <a name="downloading-the-client"></a>İstemci Yükleme
Kullanmakta olduğunuz hangi platformu olsun RemoteApp erişmek için gereken istemci bulunabilir [Uzak Masaüstü İstemcisi indirme](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) sayfası.

Farklı bağlantıları tıklatarak ya da doğrudan istemci indirme başlatılacak veya sayfa, platform için uygulama mağazasında bulunan istemciye indirdiğiniz gönderir. Ekrandaki yönergeleri izleyerek istemciyi yükleyin.

İstemci aygıtınızda yüklü ve bu başlatıldıktan sonra Bu istemciden RemoteApp oturum açmak öğrenmek için aşağıdaki ilgili bölümüne geçin.

## <a name="android"></a>Android
Google Play Mağazası'ndan Microsoft Uzak Masaüstü uygulamasını yükledikten sonra bu uygulama listenizde altında bulabilirsiniz **Uzak Masaüstü**.

1. Zaten uygulamayı kullanmakta olduğunuz sürece uygulamasını başlatarak boş bir bağlantı merkezine getirir. Azure RemoteApp ile çalışmaya başlamak için Ekle düğmesine dokunun **"" +""** ve dokunun **Azure RemoteApp**.    
   
     ![Boş bağlantı Merkezi](./media/remoteapp-clients/Android1.png)
2. Hizmete erişmek için e-posta adresinizi oturum oturum açmanız gerekir. Dokunun **başlama**.
   
    ![Komut isteminde oturum](./media/remoteapp-clients/Android2.png)
3. Sonraki sayfada yazın, **e-posta adresi** ve dokunun **devam**. Bu, Azure Active Directory'yi kullanarak oturum açma işlemi başlar.
   
    ![İlk Azure Active Directory sayfası](./media/remoteapp-clients/Android3.png)
4. Microsoft hesabı (daha önce "LiveID" denir) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan. Varsa, güven ve dokunun davetleri seçin **Bitti**.    
   
    ![Davetiye sayfası](./media/remoteapp-clients/Android4.png)
5. Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale. Bir uygulama, kullanmaya başlamak için dokunun.
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/Android5.png)
6. Davetiye henüz yoksa servisi hala deneyebilirsiniz. Bunu yapmak için dokunun **ücretsiz deneme sürümü için Git** istendiğinde.
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/Android6.png)
7. Bu, RemoteApp ile başlamanıza yardımcı olmak için uygulamaların temel bir dizi erişmenizi sağlar.
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a>iOS
Uygulama Mağazası'ndan Microsoft Uzak Masaüstü uygulamasını yükledikten sonra bu uygulama listenizde altında bulabilirsiniz **RD istemcisini**.

1. Zaten uygulamayı kullanmakta olduğunuz sürece uygulamasını başlatarak boş bir bağlantı merkezine getirir. Azure RemoteApp ile çalışmaya başlamak için Ekle düğmesine dokunun **"" +""** ve dokunun **eklemek Azure RemoteApp**.
   
    ![Boş bağlantı Merkezi](./media/remoteapp-clients/IOS1.png)
2. Bu işlemi başlatmak için hizmete erişmek için e-posta adresinizi oturum imzalamak için yazmanız, **e-posta adresi** ve dokunun **devam**.
   
    ![Komut isteminde oturum](./media/remoteapp-clients/picture1.png)
3. Microsoft hesabı (LiveId) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan. Varsa, güven ve dokunun davetleri seçin **Bitti**.
   
    ![Davetiye sayfası](./media/remoteapp-clients/IOS3.png)
4. Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale. Bir uygulama başlatın ve kullanmaya başlamak için dokunun.
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/IOS4.png)
5. Davetiye henüz yoksa servisi hala deneyebilirsiniz. Bunu yapmak için dokunun **ücretsiz deneme sürümü için Git** istendiğinde.
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/IOS5.png)
6. Bu, RemoteApp ile başlamanıza yardımcı olmak için uygulamaların temel bir dizi erişmenizi sağlar.
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a>Mac OS X
Uygulama Mağazası'ndan Microsoft Uzak Masaüstü uygulamasını yükledikten sonra bu uygulama listenizde altında bulabilirsiniz **Microsoft Uzak Masaüstü**.

1. Zaten uygulamayı kullanmakta olduğunuz sürece uygulamasını başlatarak boş bir bağlantı merkezine getirir. Azure RemoteApp ile kullanmaya başlamak için tıklayın **Azure RemoteApp** düğmesi.
   
    ![Boş bağlantı Merkezi](./media/remoteapp-clients/Mac1.png)
2. Bu işlemi başlatmak için hizmete erişmek için e-posta adresinizi oturum imzalamak için dokunun **Get Started**.
   
    ![Komut isteminde oturum](./media/remoteapp-clients/Mac2.png)
3. Sonraki sayfada yazın, **e-posta adresi** ve dokunun **devam**. Bu oturum açma Azure Active Directory'yi kullanarak işlemine başlar.
   
    ![İlk Azure Active Directory sayfası](./media/remoteapp-clients/picture2.png)
4. Microsoft hesabı (LiveId) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan. Varsa, güven ve iletişim kutusunu kapatın davetleri seçin.
   
    ![Davetiye sayfası](./media/remoteapp-clients/Mac4.png)
5. Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale. Bir uygulama başlatın ve kullanmaya başlamak için çift tıklayın.
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/Mac5.png)
6. Davetiye henüz yoksa servisi hala deneyebilirsiniz. Bunu yapmak için tıklatın **ücretsiz deneme sürümü için Git** istendiğinde.
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/Mac6.png)
7. Bu, RemoteApp ile başlamanıza yardımcı olmak için uygulamaların temel bir dizi erişmenizi sağlar.
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a>Windows (Windows Phone hariç desteklenen tüm sürümleri)
Yükleme, erişim gerektiğinde ancak daha sonra yeniden şu adla uygulama listenizde bulunabilir bittikten sonra istemci otomatik olarak başlatır **Azure RemoteApp**.

1. İstemci, gördüğünüz ilk sayfa başlatma onra Azure RemoteApp beklemektedir. Devam etmek için tıklayın **Get Started**.
   
    ![Azure RemoteApp istemcisi Karşılama sayfası](./media/remoteapp-clients/Windows1.png)
2. Sonraki sayfada, Azure Active Directory'yi kullanarak Azure RemoteApp için işleminde oturum başlatır. Bu işlem Microsoft Hizmetleri geçmişte kullandıysanız, tanıdık gelecektir. Başlangıç yazarak, **e-posta adresi** tıklatıp **devam**.
   
    ![İlk Azure Active Directory istemi](./media/remoteapp-clients/Windows2.png)
3. Microsoft hesabı (LiveId) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan. Varsa, güven ve tıklayın davetleri seçin **Bitti**.
   
    ![Azure RemoteApp istemci davetleri sayfası](./media/remoteapp-clients/Windows3.png)
4. Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale. Bir uygulama başlatın ve kullanmaya başlamak için çift tıklayın.
   
    ![Azure RemoteApp istemcinin bağlantı Merkezi](./media/remoteapp-clients/Windows4.png)
5. Hiç kimse, henüz bir davet göndermişse, endişelenmeyin biz, kapsamdaki var! Dolayısıyla servisi test yine demo koleksiyona erişimi gerekir.
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a>Windows Phone 8.1
Windows Phone 8.1 Mağaza'dan Microsoft Uzak Masaüstü uygulamasını yükledikten sonra bu uygulama listenizde altında bulabilirsiniz **Uzak Masaüstü**.

1. Zaten uygulamayı kullanmakta olduğunuz sürece uygulamasını başlatarak doğrudan bir boş bağlantı merkezine getirir. Azure RemoteApp ile çalışmaya başlamak için Ekle düğmesine dokunun **"" +""** ekranın altındaki.
   
    ![Boş bağlantı Merkezi](./media/remoteapp-clients/WinPhone1.png)
2. Ardından, seçeneğine dokunun **Azure RemoteApp**.
   
    ![Öğe bir sayfa ekleyin](./media/remoteapp-clients/WinPhone2.png)
3. Bu işlemi başlatmak için hizmete erişmek için e-posta adresinizi oturum imzalamak için dokunun **bağlanmak**.
   
    ![Komut isteminde oturum](./media/remoteapp-clients/WinPhone3.png)
4. Sonraki sayfada yazın, **e-posta adresi** ve dokunun **devam**. Bu oturum açma Azure Active Directory'yi kullanarak işlemine başlar.
   
    ![İlk Azure Active Directory sayfası](./media/remoteapp-clients/WinPhone4.png)
5. Microsoft hesabı (LiveId) veya kuruluş kimliği oturum açmanız için ekrandaki yönergeleri izleyin Oturum açtıktan sonra aldığınız tüm davetleri listelendiği bir sayfa ile sunulan. Varsa, güven ve dokunun davetleri seçin **kaydetmek**.
   
    ![Davetiye sayfası](./media/remoteapp-clients/WinPhone5.png)
6. Davetleri kabul ettikten sonra erişiminiz uygulamalar listesini, cihaza indirilip ve olması bağlantı Merkezi'nde kullanılabilir hale. Bir uygulama başlatın ve kullanmaya başlamak için dokunun.
   
    ![Bir akış ile bağlantı Merkezi](./media/remoteapp-clients/WinPhone6.png)
7. Davetiye henüz yoksa servisi hala deneyebilirsiniz. Bunu yapmak için dokunun **Evet** istendiğinde.
   
    ![Komut isteminde akış Tanıtımı](./media/remoteapp-clients/WinPhone7.png)
8. Bu, RemoteApp ile başlamanıza yardımcı olmak için uygulamaların temel bir dizi erişmenizi sağlar.
   
    ![Azure RemoteApp için akış Tanıtımı](./media/remoteapp-clients/WinPhone8.png)

