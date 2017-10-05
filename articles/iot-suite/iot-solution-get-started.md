---
title: "MyDriving Azure IOT örnek: Hızlı Başlangıç | Microsoft Docs"
description: "Akış analizi, Machine Learning ve olay hub'ları da dahil olmak üzere Microsoft Azure kullanarak bir IOT sistemi mimari konusunda kapsamlı bir örnek bir uygulama kullanmaya başlayın."
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
ms.openlocfilehash: 031b492df1f186087e7b91102cbb44f552999293
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="mydriving-iot-system-quick-start"></a>MyDriving IOT sistem: Hızlı Başlangıç
MyDriving sistemidir tasarımını ve uygulamasını tipik bir gösteren bir [nesnelerin interneti](iot-suite-overview.md) telemetri cihazlardan toplar (IOT) çözümü bu verileri bulutta işler ve makine sağlamak öğrenme geçerlidir bir Uyarlamalı yanıt. Tanıtım cep telefonunuzu ve arabanızın denetim sisteminden bilgileri toplayan bir bağdaştırıcı verilerini kullanarak, car dönüşleri hakkındaki verileri kaydeder. Diğer kullanıcıların kıyasla yönlendirmeli stilinize hakkında geri bildirim sağlamak için bu verileri kullanır.

MyDriving gerçek amacı, kendi IOT çözümünüzü oluştururken başlamanıza yardımcı olmaktır. Ancak, önce şimdi, uygulamayla MyDriving kendisini--test kullanıcı ekibimiz üyesi olarak yapmalarını. Mimariye inceleyin önce bu uygulamanın ve bunun arkasındaki sistem bir tüketici olarak bir deneyim sağlar. Bu aynı zamanda, HockeyApp, kullanıcılar test uygulamalarınızın alfa, beta dağıtımları yönetme cool olanağı sunar.

## <a name="use-the-mobile-experience"></a>Mobil deneyimi kullanın
Android, iOS veya Windows 10 cihaz varsa MyDriving uygulamasını kullanabilirsiniz.

### <a name="android-and-windows-10-mobile-installation"></a>Android ve Windows 10 Mobile yükleme
Cihazınızda:

1. Geliştirme uygulamaları izin ver:
   
   * Android: İçinde **ayarları** > **güvenlik**, uygulamalardan izin **bilinmeyen kaynaklardan**.
   * : Windows 10 **ayarları** > **güncelleştirmeleri** > **geliştiriciler için**ayarlayın **geliştirici modunu**.
