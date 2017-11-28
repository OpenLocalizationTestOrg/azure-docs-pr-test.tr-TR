---
title: "Azure Service Fabric kapsayıcı uygulamanın aaaCreate | Microsoft Docs"
description: "Azure Service Fabric üzerinde ilk Windows kapsayıcı uygulamanızı oluşturun.  Python uygulama Docker görüntüsüyle, hello görüntü tooa kapsayıcı kayıt defteri itme, yapı ve Service Fabric kapsayıcı uygulaması dağıtacak."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="c4ddc-104">Windows üzerinde ilk Service Fabric kapsayıcı uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4ddc-105">Windows</span><span class="sxs-lookup"><span data-stu-id="c4ddc-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="c4ddc-106">Linux</span><span class="sxs-lookup"><span data-stu-id="c4ddc-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="c4ddc-107">Varolan bir uygulama bir Windows kapsayıcısında Service Fabric kümesi üzerinde çalışan herhangi bir değişiklik tooyour uygulama gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="c4ddc-108">Bu makalede, bir Python içeren bir Docker görüntüsü oluşturmada size yol gösterilir [Flask](http://flask.pocoo.org/) web uygulama ve tooa Service Fabric kümesi dağıtma.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="c4ddc-109">Ayrıca, kapsayıcıya alınmış uygulamanızı [Azure Container Registry](/azure/container-registry/) aracılığıyla paylaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="c4ddc-110">Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="c4ddc-111">Okuma hello tarafından Docker hakkında bilgi edinebilirsiniz [Docker genel bakış](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4ddc-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c4ddc-112">Prerequisites</span></span>
<span data-ttu-id="c4ddc-113">Şunları çalıştıran bir geliştirme bilgisayarı:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-113">A development computer running:</span></span>
* <span data-ttu-id="c4ddc-114">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c4ddc-115">[Service Fabric SDK’sı ve araçları](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="c4ddc-116">Windows için Docker.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-116">Docker for Windows.</span></span>  <span data-ttu-id="c4ddc-117">[Windows için Docker CE edinme (dengeli)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="c4ddc-118">Yükleme ve Docker, başlangıç hello Tepsi simgesi üzerinde sağ tıklayıp sonra **geçiş tooWindows kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-118">After installing and starting Docker, right-click on hello tray icon and select **Switch tooWindows containers**.</span></span> <span data-ttu-id="c4ddc-119">Windows tabanlı gerekli toorun Docker görüntüleri budur.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-119">This is required toorun Docker images based on Windows.</span></span>

<span data-ttu-id="c4ddc-120">Kapsayıcı içeren Windows Server 2016 üzerinde üç veya daha fazla düğüme sahip bir Windows kümesi - [Küme oluşturun](service-fabric-cluster-creation-via-portal.md) veya [Service Fabric’i ücretsiz deneyin](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="c4ddc-121">Azure Container Registry’deki bir kayıt defteri - Azure aboneliğinizde [Kapsayıcı kayıt defteri oluşturun](../container-registry/container-registry-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-hello-docker-container"></a><span data-ttu-id="c4ddc-122">Merhaba Docker kapsayıcısı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="c4ddc-122">Define hello Docker container</span></span>
<span data-ttu-id="c4ddc-123">Bir resim üzerinde Hello tabanlı derleme [Python görüntü](https://hub.docker.com/_/python/) Docker hub'ına bulunur.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-123">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="c4ddc-124">Docker kapsayıcınızı bir Dockerfile içinde tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="c4ddc-125">Merhaba Dockerfile, kapsayıcı içinde hello ortamı kurma, toorun istediğiniz hello uygulamasını yükleme ve bağlantı noktası eşleme için yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-125">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="c4ddc-126">Merhaba Dockerfile olan hello giriş toohello `docker build` hello görüntüsünü oluşturur komutu.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-126">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span>

<span data-ttu-id="c4ddc-127">Boş bir dizin oluşturun ve hello dosyası oluşturma *Dockerfile* (hiçbir dosya uzantılı).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-127">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="c4ddc-128">Çok Hello ekleyin*Dockerfile* ve değişikliklerinizi kaydedin:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-128">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="c4ddc-129">Okuma hello [Dockerfile başvuru](https://docs.docker.com/engine/reference/builder/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-129">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="c4ddc-130">Basit web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-130">Create a simple web application</span></span>
<span data-ttu-id="c4ddc-131">Bağlantı noktası 80 üzerinden dinleyen ve "Merhaba Dünya!" başlığını döndüren bir Flask web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="c4ddc-132">Buna Merhaba aynı dizinde, hello dosyası oluşturma *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-132">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="c4ddc-133">Merhaba aşağıdakileri ekleyin ve değişikliklerinizi kaydedin:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-133">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="c4ddc-134">Merhaba oluşturabilir *app.py* dosya ve hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-134">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a><span data-ttu-id="c4ddc-135">Merhaba yansıması oluştur</span><span class="sxs-lookup"><span data-stu-id="c4ddc-135">Build hello image</span></span>
<span data-ttu-id="c4ddc-136">Merhaba çalıştırmak `docker build` web uygulamanızı çalıştıran komutu toocreate hello görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-136">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="c4ddc-137">Bir PowerShell penceresi açın ve hello Dockerfile içeren toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-137">Open a PowerShell window and navigate toohello directory containing hello Dockerfile.</span></span> <span data-ttu-id="c4ddc-138">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-138">Run hello following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="c4ddc-139">Bu komut derlemeleri Merhaba, Dockerfile içinde hello yönergeleri kullanarak yeni görüntüsü adlandırma (-t etiketleme) hello görüntü "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="c4ddc-139">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="c4ddc-140">Bir görüntü oluşturma hello temel görüntü Docker hub'dan çeker ve uygulamanızı hello temel görüntü üstünde ekler yeni bir görüntü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-140">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="c4ddc-141">Merhaba yapı komutu tamamlandığında hello çalıştırmak `docker images` komutu hello yeni görüntüsü toosee bilgi:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-141">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="c4ddc-142">Merhaba uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-142">Run hello application locally</span></span>
<span data-ttu-id="c4ddc-143">Görüntünüzü onu hello kapsayıcı kayıt defteri yerel olarak göndermeden önce doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-143">Verify your image locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="c4ddc-144">Merhaba uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-144">Run hello application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="c4ddc-145">*ad* kapsayıcı (yerine hello kapsayıcı kimliği) çalıştıran bir ad toohello sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-145">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="c4ddc-146">Merhaba kapsayıcı başladıktan sonra kapsayıcı bir tarayıcıdan çalıştıran tooyour bağlanabilmesi IP adresini bulun:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-146">Once hello container starts, find its IP address so that you can connect tooyour running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="c4ddc-147">Kapsayıcı çalıştıran toohello bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-147">Connect toohello running container.</span></span>  <span data-ttu-id="c4ddc-148">Toohello IP adresi döndürdü, örneğin "http://172.31.194.61" işaret eden bir web tarayıcısı açın.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-148">Open a web browser pointing toohello IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="c4ddc-149">"Hello World!" Başlık hello görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="c4ddc-149">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="c4ddc-150">Merhaba tarayıcıda görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-150">display in hello browser.</span></span>

<span data-ttu-id="c4ddc-151">toostop çalıştırmak, kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-151">toostop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="c4ddc-152">Merhaba kapsayıcı geliştirme makinenizden Sil:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-152">Delete hello container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="c4ddc-153">Anında iletme hello görüntü toohello kapsayıcı kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="c4ddc-153">Push hello image toohello container registry</span></span>
<span data-ttu-id="c4ddc-154">Geliştirme makinenizde bu hello kapsayıcı çalıştıran doğruladıktan sonra Azure kapsayıcı kayıt defterinde hello görüntü tooyour kayıt defteri iletin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-154">After you verify that hello container runs on your development machine, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="c4ddc-155">Çalıştırma ``docker login`` ile tooyour kapsayıcı defterinde toolog, [kayıt defteri kimlik](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-155">Run ``docker login`` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="c4ddc-156">Merhaba aşağıdaki örnek hello kimliği ve parolası bir Azure Active Directory geçirir [hizmet sorumlusu](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-156">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="c4ddc-157">Örneğin, bir hizmet asıl tooyour kayıt defteri bir Otomasyon senaryosu için atanmış.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-157">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span> <span data-ttu-id="c4ddc-158">İsterseniz, kayıt defteri kullanıcı kimliğiniz ve parolanızı kullanarak oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="c4ddc-159">Merhaba aşağıdaki komutu bir etiket veya hello görüntünün diğer tam nitelenmiş bir yol tooyour kayıt defteri ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-159">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="c4ddc-160">Yerler hello hello görüntüde Bu örnek ```samples``` hello kayıt defteri hello kök ad alanı tooavoid dağınıklığı.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-160">This example places hello image in hello ```samples``` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="c4ddc-161">Merhaba görüntü tooyour kapsayıcı kayıt defteri gönderin:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-161">Push hello image tooyour container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a><span data-ttu-id="c4ddc-162">Visual Studio'da kapsayıcılı hello hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-162">Create hello containerized service in Visual Studio</span></span>
<span data-ttu-id="c4ddc-163">Merhaba Service Fabric SDK ve araçları bir hizmet şablonu toohelp sağlamak kapsayıcılı bir uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-163">hello Service Fabric SDK and tools provide a service template toohelp you create a containerized application.</span></span>

1. <span data-ttu-id="c4ddc-164">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-164">Start Visual Studio.</span></span>  <span data-ttu-id="c4ddc-165">**Dosya** > **Yeni** > **Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="c4ddc-166">**Service Fabric uygulaması**’nı seçin, "MyFirstContainer" olarak adlandırın ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="c4ddc-167">Seçin **Konuk kapsayıcı** hello listesinden **hizmet şablonları**.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-167">Select **Guest Container** from hello list of **service templates**.</span></span>
4. <span data-ttu-id="c4ddc-168">İçinde **görüntü adı** "myregistry.azurecr.io/samples/helloworldapp", tooyour kapsayıcı deposu gönderilen hello görüntü girin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", hello image you pushed tooyour container repository.</span></span>
5. <span data-ttu-id="c4ddc-169">Hizmetinize bir ad verin ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="c4ddc-170">İletişimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-170">Configure communication</span></span>
<span data-ttu-id="c4ddc-171">Kapsayıcılı hello hizmet iletişimi için bir uç nokta gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-171">hello containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="c4ddc-172">Ekleme bir `Endpoint` hello protokolü, bağlantı noktası ve türü toohello ServiceManifest.xml dosyasını öğe.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-172">Add an `Endpoint` element with hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="c4ddc-173">Bu makalede, kapsayıcılı hello hizmet 8081 bağlantı noktasını dinler.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-173">For this article, hello containerized service listens on port 8081.</span></span>  <span data-ttu-id="c4ddc-174">Bu örnekte, 8081 numaralı sabit bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="c4ddc-175">Bağlantı noktası belirtilmediyse, bir rastgele bağlantı noktası hello uygulama bağlantı noktası aralığından seçilir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-175">If no port is specified, a random port from hello application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="c4ddc-176">Bir uç nokta tanımlayarak, Service Fabric hello uç nokta toohello adlandırma hizmeti yayımlar.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-176">By defining an endpoint, Service Fabric publishes hello endpoint toohello Naming service.</span></span>  <span data-ttu-id="c4ddc-177">Merhaba kümede çalışan diğer hizmetler bu kapsayıcı çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-177">Other services running in hello cluster can resolve this container.</span></span>  <span data-ttu-id="c4ddc-178">Kapsayıcıya iletişimi hello kullanarak da gerçekleştirebilirsiniz [ters proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-178">You can also perform container-to-container communication using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="c4ddc-179">İletişim hello ters proxy HTTP dinleme bağlantı noktası ve ortam değişkenleri olarak toocommunicate ile istediğiniz hello Hizmetleri hello adını sağlayarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-179">Communication is performed by providing hello reverse proxy HTTP listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="c4ddc-180">Ortam değişkenlerini yapılandırma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="c4ddc-180">Configure and set environment variables</span></span>
<span data-ttu-id="c4ddc-181">Ortam değişkenleri, her kod paketi hello hizmet bildiriminde için belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-181">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="c4ddc-182">Bu özellik, kapsayıcı olarak mı dağıtıldıklarına yoksa konuk yürütülebilir dosyası olarak mı işlendiklerine bakılmaksızın tüm hizmetlerde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="c4ddc-183">Merhaba uygulaması değerleri bildirim veya onları uygulama parametreleri olarak dağıtımı sırasında belirttiğiniz ortam değişkeni geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-183">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="c4ddc-184">Merhaba aşağıdaki hizmet bildirim XML parçacığını gösterir nasıl bir örneği için bir kod paketi toospecify ortam değişkenleri:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-184">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="c4ddc-185">Bu ortam değişkenleri hello uygulama bildiriminde geçersiz kılınabilir:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-185">These environment variables can be overridden in hello application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="c4ddc-186">Kapsayıcı bağlantı noktasından konak bağlantı noktasına eşlemeyi ve kapsayıcıdan kapsayıcıya keşfi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="c4ddc-187">Bir ana bilgisayar kullanılan bağlantı noktası toocommunicate hello kapsayıcı ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-187">Configure a host port used toocommunicate  with hello container.</span></span> <span data-ttu-id="c4ddc-188">üzerinde hangi hello hello kapsayıcı tooa bağlantı hello konaktaki içinde hizmet dinliyor hello bağlantı noktası başlangıç bağlantı noktası bağlamasına eşler.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-188">hello port binding maps hello port on which hello service is listening inside hello container tooa port on hello host.</span></span> <span data-ttu-id="c4ddc-189">Ekleme bir `PortBinding` öğesinde `ContainerHostPolicies` hello ApplicationManifest.xml dosyasının öğesi.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-189">Add a `PortBinding` element in `ContainerHostPolicies` element of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="c4ddc-190">Bu makale için `ContainerPort` 80'dir (Merhaba kapsayıcı sunan bağlantı noktası 80, belirtilen hello Dockerfile) ve `EndpointRef` "Guest1TypeEndpoint" olan (Merhaba hizmet bildiriminde önceden tanımlanmış uç nokta hello).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-190">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (hello endpoint previously defined in hello service manifest).</span></span>  <span data-ttu-id="c4ddc-191">Gelen istekleri toohello hizmet bağlantı noktası 8081 tooport 80 hello kapsayıcısı üzerinde eşlenmiş.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-191">Incoming requests toohello service on port 8081 are mapped tooport 80 on hello container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="c4ddc-192">Kapsayıcı kayıt defteri kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-192">Configure container registry authentication</span></span>
<span data-ttu-id="c4ddc-193">Kapsayıcı kayıt defteri kimlik doğrulaması ekleyerek yapılandırma `RepositoryCredentials` çok`ContainerHostPolicies` hello ApplicationManifest.xml dosyasının.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-193">Configure container registry authentication by adding `RepositoryCredentials` too`ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span> <span data-ttu-id="c4ddc-194">Merhaba hizmet toodownload hello kapsayıcı resmi hello depodan verir hello myregistry.azurecr.io kapsayıcı kayıt için Hello hesabı ve parolası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-194">Add hello account and password for hello myregistry.azurecr.io container registry, which allows hello service toodownload hello container image from hello repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="c4ddc-195">Merhaba küme düğümlerinin tooall dağıtmış olan bir şifreleme sertifikası kullanarak hello deposu parolayı şifrelemek öneririz.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-195">We recommend that you encrypt hello repository password by using an encipherment certificate that's deployed tooall nodes of hello cluster.</span></span> <span data-ttu-id="c4ddc-196">Service Fabric hello hizmet paketi toohello küme dağıtırken hello şifreleme kullanılan toodecrypt hello şifreli metin sertifikasıdır.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-196">When Service Fabric deploys hello service package toohello cluster, hello encipherment certificate is used toodecrypt hello cipher text.</span></span>  <span data-ttu-id="c4ddc-197">Merhaba Invoke-ServiceFabricEncryptText cmdlet'i kullanılan toocreate hello şifre toohello ApplicationManifest.xml dosya ekleninceye hello parolası metindir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-197">hello Invoke-ServiceFabricEncryptText cmdlet is used toocreate hello cipher text for hello password, which is added toohello ApplicationManifest.xml file.</span></span>

<span data-ttu-id="c4ddc-198">Merhaba aşağıdaki betiği yeni kendinden imzalı bir sertifika oluşturur ve bunu tooa PFX dosyası aktarır.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-198">hello following script creates a new self-signed certificate and exports it tooa PFX file.</span></span>  <span data-ttu-id="c4ddc-199">Merhaba sertifika olan bir anahtar kasası aktarılır ve ardından toohello Service Fabric kümesi dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-199">hello certificate is imported into an existing key vault and then deployed toohello Service Fabric cluster.</span></span>

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="c4ddc-200">Hello kullanarak hello parolayı şifrelemek [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-200">Encrypt hello password using hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="c4ddc-201">Hello tarafından döndürülen hello şifreli metin Hello parola yerine [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet'i ve `PasswordEncrypted` çok "true".</span><span class="sxs-lookup"><span data-stu-id="c4ddc-201">Replace hello password with hello cipher text returned by hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` too"true".</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a><span data-ttu-id="c4ddc-202">Yalıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-202">Configure isolation mode</span></span>
<span data-ttu-id="c4ddc-203">Windows, kapsayıcılar için iki yalıtım modunu destekler: İşlem ve Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="c4ddc-204">Merhaba işlem yalıtım moduyla üzerinde çalışan tüm Merhaba kapsayıcılara aynı ana bilgisayar makine paylaşımı hello çekirdek hello ana bilgisayarla hello.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-204">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="c4ddc-205">Merhaba Hyper-V yalıtım moduyla hello tekrar her Hyper-V kapsayıcı ve hello kapsayıcı konak arasında yalıtılır.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-205">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="c4ddc-206">Merhaba yalıtım modunu hello belirtilen `ContainerHostPolicies` hello uygulama bildirim dosyasının öğesinde.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-206">hello isolation mode is specified in hello `ContainerHostPolicies` element in hello application manifest file.</span></span> <span data-ttu-id="c4ddc-207">belirtilebilir hello yalıtım modlar `process`, `hyperv`, ve `default`.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-207">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="c4ddc-208">Merhaba varsayılan yalıtım modunu Varsayılanları çok`process` Windows Server'da barındıran ve çok varsayılanlarını`hyperv` Windows 10 konaklarda.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-208">hello default isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="c4ddc-209">Merhaba aşağıdaki kod parçacığında hello uygulama bildirim dosyasında belirtilen hello yalıtım modu nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-209">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="c4ddc-210">Kaynak idaresini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-210">Configure resource governance</span></span>
<span data-ttu-id="c4ddc-211">[Kaynak İdaresi](service-fabric-resource-governance.md) kapsayıcı hello kaynakları hello konakta kullanabileceğiniz hello kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-211">[Resource governance](service-fabric-resource-governance.md) restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="c4ddc-212">Merhaba `ResourceGovernancePolicy` hello uygulama bildiriminde belirtilen öğesi olan bir hizmet kod paketi için kullanılan toodeclare kaynak sınırları.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-212">hello `ResourceGovernancePolicy` element, which is specified in hello application manifest, is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="c4ddc-213">Kaynak sınırları kaynakları aşağıdaki Merhaba ayarlanabilir: bellek, MemorySwap, CpuShares (CPU göreli ağırlık), MemoryReservationInMB, BlkioWeight (BlockIO göreli ağırlık).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-213">Resource limits can be set for hello following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="c4ddc-214">Bu örnekte, hizmet paketi Guest1Pkg nereye yerleştirileceğini hello küme düğümlerinde bir temel alır.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-214">In this example, service package Guest1Pkg gets one core on hello cluster nodes where it is placed.</span></span>  <span data-ttu-id="c4ddc-215">Sınırlı too1024 hello kod paketi olacak şekilde bellek sınırları absolute MB bellek (ve aynı hello yumuşak garantisi rezervasyonu).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-215">Memory limits are absolute, so hello code package is limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="c4ddc-216">Kod paketler (kapsayıcıları veya işlemler) Bu sınır ve toodo çalışırken daha fazla bellek böylece bir bellek yetersiz özel durum sonuçları mümkün tooallocate yok.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-216">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="c4ddc-217">Kaynak sınırı zorlaması toowork için bir hizmet paketi içindeki tüm kod paketleri belirtilen bellek sınırlarını olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-217">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a><span data-ttu-id="c4ddc-218">Merhaba kapsayıcı uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="c4ddc-218">Deploy hello container application</span></span>
<span data-ttu-id="c4ddc-219">Yaptığınız değişiklikleri kaydedin ve başlangıç uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-219">Save all your changes and build hello application.</span></span> <span data-ttu-id="c4ddc-220">toopublish sağ tıklatın, uygulamanızın **MyFirstContainer** Çözüm Gezgini'nde ve select **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-220">toopublish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="c4ddc-221">İçinde **bağlantı uç noktasının**, hello küme için hello yönetim uç noktası girin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-221">In **Connection Endpoint**, enter hello management endpoint for hello cluster.</span></span>  <span data-ttu-id="c4ddc-222">Örneğin, "containercluster.westus2.cloudapp.azure.com:19000".</span><span class="sxs-lookup"><span data-stu-id="c4ddc-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="c4ddc-223">Merhaba istemci bağlantısı bulabilirsiniz hello genel bakış dikey penceresinde hello kümenizdeki için uç nokta [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-223">You can find hello client connection endpoint in hello Overview blade for your cluster in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="c4ddc-224">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-224">Click **Publish**.</span></span>

<span data-ttu-id="c4ddc-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), bir Service Fabric kümesindeki uygulama ve düğümleri inceleyip yönetmeye yönelik web tabanlı bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="c4ddc-226">Bir tarayıcı açın ve toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/gidin ve hello uygulama dağıtımını izleyin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-226">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow hello application deployment.</span></span>  <span data-ttu-id="c4ddc-227">Hello uygulama dağıtır fakat hello görüntü (hangi hello görüntü boyutu bağlı olarak biraz zaman alabilir) hello küme düğümlerinde indirilene kadar bir hata durumunda iken: ![hata][1]</span><span class="sxs-lookup"><span data-stu-id="c4ddc-227">hello application deploys but is in an error state until hello image is downloaded on hello cluster nodes (which can take some time, depending on hello image size): ![Error][1]</span></span>

<span data-ttu-id="c4ddc-228">Merhaba uygulamasıdır hazır olduğunda ```Ready``` durumu: ![hazır][2]</span><span class="sxs-lookup"><span data-stu-id="c4ddc-228">hello application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="c4ddc-229">Bir tarayıcı açın ve toohttp://containercluster.westus2.cloudapp.azure.com:8081 gidin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-229">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="c4ddc-230">"Hello World!" Başlık hello görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="c4ddc-230">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="c4ddc-231">Merhaba tarayıcıda görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-231">display in hello browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="c4ddc-232">Temizleme</span><span class="sxs-lookup"><span data-stu-id="c4ddc-232">Clean up</span></span>
<span data-ttu-id="c4ddc-233">Merhaba küme çalışırken tooincur ücretleri devam, göz önünde bulundurun [kümenizi silme](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-233">You continue tooincur charges while hello cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="c4ddc-234">[Taraf kümeleri](http://tryazureservicefabric.westus.cloudapp.azure.com/) birkaç saat sonra otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="c4ddc-235">Merhaba görüntü toohello kapsayıcı kayıt defteri itme sonra hello yerel görüntü Geliştirme bilgisayarınızdan silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-235">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="c4ddc-236">Tam Service Fabric uygulaması ve hizmet bildirimleri örneği</span><span class="sxs-lookup"><span data-stu-id="c4ddc-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="c4ddc-237">Merhaba tüm hizmet ve bu makalede kullanılan uygulama bildirimleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-237">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="c4ddc-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="c4ddc-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="c4ddc-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="c4ddc-239">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="c4ddc-240">Kapsayıcı zorla sonlandırılmadan önceki zaman aralığını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c4ddc-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="c4ddc-241">Merhaba kapsayıcı Hello hizmet silme (veya bir taşıma tooanother düğümü) başlatıldıktan sonra kaldırılmadan önce hello çalışma zamanı toowait için bir zaman aralığı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-241">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="c4ddc-242">Yapılandırma hello zaman aralığı gönderir hello `docker stop <time in seconds>` komutu toohello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-242">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="c4ddc-243">Daha ayrıntılı bilgi için bkz. [docker durdurma](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="c4ddc-244">Merhaba zaman aralığı toowait hello altında belirtilen `Hosting` bölümü.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-244">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="c4ddc-245">Küme bildirimi parçacığını aşağıdaki hello nasıl tooset hello bekleme aralığı gösterir:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-245">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
<span data-ttu-id="c4ddc-246">Merhaba varsayılan zaman aralığı ayarlanır too10 saniye.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-246">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="c4ddc-247">Bu yapılandırma dinamik olduğundan, bir yapılandırma yalnızca yükseltme hello küme güncelleştirmelerini hello zaman aşımı süresi.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-247">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="c4ddc-248">Merhaba çalışma zamanı tooremove yapılandırma kullanılmayan kapsayıcı görüntüleri</span><span class="sxs-lookup"><span data-stu-id="c4ddc-248">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="c4ddc-249">Merhaba Service Fabric kümesi tooremove yapılandırabilirsiniz hello düğümünden kullanılmayan kapsayıcı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-249">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="c4ddc-250">Bu yapılandırma, disk alanı toobe hello düğüm üzerinde çok fazla sayıda kapsayıcı görüntüler varsa yeniden yakalanmadan sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-250">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="c4ddc-251">tooenable bu özellik, güncelleştirme hello `Hosting` hello aşağıdaki kod parçacığında gösterildiği gibi hello küme bildiriminde bölümünde:</span><span class="sxs-lookup"><span data-stu-id="c4ddc-251">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

<span data-ttu-id="c4ddc-252">Silinmemelidir görüntüler için bunları altında hello belirtebilirsiniz `ContainerImagesToSkip` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-252">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="c4ddc-253">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4ddc-253">Next steps</span></span>
* <span data-ttu-id="c4ddc-254">[Service Fabric’te kapsayıcı](service-fabric-containers-overview.md) çalıştırma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="c4ddc-255">Okuma hello [bir kapsayıcıda .NET uygulaması dağıtma](service-fabric-host-app-in-a-container.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-255">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="c4ddc-256">Service Fabric Hello hakkında bilgi edinin [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="c4ddc-256">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="c4ddc-257">Checkout hello [Service Fabric kapsayıcı kod örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers) github'da.</span><span class="sxs-lookup"><span data-stu-id="c4ddc-257">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
