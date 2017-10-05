---
title: "Azure IOT - Ders 2 Connect Intel Edison (C): kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Azure CLI kullanarak Azure IOT hub'ı Edison'u kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 52e3e4734dfd2b89f79b0c66683163e69b8e5f25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a>IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin
## <a name="what-you-will-do"></a>Ne yapacağını
* Bir kaynak grubu oluşturun.
* Azure IOT hub'ınızdaki kaynak grubunu oluşturun.
* Intel Edison'u Azure komut satırı arabirimi (Azure CLI) kullanarak Azure IOT hub'ına ekleyin.

IOT hub'ınıza Edison'u eklemek için Azure CLI kullandığınızda, hizmet Edison'u hizmeti ile kimlik doğrulaması için bir anahtar oluşturur. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* IOT hub'ı oluşturmak için Azure CLI kullanma
* IOT hub'ınıza Edison'u için bir cihaz kimliği oluşturma

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Azure hesabı. Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.
* Azure CLI'ın yüklü olması gerekir.

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


## <a name="register-edison-in-your-iot-hub"></a>IOT hub'ınıza Edison'u kaydetme
IOT hub'ından ileti alıp IOT hub'ına iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir

Edison'u IOT hub'ınıza çalışan aşağıdaki komutla kaydedin:

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a>Özet
IOT hub'ı oluşturulur ve Edison'u cihaz kimliğiyle IOT hub'ınıza kayıtlı. IOT hub'ınıza Edison'u iletileri gönderme hakkında bilgi edinmek hazırsınız.

## <a name="next-steps"></a>Sonraki adımlar
[Bir Azure işlevi uygulama ve işlemek ve IOT hub iletileri depolamak için bir Azure depolama hesabı oluştur][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md