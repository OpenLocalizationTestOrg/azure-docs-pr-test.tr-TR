---
title: "aaaCreate Docker barındıran Docker makine ile azure'da | Microsoft Docs"
description: "Docker toocreate docker makineler Azure kullanımını açıklar."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Docker-Machine ile Azure’da Docker Ana Bilgisayarları Oluşturma
Çalışan [Docker](https://www.docker.com/) kapsayıcıları konak VM çalışan hello docker daemon gerektirir.
Bu konuda açıklanmaktadır nasıl toouse hello [docker makine](https://docs.docker.com/machine/) toocreate yeni Linux VM'ler, yapılandırılmış ile Merhaba Docker arka plan programı, Azure'da çalışan komutu. 

**Not:** 

* *Bu makalede docker makine sürüm 0.9.0-rc2 ya da büyük bağlıdır*
* *Windows kapsayıcıları docker-makine hello yakın zaman içinde aracılığıyla desteklenir*

## <a name="create-vms-with-docker-machine"></a>Docker makineyle VM'ler oluşturma
Docker ana bilgisayar sanal makineleri Azure'da hello ile oluşturma `docker-machine create` hello kullanarak komutu `azure` sürücü. 

Hello Azure sürücüsü, abonelik kimliği gereklidir. Merhaba kullanabilirsiniz [Azure CLI](cli-install-nodejs.md) veya hello [Azure Portal](https://portal.azure.com) tooretrieve Azure aboneliğinizi. 

**Hello Azure Portal kullanarak**

* Seçin **abonelikleri** hello sol gezinti sayfası ve kopyalama hello abonelik kimliğine.

**Hello Azure CLI kullanma**

* Tür ```azure account list``` ve kopyalama hello abonelik kimliği.

Tür `docker-machine create --driver azure` toosee hello seçenekleri ve varsayılan değerleri.
Merhaba de görebilirsiniz [Docker Azure sürücü belgelerine](https://docs.docker.com/machine/drivers/azure/) daha fazla bilgi için. 

Merhaba aşağıdaki örnek dayanır hello [varsayılan değerlerin](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), ancak isteğe bağlı olarak bu değerleri ayarlayın: 

* Azure dns hello genel IP ile ilişkili hello adı ve oluşturulan sertifikaları için. Sanal makinenizin hello DNS adı budur. Hello VM sonra güvenli bir şekilde Durdur, hello dinamik IP bırakın ve hello vm ile yeni bir IP yeniden başlatıldıktan sonra hello özelliği tooreconnect sağlayın. Merhaba adı ön eki Bu bölge UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com benzersiz olması gerekir.
* Merhaba VM giden internet erişimi için bağlantı noktası 80'i açın
* Merhaba VM tooutilize daha hızlı premium depolama boyutu
* premium depolama Hello vm disk için kullanılır

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Docker docker makineyle seçin
Docker-makine konağınız için bir giriş olduktan sonra docker komutlarını çalıştırırken hello varsayılan ana bilgisayar ayarlayabilirsiniz.

## <a name="using-powershell"></a>PowerShell’i kullanma
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Bash kullanma
```bash
eval $(docker-machine env MyDockerHost)
```

Şimdi docker komutları hello belirtilen konak karşı çalıştırabilirsiniz

```
docker ps
docker info
```

## <a name="run-a-container"></a>Bir kapsayıcı çalıştırın
Yapılandırılmış olan bir konak ana bilgisayarınız doğru yapılandırılmış olup olmadığını basit bir web sunucusu tootest şimdi çalıştırabilirsiniz.
Burada bir standart nginx yansıması kullanın, bağlantı noktası 80 üzerinde dinleme yapması gerektiğini belirtin ve hello konak VM yeniden başlatılırsa, hello kapsayıcı olur de yeniden (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

Merhaba çıktı hello aşağıdaki gibi görünmelidir:

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>Test hello kapsayıcısı
Kullanarak çalışan kapsayıcılar inceleyin `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

Ve, kapsayıcı türü çalıştıran toosee hello `docker-machine ip <VM name>` toofind başlangıç IP adresi tooenter hello tarayıcıda:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Çalışan ngnix kapsayıcı](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Özet
Docker-makineyle Azure docker ana bilgisayarlar için ayrı ayrı docker ana doğrulamaları kolayca sağlayabilirsiniz.
İçin üretim hello bkz kapsayıcıları için barındırma [Azure kapsayıcı hizmeti](http://aka.ms/AzureContainerService)

Visual Studio .NET Core uygulamalarla toodevelop bakın [Visual Studio için Docker araçları](http://aka.ms/DockerToolsForVS)

