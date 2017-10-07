---
title: aaaSecure Azure App Service'te bir uygulama
description: "Bilgi nasıl toosecure bir web uygulaması, mobil uygulama arka ucu ya da Azure App Service'teki API uygulamasına."
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
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde bir uygulamanın güvenliğini sağlama
Bu makale web uygulaması, mobil uygulama arka ucu veya Azure App Service'teki API uygulamasına güvenliğini sağlama konusunda başlamanıza yardımcı olur. 

Azure App Service'te güvenlik iki düzeyi vardır: 

* **Altyapı ve platform güvenliği** -Azure toohave hello Hizmetleri güven güvenli bir şekilde hello bulutta çalıştırmak tooactually şeyler gerekir.
* **Uygulama güvenliği** -toodesign hello uygulamanın kendi güvenli bir şekilde gerekir. Bu, nasıl Azure Active Directory ile tümleştirme, sertifikaları yönetme ve nasıl toodifferent hizmetler güvenli bir şekilde geçebildiğinden emin içerir. 

#### <a name="infrastructure-and-platform-security"></a>Altyapı ve platform güvenliği
Uygulama hizmeti hello Azure VM'ler, depolama, ağ bağlantıları, web çerçeveleri, yönetim ve tümleştirme özelliklerine ve daha fazlasını bulundurur, bu nedenle daha etkin biçimde güvenli sıkı ve aracılığıyla düşük uyumluluğu gider ve sürekli toomake üzerinde emin denetler Bu:

* Uygulama hizmeti uygulamalarınız her iki hello Internet yalıtılmış ve gelen diğer müşterilerin Azure kaynaklarını hello.
* Gizli (örneğin, bağlantı dizeleri) uygulama hizmeti uygulamanızı ve bir kaynak grubundaki diğer Azure kaynaklarına (ör. SQL veritabanı) arasındaki iletişimi Azure içinde kalır ve tüm ağ sınırlar arası değil. Gizli her zaman şifrelenir.
* App Service uygulaması ve PowerShell yönetim, komut satırı arabirimi, Azure SDK'ları, REST API'leri ve karma bağlantılar gibi dış kaynaklar arasındaki tüm iletişimin düzgün şifrelenir.
* Yönetim uygulama hizmeti kaynakları korur 24 saatlik tehdit kötü amaçlı yazılımlara karşı hizmet engelleme (DDoS) dağıtılmış man-in--middle (MITM) ve diğer tehditlere. 

