---
title: "aaaDeploy Docker kapsayıcısı küme Azure'da | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Kubernetes, DC/OS veya Docker Swarm bir çözümde hello Azure portal ya da Resource Manager şablonu kullanarak dağıtın."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs"
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a>Barındırma çözümünüzü Hello Azure portal kullanarak bir Docker kapsayıcısı dağıtma



Azure Kapsayıcı Hizmeti popüler açık kaynak kapsayıcı kümeleme ve düzenleme çözümlerinin hızlı dağıtımını sağlar. Bu belge, hello Azure portal veya bir Azure Resource Manager Hızlı Başlangıç şablonu kullanarak Azure kapsayıcı hizmeti kümesi dağıtmayı adım anlatılmaktadır. 

Hello kullanarak Azure kapsayıcı hizmeti kümesi dağıtabilirsiniz [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) veya Azure kapsayıcı hizmeti API'leri hello.

Arka plan bilgileri için bkz. [Azure Container Service'e giriş](../container-service-intro.md).


## <a name="prerequisites"></a>Ön koşullar

* **Azure aboneliği**: Aboneliğiniz yoksa [ücretsiz deneme](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935) sürümüne kaydolun. Daha büyük bir küme için, kullandıkça öde veya diğer satın alma seçeneklerini göz önünde bulundurun.

    > [!NOTE]
    > Azure abonelik kullanımınızı ve [kaynak kotalarını](../../azure-subscription-service-limits.md), çekirdek kotaları gibi dağıttığınız hello küme hello boyutunu sınırlandırabilirsiniz. toorequest kota artışı, açık bir [çevrimiçi müşteri destek isteği](../../azure-supportability/how-to-create-azure-support-request.md) herhangi bir ücret alınmaz.
    >

* **SSH RSA ortak anahtar**: hello portalı veya hello Azure hızlı başlangıç şablonlarını biri dağıtırken tooprovide hello ortak anahtar Azure kapsayıcı hizmeti sanal makinelere karşı kimlik doğrulaması için gereksinim duyduğunuz. toocreate güvenli Kabuk (SSH) RSA anahtarları bkz hello [OS X ve Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) veya [Windows](../../virtual-machines/linux/ssh-from-windows.md) Kılavuzu. 

* **Hizmet asıl istemci Kimliğini ve parolasını** (yalnızca Kubernetes): daha fazla bilgi ve yönergeler toocreate için bir Azure Active Directory hizmet asıl, bkz: [hello hizmet sorumlusu Kubernetes kümesi için hakkında](../kubernetes/container-service-kubernetes-service-principal.md).



## <a name="create-a-cluster-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir küme oluşturma
1. Oturum açma toohello Azure portal seçin **yeni**ve arama için Azure Marketi hello **Azure kapsayıcı hizmeti**.

    ![Market’te Azure Container Service](./media/container-service-deployment/acs-portal1.png)  <br />

2. **Azure Container Service**'e ve ardından **Oluştur**'a tıklayın.

3. Merhaba üzerinde **Temelleri** dikey penceresinde, aşağıdaki bilgilerle hello girin:

    * **Orchestrator**: hello kapsayıcı orchestrators toodeploy hello kümede birini seçin.
        * **DC/OS**: DC/OS kümesi dağıtır.
        * **Swarm** Docker Swarm kümesi dağıtır.
        * **Kubernetes**: Bir Kubernetes kümesi dağıtır.
    * **Abonelik**: Bir Azure aboneliği seçin.
    * **Kaynak grubu**: hello hello dağıtım için yeni bir kaynak grubu adını girin.
    * **Konum**: hello Azure kapsayıcı hizmeti dağıtımı için bir Azure bölgesi seçin. Kullanım durumu için bkz. [Bölgelere göre kullanılabilir ürünler](https://azure.microsoft.com/regions/services/).
    
    ![Temel ayarlar](./media/container-service-deployment/acs-portal3.png)  <br />
    
    Tıklatın **Tamam** hazır tooproceed olduğunuzda.

4. Merhaba üzerinde **ana yapılandırma** dikey penceresinde hello Linux ana düğüm veya düğümler (bazı ayarları olan belirli tooeach orchestrator) hello kümedeki ayarlarını aşağıdaki hello girin:

    * **Ana DNS adı**: hello kullanılacak önek toocreate benzersiz bir hello ana etki alanı adı (FQDN) tam. Ana FQDN'sidir hello biçiminde hello *önek*Yönetim*konumu*. cloudapp.azure.com.
    * **Kullanıcı adı**: hello hello Linux sanal makineleri hello kümedeki her bir hesap için kullanıcı adı.
    * **SSH RSA ortak anahtar**: hello ortak anahtar toobe hello Linux sanal makinelere karşı kimlik doğrulaması için kullanılan ekleyin. Bu anahtar hiçbir satır sonları içerir ve hello içerir önemlidir `ssh-rsa` öneki. Merhaba `username@domain` sonek isteğe bağlıdır. Merhaba anahtar hello aşağıdaki gibi görünmelidir: **ssh-rsa AAAAB3Nz... <>...... UcyupgH azureuser@linuxvm** . 
    * **Hizmet sorumlusu**: Merhaba Kubernetes orchestrator seçtiyseniz, Azure Active Directory girin **hizmet asıl istemci kimliği** (Merhaba AppID olarak da adlandırılır) ve **hizmet asıl gizli** (parola). Daha fazla bilgi için bkz: [hello hizmet sorumlusu Kubernetes kümesi için hakkında](../kubernetes/container-service-kubernetes-service-principal.md).
    * **Ana sayısı**: Merhaba hello kümedeki ana sunucu sayısı.
    * **VM tanılama**: bazı orchestrators için VM tanılama hello katmanlardaki etkinleştirebilirsiniz.

    ![Ana sunucu yapılandırması](./media/container-service-deployment/acs-portal4.png)  <br />

    Tıklatın **Tamam** hazır tooproceed olduğunuzda.

5. Merhaba üzerinde **Aracısı yapılandırması** dikey penceresinde, aşağıdaki bilgilerle hello girin:

    * **Aracı sayısı**: Docker Swarm ve Kubernetes için bu değer hello ilk hello aracı ölçek grubundaki aracıların sayısıdır. DC/OS için bu hello ilk özel ölçek kümesindeki aracıları sayısıdır. Ayrıca, DC/OS için önceden belirlenen sayıda aracı içeren bir ortak ölçek kümesi oluşturulur. Merhaba bu ortak ölçek grubundaki aracıların sayısı hello kümedeki ana sunucu hello sayısı tarafından belirlenir: bir Yöneticisi için bir ortak aracı ve üç ya da beş yöneticileri için iki ortak aracıları.
    * **Aracı sanal makine boyutu**: Merhaba hello Aracısı sanal makinelerin boyutu.
    * **İşletim sistemi**: Bu ayar yalnızca hello Kubernetes orchestrator seçtiyseniz, şu anda kullanılabilir değil. Bir Linux dağıtım veya bir Windows Server işletim sistemi toorun hello aracılar üzerinde seçin. Bu ayar, kümenizin kapsayıcı uygulamalarında Linux mu yoksa Windows mu çalıştırabileceğini belirler. 

        > [!NOTE]
        > Windows kapsayıcı desteği Kubernetes kümeleri için önizleme sürümündedir. DC/OS ve Swarm kümelerinde Azure Container Service şu an için yalnızca Linux aracıları desteklemektedir.

    * **Aracı kimlik bilgilerini**: hello Windows işletim sistemi seçtiyseniz, bir yönetici girin **kullanıcı adı** ve **parola** hello Aracısı VM'ler için. 

    ![Aracı yapılandırması](./media/container-service-deployment/acs-portal5.png)  <br />

    Tıklatın **Tamam** hazır tooproceed olduğunuzda.

6. Hizmet doğrulama tamamlandıktan sonra **Tamam**'a tıklayın.

    ![Doğrulama](./media/container-service-deployment/acs-portal6.png)  <br />

7. Merhaba koşullarını gözden geçirin. toostart hello dağıtım işlemi, tıklatın **oluşturma**.

    Toopin hello dağıtım toohello Azure portal tercih ettiyseniz hello dağıtım durumunu görebilirsiniz.

    ![Dağıtım durumu](./media/container-service-deployment/acs-portal8.png)  <br />

Merhaba dağıtım birkaç dakika toocomplete alır. Ardından, hello Azure kapsayıcı hizmeti kümesi kullanım için hazırdır.


## <a name="create-a-cluster-by-using-a-quickstart-template"></a>Hızlı başlangıç şablonu kullanarak küme oluşturma
Azure hızlı başlangıç, kullanılabilir toodeploy Azure kapsayıcı hizmeti kümesinde şablonlarıdır. Merhaba, hızlı başlangıç şablonlarını değiştirilmiş tooinclude ek veya Gelişmiş Azure yapılandırma olabilir sağlanan. toocreate bir Azure Hızlı Başlangıç şablonu kullanarak bir Azure kapsayıcı hizmeti kümesi, bir Azure aboneliği gerekir. Bir aboneliğiniz yoksa [ücretsiz deneme](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935) sürümüne kaydolun. 

Bu adımları toodeploy bir şablonu kullanarak bir küme izleyin ve Azure CLI 2.0 hello (bkz [yükleme ve kurulum yönergeleri](/cli/azure/install-az-cli2)).

> [!NOTE] 
> Bir Windows sisteminde değilseniz, Azure PowerShell kullanarak şablon benzer adımları toodeploy kullanabilirsiniz. Bu bölümün sonraki kısımlarında verilen adımlara bakın. Ayrıca, bir şablonu hello aracılığıyla dağıtabilirsiniz [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) veya diğer yöntemleri.

1. toodeploy bir DC/OS, Docker Swarm veya Kubernetes kümesi seçin hello kullanılabilir hızlı başlangıç şablonlarından birini Github'dan. Kısmi bir liste görüntülenir. Merhaba DC/OS ve Swarm şablonları olan hello hello varsayılan orchestrator seçimi dışında aynı.

    * [DC/OS şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Swarm şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Kubernetes şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Tooyour Azure hesabı oturum (`az login`) ve bu hello Azure CLI bağlı tooyour Azure aboneliği olduğundan emin olun. Komutu aşağıdaki hello kullanarak hello varsayılan abonelik görebilirsiniz:

    ```azurecli
    az account show
    ```
    
    Birden fazla abonelik ve gerek tooset farklı varsayılan bir abonelik varsa, çalıştırmanız `az account set --subscription` ve hello abonelik kimliği veya adı belirtin.

3. En iyi uygulama, yeni bir kaynak grubu hello dağıtım için kullanın. toocreate bir kaynak grubu kullanmak hello `az group create` komutu, bir kaynak grubu adı ve konum belirtin: 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. Bir JSON dosyası içeren hello gerekli şablon parametreleri oluşturun. Adlı indirme hello parametreler dosyası `azuredeploy.parameters.json` hello Azure kapsayıcı hizmeti şablonu eşlik `azuredeploy.json` github'da. Kümeniz için gerekli parametre değerlerini girin. 

    Örneğin, toouse hello [DC/OS şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), parametre için değerler `dnsNamePrefix` ve `sshRSAPublicKey`. Merhaba açıklamalarına bakın `azuredeploy.json` ve diğer parametreler için Seçenekler.  
 

5. Komut, aşağıdaki hello ile Merhaba dağıtım parametreler dosyası geçirerek bir kapsayıcı hizmeti kümesi oluşturma yeri:

    * **RESOURCE_GROUP** hello hello önceki adımda oluşturduğunuz hello kaynak grubunun adı.
    * **DEPLOYMENT_NAME** toohello dağıtım size bir ad (isteğe bağlı).
    * **Template_urı** hello hello dağıtım dosyasının konumudur `azuredeploy.json`. Bu URI hello Raw dosyasını bir işaretçi toohello GitHub kullanıcı arabirimini değil olmalıdır. toofind bu URI, select hello `azuredeploy.json` dosya Github'da öğesini tıklatıp hello **Raw** düğmesi.  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    Merhaba komut satırındaki JSON biçimli dize olarak parametreleri de sağlayabilirsiniz. Komut benzer toohello aşağıdakileri kullanın:

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > Merhaba dağıtım birkaç dakika toocomplete alır.
    > 

### <a name="equivalent-powershell-commands"></a>Eşdeğer PowerShell komutları
Azure Container Service küme şablonu dağıtmak için PowerShell de kullanabilirsiniz. Bu belge hello sürümü 1.0 temel [Azure PowerShell Modülü](https://azure.microsoft.com/blog/azps-1-0/).

1. toodeploy bir DC/OS, Docker Swarm veya Kubernetes kümesi seçin hello kullanılabilir hızlı başlangıç şablonlarından birini Github'dan. Kısmi bir liste görüntülenir. Merhaba DC/OS ve Swarm şablonları olan Merhaba, aynı hello varsayılan orchestrator seçimi hello özel durumla unutmayın.

    * [DC/OS şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Swarm şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Kubernetes şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Azure aboneliğinizde küme oluşturmadan önce PowerShell oturumunuzun tooAzure içinde imzalanmış doğrulayın. Bu hello ile yapabileceğiniz `Get-AzureRMSubscription` komutu:

    ```powershell
    Get-AzureRmSubscription
    ```

3. TooAzure toosign gerekirse hello kullanın `Login-AzureRMAccount` komutu:

    ```powershell
    Login-AzureRmAccount
    ```

4. En iyi uygulama, yeni bir kaynak grubu hello dağıtım için kullanın. toocreate bir kaynak grubu kullanmak hello `New-AzureRmResourceGroup` komut ve kaynak grubu adını ve hedef bölgesini belirtin:

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. Bir kaynak grubu oluşturduktan sonra komutu aşağıdaki hello ile kümenizi oluşturabilirsiniz. Merhaba hello URI'sini istenen şablon hello ile belirtilen `-TemplateUri` parametresi. Bu komutu çalıştırdığınızda, PowerShell sizden dağıtım parametre değerlerini ister.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a>Şablon parametrelerini belirtin
PowerShell ile bilginiz varsa, eksi işareti (-) yazarak ve ardından hello SEKME tuşuna basarak bir cmdlet için kullanılabilir parametrelerde hello aracılığıyla gezinebilirsiniz bildirin. Bu işlev şablonunuzda tanımladığınız parametreler için de geçerlidir. Merhaba şablon adını yazmanızın hemen ardından hello cmdlet hello şablonu getirir, hello parametreleri ayrıştırır ve hello şablon parametreleri toohello komutu dinamik olarak ekler. Bu, kolay toospecify hello şablon parametre değerlerini kolaylaştırır. Ve PowerShell gerekli parametre değerini unutursanız, hello değeri ister.

Burada, parametreleri içeren hello tam komut verilmiştir. Merhaba hello kaynakların adları için kendi değerlerinizi sağlar.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a>Sonraki adımlar
Artık çalışan bir kümeniz olduğuna göre, bağlantı ve yönetim ayrıntıları için aşağıdaki belgelere bakın:

* [Tooan Azure kapsayıcı hizmeti kümesine bağlanma](../container-service-connect.md)
* [Azure Container Service ve DC/OS ile çalışma](container-service-mesos-marathon-rest.md)
* [Azure Container Service ve Docker Swarm ile çalışma](container-service-docker-swarm.md)
* [Azure Container Service ve Kubernetes ile çalışma](../kubernetes/container-service-kubernetes-walkthrough.md)
