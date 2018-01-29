---
title: "Azure Service Fabric ile çalışmak için Mac OS X’te geliştirme ortamınızı ayarlama | Microsoft Docs"
description: "Çalışma zamanını, SDK'yı ve araçları yükleyip yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra Mac OS X üzerinde uygulama derlemek için hazır hale gelirsiniz."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/17/2017
ms.author: saysa
ms.openlocfilehash: 328b2778a68e32d95b666124bf7bba969a5f52a6
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/18/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Mac OS X’te geliştirme ortamınızı ayarlama
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

Mac OS X kullanarak Linux kümelerinde çalışacak Service Fabric uygulamaları derleyebilirsiniz. Bu belgede Mac’inizi geliştirme için nasıl ayarlayacağınız ele alınmaktadır.

## <a name="prerequisites"></a>Ön koşullar
Service Fabric, OS X üzerinde yerel olarak çalışmaz. Yerel bir Service Fabric kümesini çalıştırmak için önceden yapılandırılmış bir Docker kapsayıcı görüntüsü sağlanır. Başlamadan önce şunlar gereklidir:

* En az 4 GB RAM.
* [Docker](https://www.docker.com/)'ın en son sürümü.
* Service Fabric [One-box Docker kapsayıcı görüntüsüne](https://hub.docker.com/r/servicefabricoss/service-fabric-onebox/) erişim.

>[!TIP]
>
>Docker’ı Mac bilgisayarınıza yüklemek için [Docker belgelerinde](https://docs.docker.com/docker-for-mac/install/#what-to-know-before-you-install) gösterilen adımları izleyebilirsiniz. Yükledikten sonra [yüklemenizi doğrulayın](https://docs.docker.com/docker-for-mac/#check-versions-of-docker-engine-compose-and-machine).
>

## <a name="create-a-local-container-and-set-up-service-fabric"></a>Yerel bir kapsayıcı oluşturma ve Service Fabric’i ayarlama
Yerel bir Docker kapsayıcısı ayarlamak ve üzerinde bir Service Fabric kümesi çalıştırmak için şu adımları uygulayın:

1. Docker Hub deposundan Service Fabric onebox kapsayıcı görüntüsü çekin:

    ```bash
    docker pull servicefabricoss/service-fabric-onebox
    ```

2. Ana bilgisayarınızda Docker daemon yapılandırmasını şu ayarlarla güncelleştirin ve Docker daemon programını yeniden başlatın: 

    ```json
    {
        "ipv6": true,
        "fixed-cidr-v6": "fd00::/64"
    }
    ```
    Bu ayarları doğrudan Docker yükleme yolunuzdaki daemon.json dosyasında güncelleştirebilirsiniz.
    
    >[!NOTE]
    >
    >Daemon.json dosyasının konumu makineden makineye farklılık gösterebilir. Örneğin, ~/Library/Containers/com.docker.docker/Data/database/com.docker.driver.amd64-linux/etc/docker/daemon.json.
    >
    >Daemon yapılandırma ayarlarını doğrudan Docker’da değiştirmek önerilen yaklaşımdır. **Docker simgesi**’ni ve ardından **Tercihler** > **Daemon** > **Gelişmiş**’i seçin.
    >

3. Bir Service Fabric onebox kapsayıcı örneği başlatın ve ilk adımda aşağı çektiğiniz görüntüyü kullanın:

    ```bash
    docker run -itd -p 19080:19080 --name sfonebox servicefabricoss/service-fabric-onebox
    ```
    >[!TIP]
    >Kapsayıcı örneğiniz için bir ad belirterek, örneğinizin daha okunaklı bir biçimde işlenebilmesini sağlayın. 
    >
    >Uygulamanız belirli bağlantı noktalarını dinliyorsa, bağlantı noktaları ek `-p` etiketleri kullanılarak belirtilmelidir. Örneğin, uygulamanız 8080 bağlantı noktasını dinliyorsa, şuradaki `-p` etiketini ekleyin:
    >
    >`run docker run -itd -p 19080:19080 -p 8080:8080 --name sfonebox servicefabricoss/service-fabric-onebox`
    >

4. Etkileşimli SSH modunda Docker kapsayıcısı oturumunu açın:

    ```bash
    docker exec -it sfonebox bash
    ```

5. Gerekli bağımlılıkları getirecek olan ayar betiğini çalıştırın ve kümeyi kapsayıcı üzerinde başlatın:

    ```bash
    ./setup.sh     # Fetches and installs the dependencies required for Service Fabric to run
    ./run.sh       # Starts the local cluster
    ```

6. 5. adım tamamlandıktan sonra Mac’inizde `http://localhost:19080` konumuna gidin. Service Fabric Explorer’ı görmeniz gerekir.

## <a name="set-up-the-service-fabric-cli-sfctl-on-your-mac"></a>Mac'inizde Service Fabric CLI'sını (sfctl) ayarlama

Service Fabric CLI'sını (`sfctl`) Mac'inize yüklemek için [Service Fabric CLI'sı](service-fabric-cli.md#cli-mac) talimatlarını izleyin.
CLI kümeler, uygulamalar ve hizmetler de dahil olmak üzere Service Fabric varlıklarıyla etkileşimi destekleyen komutlar içerir.

## <a name="create-your-application-on-your-mac-by-using-yeoman"></a>Yeoman kullanarak Mac'inizde uygulama oluşturma

Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar. Service Fabric Yeoman şablon oluşturucunun makinenizde çalıştığından emin olmak için şu adımları izleyin:

1. Node.js ve Düğüm Paketi Yöneticisi (NPM) Mac’inizde yüklü olmalıdır. Yazılım, [HomeBrew](https://brew.sh/) kullanılarak şurada anlatıldığı gibi yüklenebilir:

    ```bash
    brew install node
    node -v
    npm -v
    ```
2. NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleyin:

    ```bash
    npm install -g yo
    ```
3. Başlarken [belgelerinde](service-fabric-get-started-linux.md) bulunan adımları izleyerek kullanmak istediğiniz Yeoman oluşturucuyu yükleyin. Yeoman kullanarak Service Fabric uygulamaları oluşturmak için şu adımları takip edin:

    ```bash
    npm install -g generator-azuresfjava       # for Service Fabric Java Applications
    npm install -g generator-azuresfguest      # for Service Fabric Guest executables
    npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
    ```
4. Mac’inizde bir Service Fabric Java uygulaması derlemek için ana makinede JDK sürüm 1.8 ve Gradle yüklü olmalıdır. Yazılım, [HomeBrew](https://brew.sh/) kullanılarak şurada anlatıldığı gibi yüklenebilir: 

    ```bash
    brew update
    brew cask install java
    brew install gradle
    ```

## <a name="deploy-your-application-on-your-mac-from-the-terminal"></a>Uygulamanızı terminalden Mac’inize dağıtma

Service Fabric uygulamanızı oluşturup derledikten sonra [Service Fabric CLI](service-fabric-cli.md#cli-mac)’yi kullanarak uygulamanızı dağıtabilirsiniz:

1. Mac’inizdeki kapsayıcı örneğinin içinde çalışan Service Fabric kümesine bağlanın:

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Proje dizininize gidip yükleme betiğini çalıştırın:

    ```bash
    cd MyProject
    bash install.sh
    ```

## <a name="set-up-net-core-20-development"></a>.NET Core 2.0 ile geliştirmeyi ayarlama

[C# Service Fabric uygulamaları oluşturmaya](service-fabric-create-your-first-linux-application-with-csharp.md) başlamak amacıyla [Mac için .NET Core 2.0 SDK'sını](https://www.microsoft.com/net/core#macos) yükleyin. .NET Core 2.0 Service Fabric uygulamaları paketleri NuGet.org üzerinde barındırılmaktadır ve şu anda önizleme sürümündedir.

## <a name="install-the-service-fabric-plug-in-for-eclipse-neon-on-your-mac"></a>Mac’inizde Eclipse Neon için Service Fabric eklentisini yükleme

Azure Service Fabric, Java IDE için Eclipse Neon’a yönelik bir eklenti sağlar. Eklenti, Java hizmetleri oluşturma, derleme ve dağıtma işlemlerini basitleştirir. Eclipse içi Service Fabric eklentisinin son sürümünü yüklemek veya son sürümüne güncelleştirmek için [şu adımları](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) izleyin. [Eclipse için Service Fabric belgeleri](service-fabric-get-started-eclipse.md)ndeki adımlar da geçerlidir: bir uygulama derleme, uygulamaya bir hizmet ekleme, bir uygulamayı kaldırma ve benzeri.

Son adım ise, ana bilgisayarınızla paylaşılan bir yolu olan kapsayıcı örneği oluşturmak olacaktır. Eklentinin Mac’inizdeki Docker kapsayıcısı ile çalışması için bu tür örnek oluşturma gerekir. Örneğin:

```bash
docker run -itd -p 19080:19080 -v /Users/sayantan/work/workspaces/mySFWorkspace:/tmp/mySFWorkspace --name sfonebox servicefabricoss/service-fabric-onebox
```

Öznitelikleri şunlardır:
* `/Users/sayantan/work/workspaces/mySFWorkspace`, Mac’inizdeki çalışma alanının tam yolu.
* `/tmp/mySFWorkspace`, çalışma alanının eşlenmesi gereken kapsayıcının içindeki yol.

>[!NOTE]
> 
>Çalışma alanınız için farklı bir adınız/yolunuz varsa, bu değerleri `docker run` komutunda güncelleştirin.
> 
>Kapsayıcıyı `sfonebox` dışında bir adla başlatırsanız, Service Fabric aktör Java uygulamanızdaki testclient.sh dosyasında ad değerini güncelleştirin.
>

## <a name="next-steps"></a>Sonraki adımlar
<!-- Links -->
* [Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-create-your-first-linux-application-with-java.md)
* [Linux üzerinde Eclipse için Service Fabric eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-get-started-eclipse.md)
* [Azure portalında bir Service Fabric kümesi oluşturma](service-fabric-cluster-creation-via-portal.md)
* [Azure Resource Manager’ı kullanarak bir Service Fabric kümesi oluşturma](service-fabric-cluster-creation-via-arm.md)
* [Service Fabric uygulama modelini anlama](service-fabric-application-model.md)
* [Uygulamalarınızı yönetmek için Service Fabric CLI'yı kullanma](service-fabric-application-lifecycle-sfctl.md)
* [Windows üzerinde Linux geliştirme ortamı hazırlama](service-fabric-local-linux-cluster-windows.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
