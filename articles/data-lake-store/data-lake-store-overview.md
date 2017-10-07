---
title: Azure Data Lake Store aaaOverview | Microsoft Docs
description: "Diğer veri depolarına kıyasla sağladığı Azure Data Lake Store ve hello değeri anlamak"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Azure Data Lake Store'a genel bakış
Azure Data Lake Store, büyük veri analitik iş yükleri için kuruluş çapında hiper ölçekli bir depodur. Azure Data Lake, işletimsel ve keşifsel analiz için tek bir konumda herhangi boyutu, türü ve alım hızına toocapture veri sağlar.

> [!TIP]
> Kullanım hello [Data Lake Store öğrenme yolunu](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/) hello Azure Data Lake Store hizmetini keşfetmeye toostart.
> 
> 

Azure Data Lake Store Hadoop'tan erişilebilir (Hdınsight kümesi ile kullanılabilir) kullanarak hello WebHDFS ile uyumlu REST API'leri. Özel olarak tasarlanmış tooenable Analytics hello depolanan verileri ve performans veri analizi senaryoları için ayarlanmış. İsteğe bağlı olarak Hello kutudan çıktığında, tüm hello Kurumsal düzeydeki özellikleri içerir — güvenlik, yönetilebilirlik, ölçeklenebilirlik, güvenilirlik ve kullanılabilirlik — gerçek Kurumsal kullanım vakaları için gerekli.

![Azure Data Lake](./media/data-lake-store-overview/data-lake-store-concept.png)

Bazı hello Azure Data Lake anahtar özelliklerini hello hello şunları içerir.

### <a name="built-for-hadoop"></a>Hadoop için geliştirilmiştir
Hello Azure Data Lake store, Hadoop dağıtılmış dosya sistemi (HDFS ile) uyumlu bir Apache Hadoop dosya sistemidir ve hello Hadoop ekosistemi ile çalışır.  Varolan Hdınsight uygulamaları ya da hello WebHDFS API kullanan hizmetler Data Lake Store ile kolayca tümleştirilebilir. Ayrıca, Data Lake Store uygulamalar için WebHDFS ile uyumlu bir REST arabirimini kullanıma sunar.

Data Lake Store içinde depolanan veriler, MapReduce veya Hive gibi Hadoop analitik çerçeveler kullanılarak kolayca çözümlenebilir. Microsoft Azure Hdınsight kümeleri sağlanabilir ve toodirectly Data Lake Store'da depolanan verilere erişmek yapılandırılır.

### <a name="unlimited-storage-petabyte-files"></a>Sınırsız depolama, petabayt boyutlu dosyalar
Azure Data Lake Store, sınırsız depolama sağlar ve analiz için çeşitli verilerin depolanmasına uygundur. Hesap boyutları, dosya boyutları veya bir veri gölü içinde depolanabilen veri miktarı hello herhangi bir sınır getirmez. Tek tek dosyaların herhangi bir türde veri kilobayt toopetabytes harika seçim toostore kolaylaştırarak boyutu değişebilir. Veri, işlemi birden çok kopya depolanır ve hangi Merhaba veri hello veri gölü içinde depolanabilen hello süre bir sınırlama yoktur.

### <a name="performance-tuned-for-big-data-analytics"></a>Büyük veri analizi için performans ayarı yapılmıştır
Azure Data Lake Store, büyük ölçekli, çok büyük verim tooquery gerektirir ve büyük miktarlarda verinin çözümlemek analitik sistemlerin çalıştırılması için geliştirilmiştir. Merhaba veri gölü, bir dosyanın parçalarını birkaç ayrı depolama sunucusu yayar. Bu işleme veri analizinin gerçekleştirilmesi hello dosyasında paralel okurken okunan hello artırır.

### <a name="enterprise-ready-highly-available-and-secure"></a>Kurumsal kullanıma hazırdır: Yüksek kullanılabilirliğe sahip ve güvenlidir
Azure Data Lake Store, endüstri standardı kullanılabilirlik ve güvenilirlik sağlar. Veri varlıklarınız, herhangi bir beklenmeyen arızaya karşı yedek kopyaları tooguard yaparak işlemi depolanır. Kuruluşlar Azure Data Lake'i kendi çözümlerinde, var olan bir veri platformunun önemli bir parçası olarak kullanabilir.

