---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 2: kayıt cihazı | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT hub'ı Internet şeyler bulut, azure IOT hub oluşturma aygıt, tı sensortag, tı Boşalt"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Azure IOT hub'ınızı oluşturun ve Cihazınızı kaydedin

## <a name="what-you-will-do"></a>Ne yapacağını

- Kaynak grubu oluşturma
- İlk IOT hub'ınızı oluşturma
- Cihazınızı IOT hub'hello Azure CLI kullanarak kaydedin. 

IOT hub'ınıza Cihazınızı kaydederken hello Azure IOT Hub hizmeti, cihaz toouse tooauthenticate hello hizmetiyle için bir anahtar oluşturur. 

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu alıştırmanın ilerisinde şunları öğreneceksiniz:

- Nasıl toouse hello Azure CLI toocreate IOT hub'ı.
- Nasıl tooregister bir IOT hub'ındaki bir aygıt.

## <a name="what-you-need"></a>Ne gerekiyor

- Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.
- Hello Azure CLI yüklenmiş olması gerekir.

## <a name="create-an-iot-hub"></a>IoT hub oluşturma

toocreate IOT hub'ı, şu adımları izleyin:

1. İçinde tooyour hello aşağıdaki komutu çalıştırarak Azure hesabı imzalayın:

   ```bash
   az login
   ```

   Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.

2. Merhaba varsayılan hello aşağıdaki komutu çalıştırarak toouse istediğiniz Azure aboneliği ayarlayın:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`Merhaba Hello çıktısında bulunabilir `az login` veya hello `az account list` komutu.

3. Merhaba sağlayıcıyı hello aşağıdaki komutu çalıştırarak kaydedin. Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir. Merhaba sağlayıcısı teklifleri hello Azure kaynak dağıtmadan önce hello sağlayıcısı kaydetmeniz gerekir.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Adlı bir kaynak grubu oluşturmak `iot-gateway` hello aşağıdaki komutu çalıştırarak hello Batı ABD bölgesindeki:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`kaynak grubu oluşturma hello bir konumdur. Başka bir konuma toouse istiyorsanız çalıştırabilirsiniz `az account list-locations -o table` toosee tüm hello konumları Azure destekler.

5. Hello IOT hub oluşturma `iot-gateway` hello aşağıdaki komutu çalıştırarak kaynak grubu:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

Varsayılan olarak, hello aracı hello ücretsiz fiyatlandırma katmanında bir IOT hub'ı oluşturur. Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir. Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.

## <a name="register-your-device-in-your-iot-hub"></a>IOT hub'ınıza Cihazınızı kaydedin

IOT hub'ından ileti alıp tooyour IOT hub'ı iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir
Cihazınızı IOT hub'ınıza çalışan aşağıdaki komutla kaydedin:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Özet

IOT hub'ı oluşturulur ve mantıksal Cihazınızı cihaz kimliğiyle IOT hub'ınıza kayıtlı. Tooconfigure ve fiziksel cihaz tooyour IOT hub'ınıza hello çalıştırma bir ağ geçidi örnek uygulama toosend verileri nasıl bulut hazır toolearn demektir.

## <a name="next-steps"></a>Sonraki adımlar
[Yapılandırma ve bırak örnek uygulamayı çalıştırma](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)