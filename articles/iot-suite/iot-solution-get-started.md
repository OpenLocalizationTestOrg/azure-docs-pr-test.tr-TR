---
title: "MyDriving Azure IOT örnek: Hızlı Başlangıç | Microsoft Docs"
description: "Nasıl kapsamlı bir örnek bir uygulama ile çalışmaya başlama tooarchitect akış analizi, Machine Learning ve olay hub'ları da dahil olmak üzere Microsoft Azure kullanarak bir IOT sistemi."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a>MyDriving IOT sistem: Hızlı Başlangıç
MyDriving sistemidir hello tasarımını ve uygulamasını tipik bir gösteren bir [nesnelerin interneti](iot-suite-overview.md) telemetri cihazlardan toplar (IOT) çözümü hello bulutta bu verileri işler ve machine learning uygulanır tooprovide Uyarlamalı yanıt. Merhaba tanıtım cep telefonunuzu ve arabanızın denetim sisteminden bilgileri toplayan bir bağdaştırıcı verilerini kullanarak, car dönüşleri hakkındaki verileri kaydeder. Bu veri tooprovide geri bildirim yönlendirmeli stilinize karşılaştırma tooother kullanıcılar üzerinde kullanır.

Merhaba gerçek MyDriving amacı kendi IOT çözümünüzü oluştururken başlattığınız tooget budur. Ancak, önce şimdi uygulamayla hello MyDriving kendisini--test kullanıcı ekibimiz üyesi olarak adımıdır alın. Merhaba mimariye inceleyin önce bu size hello uygulamanın ve bunun arkasındaki hello sistem bir tüketici olarak bir deneyim sağlar. Bu aynı zamanda, tooHockeyApp, uygulamaları tootest kullanıcılarınızın hello alfa ve beta dağıtımlarını yönetme harika bir yol sunar.

## <a name="use-hello-mobile-experience"></a>Merhaba mobil deneyimi kullanın
Android, iOS veya Windows 10 cihaz varsa hello MyDriving uygulamasını kullanabilirsiniz.

### <a name="android-and-windows-10-mobile-installation"></a>Android ve Windows 10 Mobile yükleme
Cihazınızda:

1. Geliştirme uygulamaları izin ver:
   
   * Android: İçinde **ayarları** > **güvenlik**, uygulamalardan izin **bilinmeyen kaynaklardan**.
   * : Windows 10 **ayarları** > **güncelleştirmeleri** > **geliştiriciler için**ayarlayın **geliştirici modunu**.
