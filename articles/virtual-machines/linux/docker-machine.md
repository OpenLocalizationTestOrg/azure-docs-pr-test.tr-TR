---
title: "aaaUse Docker makine toocreate Linux barındıran Azure'da | Microsoft Docs"
description: "Azure'da toouse Docker makine toocreate Docker nasıl barındıran açıklar."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a>Azure'da toouse Docker makine toocreate nasıl barındırır
Bu makale ayrıntıları nasıl toouse [Docker makine](https://docs.docker.com/machine/) Azure toocreate konakların. Merhaba `docker-machine` komutu Azure'da bir Linux sanal makine (VM) oluşturur sonra Docker yükler. Daha sonra Azure kullanarak Docker ana bilgisayarları yönetebilirsiniz hello aynı yerel araçlarını ve iş akışları.

## <a name="create-vms-with-docker-machine"></a>Docker makineyle VM'ler oluşturma
İlk olarak, Azure abonelik Kimliğinizi elde [az hesabı Göster](/cli/azure/account#show) gibi:

```azurecli
sub=$(az account show --query "id" -o tsv)
```

Azure ile Docker ana bilgisayar sanal makineleri oluşturmak `docker-machine create` belirterek *azure* hello sürücü olarak. Daha fazla bilgi için bkz: Merhaba [Docker Azure sürücü belgeleri](https://docs.docker.com/machine/drivers/azure/)

Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM*, adlı bir kullanıcı hesabı oluşturur *azureuser*ve bağlantı noktası açar *80* hello üzerinde VM ana bilgisayar. Tooyour Azure hesabı içinde tüm komut istemlerini toolog izleyin ve Docker makine izinleri toocreate vermek ve kaynaklarını yönetme.

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

Hello çıkış benzer toohello örnek aşağıdaki gibidir:

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a>Docker Kabuk yapılandırın
tooconnect tooyour Docker ana, azure'da hello uygun bağlantı ayarlarını tanımlayın. Merhaba hello çıktının sonunda belirtildiği gibi Docker ana bilgisayarınız hello bağlantı bilgilerini aşağıdaki gibi görüntüleyin: 

```bash
docker-machine env myvmdocker
```

Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

Her iki çalışma hello yapabilecekleriniz toodefine hello bağlantı ayarlarını yapılandırma komut önerilen (`eval $(docker-machine env myvmdocker)`), ya da el ile Merhaba ortam değişkenlerini ayarlayabilirsiniz. 

## <a name="run-a-container"></a>Bir kapsayıcı çalıştırın
toosee eylem içinde bir kapsayıcı sağlar temel NGINX Web çalıştırın. İle bir kapsayıcı oluşturmak `docker run` ve bağlantı noktası 80 web trafiği için aşağıdaki gibi açın:

```bash
docker run -d -p 80:80 --restart=always nginx
```

Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

Çalışan kapsayıcılar ile Görünüm `docker ps`. Merhaba aşağıdaki örnek çıkış 80 kullanıma sunulan bağlantı noktası ile çalışan hello NGINX kapsayıcısı gösterir:

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a>Test hello kapsayıcısı
Docker ana bilgisayarın Hello ortak IP adresi aşağıdaki gibi alın:


```bash
docker-machine ip myvmdocker
```

toosee hello kapsayıcı eylem, bir web tarayıcısı açın ve komut önceki hello hello çıktısında not ettiğiniz hello ortak IP adresini girin:

![Çalışan ngnix kapsayıcı](./media/docker-machine/nginx.png)

## <a name="next-steps"></a>Sonraki adımlar
Ana bilgisayarlar ile Merhaba oluşturabilirsiniz [Docker VM uzantısı](dockerextension.md). Docker Compose kullanarak ile ilgili örnekler için bkz: [Docker ve azure'da oluşturma kullanmaya başlama](docker-compose-quickstart.md).
