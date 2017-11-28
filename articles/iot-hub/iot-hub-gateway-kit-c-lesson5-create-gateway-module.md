---
title: "aaaCreate ilk Azure IOT ağ geçidi modülünüzün | Microsoft Docs"
description: "Bir modül oluşturun ve tooa örnek uygulama toocustomize modülü davranışları ekleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="6aabc-103">Ders 5: İlk Azure IOT ağ geçidi modülünüzün oluşturma</span><span class="sxs-lookup"><span data-stu-id="6aabc-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="6aabc-104">Azure IOT kenar Java, .NET veya Node.js ile yazılmış toobuild modülleri sağlar, ancak bu öğreticide, bir modül C'deki oluşturmak için hello adım adım anlatılmaktadır</span><span class="sxs-lookup"><span data-stu-id="6aabc-104">While Azure IoT Edge allows you toobuild modules written in Java, .NET, or Node.js, this tutorial walks you through hello steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6aabc-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="6aabc-105">What you will do</span></span>

- <span data-ttu-id="6aabc-106">Derleme ve Intel NUC üzerinde hello hello_world örnek uygulamayı çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="6aabc-106">Compile and run hello hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="6aabc-107">Bir modül oluşturun ve Intel NUC üzerinde derleyin.</span><span class="sxs-lookup"><span data-stu-id="6aabc-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="6aabc-108">Merhaba yeni modül toohello hello_world örnek uygulaması eklemek ve ardından hello örnek Intel NUC üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6aabc-108">Add hello new module toohello hello_world sample app and then run hello sample on Intel NUC.</span></span> <span data-ttu-id="6aabc-109">bir zaman damgasına sahip "hello_world" ileti Hello yeni modül yazdırır.</span><span class="sxs-lookup"><span data-stu-id="6aabc-109">hello new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6aabc-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="6aabc-110">What you will learn</span></span>

- <span data-ttu-id="6aabc-111">Nasıl toocompile ve Intel NUC üzerinde bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6aabc-111">How toocompile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="6aabc-112">Nasıl toocreate bir modül.</span><span class="sxs-lookup"><span data-stu-id="6aabc-112">How toocreate a module.</span></span>
- <span data-ttu-id="6aabc-113">Nasıl tooadd modülü tooa örnek uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6aabc-113">How tooadd module tooa sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6aabc-114">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="6aabc-114">What you need</span></span>

<span data-ttu-id="6aabc-115">Ana bilgisayarınızda yüklü Azure IOT kenar.</span><span class="sxs-lookup"><span data-stu-id="6aabc-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="6aabc-116">Klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="6aabc-116">Folder structure</span></span>

<span data-ttu-id="6aabc-117">Ders 1 klonlanmış hello örnek kod Hello Ders 5 alt klasöründe, var olan bir `module` klasör ve `sample` klasör.</span><span class="sxs-lookup"><span data-stu-id="6aabc-117">In hello Lesson 5 subfolder of hello sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="6aabc-119">Merhaba `module/my_module` klasörü hello kaynak kodu ve komut dosyası toobuild hello modülü içerir.</span><span class="sxs-lookup"><span data-stu-id="6aabc-119">hello `module/my_module` folder contains hello source code and script toobuild hello module.</span></span>
- <span data-ttu-id="6aabc-120">Merhaba `sample` hello kaynak kodu ve komut dosyası toobuild hello örnek uygulaması içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="6aabc-120">hello `sample` folder contains hello source code and script toobuild hello sample app.</span></span>

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="6aabc-121">Derleme ve Intel NUC üzerinde hello hello_world örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6aabc-121">Compile and run hello hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="6aabc-122">Merhaba `hello_world` bir örnek oluşturur üzerinde hello dayalı bir ağ geçidi `hello_world.json` hello uygulamayla ilişkili hello iki önceden tanımlanmış modüller belirleyen dosya.</span><span class="sxs-lookup"><span data-stu-id="6aabc-122">hello `hello_world` sample creates a gateway based on hello `hello_world.json` file which specifies hello two predefined modules associated with hello app.</span></span> <span data-ttu-id="6aabc-123">Merhaba ağ geçidi "hello world" iletisini tooa dosya her 5 saniyede bir günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="6aabc-123">hello gateway logs a "hello world" message tooa file every 5 seconds.</span></span> <span data-ttu-id="6aabc-124">Bu bölümde, derleme ve çalıştırma hello `hello_world` kendi varsayılan modülü ile uygulama.</span><span class="sxs-lookup"><span data-stu-id="6aabc-124">In this section, you compile and run hello `hello_world` app with its default module.</span></span>

