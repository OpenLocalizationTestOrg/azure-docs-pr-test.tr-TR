---
title: "Service Fabric kümesi güvenli | Microsoft Docs"
description: "Service Fabric kümesi ve bu senaryolar uygulamak için kullanılan farklı teknolojileri için güvenlik senaryoları açıklanmıştır."
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
ms.openlocfilehash: 5afbe575a8affc37b8f902c0988585a83921e3d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Service Fabric kümesi güvenlik senaryoları
Service Fabric kümesi sahip olduğunuz bir kaynaktır. Kümeler, yetkisiz kullanıcıların özellikle üretim iş yükleri üzerinde çalıştırılan sahip olduğunda, kümeniz için bağlanmasını önlemek için güvenli hale getirilmelidir. Güvenli olmayan bir küme oluşturmak mümkün olsa da, genel internet yönetim uç noktalarını kullanıma sunar, bunu yapmak bu nedenle, anonim bağlanmasına olanak sağlar. 

Bu makalede, Azure veya tek başına ve bu senaryolar uygulamak için kullanılan teknolojiler çalıştıran kümeler için güvenlik senaryoları genel bir bakış sağlar. Küme güvenlik senaryolar şunlardır:

* Düğümü düğümü güvenlik
* İstemcisi düğümü güvenlik
* Rol tabanlı erişim denetimi (RBAC)

## <a name="node-to-node-security"></a>Düğümü düğümü güvenlik
VM'ler veya kümede makineler arasındaki iletişimin güvenliğini sağlar. Bu, kümeye katılmak için yetkili bilgisayarları uygulamaları ve Hizmetleri kümedeki barındırma katılabilir sağlar.

![Düğümü düğümü iletişim diyagramı][Node-to-Node]

