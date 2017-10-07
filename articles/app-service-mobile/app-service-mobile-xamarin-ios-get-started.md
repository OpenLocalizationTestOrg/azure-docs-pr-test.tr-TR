---
title: "aaaGet Xamarin.iOS uygulamaları için Azure App Service Mobile Apps ile başlatılan | Microsoft Docs"
description: "Xamarin.iOS geliştirme için Mobile Apps kullanmaya Bu öğretici tooget izleyin."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Yeni bir Xamarin.iOS uygulaması oluşturma
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooa Xamarin.iOS mobil uygulamasına Azure mobil uygulaması arka ucunu kullanarak gösterir.  Hem yeni bir mobil arka uç hem de Azure’da uygulama verilerini depolayan basit bir *Yapılacaklar listesi* oluşturursunuz.

Bu öğreticiyi tamamlamak Azure App Service'te hello Mobile Apps özelliğini kullanmayla ilgili diğer tüm Xamarin.iOS öğreticileri için önkoşuldur.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. Bir hesabınız yoksa, bir Azure deneme sürümünü kaydolabilir ve deneme bittikten sonra dahi kullanmaya devam edebileceğiniz too10 ücretsiz mobil uygulama alın. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Xamarin ile Visual Studio. Yönergeler için bkz. [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx).
* Xcode v7.0 veya daha sonraki sürümü ve Xamarin Studio Community yüklü bir Mac. Bkz. [Visual Studio ve Xamarin için kurulum ve yükleme](https://msdn.microsoft.com/library/mt613162.aspx) ve [Mac kullanıcıları için kurulum, yükleme ve doğrulamalar](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-an-azure-mobile-app-backend"></a>Azure Mobil Uygulama arka ucu oluşturma
Bu adımları toocreate bir mobil uygulama arka ucu izleyin.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Merhaba sunucu projesi yapılandırmak
Artık, mobil istemci uygulamalarınız tarafından kullanılabilecek bir Azure Mobil Uygulama arka ucu sağladınız. Ardından, basit bir "Yapılacaklar listesi" için bir sunucu projesi indirme arka uç ve tooAzure yayımlayın.

Aşağıdaki adımları tooconfigure hello sunucu projesi toouse hello ya da hello Node.js veya .NET arka uç izleyin.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>Merhaba Xamarin.iOS uygulamasını indirme ve çalıştırma
1. Açık hello [Azure portal] bir tarayıcı penceresinde.
2. Hello ayarları dikey mobil uygulamanızın penceresinde **Get Started** > **Xamarin.iOS**. 3. adımın altında, henüz seçili değilse **Yeni uygulama oluştur**’a tıklayın.  Merhaba İleri'yi **karşıdan** düğmesi.

      Tooyour mobil arka uç bağlanan bir istemci uygulaması indirilir. Merhaba sıkıştırılmış proje dosyasını yerel bilgisayarınıza kaydedin ve kaydettiğiniz yeri not edin.
3. İndirdiğiniz Merhaba projeyi çıkarın ve Xamarin Studio (veya Visual Studio) açın.

    ![][9]

    ![][8]
4. Merhaba F5 anahtar toobuild hello proje tuşuna basın ve hello uygulamayı hello iPhone öykünücüsünde başlatın.
5. Merhaba uygulamada gibi anlamlı bir metin yazın *Xamarin öğren*ve ardından hello  **+**  düğmesi.

    ![][10]

    Veriler hello istek hello Todoıtem tablosuna eklenir. Merhaba tabloda depolanan öğeler hello mobil uygulama arka ucu tarafından döndürülür ve veriler hello listesinde görüntülenir.

> [!NOTE]
> Mobil uygulama arka uç tooquery erişen hello kodu gözden geçirin ve hello QSTodoService.cs C# dosyasına veri eklemek.
>
>

## <a name="next-steps"></a>Sonraki adımlar
* [Çevrimdışı eşitleme tooyour uygulama Ekle](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [Kimlik doğrulama tooyour uygulama Ekle](app-service-mobile-xamarin-ios-get-started-users.md)
* [Anında iletme bildirimleri tooyour Xamarin.Android uygulaması ekleyin](app-service-mobile-xamarin-ios-get-started-push.md)
* [Nasıl toouse hello Azure Mobile Apps için yönetilen](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[Azure portal]: https://portal.azure.com/
