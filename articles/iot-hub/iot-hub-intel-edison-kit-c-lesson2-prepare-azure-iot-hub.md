---
title: "Connect Intel Edison (C) tooAzure IOT - Ders 2: kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Edison'u hello Azure IOT hub'hello Azure CLI kullanarak kaydedin."
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
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a>IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin
## <a name="what-you-will-do"></a>Ne yapacağını
* Bir kaynak grubu oluşturun.
* Azure IOT hub'ınızı hello kaynak grubunda oluşturun.
* Intel Edison'u toohello Azure IOT hub'hello Azure komut satırı arabirimi (Azure CLI) kullanarak ekleyin.

Hello Azure CLI tooadd Edison'u tooyour IOT hub'ı kullandığınızda, hello hizmeti hello hizmetiyle Edison'u tooauthenticate için bir anahtar oluşturur. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl toouse hello Azure CLI toocreate IOT hub'ı.
* Nasıl toocreate IOT hub'ınızdaki Edison'u için bir cihaz kimliği.

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Azure hesabı. Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.
* Hello Azure CLI yüklenmiş olması gerekir.

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


## <a name="register-edison-in-your-iot-hub"></a>IOT hub'ınıza Edison'u kaydetme
IOT hub'ından ileti alıp tooyour IOT hub'ı iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir

Edison'u IOT hub'ınıza çalışan aşağıdaki komutla kaydedin:

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a>Özet
IOT hub'ı oluşturulur ve Edison'u cihaz kimliğiyle IOT hub'ınıza kayıtlı. Nasıl toosend Edison'u tooyour IOT hub'ından iletileri hazır toolearn demektir.

## <a name="next-steps"></a>Sonraki adımlar
[Bir Azure işlevi uygulama ve Azure Storage hesabı tooprocess ve deposu IOT hub'ı iletileri oluşturmak][process-and-store-iot-hub-messages].


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md