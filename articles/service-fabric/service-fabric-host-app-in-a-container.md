---
title: "aaaDeploy kapsayıcı tooAzure Service Fabric, bir .NET uygulamasında | Microsoft Docs"
description: "Nasıl öğretilmektedir toopackage Docker kapsayıcısı içinde Visual Studio'da .NET uygulaması. Bu yeni \"kapsayıcı\" uygulama sonra dağıtılan tooa Service Fabric kümesi."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Bir Windows kapsayıcı tooAzure Service Fabric bir .NET uygulamasında dağıtma

Bu öğretici şunların nasıl yapıldığını gösterir toodeploy Azure üzerinde bir Windows kapsayıcıda mevcut bir ASP.NET uygulamasını.

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Visual Studio'da bir Docker projesi oluşturma
> * Varolan bir uygulama containerize
> * Visual Studio ve VSTS sürekli tümleştirme Kurulumu

## <a name="prerequisites"></a>Ön koşullar

1. Yükleme [Docker Windows CE](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) kapsayıcıları üzerinde Windows 10 çalıştırabilmeniz için.
2. Merhaba ile öğrenmeniz [Windows 10 kapsayıcıları quickstart][link-container-quickstart].
3. Merhaba karşıdan [Fabrikam Fiber CallCenter] [ link-fabrikam-github] örnek uygulama.
4. Yükleme [Azure PowerShell][link-azure-powershell-install]
5. Merhaba yüklemek [Visual Studio 2017 için sürekli teslim araçları uzantısı][link-visualstudio-cd-extension]
6. Oluşturma bir [Azure aboneliği] [ link-azure-subscription] ve [Visual Studio Team Services hesabı][link-vsts-account]. 
7. [Azure üzerinde bir küme oluşturun](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>Merhaba uygulaması containerize

Sahip olduğunuza göre bir [Service Fabric kümesi Azure'da çalışan](service-fabric-tutorial-create-cluster-azure-ps.md) hazır toocreate olan ve kapsayıcılı uygulamayı dağıtın. uygulamamız bir kapsayıcıda çalışan toostart tooadd ihtiyacımız **Docker Destek** Visual Studio'da toohello projesi. Eklediğinizde **Docker Destek** iki şey toohello uygulama olur. İlk olarak, bir _Dockerfile_ toohello projesi eklenir. Bu yeni dosya nasıl hello kapsayıcı görüntü yerleşik toobe açıklanmaktadır. Ardından ikinci, yeni bir _docker compose'u_ proje toohello çözüm eklenir. Merhaba yeni proje içeren birkaç dosyaları docker compose'u. Docker compose'u dosyaları hello kapsayıcı nasıl yürütüleceğini kullanılan toodescribe olabilir.

İle çalışma hakkında daha fazla bilgi [Visual Studio kapsayıcı Araçları][link-visualstudio-container-tools].

>[!NOTE]
>Bu hello Windows kapsayıcı görüntülerini bilgisayarınızda çalıştırdığınız ilk kez kullanıyorsanız, Docker CE hello temel görüntüler, kapsayıcıları için aşağı çekmek gerekir. Bu öğreticide kullanılan hello görüntüleri 14 GB bağımsızdır. Bir tane terminal komutu toopull hello taban görüntüleri aşağıdaki hello çalıştırın:
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Docker desteği ekleme

Açık hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] dosyasını Visual Studio'da.

Sağ hello **FabrikamFiber.Web** Proje > **Ekle** > **Docker Destek**.

### <a name="add-support-for-sql"></a>SQL desteği ekleme

Bir SQL server gerekli toorun Merhaba uygulaması olacak şekilde bu uygulama SQL hello veri sağlayıcısı olarak kullanır. Bizim docker compose.override.yml dosyasındaki bir SQL Server kapsayıcı yansıma başvuru.

Visual Studio'da açın **Çözüm Gezgini**, bulma **docker compose'u**ve açık hello dosya **docker compose.override.yml**.

Toohello gidin `services:` düğümü, adlandırılmış bir düğüm eklemek `db:` hello SQL Server girişi hello kapsayıcısı için tanımlar.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>Ana bilgisayardan erişilebilir olduğu müddetçe, yerel hata ayıklama için tercih ettiğiniz herhangi bir SQL sunucusu kullanabilirsiniz. Ancak, **localdb** desteklemediği `container -> host` iletişim.

>[!WARNING]
>SQL Server çalıştıran bir kapsayıcıda kalıcı veri desteklemiyor. Merhaba kapsayıcı sona erdiğinde, verileriniz silinir. Bu yapılandırma, üretim için kullanmayın.

Toohello gidin `fabrikamfiber.web:` düğümü ve adlı bir alt düğüm eklemek `depends_on:`. Bu, hello sağlar `db` hizmetini (Merhaba SQL Server kapsayıcısı) web uygulamamız önce (fabrikamfiber.web) başlatır.

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Merhaba web yapılandırma güncelleştir

Merhaba edilene **FabrikamFiber.Web** proje, güncelleştirme hello bağlantı dizesine hello **web.config** dosya, SQL Server hello kapsayıcısında toopoint toohello.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>Bir yayın oluştururken farklı SQL Server web uygulamanızın veya yapı toouse istiyorsanız, başka bir bağlantı dizesi tooyour web.release.config dosyası ekleyin.

### <a name="test-your-container"></a>Test, kapsayıcısı

Tuşuna **F5** , kapsayıcı toorun ve hata ayıklama hello uygulamada.

Kenar başlangıç IP adresi hello kapsayıcısının hello iç NAT ağda (genellikle 172.x.x.x) kullanan uygulamanızın tanımlanmış başlatma sayfasını açar. Visual Studio 2017 kullanarak kapsayıcıları uygulamalarında hata ayıklama hakkında daha fazla toolearn bkz [bu makalede][link-debug-container].

![bir kapsayıcıda fabrikam örneği][image-web-preview]

Merhaba kapsayıcı oluşturulur ve bir Service Fabric uygulaması paketlenmiş hazır toobe sunulmuştur. Makinenizde yerleşik hello kapsayıcı görüntüsünü oluşturduktan sonra tooany kapsayıcı kayıt defteri itme ve tooany konak toorun çekmek.

## <a name="get-hello-application-ready-for-hello-cloud"></a>Merhaba uygulaması hello bulut için hazırlanma

tooget Merhaba uygulaması Azure Service Fabric içinde çalıştırmak için hazır, toocomplete iki adım gerekir:

1. Başlangıç bağlantı noktası toobe mümkün tooreach web uygulamamız hello Service Fabric kümesindeki burada istiyoruz kullanıma sunar.
2. Bir üretim hazır SQL veritabanı uygulamamız için sağlayın.

### <a name="expose-hello-port-for-hello-app"></a>Merhaba uygulama için başlangıç bağlantı noktası kullanıma sunma
Merhaba Service Fabric kümesi yapılandırılmış, bağlantı noktası olan *80* açık varsayılan olarak hello Azure yük dengeleyici, gelen trafiği toohello küme dengeler. Biz bu bağlantı noktasında bizim kapsayıcı bizim docker-compose.yml dosyası getirebilir.

Visual Studio'da açın **Çözüm Gezgini**, bulma **docker compose'u**ve açık hello dosya **docker compose.override.yml**.

Merhaba değiştirme `fabrikamfiber.web:` düğümü adlı bir alt düğüm eklemek `ports:`.

Bir dize girişi ekleme `- "80:80"`.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>Bir üretim SQL veritabanını kullan
Üretimde çalıştırırken, verilerimizi ihtiyacımız bizim veritabanında kalıcı. Bir kapsayıcıda şu anda yolu tooguarantee kalıcı veri yok, bu nedenle bir kapsayıcıda SQL Server'daki üretim verileri depolanamıyor.

Bir Azure SQL veritabanı kullanan öneririz. tooset ayarlama ve çalıştırma Azure, yönetilen bir SQL Server'da ziyaret hello [Azure SQL veritabanı hızlı başlangıç ipuçları] [ link-azure-sql] makalesi.

>[!NOTE]
>Toochange hello bağlantı dizeleri toohello SQL Server'da hello unutmayın **web.release.config** hello dosyasında **FabrikamFiber.Web** projesi.
>
>SQL veritabanı erişilebilir olduğundan, bu uygulama düzgün biçimde başarısız olur. Şimdi toogo seçin ve SQL server ile Merhaba uygulaması dağıtın.

## <a name="deploy-with-visual-studio-team-services"></a>Visual Studio Team Services ile dağıtma

tooset Visual Studio Team Services kullanarak dağıtım, gereksinim duyduğunuz tooinstall hello [sürekli teslim araçları uzantısı için Visual Studio 2017][link-visualstudio-cd-extension]. Bu uzantıyı Visual Studio Team Services yapılandırarak kolay toodeploy tooAzure kolaylaştırır ve dağıtılmış uygulama tooyour Service Fabric kümesi alın.

başlatıldı, tooget kaynak denetiminde kodunuzun barındırılması gerekir. Bu bölümde Hello kalan varsayar **git** kullanılıyor.

### <a name="set-up-a-vsts-repo"></a>VSTS depodaki ayarlayın
Merhaba sağ alt köşesinde Visual Studio, tıklatın **tooSource denetim eklemek** > **Git** (veya hangi seçeneği tercih).

![Merhaba kaynak denetimi düğmesine basın][image-source-control]

Merhaba, _Takım Gezgini_ bölmesi, basın **yayımlama Git deposuna**.

VSTS havuz adı ve tuşuna seçin **depo**.

![Depodaki tooVSTS yayımlama][image-publish-repo]

Kodunuzu VSTS kaynak deposu ile eşitlenir, sürekli tümleştirme ve kesintisiz teslim yapılandırabilirsiniz.

### <a name="setup-continuous-delivery"></a>Kurulum kesintisiz teslim

İçinde _Çözüm Gezgini_, sağ hello **çözüm** > **yapılandırma kesintisiz teslim**.

Hello Azure aboneliği seçin.

Ayarlama **ana bilgisayar türü** çok**Service Fabric kümesi**.

Ayarlama **hedef ana bilgisayarın** hello önceki bölümde oluşturduğunuz toohello service fabric kümesi.

Seçin bir **kapsayıcı kayıt defteri** toopublish, kapsayıcıya.

>[!TIP]
>Kullanım hello **Düzenle** düğmesini toocreate bir kapsayıcı kayıt defteri.

**Tamam**'a basın.

![Kurulum service fabric sürekli tümleştirme][image-setup-ci]
   
   Merhaba Yapılandırma tamamlandıktan sonra dağıtılan tooService doku kapsayıcıdır. Güncelleştirmeleri toohello depo itme her bir yeni derleme ve sürüm gerçekleştirilir.
   
   >[!NOTE]
   >Yapı hello kapsayıcı görüntüleri yaklaşık 15 dakika sürebilir.
   >Merhaba ilk dağıtım toohello Service Fabric kümesi hello temel Windows Server Core kapsayıcı görüntüleri toobe indirilen neden olur. Merhaba indirme ek 5-10 dakika toocomplete alır.

Kümenizin Hello URL'yi kullanarak toohello Fabrikam çağrı merkezi uygulama göz atın: Örneğin, *http://mycluster.westeurope.cloudapp.azure.com*

Kapsayıcılı ve hello Fabrikam çağrı merkezi çözümü dağıtılmış göre hello açabilirsiniz [Azure portal] [ link-azure-portal] ve Service Fabric çalışan hello uygulama bakın. tootry Merhaba uygulaması, bir web tarayıcısı açın ve Service Fabric kümesi toohello URL'sini gidin.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Visual Studio'da bir Docker projesi oluşturma
> * Varolan bir uygulama containerize
> * Visual Studio ve VSTS sürekli tümleştirme Kurulumu

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
