---
title: "Azure Service Fabric kapsayıcı uygulamanın Linux'ta aaaCreate | Microsoft Docs"
description: "Azure Service Fabric üzerinde ilk Linux kapsayıcı uygulamanızı oluşturun.  Uygulamanızı Docker görüntüsüyle, hello görüntü tooa kapsayıcı kayıt defteri itme, yapı ve Service Fabric kapsayıcı uygulaması dağıtacak."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>Linux üzerinde ilk Service Fabric kapsayıcı uygulamanızı oluşturma
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Varolan bir uygulama bir Linux kapsayıcısında Service Fabric kümesi üzerinde çalışan herhangi bir değişiklik tooyour uygulama gerektirmez. Bu makalede, bir Python içeren bir Docker görüntüsü oluşturmada size yol gösterilir [Flask](http://flask.pocoo.org/) web uygulama ve tooa Service Fabric kümesi dağıtma.  Ayrıca, kapsayıcıya alınmış uygulamanızı [Azure Container Registry](/azure/container-registry/) aracılığıyla paylaşırsınız.  Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar. Okuma hello tarafından Docker hakkında bilgi edinebilirsiniz [Docker genel bakış](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Ön koşullar
* Şunları çalıştıran bir geliştirme bilgisayarı:
  * [Service Fabric SDK’sı ve araçları](service-fabric-get-started-linux.md).
  * [Linux için Docker CE](https://docs.docker.com/engine/installation/#prior-releases). 
  * [Service Fabric CLI](service-fabric-cli.md)

* Azure Container Registry’deki bir kayıt defteri - Azure aboneliğinizde [Kapsayıcı kayıt defteri oluşturun](../container-registry/container-registry-get-started-portal.md). 

## <a name="define-hello-docker-container"></a>Merhaba Docker kapsayıcısı tanımlayın
Bir resim üzerinde Hello tabanlı derleme [Python görüntü](https://hub.docker.com/_/python/) Docker hub'ına bulunur. 

Docker kapsayıcınızı bir Dockerfile içinde tanımlayın. Merhaba Dockerfile, kapsayıcı içinde hello ortamı kurma, toorun istediğiniz hello uygulamasını yükleme ve bağlantı noktası eşleme için yönergeler içerir. Merhaba Dockerfile olan hello giriş toohello `docker build` hello görüntüsünü oluşturur komutu. 

Boş bir dizin oluşturun ve hello dosyası oluşturma *Dockerfile* (hiçbir dosya uzantılı). Çok Hello ekleyin*Dockerfile* ve değişikliklerinizi kaydedin:

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

Okuma hello [Dockerfile başvuru](https://docs.docker.com/engine/reference/builder/) daha fazla bilgi için.

## <a name="create-a-simple-web-application"></a>Basit web uygulaması oluşturma
Bağlantı noktası 80 üzerinden dinleyen ve "Merhaba Dünya!" başlığını döndüren bir Flask web uygulaması oluşturun.  Buna Merhaba aynı dizinde, hello dosyası oluşturma *requirements.txt*.  Merhaba aşağıdakileri ekleyin ve değişikliklerinizi kaydedin:
```
Flask
```

Merhaba oluşturabilir *app.py* dosya ve hello aşağıdakileri ekleyin:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a>Merhaba yansıması oluştur
Merhaba çalıştırmak `docker build` web uygulamanızı çalıştıran komutu toocreate hello görüntüsü. Bir PowerShell penceresi açın ve çok gidin*c:\temp\helloworldapp*. Merhaba aşağıdaki komutu çalıştırın:

```bash
docker build -t helloworldapp .
```

Bu komut derlemeleri Merhaba, Dockerfile içinde hello yönergeleri kullanarak yeni görüntüsü adlandırma (-t etiketleme) hello görüntü "helloworldapp". Bir görüntü oluşturma hello temel görüntü Docker hub'dan çeker ve uygulamanızı hello temel görüntü üstünde ekler yeni bir görüntü oluşturur.  

Merhaba yapı komutu tamamlandığında hello çalıştırmak `docker images` komutu hello yeni görüntüsü toosee bilgi:

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>Merhaba uygulama yerel olarak çalıştırma
Kapsayıcılı uygulamanız bu hello kapsayıcı kayıt defteri yerel olarak göndermeden önce çalıştığını doğrulayın.  

Merhaba uygulamayı çalıştırın, bilgisayarınızın 4000 numaralı bağlantı noktasını toohello kapsayıcının eşleme 80 kullanıma sunulan bağlantı noktası:

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*ad* kapsayıcı (yerine hello kapsayıcı kimliği) çalıştıran bir ad toohello sağlar.

Kapsayıcı çalıştıran toohello bağlayın.  Bağlantı 4000, örneğin "http://localhost:4000" döndürülen toohello IP adresini işaret eden bir web tarayıcısı açın. "Hello World!" Başlık hello görmeniz gerekir Merhaba tarayıcıda görüntüleyin.

![Merhaba Dünya!][hello-world]

toostop çalıştırmak, kapsayıcı:

```bash
docker stop my-web-site
```

Merhaba kapsayıcı geliştirme makinenizden Sil:

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>Anında iletme hello görüntü toohello kapsayıcı kayıt defteri
Merhaba uygulaması Docker içinde çalıştığını doğruladıktan sonra Azure kapsayıcı kayıt defterinde hello görüntü tooyour kayıt defteri iletin.

Çalıştırma `docker login` ile tooyour kapsayıcı defterinde toolog, [kayıt defteri kimlik](../container-registry/container-registry-authentication.md).

Merhaba aşağıdaki örnek hello kimliği ve parolası bir Azure Active Directory geçirir [hizmet sorumlusu](../active-directory/active-directory-application-objects.md). Örneğin, bir hizmet asıl tooyour kayıt defteri bir Otomasyon senaryosu için atanmış.  İsterseniz, kayıt defteri kullanıcı kimliğiniz ve parolanızı kullanarak oturum açabilirsiniz.

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Merhaba aşağıdaki komutu bir etiket veya hello görüntünün diğer tam nitelenmiş bir yol tooyour kayıt defteri ile oluşturur. Yerler hello hello görüntüde Bu örnek `samples` hello kayıt defteri hello kök ad alanı tooavoid dağınıklığı.

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Merhaba görüntü tooyour kapsayıcı kayıt defteri gönderin:

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>Paket hello Docker Yeoman görüntüsüyle
Merhaba Linux için Service Fabric SDK içerir bir [Yeoman](http://yeoman.io/) kolay toocreate kolaylaştırır Oluşturucu uygulamanız ve kapsayıcı görüntü ekleyin. Yeoman tek bir Docker kapsayıcısı uygulamayla adlı toocreate kullanalım *SimpleContainerApp*.

toocreate Service Fabric kapsayıcı uygulaması, bir terminal penceresi açın ve Çalıştır `yo azuresfcontainer`.  

Uygulamanızı adlandırın (örneğin, "mycontainer"). 

Bir kapsayıcı kayıt defterindeki hello kapsayıcı görüntüsü için Hello URL'si girin (örneğin, ""). 

Bu resimle bir iş yükü giriş tanımlanmış noktası, tooexplicitly belirtin giriş komutları (başlatma işleminden sonra çalışan hello kapsayıcı tutar hello kapsayıcı içinde çalıştırma komutları). 

"1" örnek sayısı belirtin.

![Kapsayıcılar için Service Fabric Yeoman oluşturucusu][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>Bağlantı noktası eşlemesini ve kapsayıcı deposu kimlik doğrulamasını yapılandırma
Kapsayıcı içinde alınmış hizmetinize iletişim için bir uç nokta gerekir.  Şimdi hello protokolü, bağlantı noktası ve tür ekleyin tooan `Endpoint` hello ServiceManifest.xml dosyasında. Bu makalede, kapsayıcılı hello hizmet 4000 bağlantı noktasını dinler: 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
Merhaba sağlama `UriScheme` otomatik olarak kapsayıcı uç nokta hello bulunabilirlik için Service Fabric adlandırma hizmeti ile hello kaydeder. Bir tam ServiceManifest.xml örnek dosya hello bu makalenin sonundaki sağlanır. 

Merhaba kapsayıcı bağlantı noktası ana bilgisayar bağlantı noktası eşleme belirterek yapılandırma bir `PortBinding` ilkesinde `ContainerHostPolicies` hello ApplicationManifest.xml dosyasının.  Bu makale için `ContainerPort` 80'dir (Merhaba kapsayıcı sunan bağlantı noktası 80, belirtilen hello Dockerfile) ve `EndpointRef` olan "myserviceTypeEndpoint" (Merhaba uç noktası hello hizmet bildiriminde tanımlanan).  Gelen istekleri toohello hizmet bağlantı noktası 4000 tooport 80 hello kapsayıcısı üzerinde eşlenmiş.  Ardından, kapsayıcı bir özel deposu ile tooauthenticate gerekirse, ekleyin `RepositoryCredentials`.  Bu makalede, hello hesap adı ve parola hello myregistry.azurecr.io kapsayıcı kayıt defteri ekleyin. 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>Derleme ve paket Merhaba Service Fabric uygulaması
Merhaba Service Fabric Yeoman şablonları içerir bir yapı komut dosyası için [Gradle](https://gradle.org/), hangi toobuild hello hello terminal uygulamasından kullanabilirsiniz. Merhaba aşağıdaki çalıştırma toobuild ve paket hello uygulaması:

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>Merhaba uygulaması dağıtma
Merhaba uygulama oluşturulduktan sonra toohello yerel küme hello Service Fabric CLI kullanarak dağıtabilirsiniz.

Toohello yerel Service Fabric kümesi bağlayın.

```bash
sfctl cluster select --endpoint http://localhost:19080
```

Kullanım hello hello şablonu toocopy Merhaba uygulaması toohello kümenin görüntü deposu paketini, hello uygulama türünü kaydetme ve hello uygulama örneğini oluşturmak sağlanan komut dosyası yükleyin.

```bash
./install.sh
```

Bir tarayıcı açın ve http://localhost: 19080/Explorer (Merhaba Vagrant Mac OS X kullanıyorsanız VM hello özel IP ile değiştir localhost) konumunda tooService Fabric Gezgini'ne gidin. Merhaba uygulamaları düğümünü genişletin ve şimdi uygulama türü için bir giriş ve hello bu türünün ilk örneği için başka bir yoktur.

Kapsayıcı çalıştıran toohello bağlayın.  Bağlantı 4000, örneğin "http://localhost:4000" döndürülen toohello IP adresini işaret eden bir web tarayıcısı açın. "Hello World!" Başlık hello görmeniz gerekir Merhaba tarayıcıda görüntüleyin.

![Merhaba Dünya!][hello-world]

## <a name="clean-up"></a>Temizleme
Merhaba kaldırma komut dosyası kullan hello şablon toodelete hello uygulama örneği hello yerel geliştirme kümeden sağlanan ve hello uygulama türü kaydını silin.

```bash
./uninstall.sh
```

Merhaba görüntü toohello kapsayıcı kayıt defteri itme sonra hello yerel görüntü Geliştirme bilgisayarınızdan silebilirsiniz:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Tam Service Fabric uygulaması ve hizmet bildirimleri örneği
Merhaba tüm hizmet ve bu makalede kullanılan uygulama bildirimleri aşağıda verilmiştir.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a>Daha fazla Hizmetleri tooan varolan uygulama ekleme

başka bir kapsayıcı hizmeti tooan uygulaması zaten yeoman, kullanılarak oluşturulan tooadd gerçekleştirmek hello adımları izleyin:

1. Merhaba var olan uygulamanın toohello kök dizini değiştirin.  Örneğin, `cd ~/YeomanSamples/MyApplication`, `MyApplication` Yeoman tarafından oluşturulan hello uygulamasıdır.
2. `yo azuresfcontainer:AddService` öğesini çalıştırın

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a>Kapsayıcı zorla sonlandırılmadan önceki zaman aralığını yapılandırın

Merhaba kapsayıcı Hello hizmet silme (veya bir taşıma tooanother düğümü) başlatıldıktan sonra kaldırılmadan önce hello çalışma zamanı toowait için bir zaman aralığı yapılandırabilirsiniz. Yapılandırma hello zaman aralığı gönderir hello `docker stop <time in seconds>` komutu toohello kapsayıcı.   Daha ayrıntılı bilgi için bkz. [docker durdurma](https://docs.docker.com/engine/reference/commandline/stop/). Merhaba zaman aralığı toowait hello altında belirtilen `Hosting` bölümü. Küme bildirimi parçacığını aşağıdaki hello nasıl tooset hello bekleme aralığı gösterir:

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
Merhaba varsayılan zaman aralığı ayarlanır too10 saniye. Bu yapılandırma dinamik olduğundan, bir yapılandırma yalnızca yükseltme hello küme güncelleştirmelerini hello zaman aşımı süresi. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Merhaba çalışma zamanı tooremove yapılandırma kullanılmayan kapsayıcı görüntüleri

Merhaba Service Fabric kümesi tooremove yapılandırabilirsiniz hello düğümünden kullanılmayan kapsayıcı görüntüler. Bu yapılandırma, disk alanı toobe hello düğüm üzerinde çok fazla sayıda kapsayıcı görüntüler varsa yeniden yakalanmadan sağlar.  tooenable bu özellik, güncelleştirme hello `Hosting` hello aşağıdaki kod parçacığında gösterildiği gibi hello küme bildiriminde bölümünde: 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

Silinmemelidir görüntüler için bunları altında hello belirtebilirsiniz `ContainerImagesToSkip` parametresi. 


## <a name="next-steps"></a>Sonraki adımlar
* [Service Fabric’te kapsayıcı](service-fabric-containers-overview.md) çalıştırma hakkında daha fazla bilgi edinin.
* Okuma hello [bir kapsayıcıda .NET uygulaması dağıtma](service-fabric-host-app-in-a-container.md) Öğreticisi.
* Service Fabric Hello hakkında bilgi edinin [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).
* Checkout hello [Service Fabric kapsayıcı kod örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers) github'da.

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
