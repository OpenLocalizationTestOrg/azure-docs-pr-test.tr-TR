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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Ders 5: İlk Azure IOT ağ geçidi modülünüzün oluşturma
Azure IOT kenar, Java, .NET veya Node.js ile yazılmış modüller oluşturmanıza olanak sağlar, ancak bu öğreticide, bir modül C'deki oluşturmak için adım adım anlatılmaktadır

## <a name="what-you-will-do"></a>Ne yapacağını

- Derleme ve Intel NUC üzerinde hello_world örnek uygulamayı çalıştırın.
- Bir modül oluşturun ve Intel NUC üzerinde derleyin.
- Yeni modül hello_world örnek uygulamaya ekleyin ve ardından örnek Intel NUC üzerinde çalıştırın. Bir zaman damgasına sahip "hello_world" ileti yeni modül yazdırır.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

- Nasıl derlemek ve Intel NUC üzerinde bir örnek uygulamayı çalıştırın.
- Bir modül oluşturma
- Modül bir örnek uygulama ekleme.

## <a name="what-you-need"></a>Ne gerekiyor

Ana bilgisayarınızda yüklü Azure IOT kenar.

## <a name="folder-structure"></a>Klasör yapısı

Ders 1 klonlanmış örnek kod Ders 5 alt klasöründe, var olan bir `module` klasör ve `sample` klasör.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- `module/my_module` Klasörü kaynak kodu ve modülü oluşturmak için komut dosyası içerir.
- `sample` Klasörü kaynak kodu ve örnek uygulamanızı oluşturmak için komut dosyası içerir.

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a>Derleme ve Intel NUC üzerinde hello_world örnek uygulamayı çalıştırma

`hello_world` Bir örnek oluşturur dayalı bir ağ geçidi `hello_world.json` uygulamayla ilişkili iki önceden tanımlanmış modüller belirleyen dosya. Ağ Geçidi "hello world" iletisini her 5 saniyede bir dosyaya kaydeder. Bu bölümde, derleme ve çalıştırma `hello_world` kendi varsayılan modülü ile uygulama.

Derlemek ve çalıştırmak için `hello_world` uygulama, ana bilgisayarda aşağıdaki adımları izleyin:

1. Aşağıdaki komutları çalıştırarak yapılandırma dosyalarını başlatın:

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Ağ geçidi yapılandırma dosyasını Intel NUC MAC adresiyle güncelleştirin. Ders aracılığıyla uyguladıysanız bu adımı atlayın [yapılandırma ve bırak örnek uygulamayı çalıştırma][config_ble].

   1. Ağ geçidi yapılandırma dosyası, aşağıdaki komutu çalıştırarak açın:

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. Ağ Geçidi'nin MAC adresi güncelleştirme, [Intel NUC IOT ağ geçidi olarak ayarlama][setup_nuc]ve ardından dosyayı kaydedin.

1. Aşağıdaki komutu çalıştırarak örnek kaynak kodu derleme:

   ```bash
   gulp compile
   ```

   Komut için Intel NUC örnek kaynak kodu aktarır ve çalıştırır `build.sh` onu derlemek için.

1. Çalıştırma `hello_world` aşağıdaki komutu çalıştırarak Intel NUC uygulamasını:

   ```bash
   gulp run
   ```

   Komutu çalıştırır `../Tools/run-hello-world.js` belirtilen `config.json` üzerinde Intel NUC örnek uygulamayı başlatmak için.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Yeni bir modül oluşturun ve Intel NUC üzerinde derleyin

Aşağıdaki adımlar, yeni bir modül oluşturmada size yol ve Intel NUC üzerinde derleyin. İleti aldıktan sonra bir zaman damgasına sahip modülü yazdırır. Bu bölümde, ilk özelleştirilmiş ağ geçidi modülü oluşturacaksınız.

Herhangi bir Azure IOT kenar Modülü aşağıdaki arabirimleri uygulamanız gerekir:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

