---
title: "Arduino tooAzure IOT - Ders 2 bağlanın: kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Adafruit yumuşatma M0 WiFi hello Azure IOT hub'hello Azure CLI kullanarak kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "bağlanma arduino toocloud, azure IOT hub, Internet şeyler bulut azure IOT hub cihaz, arduino bulut oluşturma"
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
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a>IOT hub'ınızı oluşturun ve Adafruit yumuşatma M0 WiFi Arduino panonuzu kaydedin

## <a name="what-you-will-do"></a>Ne yapacağını
* Bir kaynak grubu oluşturun.
* Azure IOT hub'ınızı hello kaynak grubunda oluşturun.
* Hello Azure komut satırı arabirimi (Azure CLI) kullanarak Arduino Panosu toohello Azure IOT hub'ınızı ekleyin.

Arduino tablosu tooyour IOT hub'ınızı hello Azure CLI tooadd kullandığınızda, hello hizmeti, Arduino Panosu tooauthenticate hello hizmetiyle için bir anahtar oluşturur. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshoot].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl toouse hello Azure CLI toocreate IOT hub'ı.
* Nasıl toocreate bir cihaz kimliği, Arduino için IOT hub'ınıza tahtası.

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Azure hesabı
* Azure CLI yüklü bir bilgisayar hello

## <a name="create-your-iot-hub"></a>IOT hub'ınızı oluşturma
Azure IOT Hub bağlanmak, izlemek ve milyonlarca IOT varlıklarını yönetmenize yardımcı olur. toocreate IOT hub'ınızı şu adımları izleyin:

1. İçinde tooyour hello aşağıdaki komutu çalıştırarak Azure hesabı imzalayın:

   ```bash
   az login
   ```

   Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.

2. Merhaba aşağıdaki komutu çalıştırarak toouse istediğiniz hello varsayılan abonelik ayarlayın:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`Merhaba Hello çıktısında bulunabilir `az login` veya hello `az account list` komutu.

3. Merhaba sağlayıcıyı hello aşağıdaki komutu çalıştırarak kaydedin. Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir. Merhaba sağlayıcısı teklifleri hello Azure kaynak dağıtmadan önce hello sağlayıcısı kaydetmeniz gerekir.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. Adlı bir kaynak grubu hello Batı ABD bölgesinde hello aşağıdaki komutu çalıştırarak IOT örnek oluşturun:

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`kaynak grubu oluşturma hello bir konumdur. Başka bir konuma toouse istiyorsanız çalıştırabilirsiniz `az account list-locations -o table` toosee tüm hello konumları Azure destekler.

5. IOT hub'ı hello aşağıdaki komutu çalıştırarak hello IOT örnek kaynak grubunda oluşturun:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

Varsayılan olarak, hello aracı hello ücretsiz fiyatlandırma katmanında bir IOT hub'ı oluşturur. Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir.
> Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.

## <a name="register-your-arduino-board-in-your-iot-hub"></a>IOT hub'ınıza Arduino panonuzu kaydetme
IOT hub'ından ileti alıp tooyour IOT hub'ı iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir

Arduino panonuzu çalışan aşağıdaki komutu tarafından IOT hub'ınıza kaydedin:

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a>Özet
IOT hub'ı oluşturulur ve Arduino panonuzu cihaz kimliğiyle IOT hub'ınıza kayıtlı. Arduino tablosu tooyour IOT hub'dan nasıl toosend iletileri hazır toolearn demektir.

## <a name="next-steps"></a>Sonraki adımlar
[Bir Azure işlevi uygulama ve Azure Storage hesabı tooprocess ve deposu IOT hub'ı iletileri oluşturmak][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md