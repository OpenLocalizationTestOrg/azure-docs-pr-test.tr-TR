---
title: "Azure service fabric güvenliğine genel bakış | Microsoft Docs"
description: "Bu makalede Azure service fabric güvenliğine genel bakış sağlar."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 4cbd2791649c6d2dd005521cedb44c17aa874073
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-service-fabric-security-overview"></a>Azure Service Fabric güvenliğine genel bakış
[Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) paketini, dağıtmak ve ölçeklenebilir ve güvenilir mikro hizmetleri yönetmek kolaylaştıran bir dağıtılmış sistemler platformudur. Service Fabric geliştirmeye ve bulut uygulamalarını yönetme önemli sorunları giderir. Geliştiriciler ve yöneticiler, karmaşık altyapı sorunlarını çözmeye çalışmak yerine görev açısından kritik, zorlu iş yüklerini uygulamaya odaklanabilir. Service Fabric, bu iş yüklerinin ölçeklenebilir, güvenilir ve yönetilebilir olmasını sağlar.

Azure Service Fabric güvenliğine genel bakış makalede aşağıdaki alanlar üzerinde odaklanır:

-   Kümenizi güvenliğini sağlama
-   İzleme ve tanılama
-   Sertifikaları kullanılarak güvenli
-   Rol tabanlı erişim denetimi (RBAC)
-   Windows güvenliği kullanarak güvenli küme
-   Service Fabric uygulama güvenliğini yapılandırma
-   Güvenli iletişim için Azure Service Fabric güvenlik hizmetleri

## <a name="securing-your-cluster"></a>Kümenizi güvenliğini sağlama
Azure Service Fabric bir orchestrator Hizmetleri makine bir kümede, yetkisiz kullanıcıların özellikle üretim iş yükleri üzerinde çalıştırılan sahip olduğunda, kümeniz için bağlanmasını önlemek için kümeleri güvenli hale getirilmelidir. Güvenli olmayan bir küme oluşturmak mümkün olsa da, genel internet yönetim uç noktalarını kullanıma sunar, bunu yapmak bu nedenle, anonim bağlanmasına olanak sağlar.

Bu bölümde, Azure veya tek başına ve bu senaryolar uygulamak için kullanılan teknolojiler çalıştıran kümeler için güvenlik senaryoları genel bir bakış sağlar. Küme güvenlik senaryolar şunlardır:

-   Düğümü düğümü güvenlik
-   İstemcisi düğümü güvenlik

### <a name="node-to-node-security"></a>Düğümü düğümü güvenlik
VM'ler veya kümede makineler arasındaki iletişimin güvenliğini sağlar. Bu, kümeye katılmak için yetkili bilgisayarları uygulamaları ve Hizmetleri kümedeki barındırma katılabilir sağlar.

