---
title: aaaWhat olan Azure Analysis Services | Microsoft Docs
description: "Analysis Services Hello büyük resmi Azure'da alın."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>Azure Analysis Services nedir?
![Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure Analysis Services hello bulutta modelleme Kurumsal düzeyde verileri sağlar. Bu tümüyle yönetilen bir hizmet olarak platformdur (PaaS) ve Azure veri platformu hizmetleriyle tümleştirilmiştir. 

Analysis Services ile birden fazla kaynaktan veri birleştirebilir, ölçümlerini tanımlayabilir ve tek, güvenilen bir anlam veri modelinde verilerinizin güvenliğini sağlayabilirsiniz. Hello veri modeli, Power BI, Excel, Raporlama Hizmetleri, üçüncü taraf ve özel uygulamalar gibi istemci uygulamalarını verilerle oldukça büyük miktardaki, kullanıcıların toobrowse için daha kolay ve hızlı bir yol sağlar.

![Veri kaynakları](./media/analysis-services-overview/aas-overview-data-sources.png)

Kullanıma [bu videoyu](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4) Azure Analysis Services ile Microsoft nasıl uyum sağladığı toolearn genel BI özellikleri ve nasıl hello bulutunu, veri modelleri alma yararlı olabilir.

## <a name="built-on-sql-server-analysis-services"></a>SQL Server Analysis Services’ı temel alır
Azure Analysis Services, SQL Server Analysis Services Enterprise Edition’da bulunan harika özelliklerin çoğu ile uyumludur. Azure Analysis Services tablolu modellere hello 1200 ve 1400 destekleyen [Uyumluluk Düzeyleri](analysis-services-compat-level.md). Bölümler, satır düzeyinde güvenlik, çift yönlü ilişkiler ve çeviriler gibi özelliklerin tümü desteklenir. Bellek içi ve DirectQuery modları, çok büyük ve karmaşık veri kümeleri üzerinde ışık hızında sorgular anlamına gelir.

Tablosal modeller hızlı geliştirme sunar ve bunlar üst düzeyde özelleştirilebilir. Geliştiriciler için tablolu modeller hello tablo nesne modeli (ZEL) toodescribe model nesneleri içerir. ZEL hello JSON'de açığa [tablolu modeli komut dosyası dili (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) ve hello AMO veri tanımlama dili hello aracılığıyla [Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) ad alanı.

## <a name="better-with-azure"></a>Azure'la daha iyi
Azure Analysis Services toobuild etkinleştirme birçok Azure hizmetleriyle tümleşen Gelişmiş bir analiz çözümleri. İle tümleştirme [Azure Active Directory](../active-directory/active-directory-whatis.md) güvenli, rol tabanlı erişim tooyour kritik verileri sağlar. İle tümleştirmek [Azure Data Factory](../data-factory/data-factory-introduction.md) hello modeline verileri yükler bir etkinlik ekleyerek ardışık düzenler. Özel kodla modellerde basit düzenlemeler yapmak için [Azure Otomasyonu](../automation/automation-intro.md) ve [Azure İşlevleri](../azure-functions/functions-overview.md) kullanılabilir.

## <a name="get-up-and-running-quickly"></a>Hızla çalışmaya başlayın
Azure portalında, birkaç dakikada [sunucu oluşturabilirsiniz](analysis-services-create-server.md). Ayrıca, Azure Resource Manager [şablonları](../azure-resource-manager/resource-manager-create-first-template.md) ve PowerShell'le, bildirim temelli bir şablon kullanarak sunucu sağlayabilirsiniz. Basit bir şablonla, birden çok hizmeti ve bunların yanında depolama hesapları ve Azure İşlevleri gibi diğer Azure bileşenlerini dağıtabilirsiniz. 

Sunucu oluşturduğunuzda, doğrudan Azure portalında bir tablosal model oluşturabilirsiniz. Merhaba yeni (Önizleme) ile [Web Tasarımcı özelliği](analysis-services-create-model-portal.md), tooan Azure SQL Database, Azure SQL veri ambarı veri kaynağı, bağlanma veya Power BI Desktop .pbix dosyasını içeri aktarın. Tablolar arasındaki ilişkileri otomatik olarak oluşturulur ve ölçüleri oluşturabilir veya tarayıcınızdan sağ json biçiminde hello model.bim dosyasını düzenleyin.

## <a name="scale-tooyour-needs"></a>Ölçek tooyour gereksinimleri
Azure Analysis Services; Geliştirici, Temel ve Standart katmanlarında sunulur. Her katman içinde plan maliyetleri according tooprocessing güç, QPUs ve bellek boyutu değişir. Sunucu oluşturduğunuzda, katman içinde bir plan seçersiniz. Planları değiştirme veya aşağı hello içinde aynı katmanı veya yükseltme tooa daha yüksek katman, ancak daha yüksek katman tooa alt katmanından bir düşürülemiyor.

Ölçeği artırın, azaltın veya sunucunuzu duraklatın. Hello Azure portal kullanın veya PowerShell kullanarak, toplam denetim üzerinde-çalışma sırasında sahip. Sadece kullandığınız kadar ödersiniz. toolearn hakkında daha fazla bilgi hello farklı planları ve katmanları ve kullanım hello fiyatlandırma hesaplayıcısı toodetermine hello sağ planı için bkz: [Azure Analysis Services fiyatlandırması](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="keep-your-data-close"></a>Verileriniz yakınınızda olsun
Azure Analysis Services sunucuları hello aşağıdakileri oluşturulabilir [Azure bölgeleri](https://azure.microsoft.com/regions/):

| Kuzey ve Güney Amerika | Avrupa | Asya Pasifik |
|----------|--------|--------------|
|  Güney Brezilya<br> Orta Kanada<br> Doğu ABD 2<br> Orta Kuzey ABD<br> Orta Güney ABD<br> Batı Orta ABD<br> Batı ABD | Kuzey Avrupa<br> Birleşik Krallık Güney<br> Batı Avrupa |   Avustralya Güneydoğu<br> Japonya Doğu<br> Güneydoğu Asya<br> Batı Hindistan  |

Bu liste eksik kalmış olabilir yeni bölgeler tüm hello zaman ekleniyor. Azure portalında sunucunuzu oluştururken veya Azure Resource Manager şablonlarını kullanarak konum seçersiniz. tooget hello en iyi performans, en geniş kullanıcı tabanınızı en yakın bir konum seçin. Modellerinizi birden çok bölgedeki yedekli sunuculara dağıtarak [yüksek kullanılabilirliği](analysis-services-bcdr.md) güvence altına alın.

## <a name="migrate-your-existing-tabular-models"></a>Mevcut tablosal modellerinizi geçirin
Mevcut şirket içi SQL Server Analysis Services modeli çözümlerini zaten varsa, önemli bir değişiklik yapılmadan tooAzure Analysis Services geçirebilirsiniz. toomigrate, kullanabileceğiniz SSDT toodeploy modeli tooyour sunucunuz. Öte yandan, SSMS'de yedekleme ve geri yüklemeyi veya TMSL'yi de kullanabilirsiniz.

Şirket içi veri kaynakları varsa, tooinstall gerekir ve yapılandırma bir [şirket içi veri ağ geçidi](analysis-services-gateway.md). Rolleri ve Rol üyeleri zaten yapılandırılmış varsa, rolleri geçirme ancak SSMS veya PowerShell kullanarak tooreadd Rol üyeleri sahip.

## <a name="connect-toopopular-data-sources"></a>Toopopular veri kaynaklarına bağlanma
Azure Analysis Services destekleyen [toodata kaynaklarına bağlanma](analysis-services-datasource.md) şirket içi kuruluşunuz ve hello bulut. Şirket için ve bulut veri kaynaklarından toplanan verileri birleştirerek karma bir çözüm oluşturun. 

Yeni Tablo 1400 modelleri hello M formül sorgu diline dayalı SSDT hello modern Veri Al özelliğini kullanın. Alma verilerle daha fazla veri dönüştürme, karma özellikleri ve hello özelliği toocreate sahip ve kendi Gelişmiş M formül dil sorgular düzenleyin. Örneğin, tablosal 1400 modelleriyle Azure Blob Depolama'da veri dosyaları üzerinde modelleme yapabilirsiniz.

## <a name="use-hello-tools-you-already-know"></a>Zaten bildiğiniz hello araçlarını kullanma

![BI geliştirici araçları](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>Visual Studio için SQL Server Veri Araçları (SSDT)
Geliştirmek ve hello ücretsiz modelleriyle dağıtmak [Visual Studio için SQL Server veri Araçları (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx). SSDT'de, hızla başlangıç yapıp ilerlemeniz için Analysis Services proje şablonları vardır. SSDT şimdi hello modern Veri Al datasource sorgu ve karma işlev tablo 1400 modelleri için içerir. Power BI Desktop ve Excel 2016 Veri Al değilseniz, ne kadar kolay toocreate yüksek oranda özelleştirilmiş veri kaynağı sorgularının olduğunu bildiğiniz.

#### <a name="sql-server-management-studio"></a>Sql Server Management Studio
[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)’yu (SSMS) kullanarak sunucularınızı ve model veritabanlarınızı yönetin. Merhaba bulutta tooyour sunucuları bağlayın. Hello XMLA sorgu penceresinden sağ TMSL komut dosyalarını çalıştırmak ve TMSL komut dosyalarını kullanarak görevlerini otomatikleştirmek. Yeni özellikler ve işlevler hızla kullanıma sunulur çünkü SSMS her ay güncelleştirilir.

#### <a name="powershell"></a>PowerShell
Sunucu kaynak yönetimi görevlerini sunucuları oluşturma, askıya almak veya sunucu işlemlerini sürdürme veya hello hizmet düzeyi (katman) değiştirme gibi Azure Resource Manager (AzureRM) cmdlet'lerini kullanın. Ekleme veya kaldırma Rol üyeleri gibi veritabanlarını yönetmeyle ilgili diğer görevler işleme veya TMSL komut dosyası çalıştırarak cmdlet'lerini kullanın hello SqlServer modülünde. AzureRM ve SQLServer modülleri hello kullanılabilir [PowerShell Galerisi](https://www.powershellgallery.com/).


## <a name="your-data-is-secure"></a>Verileriniz güvende
![Veri görselleştirmeleri](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>Kimlik Doğrulaması
Azure Analysis Services için kullanıcı kimlik doğrulaması, [Azure Active Directory (AAD)](../active-directory/active-directory-whatis.md) tarafından işlenir. Toolog tooan Azure Analysis Services veritabanında, kullanıcıların kullanımı bir kuruluş hesabı kimlik erişim toohello veritabanı ile çalışırken tooaccess çalışıyor olabilirsiniz. Bu kullanıcı kimlikleri hello Azure Analysis Services sunucusunun bulunduğu hello abonelik için hello varsayılan Azure Active Directory üyeleri olmalıdır. toolearn daha, fazla [kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md).

#### <a name="data-security"></a>Veri güvenliği
Azure Analysis Services, Azure Blob Depolama toopersist depolama ve Analysis Services veritabanları için meta verileri kullanır. Blob’daki veri dosyaları, Azure Blob Sunucu Tarafı Şifrelemesi (SSE) kullanılarak şifrelenir. Doğrudan Sorgu modu kullanılırken yalnızca meta veriler depolanır. Merhaba gerçek veri hello veri kaynağından sorgu zamanında erişilir.

#### <a name="on-premises-data-sources"></a>Şirket içi veri kaynakları
Güvenli erişim toodata bulunan şirket içi kuruluşunuzdaki yükleme ve yapılandırma elde edilir bir [şirket içi veri ağ geçidi](analysis-services-gateway.md). Ağ geçitleri, doğrudan sorgu ve bellek içi modları için erişim toodata sağlar. Bir Azure Analysis Services modeli tooan şirket içi veri kaynağına bağlandığında, bir sorgu hello şifrelenmiş kimlik bilgileri hello şirket içi veri kaynağı için birlikte oluşturulur. Merhaba ağ geçidi bulut Hizmeti'ne hello sorgu analiz eder ve hello isteği tooan Azure Service Bus iter. Merhaba şirket içi ağ geçidi hello Azure hizmet veri yolu için bekleyen istekler yoklar. Merhaba ağ geçidi sonra hello sorgu alır, hello kimlik şifresini çözer ve yürütme için toohello veri kaynağına bağlanır. Merhaba sonuçlar ardından hello veri kaynağından gönderilen, toohello ağ geçidi yedekleyin ve toohello Azure Analysis Services veritabanı.

Azure Analysis Services tarafından hello tabidir [Microsoft çevrimiçi Hizmet Koşulları'nı](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) ve hello [Microsoft Online Services gizlilik bildirimi](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).
toolearn Azure güvenliği hakkında daha fazla bilgi görmek hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/Security/AzureSecurity).

## <a name="supports-hello-latest-client-tools"></a>Merhaba son istemci araçları destekler
![Veri görselleştirmeleri](./media/analysis-services-overview/aas-overview-clients.png)

Power BI, Excel ve üçüncü taraf araçları gibi modern veri keşif ve görselleştirme araçları, kullanıcılara modern verileriniz üzerinde üst düzeyde etkileşimli ve görsel açıdan zengin öngörüler sağlar.

İstemcilerin kullandığı MSOLAP, AMO veya ADOMD [istemci kitaplıkları](analysis-services-data-providers.md) tooconnect tooAnalysis Hizmetleri sunucuları. Power BI Masaüstü ve Excel gibi Microsoft istemci uygulamaları bu istemci kitaplıklarının üçünü de yükler. Ancak unutmayın, hello sürümü veya güncelleştirmelerinin sıklığını bağlı olarak, istemci kitaplıkları hello en son sürümleri Azure Analysis Services tarafından gerekli olmayabilir. Merhaba aynı toocustom uygulamaları veya AsCmd, ZEL, ADOMD.NET gibi diğer arabirimleri için geçerlidir. Bu uygulamalar genellikle el ile bir paketinin bir parçası hello kitaplıkları yükleme gerektirir.


## <a name="get-help"></a>Yardım alın

#### <a name="documentation"></a>Belgeler
Azure Analysis Services yukarı basit tooset ve toomanage ' dir. Toocreate gerekir ve sunucu hizmetlerinizi burada yönetmek tüm hello bilgileri bulabilirsiniz. Bir veri modeli toodeploy tooyour sunucusu oluştururken, onu sahip çok hello aynı tooan şirket içi sunucu dağıttığınız bir veri modeli oluşturmak için olduğu gibi. [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services) sayfasında kavramsal makaleler, yordamsal makaleler, öğreticiler ve başvuru makalelerinden oluşan kapsamlı bir kitaplık sunulmaktadır.

#### <a name="videos"></a>Videolar
[Channel 9’da Azure Analysis Services](https://channel9.msdn.com/series/Azure-Analysis-Services) sayfasındaki yararlı videoları inceleyin.

#### <a name="blogs"></a>Bloglar
Her şey çok hızlı gelişiyor. Her zaman en son bilgiler hello hello alabilir [Analysis Services ekip blogu](https://blogs.msdn.microsoft.com/analysisservices/) ve [Azure blogu](https://azure.microsoft.com/blog/).

#### <a name="community"></a>Topluluk
Analysis Services’ın canlı bir kullanıcı topluluğu vardır. Üzerinde Hello görüşmeye [Azure Analysis Services Forumu](https://aka.ms/azureanalysisservicesforum).

## <a name="feedback"></a>Geri Bildirim
Bir öneriniz veya özellik isteğiniz mi var? Yorumlarınızı emin tooleave olması [Azure Analysis Services geribildirim](https://aka.ms/azureanalysisservicesfeedback).

Merhaba belgeler hakkında öneriler var mı? Her makalenin hello altındaki Livefyre kullanarak yorum ekleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Azure Analysis Services hakkında daha fazla bildiğinize göre zamanı tooget başlatıldı. Nasıl çok öğrenin[bir sunucu oluşturmak](analysis-services-create-server.md) azure'da. Sunucunuz hazır olduğunda hello ilerleyebilirsiniz [Adventure Works Öğreticisi](tutorials/aas-adventure-works-tutorial.md) toolearn nasıl toocreate tam olarak işlevsel bir tablo modeline ve tooyour sunucu dağıtabilirsiniz.