Altyapı ve platform güvenliği hakkında daha fazla bilgi için bkz: [Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Uygulama güvenliği
Azure hello altyapı ve uygulamanızın üzerinde çalıştığı platform güvenliğini sağlamak için sorumlu olsa da, sorumluluk toosecure olduğundan, uygulamanızın. Toodevelop, gereken diğer bir deyişle, dağıtma ve uygulama kodu ve içerik güvenli bir şekilde yönetme. Bu, uygulama kodu veya içeriği hala savunmasız toothreats gibi olabilir:

* SQL ekleme
* Oturumu ele geçirme
* Çapraz site-komut dosyası oluşturma
* Uygulama düzeyi MITM
* Uygulama düzeyi DDoS

Web tabanlı uygulamalar için güvenlik konuları tam bir irdelemesi hello bu belgenin kapsamında değildir. Merhaba, uygulamanızın güvenliğini sağlama konusunda daha ayrıntılı yönergeler için başlangıç noktası olarak bkz [açık Web uygulaması güvenlik proje (OWASP)](https://www.owasp.org/index.php/Main_Page), özellikle hello [ilk 10 proje.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), hangi listeleri hello geçerli ilk 10 OWASP üyeleri tarafından belirlenen kritik web uygulaması güvenlik açıkları.

## <a name="perform-penetration-testing-on-your-app"></a>Uygulamanıza sınama sızma gerçekleştirin
Merhaba en kolay yolu tooget birini kullanmaya testi ile uygulama hizmeti uygulamanızı güvenlik açıklarından için toouse hello [Tinfoil Security ile tümleştirme](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform tek tıklatmayla güvenlik açığı uygulamanıza tarama. Kolay anlaşılır bir raporda hello test sonuçlarını görüntülemek ve bilgi nasıl toofix her bir güvenlik açığı hakkında adım adım yönergeler.

Tooperform tercih ederseniz, kendi sızma testleri veya başka bir tarayıcı paketi ya da sağlayıcı toouse istediğiniz, hello izlemelisiniz [onay işlemini test Azure sızma](https://security-forms.azure.com/penetration-testing/terms) ve önceki onay tooperform istenen hello sızma edinme test eder.

## <a name="https"></a>Müşteri ile güvenli iletişim
Merhaba kullanırsanız  **\*. azurewebsites.net** App Service uygulamanız için oluşturulan etki alanı adı bir SSL sertifikası tüm koşuluyla, HTTPS hemen kullanabileceğiniz  **\*. azurewebsites.net** etki alanı adları. Siteniz kullanıyorsa bir [özel etki alanı adı](app-service-web-tutorial-custom-domain.md), bir SSL sertifikası çok yükleyebilirsiniz[HTTPS'yi etkinleştirmek](app-service-web-tutorial-custom-ssl.md) hello özel etki alanı.

Etkinleştirme [HTTPS](https://en.wikipedia.org/wiki/HTTPS) hello iletişimi, uygulama ve onun kullanıcıları arasında MITM saldırılarına karşı korumaya yardımcı olabilirsiniz.

## <a name="secure-data-tier"></a>Güvenli veri katmanı
Uygulama hizmeti ile SQL veritabanı yüksek oranda tümleştirir, tüm hello bağlantı dizeleri hello Panosu şifrelenir ve yalnızca VM hello üzerinde şifresi şekilde bu hello uygulama üzerinde çalıştığı *ve* yalnızca zaman hello uygulama çalıştırır. Ayrıca, Azure SQL veritabanı uygulama verilerinizi siber tehditlere karşı dahil olmak üzere, güvenli çok sayıda güvenlik özellikleri toohelp içeren [çalışmıyorken şifreleme](https://msdn.microsoft.com/library/dn948096.aspx), [her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx), [ Dinamik veri maskeleme](../sql-database/sql-database-dynamic-data-masking-get-started.md), ve [tehdit algılama](../sql-database/sql-database-threat-detection.md). Hassas verileri veya uyumluluk gereksinimlerine sahip olup [SQL veritabanınızın güvenliğini sağlama](../sql-database/sql-database-security-overview.md) hakkında daha fazla bilgi için toosecure verilerinizi.

ClearDB gibi bir üçüncü taraf veritabanı sağlayıcısı kullanırsanız hello sağlayıcının belgelerine doğrudan en iyi güvenlik uygulamaları ile danışmalısınız.  

## <a name="develop"></a>Güvenli geliştirme ve dağıtım
### <a name="publishing-profiles-and-publish-settings"></a>Yayımlama profilleri ve yayımlama ayarları
Uygulamaları geliştirirken, yönetim görevlerini gerçekleştirme veya yardımcı programlarını kullanarak görevleri otomatikleştirme **Visual Studio**, **Web Matrix**, **Azure PowerShell** veya hello **Azure komut satırı arabirimi (Azure CLI)**, ya da kullanabileceğiniz bir *yayımlama ayarları* dosya veya bir *yayımlama profilini*. Hem dosya türlerini Azure kimlik doğrulaması ve tooprevent yetkisiz erişime korunması.

* A **yayımlama ayarları** dosyası içerir
  
  * Azure abonelik Kimliğinizi
  * Aboneliğiniz için tooperform yönetim görevleri sayesinde bir yönetim sertifikası *bir hesap adı veya parola tooprovide kalmadan*.
* A **yayımlama profilini** dosyası içerir
  
  * Bilgi tooyour uygulama yayımlamak için

Yayımlama ayarları dosyası veya yayımlama profili dosyası kullanan bir yardımcı programı kullanırsanız, hello yayımlama ayarlarını içeren hello dosyasını içeri aktarın veya profil hello yardımcı programı ve ardından **silmek** hello dosya. Hello dosyayı korursanız gerekir, örneğin, hello bir projede çalışıyor başkalarıyla tooshare depolamak, güvenli bir konumda gibi bir *şifrelenmiş* kısıtlı izinleri olan dizin.

Ayrıca, hello alınan kimlik bilgilerini güvenli hale getirilen emin olmanız gerekir. Örneğin, **Azure PowerShell** ve hello **Azure komut satırı arabirimi (Azure CLI)** her ikisi de içeri aktarılan bilgileri depolamak, **giriş dizini** ( *~*  Linux veya OS X çalıştıran sistemlerde ve */users/kullanıcıadınız* Windows sistemlerinde.) Ek güvenlik için çok isteyebilir**şifrelemek** işletim sistemi için sağlanan şifreleme araçları kullanarak bu konumları.

### <a name="configuration-settings-and-connection-strings"></a>Yapılandırma ayarlarını ve bağlantı dizeleri
Genel yöntem toostore bağlantı dizeleri, kimlik doğrulama kimlik bilgileri ve diğer hassas bilgiler yapılandırma dosyalarında olduğu. Ne yazık ki, bu dosyalar, Web sitenizde kullanıma sunulan ya da bu bilgileri gösterme ortak bir depoya işaretli. Basit bir arama [GitHub](https://github.com), örneğin, sayısız yapılandırma dosyaları hello ortak depoları gösterilen parolalarında ile açığa.

Merhaba en iyi uygulama bu bilgiler, uygulamanızın yapılandırma dosyaları dışında tookeep olur. Uygulama hizmeti hello çalışma zamanı ortamı olarak bir parçası olarak yapılandırma bilgilerini depolamak olanak tanır **uygulama ayarları** ve **bağlantı dizeleri**. Merhaba değerlerdir gösterilen tooyour uygulama çalışma zamanında *ortam değişkenleri* çoğu programlama dili için. Bu değerler, çalışma zamanında .NET yapılandırması içine .NET uygulamaları için eklenmiş. Görüntüleyebilir veya yapılandırabilirsiniz sürece bu durumlar dışında bu yapılandırma ayarları şifrelenmiş olarak kalır hello kullanarak [Azure Portal](https://portal.azure.com) veya PowerShell veya Azure CLI hello gibi yardımcı programları. 

App Service içinde yapılandırma bilgilerini depolamak için hello uygulamanın yönetici toolock hello üretim uygulamaları için hassas bilgileri aşağı mümkün kılar. Geliştiriciler, uygulama geliştirme için yapılandırma ayarlarını ayrı bir dizi kullanabilir ve hello ayarları otomatik olarak App Service içinde yapılandırılan hello ayarları yerini. Değil bile hello geliştiricilerin hello üretim uygulaması için yapılandırılmış tooknow hello gizli gerekir. Uygulama ayarlarının ve bağlantı dizelerinin App Service'te yapılandırma hakkında daha fazla bilgi için bkz: [web uygulamaları yapılandırma](web-sites-configure.md).

### <a name="ftps"></a>FTPS
Azure uygulama hizmeti uygulamanızı güvenli FTP Erişim toohello dosya sistemi sağlayan **FTPS**. Merhaba web uygulaması ve bunun yanı sıra tanılama toosecurely erişim hello uygulama kodu bu sayede günlükleri. FTPS her zaman yerine FTP kullanmanız önerilir. 

Merhaba FTPS bağlantı uygulamanız için aşağıdaki adımları hello ile bulunabilir:

1. Açık hello [Azure Portal](https://portal.azure.com).
2. Seçin **tümüne Gözat**.
3. Merhaba gelen **Gözat** dikey penceresinde, select **uygulama hizmetleri**.
4. Merhaba gelen **uygulama hizmetleri** dikey penceresinde, Select hello istenen uygulama.
5. Merhaba uygulamanın dikey penceresinden seçin **tüm ayarları**.
6. Merhaba gelen **ayarları** dikey penceresinde, select **özellikleri**.
7. Merhaba FTP ve FTPS bağlantılarını hello üzerinde sağlanan **ayarları** dikey. 

FTPS hakkında daha fazla bilgi için bkz: [Dosya Aktarım Protokolü](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Sonraki adımlar
Hello Azure platformu, raporlama hakkında daha fazla bilgi hello güvenliği hakkında daha fazla bilgi için bir **güvenlik olay ya da kötüye**, veya tooinform, gerçekleştirme Microsoft **sızma testi** biri, Site, hello hello güvenlik bölümüne bakın [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Daha fazla bilgi için **web.config** veya **applicationhost.config** App Service uygulamalarının dosyalarında bkz [Azure App Service web apps kilidi yapılandırma seçenekleri](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Saldırı seviyelerinden yararlı olabilir, uygulama hizmeti uygulamalar için günlük kaydı bilgileri hakkında bilgi için bkz: [tanılama günlük kaydını etkinleştir](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

