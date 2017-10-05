---
title: "C için Azure IOT cihaz SDK'sı | Microsoft Docs"
description: "C için Azure IOT cihaz SDK'sı ile başlayın ve IOT hub ile iletişim cihaz uygulamaları oluşturmayı öğrenin."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 459b630f28fe48064f4ba280974f3fdbdb82f0a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="8bb2d-103">C için Azure IOT cihaz SDK'sı</span><span class="sxs-lookup"><span data-stu-id="8bb2d-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="8bb2d-104">**Azure IOT cihaz SDK'sı** iletileri gelen iletileri gönderme ve alma işlemini basitleştirmek için tasarlanmış bir dizi kitaplıktır **Azure IOT Hub** hizmet.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="8bb2d-105">Her belirli bir platformu hedefleyen SDK, farklı çeşidi vardır, ancak bu makalede **C için Azure IOT cihaz SDK'sı**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="8bb2d-106">C için Azure IOT cihaz SDK'sı ANSI C taşınabilirliği en üst düzeye çıkarmak için (C99) yazılır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="8bb2d-107">Bu özellik kitaplıkları birden çok platformlarda ve cihazlarda özellikle disk en aza burada çalışması için oldukça uygun hale getirir ve bellek alanını önceliktir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="8bb2d-108">Çok çeşitli platformlar üzerinde SDK test edilmiştir vardır (bkz [Azure IOT cihaz katalog için onaylanmıştır](https://catalog.azureiotsuite.com/) Ayrıntılar için).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="8bb2d-109">Bu makalede Windows platformunda çalışan örnek kodu izlenecek yollar içerse de, bu makaledeki kod desteklenen platformlar aynı aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="8bb2d-110">Bu makalede c için Azure IOT cihaz SDK mimarisini sunar Cihaz kitaplığı başlatılamıyor, IOT Hub'ına veri göndermek ve buradan ileti almak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="8bb2d-111">Bu makaledeki bilgiler SDK'sını kullanmaya başlamak için yeterli olmalıdır, ancak ayrıca işaretçileri kitaplıkları hakkında ek bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="8bb2d-112">SDK mimarisi</span><span class="sxs-lookup"><span data-stu-id="8bb2d-112">SDK architecture</span></span>

<span data-ttu-id="8bb2d-113">Bulabileceğiniz [ **C için Azure IOT cihaz SDK'sı** ](https://github.com/Azure/azure-iot-sdk-c) GitHub depo ve görünüm ayrıntılarını API [C API Başvurusu](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="8bb2d-114">En son sürümünü kitaplıkları bulunabilir **ana** deponun dalı:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="8bb2d-115">Çekirdek uygulama SDK'ın bulunduğu **ıothub\_istemci** SDK en düşük API katmanı uyarlamasını içeren klasörü: **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="8bb2d-116">**IoTHubClient** kitaplığı IOT Hub'ına iletileri göndermek ve IOT Hub'ından iletileri almak için ham Mesajlaşma uygulama API'leri içerir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="8bb2d-117">Bu kitaplık kullanırken, ileti serileştirme uygulamak için sorumlu olan, ancak diğer ayrıntıları IOT Hub ile iletişim için işlenir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="8bb2d-118">**Seri hale getirici** klasörü yardımcı işlevleri ve istemci kitaplığı kullanılarak Azure IOT Hub'ına göndermeden önce verilerini seri hale getirmek nasıl Göster örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="8bb2d-119">Seri hale getirici kullanımını zorunlu değildir ve kolaylık sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="8bb2d-120">Kullanılacak **seri hale getirici** kitaplığı, IOT Hub ve ondan almayı beklediğinizi iletileri göndermek için veri modeli tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="8bb2d-121">Model tanımlandıktan sonra SDK serileştirme ayrıntılar hakkında endişelenmeden cihaz Bulut ve bulut-cihaz iletilerini ile kolayca çalışmanızı sağlayan bir API yüzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="8bb2d-122">Kitaplık MQTT ve AMQP gibi protokoller kullanarak aktarım uygulayan diğer açık kaynak kitaplıkları bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="8bb2d-123">**IoTHubClient** kitaplığı diğer açık kaynak kitaplıkları bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="8bb2d-124">[Azure C paylaşılan yardımcı programı](https://github.com/Azure/azure-c-shared-utility) kitaplığı çeşitli Azure ile ilgili C SDK gerekli (dizeler, liste işleme ve g/ç gibi) temel görevleri için ortak işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="8bb2d-125">[Azure uAMQP](https://github.com/Azure/azure-uamqp-c) bir istemci-tarafı uygulaması kısıtlı kaynak cihazlar için en iyi duruma getirilmiş AMQP olan kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="8bb2d-126">[Azure uMQTT](https://github.com/Azure/azure-umqtt-c) MQTT protokolünü uygulamaya yönelik genel amaçlı bir kitaplığı ve kısıtlı kaynak cihazlar için en iyi duruma getirilmiş kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="8bb2d-127">Bu kitaplıklar kullanımını örnek kodu bakarak anlamak daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="8bb2d-128">Aşağıdaki bölümlerde, SDK'da bulunan örnek uygulamalar çeşitli size yol.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="8bb2d-129">Bu kılavuz çeşitli özellikleri SDK'ın mimari katmanları ve API'leri nasıl giriş bilgileri için iyi bir fikir vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="8bb2d-130">Örneği çalıştırmadan önce</span><span class="sxs-lookup"><span data-stu-id="8bb2d-130">Before you run the samples</span></span>

<span data-ttu-id="8bb2d-131">Örnekler C için Azure IOT cihaz SDK'sı çalıştırmadan önce şunları yapmalısınız [IOT hub'ı hizmet örneği oluşturma](iot-hub-create-through-portal.md) Azure aboneliğinizde.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="8bb2d-132">Ardından aşağıdaki görevleri tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="8bb2d-133">Geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="8bb2d-133">Prepare your development environment</span></span>
* <span data-ttu-id="8bb2d-134">Cihaz kimlik bilgileri edinin.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="8bb2d-135">Geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="8bb2d-135">Prepare your development environment</span></span>

<span data-ttu-id="8bb2d-136">Paketleri (örneğin, Windows için NuGet veya apt_get Debian ve Ubuntu) ortak platformlar için sağlanır ve bu paketleri kullanılabilir olduğunda örnekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="8bb2d-137">Bazı durumlarda, Cihazınızda veya için SDK derleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="8bb2d-138">SDK derlemek ihtiyacınız varsa bkz [geliştirme ortamınızı hazırlama](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) GitHub deposunda.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="8bb2d-139">Örnek uygulama kodu almak için SDK'ın bir kopyasını Github'dan indirin.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="8bb2d-140">Kaynak sunucudan kopyanızı almak **ana** dalı [GitHub deposunu](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="8bb2d-141">Cihaz kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="8bb2d-141">Obtain the device credentials</span></span>

<span data-ttu-id="8bb2d-142">Örnek koda sahip olduğunuza göre sonraki bir şey yapmak için aygıt kimlik bilgileri kümesi almaktır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="8bb2d-143">Bir cihaz IOT hub'ı erişebilmeleri, önce cihaz IOT Hub kimlik kayıt defterine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="8bb2d-144">Cihazınızı eklediğinizde, cihazın IOT hub'ına bağlanabilmesi gereken cihaz kimlik bilgileri kümesi alır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="8bb2d-145">Sonraki bölümde açıklanan örnek uygulamalar bu kimlik bilgileri biçiminde beklediğiniz bir **cihaz bağlantı dizesi**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="8bb2d-146">IOT hub'ınızı yönetmenize yardımcı olmak için birkaç açık kaynaklı araçları vardır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="8bb2d-147">Adlı bir Windows uygulaması [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="8bb2d-148">Platformlar arası node.js CLI aracı adlı [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="8bb2d-149">Bu öğretici grafik kullanır *aygıt explorer* aracı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="8bb2d-150">Aynı zamanda *iothub-explorer* CLI aracını kullanmayı tercih ederseniz, aracı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="8bb2d-151">Cihaz ekleme de dahil olmak üzere IOT hub'da çeşitli işlevleri gerçekleştirmek için Azure IOT hizmeti kitaplıkları aygıtı explorer aracını kullanır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="8bb2d-152">Bir cihaz eklemek için aygıtı explorer aracını kullanırsanız, cihazınız için bir bağlantı dizesi alın.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="8bb2d-153">Örnek uygulamaları çalıştırmak için bu bağlantı dizesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="8bb2d-154">Cihaz explorer aracıyla bilmiyorsanız, aşağıdaki yordamı bir cihaz ekleme ve bir cihaz bağlantı dizesini almak için kullanmak üzere açıklar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="8bb2d-155">Cihaz explorer aracını yüklemek için bkz: [IOT Hub cihazları için cihaz Gezgini'ni kullanma](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="8bb2d-156">Programını çalıştırdığınızda, bu arabirim bakın:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-156">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="8bb2d-157">Girin, **IOT Hub bağlantı dizesine** tıklatın ve ilk alan **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="8bb2d-158">IOT Hub ile iletişim kurabilmesi için bu adımı aracı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="8bb2d-159">IOT Hub bağlantı dizesine yapılandırıldığında tıklatın **Yönetim** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="8bb2d-160">Bu sekme, IOT hub'ınıza kayıtlı cihazları yöneteceğiniz kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="8bb2d-161">Tıklayarak bir cihaz oluşturma **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="8bb2d-162">Bir iletişim kutusu (birincil ve ikincil) önceden doldurulmuş haldedir anahtarları bir kümesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="8bb2d-163">Girin bir **cihaz kimliği** ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="8bb2d-164">Cihaz oluşturulduğunda, cihazları, yeni oluşturduğunuz de dahil olmak üzere tüm kayıtlı cihazlar ile güncelleştirmeleri listeleyin.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="8bb2d-165">Yeni aygıtınızı sağ tıklatın, bu menü bakın:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="8bb2d-166">Seçerseniz **kopyalama seçili cihaz için bağlantı dizesi**, cihaz bağlantı dizesini panoya kopyalandı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="8bb2d-167">Cihaz bağlantı dizesi bir kopyasını tutun.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="8bb2d-168">Aşağıdaki bölümlerde açıklanan örnek uygulamaları çalıştırırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="8bb2d-169">Yukarıdaki adımları tamamladıktan sonra bazı kodları çalıştıran başlatmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="8bb2d-170">Her iki örnek bir sabit bir bağlantı dizesi girin olanak tanıyan ana kaynak dosyasının en üstte vardır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="8bb2d-171">Örneğin, karşılık gelen satırından **ıothub\_istemci\_örnek\_mqtt** uygulama şu şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="8bb2d-172">IoTHubClient kitaplığını kullanma</span><span class="sxs-lookup"><span data-stu-id="8bb2d-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="8bb2d-173">İçinde **ıothub\_istemci** klasöründe [azure-IOT-sdk-c](https://github.com/azure/azure-iot-sdk-c) deposunu var. bir **örnekleri** adlıbiruygulamaiçerenklasörde**ıothub\_istemci\_örnek\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="8bb2d-174">Windows sürümü, **ıothub\_istemci\_örnek\_mqtt** uygulama aşağıdaki Visual Studio çözümü içerir:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="8bb2d-175">Bu projeyi Visual Studio 2017 içinde açarsanız, en son sürüme projenizin hedefini ister kabul edin.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="8bb2d-176">Bu çözüm, tek bir proje içerir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-176">This solution contains a single project.</span></span> <span data-ttu-id="8bb2d-177">Bu çözümde yüklü olan dört NuGet paketleri vardır:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="8bb2d-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="8bb2d-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="8bb2d-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="8bb2d-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="8bb2d-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="8bb2d-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="8bb2d-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="8bb2d-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="8bb2d-182">Her zaman gereksinim duyduğunuz **Microsoft.Azure.C.SharedUtility** paketini SDK ile çalışırken.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="8bb2d-183">Bu örnek MQTT protokolünü kullanır, bu nedenle içermelidir **Microsoft.Azure.umqtt** ve **Microsoft.Azure.IoTHub.MqttTransport** paketleri (AMQP ve HTTP eşdeğer paketleri vardır).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="8bb2d-184">Örnek kullandığından **IoTHubClient** kitaplığı de dahil etmelisiniz **Microsoft.Azure.IoTHub.IoTHubClient** çözümünüzdeki paket.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="8bb2d-185">Örnek uygulama için uygulama Bul **ıothub\_istemci\_örnek\_mqtt.c** kaynak dosyası.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="8bb2d-186">Ne kullanmak için gerekli olan aracılığıyla yürütmek için bu örnek uygulama aşağıdaki adımları kullanın **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="8bb2d-187">Kitaplığı başlatılamıyor</span><span class="sxs-lookup"><span data-stu-id="8bb2d-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="8bb2d-188">Kitaplıkları ile çalışmaya başlamadan önce bazı platforma özgü başlatma gerçekleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="8bb2d-189">Örneğin, AMQP Linux'ta kullanmayı planlıyorsanız, OpenSSL kitaplığı başlatması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="8bb2d-190">Örnekleri [GitHub deposunu](https://github.com/Azure/azure-iot-sdk-c) yardımcı işlevini çağırın **platform\_init** ne zaman istemci başlar ve arama **platform\_deinit**çıkmadan önce işlevi.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="8bb2d-191">Bu işlevler platform.h üstbilgi dosyasında bildirilir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="8bb2d-192">Bu işlevler, hedef platformu için tanımlarını incelemek [depo](https://github.com/Azure/azure-iot-sdk-c) , istemci herhangi bir platforma özgü başlatma kod dahil gerekip gerekmediğini belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="8bb2d-193">Kitaplıkları ile çalışmaya başlamak için öncelikle bir IOT Hub istemci tanıtıcısı atayın:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="8bb2d-194">Bu işleve aygıt explorer aracından aldığınız cihaz bağlantı dizesi bir kopyasını geçirin.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="8bb2d-195">Ayrıca kullanılacak iletişim protokolü belirlemeniz.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="8bb2d-196">Bu örnek MQTT kullanır, ancak AMQP ve HTTP ayrıca seçeneklerdir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="8bb2d-197">Geçerli bir olduğunda **IOTHUB\_istemci\_İŞLEMEK**, IOT hub'ı gelen ve giden ileti gönderme ve alma için API'larını çağırma başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="8bb2d-198">İletileri gönder</span><span class="sxs-lookup"><span data-stu-id="8bb2d-198">Send messages</span></span>

<span data-ttu-id="8bb2d-199">Örnek uygulama, IOT hub'ınıza ileti göndermek için bir döngü ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="8bb2d-200">Aşağıdaki kod parçacığında:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-200">The following snippet:</span></span>

- <span data-ttu-id="8bb2d-201">Bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-201">Creates a message.</span></span>
- <span data-ttu-id="8bb2d-202">Bir özellik iletiye ekler.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-202">Adds a property to the message.</span></span>
- <span data-ttu-id="8bb2d-203">Bir ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-203">Sends a message.</span></span>

<span data-ttu-id="8bb2d-204">İlk olarak, bir ileti oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="8bb2d-205">İleti gönderme her zaman, veriler gönderilirken çağrılan bir geri çağırma işlevini referansı belirtin.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="8bb2d-206">Bu örnekte geri çağırma işlevi çağrılır **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="8bb2d-207">Aşağıdaki kod parçacığında bu geri çağırma işlevini gösterir:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-207">The following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="8bb2d-208">Çağrı Not **IoTHubMessage\_Destroy** iletiyle bittiğinde işlev.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="8bb2d-209">Bu işlev, ileti oluşturduğunuzda ayrılan kaynakları serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="8bb2d-210">İleti alma</span><span class="sxs-lookup"><span data-stu-id="8bb2d-210">Receive messages</span></span>

<span data-ttu-id="8bb2d-211">Bir ileti alma zaman uyumsuz bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="8bb2d-212">İlk olarak, aygıt bir ileti aldığında çağırmak için geri çağırma kaydedin:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-212">First, you register the callback to invoke when the device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="8bb2d-213">Son parametresi, istediğiniz void bir işaretçidir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="8bb2d-214">Örnekte, bir tamsayıya işaretçidir ancak daha karmaşık veri yapısı için bir işaretçi olabilir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="8bb2d-215">Bu parametre, paylaşılan durumuna bu işlev, çağrıyı ile çalışmak geri çağırma işlevi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="8bb2d-216">Aygıt bir ileti aldığında, kayıtlı bir geri çağırma işlevi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="8bb2d-217">Bu geri çağırma işlevini alır:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-217">This callback function retrieves:</span></span>

* <span data-ttu-id="8bb2d-218">Bağıntı kimliği iletisi ve ileti kimliği.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="8bb2d-219">İleti içeriği.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-219">The message content.</span></span>
* <span data-ttu-id="8bb2d-220">Tüm özel özellikler iletisi.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-220">Any custom properties from the message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="8bb2d-221">Kullanım **IoTHubMessage\_GetByteArray** bir dizedir ileti almak için işlevi.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="8bb2d-222">Kitaplığı kapatması</span><span class="sxs-lookup"><span data-stu-id="8bb2d-222">Uninitialize the library</span></span>

<span data-ttu-id="8bb2d-223">Gönderen olaylar ve alıcı iletileri bittiğinde, IOT kitaplığı kapatması.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="8bb2d-224">Bunu yapmak için aşağıdaki işlev çağrısı yürütün:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="8bb2d-225">Bu çağrı tarafından önceden ayrılmış kaynakları boşaltır **IoTHubClient\_CreateFromConnectionString** işlevi.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="8bb2d-226">Gördüğünüz gibi ile ileti gönderme ve alma kolay **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="8bb2d-227">Kitaplık kullanmak için hangi Protokolü dahil olmak üzere IOT Hub ile iletişim ayrıntılarını işler, (Geliştirici açısından bakıldığında, bir basit yapılandırma seçeneği budur).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="8bb2d-228">**IoTHubClient** kitaplığı da Cihazınızı IOT Hub'ına gönderir verilerini seri hale getirmek nasıl üzerinden kesin bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="8bb2d-229">Bazı durumlarda bu düzeyi denetiminin bir avantajı, ancak diğer ile endişelenmeniz istemediğiniz bir uygulama ayrıntısı şöyle.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="8bb2d-230">Bu durumda, kullanarak düşünebilirsiniz **seri hale getirici** sonraki bölümde açıklanan kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="8bb2d-231">Seri hale getirici kitaplığını kullanma</span><span class="sxs-lookup"><span data-stu-id="8bb2d-231">Use the serializer library</span></span>

<span data-ttu-id="8bb2d-232">Kavramsal olarak **seri hale getirici** kitaplığı bulunur üstünde **IoTHubClient** SDK'sı kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="8bb2d-233">Kullandığı **IoTHubClient** kitaplığı IOT Hub, ancak temel alınan iletişimi için ileti serileştirme postalarla yük geliştiriciden kaldırmak modelleme yetenekleri ekler.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="8bb2d-234">Nasıl bu kitaplığı works en iyi bir örnek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="8bb2d-235">İçinde **seri hale getirici** klasöründe [azure-IOT-sdk-c deposu](https://github.com/Azure/azure-iot-sdk-c), olan bir **örnekleri** adlı bir uygulama içeren klasörde **simplesample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="8bb2d-236">Bu örnek Windows sürümü aşağıdaki Visual Studio çözümü içerir:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="8bb2d-237">Bu projeyi Visual Studio 2017 içinde açarsanız, en son sürüme projenizin hedefini ister kabul edin.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="8bb2d-238">Önceki örnek olarak, bunun birkaç NuGet paketlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="8bb2d-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="8bb2d-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="8bb2d-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="8bb2d-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="8bb2d-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="8bb2d-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="8bb2d-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="8bb2d-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="8bb2d-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="8bb2d-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="8bb2d-244">Önceki örnekte, bu paketleri çoğunu gördünüz ancak **Microsoft.Azure.IoTHub.Serializer** yenidir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="8bb2d-245">Bu paket kullandığınızda gereklidir **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="8bb2d-246">Örnek uygulama uyarlamasını bulabilirsiniz **simplesample\_mqtt.c** dosya.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="8bb2d-247">Aşağıdaki bölümlerde bu örnek anahtar bölümleri size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="8bb2d-248">Kitaplığı başlatılamıyor</span><span class="sxs-lookup"><span data-stu-id="8bb2d-248">Initialize the library</span></span>

<span data-ttu-id="8bb2d-249">İle çalışmaya başlamak için **seri hale getirici** kitaplığı API'leri başlatma çağırın:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="8bb2d-250">Çağrı **seri hale getirici\_init** işlevi bir kerelik çağrısı ve temel kitaplığı başlatır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="8bb2d-251">Ardından, çağrı **IoTHubClient\_ÜM\_CreateFromConnectionString** giriş olarak aynı API işlevi **IoTHubClient** örnek.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="8bb2d-252">Bu çağrı, cihaz bağlantı dizesini ayarlar (Bu da Protokolü burada seçtiğiniz çağrıdır, kullanmak istediğiniz).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="8bb2d-253">Bu örnek taşıma olarak MQTT kullanır, ancak AMQP veya HTTP kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="8bb2d-254">Son olarak, arama **oluşturma\_modeli\_örneği** işlevi.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="8bb2d-255">**WeatherStation** model ad alanıdır ve **ContosoAnemometer** model adıdır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="8bb2d-256">Model örneği oluşturulduktan sonra ileti gönderme ve alma başlatmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="8bb2d-257">Ancak, anlaşılması önemlidir hangi bir modeldir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="8bb2d-258">Model tanımlayın</span><span class="sxs-lookup"><span data-stu-id="8bb2d-258">Define the model</span></span>

<span data-ttu-id="8bb2d-259">Bir model **seri hale getirici** kitaplığı tanımlar Cihazınızı IOT Hub'ına gönderebilirsiniz iletileri ve adlı iletileri *Eylemler* alabileceği modelleme dilde.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="8bb2d-260">C makroları olarak bir dizi kullanılarak bir modeli tanımlamak **simplesample\_mqtt** örnek uygulama:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="8bb2d-261">**Başlamak\_ad alanı** ve **son\_ad alanı** makroları iki bağımsız değişken olarak model ad alanı alın.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="8bb2d-262">Bu makrolar arasında herhangi bir şey tanımını modelinizi veya modelleri ve modelleri kullanın ve veri yapılarını olduğunu beklenir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="8bb2d-263">Bu örnekte, yok adlı tek bir model **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="8bb2d-264">Bu model Cihazınızı IOT Hub'ına gönderebilirsiniz veri iki parça tanımlar: **DeviceID** ve **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="8bb2d-265">Ayrıca Cihazınızı alabilir üç eylem (iletileri) tanımlar: **TurnFanOn**, **TurnFanOff**, ve **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="8bb2d-266">Her veri öğesi türüne sahip ve her eylemi bir ad (ve isteğe bağlı bir parametre kümesi) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="8bb2d-267">Model içinde tanımlanan eylemleri ve veri IOT Hub'ına iletileri göndermek için kullandıkları ve cihaza gönderilen iletilere yanıt API yüzeyi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="8bb2d-268">Bu model kullanımı örnek en iyi anlaşılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="8bb2d-269">İletileri gönder</span><span class="sxs-lookup"><span data-stu-id="8bb2d-269">Send messages</span></span>

<span data-ttu-id="8bb2d-270">IOT Hub'ına gönderebilirsiniz veri modelini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="8bb2d-271">Bu örnekte, iki veri öğelerinin anlaşılır bir tanımlanan kullanarak **WITH_DATA** makrosu.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="8bb2d-272">Göndermek için gereken birkaç adım vardır **DeviceID** ve **WindSpeed** bir IOT hub'ına değerleri.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="8bb2d-273">Göndermek istediğiniz veri kümesi için ilk şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="8bb2d-274">Daha önce tanımladığınız modeli üyeleri ayarlayarak değerleri ayarlamanıza olanak tanır bir **yapısı**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="8bb2d-275">Ardından, ileti göndermek istediğiniz sıralayın:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-275">Next, serialize the message you want to send:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="8bb2d-276">Bu kod cihaz-bulut bir arabelleğe serileştirir (tarafından başvurulan **hedef**).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="8bb2d-277">Kod sonra çağırır **sendMessage** işlevi IOT Hub'ına ileti göndermek için:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="8bb2d-278">Son parametresi, ikinci **IoTHubClient\_ÜM\_SendEventAsync** verileri başarıyla gönderildiğinde çağrılan bir geri çağırma işlevini başvurudur.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="8bb2d-279">Aşağıdaki örnekte geri çağırma işlevi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="8bb2d-280">İkinci parametresi, kullanıcı bağlamı için bir işaretçidir; aynı işaretçi geçirilen **IoTHubClient\_ÜM\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="8bb2d-281">Bu durumda, bağlam basit bir sayaç olmakla birlikte, istediğiniz herhangi bir şey olabilir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="8bb2d-282">Tüm olan cihaz bulut iletilerini göndermek için yoktur.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="8bb2d-283">Karşılamak üzere sol yalnızca ileti alma şeydir.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="8bb2d-284">İleti alma</span><span class="sxs-lookup"><span data-stu-id="8bb2d-284">Receive messages</span></span>

<span data-ttu-id="8bb2d-285">Yol iletileri iş ileti works benzer şekilde alma **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="8bb2d-286">İlk olarak, bir ileti geri çağırma işlevini kaydedin:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="8bb2d-287">Ardından, bir ileti alındığında çağrılan geri çağırma işlevi yazın:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="8bb2d-288">Bu kodu Demirbaş.--herhangi bir çözüm için aynı olur.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="8bb2d-289">Bu işlev iletiyi alır ve uygun işlev çağrısı aracılığıyla yönlendirme mvc'deki **yürütme\_KOMUTU**.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="8bb2d-290">Çağrılan işlev modelinizi Eylemler tanımını bu noktada bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="8bb2d-291">Modelinizi bir eylem tanımladığınızda, Cihazınızı karşılık gelen ileti aldığında çağrılan işlev uygulamak için gereken.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="8bb2d-292">Örneğin bu eylemi modelinizi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="8bb2d-293">Bu imza işleviyle tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="8bb2d-294">Nasıl işlevi modeldeki eylemin adı adıyla ve işlev parametrelerinin eylem için belirtilen parametreler eşleşen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="8bb2d-295">İlk parametre her zaman gereklidir ve model örneği için bir işaretçi içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="8bb2d-296">Cihaz Bu imza eşleşen bir ileti aldığında, ilgili işlev çağrılır.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="8bb2d-297">Bu nedenle, yanı sıra Demirbaş kod eklemek zorunda **IoTHubMessage**, olan modelinizde tanımlı her eylem için basit bir işlevin tanımlamanın yalnızca sağlasa da iletileri alma.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="8bb2d-298">Kitaplığı kapatması</span><span class="sxs-lookup"><span data-stu-id="8bb2d-298">Uninitialize the library</span></span>

<span data-ttu-id="8bb2d-299">Verileri gönderilirken ve alıcı iletileri bittiğinde, IOT kitaplığı kapatması:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="8bb2d-300">Bu üç işlevlerin her biri daha önce açıklanan üç başlatma işlevleri ile hizalar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="8bb2d-301">Bu API'larını çağırma önceden ayrılan kaynakları serbest sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bb2d-302">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8bb2d-302">Next Steps</span></span>

<span data-ttu-id="8bb2d-303">Bu makalede kitaplıklarda kullanma temelleri kapsamdaki **C için Azure IOT cihaz SDK'sı**. SDK'ın nelerin dahil olduğunu anlamak için yeterli bilgi sağlanan mimarisi ve Windows örnekleri ile çalışmaya başlamak nasıl.</span><span class="sxs-lookup"><span data-stu-id="8bb2d-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="8bb2d-304">Sonraki makalede açıklayarak SDK açıklaması devam [IoTHubClient Kitaplığı hakkında daha fazla](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="8bb2d-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="8bb2d-305">IOT Hub için geliştirme hakkında daha fazla bilgi için bkz: [Azure IOT SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="8bb2d-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="8bb2d-306">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="8bb2d-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8bb2d-307">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8bb2d-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
