---
title: "hello Azure CLI 1.0 ile aaaUse hello Azure Docker VM uzantısı | Microsoft Docs"
description: "Nasıl toouse Docker VM uzantısı tooquickly hello ve güvenli bir şekilde Azure Resource Manager şablonları kullanarak Docker bir ortamda dağıtmak öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a>Merhaba Docker VM uzantısı hello Azure CLI 1.0 ile kullanarak azure'da bir Docker ortam oluşturma
Docker popüler kapsayıcı yönetimi ve kapsayıcıları Linux (ve Windows da) ile tooquickly çalışma sağlayan görüntüleme platform ' dir. Azure'da, Docker tooyour gereksinimlerine göre dağıtabileceğiniz çeşitli yolları vardır. Bu makalede hello Docker VM uzantısı ve Azure Resource Manager şablonları kullanarak odaklanır. 

Docker makine ve Azure kapsayıcı hizmetlerini kullanma dahil olmak üzere hello farklı dağıtım yöntemleri hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* tooquickly prototip bir uygulama kullanarak tek bir Docker ana oluşturabilirsiniz [Docker makine](docker-machine.md).
* Daha büyük ve daha kararlı ortamlar için de destekler hello Azure Docker VM uzantısı kullanabileceğiniz [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate tutarlı kapsayıcı dağıtımlarını. Bu makale Hello Azure Docker VM uzantısı kullanılarak ayrıntıları.
* dağıtabileceğiniz ek planlama ve yönetim araçları sağlayan toobuild üretime hazır, ölçeklenebilir ortamlar, bir [Azure kapsayıcı hizmetlerini Docker Swarm kümesinde](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#azure-docker-vm-extension-overview) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](dockerextension.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için 

## <a name="azure-docker-vm-extension-overview"></a>Azure Docker VM uzantısı genel bakış
Hello Azure Docker VM uzantısı yükler ve hello Docker arka plan programı, Docker istemcisi ve Docker Compose, Linux sanal makine (VM) yapılandırır. Hello Azure Docker VM uzantısı kullanarak, daha fazla denetim ve yalnızca Docker makine kullanarak veya kendiniz hello Docker ana oluşturarak daha özelliklere sahip. Gibi bu ek özellikler [Docker Compose](https://docs.docker.com/compose/overview/), daha sağlam geliştirici veya üretim ortamları için uygun hello Azure Docker VM uzantısı olun.

Azure Resource Manager şablonları hello tüm ortamınızın yapısını tanımlar. Şablonları toocreate izin ver ve hello Docker ana bilgisayar sanal makineleri, depolama, rol tabanlı erişim denetimi (RBAC) ve tanılama gibi kaynakları yapılandırın. Bu şablonlar toocreate ek dağıtımlar tutarlı bir şekilde yeniden kullanabilirsiniz. Azure Resource Manager ve şablonları hakkında daha fazla bilgi için bkz: [Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md). 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Şablon hello Azure Docker VM uzantısı ile dağıtma
Şimdi var olan bir Hızlı Başlangıç şablonu toocreate hello Azure Docker VM uzantısı tooinstall kullanan bir Ubuntu VM kullanın ve hello Docker ana yapılandırın. Merhaba şablon burada görüntüleyebilirsiniz: [basit bir Ubuntu VM docker'la dağıtımını](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Merhaba gereksinim [en son Azure CLI](../../cli-install-nodejs.md) yüklü ve aşağıdaki gibi hello Resource Manager modunu kullanarak oturum:

```azurecli
azure config mode arm
```

Merhaba hello şablon URI belirtme Azure CLI kullanarak hello şablonunu dağıtın. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westus* konumu. Kendi kaynak grubu adı ve konumu aşağıdaki şekilde kullanın:

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Depolama hesabınız Hello istemleri tooname yanıt, bir kullanıcı adı ve parola girin ve bir DNS adını belirtin. Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Hello Azure CLI yalnızca birkaç saniye sonra toohello istemi verir, ancak Docker ana bilgisayarınız hala oluşturuluyor ve Azure Docker VM uzantısı tarafından hello yapılandırılmış. Merhaba dağıtım toofinish birkaç dakika sürer. Hello kullanarak hello Docker ana bilgisayar durumunu ilgili ayrıntıları görüntüleyebilirsiniz `azure vm show` komutu.

Merhaba aşağıdaki örnek hello durumunu hello adlı VM denetler *myDockerVM* (Merhaba hello şablondan varsayılan adı - bu adı değiştirmemeniz) adlı hello kaynak grubunda *myResourceGroup*. Merhaba hello önceki adımda oluşturduğunuz hello kaynak grubunun adını girin:

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

Merhaba hello çıktısını `azure vm show` benzer toohello izlemektir örnek komut:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

Hello gördüğünüz hello Çıktı Hello yukarıya yakın **ProvisioningState** hello VM. Bu görüntülendiğinde *başarılı*hello dağıtımı tamamlandı ve SSH toohello VM kullanabilirsiniz.

Merhaba çıktı hello sonuna doğru *FQDN* Docker ana bilgisayarınız hello tam etki alanı adını görüntüler. Bu FQDN, kullandığınız olan adımları kalan hello tooSSH tooyour Docker ana bilgisayar.

## <a name="deploy-your-first-nginx-container"></a>İlk nginx kapsayıcısı dağıtma
Bir kez hello dağıtımı tamamlandı, SSH tooyour yeni Docker ana yerel bilgisayarınızdan. Kullanıcı adınızı ve FQDN şu şekilde girin:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

Şimdi toohello Docker ana oturum sonra bir nginx kapsayıcısı çalıştırın:

```bash
sudo docker run -d -p 80:80 nginx
```

Merhaba nginx görüntü indirilen olarak aşağıdaki örneğine benzer toohello ve başlatılan bir kapsayıcı Hello çıktısı şöyledir:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Aşağıdaki gibi Docker ana bilgisayarında çalışan Merhaba kapsayıcılara Hello durumunu kontrol edin:

```bash
sudo docker ps
```

Merhaba çıktı aşağıdaki örneğine benzer toohello, o hello nginx kapsayıcısı gösteren çalıştığını ve 80 ve 443 numaralı TCP bağlantı noktaları ve iletilen:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

Eylem, kapsayıcıyı toosee açın yukarı bir web tarayıcısı ve hello FQDN, Docker ana bilgisayar adını girin:

![Çalışan ngnix kapsayıcı](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Azure Docker VM uzantısı şablon başvurusu
Merhaba önceki örneği var olan bir Hızlı Başlangıç şablonu kullanır. Ayrıca kendi Resource Manager şablonları ile hello Azure Docker VM uzantısı dağıtabilirsiniz. toodo, bu nedenle, tooyour Resource Manager şablonları aşağıdaki, hello tanımlama hello ekleyin *vmName* vm'nizin uygun şekilde:

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

İzlenecek okuyarak Resource Manager şablonları kullanma hakkında daha ayrıntılı bulabilirsiniz [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).

## <a name="next-steps"></a>Sonraki adımlar
Çok isteyebilir[hello Docker arka plan programı TCP bağlantı noktası](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), anlamak [Docker güvenlik](https://docs.docker.com/engine/security/security/), veya kullanarak kapsayıcıları dağıtma [Docker Compose](https://docs.docker.com/compose/overview/). Merhaba hello Azure Docker VM uzantısı kendisi hakkında daha fazla bilgi için bkz: [GitHub proje](https://github.com/Azure/azure-docker-extension/).

Merhaba ek Docker dağıtım seçenekleri Azure hakkında daha fazla bilgi okuyun:

* [Docker makine hello Azure sürücüsü ile kullanma](docker-machine.md)  
* [Docker ile çalışmaya başlama ve toodefine oluşturma ve birden çok kapsayıcı uygulaması bir Azure sanal makine üzerinde çalışan](docker-compose-quickstart.md).
* [Azure Container Service kümesi dağıtma](../../container-service/dcos-swarm/container-service-deployment.md)

