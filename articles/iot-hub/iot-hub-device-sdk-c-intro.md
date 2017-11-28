---
title: "c aaaThe Azure IOT cihaz SDK'sı | Microsoft Docs"
description: "Hello Azure IOT cihaz SDK'sı için C başlamak ve öğrenin toocreate cihaz uygulamaları, iletişim kurma biçimini bir IOT hub ile."
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
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="3790f-103">C için Azure IOT cihaz SDK'sı</span><span class="sxs-lookup"><span data-stu-id="3790f-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="3790f-104">Merhaba **Azure IOT cihaz SDK'sı** olan bir dizi tasarlanmıştır Merhaba tooand alıcı iletileri gönderme toosimplify hello işlemi **Azure IOT Hub** hizmet.</span><span class="sxs-lookup"><span data-stu-id="3790f-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="3790f-105">Merhaba her belirli bir platformu hedefleyen SDK, farklı çeşidi vardır, ancak bu makalede hello **C için Azure IOT cihaz SDK'sı**.</span><span class="sxs-lookup"><span data-stu-id="3790f-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="3790f-106">c Hello Azure IOT cihaz SDK'sı ANSI C (C99) toomaximize taşınabilirlik yazılır.</span><span class="sxs-lookup"><span data-stu-id="3790f-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="3790f-107">Bu özellik hello kitaplıkları oldukça uygun toooperate birden çok platformlarda ve cihazlarda, özellikle disk en aza burada yapar ve bellek alanını önceliktir.</span><span class="sxs-lookup"><span data-stu-id="3790f-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="3790f-108">Çok çeşitli platformlar üzerinde hangi hello SDK'sı test vardır (Merhaba bkz [Azure IOT cihaz katalog için onaylanmıştır](https://catalog.azureiotsuite.com/) Ayrıntılar için).</span><span class="sxs-lookup"><span data-stu-id="3790f-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="3790f-109">İzlenecek yollar hello Windows platformunda çalışan örnek kodu, bu makalede bulunmasına karşın, bu makalede açıklanan hello kod hello desteklenen platformlar aynı aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="3790f-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="3790f-110">Bu makalede C. hello Azure IOT cihaz SDK'sı toohello mimarisini sunar Nasıl tooinitialize hello aygıtı kitaplığı veri tooIoT Hub, ileti gönderme ve ondan alma gösterir.</span><span class="sxs-lookup"><span data-stu-id="3790f-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="3790f-111">Bu makaledeki Hello bilgiler hello SDK kullanmaya yeterli tooget olmalı, ancak işaretçileri tooadditional hakkında da bilgi hello kitaplıkları sağlar.</span><span class="sxs-lookup"><span data-stu-id="3790f-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="3790f-112">SDK mimarisi</span><span class="sxs-lookup"><span data-stu-id="3790f-112">SDK architecture</span></span>

<span data-ttu-id="3790f-113">Merhaba bulabilirsiniz [ **C için Azure IOT cihaz SDK'sı** ](https://github.com/Azure/azure-iot-sdk-c) GitHub depo ve görünüm ayrıntılarını hello hello API [C API Başvurusu](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="3790f-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="3790f-114">Merhaba kitaplıkları en son sürümünü Hello hello bulunabilir **ana** hello deponun dalı:</span><span class="sxs-lookup"><span data-stu-id="3790f-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="3790f-115">Merhaba çekirdek hello SDK hello uygulamasıdır **ıothub\_istemci** hello en düşük API katmanı hello SDK'hello uyarlamasını içeren klasörü: Merhaba **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="3790f-116">Merhaba **IoTHubClient** kitaplığı IOT Hub'ından ileti alıp iletileri tooIoT Hub göndermeyi için ham Mesajlaşma uygulama API'leri içerir.</span><span class="sxs-lookup"><span data-stu-id="3790f-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="3790f-117">Bu kitaplık kullanırken, ileti serileştirme uygulamak için sorumlu olan, ancak diğer ayrıntıları IOT Hub ile iletişim için işlenir.</span><span class="sxs-lookup"><span data-stu-id="3790f-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="3790f-118">Merhaba **seri hale getirici** klasörü yardımcı işlevleri ve nasıl tooAzure IOT hub'ı kullanarak göndermeden önce tooserialize veri istemci kitaplığı hello Göster örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="3790f-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="3790f-119">Merhaba seri hale getirici Hello kullanımını zorunlu değildir ve kolaylık sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3790f-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="3790f-120">toouse hello **seri hale getirici** kitaplığı tooreceive dışarı beklediğiniz hello veri toosend tooIoT Hub ve hello iletileri belirten bir model tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3790f-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="3790f-121">Merhaba modeli tanımlandığında hello SDK, sağlayan bir API yüzeyi ile tooeasily iş cihaz bulut ile sağlar ve Serileştirme ayrıntılar hakkında kaygısı olmadan bulut-cihaz iletilerini hello.</span><span class="sxs-lookup"><span data-stu-id="3790f-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="3790f-122">Merhaba kitaplığı MQTT ve AMQP gibi protokoller kullanarak aktarım uygulayan diğer açık kaynak kitaplıkları bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3790f-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="3790f-123">Merhaba **IoTHubClient** kitaplığı diğer açık kaynak kitaplıkları bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="3790f-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="3790f-124">Merhaba [Azure C paylaşılan yardımcı programı](https://github.com/Azure/azure-c-shared-utility) kitaplığı çeşitli Azure ile ilgili C SDK gerekli (dizeler, liste işleme ve g/ç gibi) temel görevleri için ortak işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="3790f-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="3790f-125">Merhaba [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) bir istemci-tarafı uygulaması kısıtlı kaynak cihazlar için en iyi duruma getirilmiş AMQP olan kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="3790f-126">Merhaba [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) hello MQTT protokolünü uygulamaya yönelik genel amaçlı bir kitaplığı ve kısıtlı kaynak cihazlar için en iyi duruma getirilmiş kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="3790f-127">Bu kitaplıklar daha kolay toounderstand örnek kodu incelemeden tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3790f-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="3790f-128">Aşağıdaki bölümlerde Merhaba, birkaç hello SDK dahil hello örnek uygulamalar size yol.</span><span class="sxs-lookup"><span data-stu-id="3790f-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="3790f-129">Bu izlenecek iyi bir hello mimari katmanların hello SDK API'leri iş bir giriş toohow hello ve çeşitli özellikleri Merhaba eşitleyerek vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3790f-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="3790f-130">Merhaba örnekleri çalıştırmadan önce</span><span class="sxs-lookup"><span data-stu-id="3790f-130">Before you run hello samples</span></span>

<span data-ttu-id="3790f-131">Hello Azure IOT cihaz SDK'sı hello örnekleri için C çalıştırabilmeniz için önce şunları yapmalısınız [hello IOT hub'ı hizmet örneği oluşturma](iot-hub-create-through-portal.md) Azure aboneliğinizde.</span><span class="sxs-lookup"><span data-stu-id="3790f-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="3790f-132">Ardından hello aşağıdaki görevleri tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="3790f-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="3790f-133">Geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="3790f-133">Prepare your development environment</span></span>
* <span data-ttu-id="3790f-134">Cihaz kimlik bilgileri edinin.</span><span class="sxs-lookup"><span data-stu-id="3790f-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="3790f-135">Geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="3790f-135">Prepare your development environment</span></span>

<span data-ttu-id="3790f-136">Paketleri (örneğin, Windows için NuGet veya apt_get Debian ve Ubuntu) ortak platformlar için sağlanır ve bu paketleri kullanılabilir olduğunda hello örnekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3790f-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="3790f-137">Bazı durumlarda, Cihazınızda veya için toocompile hello SDK gerekir.</span><span class="sxs-lookup"><span data-stu-id="3790f-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="3790f-138">Toocompile hello SDK gerekirse bkz [geliştirme ortamınızı hazırlama](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) hello GitHub deposundaki.</span><span class="sxs-lookup"><span data-stu-id="3790f-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="3790f-139">tooobtain hello örnek uygulama kodu, bir hello SDK github'dan kopyasını indirme.</span><span class="sxs-lookup"><span data-stu-id="3790f-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="3790f-140">Hello hello kaynak kopyanızı almak **ana** hello dalı [GitHub deposunu](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="3790f-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="3790f-141">Merhaba aygıt kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="3790f-141">Obtain hello device credentials</span></span>

<span data-ttu-id="3790f-142">Merhaba örnek kaynak koda sahip olduğunuza göre hello sonraki şey toodo tooget aygıt kimlik bilgileri kümesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="3790f-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="3790f-143">Bir aygıt toobe mümkün tooaccess için IOT hub'ı, öncelikle hello aygıt toohello IOT Hub kimlik kayıt eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3790f-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="3790f-144">Cihazınızı eklediğinizde, hello aygıt toobe mümkün tooconnect toohello IOT hub için gereksinim duyduğunuz aygıt kimlik bilgisi kümesi alır.</span><span class="sxs-lookup"><span data-stu-id="3790f-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="3790f-145">Merhaba biçiminde Hello sonraki bölümde açıklanan hello örnek uygulamaları beklediğiniz bu kimlik bilgileri bir **cihaz bağlantı dizesi**.</span><span class="sxs-lookup"><span data-stu-id="3790f-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="3790f-146">IOT hub'ınızı yönetmek birkaç açık kaynaklı araçları toohelp vardır.</span><span class="sxs-lookup"><span data-stu-id="3790f-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="3790f-147">Adlı bir Windows uygulaması [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="3790f-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="3790f-148">Platformlar arası node.js CLI aracı adlı [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="3790f-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="3790f-149">Bu öğretici hello grafik kullanır *aygıt explorer* aracı.</span><span class="sxs-lookup"><span data-stu-id="3790f-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="3790f-150">Merhaba de kullanabilirsiniz *iothub-explorer* toouse CLI aracı tercih ederseniz, aracı.</span><span class="sxs-lookup"><span data-stu-id="3790f-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="3790f-151">Merhaba aygıtı explorer aracını hello Azure IOT hizmeti kitaplıkları tooperform cihaz ekleme de dahil olmak üzere IOT hub'da çeşitli işlevleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="3790f-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="3790f-152">Merhaba aygıt Gezgini aracı tooadd bir aygıtı kullanırsanız, cihazınız için bir bağlantı dizesi alın.</span><span class="sxs-lookup"><span data-stu-id="3790f-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="3790f-153">Bu bağlantı dizesi toorun hello örnek uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="3790f-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="3790f-154">Hello aygıt explorer aracıyla bilmiyorsanız, aşağıdaki yordamı hello açıklar nasıl toouse, tooadd bir cihaz ve cihaz bağlantı dizesini edinin.</span><span class="sxs-lookup"><span data-stu-id="3790f-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="3790f-155">tooinstall hello aygıtı explorer aracını bkz [nasıl toouse hello aygıt Explorer için IOT Hub cihazları](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="3790f-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="3790f-156">Merhaba programını çalıştırdığınızda, bu arabirim bakın:</span><span class="sxs-lookup"><span data-stu-id="3790f-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="3790f-157">Girin, **IOT Hub bağlantı dizesine** hello ilk alan ve tıklayın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="3790f-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="3790f-158">IOT Hub ile iletişim kurabilmesi için bu adımı hello aracı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="3790f-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="3790f-159">Merhaba IOT Hub bağlantı dizesine yapılandırıldığında, hello tıklatın **Yönetim** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="3790f-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="3790f-160">Bu sekme, IOT hub'ınıza kayıtlı hello cihazları yöneteceğiniz kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3790f-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="3790f-161">Merhaba tıklayarak bir cihaz oluşturma **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3790f-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="3790f-162">Bir iletişim kutusu (birincil ve ikincil) önceden doldurulmuş haldedir anahtarları bir kümesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3790f-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="3790f-163">Girin bir **cihaz kimliği** ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="3790f-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="3790f-164">Merhaba cihaz oluşturulduğunda, hello aygıtları tek, yeni oluşturduğunuz hello dahil olmak üzere tüm kayıtlı hello aygıtlarla güncelleştirmeleri listeleyin.</span><span class="sxs-lookup"><span data-stu-id="3790f-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="3790f-165">Yeni aygıtınızı sağ tıklatın, bu menü bakın:</span><span class="sxs-lookup"><span data-stu-id="3790f-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="3790f-166">Seçerseniz **kopyalama seçili cihaz için bağlantı dizesi**, hello cihaz bağlantı dizesidir, kopyalanan toohello Pano.</span><span class="sxs-lookup"><span data-stu-id="3790f-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="3790f-167">Merhaba cihaz bağlantı dizesi bir kopyasını tutun.</span><span class="sxs-lookup"><span data-stu-id="3790f-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="3790f-168">Aşağıdaki bölümlerde hello açıklanan hello örnek uygulamaları çalıştırırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="3790f-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="3790f-169">Yukarıdaki hello adımları tamamladıktan sonra bazı kodları çalıştıran hazır toostart demektir.</span><span class="sxs-lookup"><span data-stu-id="3790f-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="3790f-170">Her iki örnek bir sabit bir bağlantı dizesi tooenter olanak sağlayan hello ana kaynak dosyası hello üstünde vardır.</span><span class="sxs-lookup"><span data-stu-id="3790f-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="3790f-171">Örneğin, karşılık gelen satırından hello hello **ıothub\_istemci\_örnek\_mqtt** uygulama şu şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="3790f-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="3790f-172">Merhaba IoTHubClient kitaplığını kullanma</span><span class="sxs-lookup"><span data-stu-id="3790f-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="3790f-173">Hello içinde **ıothub\_istemci** hello klasöründe [azure-IOT-sdk-c](https://github.com/azure/azure-iot-sdk-c) deposunu var. bir **örnekleri** adlıbiruygulamaiçerenklasör**ıothub\_istemci\_örnek\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="3790f-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="3790f-174">Merhaba Windows hello sürümü **ıothub\_istemci\_örnek\_mqtt** uygulama, Visual Studio çözümü aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="3790f-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="3790f-175">Bu projeyi Visual Studio 2017 içinde açarsanız, hello istemleri tooretarget hello proje toohello en son sürümünü kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3790f-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="3790f-176">Bu çözüm, tek bir proje içerir.</span><span class="sxs-lookup"><span data-stu-id="3790f-176">This solution contains a single project.</span></span> <span data-ttu-id="3790f-177">Bu çözümde yüklü olan dört NuGet paketleri vardır:</span><span class="sxs-lookup"><span data-stu-id="3790f-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="3790f-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="3790f-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="3790f-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="3790f-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="3790f-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="3790f-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="3790f-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="3790f-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="3790f-182">Her zaman hello ihtiyacınız **Microsoft.Azure.C.SharedUtility** paketini hello SDK ile çalışırken.</span><span class="sxs-lookup"><span data-stu-id="3790f-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="3790f-183">Bu örnek hello MQTT protokolünü kullanır, bu nedenle hello içermelidir **Microsoft.Azure.umqtt** ve **Microsoft.Azure.IoTHub.MqttTransport** (eşdeğer paketi vardır AMQP ve HTTP için paketler ).</span><span class="sxs-lookup"><span data-stu-id="3790f-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="3790f-184">Merhaba örnek hello kullandığından **IoTHubClient** kitaplığı hello de dahil etmelisiniz **Microsoft.Azure.IoTHub.IoTHubClient** çözümünüzdeki paket.</span><span class="sxs-lookup"><span data-stu-id="3790f-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="3790f-185">Hello hello uygulama hello örnek uygulama için bulabilirsiniz **ıothub\_istemci\_örnek\_mqtt.c** kaynak dosyası.</span><span class="sxs-lookup"><span data-stu-id="3790f-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="3790f-186">Merhaba aşağıdaki adımları kullanın Bu örnek uygulama toowalk toouse hello gerekli olan size **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="3790f-187">Merhaba kitaplığı başlatılamıyor</span><span class="sxs-lookup"><span data-stu-id="3790f-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="3790f-188">Merhaba kitaplıkları ile çalışmaya başlamadan önce bazı platforma özgü başlatma tooperform gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3790f-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="3790f-189">Örneğin, Linux üzerinde toouse AMQP düşünüyorsanız hello OpenSSL kitaplığı başlatması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3790f-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="3790f-190">Merhaba hello örneklerinde [GitHub deposunu](https://github.com/Azure/azure-iot-sdk-c) hello yardımcı programı işlevi çağrısı **platform\_init** zaman hello istemci başlatır ve çağrı hello **platform\_deinit ** çıkmadan önce işlevi.</span><span class="sxs-lookup"><span data-stu-id="3790f-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="3790f-191">Bu işlevler hello platform.h üstbilgi dosyasında bildirilir.</span><span class="sxs-lookup"><span data-stu-id="3790f-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="3790f-192">Hedef platformunuzu hello için bu işlevlerin Hello tanımlarını incelemek [deposu](https://github.com/Azure/azure-iot-sdk-c) toodetermine tooinclude herhangi bir platforma özgü başlatma kod, istemci gerekmediğini.</span><span class="sxs-lookup"><span data-stu-id="3790f-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="3790f-193">Merhaba kitaplıklarla çalışma toostart önce bir IOT Hub istemci tanıtıcısı atayın:</span><span class="sxs-lookup"><span data-stu-id="3790f-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="3790f-194">Merhaba aygıt Gezgini aracı toothis işlevinden elde hello cihaz bağlantı dizesi bir kopyasını geçirin.</span><span class="sxs-lookup"><span data-stu-id="3790f-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="3790f-195">Ayrıca hello iletişim protokolü toouse belirlemeniz.</span><span class="sxs-lookup"><span data-stu-id="3790f-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="3790f-196">Bu örnek MQTT kullanır, ancak AMQP ve HTTP ayrıca seçeneklerdir.</span><span class="sxs-lookup"><span data-stu-id="3790f-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="3790f-197">Geçerli bir olduğunda **IOTHUB\_istemci\_İŞLEMEK**, hello API'leri toosend çağırma başlatın ve IOT Hub'ından iletileri tooand alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3790f-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="3790f-198">İletileri gönder</span><span class="sxs-lookup"><span data-stu-id="3790f-198">Send messages</span></span>

<span data-ttu-id="3790f-199">Merhaba örnek uygulaması bir döngü toosend iletileri tooyour IOT hub ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3790f-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="3790f-200">kod parçacığında hello:</span><span class="sxs-lookup"><span data-stu-id="3790f-200">hello following snippet:</span></span>

- <span data-ttu-id="3790f-201">Bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3790f-201">Creates a message.</span></span>
- <span data-ttu-id="3790f-202">Bir özellik toohello iletisi ekler.</span><span class="sxs-lookup"><span data-stu-id="3790f-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="3790f-203">Bir ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="3790f-203">Sends a message.</span></span>

<span data-ttu-id="3790f-204">İlk olarak, bir ileti oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3790f-204">First, create a message:</span></span>

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
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="3790f-205">İleti gönderme her zaman hello veriler gönderilirken çağrılan bir başvuru tooa geri çağırma işlevi belirtin.</span><span class="sxs-lookup"><span data-stu-id="3790f-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="3790f-206">Bu örnekte, hello geri çağırma işlevini çağırdı **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="3790f-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="3790f-207">Aşağıdaki kod parçacığında hello bu geri çağırma işlevini gösterir:</span><span class="sxs-lookup"><span data-stu-id="3790f-207">hello following snippet shows this callback function:</span></span>

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

<span data-ttu-id="3790f-208">Not hello çağrısı toohello **IoTHubMessage\_Destroy** hello iletisiyle bittiğinde işlev.</span><span class="sxs-lookup"><span data-stu-id="3790f-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="3790f-209">Bu işlev, selamlama iletisine oluştururken ayrılmış hello kaynakları serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="3790f-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="3790f-210">İleti alma</span><span class="sxs-lookup"><span data-stu-id="3790f-210">Receive messages</span></span>

<span data-ttu-id="3790f-211">Bir ileti alma zaman uyumsuz bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="3790f-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="3790f-212">İlk olarak, Hello aygıt bir ileti aldığında hello geri çağırma tooinvoke kaydedin:</span><span class="sxs-lookup"><span data-stu-id="3790f-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

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

<span data-ttu-id="3790f-213">Merhaba son istediğiniz void işaretçi toowhatever parametresidir.</span><span class="sxs-lookup"><span data-stu-id="3790f-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="3790f-214">İsteğe bağlı olarak Hello örnek bir işaretçi tooan tamsayı olan ancak bir işaretçi tooa olabilir daha karmaşık veri yapısı.</span><span class="sxs-lookup"><span data-stu-id="3790f-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="3790f-215">Bu parametre hello geri çağırma işlevi toooperate hello çağıran paylaşılan durumuyla bu işlevin üzerinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="3790f-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="3790f-216">Merhaba aygıt bir ileti aldığında hello kayıtlı geri çağırma işlevi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3790f-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="3790f-217">Bu geri çağırma işlevini alır:</span><span class="sxs-lookup"><span data-stu-id="3790f-217">This callback function retrieves:</span></span>

* <span data-ttu-id="3790f-218">Merhaba ileti kimliği ve hello iletisi bağıntı kimliği.</span><span class="sxs-lookup"><span data-stu-id="3790f-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="3790f-219">Merhaba ileti içeriği.</span><span class="sxs-lookup"><span data-stu-id="3790f-219">hello message content.</span></span>
* <span data-ttu-id="3790f-220">Tüm özel özellikler Başlangıç iletisi.</span><span class="sxs-lookup"><span data-stu-id="3790f-220">Any custom properties from hello message.</span></span>

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
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
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

<span data-ttu-id="3790f-221">Kullanım hello **IoTHubMessage\_GetByteArray** , bu örnekte bir dizedir işlev tooretrieve Başlangıç iletisi.</span><span class="sxs-lookup"><span data-stu-id="3790f-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="3790f-222">Merhaba kitaplığı kapatması</span><span class="sxs-lookup"><span data-stu-id="3790f-222">Uninitialize hello library</span></span>

<span data-ttu-id="3790f-223">Ne zaman gönderen olaylar işiniz bittiğinde ve iletileri alma, hello IOT kitaplığı kapatması.</span><span class="sxs-lookup"><span data-stu-id="3790f-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="3790f-224">toodo, bu nedenle, işlev çağrısı aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="3790f-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="3790f-225">Merhaba tarafından önceden ayrılmış hello kaynakları bu çağrıyı boşaltır **IoTHubClient\_CreateFromConnectionString** işlevi.</span><span class="sxs-lookup"><span data-stu-id="3790f-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="3790f-226">Gördüğünüz gibi kolay toosend olan ve hello ile iletilerini **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="3790f-227">Merhaba kitaplığı hangi protokolü toouse dahil olmak üzere IOT Hub ile iletişim kurmasını hello ayrıntılarını işleyen (Merhaba Geliştirici hello açısından basit yapılandırma seçeneği budur).</span><span class="sxs-lookup"><span data-stu-id="3790f-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="3790f-228">Merhaba **IoTHubClient** kitaplığı da tooserialize hello verilerini Cihazınızı tooIoT Hub nasıl göndereceğini üzerinden kesin bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="3790f-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="3790f-229">Bazı durumlarda bu düzeyi denetiminin bir avantajı, ancak diğer toobe ilgili istemediğiniz bir uygulama ayrıntısı şöyle.</span><span class="sxs-lookup"><span data-stu-id="3790f-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="3790f-230">Merhaba durum söz konusuysa hello kullanarak düşünebilirsiniz **seri hale getirici** hello sonraki bölümde açıklanan kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="3790f-231">Merhaba seri hale getirici kitaplığını kullanma</span><span class="sxs-lookup"><span data-stu-id="3790f-231">Use hello serializer library</span></span>

<span data-ttu-id="3790f-232">Kavramsal olarak hello **seri hale getirici** kitaplığı hello üstünde bulunur **IoTHubClient** hello SDK'sı kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="3790f-233">Merhaba kullanan **IoTHubClient** IOT Hub, ancak ile iletişim için temel alınan hello kitaplığının hello yük ileti serileştirme postalarla hello geliştiriciden kaldırmak modelleme yetenekleri ekler.</span><span class="sxs-lookup"><span data-stu-id="3790f-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="3790f-234">Nasıl bu kitaplığı works en iyi bir örnek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3790f-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="3790f-235">İç hello **seri hale getirici** hello klasöründe [azure-IOT-sdk-c deposu](https://github.com/Azure/azure-iot-sdk-c), olan bir **örnekleri** adlı bir uygulama içeren klasörde **simplesample \_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="3790f-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="3790f-236">Merhaba Windows sürümü bu örnek, Visual Studio çözümü aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="3790f-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="3790f-237">Bu projeyi Visual Studio 2017 içinde açarsanız, hello istemleri tooretarget hello proje toohello en son sürümünü kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3790f-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="3790f-238">Merhaba önceki örnek olarak, bunun birkaç NuGet paketlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="3790f-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="3790f-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="3790f-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="3790f-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="3790f-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="3790f-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="3790f-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="3790f-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="3790f-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="3790f-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="3790f-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="3790f-244">Bu paketleri hello önceki örnekteki çoğunu gördünüz ancak **Microsoft.Azure.IoTHub.Serializer** yenidir.</span><span class="sxs-lookup"><span data-stu-id="3790f-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="3790f-245">Bu paket hello kullandığınızda gereklidir **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="3790f-246">Merhaba örnek uygulaması hello uyarlamasını hello bulabilirsiniz **simplesample\_mqtt.c** dosya.</span><span class="sxs-lookup"><span data-stu-id="3790f-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="3790f-247">Hello aşağıdaki bölümlerde bu örnek anahtar bölümleri hello size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="3790f-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="3790f-248">Merhaba kitaplığı başlatılamıyor</span><span class="sxs-lookup"><span data-stu-id="3790f-248">Initialize hello library</span></span>

<span data-ttu-id="3790f-249">Merhaba ile çalışma toostart **seri hale getirici** çağrısı hello başlatma API'leri kitaplığı:</span><span class="sxs-lookup"><span data-stu-id="3790f-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

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

<span data-ttu-id="3790f-250">Merhaba çağrısı toohello **seri hale getirici\_init** işlevi tek seferlik bir çağrı ve başlatır hello temel kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="3790f-251">Sonra hello çağırın **IoTHubClient\_ÜM\_CreateFromConnectionString** hello olduğu gibi aynı API hello işlevi **IoTHubClient** örnek.</span><span class="sxs-lookup"><span data-stu-id="3790f-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="3790f-252">Bu çağrı, cihaz bağlantı dizesini ayarlar (Bu da hello Protokolü burada seçtiğiniz çağrıdır toouse istediğiniz).</span><span class="sxs-lookup"><span data-stu-id="3790f-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="3790f-253">Bu örnek hello taşıma olarak MQTT kullanır, ancak AMQP veya HTTP kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3790f-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="3790f-254">Son olarak, hello çağrısı **oluşturma\_modeli\_örneği** işlevi.</span><span class="sxs-lookup"><span data-stu-id="3790f-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="3790f-255">**WeatherStation** hello modelinin hello ad alanıdır ve **ContosoAnemometer** hello modeli hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="3790f-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="3790f-256">Merhaba model örneği oluşturulduktan sonra ileti toostart gönderme ve alma kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3790f-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="3790f-257">Ancak, önemli toounderstand hangi bir modeldir olur.</span><span class="sxs-lookup"><span data-stu-id="3790f-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="3790f-258">Merhaba modeli tanımlayın</span><span class="sxs-lookup"><span data-stu-id="3790f-258">Define hello model</span></span>

<span data-ttu-id="3790f-259">Merhaba modelinde **seri hale getirici** kitaplığı tanımlar Cihazınızı tooIoT olarak adlandırılan, Hub ve hello iletiler gönderebilir Merhaba iletileri *Eylemler* alabileceği dil modelleme hello içinde.</span><span class="sxs-lookup"><span data-stu-id="3790f-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="3790f-260">C makroları hello gibi bir dizi kullanılarak bir modeli tanımlamak **simplesample\_mqtt** örnek uygulama:</span><span class="sxs-lookup"><span data-stu-id="3790f-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="3790f-261">Merhaba **başlamak\_ad alanı** ve **son\_ad alanı** makroları iki bağımsız değişken olarak hello modelinin hello ad alın.</span><span class="sxs-lookup"><span data-stu-id="3790f-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="3790f-262">Bu makrolar arasında herhangi bir şey hello tanımını modeli veya modelleri ve hello modelleri kullanma hello veri yapılarını olduğunu beklenir.</span><span class="sxs-lookup"><span data-stu-id="3790f-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="3790f-263">Bu örnekte, yok adlı tek bir model **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="3790f-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="3790f-264">Bu model Cihazınızı tooIoT Hub gönderebilirsiniz veri iki parça tanımlar: **DeviceID** ve **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="3790f-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="3790f-265">Ayrıca Cihazınızı alabilir üç eylem (iletileri) tanımlar: **TurnFanOn**, **TurnFanOff**, ve **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="3790f-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="3790f-266">Her veri öğesi türüne sahip ve her eylemi bir ad (ve isteğe bağlı bir parametre kümesi) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3790f-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="3790f-267">Merhaba verilere ve eylemlere hello modelde tanımlanmış toosend iletileri tooIoT hub'ı kullanın ve gönderilen toomessages toohello aygıt yanıt API yüzeyi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3790f-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="3790f-268">Bu model kullanımı örnek en iyi anlaşılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3790f-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="3790f-269">İletileri gönder</span><span class="sxs-lookup"><span data-stu-id="3790f-269">Send messages</span></span>

<span data-ttu-id="3790f-270">Merhaba modeli tooIoT Hub gönderebilirsiniz hello verileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3790f-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="3790f-271">Bu örnekte, anlamına hello birini hello kullanılarak tanımlanan iki veri öğeleri **WITH_DATA** makrosu.</span><span class="sxs-lookup"><span data-stu-id="3790f-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="3790f-272">Çeşitli adımları gerekli toosend vardır **DeviceID** ve **WindSpeed** tooan IOT hub'ı değerleri.</span><span class="sxs-lookup"><span data-stu-id="3790f-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="3790f-273">Merhaba, ilk toosend istediğiniz tooset hello veri şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3790f-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="3790f-274">Hello daha önce tanımladığınız modeli tooset hello değerleri üyeleri ayarlayarak sağlayan bir **yapısı**.</span><span class="sxs-lookup"><span data-stu-id="3790f-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="3790f-275">Ardından, selamlama iletisine toosend istediğiniz sıralayın:</span><span class="sxs-lookup"><span data-stu-id="3790f-275">Next, serialize hello message you want toosend:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="3790f-276">Bu kod hello cihaz bulut tooa arabellek serileştiren (tarafından başvurulan **hedef**).</span><span class="sxs-lookup"><span data-stu-id="3790f-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="3790f-277">Merhaba kod sonra hello çağırır **sendMessage** toosend hello ileti tooIoT Hub işlev:</span><span class="sxs-lookup"><span data-stu-id="3790f-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="3790f-278">İkinci toolast parametresinin hello **IoTHubClient\_ÜM\_SendEventAsync** hello veri başarıyla gönderildiğinde çağrılan bir başvuru tooa geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="3790f-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="3790f-279">Merhaba örnek hello geri çağırma işlevi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3790f-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="3790f-280">Merhaba ikinci bir işaretçi toouser bağlamı parametredir; aynı işaretçi geçirilen çok hello**IoTHubClient\_ÜM\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="3790f-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="3790f-281">Bu durumda, basit bir sayaç hello bağlamı olduğu, ancak istediğiniz herhangi bir şey olabilir.</span><span class="sxs-lookup"><span data-stu-id="3790f-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="3790f-282">Tüm olan toosending cihaz bulut iletilerini yoktur.</span><span class="sxs-lookup"><span data-stu-id="3790f-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="3790f-283">Merhaba toocover sol yalnızca şeydir nasıl tooreceive iletileri.</span><span class="sxs-lookup"><span data-stu-id="3790f-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="3790f-284">İleti alma</span><span class="sxs-lookup"><span data-stu-id="3790f-284">Receive messages</span></span>

<span data-ttu-id="3790f-285">Bir ileti alma çalışır benzer şekilde iletileri çalışma hello toohello yöntemini **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="3790f-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="3790f-286">İlk olarak, bir ileti geri çağırma işlevini kaydedin:</span><span class="sxs-lookup"><span data-stu-id="3790f-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="3790f-287">Ardından, bir ileti alındığında çağrılan hello geri çağırma işlevi yazın:</span><span class="sxs-lookup"><span data-stu-id="3790f-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
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

<span data-ttu-id="3790f-288">Bu kodu Demirbaş.--onu sahip hello aynı için herhangi bir çözümü.</span><span class="sxs-lookup"><span data-stu-id="3790f-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="3790f-289">Bu işlev hello iletiyi alır ve bunu toohello uygun işlevi hello çağrısı ile çok yönlendirme mvc'deki**yürütme\_KOMUTU**.</span><span class="sxs-lookup"><span data-stu-id="3790f-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="3790f-290">adlı hello işlevi bu noktada hello Eylemler modelinizdeki hello tanımını bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3790f-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="3790f-291">Bir eylem modelinizde tanımladığınızda, gerekli tooimplement Cihazınızı hello karşılık gelen ileti aldığında çağrılan işlev.</span><span class="sxs-lookup"><span data-stu-id="3790f-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="3790f-292">Örneğin bu eylemi modelinizi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="3790f-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="3790f-293">Bu imza işleviyle tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="3790f-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="3790f-294">Nasıl hello hello işlevi hello eylemin hello modelinde hello adı adıyla ve hello işlevi hello parametreleriyle hello eylem için belirtilen başlangıç parametreleri aynı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3790f-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="3790f-295">Merhaba ilk parametresi, her zaman gereklidir ve modelinizi bir işaretçi toohello örneğini içerir.</span><span class="sxs-lookup"><span data-stu-id="3790f-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="3790f-296">Merhaba karşılık gelen işlev Hello cihaz Bu imza eşleşen bir ileti aldığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3790f-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="3790f-297">Bu nedenle, yanı sıra tooinclude hello Demirbaş kod sahip **IoTHubMessage**, olan modelinizde tanımlı her eylem için basit bir işlevin tanımlamanın yalnızca sağlasa da iletileri alma.</span><span class="sxs-lookup"><span data-stu-id="3790f-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="3790f-298">Merhaba kitaplığı kapatması</span><span class="sxs-lookup"><span data-stu-id="3790f-298">Uninitialize hello library</span></span>

<span data-ttu-id="3790f-299">Ne zaman verileri gönderilirken işiniz bittiğinde ve iletileri alma, hello IOT kitaplığı kapatması:</span><span class="sxs-lookup"><span data-stu-id="3790f-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="3790f-300">Bu üç işlevlerin her biri daha önce açıklanan hello üç başlatma işlevleriyle hizalar.</span><span class="sxs-lookup"><span data-stu-id="3790f-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="3790f-301">Bu API'larını çağırma önceden ayrılan kaynakları serbest sağlar.</span><span class="sxs-lookup"><span data-stu-id="3790f-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3790f-302">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3790f-302">Next Steps</span></span>

<span data-ttu-id="3790f-303">Bu makalede ele alınan hello hello kitaplıklarında kullanma temelleri hello **C için Azure IOT cihaz SDK'sı**. Merhaba SDK, mimarisi ve tooget Windows örnekleri hello ile çalışmaya nasıl başlatılacağını içereceği yeterli bilgi toounderstand sağlanan.</span><span class="sxs-lookup"><span data-stu-id="3790f-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="3790f-304">Merhaba sonraki makalede açıklayarak hello SDK hello açıklaması devam [hello IoTHubClient Kitaplığı hakkında daha fazla](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="3790f-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="3790f-305">IOT hub'ı geliştirme hakkında daha fazla toolearn bkz hello [Azure IOT SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="3790f-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="3790f-306">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="3790f-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3790f-307">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="3790f-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
