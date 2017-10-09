---
title: "Linux üzerinde geliştirme ortamınızı aaaSet | Microsoft Docs"
description: "Merhaba çalışma zamanı ve SDK'sını yükleyin ve Linux üzerinde yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra hazır toobuild uygulamalar olur."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a>Linux üzerinde geliştirme ortamınızı hazırlama
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy çalıştırıp [Azure Service Fabric uygulamaları](service-fabric-application-model.md) hello çalışma zamanı ve ortak SDK Linux geliştirme makinenize yükleyin. Ayrıca isteğe bağlı Java ve .NET Core SDK’larını yükleyebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

işletim sistemi sürümleri aşağıdaki hello geliştirme için desteklenir:

* Ubuntu 16.04 (`Xenial Xerus`)

## <a name="update-your-apt-sources"></a>APT kaynaklarınızı güncelleştirme
tooinstall hello SDK ve hello ilişkili çalışma zamanı paketi üzerinden hello get apt komut satırı aracı, Gelişmiş paketleme Aracı (APT) kaynaklarınızı önce güncelleştirmeniz gerekir.

1. Bir terminal açın.
2. Merhaba Service Fabric depodaki tooyour kaynakları listeye ekleyin.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. Merhaba eklemek `dotnet` depodaki tooyour kaynakları listesi.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. Merhaba ekleme yeni Gnu gizlilik Guard (GnuPG veya GPG) tooyour APT keyring anahtar.

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. Merhaba resmi Docker GPG anahtar tooyour APT keyring ekleyin.

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. Merhaba Docker deposu ayarlama.

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. Paketinizi Yenile eklenen depoları hello üzerinde yeni göre listeler.

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>Yükleme ve hello SDK yerel Küme kurulumu için ayarlama

