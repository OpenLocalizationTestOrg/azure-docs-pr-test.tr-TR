---
title: "Azure IOT - Ders 2 Arduino bağlanın: kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Azure CLI kullanarak Azure IOT hub'ı Adafruit yumuşatma M0 WiFi kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino bağlanma bulut, azure IOT hub, bulut, azure IOT hub'ı şeyler Internet aygıt, arduino bulut oluşturma"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c5ad5e900671c7cedd3cdad2c2aa345315de223b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>IOT hub'ınızı oluşturun ve Adafruit yumuşatma M0 WiFi Arduino panonuzu kaydedin

## <a name="what-you-will-do"></a>Ne yapacağını
* Bir kaynak grubu oluşturun.
* Azure IOT hub'ınızdaki kaynak grubunu oluşturun.
* Arduino panonuzu Azure komut satırı arabirimi (Azure CLI) kullanarak Azure IOT hub'ına ekleyin.

IOT hub'ınıza Arduino panonuzu eklemek için Azure CLI kullandığınızda, hizmet Arduino panonuzu hizmeti ile kimlik doğrulaması için bir anahtar oluşturur. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshoot].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* IOT hub'ı oluşturmak için Azure CLI kullanma
* IOT hub'ınıza Arduino panonuz için bir cihaz kimliği oluşturma

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Azure hesabı
* Azure CLI'ın yüklü olan bir bilgisayar

## <a name="create-your-iot-hub"></a>IOT hub'ınızı oluşturma
Azure IOT Hub bağlanmak, izlemek ve milyonlarca IOT varlıklarını yönetmenize yardımcı olur. IOT hub'ınızı oluşturması için aşağıdaki adımları izleyin:

1. Aşağıdaki komutu çalıştırarak Azure hesabınızda oturum açın:

   ```bash
   az login
   ```

   Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.

2. Aşağıdaki komutu çalıştırarak kullanmak istediğiniz varsayılan abonelik ayarlayın:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`çıktısında bulunabilir `az login` veya `az account list` komutu.

3. Aşağıdaki komutu çalıştırarak sağlayıcıyı kaydedin. Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir. Sağlayıcısı sunar Azure kaynak dağıtabilmeniz için önce sağlayıcı kaydetmeniz gerekir.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Aşağıdaki komutu çalıştırarak IOT-örnekte, Batı ABD bölgesi adlı bir kaynak grubu oluşturun:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`kaynak grubu oluşturma konumdur. Başka bir konuma kullanmak istiyorsanız, çalıştırabilirsiniz `az account list-locations -o table` tüm konumları Azure destekler.

5. IOT hub'ı, aşağıdaki komutu çalıştırarak IOT örnek kaynak grubunda oluşturun:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

Varsayılan olarak, aracı, IOT hub'ı ücretsiz fiyatlandırma katmanı oluşturur. Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> IOT hub'ınızı adı genel olarak benzersiz olması gerekir.
> Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>IOT hub'ınıza Arduino panonuzu kaydetme
IOT hub'ından ileti alıp IOT hub'ına iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir

Arduino panonuzu çalışan aşağıdaki komutu tarafından IOT hub'ınıza kaydedin:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Özet
IOT hub'ı oluşturulur ve Arduino panonuzu cihaz kimliğiyle IOT hub'ınıza kayıtlı. IOT hub'ınıza Arduino panonuzu iletileri gönderme hakkında bilgi edinmek hazırsınız.

## <a name="next-steps"></a>Sonraki adımlar
[Bir Azure işlevi uygulama ve işlemek ve IOT hub iletileri depolamak için bir Azure depolama hesabı oluştur][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md