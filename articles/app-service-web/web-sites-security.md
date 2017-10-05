---
title: "Azure Uygulama Hizmeti’nde bir uygulamanın güvenliğini sağlama"
description: "Güvenli bir web uygulaması, mobil uygulama arka ucu veya Azure App Service'teki API uygulamasına öğrenin."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: b70d74441f3d6d9793ae516b3f04e36e786a9a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde bir uygulamanın güvenliğini sağlama
Bu makale web uygulaması, mobil uygulama arka ucu veya Azure App Service'teki API uygulamasına güvenliğini sağlama konusunda başlamanıza yardımcı olur. 

Azure App Service'te güvenlik iki düzeyi vardır: 

* **Altyapı ve platform güvenliği** -güvendiğiniz Azure Hizmetleri, aslında güvenli bir şekilde bulutta şeyler çalıştırmanız gerekir.
* **Uygulama güvenliği** -app güvenli bir şekilde tasarlamanız gerekir. Bu, nasıl Azure Active Directory ile tümleştirme, sertifikaları yönetme ve nasıl farklı hizmetler güvenli bir şekilde geçebildiğinden emin içerir. 

#### <a name="infrastructure-and-platform-security"></a>Altyapı ve platform güvenliği
Uygulama hizmeti Azure VM'ler, depolama, ağ bağlantıları, web çerçeveleri, yönetim ve tümleştirme özelliklerine ve daha fazlasını bulundurur, bu nedenle daha etkin biçimde güvenli sıkı ve aracılığıyla düşük uyumluluğu gider ve emin olmak için sürekli olarak denetler Bu:

* Uygulama hizmeti uygulamalarınız, hem Internet ve diğer müşterilerin Azure kaynakları'ndan yalıtılır.
* Gizli (örneğin, bağlantı dizeleri) uygulama hizmeti uygulamanızı ve bir kaynak grubundaki diğer Azure kaynaklarına (ör. SQL veritabanı) arasındaki iletişimi Azure içinde kalır ve tüm ağ sınırlar arası değil. Gizli her zaman şifrelenir.
* App Service uygulaması ve PowerShell yönetim, komut satırı arabirimi, Azure SDK'ları, REST API'leri ve karma bağlantılar gibi dış kaynaklar arasındaki tüm iletişimin düzgün şifrelenir.
* Yönetim uygulama hizmeti kaynakları korur 24 saatlik tehdit kötü amaçlı yazılımlara karşı hizmet engelleme (DDoS) dağıtılmış man-in--middle (MITM) ve diğer tehditlere. 

