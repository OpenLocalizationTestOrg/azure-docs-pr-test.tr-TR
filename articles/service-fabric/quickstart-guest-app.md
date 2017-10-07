---
title: "aaaQuickly var olan bir uygulama tooan Azure Service Fabric kümesi dağıtma"
description: "Azure Service Fabric kümesi toohost var olan bir Node.js uygulamasını Visual Studio ile kullanın."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Node.js uygulamasını Azure Service Fabric'te barındırma

Bu hızlı başlangıç Azure üzerinde çalışan bir var olan uygulama (Bu örnekte Node.js) tooa Service Fabric kümesi dağıtmanıza yardımcı olur.

## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce [geliştirme ortamınızı ayarladığınızdan](service-fabric-get-started.md) emin olun. Merhaba Service Fabric SDK ve Visual Studio 2017 veya 2015 yüklenmesini içerir.

Dağıtım için toohave var olan bir Node.js uygulamasını da gerekir. Bu hızlı başlangıçta, [buradan][download-sample] indirilebilen basit bir Node.js web sitesi kullanılmıştır. Bu dosya tooyour ayıklamak `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` hello sonraki adımda hello projesi oluşturduktan sonra klasör.

Azure aboneliğiniz yoksa [ücretsiz bir hesap][create-account] oluşturun.

## <a name="create-hello-service"></a>Merhaba hizmet oluşturma

Visual Studio'yu **yönetici** olarak başlatın.

`CTRL`+`SHIFT`+`N` ile bir proje oluşturun

Merhaba, **yeni proje** iletişim kutusunda, seçin **bulut > Service Fabric uygulaması**.

Ad Merhaba uygulaması **MyGuestApp** ve basın **Tamam**.

>[!IMPORTANT]
>Node.js hello 260 karakter sınırını windows olan yollar için kolayca bozulabilir. Kısa bir yol hello projesi için kendisini gibi kullandığınız **c:\code\svc1**.
   
![Visual Studio'da yeni proje iletişim kutusu][new-project]

Service Fabric hizmeti herhangi bir türde hello sonraki iletişim kutusundan oluşturabilirsiniz. Bu hızlı başlangıç için **Konuk Yürütülebilir Dosyası**'nı seçin.

Ad hello hizmeti **MyGuestService** ve hello sağ toohello üzerinde hello seçeneklerini ayarlama aşağıdaki değerler:

| Ayar                   | Değer |
| ------------------------- | ------ |
| Kod Paketi Klasörü       | _&lt;Node.js uygulamanızı Hello klasörüyle&gt;_ |
| Kod Paketi Davranışı     | Klasör içeriği tooproject kopyalama |
| Program                   | node.exe |
| Bağımsız Değişkenler                 | server.js |
| Çalışma Klasörü            | CodePackage |

**Tamam**'a basın.

![Visual Studio'da yeni hizmet iletişim kutusu][new-service]

Visual Studio hello uygulama projesi ve hello aktör hizmeti projesi oluşturur ve bunları Çözüm Gezgini'nde görüntüler.

Merhaba uygulama projesi (**MyGuestApp**) herhangi bir kod doğrudan içermiyor. Bunun yerine, bir dizi hizmet projesine başvuru sağlar. Ayrıca, bunlardan farklı olarak üç tür içerik daha barındırır:

* **Yayımlama profilleri**  
Farklı ortamlar için araç tercihleri.

* **Betikler**  
Uygulamanızı dağıtmak/yükseltmek için PowerShell betiği.

* **Uygulama tanımı**  
Merhaba uygulama bildirimi içerir *ApplicationPackageRoot*. İlişkili uygulama parametreleri dosyalarını olan altında *ApplicationParameters*, hello uygulamayı tanımlayan ve tooconfigure izin özellikle belirli bir ortam için.
    
Merhaba hizmet projesi Merhaba içeriğine genel bakış için bkz: [Reliable Services ile çalışmaya başlama](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Ağı ayarlama

Node.js uygulaması dağıtma kullandığı bağlantı noktası hello örnek **80** ve tootell kullanıma sunulan bağlantı noktası olduğunu ihtiyacımız Service Fabric ihtiyacımız.

Açık hello **ServiceManifest.xml** hello proje dosyasında. Hello bildirimi Hello kısımda olduğu bir `<Resources> \ <Endpoints>` önceden tanımlanmış bir girişi. Bu giriş tooadd değiştirme `Port`, `Protocol`, ve `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>TooAzure dağıtma

Basarsanız **F5** ve başlangıç projesi çalıştırın, dağıtılan toohello yerel küme olabilir. Ancak, şimdi tooAzure yerine dağıtın.

Merhaba projeye sağ tıklayın ve seçin **Yayımla...**  iletişim toopublish tooAzure açar.

![Yayımlama yapı hizmeti için tooazure iletişim kutusu][publish]

Select hello **PublishProfiles\Cloud.xml** hedef profil.

Daha önce yapmadıysanız, bir Azure hesabı toodeploy seçin. Henüz hesabınız yoksa, [bir hesap için kaydolun][create-account].

Altında **bağlantı uç noktasının**, hello Service Fabric kümesi toodeploy seçin. Bir yoksa seçin  **&lt;yeni küme oluştur... &gt;**  web tarayıcısı penceresi toohello Azure portal açar. Daha fazla bilgi için bkz: [hello Portalı'nda bir küme oluşturma](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal). 

Merhaba Service Fabric kümesi oluşturduğunuzda, emin tooset hello olun **özel uç noktaları** çok ayarı**80**.

![Uç noktayla Service Fabric düğüm türü yapılandırması][custom-endpoint]

Yeni bir Service Fabric kümesi oluşturuluyor bazı zaman toocomplete alır. Edildikten sonra oluşturulan, Git geri toohello yayımlama iletişim kutusu ve seçin  **&lt;yenileme&gt;**. Merhaba yeni küme hello açılan kutusunda listelenir; bunu seçin.

Tuşuna **Yayımla** ve hello dağıtım toofinish için bekleyin.

Bu birkaç dakika sürebilir. İşlem tamamlandıktan sonra hello uygulama toobe tam olarak kullanılabilir için birkaç dakika sürebilir.

## <a name="test-hello-website"></a>Test hello Web sitesi

Hizmetiniz yayımlandıktan sonra, hizmeti web tarayıcısında test edin. 

İlk olarak, hello Azure portalını açın ve Service Fabric hizmetinizi bulun.

Hello hizmeti adresi Hello genel bakış dikey penceresini denetleyin. Hello kullan hello etki alanı adından _istemci bağlantı uç noktasının_ özelliği. Örneğin, `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Service fabric genel bakış dikey penceresinde hello Azure portalı][overview]

Merhaba göreceğiniz toothis adresine gidin `HELLO WORLD` yanıt.

## <a name="delete-hello-cluster"></a>Merhaba küme silme

Siz bu hızlı başlangıç için oluşturduğunuz hello kaynakların tümünü bu kaynakları için ücretlendirilirsiniz toodelete unutmayın.

## <a name="next-steps"></a>Sonraki adımlar
[Konuk yürütülebilir dosyaları](service-fabric-deploy-existing-app.md) hakkındaki diğer yazıları okuyun.

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F