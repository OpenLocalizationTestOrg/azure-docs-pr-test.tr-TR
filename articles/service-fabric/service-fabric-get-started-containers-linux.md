---
title: "Linux üzerinde Azure Service Fabric kapsayıcı uygulaması oluşturma | Microsoft Docs"
description: "Azure Service Fabric üzerinde ilk Linux kapsayıcı uygulamanızı oluşturun.  Uygulamanızla bir Docker görüntüsü oluşturun, görüntüyü bir kapsayıcı kayıt defterine iletin, bir Service Fabric kapsayıcı uygulaması oluşturup dağıtın."
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
ms.openlocfilehash: 8355478cb2fff3a63bc4a9b359ec8e2b132c80f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="d4b9a-104">Linux üzerinde ilk Service Fabric kapsayıcı uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4b9a-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4b9a-105">Windows</span><span class="sxs-lookup"><span data-stu-id="d4b9a-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="d4b9a-106">Linux</span><span class="sxs-lookup"><span data-stu-id="d4b9a-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="d4b9a-107">Bir Service Fabric kümesindeki Linux kapsayıcısında mevcut olan bir uygulamayı çalıştırmak için uygulamanızda herhangi bir değişiklik yapılması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="d4b9a-108">Bu makalede, Python [Flask](http://flask.pocoo.org/) web uygulaması içeren bir Docker görüntüsü oluşturma ve bunu Service Fabric kümesine dağıtma işlemlerinde size yol gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="d4b9a-109">Ayrıca, kapsayıcıya alınmış uygulamanızı [Azure Container Registry](/azure/container-registry/) aracılığıyla paylaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="d4b9a-110">Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="d4b9a-111">[Docker’a Genel Bakış](https://docs.docker.com/engine/understanding-docker/) makalesini okuyarak Docker hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4b9a-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d4b9a-112">Prerequisites</span></span>
* <span data-ttu-id="d4b9a-113">Şunları çalıştıran bir geliştirme bilgisayarı:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-113">A development computer running:</span></span>
  * <span data-ttu-id="d4b9a-114">[Service Fabric SDK’sı ve araçları](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="d4b9a-115">[Linux için Docker CE](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="d4b9a-116">Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="d4b9a-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="d4b9a-117">Azure Container Registry’deki bir kayıt defteri - Azure aboneliğinizde [Kapsayıcı kayıt defteri oluşturun](../container-registry/container-registry-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-the-docker-container"></a><span data-ttu-id="d4b9a-118">Docker kapsayıcısını tanımlama</span><span class="sxs-lookup"><span data-stu-id="d4b9a-118">Define the Docker container</span></span>
<span data-ttu-id="d4b9a-119">Docker Hub’ında bulunan [Python görüntüsünü](https://hub.docker.com/_/python/) temel alan bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-119">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="d4b9a-120">Docker kapsayıcınızı bir Dockerfile içinde tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="d4b9a-121">Dockerfile, kapsayıcınızın içindeki ortamı ayarlama, çalıştırmak istediğiniz uygulamayı yükleme ve bağlantı noktalarını eşleme yönergelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-121">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="d4b9a-122">Dockerfile, görüntüyü oluşturan `docker build` komutunun girdisidir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-122">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span> 

<span data-ttu-id="d4b9a-123">Boş bir dizin oluşturun ve *Dockerfile* dosyasını oluşturun (dosya uzantısı kullanmayın).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-123">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="d4b9a-124">Aşağıdakini *Dockerfile* dosyasına ekleyin ve değişikliklerinizi kaydedin:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-124">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="d4b9a-125">Daha fazla bilgi için [Dockerfile başvurusunu](https://docs.docker.com/engine/reference/builder/) okuyun.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-125">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="d4b9a-126">Basit web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4b9a-126">Create a simple web application</span></span>
<span data-ttu-id="d4b9a-127">Bağlantı noktası 80 üzerinden dinleyen ve "Merhaba Dünya!" başlığını döndüren bir Flask web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="d4b9a-128">Aynı dizinde, *requirements.txt* dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-128">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="d4b9a-129">Aşağıdakini dosyaya ekleyin ve değişikliklerinizi kaydedin:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-129">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="d4b9a-130">Ayrıca, *app.py* dosyasını da oluşturun ve aşağıdakini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-130">Also create the *app.py* file and add the following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-the-image"></a><span data-ttu-id="d4b9a-131">Görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4b9a-131">Build the image</span></span>
<span data-ttu-id="d4b9a-132">Web uygulamanızı çalıştıran görüntüyü oluşturmak için `docker build` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-132">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="d4b9a-133">Bir PowerShell penceresi açıp *c:\temp\helloworldapp* dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-133">Open a PowerShell window and navigate to *c:\temp\helloworldapp*.</span></span> <span data-ttu-id="d4b9a-134">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-134">Run the following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="d4b9a-135">Bu komut Dockerfile içindeki yönergeleri kullanarak yeni görüntüyü oluşturur ve "helloworldapp" olarak adlandırır (-t etiketi).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-135">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="d4b9a-136">Görüntü oluşturulduğunda, temel görüntü Docker Hub’ından alınır ve uygulamanızı temel görüntünün üstüne ekleyen yeni bir görüntü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-136">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="d4b9a-137">Oluşturma komutu tamamlandıktan sonra, yeni görüntü üzerindeki bilgileri görmek için `docker images` komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-137">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="d4b9a-138">Uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d4b9a-138">Run the application locally</span></span>
<span data-ttu-id="d4b9a-139">Kapsayıcıya alınmış uygulamanızı kapsayıcı kayıt defterine göndermeden önce uygulamanın yerel olarak çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-139">Verify that your containerized application runs locally before pushing it the container registry.</span></span>  

<span data-ttu-id="d4b9a-140">Bilgisayarınızın 4000 numaralı bağlantı noktasını kapsayıcının ortaya konan 80 numaralı bağlantı noktasına eşleyerek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-140">Run the application, mapping your computer's port 4000 to the container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="d4b9a-141">*name*, çalışan kapsayıcıya bir ad verir (kapsayıcı kimliği yerine).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-141">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="d4b9a-142">Çalışan kapsayıcıya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-142">Connect to the running container.</span></span>  <span data-ttu-id="d4b9a-143">4000 numaralı bağlantı noktasında döndürülen IP adresine işaret eden bir web tarayıcısı açın (örneğin, "http://localhost:4000").</span><span class="sxs-lookup"><span data-stu-id="d4b9a-143">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="d4b9a-144">"Hello World!" başlığının</span><span class="sxs-lookup"><span data-stu-id="d4b9a-144">You should see the heading "Hello World!"</span></span> <span data-ttu-id="d4b9a-145">tarayıcıda gösterildiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-145">display in the browser.</span></span>

![Merhaba Dünya!][hello-world]

<span data-ttu-id="d4b9a-147">Kapsayıcınızı durdurmak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-147">To stop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="d4b9a-148">Kapsayıcıyı geliştirme makinenizden silin:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-148">Delete the container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="d4b9a-149">Görüntüyü kapsayıcı kayıt defterine gönderme</span><span class="sxs-lookup"><span data-stu-id="d4b9a-149">Push the image to the container registry</span></span>
<span data-ttu-id="d4b9a-150">Uygulamanın Docker'da çalıştığını doğruladıktan sonra, görüntüyü Azure Container Registry'de kayıt defterine gönderin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-150">After you verify that the application runs in Docker, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="d4b9a-151">Kapsayıcı kayıt defterinizde [kayıt defteri kimlik bilgileriniz](../container-registry/container-registry-authentication.md) ile oturum açmak için `docker login` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-151">Run `docker login` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="d4b9a-152">Aşağıdaki örnekte, bir Azure Active Directory [hizmet sorumlusunun](../active-directory/active-directory-application-objects.md) kimliği ve parolası geçirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-152">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="d4b9a-153">Örneğin, bir otomasyon senaryosu için kayıt defterinize bir hizmet sorumlusu atamış olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-153">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>  <span data-ttu-id="d4b9a-154">İsterseniz, kayıt defteri kullanıcı kimliğiniz ve parolanızı kullanarak oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="d4b9a-155">Aşağıdaki komut, görüntünün kayıt defterinize ait tam yolu içeren bir etiketini veya diğer adını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-155">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="d4b9a-156">Bu örnek, kayıt defterinin kökünde dağınıklığı önlemek için `samples` ad alanına görüntüyü yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-156">This example places the image in the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="d4b9a-157">Görüntüyü kapsayıcı kayıt defterinize gönderin:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-157">Push the image to your container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-the-docker-image-with-yeoman"></a><span data-ttu-id="d4b9a-158">Docker görüntüsünü Yeoman ile paketleme</span><span class="sxs-lookup"><span data-stu-id="d4b9a-158">Package the Docker image with Yeoman</span></span>
<span data-ttu-id="d4b9a-159">Linux için Service Fabric SDK’sı uygulamanızı oluşturmayı ve kapsayıcı görüntüsü eklemeyi kolaylaştıran bir [Yeoman](http://yeoman.io/) oluşturucu içerir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-159">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="d4b9a-160">Şimdi Yeoman kullanarak *SimpleContainerApp* adlı tek bir Docker kapsayıcısı olan bir uygulama oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-160">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="d4b9a-161">Service Fabric kapsayıcı uygulaması oluşturmak için, terminal penceresini açın ve `yo azuresfcontainer` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-161">To create a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="d4b9a-162">Uygulamanızı adlandırın (örneğin, "mycontainer").</span><span class="sxs-lookup"><span data-stu-id="d4b9a-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="d4b9a-163">Kapsayıcı kayıt defterindeki kapsayıcı görüntüsünün URL'sini sağlayın (örneğin, "").</span><span class="sxs-lookup"><span data-stu-id="d4b9a-163">Provide the URL for the container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="d4b9a-164">Bu görüntüde iş yükü giriş noktası tanımlanmış olduğundan, giriş komutlarının açıkça belirtilmesi gerekir (komutlar kapsayıcının içinde çalıştırılır ve bu da başlatma sonrasında kapsayıcıyı çalışır durumda tutar).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-164">This image has a workload entry-point defined, so need to explicitly specify input commands (commands run inside the container, which will keep the container running after startup).</span></span> 

<span data-ttu-id="d4b9a-165">"1" örnek sayısı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-165">Specify an instance count of "1".</span></span>

![Kapsayıcılar için Service Fabric Yeoman oluşturucusu][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="d4b9a-167">Bağlantı noktası eşlemesini ve kapsayıcı deposu kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4b9a-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="d4b9a-168">Kapsayıcı içinde alınmış hizmetinize iletişim için bir uç nokta gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="d4b9a-169">Şimdi ServiceManifest.xml dosyasındaki `Endpoint` öğesine protokol, bağlantı noktası ve tür ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-169">Now add the protocol, port, and type to an `Endpoint` in the ServiceManifest.xml file.</span></span> <span data-ttu-id="d4b9a-170">Bu makalede kapsayıcı hizmeti 4000 numaralı bağlantı noktasında dinler:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-170">For this article, the containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="d4b9a-171">`UriScheme` değerinin sağlanması, kapsayıcı uç noktasını bulunabilirlik için Service Fabric Adlandırma hizmetine otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-171">Providing the `UriScheme` automatically registers the container endpoint with the Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="d4b9a-172">Bu makalenin sonunda tam bir ServiceManifest.xml örnek dosyası verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-172">A full ServiceManifest.xml example file is provided at the end of this article.</span></span> 

<span data-ttu-id="d4b9a-173">ApplicationManifest.xml dosyasının `ContainerHostPolicies` kısmında bir `PortBinding` ilkesi belirterek kapsayıcı bağlantı noktasından ana bilgisayar bağlantı noktasına eşleme yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-173">Configure the container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="d4b9a-174">Bu makalede `ContainerPort` değeri 80 (Dockerfile içinde belirtildiği gibi kapsayıcı 80 numaralı bağlantı noktasını gösterir) ve `EndpointRef` değeri "myserviceTypeEndpoint"’tir (hizmet bildiriminde tanımlanan uç nokta).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-174">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (the endpoint defined in the service manifest).</span></span>  <span data-ttu-id="d4b9a-175">4000 numaralı bağlantı noktasında hizmete gelen istekler, kapsayıcı üzerindeki 80 numaralı bağlantı noktasıyla eşlenir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-175">Incoming requests to the service on port 4000 are mapped to port 80 on the container.</span></span>  <span data-ttu-id="d4b9a-176">Kapsayıcınızın özel bir depoda kimlik doğrulaması yapması gerekiyorsa, `RepositoryCredentials` öğesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-176">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="d4b9a-177">Bu makale için, myregistry.azurecr.io kapsayıcı kayıt defterine ait hesap adını ve parolayı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-177">For this article, add the account name and password for the myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-the-service-fabric-application"></a><span data-ttu-id="d4b9a-178">Service Fabric uygulamasını oluşturma ve paketleme</span><span class="sxs-lookup"><span data-stu-id="d4b9a-178">Build and package the Service Fabric application</span></span>
<span data-ttu-id="d4b9a-179">Service Fabric Yeoman şablonları, uygulamayı terminalden oluşturmak için kullanabileceğiniz bir [Gradle](https://gradle.org/) derleme betiği içerir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-179">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span> <span data-ttu-id="d4b9a-180">Uygulamayı derlemek ve paketlemek için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-180">To build and package the application, run the following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-the-application"></a><span data-ttu-id="d4b9a-181">Uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="d4b9a-181">Deploy the application</span></span>
<span data-ttu-id="d4b9a-182">Uygulama oluşturulduktan sonra Service Fabric CLI kullanarak yerel kümeye dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-182">Once the application is built, you can deploy it to the local cluster using the Service Fabric CLI.</span></span>

<span data-ttu-id="d4b9a-183">Yerel Service Fabric kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-183">Connect to the local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="d4b9a-184">Uygulama paketini kümenin görüntü deposuna kopyalamak, uygulama türünü kaydetmek ve uygulamanın bir örneğini oluşturmak için şablonda verilen yükleme betiğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-184">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="d4b9a-185">Bir tarayıcı açın ve http://localhost:19080/Explorer adresindeki Service Fabric Explorer’a gidin (Vagrant’ı Mac OS X üzerinde kullanıyorsanız localhost ifadesini sanal makinenin özel IP’si ile değiştirin).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-185">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="d4b9a-186">Uygulamalar düğümünü genişletin ve şu anda uygulamanızın türü için bir giriş ve bu türün ilk örneği için başka bir giriş olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-186">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

<span data-ttu-id="d4b9a-187">Çalışan kapsayıcıya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-187">Connect to the running container.</span></span>  <span data-ttu-id="d4b9a-188">4000 numaralı bağlantı noktasında döndürülen IP adresine işaret eden bir web tarayıcısı açın (örneğin, "http://localhost:4000").</span><span class="sxs-lookup"><span data-stu-id="d4b9a-188">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="d4b9a-189">"Hello World!" başlığının</span><span class="sxs-lookup"><span data-stu-id="d4b9a-189">You should see the heading "Hello World!"</span></span> <span data-ttu-id="d4b9a-190">tarayıcıda gösterildiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-190">display in the browser.</span></span>

![Merhaba Dünya!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="d4b9a-192">Temizleme</span><span class="sxs-lookup"><span data-stu-id="d4b9a-192">Clean up</span></span>
<span data-ttu-id="d4b9a-193">Yerel dağıtım kümesinden uygulama örneğini silmek ve uygulama türünün kaydını silmek için şablonda sağlanan kaldırma betiğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-193">Use the uninstall script provided in the template to delete the application instance from the local development cluster and unregister the application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="d4b9a-194">Görüntüyü kapsayıcı kayıt defterine gönderdikten sonra yerel görüntüyü geliştirme bilgisayarınızdan silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-194">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="d4b9a-195">Tam Service Fabric uygulaması ve hizmet bildirimleri örneği</span><span class="sxs-lookup"><span data-stu-id="d4b9a-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="d4b9a-196">Bu makalede kullanılan tam hizmet ve uygulama bildirimleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-196">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="d4b9a-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d4b9a-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="d4b9a-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d4b9a-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion 
       should match the Name and Version attributes of the ServiceManifest element defined in the 
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
    <!-- The section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using the 
         ServiceFabric PowerShell module.
         
         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount to 1.  On a multi-node production 
      cluster, set InstanceCount to -1 for the container service to run on every node in 
      the cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="d4b9a-199">Mevcut bir uygulamaya daha fazla hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="d4b9a-199">Adding more services to an existing application</span></span>

<span data-ttu-id="d4b9a-200">Yeoman kullanılarak zaten oluşturulmuş bir uygulamaya başka bir kapsayıcı hizmeti eklemek için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-200">To add another container service to an application already created using yeoman, perform the following steps:</span></span>

1. <span data-ttu-id="d4b9a-201">Dizini mevcut uygulamanın kök dizinine değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-201">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="d4b9a-202">Örneğin Yeoman tarafından oluşturulan uygulama `MyApplication` ise `cd ~/YeomanSamples/MyApplication` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="d4b9a-203">`yo azuresfcontainer:AddService` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d4b9a-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="d4b9a-204">Kapsayıcı zorla sonlandırılmadan önceki zaman aralığını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d4b9a-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="d4b9a-205">Hizmet silme (veya başka bir düğüme taşıma) başladıktan sonra, çalışma zamanının kapsayıcı kaldırılmadan önce ne kadar bekleyeceğine ilişkin bir zaman aralığı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-205">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="d4b9a-206">Zaman aralığını yapılandırma, kapsayıcıya `docker stop <time in seconds>` komutunu gönderir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-206">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="d4b9a-207">Daha ayrıntılı bilgi için bkz. [docker durdurma](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="d4b9a-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="d4b9a-208">Beklenecek zaman aralığı, `Hosting` bölümünde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-208">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="d4b9a-209">Aşağıdaki küme bildirimi kod parçacığı, bekleme aralığının nasıl ayarlandığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-209">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="d4b9a-210">Varsayılan zaman aralığı 10 saniye olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-210">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="d4b9a-211">Bu yapılandırma dinamik olduğundan, kümedeki yalnızca yapılandırmaya yönelik bir güncelleştirme zaman aşımını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-211">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="d4b9a-212">Kullanılmayan kapsayıcı görüntülerini kaldırmak için çalışma zamanını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4b9a-212">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="d4b9a-213">Service Fabric kümesini kullanılmayan kapsayıcı görüntülerini düğümden kaldıracak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-213">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="d4b9a-214">Bu yapılandırma, düğümde çok fazla kapsayıcı görüntüsü varsa yeniden disk alanı elde edilmesine imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-214">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="d4b9a-215">Bu özelliği etkinleştirmek için küme bildirimindeki `Hosting` bölümünü aşağıdaki kod parçacığında gösterildiği gibi güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="d4b9a-215">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="d4b9a-216">Silinmemesi gereken görüntüleri `ContainerImagesToSkip` parametresi altında belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-216">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="d4b9a-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d4b9a-217">Next steps</span></span>
* <span data-ttu-id="d4b9a-218">[Service Fabric’te kapsayıcı](service-fabric-containers-overview.md) çalıştırma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="d4b9a-219">[Kapsayıcı içinde .NET uygulaması dağıtma](service-fabric-host-app-in-a-container.md) öğreticisini okuyun.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-219">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="d4b9a-220">Service Fabric [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md) hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-220">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="d4b9a-221">GitHub’da [Service Fabric kapsayıcı kod örneklerine](https://github.com/Azure-Samples/service-fabric-dotnet-containers) bakın.</span><span class="sxs-lookup"><span data-stu-id="d4b9a-221">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
