---
title: "İlk Azure IOT ağ geçidi modülü oluşturun | Microsoft Docs"
description: "Bir modül oluşturun ve modül davranışları özelleştirmek için bir örnek uygulama ekleyin."
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
ms.openlocfilehash: 5e28422158684c3aaf0ac3fdf5b19c80fbccfb02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="d36aa-103">Ders 5: İlk Azure IOT ağ geçidi modülünüzün oluşturma</span><span class="sxs-lookup"><span data-stu-id="d36aa-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="d36aa-104">Azure IOT kenar, Java, .NET veya Node.js ile yazılmış modüller oluşturmanıza olanak sağlar, ancak bu öğreticide, bir modül C'deki oluşturmak için adım adım anlatılmaktadır</span><span class="sxs-lookup"><span data-stu-id="d36aa-104">While Azure IoT Edge allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d36aa-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="d36aa-105">What you will do</span></span>

- <span data-ttu-id="d36aa-106">Derleme ve Intel NUC üzerinde hello_world örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d36aa-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="d36aa-107">Bir modül oluşturun ve Intel NUC üzerinde derleyin.</span><span class="sxs-lookup"><span data-stu-id="d36aa-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="d36aa-108">Yeni modül hello_world örnek uygulamaya ekleyin ve ardından örnek Intel NUC üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d36aa-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="d36aa-109">Bir zaman damgasına sahip "hello_world" ileti yeni modül yazdırır.</span><span class="sxs-lookup"><span data-stu-id="d36aa-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d36aa-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="d36aa-110">What you will learn</span></span>

- <span data-ttu-id="d36aa-111">Nasıl derlemek ve Intel NUC üzerinde bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d36aa-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="d36aa-112">Bir modül oluşturma</span><span class="sxs-lookup"><span data-stu-id="d36aa-112">How to create a module.</span></span>
- <span data-ttu-id="d36aa-113">Modül bir örnek uygulama ekleme.</span><span class="sxs-lookup"><span data-stu-id="d36aa-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d36aa-114">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="d36aa-114">What you need</span></span>

<span data-ttu-id="d36aa-115">Ana bilgisayarınızda yüklü Azure IOT kenar.</span><span class="sxs-lookup"><span data-stu-id="d36aa-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="d36aa-116">Klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="d36aa-116">Folder structure</span></span>