Kaynaklarınızın güncelleştirildikten sonra hello SDK yükleyebilirsiniz. Merhaba Service Fabric SDK paketini yükleyin, hello yükleme onaylayın ve toohello Lisans Sözleşmesi'ni kabul etmiş olursunuz.

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   Merhaba aşağıdaki komutları kabul hello lisans Service Fabric paketler için otomatikleştirin:
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>Yerel küme oluşturma
  Merhaba yükleme başarılı olursa, mümkün toostart yerel bir küme olmalıdır.

  1. Merhaba Küme kurulumu betiğini çalıştırın.

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. Bir web tarayıcısı açın ve çok Git[Service Fabric Explorer](http://localhost:19080/Explorer). Merhaba küme başlatılmış olup olmadığını hello Service Fabric Explorer Pano görmeniz gerekir.

      ![Linux üzerinde Service Fabric Explorer][sfx-linux]

  Bu noktada, önceden oluşturulmuş Service Fabric uygulama paketlerini ve yeni paketleri konuk kapsayıcılar veya konuk yürütülebilir öğelere göre dağıtabilirsiniz. Merhaba Java veya .NET Core SDK kullanarak toobuild yeni hizmetler, sonraki bölümlerde verilmiştir hello isteğe bağlı kurulum adımları izleyin.


  > [!NOTE]
  > Tek başına kümeler Linux’da desteklenmez. Merhaba Önizleme destekler yalnızca bir kutusunu ve Azure Linux çoklu makine kümeleri.
  >

## <a name="set-up-hello-service-fabric-cli"></a>Service Fabric CLI Hello ayarlayın

Merhaba [Service Fabric CLI](service-fabric-cli.md) kümeleri ve uygulamalar dahil olmak üzere Service Fabric varlıkları ile etkileşim için komut yok. Python üzerinde dayanır, bu nedenle toohave python ve PIP komutu aşağıdaki hello ile devam etmeden önce yüklü olduğundan emin olun:

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>Yükleme ve hello oluşturucuları kapsayıcıları ve Konuk yürütülebilir dosyalar için ayarlama
Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric uygulamaları oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar. Lütfen makinenizde çalışmak için hello Service Fabric yeoman şablon oluşturucu sahip tooensure hello adımları izleyin.

1. Makinenize nodejs ve NPM yükleme

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme

  ```bash
  sudo npm install -g yo
  ```
3. Merhaba Service Fabric Yeo kapsayıcı oluşturucu ve Konuk execuatble Oluşturucu NPM yükleme

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

Merhaba oluşturucuları yukarıda yükledikten sonra çalıştırarak Konuk çalıştırılabilir veya kapsayıcı Hizmetleri mümkün toocreate uygulamalarla olmalıdır `yo azuresfguest` veya `yo azuresfcontainer` sırasıyla.

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>Merhaba gerekli Java yapıları (isteğe bağlı, modelleri programlama toouse hello Java istiyorsanız) yükleyin

Java kullanarak toobuild Service Fabric Hizmetleri emin olun JDK derleme görevleri çalıştırmak için kullanılan Gradle ile birlikte yüklenen 1.8. Aşağıdaki kod parçacığında hello açık JDK 1.8 Gradle birlikte yükler. Merhaba Service Fabric Java kitaplıkları Maven alınır.

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>Merhaba Eclipse Neon eklentisini yükleyin (isteğe bağlı)

Hizmet yapıdan için hello içinde hello Eclipse eklenti yükleyebilirsiniz **Java geliştiricileri için Eclipse IDE**. Toplama tooService doku Java uygulamaları Eclipse toocreate Service Fabric Konuk yürütülebilir uygulamalar ve kapsayıcı uygulamaları kullanabilirsiniz.

1. Eclipse'te, en son Eclipse Neon olduğundan ve en son Buildship sürümü hello emin olun (1.0.17 veya sonraki bir sürümü) yüklü. Seçerek yüklü bileşenlerin hello sürümlerini kontrol edebilirsiniz **yardımcı** > **Yükleme ayrıntıları**. Merhaba yönergeleri kullanarak Buildship güncelleştirebilirsiniz [Eclipse Buildship: Eclipse için eklentilerini Gradle][buildship-update].

2. tooinstall hello Service Fabric eklentisini seçin **yardımcı** > **yeni yazılımı yükle**.

3. Merhaba, **çalışmak** kutusuna **http://dl.microsoft.com/eclipse**.

4. **Ekle**'ye tıklayın.

    ![Merhaba kullanılabilir yazılım sayfası][sf-eclipse-plugin]

5. Select hello **ServiceFabric** eklentisi ve ardından **sonraki**.

6. Merhaba yükleme adımlarını tamamlayın ve hello son kullanıcı lisans sözleşmesini kabul edin.

Hello Service Fabric yüklü Eclipse eklenti zaten varsa, hello en son sürümüne sahip olduğunuzdan emin olun. Seçerek kontrol **yardımcı** > **Yükleme ayrıntıları** ve ardından için Service Fabric hello listesinde arama yüklü eklentileri. Daha yeni bir sürüm varsa, **Güncelleştir**’i seçin.

Daha fazla bilgi için bkz. [Eclipse Java uygulama geliştirmesi için Service Fabric eklentisi](service-fabric-get-started-eclipse.md).


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>Merhaba .NET Core SDK (isteğe bağlı, toouse hello .NET Core programlama modelleri istiyorsanız) yükleyin
Merhaba .NET Core SDK hello kitaplıkları ve gerekli toobuild Service Fabric .NET Core hizmetleriyle şablonlar sağlar. Merhaba .NET Core SDK paketini çalışan hello aşağıdaki tarafından yükle-

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>Güncelleştirme hello SDK ve çalışma zamanı

tooupdate toohello ve en son sürümünü hello SDK çalışma zamanı, hello aşağıdaki komutları çalıştırın (istemediğiniz hello SDK'ları seçimini kaldırın):

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
tooupdate hello Java SDK'sı ikili Maven gelen tooupdate hello sürüm hello karşılık gelen ikili hello ayrıntılarını ihtiyacınız ``build.gradle`` dosya toopoint toohello en son sürümü. tam olarak tooupdate hello sürüm, ihtiyaç duyacağınız tooknow tooany başvurabilir ``build.gradle`` Service Fabric başlama örnekleri dosyasında [burada](https://github.com/Azure-Samples/service-fabric-java-getting-started).

> [!NOTE]
> Merhaba paketleri güncelleştiriliyor çalıştıran, yerel geliştirme küme toostop neden olabilir. Yerel kümenizdeki, bu sayfada hello yönergeleri izleyerek bir yükseltmeden sonra yeniden başlatın.

## <a name="next-steps"></a>Sonraki adımlar

* [Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-create-your-first-linux-application-with-java.md)
* [Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-get-started-eclipse.md)
* [Linux üzerinde ilk CSharp uygulamanızı oluşturma](service-fabric-create-your-first-linux-application-with-csharp.md)
* [OSX üzerinde geliştirme ortamınızı hazırlama](service-fabric-get-started-mac.md)
* [Merhaba Service Fabric CLI toomanage uygulamalarınızı kullanın](service-fabric-application-lifecycle-sfctl.md)
* [Service Fabric Windows/Linux farkları](service-fabric-linux-windows-differences.md)
* [Service Fabric CLI kullanmaya başlama](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
