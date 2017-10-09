---
title: "Service Fabric kümesi aaaSecure | Microsoft Docs"
description: "Merhaba güvenlik senaryoları için Service Fabric kümesi ve hello kullanılan farklı teknolojiler tooimplement bu senaryoları açıklanmıştır."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Service Fabric kümesi güvenlik senaryoları
Service Fabric kümesi sahip olduğunuz bir kaynaktır. Kümeleri özellikle üretim iş yükleri üzerinde çalıştırılan olduğunda tooyour küme bağlanma güvenli tooprevent yetkisiz kullanıcıların olması gerekir. Olası toocreate güvenli olmayan bir küme olmasına karşın, yönetim uç noktaları toohello gösterir böylece anonim kullanıcılar tooconnect tooit verir genel Internet. 

Bu makale, Azure veya tek başına çalışan kümeler için güvenlik senaryoları hello genel bir bakış sağlar ve bu senaryolar çeşitli kullanılan teknolojiler tooimplement hello. Merhaba küme güvenlik senaryolar şunlardır:

* Düğümü düğümü güvenlik
* İstemcisi düğümü güvenlik
* Rol tabanlı erişim denetimi (RBAC)

## <a name="node-to-node-security"></a>Düğümü düğümü güvenlik
Merhaba VM'ler ya da hello kümesindeki makineleri arasındaki iletişimin güvenliğini sağlar. Bu uygulamalar ve hizmetler hello kümedeki barındırma yetkili toojoin hello küme yalnızca bilgisayarları katılabilir sağlar.

![Düğümü düğümü iletişim diyagramı][Node-to-Node]