<span data-ttu-id="d36aa-117">Ders 1 klonlanmış örnek kod Ders 5 alt klasöründe, var olan bir `module` klasör ve `sample` klasör.</span><span class="sxs-lookup"><span data-stu-id="d36aa-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="d36aa-119">`module/my_module` Klasörü kaynak kodu ve modülü oluşturmak için komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="d36aa-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="d36aa-120">`sample` Klasörü kaynak kodu ve örnek uygulamanızı oluşturmak için komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="d36aa-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="d36aa-121">Derleme ve Intel NUC üzerinde hello_world örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d36aa-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="d36aa-122">`hello_world` Bir örnek oluşturur dayalı bir ağ geçidi `hello_world.json` uygulamayla ilişkili iki önceden tanımlanmış modüller belirleyen dosya.</span><span class="sxs-lookup"><span data-stu-id="d36aa-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="d36aa-123">Ağ Geçidi "hello world" iletisini her 5 saniyede bir dosyaya kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d36aa-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="d36aa-124">Bu bölümde, derleme ve çalıştırma `hello_world` kendi varsayılan modülü ile uygulama.</span><span class="sxs-lookup"><span data-stu-id="d36aa-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="d36aa-125">Derlemek ve çalıştırmak için `hello_world` uygulama, ana bilgisayarda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d36aa-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="d36aa-126">Aşağıdaki komutları çalıştırarak yapılandırma dosyalarını başlatın:</span><span class="sxs-lookup"><span data-stu-id="d36aa-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="d36aa-127">Ağ geçidi yapılandırma dosyasını Intel NUC MAC adresiyle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d36aa-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="d36aa-128">Ders aracılığıyla uyguladıysanız bu adımı atlayın [yapılandırma ve bırak örnek uygulamayı çalıştırma][config_ble].</span><span class="sxs-lookup"><span data-stu-id="d36aa-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="d36aa-129">Ağ geçidi yapılandırma dosyası, aşağıdaki komutu çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="d36aa-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="d36aa-130">Ağ Geçidi'nin MAC adresi güncelleştirme, [Intel NUC IOT ağ geçidi olarak ayarlama][setup_nuc]ve ardından dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d36aa-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="d36aa-131">Aşağıdaki komutu çalıştırarak örnek kaynak kodu derleme:</span><span class="sxs-lookup"><span data-stu-id="d36aa-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="d36aa-132">Komut için Intel NUC örnek kaynak kodu aktarır ve çalıştırır `build.sh` onu derlemek için.</span><span class="sxs-lookup"><span data-stu-id="d36aa-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="d36aa-133">Çalıştırma `hello_world` aşağıdaki komutu çalıştırarak Intel NUC uygulamasını:</span><span class="sxs-lookup"><span data-stu-id="d36aa-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="d36aa-134">Komutu çalıştırır `../Tools/run-hello-world.js` belirtilen `config.json` üzerinde Intel NUC örnek uygulamayı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="d36aa-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="d36aa-136">Yeni bir modül oluşturun ve Intel NUC üzerinde derleyin</span><span class="sxs-lookup"><span data-stu-id="d36aa-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="d36aa-137">Aşağıdaki adımlar, yeni bir modül oluşturmada size yol ve Intel NUC üzerinde derleyin.</span><span class="sxs-lookup"><span data-stu-id="d36aa-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="d36aa-138">İleti aldıktan sonra bir zaman damgasına sahip modülü yazdırır.</span><span class="sxs-lookup"><span data-stu-id="d36aa-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="d36aa-139">Bu bölümde, ilk özelleştirilmiş ağ geçidi modülü oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d36aa-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="d36aa-140">Herhangi bir Azure IOT kenar Modülü aşağıdaki arabirimleri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d36aa-140">Any Azure IoT Edge module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="d36aa-141">İsteğe bağlı olarak aşağıdaki arabirimi uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d36aa-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="d36aa-142">Aşağıdaki diyagramda bir modül önemli durumu yollarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d36aa-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="d36aa-143">Kare dikdörtgenler modülü durumlar arasında taşındığında işlemlerini gerçekleştirmek için uygulama yöntemleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d36aa-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="d36aa-144">Oval modülü olabilir ana durumlarıdır.</span><span class="sxs-lookup"><span data-stu-id="d36aa-144">The ovals are major states the module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="d36aa-146">Şimdi şablona dayalı bir modül oluşturalım:</span><span class="sxs-lookup"><span data-stu-id="d36aa-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="d36aa-147">Aşağıdaki komutu çalıştırarak şablonu klasörü açın:</span><span class="sxs-lookup"><span data-stu-id="d36aa-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="d36aa-149">`src/my_module.c`bir modül oluşturmayı kolaylaştıran bir şablon olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="d36aa-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="d36aa-150">Şablon arabirimler bildirir.</span><span class="sxs-lookup"><span data-stu-id="d36aa-150">The template declares the interfaces.</span></span> <span data-ttu-id="d36aa-151">Yapmanız gereken tek şey mantığı eklemek için `MyModule_Receive` işlevi.</span><span class="sxs-lookup"><span data-stu-id="d36aa-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="d36aa-152">`build.sh`Intel NUC modülünü derlemek için derleme komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="d36aa-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="d36aa-153">Açık `src/my_module.c` dosya ve iki üst bilgi dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="d36aa-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="d36aa-154">Aşağıdaki kodu ekleyin `MyModule_Receive` işlevi:</span><span class="sxs-lookup"><span data-stu-id="d36aa-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
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
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="d36aa-155">Güncelleştirme `config.json` belirtmek için dosya `workspace` ana bilgisayarınız ve Intel NUC dağıtım yolda klasör.</span><span class="sxs-lookup"><span data-stu-id="d36aa-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="d36aa-156">Derleme, dosyaları sırasında `workspace` klasörü dağıtım yoluna aktarılan.</span><span class="sxs-lookup"><span data-stu-id="d36aa-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="d36aa-157">Açık `config.json` aşağıdaki komutu çalıştırarak dosya:</span><span class="sxs-lookup"><span data-stu-id="d36aa-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="d36aa-158">Güncelleştirme `config.json` aşağıdaki yapılandırmaya sahip:</span><span class="sxs-lookup"><span data-stu-id="d36aa-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="d36aa-160">Modül, aşağıdaki komutu çalıştırarak derleyin:</span><span class="sxs-lookup"><span data-stu-id="d36aa-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="d36aa-161">Komut kaynak kodunu Intel NUC aktarır ve çalıştırır `build.sh` modülü derlemek için.</span><span class="sxs-lookup"><span data-stu-id="d36aa-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="d36aa-162">Modül hello_world örnek uygulamaya ekleyin ve üzerinde Intel NUC uygulama çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d36aa-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="d36aa-163">Bu görevi gerçekleştirmek için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d36aa-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="d36aa-164">Aşağıdaki komutu çalıştırarak tüm kullanılabilir modül ikili dosyalarını (.so dosyaları) Intel NUC listesi:</span><span class="sxs-lookup"><span data-stu-id="d36aa-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="d36aa-165">İkili yolunu `my_module` , derlenmiş olarak aşağıda listelenmiş olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="d36aa-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="d36aa-166">Varsayılan oturum açma kullanıcı değiştirirseniz `config-gateway.json`, ikili yolu ile başlar `home/<your username>` yerine `root`.</span><span class="sxs-lookup"><span data-stu-id="d36aa-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="d36aa-167">Ekleme `my_module` için `hello_world` örnek uygulaması:</span><span class="sxs-lookup"><span data-stu-id="d36aa-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="d36aa-168">Açık `hello_world.json` aşağıdaki komutu çalıştırarak dosya:</span><span class="sxs-lookup"><span data-stu-id="d36aa-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="d36aa-169">Aşağıdaki kodu ekleyin `modules` bölümü:</span><span class="sxs-lookup"><span data-stu-id="d36aa-169">Add the following code to the `modules` section:</span></span>

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

      <span data-ttu-id="d36aa-170">Değeri `module.path` olmalıdır `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="d36aa-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="d36aa-171">Kod bildirir `my_module` Belirtilen modül ikili konumunu yanı sıra ağ geçidi ile ilişkilendirilecek `module.path`.</span><span class="sxs-lookup"><span data-stu-id="d36aa-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="d36aa-172">Aşağıdaki kodu ekleyin `links` bölümü:</span><span class="sxs-lookup"><span data-stu-id="d36aa-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="d36aa-173">Bu kod iletileri aktarıldığı belirtir `hello_world` modülüne `my_module`.</span><span class="sxs-lookup"><span data-stu-id="d36aa-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="d36aa-175">Çalıştırma `hello_world` aşağıdaki komutu çalıştırarak örnek uygulaması:</span><span class="sxs-lookup"><span data-stu-id="d36aa-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="d36aa-176">`--config` Parametresi zorlar `run-hello-world.js` kullanarak çalıştırmak için betik `hello_world.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="d36aa-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="d36aa-178">Tebrikler.</span><span class="sxs-lookup"><span data-stu-id="d36aa-178">Congratulations.</span></span> <span data-ttu-id="d36aa-179">Bu yeni modül davranışını şimdi görebilirsiniz, yalnızca yazdırır "hello world" iletileri bir zaman damgasına sahip, farklı sonuç özgün "hello_world" modülünden çıkışı.</span><span class="sxs-lookup"><span data-stu-id="d36aa-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d36aa-180">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d36aa-180">Next Steps</span></span>

<span data-ttu-id="d36aa-181">Yeni bir modül oluşturulmuş, hello_world örnek ve get ile yeni modül ağ geçidiniz üzerinde çalıştırmak için örnek uygulama eklenen.</span><span class="sxs-lookup"><span data-stu-id="d36aa-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="d36aa-182">Azure IOT ağ geçidi modüller hakkında daha fazla bilgi edinmek istiyorsanız, daha fazla modülü örnekleri aşağıda bulabilirsiniz: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="d36aa-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
