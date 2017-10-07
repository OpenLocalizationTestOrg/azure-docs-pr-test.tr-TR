---
title: "Linux için Docker VM uzantısı aaaUsing | Microsoft Docs"
description: "Docker ve hello Azure sanal makine uzantıları ve nasıl toocreate kullanarak docker ana bilgisayarları Azure sanal makineleri hello Azure CLI Klasik dağıtım modelinde açıklar."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>Merhaba Docker VM uzantısı hello Klasik Azure portalı ile kullanma
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

[Docker](https://www.docker.com/) hello kullanır en popüler sanallaştırma yaklaşımlardan biri [Linux kapsayıcıları](http://en.wikipedia.org/wiki/LXC) verileri yalıtarak ve bilgi işlem paylaşılan kaynakları üzerinde bir yolu olarak sanal makineleri yerine. Merhaba Docker VM uzantısı tarafından yönetilen kullanabilirsiniz [Azure Linux Aracısı] toocreate kapsayıcıları uygulamalarınızın Azure ile ilgili herhangi bir sayıda barındıran bir Docker VM.

> [!NOTE]
> Bu konuda nasıl toocreate Docker sanal makineden bir hello Klasik Azure portalı açıklanmaktadır. toocreate Docker VM hello komut satırında nasıl görürüm toosee [nasıl toouse hello Docker VM uzantısı hello Azure komut satırı arabirimi (Azure CLI)]. toosee kapsayıcıları ve bunların avantajları üst düzey bir tartışma bkz hello [Docker yüksek düzey Beyaz Tahta](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Resim Galerisi hello yeni bir VM oluşturun
Merhaba ilk adım bir Azure VM hello Docker VM uzantısı, Ubuntu 14.04 LTS görüntüden hello görüntü Galerisi örneği sunucu görüntüsünü ve Ubuntu 14.04 masaüstü istemci olarak kullanarak destekleyen Linux görüntüsünden gerektirir. Merhaba Portalı'nda tıklatın **+ yeni** hello köşe toocreate yeni bir VM örneği sol alt ve bir Ubuntu 14.04 LTS görüntü hello seçim yok ya da hello seçin görüntü Galerisi, aşağıda gösterildiği gibi tamamlayın.

> [!NOTE]
> Şu anda yalnızca Temmuz 2014'den daha yeni Ubuntu 14.04 LTS görüntüleri hello Docker VM uzantısı destekler.
> 
> 

![Yeni bir Ubuntu görüntüsü oluşturma](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Docker sertifikaları oluşturma
Hello VM oluşturulduktan sonra Docker istemci bilgisayarınızda yüklü olduğundan emin olun. (Ayrıntılar için bkz [Docker yükleme yönergeleri](https://docs.docker.com/installation/#installation).)

Merhaba çok göre Docker iletişimi için sertifika ve anahtar dosyaları oluşturma[çalıştıran Docker https ile] ve hello yerleştirin  **`~/.docker`**  istemci bilgisayarınızda dizin.

> [!NOTE]
> Hello Docker VM uzantısı hello portal şu anda base64 ile kodlanmış kimlik bilgileri gerektirir.
> 
> 

Merhaba komut satırında kullanın  **`base64`**  veya başka bir sık kullanılan aracı toocreate base64 ile kodlanmış konuları kodlama. Basit bir sertifika ve anahtar dosyaları kümesiyle bunu benzer toothis benzeyebilir:

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>Merhaba Docker VM uzantısı Ekle
tooadd Docker VM uzantısı Merhaba, oluşturduğunuz hello VM örneği bulun ve çok ilerleyin**uzantıları** ve aşağıda gösterildiği gibi VM uzantıları, Yukarı toobring tıklayın.

> [!NOTE]
> Bu işlevsellik yalnızca hello Önizleme portalında desteklenir: https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>Bir uzantı ekleme
Merhaba tıklatın **+ Ekle** toodisplay hello olası VM uzantıları toothis VM ekleyebilirsiniz.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Merhaba Docker VM uzantısı seçin
Merhaba hello Docker açıklama ve önemli bağlantılar getirir, Docker VM uzantısı seçin ve ardından **oluşturma** hello alt toobegin hello yükleme yordamı sırasında.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>Sertifika ve anahtar dosyaları ekleyin:
Merhaba form alanlarını hello grafiği aşağıdaki gösterildiği gibi hello base64 ile kodlanmış sürümleri, CA sertifikası, sunucu sertifikası ve sunucu anahtarınızı girin.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> Not (olduğu gibi hello görüntü önceki) 2376 hello varsayılan olarak doldurulur. Herhangi bir uç nokta burada girebilirsiniz, ancak hello sonraki adıma uç nokta eşleşen hello yukarı tooopen olacaktır. Merhaba varsayılan değiştirirseniz, uç nokta hello sonraki adımda eşleşen hello yukarı emin tooopen olun.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Merhaba Docker iletişim uç noktası ekleme
Oluşturduğunuz hello kaynak grubu görüntülerken hello VM ile ilişkilendirilmiş ağ güvenlik grubu seçin ve tıklatın **gelen güvenlik kuralları** tooview hello kuralları aşağıda gösterildiği gibi.

![](media/portal-use-docker/AddingEndpoint.png)

Tıklatın **+ Ekle** tooadd başka bir kural ve hello varsayılan durumda hello uç noktası için bir ad girin (Bu örnekte, **Docker**) ve 2376 'hedef bağlantı noktası aralığı'. Merhaba Protokolü değeri gösteren ayarlamak **TCP**, tıklatıp **Tamam** toocreate hello kuralı.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Docker istemci ve Azure Docker ana test
Bulun ve kopyalama hello adı VM etki alanı ve türü, istemci bilgisayarın hello komut satırında `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (burada *dockerextension* hello tarafından değiştirildi alt etki alanı için VM).

Merhaba sonuç benzer toothis görünmelidir:

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

Merhaba yukarıdaki adımları tamamladıktan sonra yapılandırılan bir Azure VM üzerinde çalışan tam olarak işlevsel bir Docker ana bilgisayar artık yüklü toobe diğer istemcilerinden tooremotely bağlı.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
Hazır toogo toohello olduğunuz [Docker Kullanıcı Kılavuzu] ve Docker VM kullanın. Tooautomate Docker ana bilgisayarları Azure Vm'lerinde komut satırı arabirimi kullanarak oluşturmak istiyorsanız, bkz: [nasıl toouse hello Docker VM uzantısı hello Azure komut satırı arabirimi (Azure CLI)]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[nasıl toouse hello Docker VM uzantısı hello Azure komut satırı arabirimi (Azure CLI)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[Azure Linux Aracısı]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[çalıştıran Docker https ile]:http://docs.docker.com/articles/https/
[Docker Kullanıcı Kılavuzu]:https://docs.docker.com/userguide/
