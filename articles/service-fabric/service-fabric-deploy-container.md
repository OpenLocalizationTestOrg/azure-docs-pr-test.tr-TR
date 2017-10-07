---
title: "aaaService doku ve kapsayıcıları dağıtma | Microsoft Docs"
description: "Service Fabric ve Merhaba kapsayıcılara toodeploy mikro hizmet uygulamaları kullanın. Bu makale, Service Fabric kapsayıcıları ve nasıl toodeploy Windows kapsayıcı görüntü bir kümede sağlar hello özellikleri açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a>Bir Windows kapsayıcı tooService doku dağıtma
> [!div class="op_single_selector"]
> * [Windows kapsayıcı dağıtma](service-fabric-deploy-container.md)
> * [Docker kapsayıcısı dağıtma](service-fabric-deploy-container-linux.md)
> 
> 

Bu makalede Windows kapsayıcılarında kapsayıcılı Hizmetleri oluşturmanın hello işlemiyle anlatılmaktadır.

Service Fabric oluşan mikro kapsayıcılarda çalışan uygulamaları oluşturmaya yardımcı çeşitli özellikleri vardır. 

Merhaba özellikleri şunlardır:

* Kapsayıcı görüntü dağıtımı ve etkinleştirme
* Kaynak İdaresi
* Depo kimlik doğrulaması
* Kapsayıcı bağlantı noktası ana bilgisayar bağlantı noktası eşleme
* Kapsayıcıya bulma ve iletişim
* Özelliği tooconfigure ve ortam değişkenlerini ayarlama

Uygulamanıza dahil kapsayıcılı hizmet toobe paketleme zaman özelliklerin her biri işleyişi konumundaki bakalım.

