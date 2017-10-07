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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Ders 5: İlk Azure IOT ağ geçidi modülünüzün oluşturma
Azure IOT kenar Java, .NET veya Node.js ile yazılmış toobuild modülleri sağlar, ancak bu öğreticide, bir modül C'deki oluşturmak için hello adım adım anlatılmaktadır

## <a name="what-you-will-do"></a>Ne yapacağını

- Derleme ve Intel NUC üzerinde hello hello_world örnek uygulamayı çalıştırma.
- Bir modül oluşturun ve Intel NUC üzerinde derleyin.
- Merhaba yeni modül toohello hello_world örnek uygulaması eklemek ve ardından hello örnek Intel NUC üzerinde çalıştırın. bir zaman damgasına sahip "hello_world" ileti Hello yeni modül yazdırır.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

- Nasıl toocompile ve Intel NUC üzerinde bir örnek uygulamayı çalıştırın.
- Nasıl toocreate bir modül.
- Nasıl tooadd modülü tooa örnek uygulaması.

## <a name="what-you-need"></a>Ne gerekiyor

Ana bilgisayarınızda yüklü Azure IOT kenar.

## <a name="folder-structure"></a>Klasör yapısı

Ders 1 klonlanmış hello örnek kod Hello Ders 5 alt klasöründe, var olan bir `module` klasör ve `sample` klasör.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- Merhaba `module/my_module` klasörü hello kaynak kodu ve komut dosyası toobuild hello modülü içerir.
- Merhaba `sample` hello kaynak kodu ve komut dosyası toobuild hello örnek uygulaması içeren klasör.

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>Derleme ve Intel NUC üzerinde hello hello_world örnek uygulamayı çalıştırma

Merhaba `hello_world` bir örnek oluşturur üzerinde hello dayalı bir ağ geçidi `hello_world.json` hello uygulamayla ilişkili hello iki önceden tanımlanmış modüller belirleyen dosya. Merhaba ağ geçidi "hello world" iletisini tooa dosya her 5 saniyede bir günlüğe kaydeder. Bu bölümde, derleme ve çalıştırma hello `hello_world` kendi varsayılan modülü ile uygulama.

toocompile ve Çalıştır hello `hello_world` uygulama, ana bilgisayarda aşağıdaki adımları izleyin:

1. Merhaba yapılandırma dosyalarını hello aşağıdaki komutları çalıştırarak başlatın:

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Merhaba ağ geçidi yapılandırma dosyasını Intel NUC MAC adresini hello ile güncelleştirin. Merhaba Ders çok uyguladıysanız bu adımı atlayın[yapılandırma ve bırak örnek uygulamayı çalıştırma][config_ble].

   1. Merhaba aşağıdaki komutu çalıştırarak Hello ağ geçidi yapılandırma dosyasını açın:

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. Güncelleştirme hello ağ geçidi MAC adresi, [Intel NUC IOT ağ geçidi olarak ayarlama][setup_nuc]ve hello dosyasını kaydedin.

1. Merhaba aşağıdaki komutu çalıştırarak Hello örnek kaynak kodu derleme:

   ```bash
   gulp compile
   ```

   Merhaba komut hello örnek kaynak kodu tooIntel NUC aktarır ve çalıştırır `build.sh` toocompile onu.

1. Merhaba çalıştırmak `hello_world` hello aşağıdaki komutu çalıştırarak Intel NUC uygulamasını:

   ```bash
   gulp run
   ```

   Merhaba komutu çalıştırır `../Tools/run-hello-world.js` belirtilen `config.json` Intel NUC üzerinde toostart hello örnek uygulama.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Yeni bir modül oluşturun ve Intel NUC üzerinde derleyin

Merhaba adımları, yeni bir modül oluşturmada size yol ve Intel NUC üzerinde derleyin. ileti aldıktan sonra bir zaman damgasına sahip Hello modülü yazdırır. Bu bölümde, ilk özelleştirilmiş ağ geçidi modülü oluşturacaksınız.

Herhangi bir Azure IOT kenar modülü arabirimler aşağıdaki hello uygulamanız gerekir:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

İsteğe bağlı olarak arabirimi aşağıdaki hello uygulayabilirsiniz:

   ```C
   pfModule_Start Module_Start
   ```

