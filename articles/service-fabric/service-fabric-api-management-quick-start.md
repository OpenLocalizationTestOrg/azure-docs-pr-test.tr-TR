---
title: "API Management Hızlı Başlangıç ile Service Fabric aaaAzure | Microsoft Docs"
description: "Bu kılavuz size nasıl tooquickly Başlarken Azure API Management ve Service Fabric gösterir."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Service Fabric ile Azure API Management hızlı başlangıç

Bu kılavuz size gösterir nasıl tooset yukarı Azure API Management Service Fabric ile ve ilk API işlemi toosend trafiği tooback uç hizmetlerinizi Service Fabric yapılandırın. Service Fabric ile Azure API Management senaryoları hakkında daha fazla toolearn bkz hello [genel bakış](service-fabric-api-management-overview.md) makalesi. 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>API Management ve Service Fabric tooAzure dağıtma

Merhaba ilk toodeploy API Management ve paylaşılan bir sanal ağ içinde bir Service Fabric kümesi tooAzure adımdır. Bu, tooany arka uç hizmeti doğrudan Service Fabric hizmet bulma, hizmet bölümü çözümleme ve iletme trafiği gerçekleştirebilmek için Service Fabric ile doğrudan API Management toocommunicate sağlar.

### <a name="topology"></a>Topoloji

Bu kılavuz hello aşağıdaki dağıtır API Management ve Service Fabric olduğu alt ağların topoloji tooAzure hello aynı sanal ağ:

 ![Resim yazısı][sf-apim-topology-overview]

