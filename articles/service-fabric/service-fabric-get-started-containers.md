---
title: "Azure Service Fabric kapsayıcı uygulamanın aaaCreate | Microsoft Docs"
description: "Azure Service Fabric üzerinde ilk Windows kapsayıcı uygulamanızı oluşturun.  Python uygulama Docker görüntüsüyle, hello görüntü tooa kapsayıcı kayıt defteri itme, yapı ve Service Fabric kapsayıcı uygulaması dağıtacak."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Windows üzerinde ilk Service Fabric kapsayıcı uygulamanızı oluşturma
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Varolan bir uygulama bir Windows kapsayıcısında Service Fabric kümesi üzerinde çalışan herhangi bir değişiklik tooyour uygulama gerektirmez. Bu makalede, bir Python içeren bir Docker görüntüsü oluşturmada size yol gösterilir [Flask](http://flask.pocoo.org/) web uygulama ve tooa Service Fabric kümesi dağıtma.  Ayrıca, kapsayıcıya alınmış uygulamanızı [Azure Container Registry](/azure/container-registry/) aracılığıyla paylaşırsınız.  Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar. Okuma hello tarafından Docker hakkında bilgi edinebilirsiniz [Docker genel bakış](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Ön koşullar
Şunları çalıştıran bir geliştirme bilgisayarı:
* Visual Studio 2015 veya Visual Studio 2017.
* [Service Fabric SDK’sı ve araçları](service-fabric-get-started.md).
*  Windows için Docker.  [Windows için Docker CE edinme (dengeli)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description). Yükleme ve Docker, başlangıç hello Tepsi simgesi üzerinde sağ tıklayıp sonra **geçiş tooWindows kapsayıcıları**. Windows tabanlı gerekli toorun Docker görüntüleri budur.

Kapsayıcı içeren Windows Server 2016 üzerinde üç veya daha fazla düğüme sahip bir Windows kümesi - [Küme oluşturun](service-fabric-cluster-creation-via-portal.md) veya [Service Fabric’i ücretsiz deneyin](https://aka.ms/tryservicefabric).

Azure Container Registry’deki bir kayıt defteri - Azure aboneliğinizde [Kapsayıcı kayıt defteri oluşturun](../container-registry/container-registry-get-started-portal.md).

## <a name="define-hello-docker-container"></a>Merhaba Docker kapsayıcısı tanımlayın
Bir resim üzerinde Hello tabanlı derleme [Python görüntü](https://hub.docker.com/_/python/) Docker hub'ına bulunur.

Docker kapsayıcınızı bir Dockerfile içinde tanımlayın. Merhaba Dockerfile, kapsayıcı içinde hello ortamı kurma, toorun istediğiniz hello uygulamasını yükleme ve bağlantı noktası eşleme için yönergeler içerir. Merhaba Dockerfile olan hello giriş toohello `docker build` hello görüntüsünü oluşturur komutu.

Boş bir dizin oluşturun ve hello dosyası oluşturma *Dockerfile* (hiçbir dosya uzantılı). Çok Hello ekleyin*Dockerfile* ve değişikliklerinizi kaydedin:

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
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

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>Merhaba yansıması oluştur
Merhaba çalıştırmak `docker build` web uygulamanızı çalıştıran komutu toocreate hello görüntüsü. Bir PowerShell penceresi açın ve hello Dockerfile içeren toohello dizinine gidin. Merhaba aşağıdaki komutu çalıştırın:

```
docker build -t helloworldapp .
```

Bu komut derlemeleri Merhaba, Dockerfile içinde hello yönergeleri kullanarak yeni görüntüsü adlandırma (-t etiketleme) hello görüntü "helloworldapp". Bir görüntü oluşturma hello temel görüntü Docker hub'dan çeker ve uygulamanızı hello temel görüntü üstünde ekler yeni bir görüntü oluşturur.  

Merhaba yapı komutu tamamlandığında hello çalıştırmak `docker images` komutu hello yeni görüntüsü toosee bilgi:

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>Merhaba uygulama yerel olarak çalıştırma
Görüntünüzü onu hello kapsayıcı kayıt defteri yerel olarak göndermeden önce doğrulayın.  

Merhaba uygulamayı çalıştırın:

```
docker run -d --name my-web-site helloworldapp
```

*ad* kapsayıcı (yerine hello kapsayıcı kimliği) çalıştıran bir ad toohello sağlar.

Merhaba kapsayıcı başladıktan sonra kapsayıcı bir tarayıcıdan çalıştıran tooyour bağlanabilmesi IP adresini bulun:
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

Kapsayıcı çalıştıran toohello bağlayın.  Toohello IP adresi döndürdü, örneğin "http://172.31.194.61" işaret eden bir web tarayıcısı açın. "Hello World!" Başlık hello görmeniz gerekir Merhaba tarayıcıda görüntüleyin.

toostop çalıştırmak, kapsayıcı:

```
docker stop my-web-site
```

Merhaba kapsayıcı geliştirme makinenizden Sil:

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>Anında iletme hello görüntü toohello kapsayıcı kayıt defteri
Geliştirme makinenizde bu hello kapsayıcı çalıştıran doğruladıktan sonra Azure kapsayıcı kayıt defterinde hello görüntü tooyour kayıt defteri iletin.

Çalıştırma ``docker login`` ile tooyour kapsayıcı defterinde toolog, [kayıt defteri kimlik](../container-registry/container-registry-authentication.md).

Merhaba aşağıdaki örnek hello kimliği ve parolası bir Azure Active Directory geçirir [hizmet sorumlusu](../active-directory/active-directory-application-objects.md). Örneğin, bir hizmet asıl tooyour kayıt defteri bir Otomasyon senaryosu için atanmış. İsterseniz, kayıt defteri kullanıcı kimliğiniz ve parolanızı kullanarak oturum açabilirsiniz.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Merhaba aşağıdaki komutu bir etiket veya hello görüntünün diğer tam nitelenmiş bir yol tooyour kayıt defteri ile oluşturur. Yerler hello hello görüntüde Bu örnek ```samples``` hello kayıt defteri hello kök ad alanı tooavoid dağınıklığı.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Merhaba görüntü tooyour kapsayıcı kayıt defteri gönderin:

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Visual Studio'da kapsayıcılı hello hizmet oluşturma
Merhaba Service Fabric SDK ve araçları bir hizmet şablonu toohelp sağlamak kapsayıcılı bir uygulaması oluşturun.

1. Visual Studio’yu çalıştırın.  **Dosya** > **Yeni** > **Proje**’yi seçin.
2. **Service Fabric uygulaması**’nı seçin, "MyFirstContainer" olarak adlandırın ve **Tamam**’a tıklayın.
3. Seçin **Konuk kapsayıcı** hello listesinden **hizmet şablonları**.
4. İçinde **görüntü adı** "myregistry.azurecr.io/samples/helloworldapp", tooyour kapsayıcı deposu gönderilen hello görüntü girin.
5. Hizmetinize bir ad verin ve **Tamam**’a tıklayın.

## <a name="configure-communication"></a>İletişimi yapılandırma
Kapsayıcılı hello hizmet iletişimi için bir uç nokta gerekir. Ekleme bir `Endpoint` hello protokolü, bağlantı noktası ve türü toohello ServiceManifest.xml dosyasını öğe. Bu makalede, kapsayıcılı hello hizmet 8081 bağlantı noktasını dinler.  Bu örnekte, 8081 numaralı sabit bağlantı noktası kullanılır.  Bağlantı noktası belirtilmediyse, bir rastgele bağlantı noktası hello uygulama bağlantı noktası aralığından seçilir.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

Bir uç nokta tanımlayarak, Service Fabric hello uç nokta toohello adlandırma hizmeti yayımlar.  Merhaba kümede çalışan diğer hizmetler bu kapsayıcı çözebilirsiniz.  Kapsayıcıya iletişimi hello kullanarak da gerçekleştirebilirsiniz [ters proxy](service-fabric-reverseproxy.md).  İletişim hello ters proxy HTTP dinleme bağlantı noktası ve ortam değişkenleri olarak toocommunicate ile istediğiniz hello Hizmetleri hello adını sağlayarak gerçekleştirilir.

## <a name="configure-and-set-environment-variables"></a>Ortam değişkenlerini yapılandırma ve ayarlama
Ortam değişkenleri, her kod paketi hello hizmet bildiriminde için belirtilebilir. Bu özellik, kapsayıcı olarak mı dağıtıldıklarına yoksa konuk yürütülebilir dosyası olarak mı işlendiklerine bakılmaksızın tüm hizmetlerde sağlanır. Merhaba uygulaması değerleri bildirim veya onları uygulama parametreleri olarak dağıtımı sırasında belirttiğiniz ortam değişkeni geçersiz kılabilirsiniz.

Merhaba aşağıdaki hizmet bildirim XML parçacığını gösterir nasıl bir örneği için bir kod paketi toospecify ortam değişkenleri:
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Bu ortam değişkenleri hello uygulama bildiriminde geçersiz kılınabilir:

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>Kapsayıcı bağlantı noktasından konak bağlantı noktasına eşlemeyi ve kapsayıcıdan kapsayıcıya keşfi yapılandırma
Bir ana bilgisayar kullanılan bağlantı noktası toocommunicate hello kapsayıcı ile yapılandırın. üzerinde hangi hello hello kapsayıcı tooa bağlantı hello konaktaki içinde hizmet dinliyor hello bağlantı noktası başlangıç bağlantı noktası bağlamasına eşler. Ekleme bir `PortBinding` öğesinde `ContainerHostPolicies` hello ApplicationManifest.xml dosyasının öğesi.  Bu makale için `ContainerPort` 80'dir (Merhaba kapsayıcı sunan bağlantı noktası 80, belirtilen hello Dockerfile) ve `EndpointRef` "Guest1TypeEndpoint" olan (Merhaba hizmet bildiriminde önceden tanımlanmış uç nokta hello).  Gelen istekleri toohello hizmet bağlantı noktası 8081 tooport 80 hello kapsayıcısı üzerinde eşlenmiş.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>Kapsayıcı kayıt defteri kimlik doğrulamasını yapılandırma
Kapsayıcı kayıt defteri kimlik doğrulaması ekleyerek yapılandırma `RepositoryCredentials` çok`ContainerHostPolicies` hello ApplicationManifest.xml dosyasının. Merhaba hizmet toodownload hello kapsayıcı resmi hello depodan verir hello myregistry.azurecr.io kapsayıcı kayıt için Hello hesabı ve parolası ekleyin.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

Merhaba küme düğümlerinin tooall dağıtmış olan bir şifreleme sertifikası kullanarak hello deposu parolayı şifrelemek öneririz. Service Fabric hello hizmet paketi toohello küme dağıtırken hello şifreleme kullanılan toodecrypt hello şifreli metin sertifikasıdır.  Merhaba Invoke-ServiceFabricEncryptText cmdlet'i kullanılan toocreate hello şifre toohello ApplicationManifest.xml dosya ekleninceye hello parolası metindir.

Merhaba aşağıdaki betiği yeni kendinden imzalı bir sertifika oluşturur ve bunu tooa PFX dosyası aktarır.  Merhaba sertifika olan bir anahtar kasası aktarılır ve ardından toohello Service Fabric kümesi dağıtılır.

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
Hello kullanarak hello parolayı şifrelemek [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet'i.

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Hello tarafından döndürülen hello şifreli metin Hello parola yerine [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet'i ve `PasswordEncrypted` çok "true".

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a>Yalıtım modunu yapılandırma
Windows, kapsayıcılar için iki yalıtım modunu destekler: İşlem ve Hyper-V. Merhaba işlem yalıtım moduyla üzerinde çalışan tüm Merhaba kapsayıcılara aynı ana bilgisayar makine paylaşımı hello çekirdek hello ana bilgisayarla hello. Merhaba Hyper-V yalıtım moduyla hello tekrar her Hyper-V kapsayıcı ve hello kapsayıcı konak arasında yalıtılır. Merhaba yalıtım modunu hello belirtilen `ContainerHostPolicies` hello uygulama bildirim dosyasının öğesinde. belirtilebilir hello yalıtım modlar `process`, `hyperv`, ve `default`. Merhaba varsayılan yalıtım modunu Varsayılanları çok`process` Windows Server'da barındıran ve çok varsayılanlarını`hyperv` Windows 10 konaklarda. Merhaba aşağıdaki kod parçacığında hello uygulama bildirim dosyasında belirtilen hello yalıtım modu nasıl gösterir.

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>Kaynak idaresini yapılandırma
[Kaynak İdaresi](service-fabric-resource-governance.md) kapsayıcı hello kaynakları hello konakta kullanabileceğiniz hello kısıtlar. Merhaba `ResourceGovernancePolicy` hello uygulama bildiriminde belirtilen öğesi olan bir hizmet kod paketi için kullanılan toodeclare kaynak sınırları. Kaynak sınırları kaynakları aşağıdaki Merhaba ayarlanabilir: bellek, MemorySwap, CpuShares (CPU göreli ağırlık), MemoryReservationInMB, BlkioWeight (BlockIO göreli ağırlık).  Bu örnekte, hizmet paketi Guest1Pkg nereye yerleştirileceğini hello küme düğümlerinde bir temel alır.  Sınırlı too1024 hello kod paketi olacak şekilde bellek sınırları absolute MB bellek (ve aynı hello yumuşak garantisi rezervasyonu). Kod paketler (kapsayıcıları veya işlemler) Bu sınır ve toodo çalışırken daha fazla bellek böylece bir bellek yetersiz özel durum sonuçları mümkün tooallocate yok. Kaynak sınırı zorlaması toowork için bir hizmet paketi içindeki tüm kod paketleri belirtilen bellek sınırlarını olması gerekir.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>Merhaba kapsayıcı uygulaması dağıtma
Yaptığınız değişiklikleri kaydedin ve başlangıç uygulaması oluşturma. toopublish sağ tıklatın, uygulamanızın **MyFirstContainer** Çözüm Gezgini'nde ve select **Yayımla**.

İçinde **bağlantı uç noktasının**, hello küme için hello yönetim uç noktası girin.  Örneğin, "containercluster.westus2.cloudapp.azure.com:19000". Merhaba istemci bağlantısı bulabilirsiniz hello genel bakış dikey penceresinde hello kümenizdeki için uç nokta [Azure portal](https://portal.azure.com).

**Yayımla**’ta tıklayın.

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), bir Service Fabric kümesindeki uygulama ve düğümleri inceleyip yönetmeye yönelik web tabanlı bir araçtır. Bir tarayıcı açın ve toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/gidin ve hello uygulama dağıtımını izleyin.  Hello uygulama dağıtır fakat hello görüntü (hangi hello görüntü boyutu bağlı olarak biraz zaman alabilir) hello küme düğümlerinde indirilene kadar bir hata durumunda iken: ![hata][1]

Merhaba uygulamasıdır hazır olduğunda ```Ready``` durumu: ![hazır][2]

Bir tarayıcı açın ve toohttp://containercluster.westus2.cloudapp.azure.com:8081 gidin. "Hello World!" Başlık hello görmeniz gerekir Merhaba tarayıcıda görüntüleyin.

## <a name="clean-up"></a>Temizleme
Merhaba küme çalışırken tooincur ücretleri devam, göz önünde bulundurun [kümenizi silme](service-fabric-get-started-azure-cluster.md#remove-the-cluster).  [Taraf kümeleri](http://tryazureservicefabric.westus.cloudapp.azure.com/) birkaç saat sonra otomatik olarak silinir.

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
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

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

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