Windows üzerinde çalışan Azure veya tek başına kümeleri üzerinde çalışan kümelerle kullanabilirsiniz [sertifika güvenliği](https://msdn.microsoft.com/library/ff649801.aspx) veya [Windows Güvenliği](https://msdn.microsoft.com/library/ff649396.aspx) Windows Server makinelerini için.

### <a name="node-to-node-certificate-security"></a>Düğümü düğümü sertifika güvenliği
Service Fabric Küme oluşturduğunuzda, belirttiğiniz düğüm türü yapılandırmaları bir parçası olarak X.509 sunucu sertifikaları kullanır. Bu makalenin sonunda bu sertifikaları nedir ve nasıl elde veya bunları oluşturmanız hızlı bir genel bakış sağlanır.

Sertifika Güvenliği Azure portalı, Azure Resource Manager şablonları veya tek başına JSON şablon ile küme oluşturma sırasında yapılandırılır. Birincil bir sertifika ve sertifika rollover için kullanılan isteğe bağlı ikincil bir sertifika belirtebilirsiniz. Belirttiğiniz birincil ve ikincil sertifikaları yönetici istemci ve salt okunur istemci sertifikalarını belirtmek için farklı [istemcisi düğümü güvenlik](#client-to-node-security).

Azure okumak için [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](service-fabric-cluster-creation-via-arm.md) bir kümede sertifika güvenliği yapılandırma hakkında bilgi edinmek için.

Windows Server için tek başına okuma [X.509 sertifikaları kullanarak Windows'u bir tek başına kümede güvenli](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>Düğümü düğümü windows güvenliği
Windows Server için tek başına okuma [Windows güvenliği kullanarak Windows'u bir tek başına kümede güvenli](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>İstemcisi düğümü güvenlik
İstemcilerin kimliğini doğrular ve bir istemci ve bireysel düğümleri arasındaki iletişimin güvenliğini sağlar. Bu tür güvenlik kimliğini doğrular ve yalnızca yetkili kullanıcılar küme ve kümedeki dağıtılan uygulamalar erişebilmesini sağlar istemci iletişimleri güvenliğini sağlar. İstemciler, Windows güvenlik kimlik bilgilerini veya sertifika güvenlik kimlik bilgilerini benzersiz şekilde tanımlanır.

![İstemci düğüme iletişim diyagramı][Client-to-Node]

Windows üzerinde çalışan Azure veya tek başına kümeleri üzerinde çalışan kümelerle kullanabilirsiniz [sertifika güvenliği](https://msdn.microsoft.com/library/ff649801.aspx) veya [Windows Güvenliği](https://msdn.microsoft.com/library/ff649396.aspx).

### <a name="client-to-node-certificate-security"></a>İstemci düğüm sertifika güvenliği
 İstemci düğüm sertifika güvenliği Resource Manager şablonları ya da bir yönetici istemci sertifikası ve/veya bir kullanıcı istemci sertifikası belirterek tek başına JSON şablon Azure Portalı aracılığıyla ya da küme oluşturulurken yapılandırılır.  Belirttiğiniz yönetici istemci ve kullanıcı istemci sertifikalarını belirtmek için birincil ve ikincil sertifikaları farklı [düğümü düğümü güvenlik](#node-to-node-security) açısından en iyisi. Varsayılan olarak, küme sertifikaları düğümü düğümü güvenlik için izin verilen istemci yönetim sertifikalar listesine eklenir.

Yönetim sertifikası kullanılarak kümesine bağlanan istemciler, yönetim özellikleri için tam erişime sahip.  Salt okunur kullanıcı istemci sertifikası kullanılarak kümesine bağlanan istemciler yönetim özellikleri yalnızca okuma erişimi var. Diğer bir deyişle bu sertifikalar, bu makalenin sonraki bölümlerinde açıklanan rol tabanları erişim denetimi (RBAC) için kullanılır.

Azure okumak için [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](service-fabric-cluster-creation-via-arm.md) bir kümede sertifika güvenliği yapılandırma hakkında bilgi edinmek için.

Windows Server için tek başına okuma [X.509 sertifikaları kullanarak Windows'u bir tek başına kümede güvenli](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Azure üzerinde istemci düğümünde Azure Active Directory (AAD) güvenlik
Azure üzerinde çalışan kümelerle de Azure Active Directory (AAD) kullanan yönetim uç noktalarına erişime güvenliğini sağlayabilirsiniz. Bkz: [bir Azure Resource Manager şablonu kullanarak bir küme ayarlama](service-fabric-cluster-creation-via-arm.md) gerekli AAD yapıları oluşturma, küme oluşturma sırasında doldurmak nasıl ve daha sonra bu kümeye bağlanma hakkında bilgi.

## <a name="security-recommendations"></a>Güvenlik önerileri
Azure kümeler için istemciler ve sertifikaları düğümü düğümü güvenlik kimlik doğrulaması için AAD güvenlik kullanmanız önerilir.

Windows Server 2012 R2 ve Active Directory varsa, tek başına Windows Server için Windows Güvenlik grubu ile kullanmanız önerilir kümeleri (GMA) yönetilen hesapları. Hala Windows güvenliği Windows hesaplarıyla kullanmayacak.

## <a name="role-based-access-control-rbac"></a>Rol tabanlı erişim denetimi (RBAC)
Erişim denetimi, belirli küme işlemleri farklı küme daha güvenli hale getirme kullanıcı grupları için erişimi sınırlamak Küme Yöneticisi sağlar. Bir kümeye bağlanan istemciler için desteklenen iki farklı erişim denetimi türleri: Yönetici rolü ve kullanıcı rolü.

Yöneticiler için yönetim özellikleri (okuma/yazma özellikleri dahil) tam erişime sahip. Kullanıcıların varsayılan olarak, yalnızca yönetim özellikleri (örneğin, sorgu özellikleri) okuma erişimi ve uygulamaları ve Hizmetleri çözümleme olanağı vardır.

Yönetici ve kullanıcı istemci rolleri küme oluşturma sırasında ayrı kimlikleri (Sertifikalar, AAD vb.) sağlayarak her biri için belirtin. Varsayılan erişim denetimi ayarlarını ve varsayılan ayarlarının nasıl değiştirileceği hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](service-fabric-cluster-security-roles.md).

## <a name="x509-certificates-and-service-fabric"></a>X.509 sertifikaları ve Service Fabric
X.509 dijital sertifikalar, istemciler ve sunucular kimlik doğrulaması ve şifreleme ve iletileri dijital olarak imzala için yaygın olarak kullanılır. Bu sertifikalar hakkında daha fazla ayrıntı için Git [sertifikalarla çalışma](http://msdn.microsoft.com/library/ms731899.aspx).

Dikkate alınması gereken bazı önemli noktalar:

* Üretim iş yükleri çalıştıran kümelerde kullanılan sertifikaları doğru yapılandırılmış bir Windows Server sertifika hizmetini kullanarak oluşturulmamalı veya bir onaylanan alınan [sertifika yetkilisi (CA)](https://en.wikipedia.org/wiki/Certificate_authority).
* MakeCert.exe gibi araçları ile oluşturulmuş üretim sertifikaları test veya hiçbir zaman hiçbir geçici kullanın.
* Kendinden imzalı bir sertifika kullanabilirsiniz, ancak yalnızca test kümeleri için alan ve üretim yapmalısınız.

### <a name="server-x509-certificates"></a>X.509 sertifikaları
Sunucu sertifikaları istemcilere bir sunucu (düğüm) kimlik doğrulaması ya da bir sunucu (düğüm) için bir sunucu (düğüm) kimlik doğrulaması birincil görev vardır. Bir istemci veya düğüm bir düğüm doğruladığında ilk denetimleri konu alanında ortak adı değerini denetlemek için biridir. Bu ortak adı veya sertifikalar konu diğer adları biri izin verilen Ortak adların listesinde olmalıdır.

Aşağıdaki konu diğer adlarını (SAN) ile sertifikalarını oluşturmak makalede: [güvenli LDAP sertifika için bir konu alternatif adı eklemek nasıl](http://support.microsoft.com/kb/931351).

Her değer türü belirtmek için bir başlatma öneki, konu alanı çeşitli değerler içerebilir. En yaygın olarak, başlatma "CN =" ortak adıdır; Örneğin, "CN = www.contoso.com". Konu alanı boş olması da mümkündür. İsteğe bağlı konu alternatif adı alanında doldurulursa, sertifikanın ortak adı ve konu alternatif adı her bir giriş içermelidir. Bu DNS adı değerler girilir.

Sertifikanın hedeflenen amaçlar alanının değeri, "Sunucu kimlik doğrulaması" veya "İstemci kimlik doğrulaması" gibi uygun bir değer içermesi gerekir.

### <a name="client-x509-certificates"></a>İstemci X.509 sertifikaları
İstemci sertifikaları genellikle bir üçüncü taraf sertifika yetkilisi tarafından verilen değil. Bunun yerine, geçerli kullanıcının konuma kişisel deposunda genellikle istemci sertifikalarını yok "İstemci kimlik doğrulaması" amacı olan bir kök yetkilisi tarafından yerleştirilen içerir. Karşılıklı kimlik doğrulaması gerekli olduğunda, istemcinin bu tür bir sertifika kullanabilirsiniz.

> [!NOTE]
> Service Fabric kümesi üzerindeki tüm yönetim işlemlerinin sunucu sertifikaları gerektirir. İstemci sertifikalarını yönetimi için kullanılamaz.
> 
> 

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->


## <a name="next-steps"></a>Sonraki adımlar
Bu makalede küme güvenliği hakkında kavramsal bilgiler verilmektedir. Ardından,


1.  [Resource Manager şablonu kullanarak Azure'da bir küme oluşturun](service-fabric-cluster-creation-via-arm.md) 
2.  [Azure portal](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
