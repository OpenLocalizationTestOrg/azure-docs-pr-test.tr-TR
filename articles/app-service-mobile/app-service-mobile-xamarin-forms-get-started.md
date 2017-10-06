---
title: "Xamarin.Forms kullanarak aaaGet Mobile Apps ile başlatıldı"
description: "Xamarin.Forms geliştirme için Mobile Apps'ı kullanarak Bu öğretici toostart izleyin"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>Xamarin.Forms uygulaması oluşturma
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl tooadd kullanarak bulut tabanlı arka uç hizmeti tooa Xamarin.Forms mobil uygulaması hello hello arka ucu olarak Azure App Service Mobile Apps özelliğini gösterir. Yeni bir Mobil Uygulama arka ucu ve uygulama verilerini Azure’da depolayan basit bir yapılacaklar listesi Xamarin.Forms uygulaması oluşturacaksınız.

Bu öğreticiyi tamamlamak Xamarin.Forms uygulamalarına ilişkin tüm Mobile Apps öğreticileri için ön koşuldur.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. Bir hesabınız yoksa, bir Azure deneme sürümünü kaydolabilir ve deneme bittikten sonra dahi kullanmaya devam edebileceğiniz too10 ücretsiz mobil uygulama alın. Daha fazla bilgi için bkz. [Azure Ücretsiz Denemesi](https://azure.microsoft.com/pricing/free-trial/).

* Xamarin ile Visual Studio. Merhaba bilgi için bkz [ayarlamak ayarlama ve Visual Studio ve Xamarin yükleme](https://msdn.microsoft.com/library/mt613162.aspx) sayfası.

* Xcode v7.0 veya daha sonraki sürümü ve Xamarin Studio Community yüklü bir Mac. Bilgi için bkz. [Visual Studio ve Xamarin’i ayarlama ve yükleme](https://msdn.microsoft.com/library/mt613162.aspx) ve [Mac kullanıcıları için kurulum, yükleme ve doğrulamalar](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-a-new-mobile-apps-back-end"></a>Yeni bir Mobile Apps arka ucu oluşturma

geri yeni bir Mobile Apps end, toocreate hello aşağıdaki:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Şimdi mobil istemci uygulamalarınızın kullanabileceği bir Mobile Apps arka ucu ayarlamış oldunuz. Ardından, bir basit bir Yapılacaklar listesi arka ucu için bir sunucu projesi indirin ve tooAzure yayımlayın.

## <a name="configure-hello-server-project"></a>Merhaba sunucu projesi yapılandırmak

tooconfigure hello sunucu projesi toouse Node.js veya .NET arka ucu Merhaba, aşağıdaki hello:

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>Karşıdan yükleme ve başlangıç Xamarin.Forms çözümünü çalıştırma

İki yoldan biriyle hello çözümde indirebilirsiniz. Tooa Mac indirin ve Xamarin Studio'da açın veya tooa Windows bilgisayarı yükleyebilir ve ağa bağlı bir Mac kullanarak hello iOS uygulaması oluşturmak için Visual Studio'da açın. Daha fazla bilgi için [Visual Studio ve Xamarin’i ayarlama ve yükleme](https://msdn.microsoft.com/library/mt613162.aspx) sayfasına bakın.

Mac veya Windows bilgisayarda, aşağıdaki hello:

1. Toohello Git [Azure portal].

2. Merhaba üzerinde **ayarları** mobil uygulamanızın dikey altında **mobil**seçin **Get Started** > **Xamarin.Forms**. **3. adım** altında **Yeni uygulama oluştur**’u ve ardından **İndir**’i seçin.

   Bu eylem bağlı tooyour mobil uygulama olan istemci uygulaması içeren bir projeyi indirir. Merhaba sıkıştırılmış proje dosyasını tooyour yerel bilgisayara kaydedin ve kaydettiğiniz yeri not edin.

3. İndirdiğiniz Merhaba projeyi çıkarın ve Xamarin Studio (Mac) veya Visual Studio'da (Windows) açın.

   ![Xamarin Studio'da ayıklanan proje][9]

   ![Visual Studio'da ayıklanan proje][8]

## <a name="optional-run-hello-ios-project"></a>(İsteğe bağlı) Merhaba iOS projesi çalıştırma
Bu bölümde, iOS cihazları için hello Xamarin iOS projesi çalıştırın. iOS cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.

#### <a name="in-xamarin-studio"></a>Xamarin Studio’da
1. Merhaba iOS projesine sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.

2. Merhaba üzerinde **çalıştırmak** menüsünde, select **hata ayıklamayı Başlat** toobuild hello proje ve hello uygulamayı hello iPhone öykünücüsünde başlatın.

#### <a name="in-visual-studio"></a>Visual Studio’da
1. Merhaba iOS projesine sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.

2. Merhaba üzerinde **yapı** menüsünde, select **Configuration Manager**.

3. Merhaba, **Configuration Manager** iletişim kutusu, select hello **yapı** ve **dağıtma** onay kutularını sonraki toohello iOS projesi.

4. toobuild hello proje ve hello uygulamayı hello iPhone öykünücüsünde, select hello başlatın **F5** anahtarı.

   > [!NOTE]
   > Başlangıç projesi oluşturma sorunları varsa hello NuGet Paket Yöneticisi ve güncelleştirme toohello en son sürümünü hello Xamarin destek paketlerinin çalıştırın. Hızlı Başlangıç projeleri yavaş tooupdate toohello en son sürümleri olabilir.    
   >
   >

5. Merhaba uygulamada gibi anlamlı bir metin yazın *Xamarin öğren*, ve ardından artı işaretini seçin hello (**+**).

    ![][10]

    Bu eylem, yeni mobil uygulama arka Azure üzerinde barındırılan uç bir post isteği toohello gönderir. Veriler hello istek hello Todoıtem tablosuna eklenir. Hello tabloda depolanan öğeler veri hello listesinde görüntülenen Mobile Apps sonlandırmak ve hello hello tarafından döndürülür.

    > [!NOTE]
    > Mobile Apps arka uç hello Todoıtemmanager.cs C# çözümünüzün hello taşınabilir sınıf kitaplığı proje dosyası içinde erişen hello kodu bulacaksınız.
    >
    >

## <a name="optional-run-hello-android-project"></a>(İsteğe bağlı) Merhaba Android projesi çalıştırma
Bu bölümde, hello Xamarin Android projesi Android için çalıştırın. Android cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.

#### <a name="in-xamarin-studio"></a>Xamarin Studio’da

1. Merhaba Android projesine sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.

2. toobuild hello proje ve hello uygulama hello bir Android öykünücüsünde başlatın **çalıştırmak** menüsünde, select **hata ayıklamayı Başlat**.

#### <a name="in-visual-studio"></a>Visual Studio’da

1. Merhaba Android (Droid) projesine sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.

2. Merhaba üzerinde **yapı** menüsünde, select **Configuration Manager**.

3. Merhaba, **Configuration Manager** iletişim kutusu, select hello **yapı** ve **dağıtma** onay kutularını sonraki toohello Android projesi.

4. toobuild hello proje ve hello uygulamayı Android öykünücüsünde, select hello başlatın **F5** anahtarı.

   > [!NOTE]
   > Başlangıç projesi oluşturma sorunları varsa hello NuGet Paket Yöneticisi ve güncelleştirme toohello en son sürümünü hello Xamarin destek paketlerinin çalıştırın. Hızlı Başlangıç projeleri yavaş tooupdate toohello en son sürümleri olabilir.    
   >
   >

5. Merhaba uygulamada gibi anlamlı bir metin yazın *Xamarin öğren*, ve ardından artı işaretini seçin hello (**+**).

    ![][11]
    
    Bu eylem, yeni mobil uygulama arka Azure üzerinde barındırılan uç bir post isteği toohello gönderir. Veriler hello istek hello Todoıtem tablosuna eklenir. Hello tabloda depolanan öğeler veri hello listesinde görüntülenen Mobile Apps sonlandırmak ve hello hello tarafından döndürülür.
    
    > [!NOTE]
    > Mobile Apps arka uç hello Todoıtemmanager.cs C# çözümünüzün hello taşınabilir sınıf kitaplığı proje dosyası içinde erişen hello kodu bulacaksınız.
    >
    >

## <a name="optional-run-hello-windows-project"></a>(İsteğe bağlı) Merhaba Windows projesini çalıştırın

Bu bölümde, Windows cihazları için Xamarin WinApp projesi hello çalıştırın. Windows cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.

#### <a name="in-visual-studio"></a>Visual Studio’da

1. Merhaba Windows projeleri hiçbirini sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.

2. Merhaba üzerinde **yapı** menüsünde, select **Configuration Manager**.

3. Merhaba, **Configuration Manager** iletişim kutusu, select hello **yapı** ve **dağıtma** seçtiğiniz onay kutularını sonraki toohello Windows projesi.

4. toobuild hello proje ve hello uygulamayı Windows öykünücüsünde, select hello başlatın **F5** anahtarı.

   > [!NOTE]
   > Başlangıç projesi oluşturma sorunları varsa hello NuGet Paket Yöneticisi ve güncelleştirme toohello en son sürümünü hello Xamarin destek paketlerinin çalıştırın. Hızlı Başlangıç projeleri yavaş tooupdate toohello en son sürümleri olabilir.    
   >
   >

5. Merhaba uygulamada gibi anlamlı bir metin yazın *Xamarin öğren*, ve ardından artı işaretini seçin hello (**+**).

    Bu eylem, yeni mobil uygulama arka Azure üzerinde barındırılan uç bir post isteği toohello gönderir. Veriler hello istek hello Todoıtem tablosuna eklenir. Hello tabloda depolanan öğeler veri hello listesinde görüntülenen Mobile Apps sonlandırmak ve hello hello tarafından döndürülür.
    
    ![][12]
    
    > [!NOTE]
    > Mobile Apps arka uç hello Todoıtemmanager.cs C# çözümünüzün hello taşınabilir sınıf kitaplığı proje dosyası içinde erişen hello kodu bulacaksınız.
    >
    >

## <a name="next-steps"></a>Sonraki adımlar

* [Kimlik doğrulama tooyour uygulama Ekle](app-service-mobile-xamarin-forms-get-started-users.md)  
  Bilgi nasıl bir kimlik sağlayıcısı ile uygulamanızın tooauthenticate kullanıcılar.

* [Anında iletme bildirimleri tooyour uygulama Ekle](app-service-mobile-xamarin-forms-get-started-push.md)  
  Mobile Apps arka uç toouse Azure Notification Hubs toosend hello anında iletme bildirimlerini yapılandırmak ve tooadd anında iletme bildirimleri tooyour uygulama'ı nasıl desteklediğini öğrenin.

* [Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Bilgi nasıl tooadd çevrimdışı destek Mobile Apps kullanarak uygulamanız için yedekleme son. Çevrimdışı eşitleme ile mobil uygulamanızın verilerini ağ bağlantısı olmasa bile görüntüleyebilir, ekleyebilir ve değiştirebilirsiniz.

* [Mobile Apps için Hello yönetilen istemci kullanma](app-service-mobile-dotnet-how-to-use-client-library.md)  
  İstemci SDK'sı, Xamarin uygulamanızda toowork hello ile nasıl yönetileceğini öğrenin.

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
