---
title: "Windows C kullanarak cihazı aaaConnect | Microsoft Docs"
description: "Nasıl tooconnect aygıt toohello Azure IOT paketi Uzaktan izleme çözümü Windows üzerinde çalışan C yazılmış bir uygulama kullanarak önceden yapılandırılmış açıklar."
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
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="b1d8a-103">Uzaktan izleme çözümü (Windows), cihaz toohello Bağlan</span><span class="sxs-lookup"><span data-stu-id="b1d8a-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="b1d8a-104">Windows C örnek bir çözüm oluşturun</span><span class="sxs-lookup"><span data-stu-id="b1d8a-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="b1d8a-105">Aşağıdaki adımları hello nasıl toocreate hello Uzaktan izleme ile iletişim kuran bir istemci uygulaması çözüm önceden yapılandırılmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="b1d8a-106">Bu uygulama C'de yazılmış ve yerleşik ve Windows üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="b1d8a-107">Visual Studio 2015 veya Visual Studio 2017 içinde bir başlangıç projesi oluşturun ve hello IOT Hub cihaz istemcisi NuGet paketleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b1d8a-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="b1d8a-108">Visual Studio'da hello Visual C++ kullanarak C konsol uygulaması oluşturma **Win32 konsol uygulaması** şablonu.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="b1d8a-109">Ad hello proje **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="b1d8a-110">Merhaba üzerinde **uygulama ayarları** hello sayfasında **Win32 Uygulama Sihirbazı'nı**, emin **konsol uygulaması** seçilidir ve işaretini **önceden derlenmiş Üstbilgi** ve **güvenlik geliştirme yaşam döngüsü (SDL) denetler**.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="b1d8a-111">İçinde **Çözüm Gezgini**, hello dosyaları stdafx.h, targetver.h ve stdafx.cpp silin.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="b1d8a-112">İçinde **Çözüm Gezgini**, hello dosya RMDevice.cpp tooRMDevice.c yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="b1d8a-113">İçinde **Çözüm Gezgini**, hello üzerinde sağ **RMDevice** proje ve ardından **Manage NuGet paketleri**.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="b1d8a-114">Tıklatın **Gözat**, ardından aramak ve NuGet paketleri aşağıdaki hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="b1d8a-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="b1d8a-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="b1d8a-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="b1d8a-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="b1d8a-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="b1d8a-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="b1d8a-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="b1d8a-118">İçinde **Çözüm Gezgini**, hello üzerinde sağ **RMDevice** proje ve ardından **özellikleri** tooopen hello projenin **özellik sayfaları**iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="b1d8a-119">Ayrıntılar için bkz [Visual C++ proje özelliklerini ayarlama][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="b1d8a-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="b1d8a-120">Hello tıklatın **bağlayıcı** klasörü, hello ardından **giriş** özellik sayfası.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="b1d8a-121">Ekleme **crypt32.lib** toohello **ek bağımlılıklar** özelliği.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="b1d8a-122">Tıklatın **Tamam** ve ardından **Tamam** yeniden toosave hello proje özellik değerleri.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="b1d8a-123">Merhaba Parson JSON kitaplığı toohello ekleme **RMDevice** proje ve gerekli hello eklemek `#include` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="b1d8a-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="b1d8a-124">Bilgisayarınızda uygun bir klasörde komutu aşağıdaki hello kullanarak hello Parson GitHub deposunu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="b1d8a-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="b1d8a-125">Merhaba parson.h ve parson.c dosyaları hello yerel hello Parson depo tooyour kopyadan kopyalamak **RMDevice** proje klasörü.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="b1d8a-126">Visual Studio'da hello sağ **RMDevice** proje, tıklatın **Ekle**ve ardından **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="b1d8a-127">Merhaba, **varolan öğeyi Ekle** iletişim, select hello parson.h ve parson.c dosyalarında hello **RMDevice** proje klasörü.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="b1d8a-128">Ardından **Ekle** tooadd bu iki dosya tooyour projesi.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="b1d8a-129">Visual Studio'da hello RMDevice.c dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="b1d8a-130">Merhaba varolan `#include` koddan hello ifadelerle:</span><span class="sxs-lookup"><span data-stu-id="b1d8a-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
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
    > <span data-ttu-id="b1d8a-131">Şimdi projenizi derleme tarafından ayarlanan hello doğru bağımlılıkları olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="b1d8a-132">Derleme ve hello örnek çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b1d8a-132">Build and run hello sample</span></span>

<span data-ttu-id="b1d8a-133">Kod tooinvoke hello eklemek **uzak\_izleme\_çalıştırmak** işlev oluşturmak ve hello cihaz uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="b1d8a-134">Hello yerine **ana** aşağıdaki kodu tooinvoke hello işleviyle **uzak\_izleme\_çalıştırmak** işlevi:</span><span class="sxs-lookup"><span data-stu-id="b1d8a-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="b1d8a-135">Tıklatın **yapı** ve ardından **yapı çözümü** toobuild Merhaba cihaz uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="b1d8a-136">İçinde **Çözüm Gezgini**, sağ hello **RMDevice** proje, tıklatın **hata ayıklama**ve ardından **başlangıç yeni örnek** toorun hello örnek.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="b1d8a-137">Merhaba uygulama örnek telemetri toohello önceden yapılandırılmış çözüm, hello çözüm panosunda ayarlamak istediğiniz özellik değerlerini alır ve hello çözüm panodan çağrılan toomethods yanıt gönderir gibi hello konsol iletileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b1d8a-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
