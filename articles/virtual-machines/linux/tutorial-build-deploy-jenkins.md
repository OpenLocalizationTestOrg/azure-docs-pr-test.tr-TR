---
title: CI/CD'den Jenkins Team Services ile Azure vm'lerinin | Microsoft Docs
description: "Sürekli Tümleştirme (CI) ve Visual Studio Team Services (VSTS) ya da Microsoft Team Foundation Server (TFS) yayın Yönetimi'nden Azure Vm'lerine Jenkins kullanarak bir Node.js uygulaması sürekli dağıtımını (CD) ayarlama"
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
ms.openlocfilehash: a40e26a8681df31fad664e4d1df4c1513311900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-linux-vms-using-jenkins-and-team-services"></a>Jenkins ve Team Services kullanarak Linux VM'ler için uygulamanızı dağıtma

Sürekli Tümleştirme (CI) ve sürekli dağıtımı (CD) olarak derleme, sürüm ve kullanabilirsiniz, kodunuzu dağıtmak bir ardışık düzen olur. Team Services dağıtımı için CI/CD Otomasyon Araçları'nın tam, tam özellikli bir dizi Azure'a sağlar. Jenkins CI/CD Otomasyon de sağlayan bir Popüler 3. taraf CI/CD sunucu tabanlı araçtır. Her ikisi de birlikte bulut uygulaması veya hizmeti teslim nasıl özelleştirmek için kullanabilirsiniz.

Bu öğreticide, Jenkins oluşturmak için kullandığınız bir **Node.js web uygulamasına**ve Visual Studio Team Services aygıtını dağıtılacağı bir [dağıtım grubu](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) Linux sanal makineleri içeren.

Yapacaklarınız:

> [!div class="checklist"]
> * Jenkins uygulamanızda derleme
> * Jenkins Team Services tümleştirme için yapılandırma
> * Azure sanal makineler için bir dağıtım grubu oluşturun
> * Sanal makineleri yapılandırır ve uygulamayı dağıtır bir yayın tanımı oluşturun

## <a name="before-you-begin"></a>Başlamadan önce

