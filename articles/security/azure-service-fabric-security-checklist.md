---
title: "aaaAzure service fabric güvenlik denetim listesi | Microsoft Docs"
description: "Bu makalede, bir dizi denetim listesi için Azure doku güvenlik güvenlik sağlar."
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
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Azure Service Fabric güvenlik denetim listesi
Bu makale Azure Service Fabric ortamınızın güvenliğini sağlamanıza yardımcı olacak bir kullanımı kolay denetim sağlar.

## <a name="introduction"></a>Giriş
Azure Service Fabric kolay toopackage kolaylaştıran bir dağıtılmış sistemler platformudur, dağıtın ve ölçeklenebilir ve güvenilir mikro yönetin. Service Fabric da geliştirmeye ve bulut uygulamalarını yönetme hello önemli sorunları giderir. Geliştiriciler ve yöneticiler, karmaşık altyapı sorunlarını çözmeye çalışmak yerine görev açısından kritik, zorlu iş yüklerini uygulamaya odaklanabilir. Service Fabric, bu iş yüklerinin ölçeklenebilir, güvenilir ve yönetilebilir olmasını sağlar.

## <a name="checklist"></a>Denetim listesi
Yönetim ve yapılandırma, güvenli Azure Service Fabric çözümünün önemli sorunları atlamış henüz emin denetim listesi toohelp aşağıdaki hello kullanın.


|Denetim listesi kategorisi| Açıklama |
| ------------ | -------- |
|[Rol tabanlı erişim denetimi (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>Erişim denetimi hello Küme Yöneticisi toolimit erişim toocertain küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için sağlar.</li><li>Yöneticiler tam erişim toomanagement özellikleri (okuma/yazma özellikleri dahil) sahiptir. </li><li>   Kullanıcıların varsayılan olarak, yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve hizmetleri vardır.</li></ul>|
|[X.509 sertifikaları ve Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>[Sertifikaları](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates) çalışan üretim iş yükleri doğru yapılandırılmış bir Windows Server sertifika hizmetini kullanarak oluşturulmamalı veya bir onaylanan alınan kümelerinde kullanılan [sertifika yetkilisi (CA)](https://en.wikipedia.org/wiki/Certificate_authority).</li><li>Hiçbir zaman kullanmak [geçici veya test sertifikaları](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development) gibi araçları ile oluşturulmuş üretimde [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx). </li><li>Kullanabileceğiniz bir [otomatik olarak imzalanan sertifika](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) ancak yalnızca test kümeleri için alan ve üretim yapmalısınız.</li></ul>|
|[Küme güvenliği](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>Merhaba küme güvenlik senaryoları dahil düğümü düğümü güvenlik, istemci düğümü güvenlik, [rol tabanlı erişim denetimi (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles).</li></ul>|
|[Küme kimlik doğrulaması](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Kimlik doğrulaması [düğümü düğümü iletişimi](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md) küme Federasyon. </li></ul>|
|[Sunucu kimlik doğrulaması](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Merhaba kimliğini doğrulayan [yönetim uç noktalarının küme](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal) tooa management istemcisi.</li></ul>|
|[Uygulama güvenliği](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>Şifreleme ve şifre çözme uygulama yapılandırma değerlerini.</li><li> Çoğaltma sırasında şifreleme düğümler arasında veri.</li></ul>|
|[Küme sertifikası](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>Bu sertifika bir kümede hello düğümler arasında gerekli toosecure hello iletişim yok.</li><li>  Merhaba sertifikanın parmak izini hello birincil hello parmak izi bölüm içinde ve, hello hello ThumbprintSecondary değişkenlerine ikincil ayarlayın.</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>Tooconnect toothis küme çalıştığında bu sertifikayı toohello istemci sunulur. İki farklı sunucu sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz.</li></ul>|
|ClientCertificateThumbprints| <ul><li>Kimliği doğrulanmış hello istemcilerde tooinstall istediğiniz sertifikaları kümesidir. </li></ul>|
|ClientCertificateCommonNames| <ul><li>Merhaba hello CertificateCommonName için hello ilk istemci sertifikasının ortak ad olarak ayarlayın. Merhaba CertificateIssuerThumbprint hello veren bu sertifikanın parmak izi hello ' dir. </li></ul>|
|ReverseProxyCertificate| <ul><li>Bu, olabilir, isteğe bağlı bir sertifikadır toosecure isteyip istemediğinizi belirtilen, [Ters Proxy](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy). </li></ul>|
|Anahtar Kasası| <ul><li>Azure Service Fabric kümeleri için toomanage sertifikalar kullanılır.  </li></ul>|


## <a name="next-steps"></a>Sonraki adımlar
- [Service Fabric kümesi yükseltme işlemi ve sizden beklentileri](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [Visual Studio'da, Service Fabric uygulamaları yönetme](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio).
- [Service Fabric sistem durumu modeli giriş](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction).
