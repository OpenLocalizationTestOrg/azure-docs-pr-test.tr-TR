---
title: "aaaAzure service fabric güvenliğine genel bakış | Microsoft Docs"
description: "Bu makalede hello Azure service fabric güvenlik genel bir bakış sağlar."
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
ms.openlocfilehash: ec5355983c5d59f4e0c3b855965f03ac47f1a4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-overview"></a>Azure Service Fabric güvenliğine genel bakış
[Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) kolay toopackage kolaylaştıran bir dağıtılmış sistemler platformudur dağıtma ve ölçeklenebilir ve güvenilir mikro hizmetler yönetme. Service Fabric geliştirmeye ve bulut uygulamalarını yönetme hello önemli sorunlarını ele alır. Geliştiriciler ve yöneticiler, karmaşık altyapı sorunlarını çözmeye çalışmak yerine görev açısından kritik, zorlu iş yüklerini uygulamaya odaklanabilir. Service Fabric, bu iş yüklerinin ölçeklenebilir, güvenilir ve yönetilebilir olmasını sağlar.

Azure Service Fabric güvenliğine genel bakış makalede alanları aşağıdaki hello üzerinde odaklanır:

-   Kümenizi güvenliğini sağlama
-   İzleme ve tanılama
-   Sertifikaları kullanılarak güvenli
-   Rol tabanlı erişim denetimi (RBAC)
-   Windows güvenliği kullanarak güvenli küme
-   Service Fabric uygulama güvenliğini yapılandırma
-   Güvenli iletişim için Azure Service Fabric güvenlik hizmetleri

## <a name="securing-your-cluster"></a>Kümenizi güvenliğini sağlama
Azure Service Fabric bir orchestrator Hizmetleri makine bir kümede, özellikle üretim iş yükleri üzerinde çalıştırılan olduğunda tooyour küme bağlanma güvenli tooprevent yetkisiz kullanıcıların kümeleri olması gerekir. Olası toocreate güvenli olmayan bir küme olmasına karşın, yönetim uç noktaları toohello gösterir böylece anonim kullanıcılar tooconnect tooit verir genel Internet.

Bu bölümde Azure veya tek başına çalışan kümeler için güvenlik senaryoları hello genel bir bakış sağlar ve bu senaryolar çeşitli kullanılan teknolojiler tooimplement hello. Merhaba küme güvenlik senaryolar şunlardır:

-   Düğümü düğümü güvenlik
-   İstemcisi düğümü güvenlik

### <a name="node-to-node-security"></a>Düğümü düğümü güvenlik
Merhaba VM'ler ya da hello kümesindeki makineleri arasındaki iletişimin güvenliğini sağlar. Bu uygulamalar ve hizmetler hello kümedeki barındırma yetkili toojoin hello küme yalnızca bilgisayarları katılabilir sağlar.

