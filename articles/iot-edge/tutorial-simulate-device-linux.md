---
title: "Linux Azure IOT kenarına benzetimini | Microsoft Docs"
description: "Linux sanal bir cihaz üzerinde Azure IOT kenar çalışma zamanı yükleme ve ilk modülünüzün dağıtma"
services: iot-edge
keywords: 
author: kgremban
manager: timlt
ms.author: kgremban
ms.reviewer: elioda
ms.date: 01/11/2018
ms.topic: article
ms.service: iot-edge
ms.openlocfilehash: 55770c92f5d5959e83066b425bc6ccf2b9dcc62e
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/12/2018
---
# <a name="deploy-azure-iot-edge-on-a-simulated-device-in-linux-or-macos---preview"></a>Linux veya MacOS sanal bir cihaz üzerinde Azure IOT kenar dağıtma - Önizleme

Azure IOT kenar, tüm verileri buluta itme zorunda kalmak yerine cihazlarınızda analizi ve veri işleme gerçekleştirmenizi sağlar. IOT kenar öğreticileri Azure hizmetlerine veya özel kod yerleşik modülleri, farklı türlerde dağıtmak nasıl gerçekleştirileceğini gösterir ancak önce test etmek için bir aygıt gerekir. 

Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

1. IOT Hub oluşturma
2. Bir IOT sınır cihazı kaydetme
3. IOT kenar çalışma zamanı Başlat
4. Bir modül dağıtma

![Öğretici mimarisi][2]

Bu öğreticide oluşturduğunuz sanal cihaz sıcaklık ve nem Basıncı verileri oluşturan bir izleyicisidir. İşletme öngörüleri için verileri analiz modülleri dağıtarak yapılacağını burada iş bağlı diğer Azure IOT kenar öğreticileri oluşturun. 

## <a name="prerequisites"></a>Önkoşullar

Bu öğretici, bilgisayar veya sanal makine bir nesnelerin interneti aygıtı gibi kullanır. Bir IOT sınır cihazı makinenize etkinleştirmek için aşağıdaki hizmetleri gereklidir:

* Python PIP, IOT kenar çalışma zamanı yüklenemedi.
   * Linux: `sudo apt-get install python-pip`.
   * MacOS: `sudo easy_install pip`.
* IOT kenar modüllerini çalıştırmak için docker
   * [Linux için Docker yükleme] [ lnk-docker-ubuntu] ve çalışır durumda olduğundan emin olun. 
   * [Mac için Docker yükleme] [ lnk-docker-mac] ve çalışır durumda olduğundan emin olun. 

## <a name="create-an-iot-hub"></a>IoT hub oluşturma

Öğretici, IOT Hub'ınızı oluşturarak başlayın.
![IOT Hub oluşturma][3]

[!INCLUDE [iot-hub-create-hub](../../includes/iot-hub-create-hub.md)]

## <a name="register-an-iot-edge-device"></a>Bir IOT sınır cihazı kaydetme

Bir IOT sınır cihazı, yeni oluşturulan IOT Hub ile kaydedin.
![Bir cihaz kaydetme][4]

[!INCLUDE [iot-edge-register-device](../../includes/iot-edge-register-device.md)]

## <a name="install-and-start-the-iot-edge-runtime"></a>Yükleyin ve IOT kenar çalışma zamanı başlatın

Yükleyin ve Azure IOT kenar çalışma zamanı aygıtınızda başlatın. 
![Bir cihaz kaydetme][5]

IOT kenar çalışma zamanı, tüm IOT kenar aygıtlarda dağıtılır. İki modülden oluşur. **IOT kenar Aracısı** dağıtım ve IOT sınır cihazı modülleri izlenmesini kolaylaştırır. **IOT kenar hub** IOT sınır cihazı modülleri arasında ve cihaz IOT hub'ı arasındaki iletişim yönetir. Çalışma zamanı yeni aygıtınızda yapılandırdığınızda, yalnızca IOT kenar aracı ilk başta başlayacaktır. Bir modül dağıttığınızda kenar IOT hub'ı daha sonra gelir. 

