---
title: aaaDeploy, uygulama tooAzure App Service | Microsoft Docs
description: "Bilgi nasıl toodeploy, uygulama tooAzure uygulama hizmeti."
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
ms.openlocfilehash: 5c84e4ca502874209d750c94efeb86a59aa71a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service"></a>Uygulama hizmeti, uygulama tooAzure dağıtma
Bu makalede hello en iyi seçenek toodeploy hello dosyaları web uygulaması, mobil uygulama arka ucu veya API uygulaması için çok belirlemenize yardımcı olur[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)ve ardından yönergeleri belirli tooyour tooappropriate kaynaklarla yol gösterir tercih edilen seçenek.

## <a name="overview"></a>Azure uygulama hizmeti dağıtımına genel bakış
Azure uygulama hizmeti hello uygulama çerçevesi sizin için (ASP.NET, PHP, Node.js, vb.) korur. Bazı çerçeveler Java ve Python gibi sahipken, varsayılan olarak etkin, basit bir onay işareti yapılandırma tooenable gerekebilir. Ayrıca, hello PHP sürümünü veya hello verileri, çalışma zamanının gibi uygulama çerçevesi özelleştirebilirsiniz. Daha fazla bilgi için bkz: [uygulamanızı Azure App Service'te yapılandırma](web-sites-configure.md).

Hello web sunucusu veya uygulama çerçevesi hakkında tooworry yok olduğundan, dağıtma, uygulama tooApp hizmet kodunuzu, ikili dosyaları, içerik dosyaları ve bunların ilgili dizin yapısını toohello dağıtma bir konudur [   **/site /wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) Azure (veya hello **/site/wwwroot/App_Data/işleri/** Web işleri için dizin). Uygulama hizmeti üç farklı dağıtım işlemlerini destekler. Bu makaledeki tüm hello dağıtım yöntemleri işlemlerini takip hello birini kullanın: 

* [FTP veya FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): kullanım için sık kullandığınız FTP veya FTPS gelen, dosya tooAzure aracı toomove etkin [FileZilla](https://filezilla-project.org) toofull özellikli IDE ister [NetBeans](https://netbeans.org). Dosya karşıya yükleme işlemi kesinlikle budur. Hiçbir ek hizmetleri App Service tarafından sürüm denetimi, dosya yapısı yönetimi, vb. gibi sağlanır. 
* [Kudu (Git/Mercurial veya OneDrive/Dropbox gibi)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu olan hello [dağıtım altyapısını](https://github.com/projectkudu/kudu/wiki) App Service'te. Kod tooKudu doğrudan herhangi depodan iletin. Kudu kod tooit, sürüm denetimi, paket geri yükleme, MSBuild, dahil olmak üzere itildiği zaman eklenen hizmetleri de sağlar ve [web kancaları](https://github.com/projectkudu/kudu/wiki/Web-hooks) sürekli dağıtım ve diğer otomatik görevleri. Merhaba Kudu dağıtım altyapısı, dağıtım kaynakları 3 farklı türlerini destekler:   
  
  * OneDrive ve Dropbox içerik eşitleme   
  * Otomatik eşitleme GitHub, Bitbucket ve Visual Studio Team Services ile sürekli dağıtımın deposu tabanlı  
  * El ile eşitleme yerel Git deposu tabanlı dağıtımla  
* [Web dağıtımı](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): dağıtma kod tooApp hizmeti doğrudan sık kullanılan Microsoft Visual Studio kullanarak hello dağıtım tooIIS sunucuları otomatikleştirir aynı araçları gibi araçları. Bu araç yalnızca fark dağıtım, veritabanı oluşturma, bağlantı dizeleri, vb. dönüştürmeleri destekler. Web dağıtımı ikili dosyaları oldukları önce oluşturulan uygulama tooAzure dağıtılan Kudu farklıdır. Benzer tooFTP hiçbir ek hizmetleri App Service tarafından sağlanır.

Popüler web geliştirme araçları, bir veya daha fazla bu dağıtım işlemleri destekler. Merhaba seçtiğiniz aracı hello dağıtım işlemleri belirlerken yararlanabileceğiniz, Merhaba, elden gerçek DevOps işlevselliği bağlıdır hello dağıtım işlemi hello birleşimi ve hello belirli araçları, seçin. Örneğin, Web dağıtımı gerçekleştirirseniz [Azure SDK ile Visual Studio](#vspros), Kudu Otomasyon alma olsa bile, paket geri yüklemesi ve MSBuild Otomasyon Visual Studio'da alın. 

> [!NOTE]
> Bu dağıtım işlemleri gerçekten yok [sağlama Azure kaynaklarını hello](../azure-resource-manager/resource-group-template-deploy-portal.md) , uygulamanız gerekebilir. Ancak, bağlantılı hello nasıl-tooarticles çoğunu size nasıl tooprovision uygulama hello ve, kod tooit uçtan uca dağıtmak gösterir. Hello Azure kaynaklarında sağlamaya yönelik ek seçenekler bulabileceğiniz [komut satırı araçlarını kullanarak dağıtım otomatikleştirmek](#automate) bölümü.
> 
> 

## <a name="ftp"></a>FTP içeren dosyaları karşıya yükleyerek elle dağıtma
Web içerik tooa web sunucunuz kopyalama kullanılan toomanually varsa, kullanabileceğiniz bir [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) Windows Explorer gibi yardımcı programı toocopy dosyaları veya [FileZilla](https://filezilla-project.org/).

dosyaları el ile kopyalama hello uzmanları şunlardır:

* Benzerlik ve FTP araçları için en düşük karmaşıklık. 
* Tam olarak dosyalarınızı nerede kalacaklarını bilmek.
* Ek güvenlik FTPS ile.

dosyaları el ile kopyalama hello simgeler şunlardır:

* Tooknow sahip nasıl toodeploy toohello doğru dizinleri App Service'te dosyaları. 
* Hatalar oluştuğunda geri alma için sürüm denetimi yok.
* Dağıtım sorunlarını gidermek için yerleşik dağıtım geçmişi yok.
* Birçok FTP aracı yoksa ve yalnızca fark kopyalanmasını sağlayan yalnızca tüm hello dosyaları kopyalamak için olası uzun dağıtım zaman.  

### <a name="howtoftp"></a>FTP ile nasıl tooupload dosyaları
Merhaba [Azure Portal](https://portal.azure.com) tooconnect tooyour uygulamanın dizinleri FTP veya FTPS kullanma duyduğunuz tüm hello bilgi verir.

* [Uygulama hizmeti, uygulama tooAzure dağıtmak FTP kullanma](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Bir bulut klasörle eşitleniyor tarafından dağıtma
İyi bir seçenek çok[dosyaları el ile kopyalayarak](#ftp) dosya ve klasörleri tooApp hizmet OneDrive ve Dropbox gibi bir bulut Depolama hizmetinden eşitleniyor. Bir bulut klasörle eşitleniyor hello Kudu dağıtım işlemlerinde kullanır (bkz [dağıtım işlemlerine genel bakış](#overview)).

bir bulut klasörle eşitlemenin hello uzmanları şunlardır:

* Basitlik dağıtım. Yerel çalışma dizininizi da dağıtım dizininize gelir Masaüstü eşitleme istemciler, OneDrive ve Dropbox gibi hizmetler sağlar.
* Tek tıklamayla dağıtımı.
* Merhaba Kudu dağıtım Altyapısı'ndaki tüm işlevselliği kullanılabilir (örneğin, paket geri yüklemesi, Otomasyon).

bir bulut klasörle eşitlemenin hello simgeler şunlardır:

* Hatalar oluştuğunda geri alma için sürüm denetimi yok.
* Otomatik dağıtım, el ile eşitleme gereklidir.

### <a name="howtodropbox"></a>Nasıl bir bulut klasörle eşitleniyor tarafından toodeploy
Merhaba, [Azure Portal](https://portal.azure.com), OneDrive veya Dropbox gibi bulut depolama alanınızda içerik eşitleme için bir klasör belirtmek, bu klasördeki içerik ve uygulama kodu ile çalışır ve eşitleme tooApp hizmeti ile Merhaba bir düğmesine tıklayın.

* [Eşitleme bulut klasörü tooAzure uygulama hizmeti içerikten](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Sürekli bir bulut tabanlı bir kaynak denetimi Hizmeti'nden dağıtma
Geliştirme ekibiniz gibi bir bulut tabanlı bir kaynak kodu Yönetimi (SCM) hizmet kullanıyorsa [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), veya [BitBucket](https://bitbucket.org/), uygulamayı yapılandırma Deponuzda ile toointegrate hizmet ve sürekli olarak dağıtın. 

bir bulut tabanlı bir kaynak denetimi Hizmeti'nden dağıtma hello uzmanları şunlardır:

* Sürüm denetimi tooenable geri alır.
* Özelliği tooconfigure sürekli dağıtım Git (ve uygun olan yerlerde Mercurial) depoları. 
* Dal özgü dağıtımı, farklı dalları toodifferent dağıtabilir [yuvaları](web-sites-staged-publishing.md).
* Merhaba Kudu dağıtım Altyapısı'ndaki tüm işlevselliği kullanılabilir (örneğin dağıtım sürüm oluşturma, geri alma, paket geri yüklemesi, Otomasyon).

bir bulut tabanlı bir kaynak denetimi Hizmeti'nden dağıtma hello con aşağıdaki gibidir:

* Bazı bilgi gerekli hello ilgili SCM hizmet.

### <a name="vsts"></a>Nasıl toodeploy sürekli bir kaynaktan bulut tabanlı denetim hizmeti
Merhaba, [Azure Portal](https://portal.azure.com), GitHub, Bitbucket ve Visual Studio Team Services sürekli dağıtımı yapılandırabilirsiniz.

* [Sürekli dağıtım tooAzure uygulama hizmeti](app-service-continuous-deployment.md). 

nasıl tooconfigure sürekli dağıtım depodan tarafından listelenmeyen el ile bir bulut hello Azure Portal çıkışı toofind (gibi [GitLab](https://gitlab.com/)), bkz: [el ile adımları kullanarak sürekli dağıtım ayarı](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Yerel Git dağıtma
Geliştirme ekibiniz üzerinde Git dayalı bir şirket içi yerel kaynak kodu Yönetimi (SCM) hizmetini kullanıyorsa, bu dağıtım kaynağı tooApp hizmet yapılandırabilirsiniz. 

Yerel Git dağıtma uzmanları şunlardır:

* Sürüm denetimi tooenable geri alır.
* Dal özgü dağıtımı, farklı dalları toodifferent dağıtabilir [yuvaları](web-sites-staged-publishing.md).
* Merhaba Kudu dağıtım Altyapısı'ndaki tüm işlevselliği kullanılabilir (örneğin dağıtım sürüm oluşturma, geri alma, paket geri yüklemesi, Otomasyon).

Yerel Git dağıtma dezavantajlarını aşağıdaki gibidir:

* Gerekli hello ilgili SCM sisteminizin bazı bilgisi.
* Sürekli dağıtım için hiçbir anahtar teslim çözümleri. 

### <a name="vsts"></a>Nasıl toodeploy yerel Git
Merhaba, [Azure Portal](https://portal.azure.com), yerel Git dağıtımı yapılandırabilirsiniz.

* [Yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md). 
* [Herhangi bir git/hg deposuna tooWeb uygulamalardan yayımlama](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Bir IDE kullanarak dağıtın
Zaten kullanıyorsanız, [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) ile bir [Azure SDK'sı](https://azure.microsoft.com/downloads/), veya diğer IDE paketlerini [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), ve [ Intellij Idea](https://www.jetbrains.com/idea/), IDE içinde tooAzure doğrudan dağıtabilirsiniz. Bu seçenek, bir tek tek geliştirici için idealdir.

Visual Studio, tüm üç dağıtım işlemleri (FTP, Git ve Web dağıtımı), tercihinize bağlı olarak FTP veya Git tümleştirmesi varsa diğer IDE tooApp hizmet dağıtabilirsiniz sırada destekler (bkz [dağıtım işlemlerine genel bakış](#overview)).

bir IDE kullanarak dağıtma hello uzmanları şunlardır:

* Potansiyel olarak, uçtan uca uygulama yaşam döngüsü için tooling hello en aza indirin. Geliştirme, hata ayıklama, izlemek ve IDE'yi dışında tüm taşımadan uygulama tooAzure dağıtın. 

bir IDE kullanarak dağıtma hello simgeler şunlardır:

* Araç karmaşıklığı eklendi.
* Hala bir takım projesi için bir kaynak denetimi sistemi gerektirir.

<a name="vspros"></a>Azure SDK ile Visual Studio kullanarak dağıtma ek uzmanları şunlardır:

* Azure SDK'sı Azure kaynaklarının Visual Studio'da kullanıcılarının bu birinci sınıf sağlar. Oluşturma silme düzenleme, başlatmak ve uygulamaları, sorgu hello arka uç SQL veritabanı, Canlı-debug hello Azure uygulaması ve daha fazlasını durdurun. 
* Azure üzerinde kod dosyaları düzenleme dinamik.
* Azure üzerinde Canlı uygulamaların hata ayıklama.
* Tümleşik Azure Gezgini.
* Yalnızca fark dağıtımı. 

### <a name="vs"></a>Nasıl doğrudan toodeploy Visual Studio'dan
* [Azure ve ASP.NET kullanmaya başlama](app-service-web-get-started-dotnet.md). Nasıl toocreate ve Visual Studio ve Web dağıtımı kullanarak basit bir ASP.NET MVC web projesi dağıtma.
* [Nasıl tooDeploy Visual Studio kullanarak Azure Web işleri](websites-dotnet-deploy-webjobs.md). Böylece WebJobs olarak dağıtma nasıl tooconfigure konsol uygulaması projeleri.  
* [Visual Studio kullanarak ASP.NET Web dağıtımı](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Başkalarının bu listede hello daha dağıtım görevleri daha eksiksiz bir aralığını kapsayan bir 12 öğretici bölümlük. Merhaba öğretici yazılmıştır, ancak daha sonra eklenen notları neyin eksik olduğu açıklayan bu yana bazı Azure dağıtım özellikleri eklenmiştir.
* [Bir ASP.NET Web sitesi tooAzure bir Git deposundan Visual Studio 2012'de doğrudan dağıtma](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Nasıl toodeploy bir ASP.NET web projesi Visual hello Git eklenti toocommit hello kod tooGit kullanarak ve Azure toohello Git deposu bağlanarak Studio'da açıklanmaktadır. Visual Studio 2013'ten başlayarak, Git desteğini yerleşik olarak bulunur ve bir eklenti yüklenmesini gerektirmez.

### <a name="aztk"></a>Nasıl toodeploy kullanarak hello Azure araç takımları Eclipse ve Intellij Idea için
Microsoft hello aracılığıyla doğrudan Eclipse ve Intellij olası toodeploy Web Apps tooAzure kılar [Eclipse için Azure Araç Seti](../azure-toolkit-for-eclipse.md) ve [Intellij için Azure Araç Seti](../azure-toolkit-for-intellij.md). Merhaba aşağıdaki öğreticiler ya da IDE kullanarak basit bir "Hello" world Web uygulaması tooAzure dağıtmada oynayan hello adımları gösterilmektedir:

* [Eclipse Azure'da Hello World Web uygulaması oluşturmak](app-service-web-eclipse-create-hello-world-web-app.md). Bu öğretici nasıl toouse Azure araç setini Eclipse toocreate hello ve Azure Hello World Web uygulaması dağıtma gösterir.
* [Intellij Azure'da Hello World Web uygulaması oluşturmak](app-service-web-intellij-create-hello-world-web-app.md). Bu öğretici nasıl toouse Azure Araç Seti için Intellij toocreate hello ve Azure Hello World Web uygulaması dağıtma gösterir.

## <a name="automate"></a>Komut satırı araçlarını kullanarak dağıtımı otomatik hale getir
Tercih ettiğiniz hello geliştirme ortamı olarak hello komut satırı terminal tercih ederseniz, komut satırı araçlarını kullanarak App Service uygulamanız için dağıtım görevlerini komut dosyası oluşturabilirsiniz. 

Komut satırı araçlarını kullanarak dağıtma uzmanları şunlardır:

* Dağıtım senaryoları etkinleştirir eşitlenebilir.
* Azure kaynaklarını ve kod dağıtım sağlama tümleştirin.
* Azure dağıtım varolan sürekli tümleştirme komut dosyalarına tümleştirin.

Komut satırı araçlarını kullanarak dağıtma simgeler şunlardır:

* Değil GUI tercih ederek geliştiriciler için.

### <a name="automatehow"></a>Nasıl tooautomate dağıtımı ile komut satırı araçları

Bkz: [komut satırı araçları ile Azure uygulamanızı dağıtımını otomatik hale](app-service-deploy-command-line.md) komut satırı araçları ve bağlantıları tootutorials listesi. 

## <a name="nextsteps"></a>Sonraki Adımlar
Bazı senaryolarda toobe mümkün tooeasily arasında geçiş yapma ve geriye bir hazırlama ve üretim sürümü, uygulamanızın isteyebilirsiniz. Daha fazla bilgi için bkz: [Web uygulamaları üzerinde hazırlanmış dağıtımı](web-sites-staged-publishing.md).

Bir yedekleme ve geri yükleme planı hazır olması, tüm dağıtım iş akışı önemli bir parçasıdır. Merhaba uygulama hizmeti yedekleme ve geri yükleme özelliği hakkında daha fazla bilgi için bkz: [Web uygulama yedeklemeler](web-sites-backup.md).  

Nasıl toouse Azure'nın rol tabanlı erişim denetimi toomanage erişim tooApp hizmet dağıtımı hakkında daha fazla bilgi için bkz: [RBAC ve Web uygulaması yayımlama](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