Windows üzerinde çalışan Azure veya tek başına kümeleri üzerinde çalışan kümelerle kullanabilirsiniz [sertifika güvenliği](https://msdn.microsoft.com/library/ff649801.aspx) veya [Windows Güvenliği](https://msdn.microsoft.com/library/ff649396.aspx) Windows Server makinelerini için.

**Düğümü düğümü sertifika güvenliği**

Service Fabric Küme oluşturduğunuzda, belirttiğiniz hello düğüm türü yapılandırmaları bir parçası olarak X.509 sunucu sertifikaları kullanır. Bu sertifikalar nelerdir, hızlı bir genel bakış ve [nasıl elde veya bunları oluşturmak bu makalede sağlanan](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates).

Sertifika Güvenliği hello Azure portal aracılığıyla, Azure Resource Manager şablonları veya tek başına JSON şablonunu hello küme oluşturma sırasında yapılandırılır. Birincil bir sertifika ve sertifika rollover için kullanılan isteğe bağlı ikincil bir sertifika belirtebilirsiniz. Merhaba, belirttiğiniz birincil ve ikincil sertifikaları hello yönetici istemci ve salt okunur istemci sertifikalarını belirtmek için farklı olmalıdır [istemcisi düğümü güvenlik](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security).

### <a name="client-to-node-security"></a>İstemcisi düğümü güvenlik
İstemci toonode güvenlik istemci kimlikleri kullanılarak yapılandırılır. tooestablish güven istemci ve hello küme güven hangi istemci kimlikleri hello küme tooknow yapılandırmanız gerekir. Bu iki farklı şekillerde yapılabilir:

-   Bağlanabilir hello etki alanı grubu kullanıcıları belirtin veya
-   Bağlanabilir hello etki alanı düğümü kullanıcıları belirtin.

Service Fabric bağlı tooa Service Fabric kümesi istemciler için iki farklı erişim denetim türlerini destekler:

-   Yönetici
-   Kullanıcı

Erişim denetimi Küme Yöneticisi toolimit erişim toocertain türü küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için hello hello yeteneği sağlar. Yöneticiler tam erişim toomanagement özellikleri (okuma/yazma özellikleri dahil) sahiptir. Kullanıcıların varsayılan olarak, yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve hizmetleri vardır.

**İstemci düğüm sertifika güvenliği**

İstemci düğüm sertifika güvenliği hello Azure portal, Resource Manager şablonları ya da bir yönetici istemci sertifikası ve/veya bir kullanıcı istemci sertifikası belirterek tek başına JSON şablon aracılığıyla hello küme oluşturulurken yapılandırılır. Belirttiğiniz hello yönetici istemci ve kullanıcı istemci sertifikası düğümü düğümü güvenlik için belirttiğiniz hello birincil ve ikincil sertifikaları farklı olmalıdır.

Hello Yöneticisi sertifikayı kullanarak toohello küme bağlanan istemciler tam erişim toomanagement özelliklere sahiptir. Toohello küme Hello salt okunur kullanıcı istemci sertifikası kullanarak bağlanan istemciler yalnızca okuma erişimi toomanagement özelliklere sahiptir. Bu sertifikalar hello için kullanılan diğer Word'de erişim denetimi (RBAC) rolüne taban.

Azure okumak için [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) toolearn nasıl tooconfigure sertifika kümede güvenliği.

**Azure üzerinde istemci düğümünde Azure Active Directory (AAD) güvenlik**

Azure üzerinde çalışan kümelerle toohello yönetim uç noktalarının Azure Active Directory (AAD) kullanarak erişim güvenliğini sağlayabilirsiniz. Bkz: [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) nasıl toocreate hello gerekli AAD yapılar hakkında daha fazla bilgi için nasıl toopopulate sırasında onları küme oluşturma ve nasıl tooconnect toothose daha sonra kümeleri.

AAD, bir web tabanlı oturum açma kullanıcı Arabirimi ile uygulamaları ve yerel istemci deneyimini uygulamalarla ayrılır (kiracılar da bilinir) kuruluşlar toomanage kullanıcı erişimi tooapplications, sağlar.

Service Fabric kümesi birkaç giriş noktaları tooits yönetim işlevselliği sunar dahil olmak üzere hello web tabanlı Service Fabric Explorer ve Visual Studio. Sonuç olarak, iki AAD uygulamaları toocontrol erişim toohello kümesi, bir web uygulaması ve bir yerel uygulama oluşturun.
Azure kümeler için düğümü düğümü güvenlik için AAD güvenlik tooauthenticate istemcileri ve sertifikalar kullanmanız önerilir.

Tek başına Windows sunucu kümeleri için Windows Server 2012 R2 ve Active Directory varsa Windows Güvenlik yönetilen grup hesapları (GMA) ile kullanmanız önerilir. Hala Windows güvenliği Windows hesaplarıyla kullanmayacak.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>İzleme ve tanılama Azure Service Fabric için
[İzleme ve tanılama](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) olan kritik toodeveloping, test ve uygulamaları ve Hizmetleri herhangi bir ortamın içinde dağıtma. Service Fabric çözümleri, planlama ve izleme uygulama Yardım tanılama uygulamaları emin olmak ve Hizmetleri yerel geliştirme ortamında veya üretim beklendiği gibi çalıştığını en iyi çalışır.

Güvenlik açısından, izleme ana hedefleri hello ve tanılama üzeresiniz:

-   Tooa güvenlik olayı olabilir donanım ve altyapı sorunlarını tanılamak ve algılar.
-   Gösterge tehlike (IOC) sağlayan yazılım ve uygulama sorunları algılar.
-   Kaynak anlamak tüketim toohelp önlemek yanlışlıkla hizmet reddi.

İzleme genel iş akışı hello ve tanılama üç adımdan oluşur:

-   **Olay oluşturma:** bu hem hello altyapısı (küme) ve uygulama / hizmet düzeyinde olayları (günlüklerini, izlemeleri, özel olaylar) içerir. Daha fazla bilgi edinin [altyapı düzeyi olayları](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) ve [uygulama düzeyinde olayları](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) toounderstand ne sağlanır ve nasıl tooadd daha ayrıntılı olarak izleme.
-   **Olay toplama:** oluşturulan olay toplanır ve bunlar görüntülenebilmesi toplanan toobe gerekir. Genellikle kullanmanızı öneririz [Azure tanılama](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (daha benzer tooagent tabanlı günlük toplama) veya [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (işlemdeki günlük toplama).
-   **Analiz:** olayları gereksinim toobe görselleştirilmiş ve bazı biçimi, tooallow erişilebilir çözümleme ve gerektiği gibi görünen için. Toohello çözümleme ve görselleştirme izleme ve tanılama veri geldiğinde hello pazarında mevcut birkaç harika platformları vardır. Merhaba önerdiğimiz ikisidir [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) ve [Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) son tootheir Service Fabric ile daha iyi tümleştirme.

Aynı zamanda [Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) toomonitor birçok hello Azure kaynaklarını Service Fabric kümesi oluşturulur.

Bir izleme, sistem durumu izleyebilir ve hizmetler ve rapor sistem yükü hello sistem durumu modeli hiyerarşi içinde herhangi bir şey için ayrı bir hizmettir. Bu, tek bir hizmeti hello görünümü temel alarak algılanmayacağı hataları önlemeye yardımcı olabilir. Watchdogs de (örneğin, belirli zaman aralıklarında depolama günlük dosyalarında temizleniyor) kullanıcı etkileşimi olmadan düzeltici eylemler gerçekleştiren bir iyi toohost kodu olur. Bir örnek izleme hizmeti uygulaması bulabilirsiniz [burada](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/).

## <a name="secure-using-certificates"></a>Sertifikaları kullanılarak güvenli
Sertifikaları kullanarak, onu nasıl toosecure hello iletişimine hello çeşitli, tek başına Windows küme düğümlerinin de nasıl toothis küme bağlanan tooauthenticate istemcileri X.509 sertifikaları kullanma söyler. Bu, yalnızca yetkili kullanıcılar hello küme erişebilir dağıtılan uygulamalar hello ve yönetim görevlerini gerçekleştirme sağlar. Merhaba küme oluşturulduğunda sertifika güvenliği hello kümede etkinleştirilmelidir.

### <a name="x509-certificates-and-service-fabric"></a>X.509 sertifikaları ve Service Fabric
X.509 dijital sertifikalar yaygın olarak kullanılan tooauthenticate istemcileri ve sunucuları ve tooencrypt ve iletileri dijital olarak imzala.

Merhaba aşağıdaki tabloda, Küme kurulumu gerekir hello sertifikaları listelenmektedir:

|Sertifika bilgilerini ayarlama |Açıklama|
|-------------------------------|-----------|
|ClusterCertificate|    Bu sertifika bir kümede hello düğümler arasında gerekli toosecure hello iletişim yok. İki farklı sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz.|
|ServerCertificate| Tooconnect toothis küme çalıştığında bu sertifikayı toohello istemci sunulur. İki farklı sunucu sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz.|
|ClientCertificateThumbprints|  Kimliği doğrulanmış hello istemcilerde tooinstall istediğiniz sertifikaları kümesidir.|
|ClientCertificateCommonNames|  Merhaba hello CertificateCommonName için hello ilk istemci sertifikasının ortak ad olarak ayarlayın. Merhaba CertificateIssuerThumbprint hello veren bu sertifikanın parmak izi hello ' dir.|
|ReverseProxyCertificate|   Bu, olabilir, isteğe bağlı bir sertifikadır toosecure isteyip istemediğinizi belirtilen, [Ters Proxy](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).|

Sertifikalar, güvenliğini sağlama konusunda daha fazla bilgi için [burayı](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security).

## <a name="role-based-access-control-rbac"></a>Rol tabanlı erişim denetimi (RBAC)
Erişim denetimi hello Küme Yöneticisi toolimit erişim toocertain küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için sağlar. İki farklı erişim denetimi türleri tooa küme bağlanan istemciler için desteklenir: Yönetici rolü ve kullanıcı rolü.

Yöneticiler tam erişim toomanagement özellikleri (okuma/yazma özellikleri dahil) sahiptir. Kullanıcıların varsayılan olarak, yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve hizmetleri vardır.

Merhaba yönetici ve kullanıcı istemci rolleri hello küme oluşturma sırasında ayrı kimlikleri (Sertifikalar, AAD vb.) sağlayarak her biri için belirttiğiniz. Merhaba varsayılan erişim denetimi ayarlarını ve nasıl toochange hello varsayılan ayarları hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

## <a name="secure-standalone-cluster-using-windows-security"></a>Windows güvenliği kullanarak tek başına küme güvenli
erişim tooa Service Fabric kümesi tooprevent yetkisiz, hello küme güvenlik altına almanız gerekir. Merhaba küme üretim iş yükleri çalıştığında güvenlik özellikle önemlidir. Bunu nasıl Windows güvenliği kullanarak tooconfigure düğümü düğümü ve istemci düğüm güvenlik hello ClusterConfig.JSON dosya açıklar.

**GMSA kullanarak Windows güvenliği yapılandırma**

Düğüm toonode güvenlik ayarlayarak yapılandırılmış [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) toorun gMSA altında service fabric gerektiği zaman. Sipariş toobuild güven ilişkilerini düğümler arasında bunlar birbirinden haberdar olmanız gerekir.

İstemci toonode güvenlik ClientIdentities kullanılarak yapılandırılır. Bir istemci ve hello kümesi arasında sipariş tooestablish güven içinde güven hangi istemci kimlikleri hello küme tooknow yapılandırmanız gerekir.

**Makine grubu kullanarak Windows güvenliği yapılandırma**

Düğüm toonode güvenlik toouse bir Active Directory etki alanı içindeki bir makine grubun istiyorsanız ClusterIdentity kullanarak ayarı tarafından yapılandırılır. Daha fazla bilgi için bkz: [Active Directory'de bir makine grubu oluştur](https://msdn.microsoft.com/library/aa545347).

İstemcisi düğümü güvenlik, ClientIdentities kullanılarak yapılandırılır. tooestablish güven bir istemci ve hello kümesi arasında küme hello kimlikleri güvenebileceği hello küme tooknow hello istemci yapılandırmanız gerekir. İki farklı yolla güven kurabilir:

-   Bağlanabilir hello etki alanı grubu kullanıcıları belirtin.
-   Bağlanabilir hello etki alanı düğümü kullanıcıları belirtin.

## <a name="configure-application-security-in-service-fabric"></a>Service Fabric uygulama güvenliğini yapılandırma
### <a name="managing-secrets-in-service-fabric-applications"></a>Service Fabric uygulamaları parolaları yönetme
Bu yöntem, Service Fabric uygulaması parolalarında yönetmede yardımcı olur. Gizli depolama bağlantı dizeleri, parolalar veya düz metin olarak işleneceğini olmayan diğer değerleri gibi herhangi bir önemli bilgi olabilir.

Bu yaklaşımı kullanır [Azure anahtar kasası](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) toomanage anahtarları ve gizli anahtarları. Ancak, gizli bir uygulamada herhangi bir yerde barındırılan bulut platformu belirsiz tooallow uygulamaları dağıtılan toobe tooa küme kullanmaktır. Bu akış dört ana adım vardır:

-   Veri şifreleme sertifikası alın.
-   Kümenizdeki Hello sertifikası yükleyin.
-   Bir uygulamayı hello sertifikayla dağıtırken gizli değerleri şifrelemek ve bir hizmetin Settings.xml yapılandırma dosyasına Ekle.
-   İle şifre çözme tarafından şifrelenmiş okuma değerleri Settings.xml dışında aynı şifreleme sertifikası hello.

>[!Note]
>Daha fazla bilgi edinmek [Service Fabric uygulamaları parolalarında yönetme](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="configure-security-policies-for-your-application"></a>Uygulamanıza yönelik güvenlik ilkeleri yapılandırma
Azure Service Fabric güvenlik kullanarak hello kümedeki farklı kullanıcı hesabı altında çalışan güvenli uygulamalar yardımcı olabilir. Service Fabric güvenlik ayrıca uygulamalar tarafından hello kullanıcı hesapları altında--dağıtımının hello zamanında örneğin kullanılan güvenli hello kaynakları, dizinleri ve dosyaları sertifikaları yardımcı olur. Bu çalışan uygulamaları bile paylaşılan bir barındırılan ortamda, diğerinden daha güvenli hale getirir.
Merhaba adımları içerir:

-   Bir hizmet Kurulum giriş noktası için Hello ilkesi yapılandırın.
-   PowerShell komutlarını bir Kurulum giriş noktasından başlatın.
-   Yerel hata ayıklama için konsolu yeniden yönlendirmesini kullanın.
-   Hizmet kodu paketleri için bir ilke yapılandırın.
-   HTTP ve HTTPS uç noktaları için bir güvenlik erişim ilkesi atayın.

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Güvenli iletişim için Azure Service Fabric güvenlik hizmetleri
Güvenlik iletişim hello en önemli yönlerinden birisidir. Merhaba Reliable Services uygulama çerçevesi birkaç önceden oluşturulmuş iletişimi yığınları ve kullanılan tooimprove güvenlik olabilir araçlar sağlar.

-   [Hizmet remoting kullanırken bir hizmeti güvenli hale](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication).
-   [Bir WCF tabanlı iletişim yığını kullanırken bir hizmeti güvenli hale](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack).

## <a name="next-steps"></a>Sonraki adımlar
- Kavramsal küme güvenliği hakkında bilgi için [Resource Manager şablonu kullanarak Azure'da bir küme oluşturun](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) ve [Azure portal](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal).
- Daha fazla bilgi edinmek için bkz: [Service Fabric kümesi güvenlik](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security).
