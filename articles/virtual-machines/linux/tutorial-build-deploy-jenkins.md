---
title: aaaCI/Jenkins tooAzure Team Services ile sanal makineleri CD'den | Microsoft Docs
description: "Sürekli Tümleştirme (CI) ve Visual Studio Team Services (VSTS) veya Microsoft Team Foundation Server (TFS) yayın yönetimini Jenkins tooAzure VM'lerin kullanarak bir Node.js uygulaması sürekli dağıtımını (CD) ayarlama"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>Uygulama tooLinux sanal makineleri dağıtmak Jenkins ve Team Services kullanma

Sürekli Tümleştirme (CI) ve sürekli dağıtımı (CD) olarak derleme, sürüm ve kullanabilirsiniz, kodunuzu dağıtmak bir ardışık düzen olur. Team Services için dağıtım tooAzure CI/CD Otomasyon Araçları'nın tam, tam özellikli bir kümesini sağlar. Jenkins CI/CD Otomasyon de sağlayan bir Popüler 3. taraf CI/CD sunucu tabanlı araçtır. Her iki birlikte toocustomize kullanabilirsiniz, bulut uygulaması veya hizmeti nasıl teslim.

Bu öğreticide kullandığınız Jenkins toobuild bir **Node.js web uygulamasına**ve Visual Studio Team Services toodeploy, tooa [dağıtım grubu](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) Linux sanal makineleri içeren.

Yapacaklarınız:

> [!div class="checklist"]
> * Jenkins uygulamanızda derleme
> * Jenkins Team Services tümleştirme için yapılandırma
> * Azure sanal makineler hello için bir dağıtım grubu oluşturma
> * Merhaba VM'ler yapılandırır ve hello uygulamayı dağıtır bir yayın tanımı oluşturun

## <a name="before-you-begin"></a>Başlamadan önce

