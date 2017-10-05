---
title: "3 düğümü dağıtma küme Deis | Microsoft Docs"
description: "3 düğümü oluşturma bu makalede Azure Resource Manager şablonu kullanarak azure'da küme Deis"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a0c3dd7562dfb5ce54c2ebfd4665109f59cd8fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>3 düğümünü yapılandırmak ve dağıtmak Azure kümesinde Deis
Bu makalede, sağlama aracılığıyla anlatan bir [Deis](http://deis.io/) Azure kümede. Dağıtma ve bir örnek ölçeklendirme için gerekli sertifikaları oluşturmasına tüm adımlar kapsanmaktadır **Git** yeni sağlanan kümede uygulama.

Aşağıdaki diyagramda, dağıtılan Sistem mimarisini gösterir. Küme kullanarak bir Sistem Yöneticisi yönetir araçları gibi Deis **deis** ve **deisctl**. Bağlantıları bağlantıları üye birine Küme düğümlerinde ileten bir Azure yük dengeleyici üzerinden kurulur. İstemcilerin erişim uygulamalar da yük dengeleyici aracılığıyla dağıtılan. Bu durumda, yük dengeleyici için trafiğini bir kümede barındırılan karşılık gelen Docker kapsayıcıları trafiği daha fazla routs yönlendirici kafes Deis.

  ![Dağıtılan Desis küme mimarisi diyagramı](./media/deis-cluster/architecture-overview.png)

Aşağıdaki adımlarda size çalıştırmak için ihtiyacınız vardır:

* Etkin bir Azure aboneliği. Yoksa, ücretsiz izi alma [azure.com](https://azure.microsoft.com/).
* Azure kaynak gruplarını kullanmak için iş veya Okul kimliği. Kişisel hesap ve bir Microsoft kimliğiyle günlük varsa, gerek [bir iş kimliği, kişisel sunudan oluşturma](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Ya da--bağlı olarak istemci işletim sistemi [Azure PowerShell](/powershell/azureps-cmdlets-docs) veya [Mac, Linux ve Windows için Azure CLI](../../cli-install-nodejs.md).
* [OpenSSL](https://www.openssl.org/). OpenSSL gerekli sertifikaları oluşturmak için kullanılır.
* Git istemci gibi [Git Bash](https://git-scm.com/).
* Örnek uygulamayı test etmek için de bir DNS sunucusu gerekir. Herhangi bir DNS sunucuları veya joker karakter A kayıtlarını destekleyen Hizmetleri'ni kullanabilirsiniz.
* Çalıştırmak için bir bilgisayar istemci araçları Deis. Yerel makine veya sanal makine kullanabilirsiniz. Neredeyse her Linux dağıtım noktasında bu araçları çalıştırabilirsiniz ancak Ubuntu aşağıdaki yönergeleri kullanın.

## <a name="provision-the-cluster"></a>Küme sağlama
Bu bölümde, kullanacağınız bir [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) açık kaynak havuzu şablonu [azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates). İlk olarak, şablonu kopyalayın. Ardından, kimlik doğrulama için yeni bir SSH anahtar çifti oluşturacaksınız. Ve daha sonra küme için yeni bir tanımlayıcı yapılandıracaksınız. Ve son olarak, kabuk betiği veya PowerShell Betiği kümesi sağlamak için kullanmanız.

1. Depoyu kopyalayın: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Şablon klasöre gidin:
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. SSH-keygen kullanarak yeni bir SSH anahtar çifti oluşturun:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Yukarıdaki özel anahtarı kullanarak bir sertifika oluşturun:
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file to be generated]
5. Git [https://discovery.etcd.io/new](https://discovery.etcd.io/new) yeni bir küme belirteci şuna benzer görünen oluşturmak için:
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Bu ücretsiz hizmeti benzersiz bir belirtecinden her CoreOS küme olmalıdır. Lütfen bakın [CoreOS belgelerine](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) daha fazla ayrıntı için.
6. Değiştirme **bulut config.yaml** varolan dosyaya **bulma** yeni belirteci ile belirteci:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment the following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Değiştirme **azuredeploy-parameters.json** dosya: bir metin düzenleyicisinde 4. adımda oluşturduğunuz sertifika açın. Arasındaki tüm metni kopyalayın `----BEGIN CERTIFICATE-----` ve `-----END CERTIFICATE-----` içine **sshKeyData** parametresi (tüm satırbaşı karakterlerini Kaldır gerekir).
8. Değiştirme **newStorageAccountName** parametresi. Bu VM OS diskler için depolama hesabıdır. Bu hesap adı genel olarak benzersiz olması gerekir.
9. Değiştirme **publicDomainName** parametresi. Bu yük dengeleyici genel IP ile ilişkili DNS adının bir parçası olur. Son FQDN biçimini olacaktır *[Bu parametrenin değeri]*. *[Bölge]* . cloudapp.azure.com. Örneğin, ad deishbai32 belirtirseniz ve kaynak grubu, Batı ABD bölgesi dağıtılır, ardından deishbai32.westus.cloudapp.azure.com yük dengeleyiciye son FQDN olacaktır.
10. Parametre dosyasını kaydedin. Ve ardından Azure PowerShell kullanarak küme sağlayabilirsiniz:
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    veya Azure CLI:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Kaynak grubu sağlandıktan sonra gruptaki tüm kaynakların Azure Klasik portalında görebilirsiniz. Aşağıdaki ekran görüntüsünde gösterildiği gibi bir sanal ağ aynı kullanılabilirlik kümesine katılan üç VM'ler ile kaynak grubu içerir. Grup ilişkili bir ortak IP sahip bir yük dengeleyici de içerir.
    
    ![Klasik Azure portalı üzerinde sağlanan kaynak grubu](./media/deis-cluster/resource-group.png)

## <a name="install-the-client"></a>İstemci Yükleme
Gereksinim duyduğunuz **deisctl** denetlemek için küme Deis. Deisctl tüm küme düğümlerinde otomatik olarak yüklenir ancak ayrı bir yönetim makinede deisctl kullanmak iyi bir uygulamadır. Ayrıca, tüm düğümler yalnızca özel IP adresleri yapılandırıldığından, düğüm makinelere bağlanmak için bir ortak IP sahip yük dengeleyici üzerinden tünel SSH kullanmanız gerekir. Fiziksel bir ayrı Ubuntu üzerinde deisctl ya da sanal makineyi ayarlama adımları verilmiştir.

1. Yükleme deisctl:mkdir deis
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. Özel anahtarınızı ssh aracı ekleyin:
   
        eval `ssh-agent -s`
        ssh-add [path to the private key file, see step 1 in the previous section]
3. Deisctl yapılandırın:
   
        export DEISCTL_TUNNEL=[public ip of the load balancer]:2223

Şablon 1, 2224 örneğine 2 ve 3 örneğine 2225 örnek 2223 eşleme gelen NAT kuralları tanımlar. Bu deisctl aracını kullanmak için artıklık sağlar. Klasik Azure portalı aşağıdaki kurallara inceleyebilirsiniz:

![Yük Dengeleyici NAT kuralları](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> Şu anda şablonu yalnızca 3 düğümlü kümeler destekler. Azure Resource Manager şablonu döngü sözdizimi desteklemiyor NAT kuralı tanımını uygulamasındaki bir sınırlama nedeniyle budur.
> 
> 

## <a name="install-and-start-the-deis-platform"></a>Yükleme ve başlangıç platform Deis
Artık yükleme ve başlangıç deisctl kullanarak platform Deis:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path to the private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Platform başlatma biraz zaman alır (10 dakika kadar). Özellikle, oluşturucu hizmeti başlatılıyor uzun zaman alabilir. Ve bazen başarılı olması için birkaç denemeden sürer: işlemi askıda görünüyorsa, yazmayı deneyin `ctrl+c` komutu yürütme ayırın ve yeniden deneyin.
> 
> 

Kullanabileceğiniz `deisctl list` tüm hizmetlerin çalışıp çalışmadığını doğrulamak için:

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

Tebrikler! Çalışan bir olduğuna artık Azure üzerinde clsuter Deis! Ardından, şimdi örnek eylem kümede görmek için Git uygulama dağıtın.

## <a name="deploy-and-scale-a-hello-world-application"></a>Dağıtma ve Hello World uygulama ölçeklendirme
Aşağıdaki adımlar, bir "Hello World" dağıtma gösterir küme uygulamaya gidin. Adımlar dayanır [belgelerine Deis](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Yönlendirme kafes düzgün çalışması bir joker karakter A kaydı yük dengeleyici genel IP için işaret eden bir etki alanınız için sahip olmanız gerekir. Aşağıdaki ekran görüntüsü bir örnek etki alanı kaydı için A kaydı üzerinde GoDaddy gösterir:
   
    ![Godaddy A kaydı](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Yükleme deis:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Yeni bir SSH anahtarı oluşturun ve sonra GitHub için ortak anahtarı ekleyin (doğal olarak, aynı zamanda mevcut anahtarlarınızı yeniden kullanabilirsiniz). Yeni bir SSH anahtar çifti oluşturmak için kullanın:
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s to use default file names and empty passcode)
4. İd_rsa.pub veya tercih ettiğiniz ortak anahtar için GitHub ekleyin. Bu, SSH anahtarları yapılandırma ekranında eklemek SSH anahtar düğmesini kullanarak yapabilirsiniz:
   
   ![GitHub anahtarı](./media/deis-cluster/github-key.png)
   
   <p />
5. Yeni bir kullanıcı kaydedin:
   
        deis register http://deis.[your domain]
   <p />
6. SSH anahtarı ekleyin:
   
        deis keys:add [path to your SSH public key]
   <p />      
7. Bir uygulama oluşturun.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.Git itme, birkaç dakika sürer oluşturulan ve dağıtılan, Docker görüntüleri tetikler. My deneyimlerden bazen, adım 10 (özel deponuza Pushing görüntü) kilitlenebilir. Bu gerçekleştiğinde, işlemi durdurmak, kullanarak uygulamayı kaldırma ' uygulamaları deis: – a destroy <application name> ` to remove the application and try again. You can use `apps:list deis' uygulamanızı adını öğrenmek için. Her şeyi işe yararsa komut çıktılarını sonunda aşağıdaki gibi bir şey görmeniz gerekir:
   
        -----> Launching...
               done, lambda-underdog:v2 deployed to Deis
               http://lambda-underdog.artitrack.com
               To learn more, use `deis help` or visit http://deis.io
        To ssh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Uygulama çalışıp çalışmadığını doğrulayın:
   
        curl -S http://[your application name].[your domain]
   Şunu görmeniz gerekir:
   
        Welcome to Deis!
        See the documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list to get the name of your application).
   <p />
10. Ölçek uygulama 3 örnekleri:
    
        deis scale cmd=3
    <p />
11. Kullanabileceğiniz isteğe bağlı olarak, uygulamanızın ayrıntılarını incelemek için bilgi deis. Aşağıdaki çıktıları my uygulaması dağıtımından şunlardır:
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>Sonraki Adımlar
Yeni bir sağlamak için tüm adımları gitti bu makalede Azure Resource Manager şablonu kullanarak azure'da küme Deis. Şablonu, Yük Dengeleme dağıtılan uygulamalar için yanı sıra bağlantıları tooling içinde artıklık destekler. Genel IP'ler değerli genel IP kaynakları kaydeder ve uygulamalarını barındırmak için daha güvenli bir ortam sağlayan üye düğümleri kullanarak şablonu de önler. Daha fazla bilgi için aşağıdaki makalelere bakın:

[Azure Resource Manager'a genel bakış][resource-group-overview]  
[Azure CLI kullanma][azure-command-line-tools]  
[Azure Resource Manager ile Azure PowerShell'i kullanma][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
