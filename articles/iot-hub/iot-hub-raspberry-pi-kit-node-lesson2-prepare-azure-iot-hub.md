---
featureFlags: usabilla
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 2 bağlanın: kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Azure CLI kullanarak hello IOT Hub kimlik kayıt defteri Pi kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "pi bulut Böğürtlenli pi bulut Bağlan"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>IOT hub'ınızı oluşturun ve Raspberry Pi 3 kaydedin
## <a name="what-you-will-do"></a>Ne yapacağını
* Bir kaynak grubu oluşturun.
* Azure IOT hub'ınızı hello kaynak grubunda oluşturun.
* Raspberry Pi 3 toohello Azure IOT hub'hello Azure komut satırı arabirimi (Azure CLI) kullanarak ekleyin.

Azure CLI tooadd PI tooyour IOT hub'ı kullandığınızda, hello hizmeti hello hizmetiyle Pi tooauthenticate için bir anahtar oluşturur. Herhangi bir sorun varsa, hello çözümlerini arama [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl toouse Azure CLI toocreate IOT hub'ı
* Nasıl toocreate IOT hub'ınızdaki pi bir cihaz kimliği

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Azure hesabı
* Mac veya bir Windows bilgisayar hello ile Azure CLI yüklenmiş

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
> IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir. Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.

## <a name="register-pi-in-your-iot-hub"></a>IOT hub'ınıza pi kaydetme
IOT hub'ından ileti alıp tooyour IOT hub'ı iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir Azure CLI tooregister, Pi kullanabilir ve cihaz kimlik doğrulaması için otomatik olarak imzalanan bir X.509 sertifikası oluşturun.

Merhaba aşağıdaki komutu çalıştırın:

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a>Özet
IOT hub'ı oluşturulur ve Pi cihaz kimliğiyle IOT hub'ınıza kayıtlı. Pi tooyour IOT hub'ından toosend nasıl iletileri hazır toolearn demektir.

## <a name="next-steps"></a>Sonraki adımlar
[Bir Azure işlevi uygulama ve bir Azure depolama hesabı tooprocess oluşturun ve IOT hub iletileri depolama](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