Resource Manager şablonları tooget hızlı bir şekilde başlatıldı, her dağıtım adımı için sağlanır:

 - Ağ topolojisi:
    - [Network.JSON][network-arm]
    - [Network.Parameters.JSON][network-parameters-arm]
 - Service Fabric kümesi:
    - [Cluster.JSON][cluster-arm]
    - [Cluster.Parameters.JSON][cluster-parameters-arm]
 - API Management:
    - [apim.JSON][apim-arm]
    - [apim.Parameters.JSON][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>İçinde tooAzure oturum ve aboneliğinizi seçin

Bu kılavuzu kullanır [Azure PowerShell][azure-powershell]. Yeni bir PowerShell oturumu başlattığınızda tooyour Azure hesabı oturum ve Azure komutları çalıştırmadan önce aboneliğinizi seçin.
 
Azure hesabı tooyour oturum:

```powershell
PS > Login-AzureRmAccount
```

Aboneliğinizi seçin:

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Dağıtımınız için yeni bir kaynak grubu oluşturun. Bir ad ve bir konum girin.

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>Merhaba ağ topolojisi dağıtmak

Merhaba ilk tooset hello ağ topolojisi toowhich API Management yukarı adımdır ve hello Service Fabric kümesi dağıtılır. Merhaba [network.json] [ network-arm] Resource Manager şablonu olan bir sanal ağ (VNET) iki alt ağı ve iki ağ güvenlik grupları (NSG) yapılandırılmış toocreate. 

Merhaba [network.parameters.json] [ network-parameters-arm] parametreler dosyası hello alt ağları ve API Management ve Service Fabric dağıtılacağı Nsg'ler hello adlarını içerir. Bu kılavuz, değiştirilen toobe hello parametre değerlerini gerekmez. bunlar burada değiştirilirse değiştirmeniz gerekir böylece bunları diğer Resource Manager şablonları aşağıdaki buna göre Merhaba, bu değerleri Hello API Management ve Service Fabric Resource Manager şablonları kullanın. 

 1. Aşağıdaki Resource Manager şablonu ve parametre dosyasına hello yükleyin:

    - [Network.JSON][network-arm]
    - [Network.Parameters.JSON][network-parameters-arm]

 2. PowerShell komut toodeploy hello Resource Manager şablonu ve parametre hello ağ kurulumu için aşağıdaki dosyaları hello kullan:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>Merhaba Service Fabric kümesi dağıtma

Hello ağ kaynaklarını dağıtma tamamladıktan sonra hello sonraki toodeploy hello alt ağda bir Service Fabric kümesi toohello VNET adımdır ve NSG hello Service Fabric kümesi için belirlenmiş. Bu öğretici için hello Service Fabric Resource Manager şablonu hello VNET, alt ağ ve hello önceki adımda ayarladığınız NSG önceden yapılandırılmış toouse hello adlarını ' dir. 

Merhaba Service Fabric kümesi Resource Manager şablonu yapılandırılmış toocreate sertifika güvenliği ile güvenli bir kümede ' dir. Merhaba, küme ve toomanage kullanıcı erişimi tooyour Service Fabric kümesi için kullanılan toosecure düğümü düğümü iletişim sertifikasıdır. API Management hizmet bulma için bu sertifika tooaccess hello Service Fabric adlandırma hizmeti kullanır.

Bu adım, bir sertifikanın anahtar kasası için küme güvenlik sonucunda gerektirir. Anahtar kasası ile güvenli bir küme ayarlama hakkında daha fazla bilgi için bkz: [bu kılavuz Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturma](service-fabric-cluster-creation-via-arm.md)

> [!NOTE]
> Toplama toohello sertifikasında küme erişimi için kullanılan Azure Active Directory kimlik doğrulaması ekleyebilir. Azure Active Directory şekilde toomanage kullanıcı erişimi tooyour Service Fabric kümesi önerilen Merhaba, ancak bu öğreticide gerekli olmayan toocomplete gelir. Bir sertifika her iki durumda da Azure Active Directory ile bir Service Fabric arka ucu için kimlik doğrulaması şu anda desteklemiyor Azure API Management kimlik doğrulama ve küme düğümü, düğümü güvenlik için gereklidir.

 1. Aşağıdaki Resource Manager şablonu ve parametre dosyasına hello yükleyin:
 
    - [Cluster.JSON][cluster-arm]
    - [Cluster.Parameters.JSON][cluster-parameters-arm]

 2. Merhaba boş hello parametrelerinde doldurun `cluster.parameters.json` hello dahil olmak üzere, dağıtımınız için dosya [anahtar kasası bilgileri](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) küme sertifikanızın.

 3. PowerShell komut toodeploy hello Resource Manager şablonu ve parametre dosyalarını toocreate hello Service Fabric kümesi aşağıdaki hello kullan:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>API Management dağıtma

Son olarak, API Management toohello VNET hello alt ağ ve API yönetimi için tasarlanmış NSG dağıtın. Toowait hello Service Fabric küme dağıtım toofinish için API Management dağıtmadan önce gerekmez. 

Bu öğretici için hello API Management Resource Manager şablonu hello VNET, alt ağ ve hello önceki adımda ayarladığınız NSG önceden yapılandırılmış toouse hello adlarını ' dir. 

 1. Aşağıdaki Resource Manager şablonu ve parametre dosyasına hello yükleyin:
 
    - [apim.JSON][apim-arm]
    - [apim.Parameters.JSON][apim-parameters-arm]

 2. Merhaba boş hello parametrelerinde doldurun `apim.parameters.json` dağıtımınız için.

 3. PowerShell toodeploy hello Resource Manager şablonu ve parametre betikleri için API Management aşağıdaki hello kullan:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>API Management yapılandırın

API Management ve Service Fabric kümesi dağıtıldığı sonra Service Fabric arka uç API Management'te yapılandırabilirsiniz. Bu, toocreate trafiği tooyour Service Fabric kümesi gönderir bir arka uç hizmeti ilke sağlar.

### <a name="api-management-security"></a>API yönetim güvenliği

tooconfigure hello Service Fabric arka uç, ilk tooconfigure API Management güvenlik ayarları gerekir. tooconfigure güvenlik ayarları, hello Azure portal tooyour API Management hizmetine gidin.

#### <a name="enable-hello-api-management-rest-api"></a>Merhaba API Management REST API etkinleştir

Merhaba API Management REST API hello tek yolu tooconfigure bir arka uç hizmeti şu anda değil. Merhaba ilk adımı tooenable hello API Management REST API ve onu güvenli.

 1. Hello API Management hizmeti, seçin **Yönetimi API - Önizleme** altında **güvenlik**.
 2. Merhaba denetleyin **API Management REST API etkinleştir** onay kutusu.
 3. Merhaba yönetim API'si URL Not - Bu hello URL hello Service Fabric arka uç yukarı sonraki tooset kullanacağız.
 4. Generate bir **belirtecine erişmesini** bir sona erme tarihi ve bir anahtar seçerek hello ardından **Oluştur** düğmesi hello sayfanın hello bulunun.
 5. Kopya hello **erişim belirteci** ve onu Kaydet - Bu adımları izleyerek hello kullanacağız. Bu hello birincil anahtar ve ikincil anahtar farklı olduğuna dikkat edin.

#### <a name="upload-a-service-fabric-client-certificate"></a>Service Fabric istemci sertifikasını karşıya yükle

API Management Service Fabric kümeniz erişim tooyour küme sahip bir istemci sertifikası kullanılarak hizmet bulma için kimlik doğrulaması gerekir. Kolaylık olması için Bu öğretici kullanır, varsayılan olarak kullanılan tooaccess olabilecek hello Service Fabric kümesi oluştururken, belirtilen aynı sertifika kümenizi hello.

 1. Hello API Management hizmeti, seçin **istemci sertifikalarını - Önizleme** altında **güvenlik**.
 2. Merhaba tıklatın **+ Ekle** düğmesi
 2. Merhaba özel anahtar dosyası (.pfx), Service Fabric kümesi oluştururken, belirtilen hello küme sertifika seçin, bir ad verin ve hello özel anahtar parolası sağlayın.

> [!NOTE]
> Bu öğretici, istemci kimlik doğrulaması ve küme düğümü, düğümü güvenliği için aynı sertifika hello kullanır. Service Fabric kümesi bir yapılandırılmış tooaccess varsa, ayrı bir istemci sertifikası kullanabilirsiniz.

### <a name="configure-hello-backend"></a>Merhaba arka uç yapılandırın

API Management güvenlik yapılandırıldığında, hello Service Fabric arka uç yapılandırabilirsiniz. Service Fabric arka uçlarını için belirli bir Service Fabric hizmeti yerine hello arka uç hello Service Fabric kümesi değil. Bu tek bir ilke tooroute toomore bir hizmet daha hello kümede sağlar.

Bu adım, daha önce oluşturulan hello erişim belirteci gerektirir ve tooAPI yönetim hello önceki adımda karşıya küme sertifikanızın parmak izi hello.

> [!NOTE]
> API Management hello önceki adımda ayrı istemci sertifikası kullandıysanız, bu adımda toplama toohello küme sertifika parmak izi hello istemci sertifikasını için hello parmak izi gerekir.

HTTP PUT İsteği toohello API yönetim API'si, daha önce hello API Management REST API tooconfigure hello Service Fabric arka uç hizmeti etkinleştirirken Not URL aşağıdaki hello gönderin. Görmeniz gerekir bir `HTTP 201 Created` hello komut başarılı olduğunda yanıt. Her bir alan hakkında daha fazla bilgi için bkz: hello API Management [arka uç API başvuru belgeleri](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).

HTTP komutu ve URL:
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

İstek üstbilgilerini:
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

İstek gövdesi:
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

Merhaba **url** burada parametredir hizmet kümenizdeki tüm istekleri tam hizmet adını yönlendirilen tooby varsayılan bir arka uç ilkesinde hiçbir hizmet adı belirtilirse. Sahte hizmet adı gibi kullanabilir "fabric: / sahte/service" toohave bir geri dönüş hizmet düşünmüyorsanız.

API Management toohello başvuran [arka uç API başvuru belgeleri](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) her bir alan hakkında daha fazla ayrıntı için.

#### <a name="example"></a>Örnek

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>Service Fabric arka uç hizmet dağıtma

Service Fabric arka uç tooAPI yönetim yapılandırılmış hello sahip olduğunuza göre arka uç ilkeleri tooyour Service Fabric hizmetleri trafiği göndermek için API'leri yazabilirsiniz. Ancak önce Service Fabric tooaccept isteklerinde çalışan bir hizmete gerekir.

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>Bir HTTP uç noktası ile bir Service Fabric hizmet oluşturma

Bu öğreticide, temel bir durum bilgisiz ASP.NET Core güvenilir hello varsayılan Web API projesi şablonunu kullanarak hizmet oluşturacağız. Azure API Management kullanıma hizmetiniz için bir HTTP uç noktası oluşturur:

```
/api/values
```

Tarafından Başlat [ASP.NET Core geliştirme için geliştirme ortamınızı kurma](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).

Geliştirme ortamınızı ayarladıktan sonra Visual Studio'yu yönetici olarak başlatın ve ASP.NET Core hizmet oluşturun:

 1. Visual Studio'da yeni proje dosyası seçin ->.
 2. Bulut altında Hello Service Fabric uygulaması şablonu seçin ve adlandırın **"ApiApplication"**.
 3. Merhaba ASP.NET çekirdek hizmet şablonu seçip adı hello proje **"WebApiService"**.
 4. Merhaba Web API ASP.NET Core 1.1 proje şablonu seçin.
 5. Merhaba Proje oluşturulduktan sonra açmak `PackageRoot\ServiceManifest.xml` hello kaldırıp `Port` hello uç nokta kaynak yapılandırması özniteliğinden:
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    Bu, bir bağlantı noktasından biz hello küme Resource Manager şablonu hello ağ güvenlik grubu üzerinden trafik tooflow tooit API Yönetimi'nden izin vererek açılan dinamik olarak hello uygulama bağlantı noktası aralığı, Service Fabric toospecify sağlar.
 
 6. F5 tuşuna basarak Visual Studio tooverify hello Web API'de yerel olarak kullanılabilir. 

    Service Fabric Explorer'ı açın ve ASP.NET Core toosee hello taban adresi hello hizmeti dinlediği hello belirli örneği tooa detaya. Ekleme `/api/values` toohello temel adresi ve bir tarayıcıda açın. Merhaba hello ValuesController hello Web API şablonunda Get yöntemini çağırır. İki dizeyi içeren bir JSON dizisi hello şablon tarafından sağlanan hello varsayılan yanıt verir:

    ```json
    ["value1", "value2"]`
    ```

    Bu, Azure API Management'te aracılığıyla kullanıma hello uç noktadır.

 7. Son olarak, azure'da hello uygulama tooyour küme dağıtın. [Visual Studio kullanarak](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), hello uygulama projesine sağ tıklatın ve **Yayımla**. Küme uç noktası sağlayın (örneğin, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello uygulama tooyour Service Fabric kümesi Azure'da.

Adlı bir ASP.NET Core durum bilgisiz hizmeti `fabric:/ApiApplication/WebApiService` artık Azure Service Fabric kümenizdeki çalıştırması gerekir.

## <a name="create-an-api-operation"></a>Bir API işlem oluşturma

Hazır toocreate API Management bir işlem ki artık, dış istemcilere kullanım toocommunicate ile Merhaba Service Fabric kümede çalışan ASP.NET Core durum bilgisiz hizmeti hello.

 1. Toohello Azure portalında oturum açın ve tooyour API Management hizmet dağıtımı gidin.
 2. Merhaba API Management hizmeti dikey penceresinde, seçin **API'leri - Önizleme**
 3. Merhaba tıklatarak yeni bir API eklemek **boş API** kutusu ve hello iletişim kutusunu doldurma:

     - **Web hizmeti URL'si**: Service Fabric arka uçlarını için değil Bu URL değeri kullanılır. Herhangi bir değer buraya koyabilirsiniz. Bu öğretici için kullanın: `http://servicefabric`.
     - **Ad**: API'nizi için herhangi bir ad sağlayın. Bu öğretici için kullanmak `Service Fabric App`.
     - **URL şeması**: HTTP, HTTPS ya da her ikisini de seçin. Bu öğretici için kullanmak `both`.
     - **API'si URL soneki**: bir sonek için bizim API sağlar. Bu öğretici için kullanmak `myapp`.
 
 4. Merhaba API oluşturulduktan sonra tıklatın **+ ekleme işlemi** tooadd bir ön uç API işlemi. Merhaba değerlere doldurun:
    
     - **URL**: seçin `GET` ve API hello için bir URL yolu sağlayın. Bu öğretici için kullanmak `/api/values`.
     
       Varsayılan olarak, hello URL yolu toohello arka uç Service Fabric hizmeti gönderilen hello URL yolu burada belirtilen. Merhaba kullanırsanız, hizmetiniz kullanır, bu durumda aynı URL yolunu Buraya `/api/values`, sonra hello işlemi daha fazla değişiklik yapılmadan çalışır. Bu durumda, gerek toospecify bir yolu yeniden yazma işlemi ilkenizde daha sonra kazandırır hello URL yolu, arka uç Service Fabric hizmeti tarafından kullanılan farklı bir URL yolu buraya de belirtebilir.
     - **Görünen ad**: hello API için herhangi bir ad sağlayın. Bu öğretici için kullanmak `Values`.

## <a name="configure-a-backend-policy"></a>Arka uç ilkesini yapılandırma

Merhaba arka uç ilke her şeyi birbirine bağlar. Merhaba arka uç hizmeti toowhich istekleri yönlendirilir Service Fabric yapılandırdığınız budur. Bu ilke tooany API işlemi uygulayabilirsiniz. Merhaba [Service Fabric için arka uç yapılandırması](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) hello aşağıdaki isteği yönlendirme denetimleri sağlar: 
 - Hizmet örneği seçimi ya da sabit kodlanmış bir Service Fabric hizmeti örnek adı belirterek (örneğin, `"fabric:/myapp/myservice"`) veya hello HTTP isteğinden oluşturulan (örneğin, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).
 - Tüm Service Fabric bölümleme düzenini kullanarak bir bölüm anahtarı oluşturma tarafından bölüm çözünürlüğü.
 - Durum bilgisi olan hizmetler için çoğaltma seçimi.
 - Çözümleme için bir hizmet konumu yeniden çözümlemeyi ve isteği yeniden göndermeyi toospecify hello koşulları izin koşulları yeniden deneyin.

Bu öğretici için yollar isteklerinin doğrudan toohello daha önce dağıtılan durum bilgisiz hizmet ASP.NET Core bir arka uç ilkesi oluşturun:

 1. Seçme ve düzenleme hello **gelen ilkeleri** hello için `Values` hello Düzenle simgesine tıklayarak ve ardından seçerek işlemi **kod görünümü**.
 2. Hello İlkesi Kod düzenleyicisinde ekleyin bir `set-backend-service` ilkesi altında aşağıda gösterildiği gibi ilkeleri gelen ve hello tıklatın **kaydetmek** düğmesi:
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

Service Fabric arka uç İlkesi özniteliklerini tam kümesi için toohello başvuran [API Management arka uç belgeleri](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>Merhaba API tooa ürün ekleyin. 

Merhaba API aramadan önce burada erişim toousers verebilirsiniz tooa ürün eklenmesi gerekir. 

 1. Hello API Management hizmeti, seçin **ürünler - Önizleme**.
 2. Varsayılan olarak, API Management sağlayıcıları iki ürünler: Starter ve sınırsız. Merhaba sınırsız ürün seçin.
 3. API seçin.
 4. Merhaba tıklatın **+ Ekle** düğmesi.
 5. Select hello `Service Fabric App` hello önceki adımlarda oluşturduğunuz ve hello tıklatın API **seçin** düğmesi.

### <a name="test-it"></a>test

Şimdi doğrudan hello Azure Portalı ' Service Fabric API Management ile bir istek tooyour arka uç hizmeti gönderme deneyin.

 1. Hello API Management hizmeti, seçin **API - Önizleme**.
 2. Merhaba, `Service Fabric App` hello önceki adımlarda oluşturduğunuz API seçin hello **Test** sekmesi.
 3. Merhaba tıklatın **Gönder** düğmesini toosend bir test isteği toohello arka uç hizmeti.

## <a name="next-steps"></a>Sonraki adımlar

Bu noktada, Service Fabric ve API Management temel bir kurulumu olması gerekir.

Bu öğretici, hızlı bir şekilde ayarlamak, Service Fabric kümesi tooget için temel kullanıcı sertifika tabanlı kimlik doğrulaması kullanır. Service Fabric kümesi için daha gelişmiş kullanıcı kimlik doğrulaması ile tercih [Azure Active Directory kimlik doğrulaması](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication). 

Ardından, [oluşturma ve Gelişmiş Ürün ayarları Azure API Management'te yapılandırma](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare uygulamanızı gerçek dünya trafiği için.

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
