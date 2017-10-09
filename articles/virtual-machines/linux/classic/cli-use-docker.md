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
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="9ab5f-103">Merhaba Docker VM uzantısı hello Azure komut satırı arabirimi (Azure CLI) gelen kullanma</span><span class="sxs-lookup"><span data-stu-id="9ab5f-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="9ab5f-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9ab5f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9ab5f-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="9ab5f-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="9ab5f-107">Merhaba Docker VM uzantısı hello Resource Manager modeli ile kullanma hakkında daha fazla bilgi için bkz: [burada](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9ab5f-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9ab5f-108">Bu konuda nasıl toocreate VM hello gelen hello Docker VM uzantısı ile Hizmet Yönetimi (asm) Azure CLI modunda herhangi bir platformda açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="9ab5f-109">[Docker](https://www.docker.com/) hello kullanır en popüler sanallaştırma yaklaşımlardan biri [Linux kapsayıcıları](http://en.wikipedia.org/wiki/LXC) verileri yalıtarak ve bilgi işlem paylaşılan kaynakları üzerinde bir yolu olarak sanal makineleri yerine.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="9ab5f-110">Merhaba Docker VM uzantısı ve hello kullanabilirsiniz [Azure Linux Aracısı](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate kapsayıcıları uygulamalarınızın Azure ile ilgili herhangi bir sayıda barındıran bir Docker VM.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="9ab5f-111">toosee kapsayıcıları ve bunların avantajları üst düzey bir tartışma bkz hello [Docker yüksek düzey Beyaz Tahta](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="9ab5f-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="9ab5f-112">Nasıl toouse hello Azure ile Docker VM uzantısı</span><span class="sxs-lookup"><span data-stu-id="9ab5f-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="9ab5f-113">toouse hello Docker VM uzantısı Azure ile Merhaba sürümünü yüklemeniz gerekir [Azure komut satırı arabirimi](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) değerinden daha yüksek 0.8.6 (Bu yazma Merhaba 0.10.0 geçerli sürümünde olduğu gibi).</span><span class="sxs-lookup"><span data-stu-id="9ab5f-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="9ab5f-114">Mac, Linux ve Windows hello Azure CLI yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="9ab5f-115">Merhaba tam işlem toouse Azure üzerinde Docker basittir:</span><span class="sxs-lookup"><span data-stu-id="9ab5f-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="9ab5f-116">Hello Azure CLI ve bağımlılıklarını toocontrol Azure istediğiniz hello bilgisayara yükleme (Windows, bu sanal makine olarak çalışan Linux dağıtım olacaktır)</span><span class="sxs-lookup"><span data-stu-id="9ab5f-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="9ab5f-117">Azure'da Hello Azure CLI Docker komutları toocreate VM Docker ana kullanın</span><span class="sxs-lookup"><span data-stu-id="9ab5f-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="9ab5f-118">Merhaba yerel Docker komutları toomanage Docker kapsayıcılarınızı azure'da, Docker VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="9ab5f-119">Hello Azure komut satırı arabirimi (Azure CLI) yükleyin</span><span class="sxs-lookup"><span data-stu-id="9ab5f-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="9ab5f-120">tooinstall ve hello Azure CLI yapılandırmak için bkz: [nasıl tooinstall hello Azure komut satırı arabirimi](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9ab5f-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="9ab5f-121">tooconfirm hello yükleme türü `azure` hello komut isteminde ve kısa bir süre sonra hello hello basic listeler Azure CLI ASCII art komutları kullanılabilir tooyou görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="9ab5f-122">Merhaba yükleme doğru şekilde çalışan, mümkün tootype olmalıdır `azure help vm` ve listelenen hello komutlarından birini "docker" olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="9ab5f-123">Windows, docker sahip Araçları [Docker makine](https://docs.docker.com/installation/windows/), hangi tooautomate hello oluşturma toowork docker ana bilgisayarları olarak Azure VM ile birlikte kullanabilirsiniz docker istemcinin de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="9ab5f-124">Hello Azure CLI tootooyour Azure hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="9ab5f-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="9ab5f-125">Hello Azure CLI kullanmadan önce Azure hesabı kimlik bilgilerinizi, platformda hello Azure CLI ile ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="9ab5f-126">Merhaba bölüm [nasıl tooconnect tooyour Azure aboneliği](../../../xplat-cli-connect.md) nasıl tooeither indirmek ve içeri aktarma açıklanmaktadır, **.publishsettings** dosya veya Azure CLI bir Kurumsal kimlik ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="9ab5f-127">Bazı farklar vardır davranış birini kullanırken ya da hello diğer yöntemleri, kimlik doğrulama, bu nedenle toounderstand hello farklı işlevler yukarıda emin tooread hello belge.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="9ab5f-128">Docker yükleme ve başlangıç Docker VM uzantısı için Azure kullanma</span><span class="sxs-lookup"><span data-stu-id="9ab5f-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="9ab5f-129">Merhaba izleyin [Docker yükleme yönergeleri](https://docs.docker.com/installation/#installation) tooinstall Docker yerel olarak bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="9ab5f-130">toouse Docker ile bir Azure sanal makine, VM hello için kullanılan hello Linux görüntüsü hello olmalıdır [Azure Linux VM Aracısı](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) yüklü.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="9ab5f-131">Şu anda bu sağlayan görüntüleri yalnızca iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="9ab5f-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="9ab5f-132">Ubuntu görüntüden hello Azure görüntü Galerisi veya</span><span class="sxs-lookup"><span data-stu-id="9ab5f-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="9ab5f-133">Hello Azure Linux VM Aracısı ile oluşturulan özel bir Linux görüntü yüklenir ve yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="9ab5f-134">Bkz: [Azure Linux VM Aracısı](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hakkında daha fazla bilgi için toobuild hello Azure VM Aracısı ile özel bir Linux VM.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="9ab5f-135">Hello Azure görüntü Galerisi kullanma</span><span class="sxs-lookup"><span data-stu-id="9ab5f-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="9ab5f-136">Bir Bash veya Terminal oturumu, toolocate yazarak hello VM galeri toouse en son Ubuntu görüntüde hello Azure CLI komutu aşağıdaki hello kullanın</span><span class="sxs-lookup"><span data-stu-id="9ab5f-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="9ab5f-137">bir hello resim adları gibi seçin `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, ve kullanım hello aşağıdaki toocreate, görüntü kullanarak yeni bir VM komutu.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="9ab5f-138">Burada:</span><span class="sxs-lookup"><span data-stu-id="9ab5f-138">where:</span></span>

* <span data-ttu-id="9ab5f-139">*&lt;VM buluthizmeti adı&gt;*  hello azure'da hello Docker kapsayıcısı ana bilgisayar olacak VM hello adıdır</span><span class="sxs-lookup"><span data-stu-id="9ab5f-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="9ab5f-140">*&lt;Kullanıcı adı&gt;*  hello varsayılan kök kullanıcının hello VM, hello kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="9ab5f-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="9ab5f-141">*&lt;Parola&gt;*  hello hello parolası *kullanıcıadı* Azure için karmaşıklık hello standartları karşılar hesabı</span><span class="sxs-lookup"><span data-stu-id="9ab5f-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="9ab5f-142">Parola şu anda gerekir, en az 8 karakter olmalı bir küçük harf ve bir büyük harf karakter, sayı ve aşağıdaki karakterleri hello birini gibi özel bir karakter içermelidir: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="9ab5f-143">Hayır, hello süresi cümle önceki hello hello sonunda bir özel karakter değil.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="9ab5f-144">Merhaba komutu başarılı olduysa, hello kesin bağımsız değişkenleri ve kullandığınız seçenekleri bağlı olarak hello aşağıdaki gibi bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="9ab5f-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="9ab5f-145">Sanal makine oluşturmak birkaç dakika alabilir, ancak sonra bu için hazırlanmadı (Merhaba durumu değeri `ReadyRole`) Docker arka plan programı (Merhaba Docker hizmeti) başlatır hello ve toohello Docker kapsayıcısı ana bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="9ab5f-146">tootest hello Docker Azure, türü oluşturduğunuz VM</span><span class="sxs-lookup"><span data-stu-id="9ab5f-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="9ab5f-147">Burada  *&lt;vm-adı--kullandığınız&gt;*  , çağrıda çok kullanılan hello sanal makinenin hello adı`azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="9ab5f-148">Benzeri Docker ana VM çalışır durumda olduğunu belirten toohello aşağıdaki Azure'da çalışan ve komutları için bekleyen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="9ab5f-149">Docker istemci tooobtain bilgilerinizi kullanarak tooconnect deneyebilirsiniz artık (Mac üzerinde gibi bazı Docker istemci ayarları'nda toouse sahip olabilir `sudo`):</span><span class="sxs-lookup"><span data-stu-id="9ab5f-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

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

<span data-ttu-id="9ab5f-150">Yalnızca toobe tüm çalışma olduğunu belirli, hello VM hello Docker uzantısı için inceleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ab5f-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="9ab5f-151">Docker ana VM kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="9ab5f-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="9ab5f-152">Ayrıca toocreating hello Docker VM hello `azure vm docker create` komutu da otomatik olarak HTTPS kullanarak Docker istemci bilgisayar tooconnect toohello Azure kapsayıcısı ana bilgisayarınız hello gerekli sertifikaları tooallow oluşturur ve hello sertifikaları hem depolanır İstemci ve ana makineler, uygun şekilde hello.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="9ab5f-153">Sonraki denemeler üzerinde hello varolan sertifikaları yeniden ve hello yeni ana bilgisayarla paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="9ab5f-154">Sertifikaları yerleştirilir varsayılan olarak, `~/.docker`, ve Docker bağlantı noktasında yapılandırılmış toorun **2376**.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="9ab5f-155">Toouse farklı bir bağlantı veya dizin istediğiniz sonra hello aşağıdakilerden birini kullanabilir `azure vm docker create` komut satırı seçenekleri tooconfigure Docker kapsayıcısı ana VM toouse farklı bir bağlantı veya bağlanan istemciler için farklı sertifikalar:</span><span class="sxs-lookup"><span data-stu-id="9ab5f-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="9ab5f-156">Merhaba hello konak Docker arka plan için yapılandırılmış toolisten olan ve hello bağlantılarında belirtilen hello sertifikaları kullanarak bağlantı noktası hello tarafından oluşturulan istemci kimlik doğrulaması `azure vm docker create` komutu.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="9ab5f-157">Merhaba istemci makine bu sertifikaları toogain toohello Docker ana bilgisayarına erişim olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="9ab5f-158">Bu sertifikaları olmadan çalıştıran ağa bağlı bir ana bilgisayar tooconnect toohello makine yapabilirsiniz savunmasız tooanyone olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="9ab5f-159">Merhaba varsayılan yapılandırmayı değiştirmeden önce hello riskleri tooyour bilgisayarlar ve uygulamalar anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9ab5f-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ab5f-160">Next steps</span></span>
* <span data-ttu-id="9ab5f-161">Hazır toogo toohello olduğunuz [Docker Kullanıcı Kılavuzu] ve Docker VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="9ab5f-162">toocreate Docker etkin bir VM hello yeni Portalı'nda bkz [nasıl toouse hello Docker VM uzantısı hello Portal ile].</span><span class="sxs-lookup"><span data-stu-id="9ab5f-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="9ab5f-163">Hello Azure Docker VM uzantısı da Docker bildirim temelli bir YAML dosya tootake Geliştirici modelli bir uygulama arasında herhangi bir ortamın kullanan Compose destekler ve tutarlı bir dağıtım oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ab5f-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="9ab5f-164">Bkz: [Docker ile çalışmaya başlama ve toodefine oluşturma ve birden çok kapsayıcı uygulaması bir Azure sanal makine üzerinde çalışan].</span><span class="sxs-lookup"><span data-stu-id="9ab5f-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

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
