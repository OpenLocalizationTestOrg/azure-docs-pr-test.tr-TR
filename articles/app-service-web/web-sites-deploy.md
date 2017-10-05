---
title: "Uygulamanızı Azure App Service'e dağıtma | Microsoft Docs"
description: "Uygulamanızı Azure App Service'e dağıtma öğrenin."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: f41be4e00a9250b07ca260c2858e5fc45143f746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-azure-app-service"></a>Uygulamanızı Azure App Service'e dağıtma
Bu makalede, dosyaları web uygulaması, mobil uygulama arka ucu veya API uygulamasına dağıtmak için en iyi seçeneği belirlemenize yardımcı olur [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)ve ardından, tercih ettiğiniz seçeneği özel yönergeleri ile uygun kaynaklarına size yol gösterir .

## <a name="overview"></a>Azure uygulama hizmeti dağıtımına genel bakış
Azure uygulama hizmeti uygulama çerçevesi sizin için (ASP.NET, PHP, Node.js, vb.) korur. Bazı çerçeveler Java ve Python gibi sahipken, varsayılan olarak etkin, etkinleştirmek için bir basit onay işaretine yapılandırma gerekebilir. Ayrıca, PHP sürümünü veya, çalışma zamanı verileri gibi uygulama çerçevesi özelleştirebilirsiniz. Daha fazla bilgi için bkz: [uygulamanızı Azure App Service'te yapılandırma](web-sites-configure.md).

Web sunucusu veya uygulama çerçevesi hakkında endişelenmenize gerek yoktur, uygulamanızı App Service'e dağıtma sağlasa da, kodunuzu, ikili dosyaları, içerik dosyaları ve bunların ilgili dizin yapısını çok dağıtma olduğu [ **/site/ wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) Azure (veya **/site/wwwroot/App_Data/işleri/** Web işleri için dizin). Uygulama hizmeti üç farklı dağıtım işlemlerini destekler. Bu makaledeki tüm dağıtım yöntemleri aşağıdaki işlemler birini kullanın: 

* [FTP veya FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): kullanım için sık kullandığınız FTP veya FTPS etkin dosyalarınızı sunucudan Azure'a taşımak aracı [FileZilla](https://filezilla-project.org) için tam özellikli IDE gibi [NetBeans](https://netbeans.org). Dosya karşıya yükleme işlemi kesinlikle budur. Hiçbir ek hizmetleri App Service tarafından sürüm denetimi, dosya yapısı yönetimi, vb. gibi sağlanır. 
* [Kudu (Git/Mercurial veya OneDrive/Dropbox gibi)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu olan [dağıtım altyapısını](https://github.com/projectkudu/kudu/wiki) App Service'te. Kodunuz için Kudu doğrudan herhangi depodan iletin. Kudu kodu, sürüm denetimi, paket geri yükleme, MSBuild, dahil olmak üzere itildiği zaman eklenen hizmetleri de sağlar ve [web kancaları](https://github.com/projectkudu/kudu/wiki/Web-hooks) sürekli dağıtım ve diğer otomatik görevleri. Kudu dağıtım altyapısı, dağıtım kaynakları 3 farklı türlerini destekler:   
  
  * OneDrive ve Dropbox içerik eşitleme   
  * Otomatik eşitleme GitHub, Bitbucket ve Visual Studio Team Services ile sürekli dağıtımın deposu tabanlı  
  * El ile eşitleme yerel Git deposu tabanlı dağıtımla  
* [Web dağıtımı](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): sık kullanılan Microsoft doğrudan App Service'e dağıtma kod araçları gibi dağıtım IIS sunucuları, tooling aynı kullanarak Visual Studio otomatikleştirir. Bu araç yalnızca fark dağıtım, veritabanı oluşturma, bağlantı dizeleri, vb. dönüştürmeleri destekler. Web dağıtımı için Azure dağıtılmadan önce uygulama ikili dosyaları oluşturulur Kudu farklıdır. FTP benzeyen, hiçbir ek hizmetleri App Service tarafından sağlanır.

Popüler web geliştirme araçları, bir veya daha fazla bu dağıtım işlemleri destekler. Seçtiğiniz aracı yararlanabileceğiniz dağıtım işlemleri belirlerken, elden gerçek DevOps işlevselliği dağıtım işlemi ve seçtiğiniz belirli araçları birleşimi bağlıdır. Örneğin, Web dağıtımı gerçekleştirirseniz [Azure SDK ile Visual Studio](#vspros), Kudu Otomasyon alma olsa bile, paket geri yüklemesi ve MSBuild Otomasyon Visual Studio'da alın. 

> [!NOTE]
> Bu dağıtım işlemleri gerçekten yok [Azure kaynaklarını hazırlama](../azure-resource-manager/resource-group-template-deploy-portal.md) , uygulamanız gerekebilir. Ancak, bağlantılı nasıl yapılır makaleleri çoğunu size uygulama sağlama gösterir ve kodunuzu dağıtma uçtan uca. Azure kaynaklarında sağlamaya yönelik ek seçenekler bulabileceğiniz [komut satırı araçlarını kullanarak dağıtım otomatikleştirmek](#automate) bölümü.
> 
> 

## <a name="ftp"></a>FTP içeren dosyaları karşıya yükleyerek elle dağıtma
Web içeriğinize bir web sunucusuna el ile kopyalanması için kullanılıyorsa, kullanabileceğiniz bir [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) Windows Explorer gibi dosyaları kopyalamak için yardımcı programı veya [FileZilla](https://filezilla-project.org/).

Dosyaları el ile kopyalama uzmanları şunlardır:

* Benzerlik ve FTP araçları için en düşük karmaşıklık. 
* Tam olarak dosyalarınızı nerede kalacaklarını bilmek.
* Ek güvenlik FTPS ile.

Dosyaları el ile kopyalama simgeler şunlardır:

* Uygulama hizmeti doğru dizinlerde dosyaları dağıtmak nasıl bilmek zorunda. 
* Hatalar oluştuğunda geri alma için sürüm denetimi yok.
* Dağıtım sorunlarını gidermek için yerleşik dağıtım geçmişi yok.
* Birçok FTP aracı yoksa ve yalnızca fark kopyalanmasını sağlayan yalnızca tüm dosyaları kopyalayın çünkü olası uzun dağıtım zaman.  

### <a name="howtoftp"></a>FTP içeren dosyaları karşıya yükleme yapma
[Azure Portal](https://portal.azure.com) uygulamanızın dizinleri FTP veya FTPS kullanarak bağlanmak için gereken tüm bilgileri verir.

* [Uygulamanızı Azure App Service'e FTP kullanarak dağıtma](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Bir bulut klasörle eşitleniyor tarafından dağıtma
İyi bir seçenek [dosyaları el ile kopyalayarak](#ftp) dosyalar ve klasörler için uygulama hizmeti OneDrive ve Dropbox gibi bir bulut Depolama hizmetinden eşitliyor. Bir bulut klasörle eşitleniyor dağıtım için Kudu işlemi kullanır (bkz [dağıtım işlemlerine genel bakış](#overview)).

Bir bulut klasörle eşitlemenin uzmanları şunlardır:

* Basitlik dağıtım. Yerel çalışma dizininizi da dağıtım dizininize gelir Masaüstü eşitleme istemciler, OneDrive ve Dropbox gibi hizmetler sağlar.
* Tek tıklamayla dağıtımı.
* Kudu dağıtım Altyapısı'ndaki tüm işlevselliği kullanılabilir (örneğin, paket geri yüklemesi, Otomasyon).

Bir bulut klasörle eşitlemenin simgeler şunlardır:

* Hatalar oluştuğunda geri alma için sürüm denetimi yok.
* Otomatik dağıtım, el ile eşitleme gereklidir.

### <a name="howtodropbox"></a>Bir bulut klasörle eşitleniyor tarafından dağıtma
İçinde [Azure Portal](https://portal.azure.com), OneDrive veya Dropbox gibi bulut depolama alanınızda içerik eşitleme için bir klasör belirtmek, bu klasördeki içerik ve uygulama kodu ile çalışma ve App Service'e bir düğmeyi tıklatarak ile eşitleme.

* [Eşitleme Azure App Service'e bir bulut klasöründen içerik](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Sürekli bir bulut tabanlı bir kaynak denetimi Hizmeti'nden dağıtma
Geliştirme ekibiniz gibi bir bulut tabanlı bir kaynak kodu Yönetimi (SCM) hizmet kullanıyorsa [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), veya [BitBucket](https://bitbucket.org/), uygulamayı yapılandırma Deponuzda ile tümleştirmek ve sürekli olarak dağıtmak için hizmet. 

Bir bulut tabanlı bir kaynak denetimi Hizmeti'nden dağıtma uzmanları şunlardır:

* Geri alma etkinleştirmek için sürüm denetimi.
* Sürekli dağıtım Git (ve uygun olan yerlerde Mercurial) yapılandırma yeteneği depoları. 
* Dal özgü dağıtım farklı dalları farklı [yuvaları](web-sites-staged-publishing.md).
* Kudu dağıtım Altyapısı'ndaki tüm işlevselliği kullanılabilir (örneğin dağıtım sürüm oluşturma, geri alma, paket geri yüklemesi, Otomasyon).

Bir bulut tabanlı bir kaynak denetimi Hizmeti'nden dağıtma con aşağıdaki gibidir:

* Gereken ilgili SCM hizmeti bazı bilgisi.

### <a name="vsts"></a>Sürekli bir bulut tabanlı bir kaynak denetimi Hizmeti'nden dağıtma
İçinde [Azure Portal](https://portal.azure.com), GitHub, Bitbucket ve Visual Studio Team Services sürekli dağıtımı yapılandırabilirsiniz.

* [Azure uygulama hizmeti için sürekli dağıtım](app-service-continuous-deployment.md). 

El ile Azure Portal tarafından listelenmeyen bir bulut deposu sürekli dağıtımını yapılandırmak nasıl öğrenmek için (gibi [GitLab](https://gitlab.com/)), bkz: [el ile adımları kullanarak sürekli dağıtım ayarı](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Yerel Git dağıtma
Geliştirme ekibiniz üzerinde Git dayalı bir şirket içi yerel kaynak kodu Yönetimi (SCM) hizmetini kullanıyorsa, bu uygulama hizmeti için dağıtım kaynağı olarak yapılandırabilirsiniz. 

Yerel Git dağıtma uzmanları şunlardır:

* Geri alma etkinleştirmek için sürüm denetimi.
* Dal özgü dağıtım farklı dalları farklı [yuvaları](web-sites-staged-publishing.md).
* Kudu dağıtım Altyapısı'ndaki tüm işlevselliği kullanılabilir (örneğin dağıtım sürüm oluşturma, geri alma, paket geri yüklemesi, Otomasyon).

Yerel Git dağıtma dezavantajlarını aşağıdaki gibidir:

* Gerekli ilgili SCM sisteminizin bazı bilgisi.
* Sürekli dağıtım için hiçbir anahtar teslim çözümleri. 

### <a name="vsts"></a>Yerel Git dağıtma
İçinde [Azure Portal](https://portal.azure.com), yerel Git dağıtımı yapılandırabilirsiniz.

* [Azure uygulama hizmeti için yerel Git dağıtımı](app-service-deploy-local-git.md). 
* [Web uygulamaları için herhangi bir git/hg deposuna yayımlama](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Bir IDE kullanarak dağıtın
Zaten kullanıyorsanız, [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) ile bir [Azure SDK'sı](https://azure.microsoft.com/downloads/), veya diğer IDE paketlerini [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), ve [ Intellij Idea](https://www.jetbrains.com/idea/), IDE içinde doğrudan Azure dağıtabilirsiniz. Bu seçenek, bir tek tek geliştirici için idealdir.

Visual Studio, tüm üç dağıtım işlemleri (FTP, Git ve Web dağıtımı), tercihinize bağlı olarak FTP veya Git tümleştirmesi varsa diğer IDE App Service'e dağıtabilirsiniz sırada destekler (bkz [dağıtım işlemlerine genel bakış](#overview)).

Bir IDE kullanarak dağıtma uzmanları şunlardır:

* Potansiyel olarak uçtan uca uygulama yaşam döngüsü için araç en aza indirin. Geliştirme, hata ayıklama, izlemek ve uygulamanızı IDE'yi dışında taşımadan Azure tüm dağıtın. 

Bir IDE kullanarak dağıtma simgeler şunlardır:

* Araç karmaşıklığı eklendi.
* Hala bir takım projesi için bir kaynak denetimi sistemi gerektirir.

<a name="vspros"></a>Azure SDK ile Visual Studio kullanarak dağıtma ek uzmanları şunlardır:

* Azure SDK'sı Azure kaynaklarının Visual Studio'da kullanıcılarının bu birinci sınıf sağlar. Oluşturmak, silme, düzenleme, Başlat ve uygulamaları durdurmak, arka uç SQL veritabanını sorgulamasını, Azure uygulaması ve daha fazlasını Canlı-debug. 
* Azure üzerinde kod dosyaları düzenleme dinamik.
* Azure üzerinde Canlı uygulamaların hata ayıklama.
* Tümleşik Azure Gezgini.
* Yalnızca fark dağıtımı. 

### <a name="vs"></a>Visual Studio'dan doğrudan dağıtma
* [Azure ve ASP.NET kullanmaya başlama](app-service-web-get-started-dotnet.md). Nasıl oluşturmak ve Visual Studio ve Web dağıtımı kullanarak basit bir ASP.NET MVC web projesi dağıtma.
* [Azure Visual Studio'yu kullanarak Web işleri dağıtmak için nasıl](websites-dotnet-deploy-webjobs.md). Konsol uygulaması projeleri WebJobs olarak dağıtma şekilde yapılandırmak nasıl.  
* [Visual Studio kullanarak ASP.NET Web dağıtımı](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Dağıtım görevleri daha kapsamlı bir dizi diğerlerinden bu listede kapsayan bir 12 öğretici bölümlük. Öğretici yazılmıştır, ancak daha sonra eklenen notları neyin eksik olduğu açıklayan bu yana bazı Azure dağıtım özellikleri eklenmiştir.
* [ASP.NET Web sitesi Azure Visual Studio 2012'de bir Git deposundan doğrudan dağıtma](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Visual Studio, Git ve Git deposuna bağlanan Azure Kod yürütmek için eklenti Git kullanarak bir ASP.NET web projesi dağıtma konusunda açıklanmaktadır. Visual Studio 2013'ten başlayarak, Git desteğini yerleşik olarak bulunur ve bir eklenti yüklenmesini gerektirmez.

### <a name="aztk"></a>Eclipse ve Intellij Idea için Azure araç takımları kullanarak dağıtma
Microsoft Eclipse ve Intellij aracılığıyla doğrudan Azure için Web uygulamalarını dağıtmak mümkün kılar [Eclipse için Azure Araç Seti](../azure-toolkit-for-eclipse.md) ve [Intellij için Azure Araç Seti](../azure-toolkit-for-intellij.md). Aşağıdaki öğreticiler IDE ya da Azure'u basit bir "Hello" world Web uygulaması dağıtmada söz konusu adımları gösterilmektedir:

* [Eclipse Azure'da Hello World Web uygulaması oluşturmak](app-service-web-eclipse-create-hello-world-web-app.md). Bu öğretici Azure araç setini Eclipse için oluşturmak ve bir Hello World Web uygulaması için Azure dağıtmak için nasıl kullanılacağını gösterir.
* [Intellij Azure'da Hello World Web uygulaması oluşturmak](app-service-web-intellij-create-hello-world-web-app.md). Bu öğretici Intellij için Azure araç seti oluşturmak ve bir Hello World Web uygulaması için Azure dağıtmak için nasıl kullanılacağını gösterir.

## <a name="automate"></a>Komut satırı araçlarını kullanarak dağıtımı otomatik hale getir
Komut satırı terminal seçim geliştirme ortamı olarak tercih ederseniz, komut satırı araçlarını kullanarak App Service uygulamanız için dağıtım görevlerini komut dosyası oluşturabilirsiniz. 

Komut satırı araçlarını kullanarak dağıtma uzmanları şunlardır:

* Dağıtım senaryoları etkinleştirir eşitlenebilir.
* Azure kaynaklarını ve kod dağıtım sağlama tümleştirin.
* Azure dağıtım varolan sürekli tümleştirme komut dosyalarına tümleştirin.

Komut satırı araçlarını kullanarak dağıtma simgeler şunlardır:

* Değil GUI tercih ederek geliştiriciler için.

### <a name="automatehow"></a>Komut satırı araçları ile dağıtım otomatikleştirme

Bkz: [komut satırı araçları ile Azure uygulamanızı dağıtımını otomatik hale](app-service-deploy-command-line.md) komut satırı araçları ve öğreticiler bağlantılar listesi. 

## <a name="nextsteps"></a>Sonraki Adımlar
Bazı senaryolarda kolayca geri ve ileri bir hazırlama ve üretim sürümü, uygulamanızın arasında geçiş yapabilmek isteyebilirsiniz. Daha fazla bilgi için bkz: [Web uygulamaları üzerinde hazırlanmış dağıtımı](web-sites-staged-publishing.md).

Bir yedekleme ve geri yükleme planı hazır olması, tüm dağıtım iş akışı önemli bir parçasıdır. Uygulama hizmeti hakkında bilgi için yedekleme ve özelliğini geri yükleme, bkz: [Web uygulama yedeklemeler](web-sites-backup.md).  

Uygulama hizmeti dağıtım erişimi yönetmek için Azure'nın rol tabanlı erişim denetimi kullanma hakkında daha fazla bilgi için bkz: [RBAC ve Web uygulaması yayımlama](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

