---
title: "Windows C kullanarak bir cihazı bağlanma | Microsoft Docs"
description: "Windows üzerinde çalışan C yazılmış bir uygulama kullanarak Azure IOT paketi önceden yapılandırılmış Uzaktan izleme çözümü bir aygıt bağlanmaya açıklar."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: d222bcbd64f288d4091acb0ecd2922b9ceee57e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="baff6-103">Cihazınızı bağlama Uzaktan izleme önceden yapılandırılmış çözümü için (Windows)</span><span class="sxs-lookup"><span data-stu-id="baff6-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="baff6-104">Windows C örnek bir çözüm oluşturun</span><span class="sxs-lookup"><span data-stu-id="baff6-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="baff6-105">Aşağıdaki adımlar iletişim kuran bir istemci uygulamasının Uzaktan izleme önceden yapılandırılmış çözümü nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="baff6-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="baff6-106">Bu uygulama C'de yazılmış ve yerleşik ve Windows üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="baff6-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="baff6-107">Visual Studio 2015 veya Visual Studio 2017 içinde bir başlangıç projesi oluşturun ve IOT Hub cihaz istemcisi NuGet paketleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="baff6-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="baff6-108">Visual Studio'da Visual C++ kullanarak C konsol uygulaması oluşturma **Win32 konsol uygulaması** şablonu.</span><span class="sxs-lookup"><span data-stu-id="baff6-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="baff6-109">Proje adı **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="baff6-109">Name the project **RMDevice**.</span></span>
2. <span data-ttu-id="baff6-110">Üzerinde **uygulama ayarları** sayfasındaki **Win32 Uygulama Sihirbazı'nı**, emin **konsol uygulaması** seçilidir ve işaretini **önceden derlenmiş Üstbilgi** ve **güvenlik geliştirme yaşam döngüsü (SDL) denetler**.</span><span class="sxs-lookup"><span data-stu-id="baff6-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="baff6-111">İçinde **Çözüm Gezgini**, dosyaları stdafx.h, targetver.h ve stdafx.cpp silin.</span><span class="sxs-lookup"><span data-stu-id="baff6-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="baff6-112">İçinde **Çözüm Gezgini**, dosyayı RMDevice.cpp RMDevice.c için yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="baff6-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span></span>
5. <span data-ttu-id="baff6-113">İçinde **Çözüm Gezgini**, sağ tıklayın **RMDevice** proje ve ardından **Manage NuGet paketleri**.</span><span class="sxs-lookup"><span data-stu-id="baff6-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="baff6-114">Tıklatın **Gözat**, ardından aramak ve aşağıdaki NuGet paketlerini yükleyin:</span><span class="sxs-lookup"><span data-stu-id="baff6-114">Click **Browse**, then search for and install the following NuGet packages:</span></span>
   
   * <span data-ttu-id="baff6-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="baff6-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="baff6-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="baff6-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="baff6-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="baff6-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="baff6-118">İçinde **Çözüm Gezgini**, sağ tıklayın **RMDevice** proje ve ardından **özellikleri** projenin açmak için **özellik sayfaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="baff6-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="baff6-119">Ayrıntılar için bkz [Visual C++ proje özelliklerini ayarlama][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="baff6-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="baff6-120">Tıklatın **bağlayıcı** klasörü, ardından **giriş** özellik sayfası.</span><span class="sxs-lookup"><span data-stu-id="baff6-120">Click the **Linker** folder, then click the **Input** property page.</span></span>
8. <span data-ttu-id="baff6-121">Ekleme **crypt32.lib** için **ek bağımlılıklar** özelliği.</span><span class="sxs-lookup"><span data-stu-id="baff6-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span></span> <span data-ttu-id="baff6-122">Tıklatın **Tamam** ve ardından **Tamam** projeyi özellik değerlerini yeniden kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="baff6-122">Click **OK** and then **OK** again to save the project property values.</span></span>

<span data-ttu-id="baff6-123">Parson JSON kitaplığa eklemek **RMDevice** proje ve gerekli eklemek `#include` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="baff6-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="baff6-124">Bilgisayarınızda uygun klasöründe aşağıdaki komutu kullanarak Parson GitHub deposunu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="baff6-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="baff6-125">Parson depoya yerel kopyasını parson.h ve parson.c dosyalarını kopyalayın, **RMDevice** proje klasörü.</span><span class="sxs-lookup"><span data-stu-id="baff6-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="baff6-126">Visual Studio'da sağ **RMDevice** proje, tıklatın **Ekle**ve ardından **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="baff6-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="baff6-127">İçinde **varolan öğeyi Ekle** parson.h ve parson.c Dosyaları iletişim kutusunda **RMDevice** proje klasörü.</span><span class="sxs-lookup"><span data-stu-id="baff6-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span></span> <span data-ttu-id="baff6-128">Ardından **Ekle** bu iki dosyayı projenize eklemek için.</span><span class="sxs-lookup"><span data-stu-id="baff6-128">Then click **Add** to add these two files to your project.</span></span>

1. <span data-ttu-id="baff6-129">Visual Studio'da RMDevice.c dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="baff6-129">In Visual Studio, open the RMDevice.c file.</span></span> <span data-ttu-id="baff6-130">Varolan `#include` deyimleri ile aşağıdaki kodu:</span><span class="sxs-lookup"><span data-stu-id="baff6-130">Replace the existing `#include` statements with the following code:</span></span>
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > <span data-ttu-id="baff6-131">Artık, projenizi derleme tarafından ayarlanan doğru bağımlılıkları olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="baff6-131">Now you can verify that your project has the correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="baff6-132">Derleme ve örnek çalıştırma</span><span class="sxs-lookup"><span data-stu-id="baff6-132">Build and run the sample</span></span>

<span data-ttu-id="baff6-133">Çağırmak için kodu ekleyin **uzak\_izleme\_çalıştırmak** işlev oluşturmak ve cihaz uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="baff6-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="baff6-134">Değiştir **ana** işlevi çağırmak için aşağıdaki kod ile **uzak\_izleme\_çalıştırmak** işlevi:</span><span class="sxs-lookup"><span data-stu-id="baff6-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="baff6-135">Tıklatın **yapı** ve ardından **yapı çözümü** aygıt uygulama oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="baff6-135">Click **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="baff6-136">İçinde **Çözüm Gezgini**, sağ **RMDevice** projesi,'ı tıklatın **hata ayıklama**ve ardından **başlangıç yeni örnek** örneği çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="baff6-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span></span> <span data-ttu-id="baff6-137">Konsol Uygulama önceden yapılandırılmış çözümü örnek telemetri gönderir, istenen özellik değerleri çözüm panosunda alır ve çözüm panodan çağrılan yöntemlerine yanıt iletileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="baff6-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