Altyapı ve platform güvenliği hakkında daha fazla bilgi için bkz: [Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Uygulama güvenliği
Azure altyapı ve uygulamanızın üzerinde çalıştığı platform güvenliğini sağlamak için sorumlu olsa da, bu, uygulamanızın güvenliğini sağlamak için sorumluluğundadır. Diğer bir deyişle, geliştirme, dağıtma ve uygulama kodu ve içerik güvenli bir şekilde yönetmek gerekir. Bu, uygulama kodu veya içeriği hala gibi tehditlerine karşı savunmasız olabilir:

* SQL ekleme
* Oturumu ele geçirme
* Çapraz site-komut dosyası oluşturma
* Uygulama düzeyi MITM
* Uygulama düzeyi DDoS

Web tabanlı uygulamalar için güvenlik konuları tam bir irdelemesi bu belgenin kapsamında değildir. Bir başlangıç noktası, uygulamanızın güvenliğini sağlama konusunda daha ayrıntılı yönergeler için bkz: [açık Web uygulaması güvenlik proje (OWASP)](https://www.owasp.org/index.php/Main_Page), özellikle [ilk 10 proje.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), geçerli en iyi 10 kritik listeler OWASP üyeleri tarafından belirlendiği şekilde web uygulaması güvenlik açıkları.

## <a name="perform-penetration-testing-on-your-app"></a>Uygulamanıza sınama sızma gerçekleştirin
Uygulama hizmeti uygulamanızı güvenlik açıklarını testi ile çalışmaya başlamak için en kolay yollarından biri kullanmak için [Tinfoil Security ile tümleştirme](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tek tıklatmayla güvenlik açığı uygulamanıza tarama gerçekleştirmek için. Kolay anlaşılır bir raporda test sonuçlarını görüntülemek ve adım adım yönergeler içeren her bir güvenlik açığı düzeltme öğrenin.

Kendi sızma sınamalar gerçekleştirmek veya başka bir tarayıcı paketi ya da sağlayıcı kullanmayı tercih ederseniz, uymanız gereken [onay işlemini test Azure sızma](https://security-forms.azure.com/penetration-testing/terms) ve istenen sızma testleri gerçekleştirmek için önce onay almak.

## <a name="https"></a>Müşteri ile güvenli iletişim
Kullanırsanız  **\*. azurewebsites.net** App Service uygulamanız için oluşturulan etki alanı adı bir SSL sertifikası tüm koşuluyla, HTTPS hemen kullanabileceğiniz  **\*. azurewebsites.net** etki alanı adları. Siteniz kullanıyorsa bir [özel etki alanı adı](app-service-web-tutorial-custom-domain.md), bir SSL sertifikası yükleyebilirsiniz [HTTPS'yi etkinleştirmek](app-service-web-tutorial-custom-ssl.md) özel etki alanı.

Etkinleştirme [HTTPS](https://en.wikipedia.org/wiki/HTTPS) uygulamanızı ve kullanıcı arasındaki iletişimi MITM saldırılarına karşı korumaya yardımcı olabilirsiniz.

## <a name="secure-data-tier"></a>Güvenli veri katmanı
Uygulama hizmeti yüksek oranda tümleştirildiğini SQL veritabanı ile tüm bağlantı dizeleri Panosu şifrelenir ve yalnızca uygulamayı çalıştıran VM üzerinde şifresi gibi *ve* yalnızca uygulama çalıştırıldığında. Ayrıca, Azure SQL veritabanı uygulama verilerinizi dahil olmak üzere siber tehditlere karşı korumanıza yardımcı olması için çok sayıda güvenlik özellikleri içeren [çalışmıyorken şifreleme](https://msdn.microsoft.com/library/dn948096.aspx), [her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx), [ Dinamik veri maskeleme](../sql-database/sql-database-dynamic-data-masking-get-started.md), ve [tehdit algılama](../sql-database/sql-database-threat-detection.md). Hassas verileri veya uyumluluk gereksinimlerine sahip olup [SQL veritabanınızın güvenliğini sağlama](../sql-database/sql-database-security-overview.md) verilerinizin güvenliğini sağlama hakkında daha fazla bilgi için.

ClearDB gibi bir üçüncü taraf veritabanı sağlayıcısı kullanıyorsanız, sağlayıcının belgelerine doğrudan en iyi güvenlik uygulamaları ile danışmalısınız.  

## <a name="develop"></a>Güvenli geliştirme ve dağıtım
### <a name="publishing-profiles-and-publish-settings"></a>Yayımlama profilleri ve yayımlama ayarları
Uygulamaları geliştirirken, yönetim görevlerini gerçekleştirme veya yardımcı programlarını kullanarak görevleri otomatikleştirme **Visual Studio**, **Web Matrix**, **Azure PowerShell** veya  **Azure komut satırı arabirimi (Azure CLI)**, ya da kullanabileceğiniz bir *yayımlama ayarları* dosya veya bir *yayımlama profilini*. Her iki dosya türleri Azure kimlik doğrulaması ve yetkisiz erişimi önlemek için korunması.

* A **yayımlama ayarları** dosyası içerir
  
  * Azure abonelik Kimliğinizi
  * Aboneliğiniz için yönetim görevlerini gerçekleştirmenize olanak tanıyan bir yönetim sertifikası *bir hesap adı veya parola sağlamak zorunda kalmadan*.
* A **yayımlama profilini** dosyası içerir
  
  * Bilgi için uygulamanızı yayımlama

Yayımlama ayarları dosyası veya yayımlama profili dosyası kullanan bir yardımcı programı kullanırsanız, yayımlama ayarlarını veya profil yardımcı programı içeren dosyasını içeri aktarın ve ardından **silmek** dosya. Projede Örneğin, çalışan kişilerle paylaşmak için dosyayı korursanız gerekir, güvenli bir konumda depolayabilirsiniz bir *şifrelenmiş* kısıtlı izinleri olan dizin.

Ayrıca, alınan kimlik bilgilerini güvenli olduğundan emin olmanız gerekir. Örneğin, **Azure PowerShell** ve **Azure komut satırı arabirimi (Azure CLI)** her ikisi de içeri aktarılan bilgileri depolamak, **giriş dizini** ( *~*  Linux veya OS X çalıştıran sistemlerde ve */users/kullanıcıadınız* Windows sistemlerinde.) Ek güvenlik için istediğiniz **şifrelemek** işletim sistemi için sağlanan şifreleme araçları kullanarak bu konumları.

### <a name="configuration-settings-and-connection-strings"></a>Yapılandırma ayarlarını ve bağlantı dizeleri
Bağlantı dizeleri, kimlik doğrulama kimlik bilgileri ve diğer hassas bilgiler yapılandırma dosyalarını depolamak için yaygın bir uygulamadır. Ne yazık ki, bu dosyalar, Web sitenizde kullanıma sunulan ya da bu bilgileri gösterme ortak bir depoya işaretli. Basit bir arama [GitHub](https://github.com), örneğin, ortak depoları gösterilen parolalarında sayısız yapılandırma dosyalarıyla açığa.

Bu bilgiler, uygulamanızın yapılandırma dosyaları dışında tutmak için en iyi uygulamadır bakın. Uygulama hizmeti çalışma zamanı ortamı olarak bir parçası olarak yapılandırma bilgilerini depolamak olanak tanır **uygulama ayarları** ve **bağlantı dizeleri**. Değerleri ile çalışma zamanında uygulamanıza sunulan *ortam değişkenleri* çoğu programlama dili için. Bu değerler, çalışma zamanında .NET yapılandırması içine .NET uygulamaları için eklenmiş. Görüntüleyebilir veya yapılandırabilirsiniz sürece bu durumlar dışında bu yapılandırma ayarları şifrelenmiş olarak kalır kullanarak [Azure Portal](https://portal.azure.com) veya PowerShell veya Azure CLI gibi yardımcı programları. 

App Service içinde yapılandırma bilgilerini depolamak uygulamanın yöneticinin üretim uygulamaları için hassas bilgileri kilitlemek mümkün kılar. Geliştiriciler, uygulama geliştirme için yapılandırma ayarlarını ayrı bir dizi kullanabilir ve ayarları otomatik olarak App Service içinde yapılandırdığınız ayarlarla yerini. Bile geliştiriciler üretim uygulaması için yapılandırılmış gizli bilmeniz gerekir. Uygulama ayarlarının ve bağlantı dizelerinin App Service'te yapılandırma hakkında daha fazla bilgi için bkz: [web uygulamaları yapılandırma](web-sites-configure.md).

### <a name="ftps"></a>FTPS
Azure uygulama hizmeti, uygulamanız için dosya sistemine güvenli FTP erişim sağlar **FTPS**. Bu web uygulamasının yanı sıra tanılama uygulama kodu güvenli bir şekilde erişmenize olanak tanır günlükleri. FTPS her zaman yerine FTP kullanmanız önerilir. 

Aşağıdaki adımları uygulamanız için FTPS bağlantı bulunabilir:

1. Açık [Azure Portal](https://portal.azure.com).
2. Seçin **tümüne Gözat**.
3. Gelen **Gözat** dikey penceresinde, select **uygulama hizmetleri**.
4. Gelen **uygulama hizmetleri** dikey penceresinde, istediğiniz uygulamayı seçin.
5. Uygulamanın dikey penceresinden seçin **tüm ayarları**.
6. Gelen **ayarları** dikey penceresinde, select **özellikleri**.
7. FTP ve FTPS bağlantılar sağlanır **ayarları** dikey. 

FTPS hakkında daha fazla bilgi için bkz: [Dosya Aktarım Protokolü](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Sonraki adımlar
Azure platformu, raporlama bilgi güvenliği hakkında daha fazla bilgi için bir **güvenlik olay ya da kötüye**, ya da size gerçekleştirme Microsoft bildirmek için **sızma testi** , sitenizin Güvenlik bölümüne bakın [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Daha fazla bilgi için **web.config** veya **applicationhost.config** App Service uygulamalarının dosyalarında bkz [Azure App Service web apps kilidi yapılandırma seçenekleri](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Saldırı seviyelerinden yararlı olabilir, uygulama hizmeti uygulamalar için günlük kaydı bilgileri hakkında bilgi için bkz: [tanılama günlük kaydını etkinleştir](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service'i kullanmaya başlamak istiyorsanız, Git [App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

