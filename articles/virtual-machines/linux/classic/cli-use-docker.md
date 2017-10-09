---
title: "aaaUsing hello Azure Linux için Docker VM uzantısı"
description: "Docker ve hello Azure sanal makine uzantıları açıklar ve nasıl tooprogrammatically sanal makineler oluşturmak docker ana hello komut satırından hello Azure CLI kullanarak azure'da gösterir."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a>Merhaba Docker VM uzantısı hello Azure komut satırı arabirimi (Azure CLI) gelen kullanma
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Merhaba Docker VM uzantısı hello Resource Manager modeli ile kullanma hakkında daha fazla bilgi için bkz: [burada](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bu konuda nasıl toocreate VM hello gelen hello Docker VM uzantısı ile Hizmet Yönetimi (asm) Azure CLI modunda herhangi bir platformda açıklanmaktadır. [Docker](https://www.docker.com/) hello kullanır en popüler sanallaştırma yaklaşımlardan biri [Linux kapsayıcıları](http://en.wikipedia.org/wiki/LXC) verileri yalıtarak ve bilgi işlem paylaşılan kaynakları üzerinde bir yolu olarak sanal makineleri yerine. Merhaba Docker VM uzantısı ve hello kullanabilirsiniz [Azure Linux Aracısı](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate kapsayıcıları uygulamalarınızın Azure ile ilgili herhangi bir sayıda barındıran bir Docker VM. toosee kapsayıcıları ve bunların avantajları üst düzey bir tartışma bkz hello [Docker yüksek düzey Beyaz Tahta](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a>Nasıl toouse hello Azure ile Docker VM uzantısı
toouse hello Docker VM uzantısı Azure ile Merhaba sürümünü yüklemeniz gerekir [Azure komut satırı arabirimi](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) değerinden daha yüksek 0.8.6 (Bu yazma Merhaba 0.10.0 geçerli sürümünde olduğu gibi). Mac, Linux ve Windows hello Azure CLI yükleyebilirsiniz.

Merhaba tam işlem toouse Azure üzerinde Docker basittir:

* Hello Azure CLI ve bağımlılıklarını toocontrol Azure istediğiniz hello bilgisayara yükleme (Windows, bu sanal makine olarak çalışan Linux dağıtım olacaktır)
* Azure'da Hello Azure CLI Docker komutları toocreate VM Docker ana kullanın
* Merhaba yerel Docker komutları toomanage Docker kapsayıcılarınızı azure'da, Docker VM kullanın.

### <a name="install-hello-azure-command-line-interface-azure-cli"></a>Hello Azure komut satırı arabirimi (Azure CLI) yükleyin
tooinstall ve hello Azure CLI yapılandırmak için bkz: [nasıl tooinstall hello Azure komut satırı arabirimi](../../../cli-install-nodejs.md). tooconfirm hello yükleme türü `azure` hello komut isteminde ve kısa bir süre sonra hello hello basic listeler Azure CLI ASCII art komutları kullanılabilir tooyou görmeniz gerekir. Merhaba yükleme doğru şekilde çalışan, mümkün tootype olmalıdır `azure help vm` ve listelenen hello komutlarından birini "docker" olduğunu görürsünüz.

> [!NOTE]
> Windows, docker sahip Araçları [Docker makine](https://docs.docker.com/installation/windows/), hangi tooautomate hello oluşturma toowork docker ana bilgisayarları olarak Azure VM ile birlikte kullanabilirsiniz docker istemcinin de kullanabilirsiniz.
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a>Hello Azure CLI tootooyour Azure hesabına bağlanma
Hello Azure CLI kullanmadan önce Azure hesabı kimlik bilgilerinizi, platformda hello Azure CLI ile ilişkilendirmeniz gerekir. Merhaba bölüm [nasıl tooconnect tooyour Azure aboneliği](../../../xplat-cli-connect.md) nasıl tooeither indirmek ve içeri aktarma açıklanmaktadır, **.publishsettings** dosya veya Azure CLI bir Kurumsal kimlik ile ilişkilendirin.

> [!NOTE]
> Bazı farklar vardır davranış birini kullanırken ya da hello diğer yöntemleri, kimlik doğrulama, bu nedenle toounderstand hello farklı işlevler yukarıda emin tooread hello belge.
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a>Docker yükleme ve başlangıç Docker VM uzantısı için Azure kullanma
Merhaba izleyin [Docker yükleme yönergeleri](https://docs.docker.com/installation/#installation) tooinstall Docker yerel olarak bilgisayarınızda.

toouse Docker ile bir Azure sanal makine, VM hello için kullanılan hello Linux görüntüsü hello olmalıdır [Azure Linux VM Aracısı](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) yüklü. Şu anda bu sağlayan görüntüleri yalnızca iki tür vardır:

* Ubuntu görüntüden hello Azure görüntü Galerisi veya
* Hello Azure Linux VM Aracısı ile oluşturulan özel bir Linux görüntü yüklenir ve yapılandırılır. Bkz: [Azure Linux VM Aracısı](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hakkında daha fazla bilgi için toobuild hello Azure VM Aracısı ile özel bir Linux VM.

### <a name="using-hello-azure-image-gallery"></a>Hello Azure görüntü Galerisi kullanma
Bir Bash veya Terminal oturumu, toolocate yazarak hello VM galeri toouse en son Ubuntu görüntüde hello Azure CLI komutu aşağıdaki hello kullanın

`azure vm image list | grep Ubuntu-14_04`

bir hello resim adları gibi seçin `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, ve kullanım hello aşağıdaki toocreate, görüntü kullanarak yeni bir VM komutu.

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

Burada:

* *&lt;VM buluthizmeti adı&gt;*  hello azure'da hello Docker kapsayıcısı ana bilgisayar olacak VM hello adıdır
* *&lt;Kullanıcı adı&gt;*  hello varsayılan kök kullanıcının hello VM, hello kullanıcı adı
* *&lt;Parola&gt;*  hello hello parolası *kullanıcıadı* Azure için karmaşıklık hello standartları karşılar hesabı

> [!NOTE]
> Parola şu anda gerekir, en az 8 karakter olmalı bir küçük harf ve bir büyük harf karakter, sayı ve aşağıdaki karakterleri hello birini gibi özel bir karakter içermelidir: `!@#$%^&+=`. Hayır, hello süresi cümle önceki hello hello sonunda bir özel karakter değil.
> 
> 

Merhaba komutu başarılı olduysa, hello kesin bağımsız değişkenleri ve kullandığınız seçenekleri bağlı olarak hello aşağıdaki gibi bir şey görmeniz gerekir:

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> Sanal makine oluşturmak birkaç dakika alabilir, ancak sonra bu için hazırlanmadı (Merhaba durumu değeri `ReadyRole`) Docker arka plan programı (Merhaba Docker hizmeti) başlatır hello ve toohello Docker kapsayıcısı ana bağlanabilir.
> 
> 

tootest hello Docker Azure, türü oluşturduğunuz VM

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

Burada  *&lt;vm-adı--kullandığınız&gt;*  , çağrıda çok kullanılan hello sanal makinenin hello adı`azure vm docker create`. Benzeri Docker ana VM çalışır durumda olduğunu belirten toohello aşağıdaki Azure'da çalışan ve komutları için bekleyen görmeniz gerekir. 

Docker istemci tooobtain bilgilerinizi kullanarak tooconnect deneyebilirsiniz artık (Mac üzerinde gibi bazı Docker istemci ayarları'nda toouse sahip olabilir `sudo`):

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

Yalnızca toobe tüm çalışma olduğunu belirli, hello VM hello Docker uzantısı için inceleyebilirsiniz:

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a>Docker ana VM kimlik doğrulaması
Ayrıca toocreating hello Docker VM hello `azure vm docker create` komutu da otomatik olarak HTTPS kullanarak Docker istemci bilgisayar tooconnect toohello Azure kapsayıcısı ana bilgisayarınız hello gerekli sertifikaları tooallow oluşturur ve hello sertifikaları hem depolanır İstemci ve ana makineler, uygun şekilde hello. Sonraki denemeler üzerinde hello varolan sertifikaları yeniden ve hello yeni ana bilgisayarla paylaşılan.

Sertifikaları yerleştirilir varsayılan olarak, `~/.docker`, ve Docker bağlantı noktasında yapılandırılmış toorun **2376**. Toouse farklı bir bağlantı veya dizin istediğiniz sonra hello aşağıdakilerden birini kullanabilir `azure vm docker create` komut satırı seçenekleri tooconfigure Docker kapsayıcısı ana VM toouse farklı bir bağlantı veya bağlanan istemciler için farklı sertifikalar:

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

Merhaba hello konak Docker arka plan için yapılandırılmış toolisten olan ve hello bağlantılarında belirtilen hello sertifikaları kullanarak bağlantı noktası hello tarafından oluşturulan istemci kimlik doğrulaması `azure vm docker create` komutu. Merhaba istemci makine bu sertifikaları toogain toohello Docker ana bilgisayarına erişim olması gerekir.

> [!NOTE]
> Bu sertifikaları olmadan çalıştıran ağa bağlı bir ana bilgisayar tooconnect toohello makine yapabilirsiniz savunmasız tooanyone olacaktır. Merhaba varsayılan yapılandırmayı değiştirmeden önce hello riskleri tooyour bilgisayarlar ve uygulamalar anladığınızdan emin olun.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Hazır toogo toohello olduğunuz [Docker Kullanıcı Kılavuzu] ve Docker VM kullanın. toocreate Docker etkin bir VM hello yeni Portalı'nda bkz [nasıl toouse hello Docker VM uzantısı hello Portal ile].
* Hello Azure Docker VM uzantısı da Docker bildirim temelli bir YAML dosya tootake Geliştirici modelli bir uygulama arasında herhangi bir ortamın kullanan Compose destekler ve tutarlı bir dağıtım oluşturun. Bkz: [Docker ile çalışmaya başlama ve toodefine oluşturma ve birden çok kapsayıcı uygulaması bir Azure sanal makine üzerinde çalışan].  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[nasıl toouse hello Docker VM uzantısı hello Portal ile]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Docker Kullanıcı Kılavuzu]:https://docs.docker.com/userguide/

[Docker ile çalışmaya başlama ve toodefine oluşturma ve birden çok kapsayıcı uygulaması bir Azure sanal makine üzerinde çalışan]:../docker-compose-quickstart.md
