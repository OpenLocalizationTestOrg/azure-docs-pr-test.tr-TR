---
title: "Azure Service Fabric ile Mac OS X toowork üzerinde geliştirme ortamınızı aaaSet | Microsoft Docs"
description: "Merhaba çalışma zamanı, SDK ve araçları yükleyip yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra Mac OS x hazır toobuild uygulamalar olur."
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
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Mac OS X’te geliştirme ortamınızı ayarlama
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

Mac OS X kullanarak Linux kümelerinde Service Fabric uygulamaları toorun oluşturabilirsiniz. Bu makalede yer almaktadır nasıl tooset Mac geliştirme için ayarlama.

## <a name="prerequisites"></a>Ön koşullar
Service Fabric OS x toorun üzerinde yerel olarak yerel bir Service Fabric kümesi çalışmaz, Vagrant ve VirtualBox kullanarak önceden yapılandırılmış bir Ubuntu sanal makine sağlıyoruz. Başlamadan önce şunlar gereklidir:

* [Vagrant (v1.8.4 veya üzeri)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> Vagrant ve VirtualBox toouse birbirini desteklenen sürümleri gerekir. Vagrant desteklenmeyen bir VirtualBox sürümünde kararsız davranabilir.
>

## <a name="create-hello-local-vm"></a>Oluşturma yerel VM hello
toocreate 5 düğümlü Service Fabric kümesi içeren yerel VM Merhaba, hello aşağıdaki adımları gerçekleştirin:

1. Kopya hello `Vagrantfile` deposu

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    Bu adımları Getir listeleri hello dosya `Vagrantfile` hello VM içeren yapılandırma hello konumu hello VM ile birlikte gelen indirilir.

2. Merhaba depoyu yerel kopyasını toohello gidin

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. (İsteğe bağlı) Merhaba varsayılan VM ayarlarını değiştirme

    Varsayılan olarak, hello yerel VM aşağıdaki gibi yapılandırılır:

   * 3 GB ayrılmış bellek
   * IP 192.168.50.50 yapılandırılmış özel konak ağ trafiğinin hello Mac ana bilgisayardan geçiş etkinleştirme

     Bu ayarlardan herhangi birini değiştirmek veya diğer yapılandırma toohello VM hello eklemek `Vagrantfile`. Merhaba bkz [Vagrant belgelerine](http://www.vagrantup.com/docs) hello yapılandırma seçeneklerinin tam listesi için.
4. Merhaba VM oluşturma

    ```bash
    vagrant up
    ```

   Bu adım, önceden yapılandırılmış hello VM görüntüsü, yerel olarak ayarlayın ve ardından yerel bir Service Fabric yukarı içinde küme önyükleme indirir. Bunu tootake birkaç dakika beklemelisiniz. Kurulum başarıyla tamamlarsa, hello çıkışı bu hello küme başlatılıyor belirten bir ileti görür.

    ![Sanal makine hazırlama sonrasında başlayan küme ayarı][cluster-setup-script]

    >[!TIP]
    > Merhaba VM indirme uzun sürüyorsa, wget veya curl kullanarak yükleyebilirsiniz veya toohello bağlantı tarafından belirtilen gezinme tarafından bir tarayıcı aracılığıyla **config.vm.box_url** hello dosyasında `Vagrantfile`. Onu yerel olarak indirdikten sonra düzenleme `Vagrantfile` hello görüntü indirdiğiniz toopoint toohello yerel yolu. Hello görüntü too/home/users/test/azureservicefabric.tp8.box yüklediyseniz örnek daha sonra ayarlamak için **config.vm.box_url** toothat yolu.
    >

5. Bu hello test küme ayarlanmış doğru tooService Fabric Explorer http://192.168.50.50:19080/Explorer (Merhaba varsayılan özel ağ IP tutulan varsayılarak) konumunda giderek.

    ![Service Fabric Explorer Mac hello ana bilgisayardan görüntülenebilir][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>Yeoman kullanarak Mac uygulaması oluşturma
Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar. Lütfen makinenizde çalışma hello Service Fabric yeoman şablon oluşturucu sahip tooensure hello adımları izleyin.

1. Toohave Node.js ve NPM, mac üzerinde yüklü gerekir. Aksi durumda, Node.js ve NPM hello aşağıdakileri kullanarak Homebrew kullanarak yükleyebilirsiniz. toocheck hello sürümleri Node.js ve NPM Mac'inizde yüklü, kullanabileceğiniz hello ``-v`` seçeneği.

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme

  ```bash
  npm install -g yo
  ```
3. Merhaba Yeoman yükleme Oluşturucu istediğiniz toouse, Başlarken hello hello adımlarını izleyerek [belgelerine](service-fabric-get-started-linux.md). Yeoman, kullanarak toocreate Service Fabric uygulamaları hello adımları-

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. Service Fabric Java uygulaması Mac üzerinde toobuild, ihtiyacınız - JDK 1.8 ve Gradle hello makinede yüklü.


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a>Eclipse Neon Hello Service Fabric eklentisini yükleme

Service Fabric sağlayan bir eklenti Merhaba **Java IDE için Eclipse Neon** oluşturma, derleme ve Java Hizmetleri dağıtma hello sürecini basitleştirmek. Bu genel bahsedilen hello yükleme adımlarını izleyin [belgelerine](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) yükleme veya Service Fabric Eclipse eklentisi güncelleştirme hakkında.

>[!TIP]
> Varsayılan olarak hello varsayılan IP hello belirtildiği gibi destekliyoruz ``Vagrantfile`` hello içinde ``Local.json`` oluşturulan hello uygulamasının. Hello karşılık gelen IP değiştirmek ve farklı bir IP Vagrant dağıtma durumunda, lütfen güncelleştirmek ``Local.json`` de uygulamanızın.

## <a name="next-steps"></a>Sonraki adımlar
<!-- Links -->
* [Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-create-your-first-linux-application-with-java.md)
* [Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-get-started-eclipse.md)
* [Hello Azure portalında bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-portal.md)
* [Azure Resource Manager Hello kullanarak bir Service Fabric kümesi oluştur](service-fabric-cluster-creation-via-arm.md)
* [Merhaba Service Fabric uygulama modelini anlama](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
