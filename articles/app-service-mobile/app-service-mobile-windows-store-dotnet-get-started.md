---
title: aaaCreate Mobile Apps kullanan bir evrensel Windows Platformu (UWP) | Microsoft Docs
description: "C#, Visual Basic ya da JavaScript'te Evrensel Windows Platformu (UWP) uygulaması geliştirme için Azure mobil uygulaması arka uçlarını kullanmaya ile Bu öğretici tooget izleyin."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a>Windows uygulaması oluşturma
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooa Evrensel Windows Platformu (UWP) uygulamasını gösterir. Daha fazla bilgi için bkz. [Mobile Apps nedir?](app-service-mobile-value-prop.md). Merhaba ekran tamamlandı hello uygulamadan yakalar şunlardır:

![Tamamlanmış masaüstü uygulaması](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
Masaüstünde çalışma.

![Tamamlanmış. telefon uygulaması](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
Telefonda çalışma

Bu öğreticiyi tamamlamak UWP uygulamalarına ilişkin tüm Mobil Uygulama öğreticileri için ön koşuldur.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. Bir hesabınız yoksa, bir Azure deneme sürümünü kaydolabilir ve deneme bittikten sonra dahi kullanmaya devam edebileceğiniz too10 ücretsiz mobil uygulama alın. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio Community 2015] ya da daha yeni sürümü.

## <a name="create-a-new-azure-mobile-app-backend"></a>Yeni bir Azure Mobil Uygulama arka ucu oluşturma
Bu adımları toocreate yeni bir mobil uygulama arka ucu izleyin.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Artık, mobil istemci uygulamalarınız tarafından kullanılabilecek bir Azure Mobil Uygulama arka ucu sağladınız. Ardından, basit bir "Yapılacaklar listesi" için bir sunucu projesi yükleyecek arka uç ve tooAzure yayımlayın.

## <a name="configure-hello-server-project"></a>Merhaba sunucu projesi yapılandırmak
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a>Karşıdan yükleme ve hello istemci projesi çalıştırma
Mobil uygulama arka ucunuzu yapılandırdıktan sonra yeni bir istemci uygulaması oluşturabilir veya var olan bir uygulama tooconnect tooAzure değiştirin. Bu bölümde, özelleştirilmiş tooconnect tooyour mobil uygulama arka ucu olan bir UWP uygulaması şablonu projesi indirirsiniz.

1. Hello edilene **Hızlı Başlangıç** , mobil uygulama arka ucu için dikey tıklayın **yeni uygulama oluştur** > **karşıdan**, hello sıkıştırılmış proje dosyalarını ayıklayın tooyour yerel bilgisayar.

    ![Windows hızlı başlangıç projesi indirme](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. (İsteğe bağlı) Merhaba UWP uygulaması projesi toohello eklemek hello sunucu projesi olarak aynı çözüme. Bu, daha kolay toodebug ve her ikisi de uygulama ve hello arka uç hello test kılar toodo Bunu seçerseniz, aynı Visual Studio çözümü hello. bir UWP uygulaması projesi toohello çözüm tooadd, Visual Studio 2015 veya sonraki bir sürümünü kullanıyor olmanız gerekir.
3. Merhaba başlangıç projesi olarak Hello UWP uygulaması ile hello F5 anahtar toodeploy ve çalışma hello uygulama basın.
4. Merhaba uygulamada gibi anlamlı bir metin yazın *tam hello öğretici*, hello içinde **Todoıtem Ekle** metin kutusuna ve ardından **kaydetmek**.

    ![Windows hızlı başlangıç tamamlanmış masaüstü](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    Bu, Azure'da barındırılan bir POST isteği toohello yeni mobil uygulama arka ucu gönderir.
5. (İsteğe bağlı) Merhaba uygulamayı durdurun ve farklı cihaz veya mobil öykünücü üzerinde yeniden başlatın.

    ![Windows hızlı başlangıç tamamlanmış telefon](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    Merhaba önceki adımda kaydedilen verilerin Hello UWP uygulaması başladıktan sonra Azure'dan yüklenip yüklenmediğine dikkat edin.

## <a name="next-steps"></a>Sonraki adımlar
* [Kimlik doğrulama tooyour uygulama Ekle](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Bilgi nasıl bir kimlik sağlayıcısı ile uygulamanızın tooauthenticate kullanıcılar.
* [Anında iletme bildirimleri tooyour uygulama Ekle](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Mobil uygulama arka uç toouse Azure Notification Hubs toosend anında iletme bildirimleri yapılandırmak ve tooadd anında iletme bildirimleri tooyour uygulama'ı nasıl desteklediğini öğrenin.
* [Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Bir mobil uygulama arka ucu kullanarak uygulamanıza çevrimdışı tooadd destek nasıl bilgi edinin. Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
