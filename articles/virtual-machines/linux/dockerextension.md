---
title: "Azure Docker VM uzantısını kullanan | Microsoft Docs"
description: "Docker VM uzantısı hızlı ve güvenli bir şekilde Azure Resource Manager şablonları ve Azure CLI 2.0 kullanarak Docker bir ortamda dağıtmak için nasıl kullanılacağını öğrenin"
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
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a>Docker VM uzantısı kullanarak Azure'da bir Docker ortam oluşturma
Docker popüler kapsayıcı yönetimi ve hızlı bir şekilde ile kapsayıcıları Linux üzerinde çalışmanıza olanak sağlar görüntüleme platform ' dir. Azure'da, sizin ihtiyaçlarınıza göre Docker dağıtabilirsiniz çeşitli yolları vardır. Bu makalede, Docker VM uzantısı ve Azure Resource Manager şablonları ile Azure CLI 2.0 kullanarak odaklanır. Bu adımları [Azure CLI 1.0](dockerextension-nodejs.md) ile de gerçekleştirebilirsiniz.

## <a name="azure-docker-vm-extension-overview"></a>Azure Docker VM uzantısı genel bakış
Azure Docker VM uzantısı yükler ve Docker arka plan programı, Docker istemcisi ve Docker Compose, Linux sanal makine (VM) yapılandırır. Azure Docker VM uzantısı kullanarak, daha fazla denetim ve yalnızca Docker makine kullanarak veya kendiniz Docker ana oluşturarak daha özelliklere sahip. Gibi bu ek özellikler [Docker Compose](https://docs.docker.com/compose/overview/), Azure Docker VM uzantısı daha sağlam geliştirici veya üretim ortamları için uygun olun.

Docker makine ve Azure kapsayıcı hizmetlerini kullanma dahil farklı dağıtım yöntemi hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

* Uygulama bir hızlı bir şekilde prototip için kullanarak tek bir Docker ana oluşturabilirsiniz [Docker makine](docker-machine.md).
* Ek planlama ve yönetim araçları sağlar üretime hazır, ölçeklenebilir ortamlar oluşturmak için dağıtabileceğiniz bir [Azure kapsayıcı hizmetlerini Docker Swarm kümesinde](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a>Bir şablonu Azure Docker VM uzantısı ile dağıtma
Şimdi yüklemek ve Docker ana yapılandırmak için Azure Docker VM uzantısını kullanan bir Ubuntu VM oluşturmak için var olan bir hızlı başlangıç şablonunu kullanın. Şablon burada görüntüleyebilirsiniz: [basit bir Ubuntu VM docker'la dağıtımını](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). En son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve bir Azure hesabı kullanarak oturum açmış [az oturum açma](/cli/azure/#login).

İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *westus* konumu:

```azurecli
az group create --name myResourceGroup --location westus
```

Ardından, bir VM'yi dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) Azure Docker VM uzantısını içeren [github'daki bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Kendi değerlerini sağlamanız *newStorageAccountName*, *adminUsername*, *Admınpassword*, ve *dnsNameForPublicIP* gibi:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Tamamlamak için dağıtım için birkaç dakika sürer. Dağıtım tamamlandıktan sonra [sonraki adımına geçmek](#deploy-your-first-nginx-container) SSH, VM için. 

Bunun yerine denetim komut istemini dönüp işlemi arka planda devam dağıtım izin için isteğe bağlı olarak ekleyin `--no-wait` yukarıdaki komut için bayrak. Bu işlem birkaç dakika dağıtım devam ederken diğer iş CLI işlemleri yapmanıza olanak tanır. 

Ardından Docker ana durumuyla ilgili ayrıntıları görüntüleyebilirsiniz [az vm Göster](/cli/azure/vm#show). Aşağıdaki örnek adlı VM durumunu denetler *myDockerVM* (varsayılan ad şablondan - bu adı değişmez) kaynak grubunda adlı *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Bu komut döndüğünde *başarılı*, dağıtım sona erdi ve sonraki adımda VM için SSH kullanabilirsiniz.

## <a name="deploy-your-first-nginx-container"></a>İlk nginx kapsayıcısı dağıtma
DNS adı dahil olmak üzere, VM ayrıntılarını görüntülemek için kullanın `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. Yeni Docker SSH yerel bilgisayarınızdan gibi ana bilgisayar:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Şimdi Docker ana bilgisayara oturum açtıktan sonra bir nginx kapsayıcısı çalıştırın:

```bash
sudo docker run -d -p 80:80 nginx
```

Çıktı nginx görüntü yüklenir ve bir kapsayıcı başlatıldı olarak aşağıdaki örneğe benzer:

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Aşağıdaki gibi Docker ana bilgisayarında çalışan kapsayıcılar durumunu kontrol edin:

```bash
sudo docker ps
```

Çıktı aşağıdaki örneğe benzer, nginx kapsayıcısı gösteren çalıştığını ve 80 ve 443 numaralı TCP bağlantı noktaları ve iletilen:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

Uygulamada, kapsayıcı görmek için bir web tarayıcısını açın ve Docker ana bilgisayarının DNS adını girin:

![Çalışan ngnix kapsayıcı](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Azure Docker VM uzantısı şablon başvurusu
Önceki örnekte, var olan bir Hızlı Başlangıç şablonu kullanır. Ayrıca, Azure Docker VM uzantısı kendi Resource Manager şablonları ile dağıtabilirsiniz. Bunu yapmak için aşağıdaki tanımlama, Resource Manager şablonlarınızı ekleyin `vmName` vm'nizin uygun şekilde:

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
İçin isteyebilir [Docker daemon TCP bağlantı noktası yapılandırma](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), anlamak [Docker güvenlik](https://docs.docker.com/engine/security/security/), veya kullanarak kapsayıcıları dağıtma [Docker Compose](https://docs.docker.com/compose/overview/). Azure Docker VM uzantısı kendisi hakkında daha fazla bilgi için bkz: [GitHub proje](https://github.com/Azure/azure-docker-extension/).

Azure'da ek Docker dağıtım seçenekleri hakkında daha fazla bilgi okuyun:

* [Docker makine Azure sürücüsüyle kullanın](docker-machine.md)  
* [Docker ve oluşturma tanımlamak ve bir Azure sanal makine üzerinde birden çok kapsayıcı uygulamayı çalıştırmak için kullanmaya başlama](docker-compose-quickstart.md).
* [Azure Container Service kümesi dağıtma](../../container-service/dcos-swarm/container-service-deployment.md)

