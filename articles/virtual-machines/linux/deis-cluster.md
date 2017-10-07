---
title: "3 düğümü Deis aaaDeploy küme | Microsoft Docs"
description: "Bu makalede nasıl toocreate 3 düğümü Deis bir Azure Resource Manager şablonu kullanarak azure'da küme"
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
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>3 düğümünü yapılandırmak ve dağıtmak Azure kümesinde Deis
Bu makalede, sağlama aracılığıyla anlatan bir [Deis](http://deis.io/) Azure kümede. Merhaba gerekli sertifikaları toodeploying oluşturma ve bir örnek ölçeklendirme hello adımların tümünü kapsayan **Git** hello yeni sağlanan kümede uygulama.

Merhaba Aşağıdaki diyagramda dağıtılan hello sistemin hello mimarisi gösterilmektedir. Küme hello kullanarak bir Sistem Yöneticisi yönetir araçları gibi Deis **deis** ve **deisctl**. Bağlantıları hello bağlantıları tooone hello üyesinin hello küme düğümlerinde ileten bir Azure yük dengeleyici üzerinden kurulur. Merhaba istemcileri erişim uygulamalar da hello yük dengeleyici aracılığıyla dağıtılan. Bu durumda, hello yük dengeleyici hello trafiği tooa iletir daha fazla trafik toocorresponding Docker kapsayıcıları hello kümede barındırılan routs yönlendirici kafes Deis.

  ![Dağıtılan Desis küme mimarisi diyagramı](./media/deis-cluster/architecture-overview.png)

Aşağıdaki adımları hello aracılığıyla sipariş toorun ihtiyacınız vardır:

* Etkin bir Azure aboneliği. Yoksa, ücretsiz izi alma [azure.com](https://azure.microsoft.com/).
* Bir iş veya Okul kimlik toouse Azure kaynak gruplarını. Kişisel hesap ve bir Microsoft kimliğiyle günlük varsa, çok ihtiyacınız[bir iş kimliği, kişisel sunudan oluşturma](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Ya da--istemci işletim sistemine bağlı olarak--hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) veya hello [Mac, Linux ve Windows için Azure CLI](../../cli-install-nodejs.md).
* [OpenSSL](https://www.openssl.org/). OpenSSL kullanılan toogenerate hello gerekli sertifikaları olur.
* Git istemci gibi [Git Bash](https://git-scm.com/).
* tootest Merhaba örnek uygulaması, bir DNS sunucusu gerekir. Herhangi bir DNS sunucuları veya joker karakter A kayıtlarını destekleyen Hizmetleri'ni kullanabilirsiniz.
* Bir bilgisayar toorun istemci araçları Deis. Yerel makine veya sanal makine kullanabilirsiniz. Neredeyse her Linux dağıtım noktasında bu araçları çalıştırabilirsiniz ancak hello aşağıdaki yönergeleri kullanın Ubuntu.

## <a name="provision-hello-cluster"></a>Sağlama hello küme
Bu bölümde, kullanacağınız bir [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) hello açık kaynak havuzu şablonu [azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates). İlk olarak, hello şablonu kopyalayın. Ardından, kimlik doğrulama için yeni bir SSH anahtar çifti oluşturacaksınız. Ve daha sonra küme için yeni bir tanımlayıcı yapılandıracaksınız. Ve son olarak, hello Kabuk betiği veya hello PowerShell komut dosyası tooprovision hello küme kullanacaksınız.

1. Kopya hello deposu: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Toohello şablon klasöre gidin:
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. SSH-keygen kullanarak yeni bir SSH anahtar çifti oluşturun:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Özel anahtarı yukarıda Hello kullanarak bir sertifika oluşturun:
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. Çok Git[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate yeni bir küme belirteç görünen şuna benzer:
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Her CoreOS küme toohave bu ücretsiz hizmetinden benzersiz bir belirteç gerekiyor. Lütfen bakın [CoreOS belgelerine](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) daha fazla ayrıntı için.
6. Merhaba değiştirme **bulut config.yaml** tooreplace hello varolan dosya **bulma** hello yeni belirteci ile belirteci:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Merhaba değiştirme **azuredeploy-parameters.json** dosya: bir metin düzenleyicisinde 4. adımda oluşturduğunuz açık hello sertifika. Arasındaki tüm metni kopyalayın `----BEGIN CERTIFICATE-----` ve `-----END CERTIFICATE-----` hello içine **sshKeyData** (gerekir tooremove tüm satırbaşı karakterlerini) parametre.
8. Merhaba değiştirme **newStorageAccountName** parametresi. VM OS diskler için depolama hesabı hello budur. Bu hesap adı toobe genel benzersiz sahiptir.
9. Merhaba değiştirme **publicDomainName** parametresi. Bu hello yük dengeleyici genel IP ile ilişkili hello DNS adının bir parçası olur. Merhaba son FQDN hello biçimi olacaktır *[Bu parametrenin değeri]*. *[Bölge]* . cloudapp.azure.com. Örneğin, deishbai32 hello adı belirtin ve hello kaynak grubu dağıtılan toohello Batı ABD bölgesi sonra hello son ise FQDN tooyour yük dengeleyici deishbai32.westus.cloudapp.azure.com olabilir.
10. Merhaba parametre dosyasını kaydedin. Ve ardından Azure PowerShell kullanarak hello küme sağlayabilirsiniz:
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    veya Azure CLI:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Merhaba kaynak grubu sağlandıktan sonra Azure Klasik portalında hello gruptaki tüm hello kaynakların görebilirsiniz. Aşağıdaki ekran, hello hello kaynak grubu içeren bir sanal ağ üç VM'ler ile gösterildiği gibi toohello birleştirilir aynı kullanılabilirlik kümesi. Merhaba grubunun ilişkili bir ortak IP sahip bir yük dengeleyici de içerir.
    
    ![Klasik Azure portalı üzerinde Hello sağlanan kaynak grubu](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Merhaba istemcisini yükleme
Gereksinim duyduğunuz **deisctl** toocontrol, küme Deis. Deisctl tüm hello küme düğümlerinde otomatik olarak yüklenir ancak ayrı bir yönetim makinede iyi bir uygulama toouse deisctl var. Ayrıca, tüm düğümler yalnızca özel IP adresleriyle yapılandırılmış olmadığından toouse tooconnect toohello düğümü makineler ortak bir IP hello yük dengeleyici ile SSH tünel gerekir. Merhaba aşağıdaki deisctl ayrı bir Ubuntu fiziksel veya sanal makine kurma hello adımlardır.

1. Yükleme deisctl:mkdir deis
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. Özel anahtar toossh aracınızı ekleyin:
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. Deisctl yapılandırın:
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

Merhaba şablonu tanımlar 2223 tooinstance 1, eşleme gelen NAT kuralları 2224 tooinstance 2 ve 3 2225 tooinstance. Bu, hello deisctl aracını kullanmak için artıklık sağlar. Klasik Azure portalı aşağıdaki kurallara inceleyebilirsiniz:

![Merhaba yük dengeleyicisi NAT kuralları](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> Şu anda hello şablonu yalnızca 3 düğümlü kümeler destekler. Azure Resource Manager şablonu döngü sözdizimi desteklemiyor NAT kuralı tanımını uygulamasındaki bir sınırlama nedeniyle budur.
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>Yükleme ve hello Başlat platform Deis
Deisctl tooinstall kullanın ve hello Başlat artık platform Deis:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Başlangıç hello platform biraz zaman alır (10 dakika kadar). Özellikle, hello Oluşturucu hizmeti başlatılıyor uzun zaman alabilir. Ve bazen birkaç denemeden toosucceed sürer: hello işlemi toohang görünüyorsa, yazmayı deneyin `ctrl+c` toobreak yürütülmesi hello komutu ve yeniden deneyin.
> 
> 

Kullanabileceğiniz `deisctl list` tüm hizmetleri çalıştırılıyorsa tooverify:

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

Tebrikler! Çalışan bir olduğuna artık Azure üzerinde clsuter Deis! Ardından, şimdi örnek Git uygulama toosee hello eylem kümede dağıtın.

## <a name="deploy-and-scale-a-hello-world-application"></a>Dağıtma ve Hello World uygulama ölçeklendirme
Merhaba aşağıdaki adımları nasıl toodeploy "Hello World" Git Göster uygulama toohello kümesi. Merhaba adımları temel [belgelerine Deis](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Merhaba yönlendirme kafes toowork için düzgün şekilde hello yük dengeleyicinin genel IP toohello işaret eden etki alanınız için toohave bir joker karakter A kaydı gerekir. Merhaba aşağıdaki ekran görüntüsü bir örnek etki alanı kaydı için hello A kaydı üzerinde GoDaddy gösterir:
   
    ![Godaddy A kaydı](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Yükleme deis:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Yeni bir SSH anahtarı oluşturun ve sonra hello ortak anahtar tooGitHub ekleyin (doğal olarak, aynı zamanda mevcut anahtarlarınızı yeniden kullanabilirsiniz). Yeni bir SSH anahtar çifti, toocreate kullanın:
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. İd_rsa.pub veya tercih ettiğiniz, tooGitHub hello ortak anahtarı ekleyin. Bu, SSH anahtarları yapılandırma ekranında hello eklemek SSH anahtar düğmesini kullanarak yapabilirsiniz:
   
   ![GitHub anahtarı](./media/deis-cluster/github-key.png)
   
   <p />
5. Yeni bir kullanıcı kaydedin:
   
        deis register http://deis.[your domain]
   <p />
6. Merhaba SSH anahtarını ekleyin:
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. Bir uygulama oluşturun.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.Merhaba git itme, birkaç dakika sürer oluşturulan ve dağıtılan, Docker görüntüleri toobe tetikler. My deneyimlerden bazen, adım 10 (Pushing görüntü tooprivate depo) kilitlenebilir. Bu gerçekleştiğinde, hello işlemi durdurabilirsiniz Kaldır hello kullanılarak uygulama ' uygulamaları deis: – a destroy <application name> ` tooremove hello application and try again. You can use `apps:list deis' toofind uygulamanızın hello adı çıkışı. Her şeyi işe yararsa komut çıktılarını hello sonunda hello aşağıdaki gibi bir şey görmeniz gerekir:
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Merhaba uygulaması çalışıp çalışmadığını doğrulayın:
   
        curl -S http://[your application name].[your domain]
   Şunu görmeniz gerekir:
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. Ölçek hello uygulama too3 örnekleri:
    
        deis scale cmd=3
    <p />
11. İsteğe bağlı olarak kullanabileceğiniz bilgi tooexamine Ayrıntılar, uygulamanızın deis. Merhaba aşağıdaki çıktıları my uygulaması dağıtımından şunlardır:
    
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
Yeni bir Deis tüm hello adımları tooprovision gitti bu makalede Azure Resource Manager şablonu kullanarak azure'da küme. Merhaba şablonu Yük Dengeleme dağıtılan uygulamalar için yanı sıra bağlantıları tooling içinde artıklık destekler. Genel IP'ler değerli genel IP kaynakları kaydeder ve toohost uygulamaları daha güvenli bir ortam sağlayan üye düğümlerinde kullanarak Hello şablon de önler. toolearn daha makaleler hello bakın:

[Azure Resource Manager'a genel bakış][resource-group-overview]  
[Nasıl toouse hello Azure CLI][azure-command-line-tools]  
[Azure Resource Manager ile Azure PowerShell'i kullanma][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
