---
title: "aaaUse hello Azure Docker VM uzantısı | Microsoft Docs"
description: "Nasıl toouse Docker VM uzantısı tooquickly hello ve güvenli bir şekilde Azure Resource Manager şablonları kullanarak Docker bir ortamda dağıtmak ve Azure CLI 2.0 hello öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a>Azure'da hello Docker VM uzantısı kullanarak bir Docker ortam oluşturma
Docker popüler kapsayıcı yönetimi ve kapsayıcıları tooquickly çalışmak Linux'ta verir görüntüleme platform ' dir. Azure'da, Docker tooyour gereksinimlerine göre dağıtabileceğiniz çeşitli yolları vardır. Bu makalede, Azure CLI 2.0 hello ile Merhaba Docker VM uzantısı ve Azure Resource Manager şablonları kullanarak odaklanır. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Azure Docker VM uzantısı genel bakış
Hello Azure Docker VM uzantısı yükler ve hello Docker arka plan programı, Docker istemcisi ve Docker Compose, Linux sanal makine (VM) yapılandırır. Hello Azure Docker VM uzantısı kullanarak, daha fazla denetim ve yalnızca Docker makine kullanarak veya kendiniz hello Docker ana oluşturarak daha özelliklere sahip. Gibi bu ek özellikler [Docker Compose](https://docs.docker.com/compose/overview/), daha sağlam geliştirici veya üretim ortamları için uygun hello Azure Docker VM uzantısı olun.

Docker makine ve Azure kapsayıcı hizmetlerini kullanma dahil olmak üzere hello farklı dağıtım yöntemleri hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* tooquickly prototip bir uygulama kullanarak tek bir Docker ana oluşturabilirsiniz [Docker makine](docker-machine.md).
* dağıtabileceğiniz ek planlama ve yönetim araçları sağlayan toobuild üretime hazır, ölçeklenebilir ortamlar, bir [Azure kapsayıcı hizmetlerini Docker Swarm kümesinde](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Şablon hello Azure Docker VM uzantısı ile dağıtma
Şimdi var olan bir Hızlı Başlangıç şablonu toocreate hello Azure Docker VM uzantısı tooinstall kullanan bir Ubuntu VM kullanın ve hello Docker ana yapılandırın. Merhaba şablon burada görüntüleyebilirsiniz: [basit bir Ubuntu VM docker'la dağıtımını](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Merhaba son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westus* konumu:

```azurecli
az group create --name myResourceGroup --location westus
```

Ardından, bir VM'yi dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) hello Azure Docker VM uzantısını içeren [github'daki bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Kendi değerlerini sağlamanız *newStorageAccountName*, *adminUsername*, *Admınpassword*, ve *dnsNameForPublicIP* gibi:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Merhaba dağıtım toofinish birkaç dakika sürer. Merhaba dağıtım tamamlandıktan sonra [toonext adım taşıma](#deploy-your-first-nginx-container) tooSSH tooyour VM. 

İsteğe bağlı olarak tooinstead dönüş denetimi toohello istemi ve let hello dağıtım hello arka planda devam hello ekleyin `--no-wait` komutu önceki toohello bayrak. Bu işlem tooperform sağlar hello hello dağıtım için bir kaç dakika devam ederken CLI diğer iş. 

Ardından hello Docker ana bilgisayar durumu ile ilgili ayrıntıları görüntüleyebilirsiniz [az vm Göster](/cli/azure/vm#show). Merhaba aşağıdaki örnek hello durumunu hello adlı VM denetler *myDockerVM* (Merhaba hello şablondan varsayılan adı - bu adı değiştirmemeniz) adlı hello kaynak grubunda *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Bu komut döndüğünde *başarılı*hello dağıtımı tamamlandı ve SSH toohello VM adım aşağıdaki hello de kullanabilirsiniz.

## <a name="deploy-your-first-nginx-container"></a>İlk nginx kapsayıcısı dağıtma
tooview ayrıntıları dahil olmak üzere hello DNS adı, vm'nizin `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. SSH tooyour yeni Docker ana bilgisayar yerel bilgisayarınızdan gibi:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
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

Eylem, kapsayıcıyı toosee açın yukarı bir web tarayıcısı ve Docker ana bilgisayarınız hello DNS adını girin:

![Çalışan ngnix kapsayıcı](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Azure Docker VM uzantısı şablon başvurusu
Merhaba önceki örneği var olan bir Hızlı Başlangıç şablonu kullanır. Ayrıca kendi Resource Manager şablonları ile hello Azure Docker VM uzantısı dağıtabilirsiniz. toodo, bu nedenle, tooyour Resource Manager şablonları aşağıdaki, hello tanımlama hello ekleyin `vmName` vm'nizin uygun şekilde:

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
    "typeHandlerVersion": "1.*",
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