2. İle kaydolduktan ya da, oturum açma tarafından beta test ekibimiz katılma [HockeyApp](https://rink.hockeyapp.net). HockeyApp kullanıcılar test etmek için uygulamanızın sürümleri erken dağıtmak kolaylaştırır.
   
   Windows 10 kullanıyorsanız, Edge tarayıcısını kullanın.
   
   Build 2016 katılımcı olsaydı, Microsoft'un düğmeler birini kullanarak konferans için kayıtlı aynı Microsoft hesabı e-posta oturum açın. HockeyApp ile zaten kaydolmuşsunuz.
   
   ![HockeyApp oturum açma ekranı](./media/iot-solution-get-started/image1.png)
3. Karşıdan yükleme ve uygulamayı yükleyin:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   İki öğe yok. Yüklemek **güvenilir kişiler**. Daha sonra uygulamayı yükleyin.

*Windows 10 Mobile uygulama başlatma sorunları?* Telefonunuza bir güncelleştirme veya iki arkasında olabilir. En son güncelleştirmeleri olduğuna emin olun veya yükleyin:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>iOS yükleme
Build 2016 gittiğiniz, uygulamayı test ekibimiz HockeyApp üzerinde bir üyesi olarak karşıdan yükleyin:

1. İOS Cihazınızda oturum [HockeyApp](https://rink.hockeyapp.net).
   Microsoft'un oturum açma düğmeler ve konferans kayıtlı aynı Microsoft hesabı e-posta ile oturum birini kullanın. (E-posta ve parola alanlarına kullanmayın.)
   
   ![HockeyApp oturum açma ekranı](./media/iot-solution-get-started/image1.png)
2. HockeyApp panosunda MyDriving seçin ve indirin.
3. HockeyApp beta sürümünden yetkilendirin.
   
   a. Git **ayarları** > **genel** > **profilleri ve aygıt yönetimi.**
   
   b. Güven **Bit stadyum GmbH** sertifika.

Build 2016 gitmediğiniz, derleme ve uygulamayı kendiniz dağıtın:

1. Kodu indirme [github'dan].
2. Derleme ve tarafından dağıtma [Xamarin kullanarak].

Daha ayrıntılı olarak Bul [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>OBD bağdaştırıcıyı (isteğe bağlı) Al
Bu gerçek bir nesnelerin interneti sistem yapan bölümüdür! Uygulama, olmadan kullanabilirsiniz ancak daha fazla keyif gerçek bir şey olduğunu ve pahalı olmayan.

Yerleşik tanılama (OBD), car ayarlamak ve tek sesleri ve uyarı ampul tanılamak için Garaj kullanır, car özelliğidir. Car harika antiquity olmadıkça, genellikle bir flap Pano altında arkasında kabini yuva yere bulabilirsiniz. Sağ bağlayıcısıyla altyapının performans ölçümlerini alın ve belirli ayarlamalar yapın. Bir OBD Bağlayıcısı ailenin normal yerlerden satın alınabilir. Bu, Bluetooth veya Wi-Fi telefonunuzda bir uygulama kullanarak bağlanır.

Bu durumda, car bulutunun bağlanacağı yapacağız. OBD doğrudan bağlantı için telefonunuza olsa da, uygulamamıza geçişi olarak çalışır. Arabanızın telemetri düz MyDriving IOT hub'ına yol dönüşleri oturum ve yönlendirmeli stilinize değerlendirmek için işleneceği gönderilir.

Bir OBD aygıtı bağlamak için:

1. Car OBD yuva olduğundan emin olun.
2. OBD bağdaştırıcıyı alın:
   
   * Bir Android veya Windows phone kullanıyorsanız, Bluetooth özellikli OBD II bağdaştırıcısı gerekir. Kullandık [BAFX ürünleri 34t5 Bluetooth OBDII Tarama Aracı].
   * Bir iOS telefon kullanıyorsanız, bir Wi-Fi etkin OBD bağdaştırıcısı gerekir. Kullandık [ScanTool OBDLink MX Wi-Fi: OBD bağdaştırıcısı/tanılama tarayıcı].
3. Telefonunuza bağlanmak için OBD bağdaştırıcınızı birlikte gelen yönergeleri izleyin. Aşağıdakileri göz önünde bulundurun:
   
   * Üzerinde telefon ile eşleştirilmelidir Bluetooth bağdaştırıcısı **ayarları** sayfası.
   * Bir Wi-Fi bağdaştırıcısı adres aralığı 192.168.xxx.xxx olması gerekir.
4. Çeşitli otomobiller varsa, her (en fazla üç için) ayrı bir bağdaştırıcı alabilirsiniz.

OBD bağdaştırıcıyı sahip değilseniz, uygulama konumu ve hız veri arka ucuna telefonun GPS alıcısından hala gönderir ve bir OBD benzetimini yapmak isteyip istemediğinizi sorar.

Bölüm 2.1, "IOT cihazları," kendi OBD cihaz oluşturmak için seçenekler ve uygulama OBD bağdaştırıcısı verileri nasıl kullandığı hakkında daha fazla bulabilirsiniz [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs).

## <a name="use-the-app"></a>Uygulamasını kullanma
Uygulamayı başlatın. Bir başlangıç hızlı başlangıç nasıl çalıştığını aracılığıyla yol yoktur.

### <a name="track-your-trips"></a>Dönüş izleme
Bir seyahat başlatmak için (ekranın en büyük kırmızı daire) kaydı düğmesine dokunun ve sonuna yeniden dokunun.

![İzleme seyahat için Kaydet düğmesine çizimi](./media/iot-solution-get-started/image2.png)

Hiçbir OBD aygıt ise, bir seyahat her başlattığınızda, simulator kullanmak isteyip istemediğinizi istenir.

Bir seyahat sonunda durdur düğmesine dokunun ve özeti alın.

![Özet bir seyahat örneği](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Dönüş gözden geçirin
![Geçmiş seyahat örneği](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Profilinizi gözden geçirin
![Yürüten stili profil örneği](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Test Geri bildirimlerinizi bize gönderin
Azure'daki yardımcı olmak için MyDriving kendi IOT sistemleri oluşturduğundan kesinlikle ne kadar iyi çalıştığı hakkında görüşlerinizi istiyoruz. Varsa bize bildirin:

* İlgili sorunlar veya zorluklar çalıştırın.
* Senaryonuz için daha uygun hale bir uzantı noktası yoktur.
* Belirli gereksinimleri gerçekleştirmek için daha verimli bir şekilde bulur.
* MyDriving veya bu belgeleri geliştirmek için diğer bir önerileri vardır.

MyDriving uygulama içinde yerleşik HockeyApp geri bildirim mekanizması kullanabilirsiniz: yalnızca iOS ve Android cihazlarda telefonunuza bir sallama verin veya kullanmak **geri bildirim** menü komutu. Biz hakkında konuşurken bilmeniz böylece bu ekran, otomatik olarak ekleyecek. Ve tüm talihsiz kilitlenme varsa, bunları hakkında bize iletmek için kilitlenme günlükleri HockeyApp toplar. Geri bildirim aracılığıyla da verebilirsiniz [HockeyApp portal].

Ayrıca dosya bir [GitHub sorunu], veya bir yorum yazın (en-us edition).

İşitme için sizden umuyoruz!

## <a name="next-steps"></a>Sonraki adımlar
* Araştır [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs) nasıl artık tasarlanmış ve tüm MyDriving sistem yerleşik anlamak için.
* [Bir bir sistem oluşturup](iot-solution-build-system.md) bizim Azure Resource Manager komut dosyalarını kullanarak. [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs) ayrıca yapacağınız en özelleştirmeleri alanlarında sırasında size kılavuzluk eder.

[github'dan]: https://github.com/Azure-Samples/MyDriving
[Xamarin kullanarak]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX ürünleri 34t5 Bluetooth OBDII Tarama Aracı]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD bağdaştırıcısı/tanılama tarayıcı]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[GitHub sorunu]: https://github.com/Azure-Samples/MyDriving/issues