* Jenkins hesabınıza erişmeniz gerekir. Jenkins server henüz oluşturmadıysanız, bkz: [Jenkins belgelerine](https://jenkins.io/doc/). 

* Team Services hesabınızda oturum açın (`https://{youraccount}.visualstudio.com`). 
  Alabileceğiniz bir [serbest Team Services hesabı](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).

  > [!NOTE]
  > Daha fazla bilgi için bkz: [Team Services Bağlan](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).

* Zaten yoksa, kişisel erişim belirteci (PAT), Team Services hesabı oluşturun. Jenkins Team Services hesabınıza erişmek için bu bilgileri gerektirir.
  Okuma [nasıl oluşturabilirim kişisel erişim belirteci Team Services ve TFS için](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) biri oluşturma hakkında bilgi edinmek için.

## <a name="get-the-sample-app"></a>Örnek uygulamayı Al

Bir uygulamayı dağıtmak için bir Git deposu içinde depolanan gerekir.
Bu öğretici için kullandığınız olan öneririz [Github'dan Bu örnek uygulama](https://github.com/azooinmyluggage/fabrikam-node).

1. Bu uygulamanın çatalı oluşturun ve bu öğreticinin daha sonraki adımlarda kullanılmak konumu (URL) not edin.

1. Çatalı olun **ortak** GitHub için daha sonra bağlanmayı basitleştirmek için.

> [!NOTE]
> Daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/) ve [özel bir depo ortak yapma](https://help.github.com/articles/making-a-private-repository-public/).

> [!NOTE]
> Uygulama kullanılarak oluşturulan [Yeoman](http://yeoman.io/learning/index.html); kullandığı **Express**, **bower**, ve **grunt**; ve bazı sahip **npm** paketler bağımlılık olarak.
> Örnek uygulama kümesini içeren [Azure Resource Manager şablonları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) dağıtımı için sanal makineleri Azure üzerinde dinamik olarak oluşturmak için kullanılır. Bu şablonlar görevleri tarafından kullanılan [Team Services sürüm tanımı](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).
> Ana şablon bir ağ güvenlik grubu, bir sanal makine ve sanal ağ oluşturur. Bir ortak IP adresini atar ve gelen bağlantı noktası 80'i açar. Ayrıca, dağıtım almak için makine seçmek için dağıtım grubu tarafından kullanılan bir etiket ekler.
>
> Örnek, Nginx ayarlar ve uygulamayı dağıtır bir betik de içerir. Her sanal makineler üzerinde yürütülür. Özellikle, betik düğümünde, Nginx ve PM2 yükler; Nginx ve PM2 yapılandırır; ardından düğümü uygulaması başlatır.

## <a name="configure-jenkins-plugins"></a>Jenkins eklentileri yapılandırın

İlk olarak, iki Jenkins eklentileri için yapılandırmanız gerekir **NodeJS** ve **Team Services ile tümleştirme**.

1. Jenkins hesabınızı açın ve seçin **yönetmek Jenkins**.

1. İçinde **yönetmek Jenkins** sayfasında, **eklentileri yönetme**.

1. Listenin bulmak için filtre **NodeJS** eklentisi ve yeniden başlatma gerekmeden yükleyin.

   ![Jenkins için NodeJS eklenti ekleme](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. Listenin bulmak için filtre **Team Foundation Server** eklentisini yükleyin. (Bu eklenti çalışır Team Services ve Team Foundation Server için.) Jenkins yeniden başlatılması gerekli değildir.

## <a name="configure-jenkins-build-for-nodejs"></a>Node.js için Jenkins yapı yapılandırma

Jenkins, yeni bir derleme projesi oluşturun ve aşağıdaki gibi yapılandırın:

1. İçinde **genel** sekmesinde, yapı projeniz için bir ad girin.

1. İçinde **kaynak kodu Yönetimi** sekmesine **Git** ve depo ve uygulama kodu içeren dalı ayrıntılarını girin.

   ![Bir depo, derleme ekleyin](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > Deponuzda ortak değilse seçin **Ekle** ve buna bağlanmak için kimlik bilgilerini sağlayın.

1. İçinde **yapı tetikleyicileri** sekmesine **yoklama SCM** ve zamanlama girin `H/03 * * * *` değişiklikleri için Git deposu üç dakikada yoklamak için. 

1. İçinde **yapı ortamı** sekmesine **sağlayan düğüm &amp; npm bin / klasör yolu** ve girin `NodeJS` düğümü JS yükleme değeri. Bırakın **npmrc dosya** "sistem varsayılan kullanır." olarak ayarlayın

1. İçinde **yapı** sekmesinde, aşağıdaki komutu girin `npm install` tüm bağımlılıkları güncelleştirilir emin olmak için.

## <a name="configure-jenkins-for-team-services-integration"></a>Jenkins Team Services tümleştirme için yapılandırma

1. İçinde **oluşturma sonrası eylemleri** sekmesinde için **arşivlemek için dosyaları**, girin `**/*` tüm dosyaları eklemek için.

1. İçin **tetiklemek TFS/Team Services sürümde**, hesabınızı tam URL'sini girin (gibi `https://your-account-name.visualstudio.com`), proje adı, (daha sonra oluşturulan) sürüm tanımı ve hesabınıza bağlanmak için kimlik bilgileri için bir ad.
   Kullanıcı adınızı ve daha önce oluşturduğunuz PAT gerekir. 

   ![Jenkins oluşturma sonrası eylemleri yapılandırma](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Derleme projesi kaydedin.

## <a name="create-a-jenkins-service-endpoint"></a>Jenkins hizmet uç noktası oluşturma

Hizmet uç noktası Team Services'ı için Jenkins bağlanmasına izin verir.

1. Açık **Hizmetleri** Team Services, açık sayfasında **yeni hizmet uç noktası** listesinde ve seçin **Jenkins**.

   ![Jenkins uç nokta ekleyin](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Bu bağlantıya başvurmak için kullanacağınız bir ad girin.

1. Jenkins sunucunuza ve onay URL'sini girin **kabul güvenilmeyen SSL sertifikalarını** seçeneği.

1. Jenkins hesabınız için kullanıcı adını ve parolasını girin.

1. Seçin **bağlantısını doğrulama** bilgilerin doğru olup olmadığını denetlemek için.

1. Seçin **Tamam** hizmet uç noktası oluşturulamadı.

## <a name="create-a-deployment-group"></a>Bir dağıtım grubu oluşturun

Gereksinim duyduğunuz bir [dağıtım grubu](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) sanal makineleri içeren için.

1. Açık **sürümleri** sekmesinde **yapı &amp; sürüm** hub'ı açın **dağıtım grupları** sekmesini tıklatın ve seçin **+ yeni**.

1. Dağıtım grubu ve isteğe bağlı bir açıklama için bir ad girin.
   Ardından **oluşturma**.

Azure kaynak grubu dağıtımı görev oluşturur ve Azure Resource Manager şablonu kullanarak çalıştığında VM'ler kaydeder.
Oluşturun ve sanal makineleri kendiniz kaydetmeniz gerekmez.

## <a name="create-a-release-definition"></a>Bir yayın tanımı oluşturun

Bir yayın tanımı işlem Team Services uygulamasını dağıtmak için yürütecek belirtir.
Team Services içinde sürüm tanımı oluşturmak için:

1. Açmak **sürümleri** sekmesinde **yapı &amp; yayın** hub'ı Aç  **+**  aşağı açılan listesinde, sürüm tanımlarını ve seçin **oluşturma yayın tanımı**. 

1. Seçin **boş** şablonu ve **sonraki**.

1. İçinde **yapıları** bölümünde, tıklayın **bir yapı bağlantı** ve **Jenkins**. Jenkins hizmet uç noktası bağlantınızı seçin. Ardından Jenkins kaynak iş seçip **oluşturma**. 

1. Yeni sürüm tanımı, seçin **+ görev ekleme** ve ekleme bir **Azure kaynak grubu dağıtımı** varsayılan ortamına görev.

1. Açılan ok seçin **+ Ekle görevleri** bağlantı ve bir dağıtım grubu aşaması tanımına ekleyin.

   ![Bir dağıtım grubu aşaması ekleme](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. Görev Kataloğu'nda açmak **yardımcı programı** bölüm ve bir örnek ekler **Kabuk betiği** görev.

1. Azure kaynak grubu dağıtımı görevde kullanılan parametreleri şablonu Vm'lere bağlanmak için kullanılan yönetici parolasını ayarlar.
   Değişkenle bu parola **$(adminpassword)**:
   
   - Açık **değişkenleri** sekmesini hem de **değişkenleri** bölümünde, bir ad girin `adminpassword`.

   - Yönetici parolasını girin.

   - Parolayla korumak için değer textbox yanındaki "asma kilit" simgesini seçin. 

## <a name="configure-the-azure-resource-group-deployment-task"></a>Azure kaynak grubu dağıtımı görevi yapılandırmak

**Azure kaynak grubu dağıtımı** görev, bir dağıtım grubu oluşturmak için kullanılır. Aşağıdaki gibi yapılandırın:

* **Azure aboneliği:** altındaki listeden bir bağlantı seçin **kullanılabilir Azure hizmet bağlantıları**. 
  Hiçbir bağlantı görünüyorsa seçin **Yönet**seçin **yeni hizmet uç noktası** sonra **Azure Resource Manager**ve yönergeleri izleyin.
  İade yayın tanımınızı, yenileme **AzureRM abonelik** listesinde ve oluşturduğunuz bağlantıyı seçin.

* **Kaynak grubu**: daha önce oluşturduğunuz kaynak grubunun adını girin.

* **Konum**: dağıtım için bir bölge seçin.

  ![Yeni bir kaynak grubu oluşturma](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **Şablon konumu**:`URL of the file`

* **Şablon bağlantısı**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **Şablon parametreleri bağlantısı**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **Şablon parametreleri geçersiz kılma**: geçersiz kılma listesini değerleri, örneğin: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.<br />{Yer tutucular} kendi özel değerlerinizi yerleştirin. 

* **Önkoşullar etkinleştirme**:`Configure with Deployment Group agent`

* **TFS/VSTS endpoint**: seçin **Ekle** ve "Yeni Team Foundation Server/Team Services Bağlantısı Ekle" iletişim kutusunda seçin **belirteç tabanlı kimlik doğrulaması**. Bağlantının adını ve takım projenizin URL'sini girin. Ardından oluşturmak ve girin bir [kişisel erişim belirteci (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) takım projenize bağlantı kimliğini doğrulamak için.

  ![Kişisel oluşturma erişim belirteci](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Takım projesi**: geçerli projenizi seçin.

* **Dağıtım grubu**: siz için kullanılan aynı dağıtım grubu adı girin **kaynak grubu** parametresi.

Azure kaynak grubu dağıtımı görev için varsayılan ayarları oluşturmak veya bir kaynak güncelleştirmek için ve bunu artımlı olarak yapmak için ' dir. Görev ilk kez çalıştırır ve daha sonra yalnızca güncelleştirmenizi VM'ler oluşturur.

## <a name="configure-the-shell-script-task"></a>Kabuk betiği görevi yapılandırmak

**Kabuk betiği** görev Node.js yüklemek ve uygulamayı başlatmak için her sunucuda çalıştırmak bir komut dosyası için yapılandırma sağlamak için kullanılır. Aşağıdaki gibi yapılandırın:

* **Komut dosyası yolu**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **Çalışma belirtin dizin**:`Checked`

* **Çalışma dizini**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-the-release-definition"></a>Yeniden adlandırın ve yayın tanımını kaydet

1. İçinde belirtilen adı yayın tanımına adını düzenleyin **oluşturma sonrası eylemleri** Jenkins derlemede sekmesinde. Jenkins kaynak yapıları güncelleştirildiğinde yeni sürüm tetikleme edebilmek için bu ad gerektirir.

1. İsteğe bağlı olarak, adına tıklayarak ortam adını değiştirin. 

1. Seçin **kaydetmek**ve seçin **Tamam**.

## <a name="start-a-manual-deployment"></a>El ile dağıtımı Başlat

1. Seçin **+ yayın** seçip **sürüm oluşturma**.

1. Tamamlanan yapı vurgulanan aşağı açılan listeden seçip **oluşturma**.

1. Yayın bağı açılan iletide'i seçin. Örneğin: "yayın **sürüm 1** oluşturuldu."

1. Açık **günlükleri** yayın konsol çıktısı izlemek için sekmesi.

1. Tarayıcınızda, dağıtım grubuna eklenen sunucuların birini URL'sini açın. Örneğin, girin`http://{your-server-ip-address}`

## <a name="start-a-cicd-deployment"></a>CI/CD dağıtım Başlat

1. Yayın tanımı'nda onay kutusunu temizleyin **etkin** onay kutusu **denetim seçeneklerini** Azure kaynak grubu dağıtımı görev için ayarları bölümü.
   Varolan bir dağıtım grubu için gelecekteki dağıtımlar için bu görevi yeniden yürütme gerekmez.

1. Kaynak Git deposuna gidin ve içeriğini değiştirmeye **h1** dosyasında başlık [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).

1. Değişikliğiniz uygulayın.

1. Birkaç dakika sonra oluşturulan yeni bir sürüm görürsünüz **sürümleri** Team Services veya TFS sayfası. Yayın gerçekleşmesini dağıtım görmek için açın. Tebrikler!

## <a name="next-steps"></a>Sonraki Adımlar

Bu öğreticide, Azure Jenkins derleme ve sürüm için Team Services kullanarak bir uygulama dağıtımını otomatik. Size nasıl öğrenilen için:

> [!div class="checklist"]
> * Jenkins uygulamanızda derleme
> * Jenkins Team Services tümleştirme için yapılandırma
> * Azure sanal makineler için bir dağıtım grubu oluşturun
> * Sanal makineleri yapılandırır ve uygulamayı dağıtır bir yayın tanımı oluşturun

Bir AMPUL dağıtma hakkında daha fazla bilgi için sonraki öğretici İlerlet (Linux, Apache, MySQL ve PHP) yığını.

> [!div class="nextstepaction"]
> [LAMP yığını dağıtma](tutorial-lamp-stack.md)