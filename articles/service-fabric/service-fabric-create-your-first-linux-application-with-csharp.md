---
title: "aaaCreate ilk Azure mikro uygulamanıza C# kullanarak Linux | Microsoft Docs"
description: "C# kullanarak Service Fabric uygulaması oluşturma ve dağıtma"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a>İlk Azure Service Fabric uygulamanızı oluşturma
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Service Fabric, Linux üzerinde hem .NET Core hem de Java dillerinde hizmet oluşturmaya yönelik SDK’lar sağlar. Bu öğreticide, nasıl tümleştirildiği incelenmektedir toocreate Linux ve yapı C# (.NET Core) kullanarak bir hizmet için bir uygulama.

## <a name="prerequisites"></a>Ön koşullar
Başlamadan önce [Linux geliştirme ortamınızı ayarladığınızdan](service-fabric-get-started-linux.md) emin olun. Mac OS X kullanıyorsanız, [Vagrant kullanarak bir sanal makinede Linux one-box ortamı ayarlayabilirsiniz](service-fabric-get-started-mac.md).

Ayrıca tooinstall hello isteyeceksiniz [Service Fabric CLI](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>Yükleme ve hello oluşturucuları için CSharp ayarlayın
Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric CSharp uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar. Lütfen makinenizde çalışma CSharp hello Service Fabric yeoman şablonu üreteci olan tooensure hello adımları izleyin.
1. Makinenize nodejs ve NPM yükleme

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme

  ```bash
  sudo npm install -g yo
  ```
3. Merhaba Service Fabric Yeo Java uygulama üreteci NPM yükleme

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma
Service Fabric uygulaması bir veya daha fazla hizmetlerin her hello uygulamanın işlevselliğini aktarma konusunda belirli bir rol içerebilir. Merhaba Service Fabric [Yeoman](http://yeoman.io/) son adımda yüklediğiniz, CSharp için oluşturucuyu kolay toocreate kılar ilk hizmet ve daha sonra tooadd. Yeoman toocreate uygulamanın tek bir hizmetle kullanalım.

1. Bir terminale hello iskele oluşturma komut toostart aşağıdaki hello yazın:`yo azuresfcsharp`
2. Uygulamanızı adlandırın.
3. İlk hizmetiniz Hello türünü seçin ve adlandırın. Bu öğreticinin Hello amaçları doğrultusunda, güvenilir bir aktör hizmeti seçin.

   ![C# için Service Fabric Yeoman oluşturucusu][sf-yeoman]

> [!NOTE]
> Başlangıç seçenekleri hakkında daha fazla bilgi için bkz: [Service Fabric programlama modeline genel bakış](service-fabric-choose-framework.md).
>
>

## <a name="build-hello-application"></a>Merhaba uygulaması oluşturma
Merhaba Service Fabric Yeoman şablonları toobuild hello hello terminal uygulamadan (toohello uygulama klasörü gezinme sonra) kullanabileceğiniz bir yapı betiği içerir.

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a>Merhaba uygulaması dağıtma

Merhaba uygulama oluşturulduktan sonra toohello yerel küme dağıtabilirsiniz.

1. Toohello yerel Service Fabric kümesi bağlayın.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Merhaba şablonu toocopy Merhaba uygulaması toohello kümenin görüntü deposu paketini, hello uygulama türünü kaydetme ve hello uygulama örneğini oluşturmak sağlanan hello yükleme betiğini çalıştırın.

    ```bash
    ./install.sh
    ```

Dağıtma yerleşik hello aynı başka bir Service Fabric uygulama hello uygulamasıdır. Merhaba belgelerine bakın [bir Service Fabric uygulaması hello Service Fabric CLI ile yönetme](service-fabric-application-lifecycle-sfctl.md) ayrıntılı yönergeler için.

Parametreleri toothese komutları hello oluşturulan bildirimleri hello uygulama paketi içinde bulunabilir.

Merhaba uygulama dağıtıldıktan sonra bir tarayıcı açın ve gidin [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) adresindeki [http://localhost: 19080/Explorer](http://localhost:19080/Explorer). Ardından, hello genişletin **uygulamaları** düğümü ve olduğunu şimdi uygulama türü için bir giriş ve hello bu türünün ilk örneği için başka bir not.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Merhaba test istemcisi başlatın ve bir yük devretme gerçekleştirin.
Actor projeleri kendi başına bir işlem yapamaz. Başka bir hizmet veya istemci toosend gereksinim duydukları bunları iletileri. Merhaba aktör şablon toointeract hello aktör hizmeti ile kullanabileceğiniz bir basit bir sınama betiği içerir.

1. Merhaba izleme yardımcı programı toosee hello çıkış hello aktör hizmeti kullanan hello komut dosyasını çalıştırın.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. Service Fabric Explorer'da hello birincil çoğaltma hello aktör hizmeti için barındırma düğümü bulun. Merhaba ekran görüntüsünde, onu 3 düğümdür.

    ![Service Fabric Explorer'da bulma hello birincil çoğaltma][sfx-primary]
3. Merhaba önceki adımda bulunan sonra seçin hello düğümünü tıklatın **devre dışı bırak (yeniden)** hello Eylemler menüsünden. Bu eylem, yerel kümedeki başka bir düğüm üzerinde çalışan bir yük devretme tooa ikincil bir çoğaltma zorlama bir düğümü yeniden başlatır. Bu eylemi gerçekleştirme gibi dikkat toohello çıktı hello test istemcisi ve hello sayaç tooincrement hello yük devretme rağmen devam Not ücret ödersiniz.

## <a name="adding-more-services-tooan-existing-application"></a>Daha fazla Hizmetleri tooan varolan uygulama ekleme

tooadd başka bir hizmet tooan uygulaması zaten kullanılarak oluşturulan `yo`, hello aşağıdaki adımları gerçekleştirin:
1. Merhaba var olan uygulamanın toohello kök dizini değiştirin.  Örneğin, `cd ~/YeomanSamples/MyApplication`, `MyApplication` Yeoman tarafından oluşturulan hello uygulamasıdır.
2. `yo azuresfcsharp:AddService` öğesini çalıştırın

## <a name="migrating-from-projectjson-toocsproj"></a>Project.JSON too.csproj ' geçiş
1. 'Dotnet geçirmek' proje kök dizininde çalıştıran tüm hello project.json toocsproj biçimi geçirirsiniz.
2. Güncelleştirme hello proje uygun şekilde proje dosyalarını toocsproj dosyalarında başvurur.
3. Merhaba proje dosyası adları toocsproj dosyalarında build.sh güncelleştirin.

## <a name="next-steps"></a>Sonraki adımlar

* [Reliable Actors hakkında daha fazla bilgi edinin](service-fabric-reliable-actors-introduction.md)
* [Merhaba Service Fabric CLI kullanarak Service Fabric kümeleri ile etkileşim kurma](service-fabric-cli.md)
* [Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin
* [Service Fabric CLI ile çalışmaya başlama](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
