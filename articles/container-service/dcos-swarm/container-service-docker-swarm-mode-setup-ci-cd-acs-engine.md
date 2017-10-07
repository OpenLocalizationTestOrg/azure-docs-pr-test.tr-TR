---
title: "Azure kapsayıcı hizmeti altyapısı ve Swarm modu ile aaaCI/CD | Microsoft Docs"
description: "Docker Swarm modu, bir Azure kapsayıcı kayıt defteri ve Visual Studio Team Services toodeliver sürekli olarak bir çok kapsayıcı .NET Core uygulaması ile Azure kapsayıcı hizmeti altyapısını kullanma"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Mikro docker, kapsayıcıları, hizmetleri, Swarm, Azure, Visual Studio Team Services, DevOps, ACS altyapısı"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>Tam CI/CD ardışık düzen toodeploy ACS altyapısı ve Docker Swarm Visual Studio Team Services kullanarak modu ile Azure kapsayıcı hizmeti üzerinde çok kapsayıcı uygulama

*Bu makalede dayanır [tam CI/CD kanal toodeploy Visual Studio Team Services kullanarak Docker Swarm ile Azure kapsayıcı hizmeti üzerinde çok kapsayıcı uygulama](container-service-docker-swarm-setup-ci-cd.md) belgeleri*

Günümüzde, aşağıdakilerden birini hello en büyük zorluklardan hello bulut için modern uygulamalar geliştirme mümkün toodeliver yüklenirken bu uygulamalara sürekli olarak. Bu makalede, tooimplement tam sürekli tümleştirme ve dağıtım (CI/CD) kullanarak nasıl kanal öğrenin: 
* Azure kapsayıcı hizmeti altyapısı Docker Swarm modu
* Azure Container Kayıt Defteri
* Visual Studio Team Services

Bu makalede, kullanılabilen basit bir uygulama dayalı [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), ASP.NET Core ile geliştirilen. Merhaba uygulaması dört farklı hizmetlerini oluşur: üç API'ları ve bir web ön uç web:

