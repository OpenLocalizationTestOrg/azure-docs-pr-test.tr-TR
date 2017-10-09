---
title: "Azure üzerinde geliştiriciler için başlatılan aaaGet Kılavuzu | Microsoft Docs"
description: "Bu konuda geliştirme ihtiyaçlarına hello Microsoft Azure platformu kullanmaya tooget isteyen geliştiriciler için önemli bilgiler sağlar."
services: 
cloud: 
documentationcenter: 
author: ggailey777
manager: erikre
ms.assetid: 
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: glenga
ms.openlocfilehash: 72dc2678db7738923d4bc7783e297fea6fcded83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-guide-for-azure-developers"></a>Azure geliştiricileri için kullanmaya başlama kılavuzu

## <a name="what-is-azure"></a>Azure nedir?

Azure, mevcut uygulamalarınızı barındırmak, yeni uygulamaların hello geliştirmesini akıcı hale getirmek ve hatta şirket içi uygulamalar geliştirmek tam bulut platformudur. Azure tümleştirir toodevelop gerektiğini hello bulut Hizmetleri, test, dağıtmak ve uygulamalarınızı yönetmek — hello verimliliği bulutun avantajlarını çalışırken bilgisayar.

Azure uygulamalarınızda barındırarak küçük başlayın ve müşteri talebi arttıkça uygulamanızı kolayca ölçeklendirin. Azure bile farklı bölgelere arasında yük devretme de dahil olmak üzere, yüksek kullanılabilirlik uygulamaları için gerekli olan hello güvenilirlik de sunar. Merhaba [Azure portal](https://portal.azure.com) tüm Azure hizmetlerinde kolayca yönetmenize olanak sağlar. Hizmete özgü API'leri ve şablonlar kullanarak hizmetlerinizi program aracılığıyla da yönetebilirsiniz.

**Kimler bu**: Giriş toohello uygulama geliştiricileri için Azure platformu bu kılavuzdur. Kılavuz ve Azure veya geçirme mevcut uygulamaları tooAzure yeni uygulamalarda derleme toostart gereken yönü sağlar.

## <a name="where-do-i-start"></a>Nereden başlamalıyım?

Azure'un sunduğu tüm hello Hizmetleri ile hangi hizmetlerini çözüm mimarisi toosupport gereken zorlu bir görev toofigure olabilir. Bu bölümde öne çıkan özellikleri hello Azure geliştiriciler sık kullandığınız Hizmetleri. Tüm Azure hizmetlerini bir listesi için bkz: Merhaba [Azure belgelerine](../../index.md).

İlk olarak, hakkında karar toohost uygulamanızı azure'da. Bir sanal makine (VM) bütün altyapınızı toomanage zorunda. Azure sağlar hello platform yönetim olanakları kullanabilir miyim? Belki de yalnızca bir sunucusuz framework toohost kodu yürütmesi gerekiyor?

Uygulamanızı Azure için çeşitli seçenekler sağlayan bulut depolama gerekir. Azure'nın Kurumsal kimlik doğrulamasının avantajından yararlanabilirsiniz. Aynı zamanda bulut tabanlı geliştirme ve izleme ve çoğu barındırma hizmetleri DevOps tümleştirme sunmak için de araçlar vardır.

Şimdi, bazı uygulamalarınız için araştırma öneririz hello belirli hizmetleri bakalım.

### <a name="application-hosting"></a>Uygulama barındırma

Azure uygulamanızı birkaç işlem bulut tabanlı teklifleri toorun sunar, böylece hello altyapı ayrıntıları hakkında tooworry yok. Kolayca artırın veya kaynaklarınızı, uygulama kullanımınızı büyüdükçe ölçeğinizi.

Azure uygulama geliştirme ve gereksinimlerini barındırma destek hizmetleri sunar. Azure sağlar olarak-hizmet altyapı (Iaas) uygulama barındırma üzerinde denetim tam toogive. Azure'nın hizmet olarak platform (PaaS) teklifleri hello gerekli hizmetleri toopower uygulamalarınızı tam yönetilen sağlar. Olduğu bile true sunucusuz Azure'da barındıran tüm toodo gereken kodunuzu yazın.

![Azure uygulama seçenekleri barındırma](./media/azure-developer-guide/azure-developer-hosting-options.png)


#### <a name="azure-app-service"></a>Azure App Service 

Web tabanlı projelerinizi hello hızlı yolu toopublish istediğinizde, Azure App Service göz önünde bulundurun. Uygulama hizmeti kolay tooextend sağlar, mobil istemcileriniz uygulamaları toosupport web ve kolayca tüketilen REST API'leri yayımlayın. Bu platform, üretim ve sürekli ve kapsayıcı tabanlı dağıtımlar test sosyal sağlayıcılardan, trafiği tabanlı otomatik ölçeklendirmenin kullanarak kimlik doğrulaması sağlar.

App Service içinde bir uygulama oluşturduğunuzda, şu türlerini hello birini seçin:

- [Web uygulamaları](../../app-service-web/app-service-web-overview.md): .NET, Java, PHP, Node.js ve Python içinde yazılmış Web sitelerini ve web uygulamalarını barındırmak sağlar.

- [Mobile Apps](../../app-service-mobile/app-service-mobile-value-prop.md): mobil aygıtlardan genişletir Web Apps toosupport erişim. Sosyal sağlayıcılardan ve Azure Active Directory (Azure AD) ile kimlik doğrulamasını etkinleştirir, arka uç depolama alanı sağlar ve tümleşir [Azure Notification Hubs](../../notification-hubs/notification-hubs-push-notification-overview.md) anında iletme bildirimleri için.

- [API Apps](../../app-service-api/app-service-api-apps-why-best-platform.md): daha fazla böylece istemciler kolayca bunları tüketebileceği Apı'lerinizi Swagger meta verilerle hello bulutta güvenli bir şekilde kullanıma sunma olanak tanır.

Tüm üç uygulama türleri paylaştığından uygulama hizmeti çalışma zamanı Merhaba, Web sitesi barındırma, mobil istemcileri desteklemek ve tümünü'dan Azure, Apı'lerinizi kullanıma aynı proje ya da çözüm hello. Uygulama hizmeti hakkında daha fazla toolearn bkz [nasıl uygulama hizmetinin çalışır](../../app-service/app-service-how-works-readme.md).

Uygulama hizmeti ile DevOps göz önünde tasarlanmıştır. Bu, GitHub Web kancası, Jenkins, Visual Studio Team Services, TeamCity ve diğerleri de dahil olmak üzere yayımlama ve sürekli tümleştirme dağıtımları için çeşitli araçlar destekler.

Hello kullanarak mevcut uygulamaları tooApp hizmet geçirebilirsiniz [çevrimiçi geçiş aracı](https://www.migratetoazure.net/).

>**Zaman toouse**: kullanım uygulama varolan web uygulamaları tooAzure geçirilirken hizmeti ve web uygulamaları için tam olarak yönetilen bir ana bilgisayar platformu gerektiğinde. Uygulamanızla REST API'lerini kullanıma veya toosupport mobil istemcilerin gerek duyduğunuzda uygulama hizmetini de kullanabilirsiniz.

>**Başlama**: uygulama hizmeti kolay toocreate kolaylaştırır ve ilk dağıtma [web uygulaması](../../app-service-web/web-sites-dotnet-get-started.md), [mobil uygulama](../../app-service-mobile/app-service-mobile-ios-get-started.md), veya [API uygulaması](../../app-service-api/app-service-api-dotnet-get-started.md).

>**Şimdi deneyin**: uygulama hizmeti bir Azure hesabı için toosign zorunda kalmadan bir kısa süreli uygulama tootry hello platform sağlama olanak sağlar. Merhaba platform deneyin ve [Azure uygulama hizmeti uygulamanızı oluşturun](https://tryappservice.azure.com/).

#### <a name="azure-virtual-machines"></a>Azure Sanal Makineler

Olarak-hizmet altyapı (Iaas) sağlayıcısı olarak, Azure dağıtmanıza olanak tanır tooor, uygulama tooeither Windows veya Linux sanal makineleri geçirme. Azure Virtual Network ile birlikte, Azure sanal makineleri Windows veya Linux sanal makineleri tooAzure hello dağıtımını destekler. VM'ler ile Merhaba makinenin hello yapılandırmasını toplam denetime sahip olursunuz. Sanal makineleri kullanırken, tüm sunucu yazılımı yükleme, yapılandırma, Bakım ve işletim sistemi için düzeltme ekleri sorumlu.

Vm'lerde bulunan denetim düzeyini Hello nedeniyle, bir PaaS modele uymayan Azure üzerinde çeşitli sunucu iş yükleri çalıştırabilirsiniz. Bu iş yükleri, veritabanı sunucuları, Windows Server Active Directory ve Microsoft SharePoint içerir. Daha fazla bilgi için ya da hello sanal makineleri belgelerine bakın [Linux](/azure/virtual-machines/linux/) veya [Windows](/azure/virtual-machines/windows/).

>**Zaman toouse**: tam istediğinizde kullanım sanal makineleri toomake değişiklikleri gerek kalmadan, uygulama altyapısı veya toomigrate şirket içi uygulama iş yükleri tooAzure denetleyin.

>**Başlama**: oluşturmak bir [Linux VM](../../virtual-machines/virtual-machines-linux-quick-create-portal.md) veya [Windows VM](../../virtual-machines/virtual-machines-windows-hero-tutorial.md) hello Azure Portalı'ndan.

#### <a name="azure-functions-serverless"></a>Azure işlevleri (sunucusuz)

Yerine çıkışı oluşturma ve tam bir uygulama veya hello altyapı toorun kodunuzu yönetme hakkında kaygı biri. Peki, yalnızca kodunuzu yazın ve yanıt tooevents veya bir zamanlamaya göre çalıştırılan sahip?  [Azure işlevleri](../../azure-functions/functions-overview.md) olan "sunucusuz" bir-yeni yazma sağlar ihtiyacınız kod hello sunumu stili. İşlevleriyle, HTTP isteklerini, Web kancalarını, bulut hizmeti olayları tarafından veya bir zamanlamaya göre kod yürütmeyi tetiklenir. C gibi tercih ettiğiniz geliştirme dilini içindeki kod\#, F\#, Node.js, Python veya PHP. Tüketim tabanlı faturalama ile kodunuzu yürütür ve gerektiğinde Azure ölçeklendirir hello süre için ödeme yaparsınız.

>**Zaman toouse**: Azure web tabanlı olaylar tarafından veya bir zamanlamaya göre diğer Azure Hizmetleri tarafından tetiklenen kod olduğunda işlevler kullanın. Tam bir barındırılan projesini veya yalnızca toopay kodunuzun çalıştığı hello süredir istediğinizde, yükünü hello yoktur, işlevleri de kullanabilirsiniz. toolearn daha, fazla [Azure işlevlerine genel bakış](../../azure-functions/functions-overview.md).

>**Başlama**: hello işlevleri hızlı başlangıç Öğreticisi çok izleyin[ilk işlevinizi oluşturma](../../azure-functions/functions-create-first-azure-function.md) hello portalından.

>**Şimdi deneyin**: Azure işlevleri, bir Azure hesabı için toosign gerek kalmadan kodunuzu çalıştırmak olanak sağlar. Şimdi, deneyin ve [ilk Azure işlevinizi oluşturma](https://tryappservice.azure.com/).

#### <a name="azure-service-fabric"></a>Azure Service Fabric

Azure Service Fabric, kolay toobuild kolaylaştıran bir dağıtılmış sistemler platformdur paketini, dağıtmak ve ölçeklenebilir ve güvenilir mikro. Kapsamlı uygulama yönetim özellikleri de sağlar sağlama, dağıtma, izleme, yükseltme ve düzeltme için ve dağıtılan uygulamalar siliniyor. Paylaşılan bir havuzunda makineleri çalıştırmak, uygulamaları küçük başlayın ve toohundreds ya da gerektiği şekilde makineler binlerce ölçeklendirin.

Service Fabric .NET (OWIN) ve ASP.NET Core için açık Web arabirimi ile Webapı destekler. SDK'ları .NET Core ve Java Linux'ta hizmetler oluşturmaya yönelik sağlar. Service Fabric hakkında daha fazla toolearn bkz hello [Service Fabric öğrenme yolunu](https://azure.microsoft.com/documentation/learning-paths/service-fabric/).

>**Zaman toouse:** Service Fabric olduğunda iyi bir seçimdir uygulama oluşturma ya da var olan bir uygulama toouse mikro hizmet mimarisi yeniden yazma işlemi. Daha fazla denetime ya da doğrudan erişim, hello altyapının gerektiğinde Service Fabric kullanın.

>**Kullanmaya başlama:** [ilk Azure Service Fabric uygulamanızı oluşturma](../../service-fabric/service-fabric-create-your-first-application-in-visual-studio.md).

### <a name="enhance-your-applications-with-azure-services"></a>Uygulamalarınızı Azure hizmetleriyle geliştirmek

Ayrıca barındırma, tooapplication Azure hello işlevselliği, geliştirme ve Bakım uygulamalarınızın, hem de hello Bulut ve şirket içi geliştirebilirsiniz hizmet teklifleri sağlar.

#### <a name="hosted-storage-and-data-access"></a>Barındırılan depolama ve veri erişimi

Birçok uygulama, toohost nasıl karar verir, böylece bakılmaksızın veri, uygulamanızın Microsoft azure'da depoladığınız, bir veya daha fazla depolama ve Veri Hizmetleri aşağıdaki hello göz önünde bulundurun.

-   **Azure SQL veritabanı**: hello Microsoft SQL Server altyapısını hello bulutta tablo ilişkisel veri depolamak için bir Azure tabanlı sürümü. SQL veritabanı tahmin edilebilir performans, ölçeklenebilirlik hiçbir kapalı kalma süresi, iş sürekliliği ve veri koruması sağlar.

    >**Zaman toouse**: zaman uygulamanızın gerektirdiği başvuru bütünlüğü, işlem desteği ve desteği ile veri depolama için TSQL sorgular.

    >**Başlama**: [hello Azure portal kullanarak dakika içinde bir SQL veritabanı oluşturma](../../sql-database/sql-database-get-started.md).

-   **Azure depolama**: BLOB, kuyruklar, dosyalar ve ilişkisel olmayan verileri diğer tür dayanıklı ve yüksek oranda kullanılabilir depolama sunar. Depolama hello depolama foundation VM'ler için sağlar.

    >**Zaman toouse**: zaman uygulamanızı anahtar-değer çiftleri (tablolar) gibi ilişkisel olmayan verileri depolar, BLOB'ların, paylaşımları dosyaları veya iletileri (sıralar için).

    >**Başlama**: Bu türleri depolama birini seçin: [BLOB'lar](../../storage/blobs/storage-dotnet-how-to-use-blobs.md), [tabloları](../../cosmos-db/table-storage-how-to-use-dotnet.md), [sıraları](../../storage/queues/storage-dotnet-how-to-use-queues.md), veya [dosyaları](../../storage/files/storage-dotnet-how-to-use-files.md).

-   **Azure DocumentDB**: nesne verilerini SQL sorguları özellikleri bir tam olarak yönetilen ve ölçeklenebilir NoSQL veritabanı hizmetini. Varolan MongoDB sürücüleri kullanarak DocumentDB erişebilirsiniz.
    >**Zaman toouse:** uygulamanızın JSON belgelerini toobe mümkün tooexecute SQL sorguları gerektiğinde veya MongoDB kullanıyorsanız.

    >**Başlama**: [DocumentDB C# konsol uygulaması oluşturma](../../documentdb/documentdb-get-started.md). MongoDB Geliştirici değilseniz, bkz [DocumentDB MongoDB için protokol desteği](../../documentdb/documentdb-protocol-mongodb.md).

Kullanabileceğiniz [Azure Data Factory](../../data-factory/data-factory-introduction.md) toomove mevcut şirket içi veri tooAzure. Hazır toomove veri toohello bulut yoksa [karma bağlantılar](../../biztalk-services/integration-hybrid-connection-overview.md) barındırılan uygulama hizmetiniz uygulama tooon içi kaynaklara bağlandığınız BizTalk Services olanak sağlar. Şirket içi uygulamalarınızdan tooAzure veri ve depolama hizmetleri da bağlanabilirsiniz.

#### <a name="docker-support"></a>Docker desteği

Docker kapsayıcıları, işletim sistemi sanallaştırma, bir form, uygulamaları daha etkili ve tahmin edilebilir bir şekilde dağıtmasını sağlar. Kapsayıcılı uygulama üretim hello aynı şekilde sistemlerde, geliştirme ve test gibi çalışır. Kapsayıcıları standart Docker araçlarını kullanarak yönetebilirsiniz. Var olan becerileri ve popüler açık kaynaklı araçları toodeploy kullanın ve Azure kapsayıcı tabanlı uygulamayı yönetin.

Azure, uygulamalarınızı toouse kapsayıcılarında çeşitli yöntemler sağlar.

-   **Azure Docker VM uzantısı**: Docker araçları tooact Docker ana bilgisayar olarak ile VM yapılandırmanıza olanak sağlar.

    >**Zaman toouse**: bir VM'de, uygulamalarınız için toogenerate tutarlı kapsayıcı dağıtımlarını istediğinizde ya da toouse istediğinizde [Docker Compose](https://docs.docker.com/compose/overview/).

    >**Başlama**: [hello Docker VM uzantısı kullanılarak bir Docker ortamı oluşturma](../../virtual-machines/virtual-machines-linux-dockerextension.md).

-   **Azure kapsayıcı hizmeti**: önceden kapsayıcılı toorun uygulamaları oluşturmak, yapılandırmak ve sanal makinelerde oluşan bir küme yönetmenizi sağlar. Kapsayıcı hizmeti hakkında daha fazla toolearn bkz [Azure kapsayıcı hizmeti giriş](../../container-service/container-service-intro.md).

    >**Zaman toouse**: ek planlama ve Yönetim Araçları sağlayın veya ne zaman dağıtmakta Docker Swarm kümesi toobuild üretime hazır, ölçeklenebilir ortamları gerektiğinde.

    >**Başlama**: [bir kapsayıcı hizmeti kümesini dağıtma](../../container-service/dcos-swarm/container-service-deployment.md).

-   **Docker makine**: yükleme ve Docker altyapısına sanal konaklarda docker makine komutlarını kullanarak yönetmenize olanak tanır.

    >**Zaman toouse**: tek bir Docker ana oluşturarak tooquickly prototip uygulama gerektiğinde.

-   **Uygulama hizmeti için özel Docker görüntü**: Linux üzerinde bir web uygulaması dağıttığınızda bir kapsayıcı kayıt defteri Docker kapsayıcılardan veya bir müşteri kapsayıcı kullanmanıza olanak sağlar.

    >**Zaman toouse**: Linux tooa Docker görüntü üzerinde bir web uygulaması dağıtırken.

    >**Başlama**: [Linux uygulama hizmeti için özel bir Docker görüntü kullanmak](../../app-service-web/app-service-linux-using-custom-docker-image.md).

### <a name="authentication"></a>Kimlik Doğrulaması

Önemli toonot yalnızca bildiğiniz kullanan, uygulamaları, aynı zamanda tooprevent yetkisiz erişim tooyour kaynakları kullanıyor. Azure app istemcileriniz birkaç yolu tooauthenticate sağlar.

-   **Azure Active Directory (Azure AD)**: Microsoft çok kiracılı, bulut tabanlı kimlik ve erişim yönetimi hizmeti hello. Azure AD ile tümleştirme (SSO) tooyour uygulamalarda çoklu oturum ekleyebilirsiniz. Dizin özelliklerini doğrudan Azure AD Graph API hello veya hello Microsoft Graph API kullanarak erişebilirsiniz. Yerel HTTP/REST uç noktalarını kullanarak Azure AD desteği hello OAuth2.0 yetkilendirme framework ve Open ID Connect ile tümleştirebilir ve multiplatform Azure AD kimlik doğrulama kitaplıkları hello.

    >**Zaman toouse**: tooprovide bir SSO deneyimi istediğinizde, grafik tabanlı verilerle çalışma veya kullanıcıların etki alanı tabanlı kimlik doğrulaması.

    >**Başlama**: toolearn daha, hello fazla [Azure Active Directory Geliştirici Kılavuzu](../../active-directory/active-directory-developers-guide.md).

-   **App Service kimlik doğrulaması**: uygulamanızı App Service toohost seçtiğinizde, sosyal kimlik sağlayıcıları yanı sıra Azure AD için yerleşik kimlik doğrulama desteği de alın — Facebook, Google, Microsoft ve Twitter gibi.

    >**Zaman toouse**: Azure AD kullanarak bir uygulama hizmeti uygulamasında tooenable kimlik doğrulamasını istediğinizde sosyal kimlik sağlayıcıları ya da her ikisini de.

    >**Başlama**: toolearn App Service, kimlik doğrulaması hakkında daha fazla bilgi görmek [kimlik doğrulama ve yetkilendirme Azure App Service'te](../../app-service/app-service-authentication-overview.md).

Azure, en iyi güvenlik uygulamaları hakkında daha fazla toolearn bkz [Azure güvenlik en iyi yöntemler ve yaklaşımlar](../../security/security-best-practices-and-patterns.md).

### <a name="monitoring"></a>İzleme

Uygulamanızla Azure içinde çalışır, ihtiyacınız toobe mümkün toomonitor performans sorunlarını izlemek ve müşteriler uygulamanızı nasıl kullandığını görün. Azure birkaç izleme seçeneklerini sağlar.

-   **Visual Studio Application Insights**: Canlı web uygulamalarınızın Visual Studio toomonitor ile tümleşen bir Azure barındırılan genişletilebilir bir analiz hizmetidir. Size verir toocontinuously gereksinim hello verileri, hello performans ve kullanılabilirlik, uygulamalarınızın Azure üzerinde barındırılan da veya olup olmadığını artırmak.

    >**Başlama**: izleme hello [Application Insights Öğreticisi](../../application-insights/app-insights-overview.md).

-   **Azure İzleyici**: toovisualize, sorgu, yol, arşiv ve hello ölçümleri ve Azure altyapı ve kaynaklar tarafından oluşturulan günlükleri vermemizi sağlayan bir hizmet. İzleyici hello Azure portalına bakın ve Azure kaynakları izlemek için tek bir kaynak hello veri görünümleri sağlar.
 
    >**Başlama**: [Azure İzleyicisi ile çalışmaya başlama](../../monitoring-and-diagnostics/monitoring-get-started.md).

### <a name="devops-integration"></a>DevOps tümleştirmesi

VM'ler sağlama veya web uygulamalarınızı sürekli tümleştirme ile yayımlama hello popüler DevOps Araçları'nın en Azure tümleştirir. Jenkins, GitHub, Puppet, Chef, TeamCity, Ansible, VSTS ve diğerleri gibi araçlar desteği sayesinde, zaten varsa ve varolan deneyiminizi en üst düzeye hello araçları ile çalışabilirsiniz.

>**Şimdi deneyin:** [birkaç hello DevOps tümleştirmeler deneyin](https://azure.microsoft.com/try/devops/).

>**Başlama**: bir uygulama hizmeti uygulaması için toosee DevOps seçenekleri görmek [sürekli dağıtım tooAzure uygulama hizmeti](../../app-service-web/app-service-continuous-deployment.md).


## <a name="azure-regions"></a>Azure bölgeleri

Azure Merhaba Dünya birçok bölgelerdeki genel olarak kullanılabilir olan bir genel bulut platformudur. Bir hizmet, uygulama veya azure'da VM sağladığınızda olduğunuz uygulamanızın çalıştığı belirli bir veri merkezini temsil eden bir bölge tooselect sorular veya verilerinizin depolandığı. Bu bölgeler hello üzerinde yayımlanan toospecific konumlara karşılık gelen [Azure bölgeleri](https://azure.microsoft.com/regions/) sayfası.

### <a name="choose-hello-best-region-for-your-application-and-data"></a>Uygulama ve veri için bir en iyi bölge Hello seçin

Azure kullanmanın yararları Merhaba, uygulamaları toovarious veri merkezleri Merhaba Dünya çevresinde dağıtabilirsiniz biridir. Seçtiğiniz hello bölge hello uygulamanızın performansını etkileyebilir. Örneğin, daha iyi toochoose, müşterilerin tooreduce gecikme ağ isteklerinde daha yakından toomost olan bir bölge olur. Ayrıca, bazı ülkelerde uygulamanızı dağıtmak için bölge toomeet hello yasal gereksinimlerinizi tooselect isteyebilirsiniz. Bir en iyi yöntem toostore uygulama verileri her zaman konusu hello aynı veri merkezinde veya uygulamanızı barındıran bir veri merkezinde olabildiğince yakın olası toohello veri merkezi.

### <a name="multi-region-apps"></a>Bölgeli uygulamalar

Olası rağmen Internet hatası veya doğal afet gibi bir olay nedeniyle çevrimdışı bir veri merkezinin tamamı toogo mümkün değil. Birden fazla veri merkezi tooprovide en yüksek kullanılabilirlik en iyi yöntem toohost önemli iş uygulamaları olur. Birden çok bölgeye kullanarak da genel kullanıcılar için gecikme süresini azaltmak ve esneklik için başka fırsatları uygulamaları güncelleştirirken sağlayın.

Sanal makine ve uygulama hizmetleri gibi bazı hizmetler kullanmak [Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md) bölgeleri toosupport yüksek kullanılabilirlik kurumsal uygulamalar arasında yük devretme ile tooenable bölgeli destek. Bir örnek için bkz: [Azure referans mimarisi: Web uygulaması ile yüksek kullanılabilirlik](../../guidance/guidance-web-apps-multi-region.md).

>**Zaman toouse**: yük devretme ve çoğaltma fayda enterprise ve yüksek kullanılabilirlik uygulamaları olduğunda.

## <a name="how-do-i-manage-my-applications-and-projects"></a>Benim uygulamaları ve projeleri nasıl yönetebilirim?

Azure toocreate sizin için zengin bir deneyim sağlar ve Azure kaynakları, uygulamaları ve projeleri yönetmek — hello hem program aracılığıyla [Azure portal](https://portal.azure.com/).

### <a name="command-line-interfaces-and-powershell"></a>PowerShell ve komut satırı arabirimi

Azure Bash, Terminal, hello komut istemi veya tercih ettiğiniz, komut satırı aracını kullanarak, uygulama ve hizmetlerinize hello komut satırından iki yolu toomanage sağlar. Genellikle, hello Azure portal olduğu gibi hello komut satırından hello aynı görevleri gerçekleştirebilir — oluşturma ve sanal makineler, sanal ağlar, web uygulamaları ve diğer hizmetleri yapılandırma gibi.

-   [Azure komut satırı arabirimi (CLI)](../../xplat-cli-install.md): tooan Azure aboneliğine bağlanma ve hello komut satırından Azure kaynaklarına karşı çeşitli görevleri program olanak tanır.

-   [Azure PowerShell](../../powershell-install-configure.md): bir modül kümesini sağlayan cmdlet'leriyle toomanage Azure sağlar. Windows PowerShell kullanarak kaynakları.

### <a name="azure-portal"></a>Azure portalına

Hello Azure portal toocreate kullanmak yönetebilir ve Azure kaynaklarını ve Hizmetleri Kaldır bir web tabanlı uygulamasıdır. Hello Azure portal konumundadır <https://portal.azure.com>. Özelleştirilebilir bir Pano içerir, araçları Azure kaynaklarını ve erişim toosubscription ayarlarını yönetme ve fatura bilgileri. Daha fazla bilgi için bkz: Merhaba [Azure portalına genel bakış](../../azure-portal-overview.md).

### <a name="rest-apis"></a>REST API'leri

Azure hello Azure portalı kullanıcı arabirimini destekler API'lerini bir dizi yerleşik olarak bulunur. Bu REST API'leri ayrıca program aracılığıyla sağlamak ve Azure kaynaklarına ve uygulamalarına Internet etkin herhangi bir aygıttan yönetmek desteklenen toolet çoğu. Merhaba Hello eksiksiz olarak REST API belgeleri için bkz: [Azure REST SDK'sı başvurusu](https://docs.microsoft.com/rest/api/).

### <a name="apis"></a>API'ler

Ayrıca tooREST API'leri, çoğu Azure hizmeti de program aracılığıyla kaynakları uygulamalarınızdan geliştirme platformları aşağıdaki hello için SDK'ları da dahil olmak üzere, platforma özgü Azure SDK kullanarak yönetmenizi sağlar:

-   [.NET](https://go.microsoft.com/fwlink/?linkid=834925)
-   [Node.js](http://azure.github.io/azure-sdk-for-node/)
-   [Java](https://docs.microsoft.com/java/api/)
-   [PHP](https://github.com/Azure/azure-sdk-for-php/blob/master/README.md)
-   [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/)
-   [Ruby](https://github.com/Azure/azure-sdk-for-ruby/blob/master/README.md)

Gibi hizmetleri [Mobile Apps](../../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md) ve [Azure Media Services](../../media-services/media-services-dotnet-how-to-use.md) istemci-tarafı SDK'ları toolet sağlayan web ve mobil istemci uygulamaları Hizmetleri erişim.

### <a name="azure-resource-manager"></a>Azure Resource Manager 
    
Büyük olasılıkla Azure uygulamanızı çalıştırılmasını içerir çalışma birden çok Azure Hizmetleri tüm hangi izleyin Merhaba aynı yaşam döngüsü ile bir mantıksal birim olarak düşünülebilir. Örneğin, bir web uygulaması, Web uygulamaları, SQL veritabanı, depolama, Azure Redis önbelleği ve Azure içerik teslim ağı Hizmetleri kullanabilirsiniz. [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) , iş hello kaynaklarla bir grup olarak sağlar. Dağıtma, güncelleştirme veya tek ve eşgüdümlü bir işlemle tüm hello kaynakları silin.

Ayrıca kaynakları gruplandırma ve yönetme toologically ilgili, Azure Resource Manager hello dağıtımı ve yapılandırılmasıyla ilgili kaynakların özelleştirmenize olanak sağlayan dağıtım özellikleri içerir. Örneğin, Kaynak Yöneticisi'ni kullanarak dağıtın ve birden çok sanal makine, yük dengeleyici ve bir Azure SQL veritabanı tek bir birim olarak oluşan bir uygulamayı yapılandırın.

JSON biçimli bir belge bir Azure Resource Manager şablonu kullanarak bu dağıtımlar geliştirin. Şablonları bir dağıtım tanımlamanıza ve komut dosyalarının yerine bildirim temelli şablonlar kullanarak uygulamalarınızı yönetmenize olanak tanır. Şablonlarınızı test, hazırlık ve üretim gibi farklı ortamları için çalışabilir. Örneğin, şablonları kullanarak, Azure Hizmetleri tek bir tıklatmayla hello depodaki tooa kümesi hello kodda dağıtan bir düğme tooa GitHub deposuna ekleyebilirsiniz.

>**Zaman toouse**: REST API'ler kullanarak program aracılığıyla yönetebilirsiniz, uygulamanız için şablon tabanlı bir dağıtım istediğinizde kullanım Resource Manager şablonları hello Azure CLI ve Azure PowerShell.

>**Başlama**: şablonları kullanmaya tooget bkz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md).

## <a name="understanding-accounts-subscriptions-and-billing"></a>Anlama hesapları, abonelikleri ve faturalama

Geliştiriciler, olarak sağ hello koda toodive ister ve çalışan bizim uygulamaların yapma ile mümkün olduğunca hızlı başlangıç tooget deneyin. Kesinlikle tooencourage istiyoruz Azure'da gibi kolayca çalışma toostart. toohelp kolay, Azure teklifleri sunun bir [ücretsiz deneme sürümü](https://azure.microsoft.com/free/). Gibi hatta sahip bir "ücretsiz deneyin" işlevsellik bazı hizmetler [Azure App Service](https://tryappservice.azure.com/), hangi çok bile oluşturduğunuz bir hesap gerektirmez. Kodlama ve dağıtma, uygulama tooAzure toodive olduğu gibi eğlenceli da önemli tootake olmasından Azure kullanıcı hesapları, abonelikleri ve faturalandırma açısından nasıl çalışır bazı zaman toounderstand.

### <a name="what-is-an-azure-account"></a>Bir Azure hesabı nedir?

toobe mümkün toocreate veya bir Azure aboneliği olan iş, bir Azure hesabınızın olması gerekir. Bir Azure hesap yalnızca bir kimlik Azure AD içinde veya Azure AD tarafından güvenilen bir dizinde bir iş veya Okul kuruluş gibi. Toosuch kuruluş ait değil, Microsoft, Azure AD tarafından güvenilen Account kullanarak bir abonelik her zaman oluşturabilirsiniz. Azure AD ile şirket içi Windows Server Active Directory tümleştirme hakkında daha fazla toolearn bkz [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](../../active-directory/active-directory-aadconnect.md).

Her Azure aboneliği bir Azure AD örneğiyle güven ilişkisine sahiptir. Bu dizin tooauthenticate güvenler bu anlamına gelir kullanıcılar, hizmetler ve cihazlar. Birden çok abonelik hello güvenebileceği aynı dizinde, ancak bir abonelik yalnızca bir dizine güvenir. toolearn daha, fazla [Azure aboneliklerinin Azure Active Directory ile ilişkili](../../active-directory/active-directory-how-subscriptions-associated-directory.md).

Ayrıca toodefining tek tek Azure hesabı kimlik olarak da bilinir *kullanıcılar*, ayrıca tanımlayabilirsiniz *grupları* Azure AD'de. Kullanıcı grubu oluşturmak en iyi yolu toomanage erişim tooresources bir abonelikte rol tabanlı erişim denetimi (RBAC) kullanmaktır. toocreate grupları nasıl görürüm toolearn [Azure Active Directory Önizleme'de bir grup oluşturmak](../../active-directory/active-directory-groups-create-azure-portal.md). Ayrıca oluşturabilir ve gruplarına göre yönetme [PowerShell kullanarak](../../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

### <a name="manage-your-subscriptions"></a>Aboneliklerinizi yönetme

Bir abonelik bağlantılı tooan Azure hesabı olan bir mantıksal Azure Hizmetleri birimidir. Her ilişkili hesap bir Abonelikteki bir rolü var. Faturalama Azure Hizmetleri için bir abonelik başına temelinde gerçekleştirilir. Merhaba kullanılabilir abonelik tekliflerini türüne göre bir listesi için bkz: [Microsoft Azure Teklif Ayrıntıları](https://azure.microsoft.com/support/legal/offer-details/).

#### <a name="administrator-roles"></a>Yönetici rolleri

Bir Azure aboneliği olan herhangi bir zamanda atayabilirsiniz birden fazla hesap Yönetici rolü vardır.

-   **Hesap Yöneticisi**: Bu rolün hello aboneliği üzerinde tam denetime sahip ve için fatura sorumludur hello hesabıdır.

-   **Hizmet Yöneticisi**: Bu rolün tüm hello hizmetleri üzerinde denetim hello abonelikte sahiptir. Varsayılan olarak, bu hello olan hesap yöneticisi hello gibi aynı hesabı.

-   **Ortak yönetici**: hello abonelik tooan Azure directory hello ilişkisini değiştiremezsiniz dışında bu rol aynı erişim hello Hizmet Yöneticisi hello sahiptir.

yönetici rolleri hakkında daha fazla toolearn bkz [nasıl tooadd ya da değişiklik Azure yönetici rolleri](../../billing/billing-add-change-azure-subscription-administrator.md#add-an-admin-for-a-subscription).

#### <a name="resource-groups"></a>Kaynak grupları

Yeni Azure hizmetleri sağlamak, belirli bir aboneliğe bunu. Kaynaklar olarak da bilinen ayrı ayrı Azure hizmetlerini bir kaynak grubu hello bağlamında oluşturulur. Kaynak grupları daha kolay toodeploy kolaylaştırır ve uygulama kaynaklarını yönetme. Bir kaynak grubu ile toowork bir birim olarak istediğiniz uygulamanız için tüm hello kaynakları içermelidir. Kaynakları kaynak grupları ve hatta toodifferent abonelikler arasında taşıyabilirsiniz. kaynakları taşıma hakkında toolearn bkz [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../../resource-group-move-resources.md).

Hello Azure kaynak Gezgini, aboneliğinizde önceden oluşturduğunuz hello kaynakları görselleştirmek için harika bir araçtır. toolearn daha, fazla [kullanım Azure kaynak Gezgini tooview ve kaynakları değiştirme](../../resource-manager-resource-explorer.md).

#### <a name="grant-access-tooresources"></a>GRANT erişim tooresources

TooAzure kaynaklara erişim izni verdiğinizde, her zaman hello kullanıcılarla o gerekli tooperform belirli bir görevi az ayrıcalığı sağlamak için bir en iyi uygulamadır.

-   **Rol tabanlı erişim denetimi (RBAC)**: içinde Azure, erişim izni verme belirtilen bir kapsamda toouser hesapları (sorumluları): Abonelik, kaynak grubu veya bireysel kaynaklar. RBAC, bir kaynak kümesi bir kaynak grubuna dağıtmak ve izinleri tooa belirli kullanıcı veya grup izni sağlar. Ayrıca, toohello hedef kaynak grubuna erişim tooonly hello kaynakları sınırlandırmak sağlar. Erişim tooa tek kaynak, bir sanal makine veya sanal ağ gibi da verebilirsiniz. toogrant erişim, rol toohello kullanıcı, Grup veya hizmet sorumlusu atayın. Çok sayıda önceden tanımlanmış roller yoktur ve özel rollerinizi de tanımlayabilirsiniz.

    >**Zaman toouse**: gerektiğinde ayrıntılı erişim yönetimini kullanıcılar ve gruplar için.

    >**Başlama**: toolearn daha, fazla [hello Azure portalına erişim yönetimi kullanmaya başlama](../../active-directory/role-based-access-control-what-is.md).

-   **Hizmet sorumlusu nesneleri**: Ayrıca tooproviding erişim toouser ilkeleri ve grupları, hello verebilirsiniz aynı erişim tooa hizmet sorumlusu.

    > **Zaman toouse**: ne zaman, program aracılığıyla Azure kaynaklarını yönetmek veya uygulamalar için erişim verme. Daha fazla bilgi için bkz: [oluşturma Active Directory supplication ve hizmet sorumlusu](../../resource-group-create-service-principal-portal.md).

#### <a name="tags"></a>Etiketler

Azure Resource Manager tooindividual kaynakları özel etiketler atamanıza olanak tanır. Faturalama veya izleme için tooorganize kaynak gerektiğinde anahtar-değer çiftleri olan etiketleri yararlı olabilir. Etiketler birden çok kaynak grubu içinde bir şekilde tootrack kaynaklar sağlar. Etiketler hello portalında, hello Azure Resource Manager şablonu veya programlı olarak hello REST API, hello Azure CLI veya PowerShell kullanarak atayabilirsiniz. Birden çok etiket tooeach kaynak atayabilirsiniz. toolearn daha, fazla [kullanarak Azure kaynaklarınızı tooorganize etiketler](../../resource-group-using-tags.md).

### <a name="billing"></a>Faturalandırma

Şirket içi toocloud barındırılan hizmetleri bilgi işlem içinde taşımak Merhaba, izleme ve hizmet kullanımı ve ilgili maliyetleri tahmin etme önemli sorunları var. Önemli toobe mümkün tooestimate olduğu aylık olarak toorun maliyeti ne yeni kaynaklar. Ayrıca hello faturalama hello geçerli harcama göre belirli bir ay boyunca nasıl göründüğünü toobe mümkün tooproject gerekir.

#### <a name="get-resource-usage-data"></a>Kaynak kullanım verilerini alma

Azure faturalama REST erişim tooresource tüketim ve Azure abonelikleri için meta veri bilgileri veren API kümesi sağlar. Özelliği toobetter hello bu faturalama API'leri verin tahmin etmek ve Azure maliyetlerini yönetme. İzleme ve saatlik artışlarda harcadığı miktarı analiz, harcama uyarılar oluşturabilir ve geçerli kullanım eğilimler temelinde gelecek fatura tahmin etmek.

>**Başlama**: hello faturalama API'ler kullanma hakkında daha fazla toolearn bkz [Azure faturalama kullanımını ve RateCard API'leri genel bakış](../../billing-usage-rate-card-overview.md).

#### <a name="predict-future-costs"></a>Gelecekteki maliyetleri tahmin etme

Önceden tooestimate maliyetleri zor olsa da, Azure sahip bir [fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) kaynakları dağıtılan hello maliyetini tahmin ederken kullanabilirsiniz. Merhaba faturalama dikey penceresinde hello portal ve geçerli tüketime dayanarak hello faturalama REST API'leri tooestimate gelecekteki maliyetleri de kullanabilirsiniz.

>**Başlama**: bkz [Azure faturalama kullanımını ve RateCard API'leri genel bakış](../../billing-usage-rate-card-overview.md).

#### <a name="set-up-billing-alerts"></a>Fatura uyarılarını ayarlama

Uygulamanızı veya Azure ile ilgili çözüm dağıtıldıktan sonra harcama hello uyarıda tanımlanan limitlerini hello yaklaşımını olduğunda e-posta Gönder uyarılar oluşturabilirsiniz.

>**Başlama**: toolearn daha, fazla [uyarılar, Microsoft Azure abonelikleri için ödeme yukarı ayarlamak](../../billing-set-up-alerts.md).