* Erişim tooa Jenkins hesabınızın olması gerekir. Jenkins server henüz oluşturmadıysanız, bkz: [Jenkins belgelerine](https://jenkins.io/doc/). 

* Tooyour Team Services hesabı oturum (`https://{youraccount}.visualstudio.com`). 
  Alabileceğiniz bir [serbest Team Services hesabı](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).

  > [!NOTE]
  > Daha fazla bilgi için bkz: [tooTeam Hizmetleri'ne Bağlama](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).

* Zaten yoksa, kişisel erişim belirteci (PAT), Team Services hesabı oluşturun. Jenkins bu bilgileri tooaccess Team Services hesabınızın gerektirir.
  Okuma [nasıl oluşturabilirim kişisel erişim belirteci Team Services ve TFS için](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn nasıl toogenerate biri.

## <a name="get-hello-sample-app"></a>Merhaba örnek uygulamayı Al

Git deposunda saklanan bir uygulama toodeploy gerekir.
Bu öğretici için kullandığınız olan öneririz [Github'dan Bu örnek uygulama](https://github.com/azooinmyluggage/fabrikam-node).

1. Bu uygulamanın çatalı oluşturun ve bu öğreticinin daha sonraki adımlarda kullanılmak hello konumu (URL) not edin.

1. Merhaba çatalı olun **ortak** tooGitHub daha sonra bağlanmayı toosimplify.

> [!NOTE]
> Daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/) ve [özel bir depo ortak yapma](https://help.github.com/articles/making-a-private-repository-public/).

> [!NOTE]
> Merhaba uygulama kullanarak yapılmış [Yeoman](http://yeoman.io/learning/index.html); kullandığı **Express**, **bower**, ve **grunt**; ve bazı sahip **npm**paketler bağımlılık olarak.
> Merhaba örnek uygulamayı içeren bir dizi [Azure Resource Manager şablonları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) olan kullanılan toodynamically oluşturduğunuz hello sanal makine dağıtımı için Azure üzerinde. Bu şablonlar hello görevleri tarafından kullanılan [Team Services sürüm tanımı](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).
> Merhaba ana şablon bir ağ güvenlik grubu, bir sanal makine ve sanal ağ oluşturur. Bir ortak IP adresini atar ve gelen bağlantı noktası 80'i açar. Ayrıca, hello dağıtım grubu çok select hello makineler tooreceive hello dağıtım tarafından kullanılan bir etiket ekler.
>
> Merhaba örnek, Nginx ayarlar ve hello uygulamayı dağıtır bir betik de içerir. Her hello sanal makineler üzerinde yürütülür. Özellikle, hello betik düğümünde, Nginx ve PM2 yükler; Nginx ve PM2 yapılandırır; ardından hello düğüm uygulama başlatır.

## <a name="configure-jenkins-plugins"></a>Jenkins eklentileri yapılandırın

İlk olarak, iki Jenkins eklentileri için yapılandırmanız gerekir **NodeJS** ve **Team Services ile tümleştirme**.

1. Jenkins hesabınızı açın ve seçin **yönetmek Jenkins**.

1. Merhaba, **yönetmek Jenkins** sayfasında, **eklentileri yönetme**.

1. Filtre hello listesi toolocate hello **NodeJS** eklentisi ve yeniden başlatma gerekmeden yükleyin.

   ![Merhaba NodeJS eklentisi tooJenkins ekleme](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. Filtre hello listesi toofind hello **Team Foundation Server** eklentisini yükleyin. (Bu eklenti çalışır Team Services ve Team Foundation Server için.) Jenkins yeniden başlatılması gerekli değildir.

## <a name="configure-jenkins-build-for-nodejs"></a>Node.js için Jenkins yapı yapılandırma

Jenkins, yeni bir derleme projesi oluşturun ve aşağıdaki gibi yapılandırın:

1. Merhaba, **genel** sekmesinde, yapı projeniz için bir ad girin.

1. Merhaba, **kaynak kodu Yönetimi** sekmesine **Git** ve hello deposu ve uygulama kodunuzu içeren hello şube hello ayrıntılarını girin.

   ![Depodaki tooyour derleme ekleyin](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > Deponuzda ortak değilse seçin **Ekle** ve kimlik bilgilerini tooconnect tooit sağlayın.

1. Merhaba, **yapı tetikleyicileri** sekmesine **yoklama SCM** ve hello zamanlama girin `H/03 * * * *` toopoll hello Git deposu değişiklikleri üç dakikada. 

1. Merhaba, **yapı ortamı** sekmesine **sağlayan düğüm &amp; npm bin / klasör yolu** ve girin `NodeJS` hello düğümü JS yükleme değeri için. Bırakın **npmrc dosya** "sistem varsayılan kullanır." olarak ayarlayın

1. Merhaba, **yapı** sekmesinde, hello komutu girin `npm install` tooensure tüm bağımlılıkları güncelleştirilir.

## <a name="configure-jenkins-for-team-services-integration"></a>Jenkins Team Services tümleştirme için yapılandırma

1. Merhaba, **oluşturma sonrası eylemleri** sekmesinde için **dosyaları tooarchive**, girin `**/*` tooinclude tüm dosyalar.

1. İçin **tetiklemek TFS/Team Services sürümde**, hesabınızın hello tam URL'sini girin (gibi `https://your-account-name.visualstudio.com`), hello proje adı (daha sonra oluşturulan) hello yayın tanımı için bir ad ve kimlik bilgilerini tooconnect tooyour hesabı hello.
   Kullanıcı adınızı ve hello daha önce oluşturduğunuz PAT gerekir. 

   ![Jenkins oluşturma sonrası eylemleri yapılandırma](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Merhaba yapı projeyi kaydedin.

## <a name="create-a-jenkins-service-endpoint"></a>Jenkins hizmet uç noktası oluşturma

Hizmet uç noktası Team Services tooconnect tooJenkins sağlar.

1. Açık hello **Hizmetleri** Team Services, açık hello sayfasında **yeni hizmet uç noktası** listesinde ve seçin **Jenkins**.

   ![Jenkins uç nokta ekleyin](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Toorefer toothis bağlantısının kullanacağı bir ad girin.

1. Merhaba Jenkins sunucunuzun URL'sini girin ve değer hello **kabul güvenilmeyen SSL sertifikalarını** seçeneği.

1. Jenkins hesabınızın Hello kullanıcı adı ve parola girin.

1. Seçin **bağlantısını doğrulama** bilgi hello toocheck doğru.

1. Seçin **Tamam** toocreate hello Hizmeti uç noktası.

## <a name="create-a-deployment-group"></a>Bir dağıtım grubu oluşturun

Gereksinim duyduğunuz bir [dağıtım grubu](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) çok hello sanal makineler içeriyor.

1. Açık hello **sürümleri** hello sekmesinde **yapı &amp; sürüm** hub sonra açık hello **dağıtım grupları** sekmesini tıklatın ve seçin **+ yeni**.

1. Merhaba dağıtım grubu ve isteğe bağlı bir açıklama için bir ad girin.
   Ardından **oluşturma**.

Hello Azure kaynak grubu dağıtımı görev oluşturur ve hello Azure Resource Manager şablonu kullanarak çalıştığında hello VM'ler kaydeder.
Toocreate gerek yoktur ve hello sanal makineleri kendiniz kaydedin.

## <a name="create-a-release-definition"></a>Bir yayın tanımı oluşturun

Bir yayın tanımı hello işlem Team Services toodeploy hello uygulama yürütecek belirtir.
Team Services toocreate hello yayın tanımı:

1. Açık hello **sürümleri** hello sekmesinde **yapı &amp; yayın** hub, açık hello  **+**  açılan hello sürüm tanımlarını listesinde ve seçin Merhaba **oluşturma yayın tanımı**. 

1. Select hello **boş** şablonu ve **sonraki**.

1. Merhaba, **yapıları** bölümünde, tıklayın **bir yapı bağlantı** ve seçin **Jenkins**. Jenkins hizmet uç noktası bağlantınızı seçin. Ardından hello Jenkins kaynak iş seçip **oluşturma**. 

1. Merhaba yeni yayın tanımı, seçin **+ görev ekleme** ve ekleme bir **Azure kaynak grubu dağıtımı** görev toohello varsayılan ortamı.

1. Merhaba açılan ok sonraki toohello seçin **+ Ekle görevleri** bağlantı ve bir dağıtım grubu aşaması toohello tanımını ekleyin.

   ![Bir dağıtım grubu aşaması ekleme](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. Merhaba Hello görev Kataloğu'nda açmak **yardımcı programı** bölümünde ve hello bir örnek ekler **Kabuk betiği** görev.

1. Hello Azure kaynak grubu dağıtımı görevde kullanılan hello parametreleri şablonu hello yönetici kullanılan parola tooconnect toohello VM'ler ayarlar.
   Merhaba değişkenle bu parola **$(adminpassword)**:
   
   - Açık hello **değişkenleri** sekmesi ve hello **değişkenleri** bölümünde, hello adı girin `adminpassword`.

   - Merhaba yönetici parolasını girin.

   - Merhaba "asma" simgesini sonraki toohello değeri metin kutusu tooprotect hello parola seçin. 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>Hello Azure kaynak grubu dağıtımı görev yapılandırın

Merhaba **Azure kaynak grubu dağıtımı** kullanılan toocreate hello dağıtım grubu bir görevdir. Aşağıdaki gibi yapılandırın:

* **Azure aboneliği:** altında hello listesinden bir bağlantı seçin **kullanılabilir Azure hizmet bağlantıları**. 
  Hiçbir bağlantı görünüyorsa seçin **Yönet**seçin **yeni hizmet uç noktası** sonra **Azure Resource Manager**ve hello istemleri izleyin.
  Dönüş tooyour yayın tanımı, yenileme hello **AzureRM abonelik** listesini ve oluşturduğunuz select hello bağlantısı.

* **Kaynak grubu**: daha önce oluşturduğunuz hello kaynak grubunun adını girin.

* **Konum**: hello dağıtımı için bir bölge seçin.

  ![Yeni bir kaynak grubu oluşturma](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **Şablon konumu**:`URL of hello file`

* **Şablon bağlantısı**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **Şablon parametreleri bağlantısı**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **Şablon parametreleri geçersiz kılma**: hello listesini geçersiz kılma değerleri, örneğin: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.<br />Merhaba {yer tutucuları} için belirli kendi değerlerinizi yerleştirin. 

* **Önkoşullar etkinleştirme**:`Configure with Deployment Group agent`

* **TFS/VSTS endpoint**: seçin **Ekle** ve "Yeni Team Foundation Server/Team Services Bağlantısı Ekle" Merhaba iletişim kutusunda seçin **belirteç tabanlı kimlik doğrulaması**. Merhaba bağlantının adını ve takım projenizin hello URL'sini girin. Ardından oluşturmak ve girin bir [kişisel erişim belirteci (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello bağlantı tooyour takım projesi.

  ![Kişisel oluşturma erişim belirteci](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Takım projesi**: geçerli projenizi seçin.

* **Dağıtım grubu**: girin hello için kullanılan aynı dağıtım grubu adını hello **kaynak grubu** parametresi.

hello Azure kaynak grubu dağıtımı görev için Hello varsayılan ayarları toocreate olan veya bir kaynak ve toodo kadar artımlı bir şekilde güncelleştirin. Merhaba görev hello VM'ler hello ilk kez çalıştırır ve daha sonra yalnızca güncelleştirmenizi oluşturur.

## <a name="configure-hello-shell-script-task"></a>Merhaba Kabuk betiği görev yapılandırın

Merhaba **Kabuk betiği** kullanılan tooprovide hello yapılandırması için bir komut dosyası toorun her sunucu tooinstall Node.js ve başlangıç hello uygulamada bir görevdir. Aşağıdaki gibi yapılandırın:

* **Komut dosyası yolu**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **Çalışma belirtin dizin**:`Checked`

* **Çalışma dizini**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-hello-release-definition"></a>Yeniden adlandırın ve hello yayın tanımını kaydet

1. Merhaba adını, belirtilen hello yayın tanımı toohello Düzenle **oluşturma sonrası eylemleri** Jenkins hello derlemede sekmesinde. Merhaba kaynak yapıları güncelleştirildiğinde Jenkins bu adı toobe mümkün tootrigger yeni bir sürüm gerektirir.

1. İsteğe bağlı olarak, hello adına tıklayarak hello ortamı hello adını değiştirin. 

1. Seçin **kaydetmek**ve seçin **Tamam**.

## <a name="start-a-manual-deployment"></a>El ile dağıtımı Başlat

1. Seçin **+ yayın** seçip **sürüm oluşturma**.

1. Merhaba yapı, tamamlandı hello vurgulanan aşağı açılan listeden seçip **oluşturma**.

1. Merhaba sürüm bağlantı hello açılan iletide seçin. Örneğin: "yayın **sürüm 1** oluşturuldu."

1. Açık hello **günlükleri** sekmesinde toowatch hello yayın konsol çıkışı.

1. Tarayıcınızda, hello URL'yi açın hello sunucuların birini tooyour dağıtım grubuna eklendi. Örneğin, girin`http://{your-server-ip-address}`

## <a name="start-a-cicd-deployment"></a>CI/CD dağıtım Başlat

1. Hello tanımı sürüm, hello seçeneğinin işaretini kaldırın **etkin** hello onay kutusu **denetim seçeneklerini** hello Azure kaynak grubu dağıtımı görev için hello ayarları bölümü.
   Gelecekteki dağıtımlar toohello için var olan dağıtım grubu, toore gerekmez-bu görevi yürütün.

1. Toohello kaynak Git deposu dönüp hello Merhaba içeriğine değiştirmek **h1** hello dosyasında başlık [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).

1. Değişikliğiniz uygulayın.

1. Birkaç dakika sonra hello oluşturulan yeni bir sürüm görürsünüz **sürümleri** Team Services veya TFS sayfası. Merhaba yayın toosee hello dağıtım gerçekleşmesini açın. Tebrikler!

## <a name="next-steps"></a>Sonraki Adımlar

Bu öğreticide, Jenkins derleme ve sürüm için Team Services kullanarak bir uygulama tooAzure hello dağıtımını otomatik. Şunları öğrendiniz:

> [!div class="checklist"]
> * Jenkins uygulamanızda derleme
> * Jenkins Team Services tümleştirme için yapılandırma
> * Azure sanal makineler hello için bir dağıtım grubu oluşturma
> * Merhaba VM'ler yapılandırır ve hello uygulamayı dağıtır bir yayın tanımı oluşturun

Toohello sonraki öğretici toolearn nasıl toodeploy AMPUL (Linux, Apache, MySQL ve PHP) yığın hakkında daha fazla ilerleyin.

> [!div class="nextstepaction"]
> [LAMP yığını dağıtma](tutorial-lamp-stack.md)