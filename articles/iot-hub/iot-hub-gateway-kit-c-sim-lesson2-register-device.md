---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 2: kayıt cihazı | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT hub'ı Internet şeyler bulut, azure IOT hub oluşturma aygıt, tı sensortag, tı Boşalt"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5557989453eb47e4c3a287b26603eff040eb1d96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>Azure IOT hub'ınızı oluşturun ve Cihazınızı kaydedin

## <a name="what-you-will-do"></a>Ne yapacağını

- Kaynak grubu oluşturma
- İlk IOT hub'ınızı oluşturma
- Cihazınızı IOT hub'ınıza Azure CLI kullanarak kaydedin. 

IOT hub'ınıza Cihazınızı kaydettiğinizde Azure IOT Hub hizmeti hizmeti ile kimlik doğrulaması için kullanılacak cihazınız için bir anahtar oluşturur. 

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu alıştırmanın ilerisinde şunları öğreneceksiniz:

- IOT hub'ı oluşturmak için Azure CLI kullanma
- Bir IOT hub ' bir cihazı kaydetmek nasıl.

## <a name="what-you-need"></a>Ne gerekiyor

- Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.
- Azure CLI'ın yüklü olması gerekir.

## <a name="create-an-iot-hub"></a>IoT hub oluşturma

IOT hub'ı oluşturmak için aşağıdaki adımları izleyin:

1. Aşağıdaki komutu çalıştırarak Azure hesabınızda oturum açın:

   ```bash
   az login
   ```

   Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.

2. Aşağıdaki komutu çalıştırarak kullanmak istediğiniz Azure aboneliği varsayılan ayarlayın:

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`çıktısında bulunabilir `az login` veya `az account list` komutu.

3. Aşağıdaki komutu çalıştırarak sağlayıcıyı kaydedin. Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir. Sağlayıcısı sunar Azure kaynak dağıtabilmeniz için önce sağlayıcı kaydetmeniz gerekir.

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. Adlı bir kaynak grubu oluşturmak `iot-gateway` aşağıdaki komutu çalıştırarak Batı ABD bölgesindeki:

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`kaynak grubu oluşturma konumdur. Başka bir konuma kullanmak istiyorsanız, çalıştırabilirsiniz `az account list-locations -o table` tüm konumları Azure destekler.

5. Bir IOT hub'ı oluşturmak `iot-gateway` aşağıdaki komutu çalıştırarak kaynak grubu:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

Varsayılan olarak, aracı, IOT hub'ı ücretsiz fiyatlandırma katmanı oluşturur. Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).

> [!NOTE]
> IOT hub'ınızı adı genel olarak benzersiz olması gerekir. Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.

## <a name="register-your-device-in-your-iot-hub"></a>IOT hub'ınıza Cihazınızı kaydedin

IOT hub'ından ileti alıp IOT hub'ına iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir
Cihazınızı IOT hub'ınıza çalışan aşağıdaki komutla kaydedin:

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>Özet

IOT hub'ı oluşturulur ve mantıksal Cihazınızı cihaz kimliğiyle IOT hub'ınıza kayıtlı. Yapılandırma ve verileri bulutta IOT hub'ınızı fiziksel cihazınızdan göndermek için bir ağ geçidi örnek uygulamayı çalıştırma hakkında bilgi edinmek hazırsınız.

## <a name="next-steps"></a>Sonraki adımlar
[Yapılandırma ve bir sanal cihaz bulut karşıya yükleme örnek uygulamayı çalıştırma](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)