Data Lake Store ayrıca hello depolanan veriler için kurumsal düzeyde güvenlik sağlar. Daha fazla bilgi için bkz. [Azure Data Lake Store'da verilerin güvenliğini sağlama](#DataLakeStoreSecurity).

### <a name="all-data"></a>Tüm Veriler
Azure Data Lake Store tüm verileri yerel biçiminde, olduğu gibi ve önceden yapılması gereken herhangi bir dönüştürme işlemi gerektirmeden depolayabilir. Data Lake Store değil toohello ayrı analitik çerçeveye toointerpret hello verileri bırakarak hello veriler yüklenmeden önce tanımlı bir şeması toobe gerektirir ve bir şema hello analiz hello aynı anda tanımlayın. İsteğe bağlı boyut ve biçimleri mümkün toostore dosyaları olan yapılandırılmış, Data Lake Store toohandle için yarı yapılandırılmış ve yapılandırılmamış veri mümkün kılar.

Verilere yönelik Azure Data Lake Store kapsayıcıları esasen klasör ve dosyadır. SDK'ları, Azure portalı ve Azure Powershell kullanarak hello depolanan veri üzerinde çalışır. Verilerinizi bu arabirimleri kullanarak ve hello ilgili kapsayıcıları kullandığınız hello depoya yerleştirdiğiniz sürece, istediğiniz türde veriyi depolayabilirsiniz. Data Lake Store Merhaba, depoladığı verilerin türüne göre verilerin hiç bir özel işleme gerçekleştirmez.

## <a name="DataLakeStoreSecurity"></a>Azure Data Lake Store'da verilerin güvenliğini sağlama
Azure Data Lake Store Azure Active Directory kimlik doğrulaması için kullanır ve erişim denetim listeleri (ACL'ler) toomanage erişim tooyour veri.

| Özellik | Açıklama |
| --- | --- |
| Kimlik Doğrulaması |Azure Data Lake Store, Azure Data Lake Store içinde depolanan tüm hello veriler için kimlik ve erişim yönetimi için Azure Active Directory'ye (AAD) tümleştirir. Merhaba tümleştirmesi, çok faktörlü kimlik doğrulaması, koşullu erişim, rol tabanlı erişim denetimi, uygulama kullanımını izleme, izleme ve uyarı, güvenlik dahil olmak üzere tüm AAD özelliklerinden Azure Data Lake avantajları sonucunda vb.. Azure Data Lake Store hello REST arabirimi içinde kimlik doğrulaması için hello OAuth 2.0 protokolünü destekler. |
| Erişim denetimi |Azure Data Lake Store, WebHDFS protokolünün hello tarafından kullanıma sunulan POSIX tipi izinleri destekleyerek erişim denetimi sağlar. Hello Data Lake Store genel Önizlemesi (Merhaba geçerli sürüm), ACL hello kök klasör, alt klasörler ve dosyaları tek tek etkinleştirilebilir. Data Lake Store bağlanımda ACL’lerin nasıl çalıştığı üzerine daha fazla bilgi için bkz. [Data Lake Store’da erişim denetimi](data-lake-store-access-control.md). |
| Şifreleme |Data Lake Store ayrıca hello hesapta depolanan veriler için şifreleme sağlar. Bir Data Lake Store hesabı oluşturulurken hello şifreleme ayarlarını belirtin. Şifreleme için kabul veya seçtiğiniz toohave şifrelenmiş verilerinizi kullanabilirsiniz. Hakkında daha fazla bilgi için tooprovide şifreleme ilgili yapılandırma için bkz: [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md). |

Data Lake Store'da verilerin güvenliğini sağlama hakkında daha fazla toolearn istiyor. Merhaba bağlantıları izleyin.

* Yönergeler için Data Lake Store'da toosecure verileri görmek [Azure Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md).
* Videoyu mu tercih ediyorsunuz? [Bu videoyu izleyin](https://mix.office.com/watch/1q2mgzh9nn5lx) Data Lake Store'da toosecure verilerin depolanma üzerinde.

## <a name="applications-compatible-with-azure-data-lake-store"></a>Azure Data Lake Store ile uyumlu uygulamalar
Azure Data Lake Store hello Hadoop ekosistemindeki çoğu açık kaynak bileşenle uyumludur. Ayrıca diğer Azure hizmetleriyle sorunsuz şekilde tümleştirilir. Bu da Data Lake Store'u veri depolama ihtiyaçlarınız için ideal bir seçenek yapar. Toolearn Data Lake Store hem açık kaynak bileşenlerle yanı sıra diğer Azure hizmetleriyle nasıl kullanılabileceği hakkında daha fazla bilgi aşağıda Hello bağlantıları izleyin.

* Data Lake Store ile birlikte çalışabilen açık kaynak uygulamaların listesi için bkz. [Azure Data Lake Store ile uyumlu uygulamalar ve hizmetler](data-lake-store-compatible-oss-other-applications.md).
* Bkz: [diğer Azure hizmetleriyle tümleştirme](data-lake-store-integrate-with-other-services.md) toounderstand nasıl Data Lake Store kullanılabilir diğer Azure Hizmetleri tooenable geniş bir senaryo.
* Bkz: [Data Lake Store kullanma senaryoları](data-lake-store-data-scenarios.md) toouse Data Lake depolama, veri alma gibi senaryolarda nasıl toolearn veri işleme, veri indirme ve veri görselleştirme.

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>Azure Data Lake Store dosya sistemi (adl://) nedir? 
Data Lake Store hello yeni dosya sistemi erişilen, hello AzureDataLakeFilesystem (adl: / /), Hadoop ortamlarında (Hdınsight kümesiyle kullanılabilir). Uygulama ve hizmetlere adl kullanın: / / mümkün tootake avantajı, geçerli olarak WebHDFS şu anda kullanılabilir olmayan ek performans en iyi duruma getirme. Sonuç olarak, Data Lake Store verir esneklik tooeither hello hello en iyi performansı önerilen seçenek olan Adl hello ile kullanılabilir kredi: / / veya var olan kodu devam ediliyor toouse hello WebHDFS API tarafından doğrudan güncelleştirin. Azure Hdınsight tam olarak hello AzureDataLakeFilesystem tooprovide hello en iyi performansı Data Lake Store yararlanır.

Verilerinizi Data Lake Store hello kullanarak erişebilirsiniz `adl://<data_lake_store_name>.azuredatalakestore.net`. Tooaccess hello Data Lake Store verileri nasıl hello daha fazla bilgi için bkz: [hello özelliklerini görüntüleme depolanan verileri](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>Azure Data Lake Store'u kullanmaya nasıl başlarım?
Bkz: [hello Azure Portal kullanarak Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md), nasıl Azure Portal kullanarak bir Data Lake Store tooprovision hello üzerinde. Azure Data Lake sağladıktan sonra öğrenebilirsiniz nasıl toouse büyük veri olanaklarının Azure Data Lake Analytics veya Azure Hdınsight Data Lake Store ile gibi. Ayrıca, bir .NET uygulama toocreate bir Azure Data Lake Store hesabı oluşturma ve karşıya yükleme, indirme veri vb. gibi işlemler gerçekleştirmek.

* [Azure Data Lake Analytics ile Çalışmaya Başlama](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
* [.NET SDK'yı kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Data Lake Store videoları
Videolar toolearn izlemeyi tercih ederseniz, Data Lake Store videoları çeşitli özellikler sağlar.

* [Azure Data Lake Store hesabı oluşturma](https://mix.office.com/watch/1k1cycy4l4gen)
* [Azure Data Lake Store'da Hello Veri Gezgini tooManage veri kullanın](https://mix.office.com/watch/icletrxrh6pc)
* [Azure Data Lake Analytics tooAzure Data Lake Store Bağlan](https://mix.office.com/watch/qwji0dc9rx9k)
* [Azure Data Lake Store'a Data Lake Analytics üzerinden erişme](https://mix.office.com/watch/1n0s45up381a8)
* [Azure Hdınsight tooAzure Data Lake Store Bağlan](https://mix.office.com/watch/l93xri2yhtp2)
* [Azure Data Lake Store'a Hive veya Pig üzerinden erişme](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [Azure Data Lake Deposu'ndan veri Distcp'yi (Hadoop dağıtılmış kopya) toocopy veri tooand kullanın](https://mix.office.com/watch/1liuojvdx6sie)
* [İlişkisel kaynaklar ile Azure Data Lake Store arasında Apache Sqoop toomove veri kullanın](https://mix.office.com/watch/1butcdjxmu114)
* [Azure Data Lake Store için Azure Data Factory'yi kullanarak Veri Düzenlemesi](https://mix.office.com/watch/1oa7le7t2u4ka)
* [Hello Azure Data Lake Store verilerin güvenliğini sağlama](https://mix.office.com/watch/1q2mgzh9nn5lx)