Windows üzerinde çalışan Azure veya tek başına kümeleri üzerinde çalışan kümelerle kullanabilirsiniz [sertifika güvenliği](https://msdn.microsoft.com/library/ff649801.aspx) veya [Windows Güvenliği](https://msdn.microsoft.com/library/ff649396.aspx) Windows Server makinelerini için.

### <a name="node-to-node-certificate-security"></a>Düğümü düğümü sertifika güvenliği
Service Fabric Küme oluşturduğunuzda, belirttiğiniz hello düğüm türü yapılandırmaları bir parçası olarak X.509 sunucu sertifikaları kullanır. Bu sertifikalar nedir ve nasıl elde veya bunları oluşturmanız hızlı bir genel bakış hello bu makalenin sonundaki sağlanır.

Sertifika Güvenliği hello Azure portal aracılığıyla, Azure Resource Manager şablonları veya tek başına JSON şablonunu hello küme oluşturma sırasında yapılandırılır. Birincil bir sertifika ve sertifika rollover için kullanılan isteğe bağlı ikincil bir sertifika belirtebilirsiniz. Merhaba, belirttiğiniz birincil ve ikincil sertifikaları hello yönetici istemci ve salt okunur istemci sertifikalarını belirtmek için farklı olmalıdır [istemcisi düğümü güvenlik](#client-to-node-security).

Azure okumak için [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](service-fabric-cluster-creation-via-arm.md) toolearn nasıl tooconfigure sertifika kümede güvenliği.

Windows Server için tek başına okuma [X.509 sertifikaları kullanarak Windows'u bir tek başına kümede güvenli](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>Düğümü düğümü windows güvenliği
Windows Server için tek başına okuma [Windows güvenliği kullanarak Windows'u bir tek başına kümede güvenli](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>İstemcisi düğümü güvenlik
İstemcilerin kimliğini doğrular ve bir istemci ve hello kümedeki tek düğümler arasındaki iletişimin güvenliğini sağlar. Bu tür güvenlik kimliğini doğrular ve yalnızca yetkili kullanıcılar hello küme ve hello kümede dağıtılan hello uygulamalar erişebilmesini sağlar istemci iletişimleri güvenliğini sağlar. İstemciler, Windows güvenlik kimlik bilgilerini veya sertifika güvenlik kimlik bilgilerini benzersiz şekilde tanımlanır.

![İstemci düğüme iletişim diyagramı][Client-to-Node]

Windows üzerinde çalışan Azure veya tek başına kümeleri üzerinde çalışan kümelerle kullanabilirsiniz [sertifika güvenliği](https://msdn.microsoft.com/library/ff649801.aspx) veya [Windows Güvenliği](https://msdn.microsoft.com/library/ff649396.aspx).

### <a name="client-to-node-certificate-security"></a>İstemci düğüm sertifika güvenliği
 İstemci düğüm sertifika güvenliği hello küme hello Azure portal aracılığıyla, Resource Manager şablonları ya da tek başına JSON şablonunu yönetici istemci sertifikası ve/veya bir kullanıcı istemci sertifikası belirterek oluşturulurken yapılandırılır.  Merhaba, belirttiğiniz yönetici istemci ve kullanıcı istemci sertifikası hello birincil farklı olmalıdır ve ikincil sertifikaları için belirttiğiniz [düğümü düğümü güvenlik](#node-to-node-security) açısından en iyisi. Varsayılan olarak, istemci yönetim sertifikaları listesinde izin toohello hello küme düğümü, düğümü güvenlik sertifikalarında eklenir.

Hello Yöneticisi sertifikayı kullanarak toohello küme bağlanan istemciler tam erişim toomanagement özelliklere sahiptir.  Toohello küme Hello salt okunur kullanıcı istemci sertifikası kullanarak bağlanan istemciler yalnızca okuma erişimi toomanagement özelliklere sahiptir. Diğer bir deyişle bu sertifikalar, bu makalenin sonraki bölümlerinde açıklanan hello rol tabanları erişim denetimi (RBAC) için kullanılır.

Azure okumak için [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](service-fabric-cluster-creation-via-arm.md) toolearn nasıl tooconfigure sertifika kümede güvenliği.

Windows Server için tek başına okuma [X.509 sertifikaları kullanarak Windows'u bir tek başına kümede güvenli](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Azure üzerinde istemci düğümünde Azure Active Directory (AAD) güvenlik
Azure üzerinde çalışan kümelerle toohello yönetim uç noktalarının Azure Active Directory (AAD) kullanarak erişim güvenliğini sağlayabilirsiniz. Bkz: [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](service-fabric-cluster-creation-via-arm.md) nasıl toocreate hello gerekli AAD yapılar hakkında daha fazla bilgi için nasıl toopopulate sırasında onları küme oluşturma ve nasıl tooconnect toothose daha sonra kümeleri.

## <a name="security-recommendations"></a>Güvenlik önerileri
Azure kümeler için düğümü düğümü güvenlik için AAD güvenlik tooauthenticate istemcileri ve sertifikalar kullanmanız önerilir.

Windows Server 2012 R2 ve Active Directory varsa, tek başına Windows Server için Windows Güvenlik grubu ile kullanmanız önerilir kümeleri (GMA) yönetilen hesapları. Hala Windows güvenliği Windows hesaplarıyla kullanmayacak.

## <a name="role-based-access-control-rbac"></a>Rol tabanlı erişim denetimi (RBAC)
Erişim denetimi hello Küme Yöneticisi toolimit erişim toocertain küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için sağlar. İki farklı erişim denetimi türleri tooa küme bağlanan istemciler için desteklenir: Yönetici rolü ve kullanıcı rolü.

Yöneticiler tam erişim toomanagement özellikleri (okuma/yazma özellikleri dahil) sahiptir. Kullanıcıların varsayılan olarak, yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve hizmetleri vardır.

Merhaba yönetici ve kullanıcı istemci rolleri hello küme oluşturma sırasında ayrı kimlikleri (Sertifikalar, AAD vb.) sağlayarak her biri için belirttiğiniz. Merhaba varsayılan erişim denetimi ayarlarını ve nasıl toochange hello varsayılan ayarları hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](service-fabric-cluster-security-roles.md).

## <a name="x509-certificates-and-service-fabric"></a>X.509 sertifikaları ve Service Fabric
X.509 dijital sertifikalar yaygın olarak kullanılan tooauthenticate istemcileri ve sunucuları ve tooencrypt ve iletileri dijital olarak imzala. Bu sertifikalar hakkında daha fazla ayrıntı için çok Git[sertifikalarla çalışma](http://msdn.microsoft.com/library/ms731899.aspx).

Bazı önemli noktalar tooconsider:

* Üretim iş yükleri çalıştıran kümelerde kullanılan sertifikaları doğru yapılandırılmış bir Windows Server sertifika hizmetini kullanarak oluşturulmamalı veya bir onaylanan alınan [sertifika yetkilisi (CA)](https://en.wikipedia.org/wiki/Certificate_authority).
* MakeCert.exe gibi araçları ile oluşturulmuş üretim sertifikaları test veya hiçbir zaman hiçbir geçici kullanın.
* Kendinden imzalı bir sertifika kullanabilirsiniz, ancak yalnızca test kümeleri için alan ve üretim yapmalısınız.

### <a name="server-x509-certificates"></a>X.509 sertifikaları
Sunucu sertifikalarını bir sunucu (düğüm) tooclients kimlik doğrulaması ya da bir sunucu (düğüm) tooa sunucu (düğüm) kimlik doğrulaması hello birincil görev vardır. Bir istemci veya düğüm bir düğüm doğruladığında hello ilk denetimleri toocheck hello hello konu alanında hello ortak adı değerini biridir. Bu ortak adı veya hello sertifikalar konu diğer adları biri izin verilen Ortak adların hello listesinde mevcut olması gerekir.

Merhaba aşağıdaki nasıl toogenerate konu diğer adlarını (SAN) ile sertifikaları makalede: [nasıl tooadd bir konu diğer adı tooa güvenli LDAP sertifika](http://support.microsoft.com/kb/931351).

Her bir başlatma tooindicate hello değer türü ile önek, Hello konu alanı çeşitli değerler içerebilir. En yaygın olarak, hello başlatma "CN =" ortak adıdır; Örneğin, "CN = www.contoso.com". Merhaba konu alan toobe için boş da mümkündür. Merhaba isteğe bağlı konu alternatif adı alanında doldurulursa, hello hello sertifikanın ortak adı ve konu alternatif adı her bir giriş içermelidir. Bu DNS adı değerler girilir.

Merhaba sertifikanın hello Hedeflenen amaçlar alanının Hello değeri, "Sunucu kimlik doğrulaması" veya "İstemci kimlik doğrulaması" gibi uygun bir değer içermesi gerekir.

### <a name="client-x509-certificates"></a>İstemci X.509 sertifikaları
İstemci sertifikaları genellikle bir üçüncü taraf sertifika yetkilisi tarafından verilen değil. Bunun yerine, hello hello geçerli kullanıcı konumu kişisel deposunda genellikle istemci sertifikalarını yok "İstemci kimlik doğrulaması" amacı olan bir kök yetkilisi tarafından yerleştirilen içerir. Karşılıklı kimlik doğrulaması gerekli olduğunda hello istemci bu tür bir sertifika kullanabilirsiniz.

> [!NOTE]
> Service Fabric kümesi üzerindeki tüm yönetim işlemlerinin sunucu sertifikaları gerektirir. İstemci sertifikalarını yönetimi için kullanılamaz.
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a>Sonraki adımlar
Bu makalede küme güvenliği hakkında kavramsal bilgiler verilmektedir. Ardından,


1.  [Resource Manager şablonu kullanarak Azure'da bir küme oluşturun](service-fabric-cluster-creation-via-arm.md) 
2.  [Azure portal](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
