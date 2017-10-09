---
title: "Visual Studio ile bir uygulama tooa uzaktan küme aaaPublish | Microsoft Docs"
description: "Bir uygulama tooa uzak hizmet doku toopublish nasıl küme Visual Studio kullanarak öğrenin."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Dağıtma ve Visual Studio kullanarak uygulamaları kaldırma
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient API’leri](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Hello Azure Service Fabric uzantısı Visual Studio için bir kolay, yinelenebilir ve komut dosyalı bir yolu toopublish bir uygulama tooa Service Fabric kümesi sağlar.

## <a name="hello-artifacts-required-for-publishing"></a>yayımlama için gerekli hello yapıları
### <a name="deploy-fabricapplicationps1"></a>Dağıtma FabricApplication.ps1
Bu bir yayımlama profili yolu yayımlama Service Fabric uygulamaları için parametre olarak kullanan bir PowerShell komut dosyasıdır. Bu komut dosyası uygulamanızın parçası olduğundan, Hoş Geldiniz toomodify olan, uygulamanız için gerekli olarak.

### <a name="publish-profiles"></a>Yayımlama profilleri
Adlı bir klasör hello Service Fabric uygulaması proje **PublishProfiles** gibi bir uygulama yayımlamak için gerekli bilgileri depolamak XML dosyası içeriyor:

* Service Fabric kümesi bağlantı parametreleri
* Yol tooan uygulama parametre dosyası
* Yükseltme Ayarları

Varsayılan olarak, uygulamanızın üç içerecektir yayımlama profilleri: Local.1Node.xml, Local.5Node.xml ve Cloud.xml. Kopyalama ve yapıştırma hello varsayılan dosyalarından biri, daha fazla profil ekleyebilirsiniz.

### <a name="application-parameter-files"></a>Uygulama parametre dosyaları
Adlı bir klasör hello Service Fabric uygulaması proje **ApplicationParameters** kullanıcı tarafından belirtilen uygulama bildirim parametre değerleri için XML dosyası içeriyor. Dağıtım ayarları için farklı değerler kullanabilmesi için uygulama bildirim dosyaları parametreli olabilir. uygulamanızın, kümesini parametreleştirme hakkında daha fazla toolearn bkz [Service Fabric birden çok ortamlarında yönetme](service-fabric-manage-multiple-environment-app-configuration.md).

> [!NOTE]
> Aktör Hizmetleri için Merhaba Projeyi derlemek Yayımla iletişim kutusu tooedit hello dosyasına bir düzenleyicide veya hello aracılığıyla denemeden önce ilk. Bu durum, hello bildirim dosyaları parçası hello derleme sırasında oluşturulur çünkü.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish hello Service Fabric uygulaması yayımlama iletişim kutusunu kullanarak uygulama
Merhaba aşağıdaki adımları kullanarak bir uygulama toopublish nasıl hello göstermek **Service Fabric uygulaması yayımlama** hello Visual Studio Service Fabric araçları tarafından sağlanan iletişim kutusu.

1. Merhaba kısayol menüsünde hello Service Fabric uygulaması projesinin, **Yayımla...** tooview hello **Service Fabric uygulaması yayımlama** iletişim kutusu.
   
    ![Merhaba ** yayımlama Service Fabric uygulaması ** iletişim kutusu][0]
   
    Merhaba dosyası Hello seçili **hedef profil** açılır liste kutusunda nerede olduğundan hello ayarlarının tümünü dışında **bildirim sürümleri**, kaydedilir. Varolan bir profile yeniden veya seçerek yeni bir tane oluşturun **< profillerini yönetme... >** hello içinde **hedef profil** açılır liste kutusu. Bir yayımlama profili seçtiğinizde, içeriği hello iletişim kutusunun hello karşılık gelen alanlar görünür. toosave değişikliklerinizi herhangi bir zamanda seçin hello **profili Kaydet** bağlantı.    
2. Merhaba, **bağlantı uç noktasının** bölümünde, bir yerel veya uzak Service Fabric kümenin yayımlama uç noktası belirtin. tooadd ya da değişiklik bağlantı uç noktasının Merhaba, üzerinde hello tıklatın **bağlantı uç noktasının** açılır liste. Azure Abonelikleriniz yayımlayabilirsiniz hello kullanılabilir Service Fabric kümesi bağlantı uç noktaları toowhich dayalı Hello listesini gösterir. TooVisual Studio günlüğe kaydedilmez, istendiğinde toodo kadar olacağını unutmayın.
   
    Kullanılabilir abonelikler ve kümelerinin hello kümesinden Hello küme seçimi iletişim kutusunu toochoose kullanın.
   
    ![Merhaba ** seçin Service Fabric kümesi ** iletişim kutusu][1]
   
   > [!NOTE]
   > Merhaba toopublish tooan rasgele uç noktası (örneğin, bir taraf küme için) istiyorsanız bkz **tooan rasgele küme uç noktası yayımlama** bölümüne bakın.
   > 
   > 
   
    Bir uç nokta seçildikten sonra Visual Studio hello bağlantı toohello seçili Service Fabric kümesi doğrular. Merhaba küme güvenli değilse, Visual Studio tooit hemen bağlanabilir. Merhaba küme güvenli ise, devam etmeden önce yerel bilgisayarınızda tooinstall bir sertifika gerekir. Bkz: [nasıl tooconfigure güvenli bağlantıları](service-fabric-visualstudio-configure-secure-connections.md) daha fazla bilgi için. İşiniz bittiğinde, hello seçin **Tamam** düğmesi. Merhaba seçili küme görünür hello **Service Fabric uygulaması yayımlama** iletişim kutusu.
3. Merhaba, **uygulama parametre dosyası** açılır liste kutusunda, tooan uygulama parametre dosyası gidin. Bir uygulama parametre dosyası parametrelerinin değerleri kullanıcı tarafından belirtilen hello uygulama bildirim dosyasında tutar. tooadd veya değişiklik bir parametre seçin hello **Düzenle** düğmesi. Girin veya hello hello parametrenin değeri değiştirin **parametreleri** kılavuz. İşiniz bittiğinde, hello seçin **kaydetmek** düğmesi.
   
    ![Merhaba ** Düzenle parametreleri ** iletişim kutusu][2]
4. Kullanım hello **yükseltme hello uygulama** onay kutusunu toospecify Bu yayımlama eylem olup yükseltme. Yükseltme yayımlama eylemleri normal farklı eylemler yayımlayın. Bkz: [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md) farklar listesi. tooconfigure yükseltme ayarlarını seçin hello **yükseltme ayarlarını yapılandır** bağlantı. Merhaba yükseltme parametre Düzenleyicisi görüntülenir. Bkz: [Service Fabric uygulaması hello yükseltmesini yapılandırmak](service-fabric-visualstudio-configure-upgrade.md) toolearn yükseltme parametreleri hakkında daha fazla.
5. Merhaba seçin **bildirim sürümleri...** Düğme tooview hello **Düzenle sürümleri** iletişim kutusu. Bir yükseltme tootake yer tooupdate uygulama ve hizmet sürümleri gerekir. Bkz: [Service Fabric uygulama yükseltme öğretici](service-fabric-application-upgrade-tutorial.md) toolearn nasıl uygulama ve hizmet bildirimi sürümleri etkisi bir yükseltme işlemi.
   
    ![Merhaba ** Düzenle sürümleri ** iletişim kutusu][3]
   
    Merhaba uygulama ve hizmet sürümleri 1.0.0 veya sayısal değerleri gibi anlamsal sürüm 1.0.0.0 hello biçiminde kullanırsanız, hello seçin **otomatik olarak uygulama ve hizmet sürümleri güncelleştirme** seçeneği. Ne zaman bu seçenek, hello hizmeti seçin ve uygulama sürüm numaralarını otomatik olarak güncelleştirilen bir kod, yapılandırma her veya veri paketinin sürümü güncelleştirilir. Tooedit hello sürümleri el ile tercih ederseniz, bu özellik hello onay kutusunu toodisable temizleyin.
   
   > [!NOTE]
   > Tüm paket girişleri tooappear için aktör projesi için önce hello girişleri hello Service Manifest dosyalarında hello proje toogenerate oluşturun.
   > 
   > 
6. Tamamladığınızda tüm hello gerekli ayarları belirtme seçin hello **Yayımla** seçili, uygulama toohello toopublish düğmesini Service Fabric kümesi. Belirttiğiniz hello ayarları uygulanır toohello yayımlama işlemi.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>Tooan rasgele küme uç noktası (taraf kümeleri dahil olmak üzere) yayımlama
Merhaba Visual Studio yayımlama deneyimi, Azure aboneliklerinize biriyle ilişkili tooremote kümeleri yayımlamak için en iyi duruma getirilmiştir. Ancak yayımlama Hello düzenleme doğrudan profili XML tarafından olası toopublish tooarbitrary uç noktaları (örneğin, Service Fabric taraf kümeler) olur. Yukarıda açıklandığı gibi üç yayımlama profillerini varsayılan olarak--sağlanan**Local.1Node.xml**, **Local.5Node.xml**, ve **Cloud.xml**--ancak Hoş Geldiniz toocreate farklı ortamlar için ek profiller. Tooparty kümeler, belki de adlı yayımlamak için toocreate bir profil örneği için isteyebilirsiniz **Party.xml**.

Küme güvenli tooan bağlanıyorsanız, gerekli olan tek şey hello küme bağlantı uç noktası, gibi `partycluster1.eastus.cloudapp.azure.com:19000`. Durumda, yayımlama hello hello bağlantı uç noktasında, profili şöyle görünür:

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  Tooa güvenli küme bağlanıyorsanız tooprovide hello hello istemci sertifika kimlik doğrulaması için kullanılan hello yerel deposu toobe ayrıntılarını da gerekir. Daha fazla ayrıntı için bkz: [yapılandırma güvenli bağlantılar tooa Service Fabric kümesi](service-fabric-visualstudio-configure-secure-connections.md).

  Yayımlama profilinizi ayarladıktan sonra hello başvurabilir aşağıda gösterildiği gibi Yayımla iletişim kutusu.

  ![Yeni Yayımlama profili Yayımla iletişim kutusu][4]

  Bu durumda, yeni hello yayımlama profili, Not hello varsayılan uygulama parametreleri dosyalarını tooone işaret eder. Bu, toopublish istiyorsanız, aynı uygulama yapılandırma tooa sayıda ortamları hello uygundur. Bunun aksine, toohave farklı yapılandırmaları için toopublish istediğiniz her bir ortamda istediğiniz durumlarda bu algılama toocreate karşılık gelen bir uygulama parametre dosyası olmaması anlamına gelir.

## <a name="next-steps"></a>Sonraki adımlar
tooautomate hello yayımlama işlemi sürekli tümleştirme bir ortamda nasıl görürüm toolearn [Service Fabric sürekli tümleştirme kurup](service-fabric-set-up-continuous-integration.md).

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