2. İle kaydolduktan ya da, oturum açma tarafından beta test ekibimiz katılma [HockeyApp](https://rink.hockeyapp.net). HockeyApp sürümleri kolay toodistribute erken uygulama tootest kullanıcılarınızın kolaylaştırır.
   
   Windows 10 kullanıyorsanız, hello Edge tarayıcısı kullanın.
   
   Build 2016 katılımcı olsaydı, oturum hello aynı oturum hello Microsoft düğmeleri birini kullanarak hello konferans için kayıtlı Microsoft hesabı e-posta. HockeyApp ile zaten kaydolmuşsunuz.
   
   ![HockeyApp oturum açma ekranı](./media/iot-solution-get-started/image1.png)
3. Merhaba uygulamasını indirip buradan yükleyebilirsiniz:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   İki öğe yok. Merhaba yüklemek **güvenilir kişiler**. Ardından hello uygulamasını yükleyin.

*Tüm Windows 10 Mobile başlangıç hello uygulamasını sorunları?* Telefonunuza bir güncelleştirme veya iki arkasında olabilir. Merhaba en son güncelleştirmeleri olduğuna ya da yükleme emin olun:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>iOS yükleme
Build 2016 gittiğiniz, test ekibimiz HockeyApp üzerinde bir üyesi olarak hello uygulamasını yükleyin:

1. İOS Cihazınızda çok oturum[HockeyApp](https://rink.hockeyapp.net).
   Bir hello Microsoft oturum açma düğmeleri ile oturum açın ve hello hello konferans kayıtlı aynı Microsoft hesabı e-posta kullanın. (Merhaba e-posta ve parola alanlarına kullanmayın.)
   
   ![HockeyApp oturum açma ekranı](./media/iot-solution-get-started/image1.png)
2. Merhaba HockeyApp panosundaki MyDriving seçin ve indirin.
3. HockeyApp Hello beta sürümünden yetkilendirin.
   
   a. Çok Git**ayarları** > **genel** > **profilleri ve aygıt yönetimi.**
   
   b. Merhaba güven **Bit stadyum GmbH** sertifika.

Build 2016 gitmediğiniz, yapı ve hello uygulama kendiniz dağıtabilirsiniz:

1. Merhaba kodu indirme [github'dan].
2. Derleme ve tarafından dağıtma [Xamarin kullanarak].

Daha fazla ayrıntı hello Bul [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>OBD bağdaştırıcıyı (isteğe bağlı) Al
Bu gerçek bir nesnelerin interneti sistem yapan hello bölümüdür! Daha fazla keyif hello gerçek bir şey olduğunu ve pahalı olmayan hello uygulama biri olmadan kullanabilirsiniz ancak.

Yerleşik tanılama (OBD) hello Garaj kullanır tootune, car yukarı hello ve tek sesleri ve uyarı ampul Tanılama, car özelliğidir. Car harika antiquity olmadıkça, genellikle bir flap hello Pano altında arkasında hello kabini yuva yerde bulabilirsiniz. Hello sağ bağlayıcısıyla hello altyapısının performans ölçümlerini alın ve belirli ayarlamalar yapın. Bir OBD Bağlayıcısı ailenin hello normal yerlerden satın alınabilir. Bu, telefonunuza Bluetooth veya Wi-Fi tooan uygulamasını kullanarak bağlanır.

Bu durumda, car toohello bulutunuzu tooconnect yapacağız. Merhaba OBD bağlantısından Hello doğrudan bağlantı tooyour telefon olmakla birlikte, uygulamamıza geçişi olarak çalışır. Arabanızın telemetri düz toohello olduğu MyDriving IOT hub, yol dönüşleri toolog işlenen gönderilir ve yönlendirmeli stilinize değerlendirin.

tooconnect OBD aygıt:

1. Car OBD yuva olduğundan emin olun.
2. OBD bağdaştırıcıyı alın:
   
   * Bir Android veya Windows phone kullanıyorsanız, Bluetooth özellikli OBD II bağdaştırıcısı gerekir. Kullandık [BAFX ürünleri 34t5 Bluetooth OBDII Tarama Aracı].
   * Bir iOS telefon kullanıyorsanız, bir Wi-Fi etkin OBD bağdaştırıcısı gerekir. Kullandık [ScanTool OBDLink MX Wi-Fi: OBD bağdaştırıcısı/tanılama tarayıcı].
3. İsteğe bağlı olarak, OBD bağdaştırıcısı tooconnect ile tooyour telefon gelen hello yönergeleri izleyin. Merhaba aşağıdakileri göz önünde bulundurun:
   
   * Bluetooth bağdaştırıcısı hello telefonda hello ile eşleştirilmelidir **ayarları** sayfası.
   * Bir Wi-Fi bağdaştırıcısı hello aralığı 192.168.xxx.xxx bir adres olmalıdır.
4. Çeşitli otomobiller varsa, her (en fazla üç için) ayrı bir bağdaştırıcı alabilirsiniz.

OBD bağdaştırıcıyı yoksa, hello uygulama hala konumu ve hello telefonun GPS alıcı toohello geri hızı verileri sona erdirmek ve toosimulate bir OBD isteyip istemediğinizi sorar gönderir.

Hello bölüm 2.1, "IOT cihazları," kendi OBD cihaz oluşturmak için seçenekler ve hello uygulama hello OBD bağdaştırıcısı verileri nasıl kullandığı hakkında daha fazla bulabilirsiniz [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs).

## <a name="use-hello-app"></a>Merhaba uygulama kullanma
Merhaba uygulaması başlatın. İlk bir hızlı başlangıç toowalk yoktur size nasıl çalışır.

### <a name="track-your-trips"></a>Dönüş izleme
Merhaba kayıt düğmesini (Merhaba ekranında hello sonundaki büyük kırmızı daire) toostart bir seyahat ve yeniden tooend'e dokunun.

![İzleme seyahat için hello kayıt düğmesini çizimi](./media/iot-solution-get-started/image2.png)

Hiçbir OBD aygıt ise, bir seyahat her başlattığınızda toouse hello simulator isteyip istemediğinizi istenir.

Bir seyahat Hello sonunda hello Durdur düğmesine dokunun ve özeti alın.

![Özet bir seyahat örneği](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Dönüş gözden geçirin
![Geçmiş seyahat örneği](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Profilinizi gözden geçirin
![Yürüten stili profil örneği](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Test Geri bildirimlerinizi bize gönderin
Kendi IOT sistemleri MyDriving toohelp başkalarından oluşturduğumuz çünkü kesinlikle ne kadar iyi çalıştığı konusunda toohear sizden istiyoruz. Varsa bize bildirin:

* İlgili sorunlar veya zorluklar çalıştırın.
* Daha uygun tooyour senaryo yapacağı bir uzantı noktası yoktur.
* Belirli gereksinimlerini daha verimli bir şekilde tooaccomplish bulun.
* MyDriving veya bu belgeleri geliştirmek için diğer bir önerileri vardır.

Merhaba MyDriving app içinde kendisi hello yerleşik HockeyApp geri bildirim mekanizması kullanabilirsiniz: yalnızca iOS ve Android cihazlarda telefonunuza bir sallama verin veya hello kullan **geri bildirim** menü komutu. Biz hakkında konuşurken bilmeniz böylece bu ekran, otomatik olarak ekleyecek. Ve tüm talihsiz kilitlenme varsa, HockeyApp hello kilitlenme günlükleri tootell bize bunlarla ilgili toplar. Geri bildirim hello aracılığıyla da verebilirsiniz [HockeyApp portal].

Ayrıca dosya bir [GitHub sorunu], veya bir yorum yazın (en-us edition).

Toohearing sizden umuyoruz!

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba keşfedin [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs) nasıl artık tasarlanmış ve yerleşik toounderstand hello tüm MyDriving sistem.
* [Bir bir sistem oluşturup](iot-solution-build-system.md) bizim Azure Resource Manager komut dosyalarını kullanarak. Merhaba [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs) Ayrıca, burada yaptığınız hello çoğu özelleştirmeleri alanlarında size yol gösterir.

[github'dan]: https://github.com/Azure-Samples/MyDriving
[Xamarin kullanarak]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX ürünleri 34t5 Bluetooth OBDII Tarama Aracı]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD bağdaştırıcısı/tanılama tarayıcı]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[GitHub sorunu]: https://github.com/Azure-Samples/MyDriving/issues