Windows üzerinde çalışan Azure veya tek başına kümeleri üzerinde çalışan kümelerle kullanabilirsiniz [sertifika güvenliği](https://msdn.microsoft.com/library/ff649801.aspx) veya [Windows Güvenliği](https://msdn.microsoft.com/library/ff649396.aspx) Windows Server makinelerini için.

**Düğümü düğümü sertifika güvenliği**

Service Fabric Küme oluşturduğunuzda, belirttiğiniz düğüm türü yapılandırmaları bir parçası olarak X.509 sunucu sertifikaları kullanır. Bu sertifikalar nelerdir, hızlı bir genel bakış ve [nasıl elde veya bunları oluşturmak bu makalede sağlanan](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates).

Sertifika Güvenliği Azure portalı, Azure Resource Manager şablonları veya tek başına JSON şablon ile küme oluşturma sırasında yapılandırılır. Birincil bir sertifika ve sertifika rollover için kullanılan isteğe bağlı ikincil bir sertifika belirtebilirsiniz. Belirttiğiniz birincil ve ikincil sertifikaları yönetici istemci ve salt okunur istemci sertifikalarını belirtmek için farklı [istemcisi düğümü güvenlik](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security).

### <a name="client-to-node-security"></a>İstemcisi düğümü güvenlik
Düğüm güvenlik istemciye istemci kimlikleri kullanılarak yapılandırılır. Bir istemci ve küme arasında güven oluşturmak için hangi istemci, güvenilir kimlikleri bilmeniz küme yapılandırmanız gerekir. Bu iki farklı şekillerde yapılabilir:

-   Bağlanabilmesi için etki alanı grubu kullanıcıları belirtin veya
-   Bağlanabilmesi için etki alanı düğümü kullanıcıları belirtin.

Service Fabric Service Fabric kümeye bağlı istemciler için iki farklı erişim denetim türlerini destekler:

-   Yönetici
-   Kullanıcı

Erişim denetimi, belirli türde bir küme işlemleri farklı küme daha güvenli hale getirme kullanıcı grupları için erişimi sınırlamak Küme Yöneticisi yeteneği sağlar. Yöneticiler için yönetim özellikleri (okuma/yazma özellikleri dahil) tam erişime sahip. Kullanıcıların varsayılan olarak, yalnızca yönetim özellikleri (örneğin, sorgu özellikleri) okuma erişimi ve uygulamaları ve Hizmetleri çözümleme olanağı vardır.

**İstemci düğüm sertifika güvenliği**

İstemci düğüm sertifika güvenliği Resource Manager şablonları ya da bir yönetici istemci sertifikası ve/veya bir kullanıcı istemci sertifikası belirterek tek başına JSON şablon Azure Portalı aracılığıyla ya da küme oluşturulurken yapılandırılır. Belirttiğiniz yönetici istemci ve kullanıcı istemci sertifikası düğümü düğümü güvenlik için belirttiğiniz birincil ve ikincil sertifikaları farklı olmalıdır.

Yönetim sertifikası kullanılarak kümesine bağlanan istemciler, yönetim özellikleri için tam erişime sahip. Salt okunur kullanıcı istemci sertifikası kullanılarak kümesine bağlanan istemciler yönetim özellikleri yalnızca okuma erişimi var. Bu sertifikalar rolü için kullanılan diğer Word'de erişim denetimi (RBAC) alır.

Azure okumak için [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) bir kümede sertifika güvenliği yapılandırma hakkında bilgi edinmek için.

**Azure üzerinde istemci düğümünde Azure Active Directory (AAD) güvenlik**

Azure üzerinde çalışan kümelerle de Azure Active Directory (AAD) kullanan yönetim uç noktalarına erişime güvenliğini sağlayabilirsiniz. Bkz: [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) gerekli AAD yapıları oluşturma, küme oluşturma sırasında doldurmak nasıl ve daha sonra bu kümeye bağlanma hakkında bilgi.

AAD (kiracılar da bilinir), kuruluşların uygulamaları bir web tabanlı oturum açma kullanıcı Arabirimi ile ayrılır uygulamaları ve yerel istemci bir deneyim uygulamaları için kullanıcı erişimini yönetmenizi sağlar.

Service Fabric kümesi yönetim işlevselliği, web tabanlı Service Fabric Explorer ve Visual Studio gibi çeşitli giriş noktalarını sunar. Sonuç olarak, Küme erişimi denetlemek için iki AAD uygulama, bir web uygulaması ve bir yerel uygulama oluşturun.
Azure kümeler için istemciler ve sertifikaları düğümü düğümü güvenlik kimlik doğrulaması için AAD güvenlik kullanmanız önerilir.

Tek başına Windows sunucu kümeleri için Windows Server 2012 R2 ve Active Directory varsa Windows Güvenlik yönetilen grup hesapları (GMA) ile kullanmanız önerilir. Hala Windows güvenliği Windows hesaplarıyla kullanmayacak.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>İzleme ve tanılama Azure Service Fabric için
[İzleme ve tanılama](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) geliştirme, test ve uygulamaları ve Hizmetleri herhangi bir ortamda dağıtmak için kritik öneme sahiptir. Service Fabric çözümleri, planlama ve izleme uygulama Yardım tanılama uygulamaları emin olmak ve Hizmetleri yerel geliştirme ortamında veya üretim beklendiği gibi çalıştığını en iyi çalışır.

Güvenlik açısından bakıldığında, için izleme ve tanılama başlıca amaçları şunlardır:

-   Güvenlik olayı nedeniyle olabilir donanım ve altyapı sorunlarını tanılamak ve algılar.
-   Gösterge tehlike (IOC) sağlayan yazılım ve uygulama sorunları algılar.
-   Yanlışlıkla hizmet reddi önlemeye yardımcı olmak için kaynak tüketimini anlayın.

Genel iş akışını izleme ve tanılama ve üç adımdan oluşur:

-   **Olay oluşturma:** bu hem altyapısı (küme) ve uygulama / hizmet düzeyinde olayları (günlüklerini, izlemeleri, özel olaylar) içerir. Daha fazla bilgi edinin [altyapı düzeyi olayları](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) ve [uygulama düzeyinde olayları](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) nasıl sağlandığını ve daha fazla izleme eklemek nasıl anlamak için.
-   **Olay toplama:** oluşturulan olaylar gereken toplanacağı ve bunların görüntülenebilmesi bir araya getirilir. Genellikle kullanmanızı öneririz [Azure tanılama](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (daha benzer tabanlı aracı günlük toplama) veya [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (işlemdeki günlük toplama).
-   **Analiz:** olayları görselleştirilmiş ve analiz için izin vermek ve gerektiği gibi görüntülemek için bazı biçiminde erişilebilir olması gerekir. Çözümleme ve görselleştirme izleme ve tanılama veri geldiğinde pazarında mevcut birkaç harika platformları vardır. Öneririz iki olan [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) ve [Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) nedeniyle Service Fabric ile bunların daha iyi tümleştirme.

Aynı zamanda [Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) Service Fabric kümesi yerleşik Azure kaynaklarını çoğunu izlemek için.

Bir izleme, sistem durumu izleyebilir ve hizmetler ve rapor sistem yükü sistem durumu modeli hiyerarşi içinde herhangi bir şey için ayrı bir hizmettir. Bu, tek bir hizmeti görünümü temel alarak algılanmayacağı hataları önlemeye yardımcı olabilir. Watchdogs de iyi (örneğin, belirli zaman aralıklarında depolama günlük dosyalarında temizleniyor) kullanıcı etkileşimi olmadan düzeltici eylemleri gerçekleştirir konak koduna yerlerdir. Bir örnek izleme hizmeti uygulaması bulabilirsiniz [burada](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/).

## <a name="secure-using-certificates"></a>Sertifikaları kullanılarak güvenli
Bu kümeye bağlanan istemciler X.509 kullanarak kimlik doğrulaması için sertifikaları nasıl sertifikaları kullanarak, bu, tek başına Windows kümeniz çeşitli düğümleri arasındaki iletişimin güvenliğini sağlamak de anlatır. Bu, yalnızca yetkili kullanıcılar kümeye dağıtılan uygulamalar erişmek ve yönetim görevlerini gerçekleştirme sağlar. Küme oluşturulduğunda sertifika güvenliği kümede etkinleştirilmelidir.

### <a name="x509-certificates-and-service-fabric"></a>X.509 sertifikaları ve Service Fabric
X.509 dijital sertifikalar, istemciler ve sunucular kimlik doğrulaması ve şifreleme ve iletileri dijital olarak imzala için yaygın olarak kullanılır.

Aşağıdaki tabloda, Küme kurulumu gerekir sertifikaları listelenmektedir:

|Sertifika bilgilerini ayarlama |Açıklama|
|-------------------------------|-----------|
|ClusterCertificate|    Bu sertifika, bir küme düğümlerinde arasındaki iletişimin güvenliğini sağlamak için gereklidir. İki farklı sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz.|
|ServerCertificate| Bu kümeye bağlanmaya çalıştığında bu sertifikayı istemciye sunulur. İki farklı sunucu sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz.|
|ClientCertificateThumbprints|  Kimliği doğrulanmış istemcilerde yüklemek istediğiniz sertifika kümesidir.|
|ClientCertificateCommonNames|  İlk istemci sertifikasının ortak adı için CertificateCommonName ayarlayın. Bu sertifika verenin parmak izini CertificateIssuerThumbprint olur.|
|ReverseProxyCertificate|   Bu, olabilir, isteğe bağlı bir sertifikadır güvenli isteyip istemediğinizi belirtilen, [Ters Proxy](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).|

Sertifikalar, güvenliğini sağlama konusunda daha fazla bilgi için [burayı](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security).

## <a name="role-based-access-control-rbac"></a>Rol tabanlı erişim denetimi (RBAC)
Erişim denetimi, belirli küme işlemleri farklı küme daha güvenli hale getirme kullanıcı grupları için erişimi sınırlamak Küme Yöneticisi sağlar. Bir kümeye bağlanan istemciler için desteklenen iki farklı erişim denetimi türleri: Yönetici rolü ve kullanıcı rolü.

Yöneticiler için yönetim özellikleri (okuma/yazma özellikleri dahil) tam erişime sahip. Kullanıcıların varsayılan olarak, yalnızca yönetim özellikleri (örneğin, sorgu özellikleri) okuma erişimi ve uygulamaları ve Hizmetleri çözümleme olanağı vardır.

Yönetici ve kullanıcı istemci rolleri küme oluşturma sırasında ayrı kimlikleri (Sertifikalar, AAD vb.) sağlayarak her biri için belirtin. Varsayılan erişim denetimi ayarlarını ve varsayılan ayarlarının nasıl değiştirileceği hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

## <a name="secure-standalone-cluster-using-windows-security"></a>Windows güvenliği kullanarak tek başına küme güvenli
Bir Service Fabric kümesi yetkisiz erişimi önlemek için küme güvenlik altına almanız gerekir. Küme üretim iş yükleri çalıştığında güvenlik özellikle önemlidir. Düğüm düğümü ve istemci düğümü güvenliğinin ClusterConfig.JSON dosyasında Windows güvenliği kullanarak nasıl yapılandırılacağı açıklanmaktadır.

**GMSA kullanarak Windows güvenliği yapılandırma**

Düğüm güvenlik düğüme ayarlayarak yapılandırılmış [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) service fabric gerektiği zaman gMSA altında çalıştırmak. Düğümler arasındaki güven ilişkileri oluşturmak için bunlar birbirinden haberdar olmanız gerekir.

Düğüm güvenlik istemciye ClientIdentities kullanılarak yapılandırılır. Bir istemci ve küme arasında güven sağlamak için hangi istemci, güvenilir kimlikleri bilmeniz küme yapılandırmanız gerekir.

**Makine grubu kullanarak Windows güvenliği yapılandırma**

Düğüm güvenlik düğüme, bir Active Directory etki alanı içinde bir makine grubu kullanmak istiyorsanız, ClusterIdentity kullanarak ayarı tarafından yapılandırılır. Daha fazla bilgi için bkz: [Active Directory'de bir makine grubu oluştur](https://msdn.microsoft.com/library/aa545347).

İstemcisi düğümü güvenlik, ClientIdentities kullanılarak yapılandırılır. Bir istemci ve küme arasında güven sağlamak için kümenin küme güvenebileceği kimlikleri istemci bilmeniz için yapılandırmanız gerekir. İki farklı yolla güven kurabilir:

-   Bağlanabilmesi için etki alanı grubu kullanıcıları belirtin.
-   Bağlanabilmesi için etki alanı düğümü kullanıcıları belirtin.

## <a name="configure-application-security-in-service-fabric"></a>Service Fabric uygulama güvenliğini yapılandırma
### <a name="managing-secrets-in-service-fabric-applications"></a>Service Fabric uygulamaları parolaları yönetme
Bu yöntem, Service Fabric uygulaması parolalarında yönetmede yardımcı olur. Gizli depolama bağlantı dizeleri, parolalar veya düz metin olarak işleneceğini olmayan diğer değerleri gibi herhangi bir önemli bilgi olabilir.

Bu yaklaşımı kullanır [Azure anahtar kasası](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) anahtarları ve gizli anahtarları yönetmek için. Ancak, gizli bir uygulamada bulut platformu herhangi bir yerde barındırılan bir kümeye dağıtılacak uygulamalar izin vermek için belirsiz kullanmaktır. Bu akış dört ana adım vardır:

-   Veri şifreleme sertifikası alın.
-   Sertifikayı kümenizdeki yükleyin.
-   Sertifikayla ilgili bir uygulama dağıtırken gizli değerleri şifreler ve bir hizmetin Settings.xml yapılandırma dosyasına Ekle.
-   Settings.xml dışında şifrelenmiş değerler ile aynı şifreleme sertifikası şifresini çözerek okuyun.

>[!Note]
>Daha fazla bilgi edinmek [Service Fabric uygulamaları parolalarında yönetme](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="configure-security-policies-for-your-application"></a>Uygulamanıza yönelik güvenlik ilkeleri yapılandırma
Azure Service Fabric güvenlik kullanarak, kümedeki farklı kullanıcı hesabı altında çalışan güvenli uygulamalar yardımcı olabilir. Service Fabric güvenlik aynı zamanda, uygulamalar tarafından kullanıcı hesapları altında--dağıtım zamanında örneğin kullanılan kaynaklar, dosyaları, dizinleri ve sertifikaları sağlanmasına yardımcı olur. Bu çalışan uygulamaları bile paylaşılan bir barındırılan ortamda, diğerinden daha güvenli hale getirir.
Adımları içerir:

-   Bir hizmet Kurulum giriş noktası için ilkesini yapılandırın.
-   PowerShell komutlarını bir Kurulum giriş noktasından başlatın.
-   Yerel hata ayıklama için konsolu yeniden yönlendirmesini kullanın.
-   Hizmet kodu paketleri için bir ilke yapılandırın.
-   HTTP ve HTTPS uç noktaları için bir güvenlik erişim ilkesi atayın.

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Güvenli iletişim için Azure Service Fabric güvenlik hizmetleri
Güvenlik iletişim en önemli yönlerinden birisidir. Güvenilir hizmetler uygulama çerçevesi birkaç önceden oluşturulmuş iletişimi yığınları ve güvenliği geliştirmek için kullanılan araçlar sağlar.

-   [Hizmet remoting kullanırken bir hizmeti güvenli hale](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication).
-   [Bir WCF tabanlı iletişim yığını kullanırken bir hizmeti güvenli hale](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack).

## <a name="next-steps"></a>Sonraki adımlar
- Kavramsal küme güvenliği hakkında bilgi için [Resource Manager şablonu kullanarak Azure'da bir küme oluşturun](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) ve [Azure portal](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal).
- Daha fazla bilgi edinmek için bkz: [Service Fabric kümesi güvenlik](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security).
