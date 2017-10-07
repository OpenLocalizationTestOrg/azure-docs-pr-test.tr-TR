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
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="b0115-103">Merhaba Docker VM uzantısı hello Klasik Azure portalı ile kullanma</span><span class="sxs-lookup"><span data-stu-id="b0115-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b0115-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b0115-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b0115-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="b0115-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b0115-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="b0115-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="b0115-107">[Docker](https://www.docker.com/) hello kullanır en popüler sanallaştırma yaklaşımlardan biri [Linux kapsayıcıları](http://en.wikipedia.org/wiki/LXC) verileri yalıtarak ve bilgi işlem paylaşılan kaynakları üzerinde bir yolu olarak sanal makineleri yerine.</span><span class="sxs-lookup"><span data-stu-id="b0115-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="b0115-108">Merhaba Docker VM uzantısı tarafından yönetilen kullanabilirsiniz [Azure Linux Aracısı] toocreate kapsayıcıları uygulamalarınızın Azure ile ilgili herhangi bir sayıda barındıran bir Docker VM.</span><span class="sxs-lookup"><span data-stu-id="b0115-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="b0115-109">Bu konuda nasıl toocreate Docker sanal makineden bir hello Klasik Azure portalı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b0115-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="b0115-110">toocreate Docker VM hello komut satırında nasıl görürüm toosee [nasıl toouse hello Docker VM uzantısı hello Azure komut satırı arabirimi (Azure CLI)].</span><span class="sxs-lookup"><span data-stu-id="b0115-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="b0115-111">toosee kapsayıcıları ve bunların avantajları üst düzey bir tartışma bkz hello [Docker yüksek düzey Beyaz Tahta](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="b0115-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="b0115-112">Resim Galerisi hello yeni bir VM oluşturun</span><span class="sxs-lookup"><span data-stu-id="b0115-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="b0115-113">Merhaba ilk adım bir Azure VM hello Docker VM uzantısı, Ubuntu 14.04 LTS görüntüden hello görüntü Galerisi örneği sunucu görüntüsünü ve Ubuntu 14.04 masaüstü istemci olarak kullanarak destekleyen Linux görüntüsünden gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b0115-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="b0115-114">Merhaba Portalı'nda tıklatın **+ yeni** hello köşe toocreate yeni bir VM örneği sol alt ve bir Ubuntu 14.04 LTS görüntü hello seçim yok ya da hello seçin görüntü Galerisi, aşağıda gösterildiği gibi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b0115-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="b0115-115">Şu anda yalnızca Temmuz 2014'den daha yeni Ubuntu 14.04 LTS görüntüleri hello Docker VM uzantısı destekler.</span><span class="sxs-lookup"><span data-stu-id="b0115-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Yeni bir Ubuntu görüntüsü oluşturma](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="b0115-117">Docker sertifikaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0115-117">Create Docker Certificates</span></span>
<span data-ttu-id="b0115-118">Hello VM oluşturulduktan sonra Docker istemci bilgisayarınızda yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b0115-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="b0115-119">(Ayrıntılar için bkz [Docker yükleme yönergeleri](https://docs.docker.com/installation/#installation).)</span><span class="sxs-lookup"><span data-stu-id="b0115-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="b0115-120">Merhaba çok göre Docker iletişimi için sertifika ve anahtar dosyaları oluşturma[çalıştıran Docker https ile] ve hello yerleştirin  **`~/.docker`**  istemci bilgisayarınızda dizin.</span><span class="sxs-lookup"><span data-stu-id="b0115-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="b0115-121">Hello Docker VM uzantısı hello portal şu anda base64 ile kodlanmış kimlik bilgileri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b0115-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="b0115-122">Merhaba komut satırında kullanın  **`base64`**  veya başka bir sık kullanılan aracı toocreate base64 ile kodlanmış konuları kodlama.</span><span class="sxs-lookup"><span data-stu-id="b0115-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="b0115-123">Basit bir sertifika ve anahtar dosyaları kümesiyle bunu benzer toothis benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="b0115-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

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

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="b0115-124">Merhaba Docker VM uzantısı Ekle</span><span class="sxs-lookup"><span data-stu-id="b0115-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="b0115-125">tooadd Docker VM uzantısı Merhaba, oluşturduğunuz hello VM örneği bulun ve çok ilerleyin**uzantıları** ve aşağıda gösterildiği gibi VM uzantıları, Yukarı toobring tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0115-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="b0115-126">Bu işlevsellik yalnızca hello Önizleme portalında desteklenir: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="b0115-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="b0115-127">Bir uzantı ekleme</span><span class="sxs-lookup"><span data-stu-id="b0115-127">Add an Extension</span></span>
<span data-ttu-id="b0115-128">Merhaba tıklatın **+ Ekle** toodisplay hello olası VM uzantıları toothis VM ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0115-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="b0115-129">Merhaba Docker VM uzantısı seçin</span><span class="sxs-lookup"><span data-stu-id="b0115-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="b0115-130">Merhaba hello Docker açıklama ve önemli bağlantılar getirir, Docker VM uzantısı seçin ve ardından **oluşturma** hello alt toobegin hello yükleme yordamı sırasında.</span><span class="sxs-lookup"><span data-stu-id="b0115-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="b0115-131">Sertifika ve anahtar dosyaları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0115-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="b0115-132">Merhaba form alanlarını hello grafiği aşağıdaki gösterildiği gibi hello base64 ile kodlanmış sürümleri, CA sertifikası, sunucu sertifikası ve sunucu anahtarınızı girin.</span><span class="sxs-lookup"><span data-stu-id="b0115-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="b0115-133">Not (olduğu gibi hello görüntü önceki) 2376 hello varsayılan olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="b0115-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="b0115-134">Herhangi bir uç nokta burada girebilirsiniz, ancak hello sonraki adıma uç nokta eşleşen hello yukarı tooopen olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b0115-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="b0115-135">Merhaba varsayılan değiştirirseniz, uç nokta hello sonraki adımda eşleşen hello yukarı emin tooopen olun.</span><span class="sxs-lookup"><span data-stu-id="b0115-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="b0115-136">Merhaba Docker iletişim uç noktası ekleme</span><span class="sxs-lookup"><span data-stu-id="b0115-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="b0115-137">Oluşturduğunuz hello kaynak grubu görüntülerken hello VM ile ilişkilendirilmiş ağ güvenlik grubu seçin ve tıklatın **gelen güvenlik kuralları** tooview hello kuralları aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="b0115-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="b0115-138">Tıklatın **+ Ekle** tooadd başka bir kural ve hello varsayılan durumda hello uç noktası için bir ad girin (Bu örnekte, **Docker**) ve 2376 'hedef bağlantı noktası aralığı'.</span><span class="sxs-lookup"><span data-stu-id="b0115-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="b0115-139">Merhaba Protokolü değeri gösteren ayarlamak **TCP**, tıklatıp **Tamam** toocreate hello kuralı.</span><span class="sxs-lookup"><span data-stu-id="b0115-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="b0115-140">Docker istemci ve Azure Docker ana test</span><span class="sxs-lookup"><span data-stu-id="b0115-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="b0115-141">Bulun ve kopyalama hello adı VM etki alanı ve türü, istemci bilgisayarın hello komut satırında `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (burada *dockerextension* hello tarafından değiştirildi alt etki alanı için VM).</span><span class="sxs-lookup"><span data-stu-id="b0115-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="b0115-142">Merhaba sonuç benzer toothis görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="b0115-142">hello result should appear similar toothis:</span></span>

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

<span data-ttu-id="b0115-143">Merhaba yukarıdaki adımları tamamladıktan sonra yapılandırılan bir Azure VM üzerinde çalışan tam olarak işlevsel bir Docker ana bilgisayar artık yüklü toobe diğer istemcilerinden tooremotely bağlı.</span><span class="sxs-lookup"><span data-stu-id="b0115-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="b0115-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b0115-144">Next steps</span></span>
<span data-ttu-id="b0115-145">Hazır toogo toohello olduğunuz [Docker Kullanıcı Kılavuzu] ve Docker VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="b0115-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="b0115-146">Tooautomate Docker ana bilgisayarları Azure Vm'lerinde komut satırı arabirimi kullanarak oluşturmak istiyorsanız, bkz: [nasıl toouse hello Docker VM uzantısı hello Azure komut satırı arabirimi (Azure CLI)]</span><span class="sxs-lookup"><span data-stu-id="b0115-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

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