## <a name="package-a-windows-container"></a>Paket bir Windows kapsayıcı
Bir kapsayıcı paketini oluşturduğunuzda, bir ya da Visual Studio Proje şablonu toouse seçebilirsiniz veya [hello uygulama paketini el ile oluşturmak](#manually).  Kullandığınızda, Visual Studio, hello uygulama paketi yapısı ve bildirim dosyası hello yeni proje şablonu tarafından sizin için oluşturulur.

> [!TIP]
> Merhaba en kolay yolu toopackage var olan bir kapsayıcı görüntüsünü bir hizmete toouse Visual Studio ' dir.

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>Visual Studio toopackage var olan bir kapsayıcı görüntüsünü kullanın
Visual Studio Service Fabric hizmet şablonu toohelp bir kapsayıcı tooa Service Fabric kümesi dağıtma sağlar.

1. Seçin **dosya** > **yeni proje**ve bir Service Fabric uygulaması oluşturun.
2. Seçin **Konuk kapsayıcı** hello hizmet şablonu olarak.
3. Seçin **görüntü adı** ve kapsayıcı deponuzun hello yolu toohello resmi belirtin. Örneğin, `myrepo/myimage:v1` https://hub.docker.com içinde
4. Hizmetinize bir ad verin ve **Tamam**’a tıklayın.
5. Kapsayıcılı hizmetinizi iletişim için bir uç nokta gerekiyorsa, artık hello protokolü, bağlantı noktası ve türü toohello ServiceManifest.xml dosya ekleyebilirsiniz. Örneğin: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Merhaba sağlayarak `UriScheme`, Service Fabric otomatik olarak kaydeder hello kapsayıcı uç nokta hello bulunabilirlik için adlandırma hizmeti ile. başlangıç bağlantı noktası (örnek önceki hello gösterildiği gibi) sabit veya dinamik olarak ayrılan. Bir bağlantı noktası belirtmezseniz, (hizmet olacağını gibi) hello uygulama bağlantı noktası aralığından dinamik ayrılır.
    Ayrıca belirterek tooconfigure hello kapsayıcı toohost bağlantı noktası eşlemesi gerekir bir `PortBinding` hello uygulama bildiriminde ilkesi. Daha fazla bilgi için bkz: [kapsayıcı toohost bağlantı noktası eşlemesi yapılandırma](#Portsection).
6. Kapsayıcı kaynak İdaresi gereken ardından ekleyin, bir `ResourceGovernancePolicy`.
8. Ardından, kapsayıcı bir özel deposu ile tooauthenticate gerekirse, ekleyin `RepositoryCredentials`.
7. Kapsayıcı desteği etkinleştirilmiş bir Windows Server 2016 makinede çalıştırılıyorsa hello paketini kullanmak ve eylem toodeploy tooyour yerel küme yayımlayın. 
8. Hazır olduğunuzda, yayımlama hello uygulama tooa uzaktan küme veya hello çözüm toosource denetiminde denetleyin. 

Bir örnek checkout hello [github'da Service Fabric kapsayıcı kod örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Windows Server 2016 küme oluşturma
toodeploy kapsayıcılı uygulamanız Windows Server 2016 kapsayıcı desteğiyle çalıştıran bir kümeye etkin toocreate gerekir. Kümenizi çalıştıran yerel olarak veya azure'da Azure Resource Manager aracılığıyla dağıtılan. 

toodeploy Azure Kaynak Yöneticisi'ni kullanarak bir küme seçin hello **Windows Server 2016 kapsayıcılarla** görüntü Azure seçeneği. Merhaba makalesine bakın [Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md). Azure Resource Manager ayarları aşağıdaki hello kullandığınızdan emin olun:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
Merhaba de kullanabilirsiniz [beş düğümü Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate bir küme. Alternatif olarak bir topluluk okuma [blog gönderisi](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) Service Fabric ve Windows kapsayıcıları kullanma.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>El ile paketini ve kapsayıcı görüntüsünü Dağıt
el ile kapsayıcılı hizmet paketleme hello işlemi aşağıdaki adımları hello üzerinde dayanır:

1. Merhaba kapsayıcılara tooyour depo yayımlayın.
2. Merhaba paket dizin yapısını oluşturun.
3. Merhaba hizmet bildirim dosyasını düzenleyin.
4. Merhaba uygulama bildirim dosyasının düzenleyin.

## <a name="deploy-and-activate-a-container-image"></a>Dağıtma ve kapsayıcı görüntü etkinleştirin
Merhaba Service Fabric içinde [uygulama modeli](service-fabric-application-model.md), hangi birden çok çoğaltmaları hizmete bir uygulama konağı bir kapsayıcıyı temsil eder. toodeploy ve etkinleştirme kapsayıcı, put hello adını hello kapsayıcı görüntüsüne bir `ContainerHost` hello hizmet bildirimi öğesinde.

Merhaba hizmet bildiriminde eklemek bir `ContainerHost` hello giriş noktası için. Ardından kümesi hello `ImageName` toobe hello adını hello kapsayıcı depo ve görüntü. Merhaba aşağıdaki kısmi bildirimi gösterir nasıl toodeploy hello kapsayıcı olarak adlandırılan bir örnek `myimage:v1` adlı bir depodan `myrepo`:

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

İsteğe bağlı komutları toorun hello kapsayıcısı hello altında başlatma belirtebilirsiniz `Commands` öğesi. Birden çok komutlarında virgülle-bunları sınırlar. 

## <a name="understand-resource-governance"></a>Kaynak İdaresi anlama
Kaynak İdaresi kapsayıcı hello hello kaynakları kısıtlayan hello kapsayıcı yeteneğini hello konakta kullanabilirsiniz ' dir. Merhaba `ResourceGovernancePolicy`, kendisi hello uygulama bildiriminde belirtilen bir hizmeti kod paketi için kullanılan toodeclare kaynak sınırları olduğu. Kaynak sınırları kaynakları aşağıdaki Merhaba ayarlanabilir:

* Bellek
* MemorySwap
* CpuShares (CPU göreli ağırlık)
* MemoryReservationInMB  
* BlkioWeight (BlockIO göreli ağırlık).

> [!NOTE]
> IOPS gibi belirli blok g/ç sınırları belirtmek için destek, okuma/yazma BPS ve diğerleri için gelecekteki bir sürüm planlanmaktadır.
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>Bir depo kimlik doğrulaması
bir kapsayıcı toodownload tooprovide oturum açma kimlik bilgileri toohello kapsayıcı deposu olabilir. Merhaba uygulama bildiriminde belirtilen hello oturum açma kimlik bilgileri, kullanılan toospecify hello oturum açma bilgileri veya hello kapsayıcı görüntü hello görüntü deposundan karşıdan yüklemek için SSH anahtarı, ' dir. Merhaba aşağıdaki örnekte gösterilir adlı bir hesap *TestUser* hello parola düz metin birlikte (*değil* önerilen):

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

Toohello makine dağıtmış olan bir sertifikayı kullanarak hello parolayı şifrelemek öneririz.

Merhaba aşağıdaki örnekte gösterilir adlı bir hesap *TestUser*, burada hello parola adı verilen bir sertifika kullanılarak şifrelenmiş *MyCert*. Merhaba kullanabilirsiniz `Invoke-ServiceFabricEncryptText` PowerShell komut toocreate hello gizli şifreli metin hello parolası. Daha fazla bilgi için hello makalesine bakın [Service Fabric uygulamaları parolalarında yönetme](service-fabric-application-secret-management.md).

Merhaba toodecrypt hello parola kullandı hello sertifikasının özel anahtarı yerel makinede bir bant dışı yöntem dağıtılan toohello olması gerekir. (Azure'da, Azure Resource Manager bu yöntem budur.) Ardından, Service Fabric hello hizmet paketi toohello makine dağıtırken hello gizli şifresini çözebilir. Merhaba gizli hello hesap adı ile birlikte kullanarak, onu hello kapsayıcı deposuyla sonra doğrulayabilir.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name ="Portsection"></a>Kapsayıcı toohost bağlantı noktası eşlemesi yapılandırın
Belirterek hello kapsayıcı ile bir ana bilgisayar kullanılan bağlantı noktası toocommunicate yapılandırabilirsiniz bir `PortBinding` hello uygulama bildiriminde. Merhaba kapsayıcı tooa bağlantı hello konaktaki içinde dinleyen bir Hello bağlantı noktası bağlama eşlemeleri hello bağlantı noktası toowhich hello hizmet.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>Kapsayıcıya bulma ve iletişim yapılandırın
Merhaba kullanabilirsiniz `PortBinding` öğesi toomap hello hizmet bildiriminde bir kapsayıcı bağlantı noktası tooan uç noktası. Uç noktası aşağıdaki örneğine hello hello `Endpoint1` 8905 sabit bir bağlantı noktasını belirtir. Rastgele bir bağlantı noktası hello kümenin uygulama bağlantı noktası aralığından sizin için bu durumda seçilen bağlantı noktası yok hiç da belirtebilir.


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
Bir uç nokta belirtirseniz, hello kullanarak `Endpoint` hello hizmet bildirimi Konuk kapsayıcı, Service Fabric etiketinde otomatik olarak bu uç nokta toohello adlandırma hizmeti yayımlama. Merhaba kümede çalışan diğer hizmetler, böylece çözümlemek için hello REST sorgularını kullanarak bu kapsayıcı bulabilir.

Merhaba Naming service ile kaydederek-kapsayıcıya iletişimi kapsayıcı içinde hello kullanarak gerçekleştirebileceğiniz [ters proxy](service-fabric-reverseproxy.md). İletişim hello ters proxy http dinleme bağlantı noktası ve ortam değişkenleri olarak toocommunicate ile istediğiniz hello Hizmetleri hello adını sağlayarak gerçekleştirilir. Daha fazla bilgi için hello sonraki bölüme bakın. 

## <a name="configure-and-set-environment-variables"></a>Ortam değişkenlerini yapılandırma ve ayarlama
Ortam değişkenleri, her kod paketi hello hizmet bildiriminde için belirtilebilir. Bu özellik, kapsayıcı olarak mı dağıtıldıklarına yoksa konuk yürütülebilir dosyası olarak mı işlendiklerine bakılmaksızın tüm hizmetlerde sağlanır. Merhaba uygulaması değerleri bildirim veya onları uygulama parametreleri olarak dağıtımı sırasında belirttiğiniz ortam değişkeni geçersiz kılabilirsiniz.

Merhaba aşağıdaki hizmet bildirim XML parçacığını gösterir nasıl bir örneği için bir kod paketi toospecify ortam değişkenleri:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

Bu ortam değişkenleri hello uygulama bildirim düzeyinde geçersiz kılınabilir:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

Merhaba önceki örnekte, biz hello için açık bir değer belirtilen `HttpGateway` ortam değişkeni (Merhaba değeri ayarlarız sırada 19000) `BackendServiceName` hello parametresi `[BackendSvc]` uygulama parametresi. Bu ayarlar için toospecify hello değer etkinleştirmek `BackendServiceName`değer hello uygulamayı dağıttıktan sonra hello bildiriminde sabit bir değere sahip değil.

## <a name="configure-isolation-mode"></a>Yalıtım modunu yapılandırma

Windows için kapsayıcı - işlem ve Hyper-V iki yalıtım modunu destekler.  Merhaba işlem yalıtım moduyla üzerinde çalışan tüm Merhaba kapsayıcılara aynı ana bilgisayar makine paylaşımı hello çekirdek hello ana bilgisayarla hello. Merhaba Hyper-V yalıtım moduyla hello tekrar her Hyper-V kapsayıcı ve hello kapsayıcı konak arasında yalıtılır. Merhaba yalıtım modunu hello belirtilen `ContainerHostPolicies` hello uygulama bildirim dosyasının etiketinde.  belirtilebilir hello yalıtım modlar `process`, `hyperv`, ve `default`. Merhaba `default` yalıtım modunu Varsayılanları çok`process` Windows Server'da barındıran ve çok varsayılanlarını`hyperv` Windows 10 konaklarda.  Merhaba aşağıdaki kod parçacığında hello uygulama bildirim dosyasında belirtilen hello yalıtım modu nasıl gösterir.

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a>Uygulama ve hizmet bildirimi için örnekler tamamlayın

Bir örnek uygulama bildirimi aşağıdaki gibidir:

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

Bir örnek hizmet bildirimi (uygulama bildirimi önceki hello belirtilen) aşağıdaki gibidir:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>Sonraki adımlar
Kapsayıcılı hizmetini dağıttıysanız, bilgi nasıl toomanage okuyarak kendi ömrü [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).

* [Service Fabric ve kapsayıcıları genel bakış](service-fabric-containers-overview.md)
* Bir örnek checkout [github'da Service Fabric kapsayıcı kod örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