<span data-ttu-id="6aabc-125">toocompile ve Çalıştır hello `hello_world` uygulama, ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6aabc-125">toocompile and run hello `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="6aabc-126">Merhaba yapılandırma dosyalarını hello aşağıdaki komutları çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="6aabc-126">Initialize hello configuration files by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="6aabc-127">Merhaba ağ geçidi yapılandırma dosyasını Intel NUC MAC adresini hello ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6aabc-127">Update hello gateway configuration file with hello MAC address of Intel NUC.</span></span> <span data-ttu-id="6aabc-128">Merhaba Ders çok uyguladıysanız bu adımı atlayın[yapılandırma ve bırak örnek uygulamayı çalıştırma][config_ble].</span><span class="sxs-lookup"><span data-stu-id="6aabc-128">Skip this step if you have gone through hello lesson too[configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="6aabc-129">Merhaba aşağıdaki komutu çalıştırarak Hello ağ geçidi yapılandırma dosyasını açın:</span><span class="sxs-lookup"><span data-stu-id="6aabc-129">Open hello gateway configuration file by running hello following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="6aabc-130">Güncelleştirme hello ağ geçidi MAC adresi, [Intel NUC IOT ağ geçidi olarak ayarlama][setup_nuc]ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6aabc-130">Update hello gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save hello file.</span></span>

1. <span data-ttu-id="6aabc-131">Merhaba aşağıdaki komutu çalıştırarak Hello örnek kaynak kodu derleme:</span><span class="sxs-lookup"><span data-stu-id="6aabc-131">Compile hello sample source code by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="6aabc-132">Merhaba komut hello örnek kaynak kodu tooIntel NUC aktarır ve çalıştırır `build.sh` toocompile onu.</span><span class="sxs-lookup"><span data-stu-id="6aabc-132">hello command transfers hello sample source code tooIntel NUC and runs `build.sh` toocompile it.</span></span>

1. <span data-ttu-id="6aabc-133">Merhaba çalıştırmak `hello_world` hello aşağıdaki komutu çalıştırarak Intel NUC uygulamasını:</span><span class="sxs-lookup"><span data-stu-id="6aabc-133">Run hello `hello_world` app on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="6aabc-134">Merhaba komutu çalıştırır `../Tools/run-hello-world.js` belirtilen `config.json` Intel NUC üzerinde toostart hello örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="6aabc-134">hello command runs `../Tools/run-hello-world.js` that is specified in `config.json` toostart hello sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="6aabc-136">Yeni bir modül oluşturun ve Intel NUC üzerinde derleyin</span><span class="sxs-lookup"><span data-stu-id="6aabc-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="6aabc-137">Merhaba adımları, yeni bir modül oluşturmada size yol ve Intel NUC üzerinde derleyin.</span><span class="sxs-lookup"><span data-stu-id="6aabc-137">hello steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="6aabc-138">ileti aldıktan sonra bir zaman damgasına sahip Hello modülü yazdırır.</span><span class="sxs-lookup"><span data-stu-id="6aabc-138">hello module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="6aabc-139">Bu bölümde, ilk özelleştirilmiş ağ geçidi modülü oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6aabc-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="6aabc-140">Herhangi bir Azure IOT kenar modülü arabirimler aşağıdaki hello uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6aabc-140">Any Azure IoT Edge module must implement hello following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="6aabc-141">İsteğe bağlı olarak arabirimi aşağıdaki hello uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6aabc-141">You can optionally implement hello following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="6aabc-142">Merhaba Aşağıdaki diyagramda bir modülün hello önemli durumu yolları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6aabc-142">hello following diagram shows hello important state paths of a module.</span></span> <span data-ttu-id="6aabc-143">Merhaba kare dikdörtgenler hello modülü durumlar arasında taşındığında tooperform işlemleri uygulamak yöntemleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6aabc-143">hello square rectangles represent methods you implement tooperform operations when hello module moves between states.</span></span> <span data-ttu-id="6aabc-144">Merhaba Oval hello modülü olabilir ana durumlarıdır.</span><span class="sxs-lookup"><span data-stu-id="6aabc-144">hello ovals are major states hello module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="6aabc-146">Şimdi hello şablonunu temel alan bir modül oluşturalım:</span><span class="sxs-lookup"><span data-stu-id="6aabc-146">Now let’s create a module based on hello template:</span></span>

1. <span data-ttu-id="6aabc-147">Merhaba aşağıdaki komutu çalıştırarak Hello şablonu klasörü açın:</span><span class="sxs-lookup"><span data-stu-id="6aabc-147">Open hello template folder by running hello following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="6aabc-149">`src/my_module.c`bir modülün hello oluşturulması kolaylaştıran bir şablon olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="6aabc-149">`src/my_module.c` serves as a template that facilitates hello creation of a module.</span></span> <span data-ttu-id="6aabc-150">Merhaba şablon hello arabirimleri bildirir.</span><span class="sxs-lookup"><span data-stu-id="6aabc-150">hello template declares hello interfaces.</span></span> <span data-ttu-id="6aabc-151">Tek toodo ihtiyacınız olan tooadd mantığı toohello `MyModule_Receive` işlevi.</span><span class="sxs-lookup"><span data-stu-id="6aabc-151">All you need toodo is tooadd logic toohello `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="6aabc-152">`build.sh`Merhaba yapı betik toocompile hello Intel NUC üzerinde modülüdür.</span><span class="sxs-lookup"><span data-stu-id="6aabc-152">`build.sh` is hello build script toocompile hello module on Intel NUC.</span></span>
1. <span data-ttu-id="6aabc-153">Açık hello `src/my_module.c` dosya ve iki üst bilgi dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="6aabc-153">Open hello `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="6aabc-154">Aşağıdaki kodu toohello hello eklemek `MyModule_Receive` işlevi:</span><span class="sxs-lookup"><span data-stu-id="6aabc-154">Add hello following code toohello `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="6aabc-155">Güncelleştirme hello `config.json` dosya toospecify hello `workspace` , ana bilgisayar ve hello dağıtım yolunuza Intel NUC klasörü.</span><span class="sxs-lookup"><span data-stu-id="6aabc-155">Update hello `config.json` file toospecify hello `workspace` folder on your host computer and hello deployment path on Intel NUC.</span></span> <span data-ttu-id="6aabc-156">Derleme sırasında hello hello dosyalarında `workspace` klasörü aktarılan toohello dağıtım yolu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6aabc-156">During compiling, hello files in hello `workspace` folder will be transferred toohello deployment path.</span></span>

   1. <span data-ttu-id="6aabc-157">Açık hello `config.json` hello aşağıdaki komutu çalıştırarak dosya:</span><span class="sxs-lookup"><span data-stu-id="6aabc-157">Open hello `config.json` file by running hello following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="6aabc-158">Güncelleştirme `config.json` yapılandırma aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="6aabc-158">Update `config.json` with hello following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="6aabc-160">Merhaba modülü hello aşağıdaki komutu çalıştırarak derleyin:</span><span class="sxs-lookup"><span data-stu-id="6aabc-160">Compile hello module by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="6aabc-161">Merhaba komut hello kaynak kodu tooIntel NUC aktarır ve çalıştırır `build.sh` toocompile hello modülü.</span><span class="sxs-lookup"><span data-stu-id="6aabc-161">hello command transfers hello source code tooIntel NUC and runs `build.sh` toocompile hello module.</span></span>

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a><span data-ttu-id="6aabc-162">Merhaba modülü toohello hello_world örnek uygulaması ekleyin ve üzerinde Intel NUC hello uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6aabc-162">Add hello module toohello hello_world sample app and run hello app on Intel NUC</span></span>

<span data-ttu-id="6aabc-163">tooperform bu görev, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6aabc-163">tooperform this task, follow these steps:</span></span>

1. <span data-ttu-id="6aabc-164">Tüm hello kullanılabilir modül ikili dosyalarını (.so dosyaları) hello aşağıdaki komutu çalıştırarak üzerinde Intel NUC listesi:</span><span class="sxs-lookup"><span data-stu-id="6aabc-164">List all hello available module binaries (.so files) on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="6aabc-165">Merhaba ikili yolu `my_module` , derlenmiş olarak aşağıda listelenmiş olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="6aabc-165">hello binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="6aabc-166">Merhaba varsayılan oturum açma kullanıcı değiştirirseniz `config-gateway.json`, hello ikili yolu ile başlayacak `home/<your username>` yerine `root`.</span><span class="sxs-lookup"><span data-stu-id="6aabc-166">If you change hello default login username in `config-gateway.json`, hello binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="6aabc-167">Ekleme `my_module` toohello `hello_world` örnek uygulaması:</span><span class="sxs-lookup"><span data-stu-id="6aabc-167">Add `my_module` toohello `hello_world` sample app:</span></span>

   1. <span data-ttu-id="6aabc-168">Açık hello `hello_world.json` hello aşağıdaki komutu çalıştırarak dosya:</span><span class="sxs-lookup"><span data-stu-id="6aabc-168">Open hello `hello_world.json` file by running hello following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="6aabc-169">Aşağıdaki kodu toohello hello eklemek `modules` bölümü:</span><span class="sxs-lookup"><span data-stu-id="6aabc-169">Add hello following code toohello `modules` section:</span></span>

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      <span data-ttu-id="6aabc-170">Merhaba değerini `module.path` olmalıdır `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="6aabc-170">hello value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="6aabc-171">Merhaba kod bildirir `my_module` belirtilen hello modülü ikili hello konumunu yanı sıra hello ağ geçidi ile ilişkili toobe `module.path`.</span><span class="sxs-lookup"><span data-stu-id="6aabc-171">hello code declares `my_module` toobe associated with hello gateway as well as hello location of hello module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="6aabc-172">Aşağıdaki kodu toohello hello eklemek `links` bölümü:</span><span class="sxs-lookup"><span data-stu-id="6aabc-172">Add hello following code toohello `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="6aabc-173">Bu kod iletiler hello aktarılır belirtir `hello_world` modülü çok`my_module`.</span><span class="sxs-lookup"><span data-stu-id="6aabc-173">This code specifies that messages are transferred from hello `hello_world` module too`my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="6aabc-175">Merhaba çalıştırmak `hello_world` hello aşağıdaki komutu çalıştırarak örnek uygulaması:</span><span class="sxs-lookup"><span data-stu-id="6aabc-175">Run hello `hello_world` sample app by running hello following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="6aabc-176">Merhaba `--config` parametre zorlar hello `run-hello-world.js` toorun hello kullanarak komut dosyası `hello_world.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="6aabc-176">hello `--config` parameter forces hello `run-hello-world.js` script toorun by using hello `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="6aabc-178">Tebrikler.</span><span class="sxs-lookup"><span data-stu-id="6aabc-178">Congratulations.</span></span> <span data-ttu-id="6aabc-179">Bu yeni modül hello davranışını şimdi görebilirsiniz, yalnızca yazdırır "hello world" iletileri bir zaman damgasına sahip, farklı sonuç hello özgün "hello_world" modülünden çıkışı.</span><span class="sxs-lookup"><span data-stu-id="6aabc-179">You can now see hello behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from hello original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6aabc-180">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6aabc-180">Next Steps</span></span>

<span data-ttu-id="6aabc-181">Yeni bir modül oluşturulmuş, ağ geçidiniz toohello hello_world örnek ve get hello örnek uygulama toorun hello yeni modülüyle eklemiş.</span><span class="sxs-lookup"><span data-stu-id="6aabc-181">You’ve created a new module, added it toohello hello_world sample, and get hello sample app toorun with hello new module on your gateway.</span></span> <span data-ttu-id="6aabc-182">Azure IOT ağ geçidi modüller hakkında daha fazla toolearn istiyorsanız, daha fazla modülü örnekleri aşağıda bulabilirsiniz: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="6aabc-182">If you want toolearn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
