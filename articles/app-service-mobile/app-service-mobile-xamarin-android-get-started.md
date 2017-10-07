---
title: "Xamarin.Android uygulamaları için Azure Mobile Apps ile başlatıldı aaaGet"
description: "Xamarin Android geliştirme için Azure Mobile Apps kullanmaya Bu öğretici tooget izleyin"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Xamarin.Android Uygulaması oluşturma
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooa Xamarin.Android uygulaması gösterir. Daha fazla bilgi için bkz. [Mobile Apps nedir?](app-service-mobile-value-prop.md).

Merhaba tamamlanmış uygulamadan bir ekran görüntüsü aşağıda verilmiştir:

![][0]

Bu öğreticiyi tamamlamak Xamarin Android uygulamalarına ilişkin tüm Mobile Apps öğreticileri için ön koşuldur.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. Bir hesabınız yoksa, bir Azure deneme sürümünü kaydolabilir ve too10 ücretsiz mobil uygulamalar edinebilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Xamarin ile Visual Studio. Yönergeler için bkz. [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx).

## <a name="create-an-azure-mobile-app-backend"></a>Azure Mobil Uygulama arka ucu oluşturma
Bu adımları toocreate bir mobil uygulama arka ucu izleyin.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Artık, mobil istemci uygulamalarınız tarafından kullanılabilecek bir Azure Mobil Uygulama arka ucu sağladınız. Ardından, basit bir "Yapılacaklar listesi" için bir sunucu projesi indirme arka uç ve tooAzure yayımlayın.

## <a name="configure-hello-server-project"></a>Merhaba sunucu projesi yapılandırmak
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>Merhaba Xamarin.Android uygulamasını indirme ve çalıştırma
1. Altında **indirin ve Xamarin.Android projenizi çalıştırma**, hello tıklatın **karşıdan** düğmesi.

      Merhaba sıkıştırılmış proje dosyasını tooyour yerel bilgisayara kaydedin ve kaydettiğiniz yeri not edin.
2. Tuşuna hello **F5** anahtarı toobuild hello proje ve hello uygulamayı başlatın.
3. Merhaba uygulamada gibi anlamlı bir metin yazın *tam hello öğretici* ve hello ardından **Ekle** düğmesi.

    ![][10]

    Veriler hello istek hello Todoıtem tablosuna eklenir. Merhaba tabloda depolanan öğeler hello mobil uygulama arka ucu tarafından döndürülür ve veriler hello listesinde görünür.

   > [!NOTE]
   > Mobil uygulama arka uç tooquery erişen hello kodu gözden geçirin ve hello ToDoActivity.cs C# dosyasına bulunan verileri, ekleyin.
   >
   >

## <a name="next-steps"></a>Sonraki adımlar
* [Çevrimdışı eşitleme tooyour uygulama Ekle](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Kimlik doğrulama tooyour uygulama Ekle](app-service-mobile-xamarin-android-get-started-users.md)
* [Anında iletme bildirimleri tooyour Xamarin.Android uygulaması ekleyin](app-service-mobile-xamarin-android-get-started-push.md)
* [Nasıl toouse hello Azure Mobile Apps için yönetilen](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