IOT sınır cihazı çalıştırdığı makinede IOT kenar denetim komut dosyasını karşıdan yükleyin:
```cmd
sudo pip install -U azure-iot-edge-runtime-ctl
```

Çalışma zamanı IOT kenar cihaz bağlantı dizenizi önceki bölümdeki yapılandırın:
```cmd
sudo iotedgectl setup --connection-string "{device connection string}" --auto-cert-gen-force-no-passwords
```

Çalışma zamanı'nı başlatın:
```cmd
sudo iotedgectl start
```

Docker IOT kenar Aracısı'nı bir modül olarak çalışıp çalışmadığını kontrol edin:
```cmd
sudo docker ps
```

![Docker edgeAgent bakın](./media/tutorial-simulate-device-linux/docker-ps.png)

## <a name="deploy-a-module"></a>Bir modül dağıtma

Azure IOT kenar Cihazınızı IOT Hub'ına telemetri verileri gönderecek bir modül dağıtmak için buluttan yönetin.
![Bir cihaz kaydetme][6]

[!INCLUDE [iot-edge-deploy-module](../../includes/iot-edge-deploy-module.md)]

## <a name="view-generated-data"></a>Oluşturulan görünüm verileri

Bu öğreticide, yeni bir IOT sınır cihazı oluşturulur ve IOT kenar çalışma zamanı yüklü. Ardından, cihaz için değişiklik yapmak zorunda kalmadan cihazda çalıştırmak için bir IOT kenar modülü göndermek için Azure portal kullanılır. Bu durumda, gönderilen modülü öğreticileri için kullanabileceğiniz çevresel veri oluşturur. 

Sanal cihazınız yeniden çalıştıran bilgisayarda komut istemi açın. Buluttan dağıtılan modülü IOT kenar aygıtınızda çalışır durumda olduğunu doğrulayın:

```cmd
sudo docker ps
```

![Cihazınızda üç modüller görünümü](./media/tutorial-simulate-device-linux/docker-ps2.png)

TempSensor modülünden buluta gönderilen iletiler görüntüleyin:

```cmd
sudo docker logs -f tempSensor
```

![Modülünüzün verileri görüntüleme](./media/tutorial-simulate-device-linux/docker-logs.png)

Cihaz kullanarak göndermeyi telemetriyi de görüntüleyebilirsiniz [IOT hub'ı explorer aracı][lnk-iothub-explorer]. 

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, yeni bir IOT sınır cihazı oluşturulur ve Azure IOT kenar bulut arabirimi kodu cihaza dağıtmak için kullanılır. Artık, kendi ortamı hakkında ham verileri oluşturma bir sanal cihaz var. 

Bu öğretici, tüm diğer IOT kenar öğreticileri için önkoşuldur. Azure IOT kenar işletme öngörüleri kenarına bu verileri dönüştürmek nasıl yardımcı olabileceğini öğrenmek için diğer öğreticileri birini açın devam edebilirsiniz.

> [!div class="nextstepaction"]
> [C# kod bir modül olarak geliştirmek ve dağıtmak](tutorial-csharp-module.md)


<!-- Images -->
[1]: ./media/tutorial-install-iot-edge/view-module.png
[2]: ./media/tutorial-install-iot-edge/install-edge-full.png
[3]: ./media/tutorial-install-iot-edge/create-iot-hub.png
[4]: ./media/tutorial-install-iot-edge/register-device.png
[5]: ./media/tutorial-install-iot-edge/start-runtime.png
[6]: ./media/tutorial-install-iot-edge/deploy-module.png

<!-- Links -->
[lnk-docker-ubuntu]: https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/ 
[lnk-docker-mac]: https://docs.docker.com/docker-for-mac/install/
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