İsteğe bağlı olarak aşağıdaki arabirimi uygulayabilirsiniz:

   ```C
   pfModule_Start Module_Start
   ```

Aşağıdaki diyagramda bir modül önemli durumu yollarını gösterir. Kare dikdörtgenler modülü durumlar arasında taşındığında işlemlerini gerçekleştirmek için uygulama yöntemleri temsil eder. Oval modülü olabilir ana durumlarıdır.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Şimdi şablona dayalı bir modül oluşturalım:

1. Aşağıdaki komutu çalıştırarak şablonu klasörü açın:

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`bir modül oluşturmayı kolaylaştıran bir şablon olarak görev yapar. Şablon arabirimler bildirir. Yapmanız gereken tek şey mantığı eklemek için `MyModule_Receive` işlevi.
   - `build.sh`Intel NUC modülünü derlemek için derleme komut dosyasıdır.
1. Açık `src/my_module.c` dosya ve iki üst bilgi dosyaları içerir:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Aşağıdaki kodu ekleyin `MyModule_Receive` işlevi:

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

1. Güncelleştirme `config.json` belirtmek için dosya `workspace` ana bilgisayarınız ve Intel NUC dağıtım yolda klasör. Derleme, dosyaları sırasında `workspace` klasörü dağıtım yoluna aktarılan.

   1. Açık `config.json` aşağıdaki komutu çalıştırarak dosya:

      ```bash
      code config.json
      ```

   1. Güncelleştirme `config.json` aşağıdaki yapılandırmaya sahip:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Modül, aşağıdaki komutu çalıştırarak derleyin:

   ```bash
   gulp compile
   ```

   Komut kaynak kodunu Intel NUC aktarır ve çalıştırır `build.sh` modülü derlemek için.

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a>Modül hello_world örnek uygulamaya ekleyin ve üzerinde Intel NUC uygulama çalıştırma

Bu görevi gerçekleştirmek için şu adımları izleyin:

1. Aşağıdaki komutu çalıştırarak tüm kullanılabilir modül ikili dosyalarını (.so dosyaları) Intel NUC listesi:

   ```bash
   gulp modules --list
   ```

   İkili yolunu `my_module` , derlenmiş olarak aşağıda listelenmiş olmalıdır:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Varsayılan oturum açma kullanıcı değiştirirseniz `config-gateway.json`, ikili yolu ile başlar `home/<your username>` yerine `root`.

1. Ekleme `my_module` için `hello_world` örnek uygulaması:

   1. Açık `hello_world.json` aşağıdaki komutu çalıştırarak dosya:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Aşağıdaki kodu ekleyin `modules` bölümü:

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

      Değeri `module.path` olmalıdır `/root/gateway_sample/module/my_module/build/libmy_module.so`. Kod bildirir `my_module` Belirtilen modül ikili konumunu yanı sıra ağ geçidi ile ilişkilendirilecek `module.path`.
   1. Aşağıdaki kodu ekleyin `links` bölümü:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Bu kod iletileri aktarıldığı belirtir `hello_world` modülüne `my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Çalıştırma `hello_world` aşağıdaki komutu çalıştırarak örnek uygulaması:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   `--config` Parametresi zorlar `run-hello-world.js` kullanarak çalıştırmak için betik `hello_world.json` dosya.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

Tebrikler. Bu yeni modül davranışını şimdi görebilirsiniz, yalnızca yazdırır "hello world" iletileri bir zaman damgasına sahip, farklı sonuç özgün "hello_world" modülünden çıkışı.

## <a name="next-steps"></a>Sonraki Adımlar

Yeni bir modül oluşturulmuş, hello_world örnek ve get ile yeni modül ağ geçidiniz üzerinde çalıştırmak için örnek uygulama eklenen. Azure IOT ağ geçidi modüller hakkında daha fazla bilgi edinmek istiyorsanız, daha fazla modülü örnekleri aşağıda bulabilirsiniz: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
