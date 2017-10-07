---
title: "Azure kapsayıcı hizmeti ve Swarm ile aaaCI/CD | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Docker Swarm, bir Azure kapsayıcı kayıt defteri ve Visual Studio Team Services toodeliver sürekli olarak bir çok kapsayıcı .NET Core uygulaması ile kullanma"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, kapsayıcıları, mikro-services, Azure, Visual Studio Team Services, DevOps Swarm"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>Tam CI/CD ardışık düzen toodeploy Visual Studio Team Services kullanarak Docker Swarm ile Azure kapsayıcı hizmeti üzerinde çok kapsayıcı uygulama

Aşağıdakilerden birini hello en büyük zorluklardan hello bulut için modern uygulamalar geliştirme mümkün toodeliver yüklenirken bu uygulamalara sürekli olarak. Bu makalede, tooimplement tam sürekli tümleştirme ve Docker Swarm, Azure kapsayıcı kayıt defteri ve Visual Studio Team Services ile Azure kapsayıcı hizmeti kullanarak dağıtım (CI/CD) ardışık nasıl oluşturulacağına öğrenin ve yayın yönetimi.

Bu makalede, kullanılabilen basit bir uygulama dayalı [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), ASP.NET Core ile geliştirilen. Merhaba uygulaması dört farklı hizmetlerini oluşur: üç API'ları ve bir web ön uç web:

