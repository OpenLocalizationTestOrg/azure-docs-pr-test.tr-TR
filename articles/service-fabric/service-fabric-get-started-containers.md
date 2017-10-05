---
title: "Azure Service Fabric kapsayıcı uygulaması oluşturma | Microsoft Docs"
description: "Azure Service Fabric üzerinde ilk Windows kapsayıcı uygulamanızı oluşturun.  Python uygulamasıyla bir Docker görüntüsü oluşturun, görüntüyü bir kapsayıcı kayıt defterine iletin, bir Service Fabric kapsayıcı uygulaması oluşturup dağıtın."
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
ms.openlocfilehash: 025bde02b3f342ec3399d51819d1fa8a91f11374
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="46e80-104">Windows üzerinde ilk Service Fabric kapsayıcı uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="46e80-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46e80-105">Windows</span><span class="sxs-lookup"><span data-stu-id="46e80-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="46e80-106">Linux</span><span class="sxs-lookup"><span data-stu-id="46e80-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="46e80-107">Bir Service Fabric kümesindeki Windows kapsayıcısında mevcut olan bir uygulamayı çalıştırmak için uygulamanızda herhangi bir değişiklik yapılması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="46e80-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="46e80-108">Bu makalede, Python [Flask](http://flask.pocoo.org/) web uygulaması içeren bir Docker görüntüsü oluşturma ve bunu Service Fabric kümesine dağıtma işlemlerinde size yol gösterilir.</span><span class="sxs-lookup"><span data-stu-id="46e80-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="46e80-109">Ayrıca, kapsayıcıya alınmış uygulamanızı [Azure Container Registry](/azure/container-registry/) aracılığıyla paylaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="46e80-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="46e80-110">Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="46e80-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="46e80-111">[Docker’a Genel Bakış](https://docs.docker.com/engine/understanding-docker/) makalesini okuyarak Docker hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46e80-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46e80-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="46e80-112">Prerequisites</span></span>
<span data-ttu-id="46e80-113">Şunları çalıştıran bir geliştirme bilgisayarı:</span><span class="sxs-lookup"><span data-stu-id="46e80-113">A development computer running:</span></span>
* <span data-ttu-id="46e80-114">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="46e80-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="46e80-115">[Service Fabric SDK’sı ve araçları](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="46e80-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="46e80-116">Windows için Docker.</span><span class="sxs-lookup"><span data-stu-id="46e80-116">Docker for Windows.</span></span>  <span data-ttu-id="46e80-117">[Windows için Docker CE edinme (dengeli)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="46e80-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="46e80-118">Docker’ı yükleyip başlattıktan sonra tepsi simgesine sağ tıklayıp **Windows kapsayıcılarına geç** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="46e80-118">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="46e80-119">Bu işlem, Windows temelinde Docker görüntülerini çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="46e80-119">This is required to run Docker images based on Windows.</span></span>

<span data-ttu-id="46e80-120">Kapsayıcı içeren Windows Server 2016 üzerinde üç veya daha fazla düğüme sahip bir Windows kümesi - [Küme oluşturun](service-fabric-cluster-creation-via-portal.md) veya [Service Fabric’i ücretsiz deneyin](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="46e80-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="46e80-121">Azure Container Registry’deki bir kayıt defteri - Azure aboneliğinizde [Kapsayıcı kayıt defteri oluşturun](../container-registry/container-registry-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="46e80-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-the-docker-container"></a><span data-ttu-id="46e80-122">Docker kapsayıcısını tanımlama</span><span class="sxs-lookup"><span data-stu-id="46e80-122">Define the Docker container</span></span>
<span data-ttu-id="46e80-123">Docker Hub’ında bulunan [Python görüntüsünü](https://hub.docker.com/_/python/) temel alan bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46e80-123">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="46e80-124">Docker kapsayıcınızı bir Dockerfile içinde tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="46e80-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="46e80-125">Dockerfile, kapsayıcınızın içindeki ortamı ayarlama, çalıştırmak istediğiniz uygulamayı yükleme ve bağlantı noktalarını eşleme yönergelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="46e80-125">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="46e80-126">Dockerfile, görüntüyü oluşturan `docker build` komutunun girdisidir.</span><span class="sxs-lookup"><span data-stu-id="46e80-126">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span>

<span data-ttu-id="46e80-127">Boş bir dizin oluşturun ve *Dockerfile* dosyasını oluşturun (dosya uzantısı kullanmayın).</span><span class="sxs-lookup"><span data-stu-id="46e80-127">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="46e80-128">Aşağıdakini *Dockerfile* dosyasına ekleyin ve değişikliklerinizi kaydedin:</span><span class="sxs-lookup"><span data-stu-id="46e80-128">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="46e80-129">Daha fazla bilgi için [Dockerfile başvurusunu](https://docs.docker.com/engine/reference/builder/) okuyun.</span><span class="sxs-lookup"><span data-stu-id="46e80-129">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="46e80-130">Basit web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="46e80-130">Create a simple web application</span></span>
<span data-ttu-id="46e80-131">Bağlantı noktası 80 üzerinden dinleyen ve "Merhaba Dünya!" başlığını döndüren bir Flask web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46e80-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="46e80-132">Aynı dizinde, *requirements.txt* dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46e80-132">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="46e80-133">Aşağıdakini dosyaya ekleyin ve değişikliklerinizi kaydedin:</span><span class="sxs-lookup"><span data-stu-id="46e80-133">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="46e80-134">Ayrıca, *app.py* dosyasını da oluşturun ve aşağıdakini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46e80-134">Also create the *app.py* file and add the following:</span></span>

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
## <a name="build-the-image"></a><span data-ttu-id="46e80-135">Görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="46e80-135">Build the image</span></span>
<span data-ttu-id="46e80-136">Web uygulamanızı çalıştıran görüntüyü oluşturmak için `docker build` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="46e80-136">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="46e80-137">PowerShell penceresini açın ve Dockerfile dosyasını içeren dizine gidin.</span><span class="sxs-lookup"><span data-stu-id="46e80-137">Open a PowerShell window and navigate to the directory containing the Dockerfile.</span></span> <span data-ttu-id="46e80-138">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="46e80-138">Run the following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="46e80-139">Bu komut Dockerfile içindeki yönergeleri kullanarak yeni görüntüyü oluşturur ve "helloworldapp" olarak adlandırır (-t etiketi).</span><span class="sxs-lookup"><span data-stu-id="46e80-139">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="46e80-140">Görüntü oluşturulduğunda, temel görüntü Docker Hub’ından alınır ve uygulamanızı temel görüntünün üstüne ekleyen yeni bir görüntü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="46e80-140">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="46e80-141">Oluşturma komutu tamamlandıktan sonra, yeni görüntü üzerindeki bilgileri görmek için `docker images` komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="46e80-141">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="46e80-142">Uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46e80-142">Run the application locally</span></span>
<span data-ttu-id="46e80-143">Görüntüyü kapsayıcı kayıt defterine göndermeden önce yerel olarak doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="46e80-143">Verify your image locally before pushing it the container registry.</span></span>  

<span data-ttu-id="46e80-144">Uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="46e80-144">Run the application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="46e80-145">*name*, çalışan kapsayıcıya bir ad verir (kapsayıcı kimliği yerine).</span><span class="sxs-lookup"><span data-stu-id="46e80-145">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="46e80-146">Kapsayıcı başladıktan sonra çalışan kapsayıcınıza bir tarayıcıdan bağlanabilmek için IP adresini bulun:</span><span class="sxs-lookup"><span data-stu-id="46e80-146">Once the container starts, find its IP address so that you can connect to your running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="46e80-147">Çalışan kapsayıcıya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="46e80-147">Connect to the running container.</span></span>  <span data-ttu-id="46e80-148">Döndürülen IP adresine işaret eden bir web tarayıcısı açın (örneğin, "http://172.31.194.61").</span><span class="sxs-lookup"><span data-stu-id="46e80-148">Open a web browser pointing to the IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="46e80-149">"Hello World!" başlığının</span><span class="sxs-lookup"><span data-stu-id="46e80-149">You should see the heading "Hello World!"</span></span> <span data-ttu-id="46e80-150">tarayıcıda gösterildiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="46e80-150">display in the browser.</span></span>

<span data-ttu-id="46e80-151">Kapsayıcınızı durdurmak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="46e80-151">To stop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="46e80-152">Kapsayıcıyı geliştirme makinenizden silin:</span><span class="sxs-lookup"><span data-stu-id="46e80-152">Delete the container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="46e80-153">Görüntüyü kapsayıcı kayıt defterine gönderme</span><span class="sxs-lookup"><span data-stu-id="46e80-153">Push the image to the container registry</span></span>
<span data-ttu-id="46e80-154">Kapsayıcının geliştirme makinenizde çalıştığını doğruladıktan sonra, görüntüyü Azure Container Registry içindeki kayıt defterinize gönderin.</span><span class="sxs-lookup"><span data-stu-id="46e80-154">After you verify that the container runs on your development machine, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="46e80-155">Kapsayıcı kayıt defterinizde [kayıt defteri kimlik bilgileriniz](../container-registry/container-registry-authentication.md) ile oturum açmak için ``docker login`` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="46e80-155">Run ``docker login`` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="46e80-156">Aşağıdaki örnekte, bir Azure Active Directory [hizmet sorumlusunun](../active-directory/active-directory-application-objects.md) kimliği ve parolası geçirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="46e80-156">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="46e80-157">Örneğin, bir otomasyon senaryosu için kayıt defterinize bir hizmet sorumlusu atamış olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46e80-157">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span> <span data-ttu-id="46e80-158">İsterseniz, kayıt defteri kullanıcı kimliğiniz ve parolanızı kullanarak oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46e80-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="46e80-159">Aşağıdaki komut, görüntünün kayıt defterinize ait tam yolu içeren bir etiketini veya diğer adını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46e80-159">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="46e80-160">Bu örnek, kayıt defterinin kökünde dağınıklığı önlemek için ```samples``` ad alanına görüntüyü yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="46e80-160">This example places the image in the ```samples``` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="46e80-161">Görüntüyü kapsayıcı kayıt defterinize gönderin:</span><span class="sxs-lookup"><span data-stu-id="46e80-161">Push the image to your container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-the-containerized-service-in-visual-studio"></a><span data-ttu-id="46e80-162">Visual Studio’da kapsayıcıya alınmış hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="46e80-162">Create the containerized service in Visual Studio</span></span>
<span data-ttu-id="46e80-163">Service Fabric SDK’sı ve araçları, kapsayıcıya alınmış uygulamalar oluşturmanıza yardımcı olan bir hizmet şablonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="46e80-163">The Service Fabric SDK and tools provide a service template to help you create a containerized application.</span></span>

1. <span data-ttu-id="46e80-164">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="46e80-164">Start Visual Studio.</span></span>  <span data-ttu-id="46e80-165">**Dosya** > **Yeni** > **Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="46e80-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="46e80-166">**Service Fabric uygulaması**’nı seçin, "MyFirstContainer" olarak adlandırın ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46e80-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="46e80-167">**Hizmet şablonları** listesinden **Konuk Kapsayıcı**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="46e80-167">Select **Guest Container** from the list of **service templates**.</span></span>
4. <span data-ttu-id="46e80-168">**Görüntü Adı** alanına, kapsayıcı deponuza gönderdiğiniz görüntünün dizini olan "myregistry.azurecr.io/samples/helloworldapp" değerini girin.</span><span class="sxs-lookup"><span data-stu-id="46e80-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", the image you pushed to your container repository.</span></span>
5. <span data-ttu-id="46e80-169">Hizmetinize bir ad verin ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46e80-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="46e80-170">İletişimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46e80-170">Configure communication</span></span>
<span data-ttu-id="46e80-171">Kapsayıcıya alınmış hizmetin iletişim sağlayabilmesi için bir uç nokta gerekir.</span><span class="sxs-lookup"><span data-stu-id="46e80-171">The containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="46e80-172">ServiceManifest.xml dosyasına protokol, bağlantı noktası ve tür bilgileriyle bir `Endpoint` öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46e80-172">Add an `Endpoint` element with the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="46e80-173">Bu makalede, kapsayıcıya alınmış hizmet 8081 numaralı bağlantı noktasında dinler.</span><span class="sxs-lookup"><span data-stu-id="46e80-173">For this article, the containerized service listens on port 8081.</span></span>  <span data-ttu-id="46e80-174">Bu örnekte, 8081 numaralı sabit bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="46e80-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="46e80-175">Hiçbir bağlantı noktası belirtilmemişse, uygulama bağlantı noktası aralığından rastgele bir bağlantı noktası seçilir.</span><span class="sxs-lookup"><span data-stu-id="46e80-175">If no port is specified, a random port from the application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="46e80-176">Uç nokta tanımlandığında, Service Fabric uç noktayı Adlandırma hizmetinde yayımlar.</span><span class="sxs-lookup"><span data-stu-id="46e80-176">By defining an endpoint, Service Fabric publishes the endpoint to the Naming service.</span></span>  <span data-ttu-id="46e80-177">Kümede çalışan diğer hizmetler bu kapsayıcıyı çözümleyebilir.</span><span class="sxs-lookup"><span data-stu-id="46e80-177">Other services running in the cluster can resolve this container.</span></span>  <span data-ttu-id="46e80-178">Ayrıca, [ters proxy](service-fabric-reverseproxy.md)’yi kullanarak kapsayıcıdan kapsayıcıya iletişim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46e80-178">You can also perform container-to-container communication using the [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="46e80-179">İletişim, ters proxy’nin HTTP dinleme bağlantı noktasını ve iletişim kurmak istediğiniz hizmetlerin adlarının ortam değişkenleri olarak sağlanmasıyla gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="46e80-179">Communication is performed by providing the reverse proxy HTTP listening port and the name of the services that you want to communicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="46e80-180">Ortam değişkenlerini yapılandırma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="46e80-180">Configure and set environment variables</span></span>
<span data-ttu-id="46e80-181">Ortam değişkenleri, hizmet bildirimindeki her kod paketi için belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="46e80-181">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="46e80-182">Bu özellik, kapsayıcı olarak mı dağıtıldıklarına yoksa konuk yürütülebilir dosyası olarak mı işlendiklerine bakılmaksızın tüm hizmetlerde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="46e80-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="46e80-183">Ortam değişkeni değerlerini, uygulama bildiriminde geçersiz kılabilir veya dağıtım sırasında uygulama parametresi olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46e80-183">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="46e80-184">Aşağıdaki hizmet bildirimi XML kod parçacığı, kod paketi için ortam değişkenlerinin nasıl belirtileceğini gösteren bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="46e80-184">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="46e80-185">Bu ortam değişkenleri, uygulama bildiriminde geçersiz kılınabilir:</span><span class="sxs-lookup"><span data-stu-id="46e80-185">These environment variables can be overridden in the application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="46e80-186">Kapsayıcı bağlantı noktasından konak bağlantı noktasına eşlemeyi ve kapsayıcıdan kapsayıcıya keşfi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46e80-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="46e80-187">Kapsayıcıyla iletişim kurmak için kullanılan konak bağlantı noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="46e80-187">Configure a host port used to communicate  with the container.</span></span> <span data-ttu-id="46e80-188">Bağlantı noktası bağlama, hizmetin kapsayıcı içinde dinlediği bağlantı noktasını konaktaki bağlantı noktasıyla eşler.</span><span class="sxs-lookup"><span data-stu-id="46e80-188">The port binding maps the port on which the service is listening inside the container to a port on the host.</span></span> <span data-ttu-id="46e80-189">ApplicationManifest.xml dosyasının `ContainerHostPolicies` öğesine bir `PortBinding` öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46e80-189">Add a `PortBinding` element in `ContainerHostPolicies` element of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="46e80-190">Bu makalede `ContainerPort` değeri 80 (Dockerfile içinde belirtildiği gibi kapsayıcı 80 numaralı bağlantı noktasını gösterir) ve `EndpointRef` değeri "Guest1TypeEndpoint" (hizmet bildiriminde daha önce tanımlanmış olan uç nokta) olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="46e80-190">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (the endpoint previously defined in the service manifest).</span></span>  <span data-ttu-id="46e80-191">8081 numaralı bağlantı noktasında hizmete gelen istekler, kapsayıcı üzerindeki 80 numaralı bağlantı noktasıyla eşlenir.</span><span class="sxs-lookup"><span data-stu-id="46e80-191">Incoming requests to the service on port 8081 are mapped to port 80 on the container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="46e80-192">Kapsayıcı kayıt defteri kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46e80-192">Configure container registry authentication</span></span>
<span data-ttu-id="46e80-193">ApplicationManifest.xml dosyasının `ContainerHostPolicies` öğesine bir `RepositoryCredentials` öğesi ekleyerek kapsayıcı kayıt defteri kimlik doğrulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="46e80-193">Configure container registry authentication by adding `RepositoryCredentials` to `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span> <span data-ttu-id="46e80-194">Hizmetin depodan kapsayıcı görüntüsünü indirmesini sağlayan myregistry.azurecr.io kapsayıcı kayıt defterine hesap ve parola ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46e80-194">Add the account and password for the myregistry.azurecr.io container registry, which allows the service to download the container image from the repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="46e80-195">Kümenin tüm düğümlerine dağıtılan bir şifreleme sertifikası kullanarak depo parolasını şifrelemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="46e80-195">We recommend that you encrypt the repository password by using an encipherment certificate that's deployed to all nodes of the cluster.</span></span> <span data-ttu-id="46e80-196">Service Fabric hizmet paketi kümeye dağıttığında, şifre metninin şifresini çözmek için şifreleme sertifikası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="46e80-196">When Service Fabric deploys the service package to the cluster, the encipherment certificate is used to decrypt the cipher text.</span></span>  <span data-ttu-id="46e80-197">Parolanın şifre metni Invoke-ServiceFabricEncryptText cmdlet’i kullanılarak oluşturulur ve bu metin ApplicationManifest.xml dosyasına eklenir.</span><span class="sxs-lookup"><span data-stu-id="46e80-197">The Invoke-ServiceFabricEncryptText cmdlet is used to create the cipher text for the password, which is added to the ApplicationManifest.xml file.</span></span>

<span data-ttu-id="46e80-198">Aşağıdaki betik, otomatik olarak imzalanan yeni bir sertifika oluşturup bunu PFX dosyasına aktarır.</span><span class="sxs-lookup"><span data-stu-id="46e80-198">The following script creates a new self-signed certificate and exports it to a PFX file.</span></span>  <span data-ttu-id="46e80-199">Sertifika, var olan bir anahtar kasasının içine aktarılır ve ardından Service Fabric kümesine dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="46e80-199">The certificate is imported into an existing key vault and then deployed to the Service Fabric cluster.</span></span>

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

# Create a self signed cert, export to PFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import the certificate to an existing key vault.  The key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add the certificate to all the VMs in the cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="46e80-200">[Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet’ini kullanarak parolayı şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="46e80-200">Encrypt the password using the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="46e80-201">Parolayı, [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet’i tarafından döndürülen şifre metniyle değiştirin ve `PasswordEncrypted` öğesini “true” olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="46e80-201">Replace the password with the cipher text returned by the [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` to "true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="46e80-202">Yalıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46e80-202">Configure isolation mode</span></span>
<span data-ttu-id="46e80-203">Windows, kapsayıcılar için iki yalıtım modunu destekler: İşlem ve Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="46e80-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="46e80-204">İşlem yalıtım moduyla, aynı konak makinesinde çalışan tüm kapsayıcılar çekirdeği konakla paylaşır.</span><span class="sxs-lookup"><span data-stu-id="46e80-204">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="46e80-205">Hyper-V yalıtım moduyla, çekirdekler her Hyper-V kapsayıcısı ile kapsayıcı konağı arasında yalıtılır.</span><span class="sxs-lookup"><span data-stu-id="46e80-205">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="46e80-206">Yalıtım modu, uygulama bildirimi dosyasında bulunan `ContainerHostPolicies` öğesinde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="46e80-206">The isolation mode is specified in the `ContainerHostPolicies` element in the application manifest file.</span></span> <span data-ttu-id="46e80-207">Belirtilebilen yalıtım modları `process`, `hyperv` ve `default` modlarıdır.</span><span class="sxs-lookup"><span data-stu-id="46e80-207">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="46e80-208">Varsayılan yalıtım modu, Windows Server konaklarında `process` ve Windows 10 konaklarında `hyperv` modudur.</span><span class="sxs-lookup"><span data-stu-id="46e80-208">The default isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="46e80-209">Aşağıdaki kod parçacığı uygulama bildirimi dosyasında yalıtım modunun nasıl belirtildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="46e80-209">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="46e80-210">Kaynak idaresini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46e80-210">Configure resource governance</span></span>
<span data-ttu-id="46e80-211">[Kaynak idaresi](service-fabric-resource-governance.md) kapsayıcının konakta kullanabildiği kaynakları kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="46e80-211">[Resource governance](service-fabric-resource-governance.md) restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="46e80-212">Uygulama bildiriminde belirtilen `ResourceGovernancePolicy` öğesi, hizmet kod paketinin kaynak sınırlarını tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="46e80-212">The `ResourceGovernancePolicy` element, which is specified in the application manifest, is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="46e80-213">Şu kaynaklar için kaynak sınırları ayarlanabilir: Memory, MemorySwap, CpuShares (CPU göreli ağırlığı), MemoryReservationInMB, BlkioWeight (BlockIO göreli ağırlığı).</span><span class="sxs-lookup"><span data-stu-id="46e80-213">Resource limits can be set for the following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="46e80-214">Bu örnekte, Guest1Pkg hizmet paketi bulunduğu küme düğümlerinde bir çekirdek alır.</span><span class="sxs-lookup"><span data-stu-id="46e80-214">In this example, service package Guest1Pkg gets one core on the cluster nodes where it is placed.</span></span>  <span data-ttu-id="46e80-215">Bellek sınırları mutlaktır; dolayısıyla, kod paketi 1024 MB bellekle (aynı genel garantili ayırmayla) sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="46e80-215">Memory limits are absolute, so the code package is limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="46e80-216">Kod paketleri (kapsayıcılar veya işlemler) bu sınırı aşan miktarda bellek ayıramazlar ve bunu denediklerinde yetersiz bellek özel durumu ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="46e80-216">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="46e80-217">Kaynak sınırı zorlamasının çalışması için, hizmet paketi içindeki tüm kod paketlerinin bellek sınırlarının belirtilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="46e80-217">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-the-container-application"></a><span data-ttu-id="46e80-218">Kapsayıcı uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="46e80-218">Deploy the container application</span></span>
<span data-ttu-id="46e80-219">Tüm değişikliklerinizi kaydedin ve uygulamayı derleyin.</span><span class="sxs-lookup"><span data-stu-id="46e80-219">Save all your changes and build the application.</span></span> <span data-ttu-id="46e80-220">Uygulamanızı yayımlamak için Çözüm Gezgini’nde **MyFirstContainer**’a sağ tıklayın ve **Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="46e80-220">To publish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="46e80-221">**Bağlantı Uç Noktası**’nda kümenin yönetim uç noktasını girin.</span><span class="sxs-lookup"><span data-stu-id="46e80-221">In **Connection Endpoint**, enter the management endpoint for the cluster.</span></span>  <span data-ttu-id="46e80-222">Örneğin, "containercluster.westus2.cloudapp.azure.com:19000".</span><span class="sxs-lookup"><span data-stu-id="46e80-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="46e80-223">İstemci bağlantı uç noktasını [Azure portalında](https://portal.azure.com) kümenizin Genel Bakış dikey penceresinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46e80-223">You can find the client connection endpoint in the Overview blade for your cluster in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="46e80-224">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46e80-224">Click **Publish**.</span></span>

<span data-ttu-id="46e80-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), bir Service Fabric kümesindeki uygulama ve düğümleri inceleyip yönetmeye yönelik web tabanlı bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="46e80-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="46e80-226">Bir tarayıcı açıp http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ dizinine gidin ve uygulama geliştirme adımlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="46e80-226">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow the application deployment.</span></span>  <span data-ttu-id="46e80-227">Uygulama dağıtılır, ancak görüntü küme düğümlerine yüklenene kadar hatalı durumdadır (bu işlem, görüntü boyutuna bağlı olarak biraz zaman alabilir): ![Hata][1]</span><span class="sxs-lookup"><span data-stu-id="46e80-227">The application deploys but is in an error state until the image is downloaded on the cluster nodes (which can take some time, depending on the image size): ![Error][1]</span></span>

<span data-ttu-id="46e80-228">Uygulamanın ```Ready``` durumu ![Hazır][2] olduğunda uygulama hazırdır</span><span class="sxs-lookup"><span data-stu-id="46e80-228">The application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="46e80-229">Bir tarayıcı açıp http://containercluster.westus2.cloudapp.azure.com:8081 adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="46e80-229">Open a browser and navigate to http://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="46e80-230">"Hello World!" başlığının</span><span class="sxs-lookup"><span data-stu-id="46e80-230">You should see the heading "Hello World!"</span></span> <span data-ttu-id="46e80-231">tarayıcıda gösterildiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="46e80-231">display in the browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="46e80-232">Temizleme</span><span class="sxs-lookup"><span data-stu-id="46e80-232">Clean up</span></span>
<span data-ttu-id="46e80-233">Küme çalışırken size ücret yansımaya devam edebilir, bu nedenle [kümenizi silmeyi](service-fabric-get-started-azure-cluster.md#remove-the-cluster) düşünün.</span><span class="sxs-lookup"><span data-stu-id="46e80-233">You continue to incur charges while the cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="46e80-234">[Taraf kümeleri](http://tryazureservicefabric.westus.cloudapp.azure.com/) birkaç saat sonra otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="46e80-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="46e80-235">Görüntüyü kapsayıcı kayıt defterine gönderdikten sonra yerel görüntüyü geliştirme bilgisayarınızdan silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46e80-235">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="46e80-236">Tam Service Fabric uygulaması ve hizmet bildirimleri örneği</span><span class="sxs-lookup"><span data-stu-id="46e80-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="46e80-237">Bu makalede kullanılan tam hizmet ve uygulama bildirimleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="46e80-237">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="46e80-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="46e80-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="46e80-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="46e80-239">ApplicationManifest.xml</span></span>
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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
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
    <!-- The section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="46e80-240">Kapsayıcı zorla sonlandırılmadan önceki zaman aralığını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="46e80-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="46e80-241">Hizmet silme (veya başka bir düğüme taşıma) başladıktan sonra, çalışma zamanının kapsayıcı kaldırılmadan önce ne kadar bekleyeceğine ilişkin bir zaman aralığı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46e80-241">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="46e80-242">Zaman aralığını yapılandırma, kapsayıcıya `docker stop <time in seconds>` komutunu gönderir.</span><span class="sxs-lookup"><span data-stu-id="46e80-242">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="46e80-243">Daha ayrıntılı bilgi için bkz. [docker durdurma](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="46e80-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="46e80-244">Beklenecek zaman aralığı, `Hosting` bölümünde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="46e80-244">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="46e80-245">Aşağıdaki küme bildirimi kod parçacığı, bekleme aralığının nasıl ayarlandığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="46e80-245">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="46e80-246">Varsayılan zaman aralığı 10 saniye olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="46e80-246">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="46e80-247">Bu yapılandırma dinamik olduğundan, kümedeki yalnızca yapılandırmaya yönelik bir güncelleştirme zaman aşımını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="46e80-247">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="46e80-248">Kullanılmayan kapsayıcı görüntülerini kaldırmak için çalışma zamanını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46e80-248">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="46e80-249">Service Fabric kümesini kullanılmayan kapsayıcı görüntülerini düğümden kaldıracak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46e80-249">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="46e80-250">Bu yapılandırma, düğümde çok fazla kapsayıcı görüntüsü varsa yeniden disk alanı elde edilmesine imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="46e80-250">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="46e80-251">Bu özelliği etkinleştirmek için küme bildirimindeki `Hosting` bölümünü aşağıdaki kod parçacığında gösterildiği gibi güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="46e80-251">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="46e80-252">Silinmemesi gereken görüntüleri `ContainerImagesToSkip` parametresi altında belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46e80-252">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="46e80-253">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46e80-253">Next steps</span></span>
* <span data-ttu-id="46e80-254">[Service Fabric’te kapsayıcı](service-fabric-containers-overview.md) çalıştırma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="46e80-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="46e80-255">[Kapsayıcı içinde .NET uygulaması dağıtma](service-fabric-host-app-in-a-container.md) öğreticisini okuyun.</span><span class="sxs-lookup"><span data-stu-id="46e80-255">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="46e80-256">Service Fabric [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md) hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="46e80-256">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="46e80-257">GitHub’da [Service Fabric kapsayıcı kod örneklerine](https://github.com/Azure-Samples/service-fabric-dotnet-containers) bakın.</span><span class="sxs-lookup"><span data-stu-id="46e80-257">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
