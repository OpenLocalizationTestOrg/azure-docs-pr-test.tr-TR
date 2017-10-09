---
title: "MyDriving Azure IOT örnek: Bu yapı | Microsoft Docs"
description: "Nasıl kapsamlı bir örnek bir uygulama oluşturmak tooarchitect akış analizi, Machine Learning ve olay hub'ları da dahil olmak üzere Microsoft Azure kullanarak bir IOT sistemi."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>Derleme ve hello MyDriving çözüm tooyour ortamını dağıtma
MyDriving, car veri toplar, machine learning kullanarak işler ve cep telefonunuza sunar bir nesnelerin interneti (IOT) çözümüdür. Microsoft Azure tarafından sağlanan hizmetlerin çeşitli Hello arka uç oluşur. Merhaba istemciler, Android, iOS veya Windows 10 telefonları olabilir.

Merhaba MyDriving çözüm toogive oluşturduğumuz, kendi IOT sistem oluşturma başkalarından. Merhaba gelen [MyDriving deposu github'da](https://github.com/Azure-Samples/MyDriving), Azure Resource Manager betikler kendi Azure hesabınızda oturum toodeploy hello arka uç mimarisi alabilirsiniz. Bu noktadan itibaren hello farklı hizmetleri yeniden yapılandırın, kendi verilerinizi hello sorguları toosuit değiştirmek ve benzeri. --Hello mobil uygulama, hello Azure App Service API proje ve daha fazla--hello MyDriving deposu için kod ile birlikte bu betikleri bulabilirsiniz.

Hello, hello uygulama henüz henüz denemediyseniz, Ara [Get Başlarken Kılavuzu](iot-solution-get-started.md).

Merhaba hello mimarisinin ayrıntılı bir hesabı [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs). Özet olarak, birkaç parça vardır biz toocreate benzer bir proje ayarlayın:

* A **istemci uygulaması** Android, iOS ve Windows 10 telefonlarda çalışır. Merhaba Xamarin platform tooshare kullanırız altında github'da depolanan hello kodunun kadar `src/MobileApp`. Merhaba uygulama aslında iki ayrı işlevleri gerçekleştirir:
  * Telemetri hello yerleşik tanılama (OBD) CİHAZDAN ve kendi konum hizmeti toohello sistemin bulut arka uçtan geçirir.
  * Bu kullanıcılar kendi kaydedilen yol dönüşleri hakkında burada sorgulayabilir kullanıcı arabirimidir.
* A **bulut hizmeti** gerçek zamanlı hello yol seyahat verileri alır ve işler. Bu hizmet oluşturma hello ana iş toochoose olduğunda, Parametreleştirme ve çok çeşitli Azure hizmetlerini wire. Bazı hello bölümleri betikleri toofilter ve işlem hello gelen verileri gerektirir. Bir Azure Resource Manager şablonu tooconfigure tüm hello bölümleri kullanırız.
* A **mobil hizmet uygulama** hello kullanıcı arabirimi bölümü hello cihaz uygulamasının arkasında hello web hizmetidir. Ana işini tooquery hello depolanmış, işlenen verilerin veritabanıdır. Kendi kodu altında github'da `src/MobileAppService`.
* **Xamarin ile Visual Studio** bizim geliştirme ortamıdır. Visual Studio bileşeninin hem tek başına tümleşik geliştirme ortamı (IDE) olarak yoksa, Xamarin kullanılan toobuild hello platformlar arası aygıt kodu. toobuild hello iOS, gerekli toohave OS X makinede çalışan Xamarin örneği koddur. Gerekirse, Visual Studio'dan yönetilen bir aracı olarak çalıştırılabilir.
* **Birim testi** hello aygıtı uygulamaları Xamarin Test Cloud gerçekleştirilir.
* **GitHub** burada depolarız tüm hello kodu, komut dosyaları ve şablonları hello depodur.
* **Visual Studio Team Services** toomanage hello sürekli yapı ve test hello web hizmeti ve cihaz uygulamaların kullandığı bir bulut hizmetidir.
* **HockeyApp** hello aygıt kodu kullanılan toodistribute sürümleri olan. Ayrıca, kilitlenme ve kullanım raporları ve kullanıcı geri bildirim de toplar.
* **Visual Studio Application Insights** izleyiciler hello mobil web hizmeti.

Bu nedenle, tüm, ayarlarız nasıl görelim. 

> [!NOTE] 
> Aşağıdaki adımları hello çoğunu isteğe bağlıdır.
>
>

## <a name="sign-up-for-accounts"></a>Hesapları için kaydolun
* [Visual Studio geliştirme Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). Bu ücretsiz programı kolay erişim toomany geliştirici araçları ve Visual Studio, Visual Studio Team Services ve Azure gibi hizmetler sağlar. Bunun, $25/ay kredi Azure üzerinde 12 ay sağlar. Abonelikler tooPluralsight eğitim ve Xamarin University de içerir. Ayrıca ayrı ayrı ücretsiz katmanı için kaydolabilirsiniz [Azure](https://azure.com) ve [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx), ancak bunlar Azure kredisi sağlamaz.
* [HockeyApp](https://rink.hockeyapp.net/) (isteğe bağlı), mobil uygulama test dağıtımını yönetmek için ve telemetri toplama.
* [Xamarin](https://xamarin.com/) (gerekli), hello mobil uygulama ve çalışan hata ayıklama çalıştırır ve testleri oluşturma [Xamarin Test Cloud](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (isteğe bağlı), toocreate ücretsiz ortak depoları için kendi kodunuzu (özel depoları Ücretli). Alternatif olarak, özel depoları için Visual Studio Team Services hello temel plan kullanabilirsiniz.
* [Power BI](https://powerbi.microsoft.com/) (isteğe bağlı), toocreate zengin Görselleştirmelerini hello tüm sistem arasında verileri.

> [!NOTE]
> Hesap tooaccess hello MyDriving kodda bir GitHub gerekmeyen [hello GitHub MyDriving depo](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Geliştirme Araçları'nı yükleme
Merhaba aşağıdaki hello tam çözüm geliştirmek için kurulması: bir iOS, Android ve Windows 10 Mobile bir Azure ile platformlar arası uygulama son yedekleme.

Alternatif olarak, Azure geri bitiş hello üzerinde çalışıyorsanız olmayan Mac veya Windows toodevelop hello mobil uygulamalar üzerinde Xamarin Studio kullanabilirsiniz.

Var olan bir [bu kurulumu daha uzun açıklama](https://msdn.microsoft.com/library/mt613162.aspx).

### <a name="windows-development-machine"></a>Windows geliştirme makine
Merhaba merkezi Windows Visual Studio, Android ve Windows hello App Service API projesi ve mikro hizmet uzantıları için hello MyDriving uygulaması ile çalışmaya yönelik bir araçtır.

Xamarin, Git, Öykünücüler ve diğer yararlı bileşenleri tüm Visual Studio ile tümleşiktir.

Yükle:

* [Xamarin ile Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs) (herhangi bir sürümünü--topluluk boş).
* [Evrensel Windows platformu için SQLite](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Toobuild hello Windows 10 Mobile kod gereklidir.
* [Visual Studio için Azure SDK](https://www.visualstudio.com/vs/azure-tools/). Azure'da, Azure yönetmek için komut satırı araçları ile birlikte çalışan uygulamalar için SDK hello sağlar.
* [Azure Service Fabric SDK](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Gerekli toobuild hello [mikro hizmet](../service-fabric/service-fabric-get-started.md) uzantısı.

Merhaba sağ Visual Studio uzantıları sahip olduğundan emin olun. Altında denetleyin **Araçları**, gördüğünüz **Android, iOS, Xamarin...** . Aksi takdirde, Visual Studio'yu açın, aramak için Xamarin ve hello istemleri tooinstall izleyin. Ayrıca, denetleyin **Windows için Git** yüklenir. Değilse, Visual Studio varsa, için arama ve hello istemleri tooinstall izleyin. 

### <a name="mac-development-machine"></a>Mac geliştirme makine
Merhaba Mac (Yosemite veya sonrası) için iOS toodevelop istiyorsanız gereklidir. Üzerinde Windows toodevelop Xamarin ile Visual Studio'yu kullanın ve tüm hello kodu yönetmek, ancak oturum iOS kod hello ve Xamarin Mac'te sipariş toobuild yüklü bir aracı kullanır.

![Windows üzerinde geliştirme ve Mac derleme](./media/iot-solution-build-system/image1.png)

(Alternatif olarak, Xamarin Studio doğrudan hello Mac toodevelop platformlar arası uygulamalar üzerinde kullanabilirsiniz.)

Hedef platform olarak tooinclude iOS istemiyorsanız hello Mac gerekmez.

Yükle:

* [İOS için Xamarin Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). Visual Studio ve Xamarin Windows sanal makine çalıştıran bir Mac üzerinde ayarlayabilirsiniz. Bkz: [Kurulum, yükleme ve Doğrulamalar Mac kullanıcıları için](https://msdn.microsoft.com/library/mt488770.aspx) konusuna bakın.
* [Azure geliştirme araçları](https://azure.microsoft.com/downloads/) (isteğe bağlı).

Merhaba Mac üzerinde uzaktan oturum açmayı etkinleştirme Açık **sistem tercihleri** > **paylaşım**ve ardından **uzaktan oturum açma**.

Merhaba Xamarin eklenti Windows Visual Studio'da bir iOS projesi açtığınızda hello Mac hello kimliği ister.

## <a name="fetch-hello-github-repository"></a>Merhaba GitHub deposunu getirme
Yerel bir kopyasını fetch [hello GitHub MyDriving deposu](https://github.com/Azure-Samples/MyDriving) hello kullanarak **ZIP'i indir** düğmesini GitHub, Visual Studio veya başka bir Git istemci.

Merhaba dosya tooa klasör C: gibi bir kısa yol adına sahip sıkıştırmasını\\kodu.

Tookeep ile toodate yedeklemek istediğiniz veya tooour kodu katkıda, alternatif olarak, aşağıdaki gibi hello depoyu kopyalayın:

**Git kopya https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>Bir Bing Haritalar API'si anahtarı alma
[Kaydetmek için bir Bing Haritalar API'si anahtarı](https://msdn.microsoft.com/library/ff428642.aspx).

Bu, satır 22 inç tooreplace ihtiyacınız `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-hello-demo-app"></a>Merhaba demo uygulaması oluşturma
Bu çözümlerin Visual Studio'da açın:

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

İstem için elde edersiniz:

* Bazı koruyabilmeleri projeleri güven. Tooopen seçin bunları şimdi toogo istiyorsanız.
* Yeni bir Windows 10 makine üzerinde çalışıyorsanız geliştirici modunu ayarlayın.
* Xamarin kimlik bilgilerinizi sağlayın.
* Toohello Xamarin Mac Bağlan Mac yoksa, sağ hello iOS Visual Studio'da ve ardından **projeyi**.

Merhaba çözümü yeniden derleyin.

Sorun yapı varsa, biz buldunuz hello çözümleri tooquirks deneyin:

* *Değil VINLookupApplication proje yük*: hello yüklü olduğundan emin olun [Visual Studio için Azure SDK](https://www.visualstudio.com/vs/azure-tools/).
* *Değil Service Fabric Projeyi derlemek*: ilk hello arabirimi projeleri oluşturmak ve hello Service Fabric SDK yüklü olduğundan emin olun.
* *Olmayan Android uygulaması oluşturma*:
  
  * Açık **Araçları** > **Android** > **Android SDK Manager**ve sağlamak, Android 6 (API 23) / SDK Platform yüklenir.
  * Bu dizini silin ve yeniden derleyin:<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>Tooknow hello kod alın
Merhaba çözümde, bulabilirsiniz:

* Azure uzantıları: Service Fabric.
* Azure Hdınsight: Azure seyahat verileri işlemek için betikler.
* Mobil uygulamalar: hello cihaz uygulamaları.
* MobileAppsService/MyDrivingService: hello web sonlandırın.
* Power BI: hello rapor tanımı.
* Komut dosyaları:
  
  * Kaynak Yöneticisi: şablonları toobuild hello Azure kaynakları.
  * PowerShell: Betikler toorun hello Resource Manager şablonları.
  * Azure SQL Database: Hata ayıklama veritabanları.
* SQL veritabanı: CreateTables: şema tanımları.
* Azure Stream Analytics: Bu dönüşüm hello gelen veri akışı sorgular.

## <a name="run-hello-apps-in-development-mode"></a>Merhaba uygulamaları geliştirme modunda çalıştır
Eylem toorun hello uygulamalar, kullanmakta olduğunuz hello aygıtı temel alarak alın:

* Arka uç: hello başlangıç projesi ve tuşuna F5 toorun hello arka uç web hizmeti olarak kümesi MyDrivingService. Merhaba API listeleme tarayıcı görünümünü açar.
* Mobil istemcilerin: Merhaba [mobil uygulamalar Xamarin geliştirilmiş](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * Android: ayrıntılı bilgi için bkz: [hata ayıklama Android, Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/).
  * iOS: ayrıntılı bilgi için bkz: [iOS hata ayıklama](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/).
  * Windows Phone: ayrıntılı bilgi için bkz: [Xamarin + Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/).

## <a name="upload-hello-mobile-app-toohockeyapp"></a>Merhaba mobil uygulama tooHockeyApp karşıya yükle
HockeyApp yeni sürümlerin kullanıcılara bildirme, Android, iOS veya Windows uygulama tootest kullanıcılarınızın, hello dağıtımını yönetir. Ayrıca topladığı yararlı kilitlenme raporları, ekran görüntüleri ve kullanım ölçümleri ile kullanıcı geri bildirim.

[Başlangıç yükleyerek](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) yapı uygulamanızı. Ardından, çok oturum[HockeyApp](https://rink.hockeyapp.net) geliştirme makinenizden. Merhaba Geliştirici Panoda tıklatın **yeni uygulama**ve ardından yerleşik hello dosyaları hello penceresi sürükleyin. (Daha sonra yapı hizmeti toodo bu otomatikleştirebilirsiniz.)

Şimdi, uygulama Panonuzda demektir.

![Merhaba uygulama Panoda genel bakış sekmesi](./media/iot-solution-build-system/image2.png)

Uygulamanızın üzerinde çalışacağı her platform için Hello işlemi yineleyin. Ardından, yapabileceğiniz hello aşağıdaki:

* Kullanım hello [uygulama kimliği](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) hello Pano toosend kilitlenme verilerini ve uygulamanızı geri bildirimi. MyDriving içinde src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs hello kimlikleri güncelleştirin.
* [Test kullanıcıları davet](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). Sınayıcılar kullanıcılar bir URL toorecruit alır. Bunlar ekibiniz için mümkün toosign olması, hello uygulamayı indirmek ve geri bildirim gönderin.
* Daha açık bir beta sürümü tercih ediyorsanız, hello dağıtım toopublic ayarlayın. Tıklatın **uygulamasını yönetmek** > **dağıtım** > **karşıdan Public =**. Şimdi herkes uygulamanızı indirebilir ve geri bildirim göndermek ve yeni bir sürüm duyurduğumuzda bir bildirim görürsünüz. Bazı kilitlenme raporları onlardan çok alabilirsiniz.
  
   ![Takımlar hello Panoda](./media/iot-solution-build-system/image3.png)
* [Bağlantı kilitlenme raporları tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Tıklatın **uygulamasını yönetmek** > **Visual Studio Team Services**. Kilitlenme raporları veya geri bildirim alındığında olduğunda HockeyApp iş öğelerini Team Services içinde otomatik olarak oluşturabilirsiniz.

Merhaba, daha okunur [HockeyApp site](https://hockeyapp.net).

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>Xamarin Test Cloud üzerinde Hello mobil uygulamayı test etme
[Xamarin Test Cloud](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) hello bulutta gerçek cihazlarda UI testi otomatikleştirir. Merhaba NUnit framework kullanarak uygulamanızı hello kullanıcı arabirimi aracılığıyla çalıştırma testleri yazma.

toouse Xamarin, hello dahil [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) SDK'sı bir NuGet paketi olarak gelir uygulamanıza. Xamarin şablonları ile Merhaba yeni test projeleri oluşturduğunuzda eklemiştir ve hello tanıtım uygulamasını göreceksiniz.

![Burada toofind hello hello arabirimde platformlar arası SDK](./media/iot-solution-build-system/image4.png)

Bir örnek test projesi hello deposundaki hello uygulama ile birlikte gelir. İçinde [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService), altında Ara [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/.

Visual Studio Team Services derleme kullanma, Xamarin UI birim testleri ve yapınızın bir parçası olarak çalıştırmak kolay toowrite olur.

## <a name="deploy-azure-services"></a>Azure Hizmetleri dağıtma
tooperform otomatik bir dağıtımını Azure Hizmetleri ve Team Services yapı hizmetlerine başvurun toohello ayrıntılı yönergeleri **scripts/README.md**.

Microsoft Azure toobuild bulut uygulamalarını kullanabileceğiniz çok sayıda farklı hizmetler sağlar. Birçok ayrı ayrı (App Service/Web uygulamaları gibi) kullanılabilse de, en iyi kendi olduğunda bunlar birbirine bağlı oldukları tooform tümleşik bir sistem gibi kullanırız MyDriving içinde.

Olası toocreate olduğundan ve Azure hizmetleri el ile birbirine, ancak çok daha hızlı ve daha güvenilir toouse Azure Resource Manager şablonları değil. [Resource Manager](../azure-resource-manager/resource-group-overview.md) çözümün kaynakları ve aralarındaki hello bağlantılar yapmadan hello dağıtımını otomatik hale getirir.

Merhaba GitHub deposundaki altında hello MyDriving sistemi hello şablonu bulacaksınız [betikleri/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Merhaba farklı hizmetleri bizim mimarisinde nasıl bağlandığına, kapsamlı ve kısa bir görünüm sağlar. Biz tüm bunlar ayrıntılı hello olarak açıklayan [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs), ancak yalnızca hello şablonu aracılığıyla kendisini okuyarak çok öğrenebilirsiniz.

> [!NOTE]
> Çoğu Azure Hizmetleri fiyatlandırma katmanı hello bağlı olarak ilişkili bir maliyeti vardır. Yeni tooAzure değilseniz, yapabilecekleriniz [ücretsiz denemenin](https://azure.microsoft.com/free/). Ancak, belirli hello MyDriving sistem bileşenlerinde toouse planlamıyorsanız emin tooremove olması bunları tooavoid yansıtılmasını maliyetleri. Hello "İşlem maliyetlerini tahmin" bölümünde bu makalede daha sonra tipik hizmet giderleri özetini sağlar.
> 
> 

### <a name="edit-hello-template"></a>Merhaba şablonunu düzenleyin.
toocustomize dağıtımınıza, belki de tooremove bileşenleri veya tooadd başkalarının gereksiz, önce bir senaryo kopyalarını\_complete.params.json ve senaryo\_complete.json hangi toomake değiştirir.

Merhaba senaryosunu kullanabilirsiniz\_complete.params.json dosya toooverride çeşitli varsayılan değerler, hello hizmet SKU veya hello depolama çoğaltma türü gibi aşağıdaki tablonun hello açıklandığı gibi. Merhaba varsayılan değerleri hello en düşük maliyeti seçenekleri seçin.

| **Parametre** | **Açıklama** | **Varsayılan değer** |
| --- | --- | --- |
| IOT hub'ı SKU |Azure IOT Hub hizmetin katmanı |F1 |
| Depolama hesabı türü |Depolama çoğaltma türü |Standart LRS |
| SQL hizmet hedefi |Eşzamanlılık yuvası tüketim |DW100 |
| Barındırma planı SKU |Uygulama hizmeti için hizmet planı |F1 |

Senaryoda\_complete.json:

* "BaseName" için arama ve tercih ettiğiniz tooa adını değiştirin.
* "Oluştur" arayın. Bu bölümlerin her birindeki bir kaynak oluşturur.
* SqlServerAdminLogin ve sqlServerAdminPassword toosuitable değerlerini ayarlayın.
* Bir kaynak oluşturur bir bölümü silmeden önce adını hello dosya başka bir yerinde için arama yaparak bağımlıları olup olmadığını denetleyin. Bir hizmet oluşturduğu her bölüm içerir Not bir *dependsOn* bağımlılıklarını listeleyen bölüm.

Merhaba şablonu yapılandırır burada ait. Ayrıntılar verilmektedir hello [Başvuru Kılavuzu](http://aka.ms/mydrivingdocs).

| **Hizmet** | **Açıklama ve ayrıntıları** |
| --- | --- |
| Depolama hesapları |Merhaba şablon üç hesapları oluşturur: |
| -Stream Analytics ' toplanan telemetri alır ve bu verileri API uç noktaları aracılığıyla kullanıma Azure App Service tablolar için hello yedekleme deposu olarak görev yapar bir SQL veritabanı. | |
| -Başka bir Stream Analytics işi, Hdınsight tarafından işlenen toobe geçmiş verileri öğelerden blob depolama. | |
| -Power BI ile kullanılmak üzere Hdınsight tarafından işlenen sonuçlarını alır bir SQL veritabanı. | |
| Azure IoT Hub'ı |Çift yönlü bağlantı tooeach bağlı bir aygıt oluşturur. Hello MyDriving çözümü, bir alan ağ geçidi toosend veri tooAzure IOT hub'ı hello mobil uygulama yapar. Azure IOT hub'ı sonra giriş tooStream Analytics görev yapar. |
| Azure Event Hubs |Bir çıkış sıraları Azure Service Fabric ile oluşturulan çıktı tooextensions hello Stream Analytics işi için. |
| Azure SQL Veri Ambarı | |
| Akış analizi işleri |Girişleri ve çıkışları kullanılan tooaggregate olan bir sorgu ile bağlanma hello App Service API'ları, Azure Machine Learning, uzantıları ve Power BI için gerçek zamanlı ve geçmiş verileri. |
| Machine Learning çalışma alanı |Denemeleri, R kodu ve API hizmeti içerir. |
| Azure Data Factory |Machine Learning yeniden eğitme zamanlanan. |
| Service Fabric barındırma planı |İçin Uzantılar. |
| Uygulama Hizmeti ("mobil uygulama") |Uç noktaları için mobil uygulama hello sağlar konakları hello Mobile Apps API projesi. Merhaba API kodunda dağıtılan tooApp Visual Studio hizmetinden olması gerekir. |
| Uyarı kuralları |Hataları Hello uygulama yanıtları gösteriyorsa, e-posta gönderir. |
| Application Insights |Merhaba App Service'te API performansını izlemek için. Visual Studio'da tooconfigure hello bağlantınız var. |
| Azure Key Vault |Merhaba web hizmeti küme sertifika kaydetmek için. |

### <a name="run-hello-template"></a>Merhaba şablonu çalıştırın
İçinde **scripts/README.md**, çalışan hello şablonu için ayrıntılı yönergeler de vardır.

tooprovision tüm hizmetlerin hello komut dosyası kullanarak kendi Azure hesabınızda aşağıdakilerden birini yapın aşağıdaki hello:

* PowerShell kullanın:
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *Konum* hello olan [Azure konumu](https://azure.microsoft.com/regions/), gibi `North Europe` veya `West US`. Kullanım `Get-AzureLocation` toofind kullanılabilir konumların bir listesini.
  * *resourceGroupName* tüm hello kaynaklara ait toogive toohello Grup istediğiniz hello adıdır. Merhaba kaynaklarla bittiğinde, bunları tüm birlikte bu grubu silmeden silebilirsiniz.
* DeploymentScripts/Bash/deploy.sh Bash ile çalıştırın.
* Açın ve hello Visual Studio çözümü DeploymentScripts/VS/DeployARM.sln oluşturun.

Her zaman hello şablonu çalıştırın, yeni bir isimle yeni bir kaynak kümesi oluşturur dikkat edin. toodelete hello kaynakları toohello portal gidin ve hello kaynak grubunu silebilirsiniz.

Merhaba betik herhangi bir nedenle başarısız olursa yeniden çalıştırabilirsiniz.

Visual Studio Team Services içinde sürekli tümleştirme yapılandırma seçeneği hello hello komut dosyası sağlar. Bir Team Services projesi ayarlarsanız, bir URL'ye sahip olacaksınız: https://yourAccountName.visualstudio.com. İstendiğinde hello tam URL'yi girin. Bir Team Services projesi için yeni veya var olan bir ad verebilirsiniz.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Yapı ayarlayın ve tanımları Visual Studio Team Services içinde test etme
Biz Team Services, derleme için çoğunlukla bu projede kullanın ve özelliklerini test. Ancak, ayrıca görev yönetimi Kanban panolarına ile gibi mükemmel işbirliği desteği sağlar, görevleri ve kaynak denetimi ile tümleşiktir ve geçişli kod gözden geçirme oluşturur. GitHub, Xamarin, HockeyApp ve doğal olarak, Visual Studio gibi diğer araçları ile iyi entegre olur. Hello web arabirimi veya Visual Studio aracılığıyla erişebilirsiniz, herhangi bir anda hangisi daha kullanışlı olur.

Hello adımları hello derleme ve sürüm tanımlarını kullanma hello Team Services içinde kullanılabilir eklenti hizmetleri, çeşitli [Market](https://marketplace.visualstudio.com/VSTS). Toplama toobasic yardımcı programları toorun komut satırları veya kopya dosyalarını, Xamarin, Android ve diğer satıcılar tarafından derlemeleri çağırma ve tooHockeyApp bağlanma hizmetleri vardır.

![Derleme seçenekleri Team Services](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Yapı tanımları
Derleme tanımları her hello ana hedef sahibiz. Özellik ve gerileme sınaması için değişimler de sunuyoruz. Bize vermektedir:

* MyDriving.Services (Merhaba mobil uygulama için hello arka uç web uygulaması)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android özelliği
  * MyDriving.Xamarin.Android regresyon
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS özelliği
  * MyDriving.Xamarin.iOS regresyon
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP özelliği
  * MyDriving.Xamarin.UWP regresyon

Bizim yapılandırmasının toosee hello tam ayrıntıları istiyorsanız hello 4.7 bölümüne bakın [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs), "Yapı ve sürüm yapılandırma." Merhaba izleyin aynı genel düzeni. Merhaba komut dosyası:

1. Merhaba NuGet paketi geri yükler. Merhaba ilk her yapı toorestore hello NuGet paketlerini gerekli adımlardır şekilde derlenmiş kod hello deposunda tutma.
2. Merhaba lisans etkinleştirir. Merhaba yapı gerçekleştirilir hello bulutta böylece bir lisans--ihtiyacımız Burada özellikle, Xamarin yapı hizmeti--hello için sahip olduğumuz tooactivate hello geçerli yapı makinesinde bizim lisans. Ardından, biz hemen daha sonra tooallow devre dışı, başka bir makinede kullanılan toobe.
3. Merhaba uygun hizmet kullanarak oluşturur. Merhaba mobil uygulamaları için Xamarin derlemeleri kullanırız ve hello arka uç web hizmeti için Visual Studio oluşturur.
4. Testleri oluşturur.
5. Testleri çalıştırır. Biz, Xamarin Test Cloud hello mobil uygulama testleri çalıştırın.
6. Merhaba derleme sonucu toohello bırakma konumu yayımlar.

Merhaba tetikleyici hello ana yapılar için toocontinuous tümleştirme ayarlanır. Diğer bir deyişle, kod toohello ana dalda denetlenir her zaman hello yapı çalıştırılır.

![Merhaba tetikleyici kümesi toocontinuous tümleştirme olduğu arabirimi](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Yayın tanımları
Sürüm tanımlarını ayarlandığı kadar hello aynı şekilde.

Merhaba web hizmeti için biz dağıtımı Azure web uygulaması olarak ayarlayın:

![Dağıtımı Azure web uygulaması olarak ayarlamak için arabirim](./media/iot-solution-build-system/image7.png)

Ve hello sürüm tetikleme toocontinuous dağıtım ayarlarız. Diğer bir deyişle, her iade arkasından bir güncelleştirme toohello web uygulaması başarılı yapı sonuçlanır.

![Merhaba sürüm tetikleme toocontinuous dağıtım ayarlamak için arabirim](./media/iot-solution-build-system/image8.png)

Mobil uygulamalarda, tooHockeyApp dağıtın:

![Bir mobil uygulama tooHockeyApp dağıtmak için arabirimi](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Application Insights kullanarak telemetri keşfedin
[Application Insights](../application-insights/app-insights-overview.md) hello performans ve kullanım, web hizmetleri hakkında telemetri toplar. Merhaba Application Insights SDK'sı telemetri hello hizmet toohello Azure Application Insights kaynağını gelen gönderir.

Toohello Application Insights kaynağı ayarlanan hello şablon göz atın. Burada, hello performansını grafiklerini keşfedebilirsiniz, [mobil uygulama hizmeti proje](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). Sunucu istek ve yanıt süreleri, hatalar, Göster ve özel durum sayar. Bağımlılık yanıt sürelerinin--diğer bir deyişle, çağrıları toohello veritabanı ve tooREST Machine Learning gibi API'leri grafikleri vardır. Performans sorunları varsa, hangi sisteminizin parçası neden olan mümkün toosee olacaktır.

![Örnek performans grafiği](./media/iot-solution-build-system/image11.png)

El ile ayarlanmış bir web hizmeti varsa, buna ait kolay tooget hello aynı grafik. Merhaba web hizmeti dikey penceresinde **Araçları** > **uzantıları** > **Ekle**. Seçin **Application Insights**.

![Application Insights tooget hello grafikleri seçme arabirimi](./media/iot-solution-build-system/image12.png)

Merhaba özelliği hello Application Insights SDK'sı ile uygulamanızı işaretlenerek çalışır.

Özel telemetri (veya gereç Azure dışında bir yerde çalışan bir uygulama) tarafından ekleyebileceğiniz [hello Application Insights SDK'sı ekleme](../application-insights/app-insights-asp-net.md) geliştirme zaman. Kullanıcıların ortalama seyahat uzunluğu veya toplam mesafe gibi hello uygulama bağımlı yararlı toolog ölçümleri budur. Visual Studio'da hello projesine sağ tıklayın ve ardından **Application Insights Ekle**.

![Application Insights Ekle tooadd özel telemetri seçme arabirimi](./media/iot-solution-build-system/image10.png)

Olağan dışı sayıda yanıtı hatası görürse application Insights uyarı e-postalar gönderin. Yanıt süreleri gibi çeşitli ölçümleri kendi uyarılar ayarlayabilirsiniz.

Yalnızca toobe web hizmetiniz her zaman açık ve çalışır ayarlayabilirsiniz emin [kullanılabilirlik testleri](../application-insights/app-insights-monitor-web-app-availability.md). Bu testler sitenizi Merhaba Dünya çeşitli konumlardan 15 dakikada bir ping işlemi uygulayın. Yeniden toobe bir sorun görünüyorsa bir e-posta alırsınız.

## <a name="estimate-operational-costs"></a>İşlem maliyetlerini tahmin etme
Bu çok pahalı olmayan toorun küçük ölçekli bunun gibi bir uygulama olur. Böylece geliştirme ve küçük ölçekli işlemi çok az maliyet hello Hizmetleri çoğunun ücretsiz giriş düzeyi katman vardır. Ve Elbette, kendi içinde MyDriving tüm hello özellikleri gösterilen toouse uygulamanız yok.

Burada, kabaca bir hello geliştirme yapılandırma MyDriving için ayarlanması bizim maliyetleri tahmin verilmiştir. Biz de yaptığımız bazı alternatifleri not *değil* kullanın. Kendi maliyetleri tahmin olarak bu bilgiler faydalı olabilir.

Biz varsayın:

* Beşten fazla ekibi (artı Paydaşlar Gözlemleme).
* Bir ay hakkında daha fazla çalıştırmak için.
* dört dönüşleri günde 100 kullanıcılarla.

> [!NOTE]
> Yeni tooAzure iseniz var. bir [ücretsiz bir hesap](https://azure.microsoft.com/free/).
> 
> 

| **Hizmet/bileşeni** | **Notlar** | **Maliyet/ay** |
| --- | --- | --- |
| [Visual Studio 2015 topluluk](https://www.visualstudio.com/products/visual-studio-community-vs) ile [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Platformlar arası geliştirme ortamı |Visual Studio Community. (Gerek [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) için [Xamarin.Forms](https://xamarin.com/forms), toodesign platformlar arası tek bir kod tabanının.) |$0 |
| [Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>İki yönlü veri bağlantısı toodevices |8000 iletileri + 0,5 KB/ileti boş. |$0 |
| [Akış Analizi](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   Yüksek hacimli akış veri işleme |$ Etkin durumdayken, saat başına birim akış başına 0,031 gider. Merhaba istediğiniz akış birim sayısını seçin; Daha fazla tooscale ayarlama. |$23 |
| [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> Uyarlamalı yanıtları |10/bilgisayar/ay. <br/>                                                                                                                                                                                 + 3 saatlik deneme \* $1 / denemeler saat. <br/>                                                                                                                                                           + 3.5 saatlik API CPU \* 2 $ / üretim CPU saat. <br/>                                                                                                                                                          Bu daha fazla giriş verilerle yükselmeye ancak API CPU süresi 5 min/gün yeniden eğitme, varsayar.                   <br/>                                                                                                                                                                     + 2 min/gün tooprocess 400 dönüşleri/gün Puanlama. |$20 |
| [App Service](https://azure.microsoft.com/pricing/details/app-service/)  <br/> Mobil arka uç için ana bilgisayar |Katman B1--üretim web uygulamaları. |$56 |
| [Visual Studio Team Services](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/> Yapı, birim test ve yayın Yönetimi; görev yönetimi |Özel aracılar, beş kullanıcılar. |$0 |
| [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>Performans ve web hizmetleri ve siteleri kullanımını izleme |Ücretsiz katmanı. |$0 |
| [HockeyApp](http://hockeyapp.net/pricing/) <br/> Dağıtım beta uygulamaları ve geri bildirim, kullanım ve kilitlenme verilerini toplama |İki yeni kullanıcılara yönelik uygulamaların boş.<br/> $30/ ay bundan sonra. |$0 |
| [Xamarin](https://store.xamarin.com/)<br/> Birden çok aygıt için Tekdüzen bir platform kodu |Ücretsiz deneme. <br/>$25/ ay bundan sonra. |$0 |
| [SQL veritabanı](https://azure.microsoft.com/pricing/details/sql-database/) Azure uygulama hizmeti |Temel katman; tek veritabanı modeli. |$5 |
| [Service Fabric](https://azure.microsoft.com/pricing/details/service-fabric/) (isteğe bağlı) |Yerel küme çalıştırın. |$0 |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/> Akış ve statik veri araştırma ve çok yönlü görüntüler |Ücretsiz katmanı: 1 GB, 10.000 satır/saatlik, günlük yenileme. <br/> Kullanıcı/10/ay için [daha yüksek sınırları](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/), işbirliği, bağlantı seçenekleri. |$0 |
| [Depolama](https://azure.microsoft.com/pricing/details/storage/) |L (yerel olarak yedekli) &lt; 100 G $0.024/GB. |$3 |
| [Data Factory](https://azure.microsoft.com/pricing/details/data-factory/) |Etkinlik başına 0.60 \* (8-5 FOC). |$2 |
| [Hdınsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>  Günlük yeniden eğitme için isteğe bağlı küme |$0.32/ saat 1 saat her gün için üç A3 düğümlerde * 31 gün. |$30 |
| [Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/) |Temel $11/ ay işleme birimi + $0,028 giriş. |$11 |
| OBD donanım kilidi | |$12 |
| **Toplam** | |**$157** |

Daha fazla bilgi için bkz.

* Özeti [Azure hizmeti kotalar ve sınırlar](../azure-subscription-service-limits.md#iot-hub-limits)
* Azure [fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>Bize geri bildirimlerinizi gönderin
Kendi IOT sistemleri MyDriving toohelp başkalarından oluşturduğumuz çünkü kesinlikle ne kadar iyi çalıştığı konusunda toohear sizden istiyoruz. Varsa bize bildirin:

* İlgili sorunlar veya zorluklar çalıştırın.
* Daha uygun tooyour senaryo yapacağı bir uzantı noktası yoktur.
* Belirli gereksinimlerini daha verimli bir şekilde tooaccomplish bulun.
* MyDriving veya bu belgeleri geliştirmek için diğer bir önerileri vardır.

toogive geri bildirim [sorunu] github'da dosya ya da bir yorum yazın (en-us edition).

Toohearing sizden umuyoruz!

## <a name="next-steps"></a>Sonraki adımlar
Merhaba öneririz [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs), kapsamlı bir açıklama hello sistem ve onun bileşenlerinin hello tasarımının olduğu.