![MyShop örnek uygulama](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

Merhaba hedefi toodeliver Visual Studio Team Services kullanarak sürekli bir Docker Swarm kümesinde, bu bir uygulamadır. Merhaba aşağıdaki ayrıntıları bu kesintisiz teslim ardışık düzen şekil:

![MyShop örnek uygulama](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

Kısa bir açıklama başlangıç adımları şöyledir:

1. Kod değişiklikleri olan taahhüt toohello kaynak kodu deposu (burada, GitHub) 
2. Visual Studio Team Services derlemede GitHub tetikler 
3. Visual Studio Team Services hello en son sürümünü hello kaynakları alır ve Merhaba uygulaması oluşturan tüm hello görüntü oluşturur 
4. Visual Studio Team Services hello Azure kapsayıcı kayıt defteri hizmeti kullanılarak oluşturulan her görüntü tooa Docker kayıt defteri iter 
5. Yeni bir sürüm Visual Studio Team Services tetikler 
6. Merhaba yayın hello Azure kapsayıcı hizmeti küme ana düğümünde SSH kullanarak bazı komutları çalıştırır 
7. Docker Swarm hello küme çeken hello en son sürümünü hello görüntüleri 
8. Merhaba uygulamanın yeni sürümü Hello Docker Compose kullanılarak dağıtılır 

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticiye başlamadan önce görevleri aşağıdaki toocomplete hello gerekir:

- [Azure Container Service'te Swarm kümesi oluşturma](container-service-deployment.md)
- [Azure kapsayıcı Hizmeti'nde hello Swarm kümesine bağlanın](../container-service-connect.md)
- [Azure kapsayıcı kayıt defteri oluşturma](../../container-registry/container-registry-get-started-portal.md)
- [Oluşturulan Visual Studio Team Services hesabı ve ekip projesinde olması](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Çatalı hello GitHub depo tooyour GitHub hesabı](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Ayrıca bir Ubuntu (14.04 veya 16.04) makinede yüklü Docker ile gerekir. Bu makine kullanılan hello sırasında Visual Studio Team Services tarafından derleme ve sürüm işlemler. Tek yönlü toocreate bu makine toouse hello hello kullanılabilir görüntüdür [Azure Marketi](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/). 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>1. adım: Visual Studio Team Services hesabınızın yapılandırma 

Bu bölümde, Visual Studio Team Services hesabınızın yapılandırın.

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>Visual Studio Team Services Linux derleme Aracısı'nı yapılandırma

toocreate Docker görüntüler ve bu bir Visual Studio Team Services Azure kapsayıcı defterinden görüntülere Yapı anında iletme, tooregister Linux Aracısı gerekir. Bu yükleme seçeneğiniz vardır:

* [Linux üzerinde bir aracıyla Dağıt](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [Docker toorun hello VSTS aracı kullanın](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>Merhaba Docker tümleştirmesi VSTS uzantısını yükleyin

Microsoft, yapıda VSTS uzantısı toowork docker'la sağlar ve işlemler bırakın. Bu uzantı hello kullanılabilir [VSTS Market](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker). Tıklatın **yükleme** tooadd bu uzantı tooyour VSTS hesabı:

![Merhaba Docker tümleştirmesi yükleyin](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

Kimlik bilgilerinizi kullanarak tooconnect tooyour VSTS hesap istenir. 

### <a name="connect-visual-studio-team-services-and-github"></a>Visual Studio Team Services ve GitHub Bağlan

VSTS projeniz, GitHub hesabınızda arasında bir bağlantı ayarlayın.

1. Visual Studio Team Services projenizde hello tıklatın **ayarları** simgesi hello araç ve seçin **Hizmetleri**.

    ![Visual Studio Team Services - dış bağlantı](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. Hello solda tıklatın **yeni hizmet uç noktası** > **GitHub**.

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. GitHub hesabınızla tooauthorize VSTS toowork tıklatın **Authorize** ve açılır hello penceresinde hello yordamı izleyin.

    ![Visual Studio Team Services - GitHub yetkilendirmek](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>VSTS tooyour Azure kapsayıcı kayıt defteri ve Azure kapsayıcı hizmeti kümesine bağlanma

Merhaba CI/CD ardışık düzenine alma önce hello son tooconfigure dış bağlantıları tooyour kapsayıcı kayıt defteri ve Docker Swarm kümenizde Azure adımlardır. 

1. Merhaba, **Hizmetleri** Visual Studio Team Services projenizin ayarları ekleme Hizmeti uç noktası türü **Docker kayıt defteri**. 

2. Açılır hello açılan penceresinde hello URL ve Azure kapsayıcı kaydınız hello kimlik bilgilerini girin.

    ![Visual Studio Team Services - Docker kayıt defteri](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Merhaba Docker Swarm kümesi için bir uç nokta türü ekleme **SSH**. Ardından Swarm kümenizin hello SSH bağlantı bilgilerini girin.

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

Tüm hello yapılandırma şimdi yapılır. Merhaba sonraki adımlarda oluşturan ve hello uygulama toohello Docker Swarm kümesi dağıtır hello CI/CD ardışık düzen oluşturun. 

## <a name="step-2-create-hello-build-definition"></a>2. adım: hello derleme tanımı oluşturma

Bu adımda, yapı definitionfor VSTS projenizi ayarlayın ve kapsayıcı görüntülerinizi hello yapı iş akışı tanımlayın

### <a name="initial-definition-setup"></a>Başlangıç tanım Kurulumu

1. toocreate bir derleme tanımınız connect Visual Studio Team Services proje ve tıklatın tooyour **yapı & yayın**. 

2. Merhaba, **yapı tanımları** 'yi tıklatın **+ yeni**. Select hello **boş** şablonu.

    ![Visual Studio Team Services - yeni yapı tanımı](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. GitHub depo ile kaynak denetimi Hello yeni yapı yapılandırma **sürekli tümleştirme**ve Linux Aracısı kayıtlı olduğu select hello Aracısı sırası. Tıklatın **oluşturma** toocreate hello yapı tanımı.

    ![Visual Studio Team Services - derleme tanımı oluştur](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. Merhaba üzerinde **yapı tanımlarını** sayfasında, ilk hello'ni açın **depo** sekmesinde ve hello yapı toouse hello çatalı hello önkoşullarını oluşturulan hello MyShop projesinin yapılandırın. Seçtiğinizden emin olun *acs belgeleri* hello olarak **varsayılan dalı**.

    ![Visual Studio Team Services - derleme deposu yapılandırma](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. Merhaba üzerinde **Tetikleyicileri** sekmesinde, her yürütme tetiklenen hello yapı toobe yapılandırın. Seçin **sürekli tümleştirme** ve **toplu değişiklikleri**.

    ![Visual Studio Team Services - derleme tetikleyici yapılandırması](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>Merhaba yapı iş akışı tanımlama
Merhaba sonraki adımlar hello yapı iş akışı tanımlayın. Hello için beş kapsayıcı görüntüleri toobuild vardır *MyShop* uygulama. Her görüntü hello Dockerfile hello proje klasörlerde yer alan kullanılarak oluşturulur:

* ProductsApi
* Ara sunucu
* RatingsApi
* RecommandationsApi
* ShopFront

Tooadd iki Docker adımları her görüntü için bir toobuild hello görüntüsü ve bir toopush hello görüntüsü hello Azure kapsayıcı kayıt defterinde gerekir. 

1. tooadd hello yapı iş akışı, bir adımda tıklatın **+ Ekle derleme adımı** seçip **Docker**.

    ![Visual Studio Team Services - eklemek derleme adımları](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. Merhaba kullanan tek bir adımda yapılandırma her resmi için `docker build` komutu.

    ![Visual Studio Team Services - Docker derleme](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Merhaba derleme işlemi, Azure kapsayıcı kaydınız hello seçin **görüntü yapı** eylem ve hello her görüntü tanımlar Dockerfile. Set hello **yapı bağlam** Dockerfile hello dizin kök ve hello tanımlamak **görüntü adı**. 
    
    Ekran önceki hello üzerinde gösterildiği gibi Azure kapsayıcı kaydınız URI'sini hello ile Merhaba görüntü adı başlatın. (Bu örnekte hello derleme tanımlayıcı gibi hello görüntüsünün yapı değişken tooparameterize hello etiketini de kullanabilirsiniz.)

3. Merhaba kullanır ikinci bir adım her görüntü için yapılandırma `docker push` komutu.

    ![Visual Studio Team Services - Docker gönderme](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Hello gönderme işlemi için Azure kapsayıcı kaydınız hello seçin **görüntü anında** eylemi ve hello girin **görüntü adı** hello önceki adımda oluşturulmuş.

4. Merhaba yapı yapılandırdıktan sonra ve her hello beş görüntüleri için adımları anında, hello daha fazla iki adımda iş akışı derleme ekleyin.

    a. Bir bash betik tooreplace hello kullanan bir komut satırı görevi *BuildNumber* hello docker-compose.yml dosyası hello geçerli ile olay kimliği oluşturma Ayrıntılar için ekran aşağıdaki hello bakın.

    ![Visual Studio Team Services - güncelleştirme oluşturma dosya](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. Hello sürümde kullanılabilmesi için hello bırakır bir görev oluşturma dosyası derleme yapısı olarak güncelleştirildi. Ayrıntılar için ekran aşağıdaki hello bakın.

    ![Visual Studio Team Services - Oluştur yayımlama dosyası](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. Tıklatın **kaydetmek** ve yapı tanımının adı.

## <a name="step-3-create-hello-release-definition"></a>3. adım: hello yayın tanımı oluşturma

Visual Studio Team Services verir çok[sürümleri arasında ortamlarını](https://www.visualstudio.com/team-services/release-management/). Sürekli dağıtım toomake kesintisiz bir şekilde uygulamanız farklı ortamınızı (örneğin, geliştirme, test, ön üretim ve üretim) üzerinde dağıtıldığından emin etkinleştirebilirsiniz. Azure kapsayıcı hizmeti Docker Swarm kümesi temsil eden yeni bir ortam oluşturabilirsiniz.

![Visual Studio Team Services - sürüm tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Kurulum ilk sürüm

1. toocreate bir yayın tanımı tıklatın **sürümleri** > **+ sürüm**

2. tooconfigure hello yapı kaynak tıklatın **yapıları** > **bir yapı kaynak bağlantı**. Burada, hello önceki adımda tanımlanan bu yeni sürüm tanımı toohello derleme bağlayın. Bunu yaparak, hello docker-compose.yml dosyası hello yayın işlemde kullanılabilir.

    ![Visual Studio Team Services - sürüm yapıları](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. tooconfigure hello sürüm tetikleme tıklatın **Tetikleyicileri** seçip **sürekli dağıtım**. Merhaba kümesi hello tetikleyici aynı yapı kaynağı. Bu ayar hello yapı başarıyla tamamlanır tamamlanmaz yeni bir sürüm başlayacağını sağlar.

    ![Visual Studio Team Services - sürüm Tetikleyicileri](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>Merhaba yayın iş akışı tanımlama

Merhaba yayın iş akışı eklediğiniz iki görevlerin oluşur.

1. Görev toosecurely kopyalama hello yapılandırma dosyası tooa oluşturan *dağıtmak* daha önce yapılandırdığınız hello SSH bağlantısını kullanarak hello Docker Swarm ana düğümde, klasör. Ayrıntılar için ekran aşağıdaki hello bakın.

    ![Visual Studio Team Services - sürüm SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. İkinci bir görev tooexecute bash komutu toorun yapılandırma `docker` ve `docker-compose` hello ana düğümde komutları. Ayrıntılar için ekran aşağıdaki hello bakın.

    ![Visual Studio Team Services - sürüm Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    Hello Yöneticisi kullanım hello Docker CLI ve görevleri aşağıdaki hello Docker Compose CLI toodo hello yürütülen hello komut:

    - Oturum açma toohello Azure kapsayıcı kayıt defteri (hello tanımlanan üç yapı variab'les kullanan **değişkenleri** sekmesinde)
    - Merhaba tanımlamak **DOCKER_HOST** hello Swarm uç noktası ile değişken toowork (: 2375)
    - Toohello gidin *dağıtmak* güvenli kopyalama görevi önceki hello tarafından oluşturulan ve hello docker-compose.yml dosyası içeren klasör 
    - Yürütme `docker-compose` hello yeni görüntüleri pull komutlarını Durdur hello Hizmetleri, hello Hizmetleri kaldırın ve Merhaba kapsayıcılara oluşturun.

    >[!IMPORTANT]
    > Ekran önceki hello üzerinde gösterildiği gibi hello bırakın **STDERR üzerinde başarısız** onay kutusu işaretli. Bunun nedeni bir önemli ayarı, `docker-compose` durdurma veya hello standart hata çıktısı üzerinde siliniyor kapsayıcılardır gibi birkaç tanılama iletilerini yazdırır. Merhaba onay kutusunu işaretlerseniz, tüm aşsa bile iyi Visual Studio Team Services hataları hello yayın sırasında oluştuğunu bildiriyor.
    >
3. Bu yeni sürüm tanımını kaydedin.


>[!NOTE]
>Bu dağıtım olduğundan biz hello eski hizmetleri durdurma ve hello çalıştıran yeni bir miktar kapalı kalma süresi içerir. Bu olası tooavoid mavi yeşil dağıtım yaparak olan budur.
>

## <a name="step-4-test-hello-cicd-pipeline"></a>4. Adım. Test hello CI/CD ardışık düzen

Merhaba yapılandırma ile yapılır, bu yeni saat tootest olan CI/CD ardışık düzen. Merhaba tooupdate hello kaynak kodu ve yürütme hello olduğu en kolay yolu tootest GitHub depoya değiştirir. Birkaç saniye hello kod itme sonra Visual Studio Team Services içinde çalışan yeni bir derleme görürsünüz. Başarıyla tamamlandığında, yeni bir sürüm tetiklenir ve hello hello Azure kapsayıcı hizmeti kümesinde hello uygulamasının yeni sürümünü dağıtır.

## <a name="next-steps"></a>Sonraki Adımlar

* Merhaba CI/CD Visual Studio Team Services ile ilgili daha fazla bilgi için bkz: [VSTS derleme genel bakış](https://www.visualstudio.com/docs/build/overview).
