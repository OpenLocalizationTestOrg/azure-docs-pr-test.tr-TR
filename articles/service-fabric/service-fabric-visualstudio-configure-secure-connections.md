---
title: "aaaConfigure güvenli Azure Service Fabric kümesi bağlantıları | Microsoft Docs"
description: "Nasıl toouse Visual Studio tooconfigure güvenli hello Azure Service Fabric kümesi tarafından desteklenen bağlantı hakkında bilgi edinin."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a>Visual Studio'dan güvenli bağlantılar tooa Service Fabric kümesi yapılandırın
Nasıl toouse Visual Studio toosecurely erişim Azure Service Fabric kümesi yapılandırılmış erişim denetimi ilkeleri hakkında bilgi edinin.

## <a name="cluster-connection-types"></a>Küme bağlantı türleri
İki tür bağlantı hello Azure Service Fabric kümesi tarafından desteklenir: **güvenli olmayan** bağlantıları ve **x509 sertifika tabanlı** güvenli bağlantılar. (Şirket içi, Service Fabric kümeleri barındırılan için **Windows** ve **dSTS** kimlik doğrulamaları de desteklenir.) Merhaba küme oluşturulduğunda tooconfigure hello küme bağlantı türüne sahip. Merhaba bağlantı türü, bir kez oluşturulduktan sonra değiştirilemez.

Merhaba Visual Studio Service Fabric araçları bağlanan tooa kümesi yayımlama için tüm kimlik doğrulama türlerini destekler. Bkz: [hello Azure portal ' bir Service Fabric kümesi ayarlama](service-fabric-cluster-creation-via-portal.md) yönelik yönergeler tooset güvenli Service Fabric kümesi.

## <a name="configure-cluster-connections-in-publish-profiles"></a>Küme bağlantılarını yapılandırma yayımlama profilleri
Visual Studio Service Fabric projeden yayımlama hello kullanın **Service Fabric uygulaması yayımlama** iletişim kutusu toochoose Azure Service Fabric kümesi. Altında **bağlantı uç noktasının**, aboneliğinizdeki mevcut bir kümeyi seçin.

![Merhaba ** yayımlama Service Fabric uygulaması ** iletişim kutusudur kullanılan tooconfigure Service Fabric bağlantı.][publishdialog]

Merhaba **Service Fabric uygulaması yayımlama** iletişim kutusu hello küme bağlantısı otomatik olarak doğrular. İstenirse, tooyour Azure hesabı oturum açın. Doğrulama başarılı olursa, sisteminizi hello sertifikaları güvenli bir şekilde tooconnect toohello küme yüklü veya güvenli olmayan kümenizi doğru olduğunu gösterir. Doğrulama hataları, ağ sorunları veya doğru şekilde yapılandırılmış sistem tooconnect tooa güvenli kümenizi olmamasından kaynaklanabilir.

![Merhaba ** yayımlama Service Fabric uygulama iletişim kutusu doğrular var olan ** doğru yapılandırılmış Service Fabric kümesi bağlantısı.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a>tooconnect tooa güvenli küme
1. Bir hedef küme güvenleri hello hello istemci sertifikalarının erişebildiğinden emin olun. Merhaba sertifika genellikle bir kişisel bilgi değişimi (.pfx) dosyası olarak paylaşılır. Bkz: [hello Azure portal ' bir Service Fabric kümesi ayarlama](service-fabric-cluster-creation-via-portal.md) nasıl tooconfigure hello sunucu toogrant erişim tooa istemci için.
2. Merhaba güvenilir bir sertifika yükleyin. toodo bunu hello .pfx dosyasını çift tıklatın veya hello PowerShell komut dosyası alma PfxCertificate tooimport hello sertifikaları kullanın. Merhaba sertifikası çok yüklemek**Cert: \LocalMachine\My**. Tamam tooaccept olan hello sertifika alınırken tüm varsayılan ayarlar.
3. Merhaba seçin **Yayımla...**  hello kısayol menüsünde hello proje tooopen hello komutunu **Azure uygulamasını Yayımla** iletişim kutusunu ve ardından hello hedef küme. Merhaba aracı otomatik olarak hello bağlantı çözümler ve hello parametrelerinde yayımlama hello güvenli bağlantı profilini kaydeder.
4. İsteğe bağlı: Hello düzenleyebilirsiniz profili toospecify güvenli küme bağlantısı yayımlayın.
   
   Merhaba yayımlama profili XML dosya toospecify hello sertifika bilgilerini el ile düzenlediğiniz olduğundan emin toonote hello sertifika depolama alanı adı olması, konum ve sertifika parmak izi depolamak. Bu değerler hello sertifika deposu için ad ve konum depolamak tooprovide gerekir. Bkz: [nasıl yapılır: bir sertifikanın parmak izini alma hello](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) daha fazla bilgi için.
   
   Merhaba kullanabilirsiniz *ClusterConnectionParameters* toohello Service Fabric kümesi bağlanırken parametreleri toospecify hello PowerShell parametreleri toouse. Herhangi biri hello Connect-ServiceFabricCluster cmdlet'i tarafından kabul edilen geçerli parametreleridir. Bkz: [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) kullanılabilir parametrelerin listesi.
   
   Tooa uzaktan küme yayımlıyorsanız toospecify hello uygun parametreleri, belirli küme için gerekir. Merhaba, güvenli olmayan bağlantı tooa küme örneği aşağıdadır:
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   Bağlantı tooan x509 sertifika tabanlı güvenli küme için örnek aşağıda verilmiştir:
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. Diğer gerekli tüm ayarları, yükseltme parametreler ve uygulama parametre dosyası konumu gibi düzenleyin ve ardından yayımlama hello uygulamanızdan **Service Fabric uygulaması yayımlama** Visual Studio'da iletişim kutusu.

## <a name="next-steps"></a>Sonraki adımlar
Service Fabric kümeleri erişme hakkında daha fazla bilgi için bkz: [Service Fabric Explorer kullanarak kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