![MyShop örnek uygulama](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

Merhaba hedefi toodeliver Visual Studio Team Services kullanarak sürekli bir Docker Swarm modu kümesinde, bu bir uygulamadır. Merhaba aşağıdaki ayrıntıları bu kesintisiz teslim ardışık düzen şekil:

![MyShop örnek uygulama](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Kısa bir açıklama başlangıç adımları şöyledir:

1. Kod değişiklikleri olan taahhüt toohello kaynak kodu deposu (burada, GitHub) 
2. Visual Studio Team Services derlemede GitHub tetikler 
3. Visual Studio Team Services hello en son sürümünü hello kaynakları alır ve Merhaba uygulaması oluşturan tüm hello görüntü oluşturur 
4. Visual Studio Team Services hello Azure kapsayıcı kayıt defteri hizmeti kullanılarak oluşturulan her görüntü tooa Docker kayıt defteri iter 
5. Yeni bir sürüm Visual Studio Team Services tetikler 
6. Merhaba yayın hello Azure kapsayıcı hizmeti küme ana düğümünde SSH kullanarak bazı komutları çalıştırır 
7. Docker Swarm modu hello kümede hello görüntüleri en son sürümünü hello çeker 
8. Merhaba uygulamanın yeni sürümü Hello Docker yığını kullanılarak dağıtılır 

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticiye başlamadan önce görevleri aşağıdaki toocomplete hello gerekir:

- [ACS altyapı ile Azure kapsayıcı Hizmeti'nde bir Swarm modu kümesi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [Azure kapsayıcı Hizmeti'nde hello Swarm kümesine bağlanın](../container-service-connect.md)
- [Azure kapsayıcı kayıt defteri oluşturma](../../container-registry/container-registry-get-started-portal.md)
- [Oluşturulan Visual Studio Team Services hesabı ve ekip projesinde olması](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Çatalı hello GitHub depo tooyour GitHub hesabı](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> Azure kapsayıcı Hizmeti'nde Hello Docker Swarm orchestrator eski tek başına Swarm kullanır. Şu anda hello tümleşik [Swarm modu](https://docs.docker.com/engine/swarm/) (Docker 1.12 ve daha yüksek) desteklenen bir orchestrator Azure kapsayıcı Hizmeti'nde değil. Bu nedenle, kullanıyoruz [ACS altyapısı](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), topluluk katkıda [hızlı başlatma şablonunu](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), veya hello Docker çözümde [Azure Marketi](https://azuremarketplace.microsoft.com).
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>1. adım: Visual Studio Team Services hesabınızın yapılandırma 

Bu bölümde, Visual Studio Team Services hesabınızın yapılandırın. Visual Studio Team Services projenizdeki tooconfigure VSTS Hizmetleri uç tıklatın hello **ayarları** simgesi hello araç ve seçin **Hizmetleri**.

![Açık hizmet uç noktası](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Visual Studio Team Services ve Azure hesabına bağlanma

VSTS projeniz ve Azure hesabınızda arasında bir bağlantı ayarlayın.

1. Hello solda tıklatın **yeni hizmet uç noktası** > **Azure Resource Manager**.
2. Azure hesabınızla tooauthorize VSTS toowork seçin, **abonelik** tıklatıp **Tamam**.

    ![Visual Studio Team Services - Azure yetkilendirmek](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Visual Studio Team Services ve GitHub Bağlan

VSTS projeniz, GitHub hesabınızda arasında bir bağlantı ayarlayın.

1. Hello solda tıklatın **yeni hizmet uç noktası** > **GitHub**.
2. GitHub hesabınızla tooauthorize VSTS toowork tıklatın **Authorize** ve açılır hello penceresinde hello yordamı izleyin.

    ![Visual Studio Team Services - GitHub yetkilendirmek](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>VSTS tooyour Azure kapsayıcı hizmeti kümesine bağlanma

Merhaba CI/CD ardışık düzenine alma önce hello son tooconfigure dış bağlantıları tooyour Docker Swarm kümesinde Azure adımlardır. 

1. Merhaba Docker Swarm kümesi için bir uç nokta türü ekleme **SSH**. Ardından hello SSH bağlantı bilgilerini Swarm kümenizin (ana düğüm) girin.

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

Tüm hello yapılandırma şimdi yapılır. Merhaba sonraki adımlarda oluşturan ve hello uygulama toohello Docker Swarm kümesi dağıtır hello CI/CD ardışık düzen oluşturun. 

## <a name="step-2-create-hello-build-definition"></a>2. adım: hello derleme tanımı oluşturma

Bu adımda, bir derleme tanımını VSTS projeniz için ayarlar ve kapsayıcı görüntülerinizi hello yapı iş akışı tanımlayın

### <a name="initial-definition-setup"></a>Başlangıç tanım Kurulumu

1. toocreate bir derleme tanımınız connect Visual Studio Team Services proje ve tıklatın tooyour **yapı & yayın**. Merhaba, **yapı tanımları** 'yi tıklatın **+ yeni**. 

    ![Visual Studio Team Services - yeni yapı tanımı](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. Select hello **boş işlem**.

    ![Visual Studio Team Services - yeni ve boş yapı tanımı](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. Merhaba ardından **değişkenleri** sekmesinde ve iki yeni değişken oluşturma: **RegistryURL** ve **AgentURL**. Kayıt defteri ve küme aracıları DNS Hello değerlerini yapıştırın.

    ![Visual Studio Team Services - derleme değişkenleri yapılandırması](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. Merhaba üzerinde **yapı tanımlarını** sayfası, açık hello **Tetikleyicileri** sekmesinde ve hello yapı toouse sürekli tümleştirme hello çatalı hello önkoşullarını oluşturulan hello MyShop projesinin yapılandırmak. Ardından, seçin **toplu değişiklikleri**. Seçtiğinizden emin olun *docker linux* hello olarak **dal belirtimi**.

    ![Visual Studio Team Services - derleme deposu yapılandırma](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. Son olarak, hello tıklatın **seçenekleri** sekmesinde ve hello varsayılan aracı sıra çok yapılandırma**barındırılan Linux Önizleme**.

    ![Visual Studio Team Services - konak aracı yapılandırması](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>Merhaba yapı iş akışı tanımlama
Merhaba sonraki adımlar hello yapı iş akışı tanımlayın. İlk olarak, tooconfigure hello kaynak hello kod gerekir. toodo, select **GitHub** ve **deposu** ve **şube** (docker-linux).

![Visual Studio Team Services - yapılandırma kod kaynağı](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Hello için beş kapsayıcı görüntüleri toobuild vardır *MyShop* uygulama. Her görüntü hello Dockerfile hello proje klasörlerde yer alan kullanılarak oluşturulur:

* ProductsApi
* Ara sunucu
* RatingsApi
* RecommandationsApi
* ShopFront

Her görüntü için iki Docker adımı, bir toobuild hello görüntüsü ve bir toopush hello görüntüsü hello Azure kapsayıcı kayıt defterinde gerekir. 

1. tooadd hello yapı iş akışı, bir adımda tıklatın **+ Ekle derleme adımı** seçip **Docker**.

    ![Visual Studio Team Services - eklemek derleme adımları](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. Merhaba kullanan tek bir adımda yapılandırma her resmi için `docker build` komutu.

    ![Visual Studio Team Services - Docker derleme](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Merhaba derleme işlemi, Azure kapsayıcı kaydınız hello seçin **görüntü yapı** eylem ve hello her görüntü tanımlar Dockerfile. Set hello **çalışma dizini** hello hello Dockerfile kök dizini olarak tanımlamak **görüntü adı**seçip **dahil en son etiket**.
    
    Merhaba görüntü adı bu biçimde toobe vardır: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```. Değiştir **[NAME]** hello görüntü adı ile:
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. Merhaba kullanır ikinci bir adım her görüntü için yapılandırma `docker push` komutu.

    ![Visual Studio Team Services - Docker gönderme](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Hello gönderme işlemi için Azure kapsayıcı kaydınız hello seçin **görüntü anında** eylem hello girin **görüntü adı** hello önceki adımı ve select yerleşik **dahil en son etiketi** .

4. Merhaba yapı yapılandırdıktan sonra ve her hello beş görüntüleri için adımları itme, hello daha fazla üç adımda iş akışı derleme ekleyin.

   ![Visual Studio Team Services - komut satırı görev ekleme](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Bir bash betik tooreplace hello kullanan bir komut satırı görevi *RegistryURL* hello docker-compose.yml dosyası hello RegistryURL değişkeniyle geçişi. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - kayıt defteri URL dosyasıyla güncelleştirme oluştur](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Bir bash betik tooreplace hello kullanan bir komut satırı görevi *AgentURL* hello docker-compose.yml dosyası hello AgentURL değişkeniyle geçişi.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Hello sürümde kullanılabilmesi için hello bırakır bir görev oluşturma dosyası derleme yapısı olarak güncelleştirildi. Ayrıntılar için ekran aşağıdaki hello bakın.

         ![Visual Studio Team Services - yayımlama yapı](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Oluştur yayımlama dosyası](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. Tıklatın **sıraya & Kaydet** tootest derleme tanımı.

   ![Visual Studio Team Services - Kaydet ve sırası](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - yeni kuyruk](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. Merhaba, **yapı** doğru bu ekranı toosee sahip:

  ![Visual Studio Team Services - oluşturma başarılı oldu](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>3. adım: hello yayın tanımı oluşturma

Visual Studio Team Services verir çok[sürümleri arasında ortamlarını](https://www.visualstudio.com/team-services/release-management/). Sürekli dağıtım toomake kesintisiz bir şekilde uygulamanız farklı ortamınızı (örneğin, geliştirme, test, ön üretim ve üretim) üzerinde dağıtıldığından emin etkinleştirebilirsiniz. Azure kapsayıcı hizmeti Docker Swarm modu kümenizi temsil eden bir ortam oluşturabilirsiniz.

![Visual Studio Team Services - sürüm tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Kurulum ilk sürüm

1. toocreate bir yayın tanımı tıklatın **sürümleri** > **+ sürüm**

2. tooconfigure hello yapı kaynak tıklatın **yapıları** > **bir yapı kaynak bağlantı**. Burada, hello önceki adımda tanımlanan bu yeni sürüm tanımı toohello derleme bağlayın. Bundan sonra hello docker-compose.yml dosyası hello yayın işlemde kullanılabilir.

    ![Visual Studio Team Services - sürüm yapıları](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. tooconfigure hello sürüm tetikleme tıklatın **Tetikleyicileri** seçip **sürekli dağıtım**. Merhaba kümesi hello tetikleyici aynı yapı kaynağı. Bu ayar hello yapı başarıyla tamamlandığında, yeni bir sürüm başlayacağını sağlar.

    ![Visual Studio Team Services - sürüm Tetikleyicileri](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. tooconfigure hello sürüm, değişkenleri **değişkenleri** seçip **+ değişken** toocreate üç yeni değişkenlerle hello kayıt defteri başlangıç bilgileri: **docker.username**, **docker.password**, ve **docker.registry**. Kayıt defteri ve küme aracıları DNS Hello değerlerini yapıştırın.

    ![Visual Studio Team Services - derleme deposu yapılandırma](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > Merhaba önceki ekranda gösterildiği gibi hello tıklayın **kilit** docker.password onay kutusu. Bu ayar, önemli toorestrict hello paroladır.
    >

### <a name="define-hello-release-workflow"></a>Merhaba yayın iş akışı tanımlama

Merhaba yayın iş akışı eklediğiniz iki görevlerin oluşur.

1. Görev toosecurely kopyalama hello yapılandırma dosyası tooa oluşturan *dağıtmak* daha önce yapılandırdığınız hello SSH bağlantısını kullanarak hello Docker Swarm ana düğümde, klasör. Ayrıntılar için ekran aşağıdaki hello bakın.
    
    Kaynak klasörü:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services - sürüm SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. İkinci bir görev tooexecute bash komutu toorun yapılandırma `docker` ve `docker stack deploy` hello ana düğümde komutları. Ayrıntılar için ekran aşağıdaki hello bakın.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - sürüm Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    Merhaba yöneticisinde yürütülen hello komut hello Docker CLI ve görevleri aşağıdaki hello Docker Compose CLI toodo hello kullanır:

    - Toohello Azure kapsayıcı kayıt defterinde oturum (hello tanımlanan üç derleme değişkenleri kullanan **değişkenleri** sekmesinde)
    - Merhaba tanımlamak **DOCKER_HOST** hello Swarm uç noktası ile değişken toowork (: 2375)
    - Toohello gidin *dağıtmak* güvenli kopyalama görevi önceki hello tarafından oluşturulan ve hello docker-compose.yml dosyası içeren klasör 
    - Yürütme `docker stack deploy` hello yeni görüntüleri çekmek ve hello kapsayıcıları oluşturma komutları.

    >[!IMPORTANT]
    > Merhaba önceki ekranda gösterildiği gibi hello bırakın **STDERR üzerinde başarısız** onay kutusu işaretli. Bu ayar bize toocomplete hello yayın işlem nedeniyle çok sağlar`docker-compose` durdurma veya hello standart hata çıktısı üzerinde siliniyor kapsayıcılardır gibi birkaç tanılama iletilerini yazdırır. Merhaba onay kutusunu işaretlerseniz, tüm aşsa bile iyi Visual Studio Team Services hataları hello yayın sırasında oluştuğunu bildiriyor.
    >
3. Bu yeni sürüm tanımını kaydedin.

## <a name="step-4-test-hello-cicd-pipeline"></a>4. adım: hello CI/CD ardışık test etme

Merhaba yapılandırma ile yapılır, bu yeni saat tootest olan CI/CD ardışık düzen. Merhaba tooupdate hello kaynak kodu ve yürütme hello olduğu en kolay yolu tootest GitHub depoya değiştirir. Birkaç saniye hello kod itme sonra Visual Studio Team Services içinde çalışan yeni bir derleme görürsünüz. Başarıyla tamamlandığında, yeni bir sürüm tetiklenir ve hello Azure kapsayıcı hizmeti kümesinde hello uygulamanın yeni sürümü hello dağıtılır.

## <a name="next-steps"></a>Sonraki adımlar

* Merhaba CI/CD Visual Studio Team Services ile ilgili daha fazla bilgi için bkz: [VSTS derleme genel bakış](https://www.visualstudio.com/docs/build/overview).
* Merhaba ACS altyapısı hakkında daha fazla bilgi için bkz: [ACS altyapısı GitHub deposuna](https://github.com/Azure/acs-engine).
* Merhaba Docker Swarm modu hakkında daha fazla bilgi için bkz: [Docker Swarm moduna genel bakış](https://docs.docker.com/engine/swarm/).
