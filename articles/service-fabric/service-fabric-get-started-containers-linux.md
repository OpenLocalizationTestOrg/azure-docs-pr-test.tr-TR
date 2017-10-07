---
title: "Azure Service Fabric kapsayıcı uygulamanın Linux'ta aaaCreate | Microsoft Docs"
description: "Azure Service Fabric üzerinde ilk Linux kapsayıcı uygulamanızı oluşturun.  Uygulamanızı Docker görüntüsüyle, hello görüntü tooa kapsayıcı kayıt defteri itme, yapı ve Service Fabric kapsayıcı uygulaması dağıtacak."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="29a23-104">Linux üzerinde ilk Service Fabric kapsayıcı uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="29a23-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29a23-105">Windows</span><span class="sxs-lookup"><span data-stu-id="29a23-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="29a23-106">Linux</span><span class="sxs-lookup"><span data-stu-id="29a23-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="29a23-107">Varolan bir uygulama bir Linux kapsayıcısında Service Fabric kümesi üzerinde çalışan herhangi bir değişiklik tooyour uygulama gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="29a23-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="29a23-108">Bu makalede, bir Python içeren bir Docker görüntüsü oluşturmada size yol gösterilir [Flask](http://flask.pocoo.org/) web uygulama ve tooa Service Fabric kümesi dağıtma.</span><span class="sxs-lookup"><span data-stu-id="29a23-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="29a23-109">Ayrıca, kapsayıcıya alınmış uygulamanızı [Azure Container Registry](/azure/container-registry/) aracılığıyla paylaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="29a23-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="29a23-110">Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="29a23-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="29a23-111">Okuma hello tarafından Docker hakkında bilgi edinebilirsiniz [Docker genel bakış](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="29a23-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29a23-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="29a23-112">Prerequisites</span></span>
* <span data-ttu-id="29a23-113">Şunları çalıştıran bir geliştirme bilgisayarı:</span><span class="sxs-lookup"><span data-stu-id="29a23-113">A development computer running:</span></span>
  * <span data-ttu-id="29a23-114">[Service Fabric SDK’sı ve araçları](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="29a23-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="29a23-115">[Linux için Docker CE](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="29a23-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="29a23-116">Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="29a23-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="29a23-117">Azure Container Registry’deki bir kayıt defteri - Azure aboneliğinizde [Kapsayıcı kayıt defteri oluşturun](../container-registry/container-registry-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="29a23-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="29a23-118">Merhaba Docker kapsayıcısı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="29a23-118">Define hello Docker container</span></span>
<span data-ttu-id="29a23-119">Bir resim üzerinde Hello tabanlı derleme [Python görüntü](https://hub.docker.com/_/python/) Docker hub'ına bulunur.</span><span class="sxs-lookup"><span data-stu-id="29a23-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="29a23-120">Docker kapsayıcınızı bir Dockerfile içinde tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="29a23-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="29a23-121">Merhaba Dockerfile, kapsayıcı içinde hello ortamı kurma, toorun istediğiniz hello uygulamasını yükleme ve bağlantı noktası eşleme için yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="29a23-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="29a23-122">Merhaba Dockerfile olan hello giriş toohello `docker build` hello görüntüsünü oluşturur komutu.</span><span class="sxs-lookup"><span data-stu-id="29a23-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="29a23-123">Boş bir dizin oluşturun ve hello dosyası oluşturma *Dockerfile* (hiçbir dosya uzantılı).</span><span class="sxs-lookup"><span data-stu-id="29a23-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="29a23-124">Çok Hello ekleyin*Dockerfile* ve değişikliklerinizi kaydedin:</span><span class="sxs-lookup"><span data-stu-id="29a23-124">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="29a23-125">Okuma hello [Dockerfile başvuru](https://docs.docker.com/engine/reference/builder/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="29a23-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="29a23-126">Basit web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="29a23-126">Create a simple web application</span></span>
<span data-ttu-id="29a23-127">Bağlantı noktası 80 üzerinden dinleyen ve "Merhaba Dünya!" başlığını döndüren bir Flask web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="29a23-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="29a23-128">Buna Merhaba aynı dizinde, hello dosyası oluşturma *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="29a23-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="29a23-129">Merhaba aşağıdakileri ekleyin ve değişikliklerinizi kaydedin:</span><span class="sxs-lookup"><span data-stu-id="29a23-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="29a23-130">Merhaba oluşturabilir *app.py* dosya ve hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="29a23-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="29a23-131">Merhaba yansıması oluştur</span><span class="sxs-lookup"><span data-stu-id="29a23-131">Build hello image</span></span>
<span data-ttu-id="29a23-132">Merhaba çalıştırmak `docker build` web uygulamanızı çalıştıran komutu toocreate hello görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="29a23-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="29a23-133">Bir PowerShell penceresi açın ve çok gidin*c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="29a23-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="29a23-134">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="29a23-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="29a23-135">Bu komut derlemeleri Merhaba, Dockerfile içinde hello yönergeleri kullanarak yeni görüntüsü adlandırma (-t etiketleme) hello görüntü "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="29a23-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="29a23-136">Bir görüntü oluşturma hello temel görüntü Docker hub'dan çeker ve uygulamanızı hello temel görüntü üstünde ekler yeni bir görüntü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="29a23-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="29a23-137">Merhaba yapı komutu tamamlandığında hello çalıştırmak `docker images` komutu hello yeni görüntüsü toosee bilgi:</span><span class="sxs-lookup"><span data-stu-id="29a23-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="29a23-138">Merhaba uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="29a23-138">Run hello application locally</span></span>
<span data-ttu-id="29a23-139">Kapsayıcılı uygulamanız bu hello kapsayıcı kayıt defteri yerel olarak göndermeden önce çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="29a23-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="29a23-140">Merhaba uygulamayı çalıştırın, bilgisayarınızın 4000 numaralı bağlantı noktasını toohello kapsayıcının eşleme 80 kullanıma sunulan bağlantı noktası:</span><span class="sxs-lookup"><span data-stu-id="29a23-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="29a23-141">*ad* kapsayıcı (yerine hello kapsayıcı kimliği) çalıştıran bir ad toohello sağlar.</span><span class="sxs-lookup"><span data-stu-id="29a23-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="29a23-142">Kapsayıcı çalıştıran toohello bağlayın.</span><span class="sxs-lookup"><span data-stu-id="29a23-142">Connect toohello running container.</span></span>  <span data-ttu-id="29a23-143">Bağlantı 4000, örneğin "http://localhost:4000" döndürülen toohello IP adresini işaret eden bir web tarayıcısı açın.</span><span class="sxs-lookup"><span data-stu-id="29a23-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="29a23-144">"Hello World!" Başlık hello görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="29a23-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="29a23-145">Merhaba tarayıcıda görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="29a23-145">display in hello browser.</span></span>

![Merhaba Dünya!][hello-world]

<span data-ttu-id="29a23-147">toostop çalıştırmak, kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="29a23-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="29a23-148">Merhaba kapsayıcı geliştirme makinenizden Sil:</span><span class="sxs-lookup"><span data-stu-id="29a23-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="29a23-149">Anında iletme hello görüntü toohello kapsayıcı kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="29a23-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="29a23-150">Merhaba uygulaması Docker içinde çalıştığını doğruladıktan sonra Azure kapsayıcı kayıt defterinde hello görüntü tooyour kayıt defteri iletin.</span><span class="sxs-lookup"><span data-stu-id="29a23-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="29a23-151">Çalıştırma `docker login` ile tooyour kapsayıcı defterinde toolog, [kayıt defteri kimlik](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="29a23-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="29a23-152">Merhaba aşağıdaki örnek hello kimliği ve parolası bir Azure Active Directory geçirir [hizmet sorumlusu](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="29a23-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="29a23-153">Örneğin, bir hizmet asıl tooyour kayıt defteri bir Otomasyon senaryosu için atanmış.</span><span class="sxs-lookup"><span data-stu-id="29a23-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="29a23-154">İsterseniz, kayıt defteri kullanıcı kimliğiniz ve parolanızı kullanarak oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29a23-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="29a23-155">Merhaba aşağıdaki komutu bir etiket veya hello görüntünün diğer tam nitelenmiş bir yol tooyour kayıt defteri ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="29a23-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="29a23-156">Yerler hello hello görüntüde Bu örnek `samples` hello kayıt defteri hello kök ad alanı tooavoid dağınıklığı.</span><span class="sxs-lookup"><span data-stu-id="29a23-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="29a23-157">Merhaba görüntü tooyour kapsayıcı kayıt defteri gönderin:</span><span class="sxs-lookup"><span data-stu-id="29a23-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="29a23-158">Paket hello Docker Yeoman görüntüsüyle</span><span class="sxs-lookup"><span data-stu-id="29a23-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="29a23-159">Merhaba Linux için Service Fabric SDK içerir bir [Yeoman](http://yeoman.io/) kolay toocreate kolaylaştırır Oluşturucu uygulamanız ve kapsayıcı görüntü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="29a23-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="29a23-160">Yeoman tek bir Docker kapsayıcısı uygulamayla adlı toocreate kullanalım *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="29a23-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="29a23-161">toocreate Service Fabric kapsayıcı uygulaması, bir terminal penceresi açın ve Çalıştır `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="29a23-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="29a23-162">Uygulamanızı adlandırın (örneğin, "mycontainer").</span><span class="sxs-lookup"><span data-stu-id="29a23-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="29a23-163">Bir kapsayıcı kayıt defterindeki hello kapsayıcı görüntüsü için Hello URL'si girin (örneğin, "").</span><span class="sxs-lookup"><span data-stu-id="29a23-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="29a23-164">Bu resimle bir iş yükü giriş tanımlanmış noktası, tooexplicitly belirtin giriş komutları (başlatma işleminden sonra çalışan hello kapsayıcı tutar hello kapsayıcı içinde çalıştırma komutları).</span><span class="sxs-lookup"><span data-stu-id="29a23-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="29a23-165">"1" örnek sayısı belirtin.</span><span class="sxs-lookup"><span data-stu-id="29a23-165">Specify an instance count of "1".</span></span>

![Kapsayıcılar için Service Fabric Yeoman oluşturucusu][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="29a23-167">Bağlantı noktası eşlemesini ve kapsayıcı deposu kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="29a23-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="29a23-168">Kapsayıcı içinde alınmış hizmetinize iletişim için bir uç nokta gerekir.</span><span class="sxs-lookup"><span data-stu-id="29a23-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="29a23-169">Şimdi hello protokolü, bağlantı noktası ve tür ekleyin tooan `Endpoint` hello ServiceManifest.xml dosyasında.</span><span class="sxs-lookup"><span data-stu-id="29a23-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="29a23-170">Bu makalede, kapsayıcılı hello hizmet 4000 bağlantı noktasını dinler:</span><span class="sxs-lookup"><span data-stu-id="29a23-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="29a23-171">Merhaba sağlama `UriScheme` otomatik olarak kapsayıcı uç nokta hello bulunabilirlik için Service Fabric adlandırma hizmeti ile hello kaydeder.</span><span class="sxs-lookup"><span data-stu-id="29a23-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="29a23-172">Bir tam ServiceManifest.xml örnek dosya hello bu makalenin sonundaki sağlanır.</span><span class="sxs-lookup"><span data-stu-id="29a23-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="29a23-173">Merhaba kapsayıcı bağlantı noktası ana bilgisayar bağlantı noktası eşleme belirterek yapılandırma bir `PortBinding` ilkesinde `ContainerHostPolicies` hello ApplicationManifest.xml dosyasının.</span><span class="sxs-lookup"><span data-stu-id="29a23-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="29a23-174">Bu makale için `ContainerPort` 80'dir (Merhaba kapsayıcı sunan bağlantı noktası 80, belirtilen hello Dockerfile) ve `EndpointRef` olan "myserviceTypeEndpoint" (Merhaba uç noktası hello hizmet bildiriminde tanımlanan).</span><span class="sxs-lookup"><span data-stu-id="29a23-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="29a23-175">Gelen istekleri toohello hizmet bağlantı noktası 4000 tooport 80 hello kapsayıcısı üzerinde eşlenmiş.</span><span class="sxs-lookup"><span data-stu-id="29a23-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="29a23-176">Ardından, kapsayıcı bir özel deposu ile tooauthenticate gerekirse, ekleyin `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="29a23-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="29a23-177">Bu makalede, hello hesap adı ve parola hello myregistry.azurecr.io kapsayıcı kayıt defteri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="29a23-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="29a23-178">Derleme ve paket Merhaba Service Fabric uygulaması</span><span class="sxs-lookup"><span data-stu-id="29a23-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="29a23-179">Merhaba Service Fabric Yeoman şablonları içerir bir yapı komut dosyası için [Gradle](https://gradle.org/), hangi toobuild hello hello terminal uygulamasından kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29a23-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="29a23-180">Merhaba aşağıdaki çalıştırma toobuild ve paket hello uygulaması:</span><span class="sxs-lookup"><span data-stu-id="29a23-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="29a23-181">Merhaba uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="29a23-181">Deploy hello application</span></span>
<span data-ttu-id="29a23-182">Merhaba uygulama oluşturulduktan sonra toohello yerel küme hello Service Fabric CLI kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29a23-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="29a23-183">Toohello yerel Service Fabric kümesi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="29a23-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="29a23-184">Kullanım hello hello şablonu toocopy Merhaba uygulaması toohello kümenin görüntü deposu paketini, hello uygulama türünü kaydetme ve hello uygulama örneğini oluşturmak sağlanan komut dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="29a23-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="29a23-185">Bir tarayıcı açın ve http://localhost: 19080/Explorer (Merhaba Vagrant Mac OS X kullanıyorsanız VM hello özel IP ile değiştir localhost) konumunda tooService Fabric Gezgini'ne gidin.</span><span class="sxs-lookup"><span data-stu-id="29a23-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="29a23-186">Merhaba uygulamaları düğümünü genişletin ve şimdi uygulama türü için bir giriş ve hello bu türünün ilk örneği için başka bir yoktur.</span><span class="sxs-lookup"><span data-stu-id="29a23-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="29a23-187">Kapsayıcı çalıştıran toohello bağlayın.</span><span class="sxs-lookup"><span data-stu-id="29a23-187">Connect toohello running container.</span></span>  <span data-ttu-id="29a23-188">Bağlantı 4000, örneğin "http://localhost:4000" döndürülen toohello IP adresini işaret eden bir web tarayıcısı açın.</span><span class="sxs-lookup"><span data-stu-id="29a23-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="29a23-189">"Hello World!" Başlık hello görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="29a23-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="29a23-190">Merhaba tarayıcıda görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="29a23-190">display in hello browser.</span></span>

![Merhaba Dünya!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="29a23-192">Temizleme</span><span class="sxs-lookup"><span data-stu-id="29a23-192">Clean up</span></span>
<span data-ttu-id="29a23-193">Merhaba kaldırma komut dosyası kullan hello şablon toodelete hello uygulama örneği hello yerel geliştirme kümeden sağlanan ve hello uygulama türü kaydını silin.</span><span class="sxs-lookup"><span data-stu-id="29a23-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="29a23-194">Merhaba görüntü toohello kapsayıcı kayıt defteri itme sonra hello yerel görüntü Geliştirme bilgisayarınızdan silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="29a23-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="29a23-195">Tam Service Fabric uygulaması ve hizmet bildirimleri örneği</span><span class="sxs-lookup"><span data-stu-id="29a23-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="29a23-196">Merhaba tüm hizmet ve bu makalede kullanılan uygulama bildirimleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="29a23-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="29a23-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="29a23-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="29a23-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="29a23-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="29a23-199">Daha fazla Hizmetleri tooan varolan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="29a23-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="29a23-200">başka bir kapsayıcı hizmeti tooan uygulaması zaten yeoman, kullanılarak oluşturulan tooadd gerçekleştirmek hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="29a23-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="29a23-201">Merhaba var olan uygulamanın toohello kök dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="29a23-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="29a23-202">Örneğin, `cd ~/YeomanSamples/MyApplication`, `MyApplication` Yeoman tarafından oluşturulan hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="29a23-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="29a23-203">`yo azuresfcontainer:AddService` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="29a23-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="29a23-204">Kapsayıcı zorla sonlandırılmadan önceki zaman aralığını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="29a23-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="29a23-205">Merhaba kapsayıcı Hello hizmet silme (veya bir taşıma tooanother düğümü) başlatıldıktan sonra kaldırılmadan önce hello çalışma zamanı toowait için bir zaman aralığı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29a23-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="29a23-206">Yapılandırma hello zaman aralığı gönderir hello `docker stop <time in seconds>` komutu toohello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="29a23-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="29a23-207">Daha ayrıntılı bilgi için bkz. [docker durdurma](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="29a23-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="29a23-208">Merhaba zaman aralığı toowait hello altında belirtilen `Hosting` bölümü.</span><span class="sxs-lookup"><span data-stu-id="29a23-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="29a23-209">Küme bildirimi parçacığını aşağıdaki hello nasıl tooset hello bekleme aralığı gösterir:</span><span class="sxs-lookup"><span data-stu-id="29a23-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="29a23-210">Merhaba varsayılan zaman aralığı ayarlanır too10 saniye.</span><span class="sxs-lookup"><span data-stu-id="29a23-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="29a23-211">Bu yapılandırma dinamik olduğundan, bir yapılandırma yalnızca yükseltme hello küme güncelleştirmelerini hello zaman aşımı süresi.</span><span class="sxs-lookup"><span data-stu-id="29a23-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="29a23-212">Merhaba çalışma zamanı tooremove yapılandırma kullanılmayan kapsayıcı görüntüleri</span><span class="sxs-lookup"><span data-stu-id="29a23-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="29a23-213">Merhaba Service Fabric kümesi tooremove yapılandırabilirsiniz hello düğümünden kullanılmayan kapsayıcı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="29a23-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="29a23-214">Bu yapılandırma, disk alanı toobe hello düğüm üzerinde çok fazla sayıda kapsayıcı görüntüler varsa yeniden yakalanmadan sağlar.</span><span class="sxs-lookup"><span data-stu-id="29a23-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="29a23-215">tooenable bu özellik, güncelleştirme hello `Hosting` hello aşağıdaki kod parçacığında gösterildiği gibi hello küme bildiriminde bölümünde:</span><span class="sxs-lookup"><span data-stu-id="29a23-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="29a23-216">Silinmemelidir görüntüler için bunları altında hello belirtebilirsiniz `ContainerImagesToSkip` parametresi.</span><span class="sxs-lookup"><span data-stu-id="29a23-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="29a23-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="29a23-217">Next steps</span></span>
* <span data-ttu-id="29a23-218">[Service Fabric’te kapsayıcı](service-fabric-containers-overview.md) çalıştırma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="29a23-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="29a23-219">Okuma hello [bir kapsayıcıda .NET uygulaması dağıtma](service-fabric-host-app-in-a-container.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="29a23-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="29a23-220">Service Fabric Hello hakkında bilgi edinin [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="29a23-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="29a23-221">Checkout hello [Service Fabric kapsayıcı kod örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers) github'da.</span><span class="sxs-lookup"><span data-stu-id="29a23-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