Merhaba Aşağıdaki diyagramda bir modülün hello önemli durumu yolları gösterilmektedir. Merhaba kare dikdörtgenler hello modülü durumlar arasında taşındığında tooperform işlemleri uygulamak yöntemleri temsil eder. Merhaba Oval hello modülü olabilir ana durumlarıdır.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Şimdi hello şablonunu temel alan bir modül oluşturalım:

1. Merhaba aşağıdaki komutu çalıştırarak Hello şablonu klasörü açın:

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`bir modülün hello oluşturulması kolaylaştıran bir şablon olarak görev yapar. Merhaba şablon hello arabirimleri bildirir. Tek toodo ihtiyacınız olan tooadd mantığı toohello `MyModule_Receive` işlevi.
   - `build.sh`Merhaba yapı betik toocompile hello Intel NUC üzerinde modülüdür.
1. Açık hello `src/my_module.c` dosya ve iki üst bilgi dosyaları içerir:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Aşağıdaki kodu toohello hello eklemek `MyModule_Receive` işlevi:

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

1. Güncelleştirme hello `config.json` dosya toospecify hello `workspace` , ana bilgisayar ve hello dağıtım yolunuza Intel NUC klasörü. Derleme sırasında hello hello dosyalarında `workspace` klasörü aktarılan toohello dağıtım yolu olacaktır.

   1. Açık hello `config.json` hello aşağıdaki komutu çalıştırarak dosya:

      ```bash
      code config.json
      ```

   1. Güncelleştirme `config.json` yapılandırma aşağıdaki hello ile:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Merhaba modülü hello aşağıdaki komutu çalıştırarak derleyin:

   ```bash
   gulp compile
   ```

   Merhaba komut hello kaynak kodu tooIntel NUC aktarır ve çalıştırır `build.sh` toocompile hello modülü.

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>Merhaba modülü toohello hello_world örnek uygulaması ekleyin ve üzerinde Intel NUC hello uygulamayı çalıştırma

tooperform bu görev, şu adımları izleyin:

1. Tüm hello kullanılabilir modül ikili dosyalarını (.so dosyaları) hello aşağıdaki komutu çalıştırarak üzerinde Intel NUC listesi:

   ```bash
   gulp modules --list
   ```

   Merhaba ikili yolu `my_module` , derlenmiş olarak aşağıda listelenmiş olmalıdır:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Merhaba varsayılan oturum açma kullanıcı değiştirirseniz `config-gateway.json`, hello ikili yolu ile başlayacak `home/<your username>` yerine `root`.

1. Ekleme `my_module` toohello `hello_world` örnek uygulaması:

   1. Açık hello `hello_world.json` hello aşağıdaki komutu çalıştırarak dosya:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Aşağıdaki kodu toohello hello eklemek `modules` bölümü:

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

      Merhaba değerini `module.path` olmalıdır `/root/gateway_sample/module/my_module/build/libmy_module.so`. Merhaba kod bildirir `my_module` belirtilen hello modülü ikili hello konumunu yanı sıra hello ağ geçidi ile ilişkili toobe `module.path`.
   1. Aşağıdaki kodu toohello hello eklemek `links` bölümü:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Bu kod iletiler hello aktarılır belirtir `hello_world` modülü çok`my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Merhaba çalıştırmak `hello_world` hello aşağıdaki komutu çalıştırarak örnek uygulaması:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   Merhaba `--config` parametre zorlar hello `run-hello-world.js` toorun hello kullanarak komut dosyası `hello_world.json` dosya.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

Tebrikler. Bu yeni modül hello davranışını şimdi görebilirsiniz, yalnızca yazdırır "hello world" iletileri bir zaman damgasına sahip, farklı sonuç hello özgün "hello_world" modülünden çıkışı.

## <a name="next-steps"></a>Sonraki Adımlar

Yeni bir modül oluşturulmuş, ağ geçidiniz toohello hello_world örnek ve get hello örnek uygulama toorun hello yeni modülüyle eklemiş. Azure IOT ağ geçidi modüller hakkında daha fazla toolearn istiyorsanız, daha fazla modülü örnekleri aşağıda bulabilirsiniz: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
