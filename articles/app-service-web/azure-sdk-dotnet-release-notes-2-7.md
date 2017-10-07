---
title: "aaaAzure .NET 2.7 ve .NET 2.7.1 için SDK'sı sürüm notları"
description: ".NET 2.7 ve 2.7.1 için Azure SDK sürüm notları"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: 877d070a-9bd5-49b3-8fac-6bb5f65c3554
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 8ec72b0f18702e6d811f0cbe4790685be7881d96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-27-and-net-271-release-notes"></a>.NET 2.7 ve 2.7.1 için Azure SDK sürüm notları
## <a name="overview"></a>Genel Bakış
Bu belge .NET 2.7 yayımı için Azure SDK'sı hello hello sürüm notları içeriyor. 

Merhaba belge de içeren hello Sürüm Notları'hello Azure SDK'sı için .NET 2.7.1 yayın için.

Azure SDK 2.7 yalnızca Visual Studio 2015 ve Visual Studio 2013 de desteklenir. [Azure SDK 2.6](https://azure.microsoft.com/downloads/) olan hello son SDK Visual Studio 2012 için desteklenir.

Bu sürüm hakkında ayrıntılı bilgi için bkz: [Azure SDK 2.7 duyuru post](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) ve [Azure SDK'sı 2.7.1 duyuru post](http://go.microsoft.com/fwlink/?LinkId=623850).

## <a name="azure-sdk-for-net-27"></a>.NET 2.7 için Azure SDK’sını
### <a name="sign-in-improvements-for-visual-studio-2015"></a>Oturum açma için Visual Studio 2015 geliştirmeleri
Visual Studio 2015 için Azure SDK 2.7 Visual Studio 2015'te hello yeni kimlik yönetimi özelliklerini destekler.  Azure rol tabanlı erişim denetimi, bulut çözüm sağlayıcıları, DreamSpark ve diğer hesap ve abonelik türleri üzerinden erişim hesapları için destek içerir.

oturum açma hello geliştirmeleri ile Azure SDK 2.7 dahil, yalnızca Visual Studio 2015'te kullanılabilir. Desteği Visual Studio 2013 için Azure SDK 2.7.1 dahil edilmiştir.

### <a name="mobile-sdk"></a>Mobil SDK'sı
Güncelleştirilmiş **Mobile Apps** şablonları tooreflect yeni [NuGet paketi](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) ve Kurulum işlemi.

### <a name="service-bus"></a>Service Bus
Genel hata düzeltmeleri ve geliştirmeler yapılmıştır. Güncelleştirmeler ve özellikler hakkında daha fazla ayrıntı için lütfen en son hello toohello sürüm notlarını başvurun [Service Bus NuGet](http://www.nuget.org/packages/WindowsAzure.ServiceBus/).

### <a name="hdinsight-tools"></a>Hdınsight araçları
Bu sürüm hello aşağıdaki güncelleştirmeler yapılmıştır. Bu güncelleştirmeler önizlemede. Daha fazla bilgi için bkz: [bu blog](http://go.microsoft.com/fwlink/?LinkId=619108).

* Tez işlerinde Hive için Hive grafikleri
* Tam yığını DML IntelliSense desteği
* Pig şablon desteği
* Azure Hizmetleri için Storm şablonları

#### <a name="breaking-changes"></a>Yeni değişiklikler
* Eski **Storm** hello araçları bu sürümünü kullanırken, proje yükseltilmelidir. Daha fazla bilgi için bkz: [bu blog](http://go.microsoft.com/fwlink/?LinkId=619108).
* Visual Studio Web Express artık desteklenmiyor. Daha fazla bilgi için bkz: [bu blog](http://go.microsoft.com/fwlink/?LinkId=619108).

### <a name="azure-app-service-tools"></a>Azure uygulama hizmeti araçları
Bu sürüm hello tooWeb araç uzantıları aşağıdaki güncelleştirmeler yapılmıştır. Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) blogu. 

* Eklenen DreamSpark hesaplarına desteği
* Tam tooAzure yeni Azure Resource Management API'leri hello toosupport yapılan araçları değiştirme
* Azure uygulama hizmeti desteği eklendi çok[bulut Gezgini](#cloud_explorer)

#### <a name="known-issues"></a>Bilinen sorunlar
Web uygulama dağıtım yuvası düğümleri Sunucu Gezgini hello yuvaları düğümünde görünmez ve Web uygulaması dağıtım yuvası alt düğümleri altında Cloud Explorer yükleme. Bu sorun çözümlendi ve hello sonraki SDK sürüm için hazır. 

### <a name="cloud_explorer"></a>Visual Studio 2015 için bulut Gezgini
Visual Studio içinde anahtar Geliştirici eylemler gerçekleştirmek ve bunların özelliklerini inceleyin veya Azure SDK 2.7 Cloud Explorer tooview sağlayan Visual Studio 2015 için Azure kaynaklarınızı içerir. 

Cloud explorer hello aşağıdakileri destekler:

* Azure kaynaklarınızı kaynak grubu ve kaynak türü görünümleri 
* Kaynak (kaynak türü görünümünde kullanılabilen) ada göre ara
* Abonelikler ve rol tabanlı erişim denetimi (uygulanan RBAC) sahip kaynakları desteği 
* Geliştirici odaklı Eylemler belirli tooselected kaynakları gösterir tümleşik eylem panel. Örneğin: kullanılarak oluşturulan sanal makinelerin Kaynak Yöneticisi yığını, tanılama verilerini görüntülemek için sanal makineleri vb. hello için uzaktan hata ayıklayıcı ekleyin.
* Yaygın olarak geliştirme ve test sırasında gereken Geliştirici odaklı özellikleri gösteren tümleşik özellikleri paneli 
* Hızlı hello hesap toouse kaynakları (araç çubuğunda ayarlar komutunu kullanın) numaralandırılırken değiştirme 
* (Araç çubuğunda ayarlar komutunu kullanın) kaynakları numaralandırılırken abonelikleri toouse filtreleme 
* Kaynaklar ve kaynak grupları, yönetimi için ayrıntılı bağlantılar toohello Azure portalı 

### <a name="azure-resource-manager-tools"></a>Azure Kaynak Yöneticisi Araçları
Hello Azure Kaynak Yöneticisi Araçları rol tabanlı erişim denetimi (RBAC) ve yeni abonelik türlerle güncelleştirilmiş toowork olmuştur.  Bu değişikliklerle hello özelliği toouse yeni depolama, ayrıca tooclassic depolama toostore yapıları dağıtımı sırasında hesaplarını içerir.  

Bir Azure kaynak grubu projesi hello SDK önceki bir sürümünden SDK 2.7 hello ile kullanıyorsanız, yeni bir dağıtım komut dosyası yerine Klasik depolama yeni bir depolama hesabı kullanarak gerekli toodeploy ' dir.  Tooyour proje tooadd hello yeni betik değişiklikler yapılmadan önce sizden istenir.  Merhaba eski betik adlandırılacak ve ihtiyacınız olacak toomanually toohello yeni betik herhangi bir değişiklik yapın.

### <a name="storage-explorer-tools"></a>Depolama Gezgini araçları
* Ek Bloblarını görüntüleme desteği. Daha fazla bilgisini [bu blog gönderisine](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/04/13/introducing-azure-storage-append-blob.aspx). 
* Premium depolama hesapları Sunucu Gezgini üzerinden görüntüleme desteği. Premium depolama hesapları için yalnızca desteklenen hello türü oldukları gibi Sunucu Gezgini yalnızca premium storage hesapları sayfa bloblarını görüntülenir.

### <a name="azure-data-factory-tools-for-visual-studio"></a>Visual Studio için Azure Data Factory araçları
Giriş **Azure Data Factory Araçları** Visual Studio için. Etkin hello özellikleri aşağıda verilmiştir. Bkz: [bu blog](http://go.microsoft.com/fwlink/?LinkId=617530) daha fazla bilgi için.

* **Şablona dayalı geliştirme**: kullanım ortası tabanlı şablonlar, veri taşıma şablonları veya veri işleme şablonları toodeploy uçtan uca veri tümleştirme çözümünü seçin ve uygulamalı hızla Data Factory ile çalışmaya başlama. 
* **Geliştirme ve Data Factory varlıklarını dağıtmak için Çözüm Gezgini ile tümleştirme**: oluşturmak ve ardışık düzen ve ilgili varlık Visual Studio projeleri olarak dağıtın. 
* **Geliştirme sırasında visual etkileşim için diyagram görünümü ile tümleştirme**: görsel olarak ardışık düzen ve yardımcı hello diyagram görünümü gelen veri kümeleriyle yazar. 
* **Gözatma ve zaten dağıtılmış varlıklar etkileşim için Sunucu Gezgini ile tümleştirme**: Dengeleme hello Sunucu Gezgini toobrowse zaten Dağıtılmış veri fabrikaları ve karşılık gelen varlık. Dağıtılan data factory veya herhangi bir varlığa (ardışık düzen, bağlantılı hizmet, veri kümeleri) projenize içeri aktarın. 
* **JSON şema doğrulama ve zengin IntelliSense ile düzenleme**: verimli bir şekilde yapılandırın ve Data Factory varlıklarını zengin IntelliSense ve şema doğrulama ile JSON belgelerinin Düzenle 
* **Çoklu ortam yayımlama**: yazılan ardışık düzen toodev, test ortamında veya üretim ortamında her ortam için ayrı yapılandırma dosyası oluşturarak yayımlayın.
* **Pig, Hive ve .net tabanlı veri işleme Destek**: Pig ve Data Factory projesindeki Hive betikler için destek. .Net yönetmek için C# projesine başvurma desteği etkinlik.

## <a name="azure-sdk-for-net-271"></a>.NET 2.7.1 İçin Azure SDK
bölümden hello .NET 2.7.1 yayın için Azure SDK'sı hello ile kullanıma sunulan güncelleştirmeleri içerir.

### <a name="hdinsight-tools"></a>Hdınsight araçları
Daha ayrıntılı Hdınsight araçları güncelleştirmeleri hakkında açıklama için bkz: [bu blog](http://go.microsoft.com/fwlink/?LinkId=623831).

* Hive işi işleci görünümü (yeni bir özellik)
  
    Merhaba Hive işleci görünümü özelliği, Hive sorgusu daha iyi anlamak toohelp eklendi. toosee bir köşe tüm hello işleçleri çift tıklayarak hello iş grafiği hello köşelerinin. tooview belirli bir işlecin ilgili daha fazla ayrıntı işleç getirin.
* Hive hata işaret (yeni bir özellik)
  
    tooenable, tooview hello dilbilgisi hataları hemen hello Hive hata işaret özelliği eklendi. Ayrıca, hata iletileri Gelişmiş ve ayrıntılı dilbilgisi hataları hemen şimdi görebilirsiniz (Bu sürümde kadar toosubmit bir Hive betiği toohello küme ve hata iletisi hakkında ayrıntıları alınıyor önce bir süre bekleyin yaşadığınız).  
* Storm topolojisini grafik (yeni bir özellik)
  
    Topolojiniz beklendiği gibi çalışıp çalışmadığını toosee istediğinizde, görselleştirme çok önemlidir. Bu sürümde Storm grafiklerde görselleştirme eklendi. Topolojiniz için hello önemli ölçümleri görselleştirebilirsiniz (örneğin, bir renk hava durumu belirli bir Cıvata "meşgul" olmadığını gösterir). Çift hello Cıvata/Spout tooview daha fazla ayrıntı tıklatabilirsiniz.
* Hello Azure Portal (hata düzeltmesi) oluşturulan Hdınsight kümeleri için destek
  
    Şimdi, Visual Studio tooview kullanın ve burada hello küme oluşturulmuş olsun, Hdınsight kümeleri işleri tooall gönderin.
* Daha fazla IntelliSense desteği & daha hızlı Hive meta veri yükleme (Geliştirme)
  
    Daha fazla kullanıcı dostu önerileri ekleyerek biz hello IntelliSense iyileştirilmiştir. Sorgunuzu daha kolay yazmak için örneğin, tablo diğer şimdi de IntelliSense içinde önerilebilir. Ayrıca, biz hello kovan meta iyileştirilmiştir, yalnızca birkaç sürer şekilde yüklenirken saniye toolist tüm hello veritabanları, tabloları ve sütunları Hive meta depo.

Daha ayrıntılı Hdınsight araçları güncelleştirmeleri hakkında açıklama için bkz: [bu blog](http://go.microsoft.com/fwlink/?LinkId=623831).

### <a name="improvements-in-visual-studio-2013"></a>Visual Studio 2013'te geliştirmeleri
* Azure SDK'sı 2.7.1 Visual Studio 2013 tooaccess Azure hesapları ve rol tabanlı erişim denetimi, bulut çözüm sağlayıcıları ve Dreamspark aracılığıyla abonelikleri etkinleştirir.
* Azure SDK'sı ile 2.7.1, hello yeni bulut Explorer araç penceresi de Visual Studio 2013'te kullanıma sunulmuştur.

### <a name="known-issues"></a>Bilinen sorunlar
Hello Azure SDK 2.6 veya 2.7.1 için Visual Studio Community 2013 bir olmayan - İngilizce işletim sisteminde yükleme İngilizce hello bir uyarı görüntülenir ve Visual Studio'nun İngilizce olmayan kaynakları uyumsuzluğu. Bu uyarı güvenli bir şekilde kapatıldığında. Yalnızca hello makine Visual Studio Community 2013 önceki bir yüklemesini içermiyor ve bir harici - İngilizce işletim sisteminde hello SDK yüklemekte olduğunuz ortaya çıkar. Merhaba uyarı hello RTM kaynakları tooVisual Studio hello dil paketi uyguladıktan sonra ancak güncelleştirme 4 uygulanmadan önce gösterilir. Merhaba uyarı durdurulduğundan hello dil paketi toocontinue ve hello dil paketi eksiksiz uygulanan hello güncelleştirme 4 sürümü içerik izin verir.

LightSwitch projeleri bu sürümle uyumlu değildir. Bu sorunu sonraki SDK sürüm hello ile çözümlenir.

## <a name="also-see"></a>Ayrıca bkz.
[Azure SDK'sı 2.7.1 duyuru post](http://go.microsoft.com/fwlink/?LinkId=623850)

[Azure SDK 2.7 duyuru post](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)

[Destek ve devre dışı bırakma bilgi hello .NET ve API'ler için Azure SDK'sı için](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

