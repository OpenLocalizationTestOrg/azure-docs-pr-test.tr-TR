---
title: "Intel Edison (C) için Azure IOT - bağlantı sorunlarını giderme | Microsoft Docs"
description: "Sayfa Intel Edison'u C deneyimi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino sorunlarını giderme"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dd6338ad29e0bb858c33e5bb24b8f41d3c22575a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a>Sorun giderme
## <a name="hardware-issues"></a>Donanım sorunları
Intel Edison'u ortak sorunlarını çözme hakkında daha fazla bilgi için bkz: [resmi sorun giderme sayfa](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Node.js paket sorunları
### <a name="no-response-during-gulp-tasks"></a>Gulp görevler sırasında yanıt yok
Ekleyebileceğiniz gulp görevleri çalıştırma sorunlarla varsa, `--verbose` hata ayıklama seçeneği. Geçerli gulp görevleri kullanarak sonlandırmak deneyin `Ctrl + C`, hata ayıklama iletileri aşağıdaki görmek için konsol penceresinde komutunu çalıştırın. Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>NPM sorunları
Aşağıdaki komutla NPM paket güncelleştirmeyi deneyin:

```bash
npm install -g npm
```

Sorun devam ederse, bu makalenin sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo][sample-repository].

## <a name="azure-cli-issues"></a>Azure CLI sorunları
Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır. Çözümde arayın [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) çözümleri arama. Azure CLI komutları beklendiği gibi çalışmıyor olduğunda en son sürümüne yükseltmek deneyin.

Tüm hatalar aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) içinde **sorunları** GitHub depo bölümü.

Sık karşılaşılan sorunları gidermede yardım için denetleme [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).

Lütfen "gereksinimini karşılayan bir sürüm bulunamadı" karşılıyorsa, PIP en son sürümüne yükseltmek için aşağıdaki komutu çalıştırın.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Python yükleme sorunları
### <a name="legacy-installation-issues-macos"></a>Eski yükleme sorunları (macOS)
Ne zaman yüklüyorsanız **PIP**, eski paketleri olduğunda izin hatası atılır ile birlikte yüklenen **su** izinleri. Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur. Bazı **PIP** önceki bir yükleme paketlerinden izni hataya neden olan kök tarafından oluşturulmuş. Kök tarafından yüklenen bu paketleri kaldırmak için çözümüdür. Bu görevi tamamlamak için aşağıdaki adımları kullanın:

1. Gidin: /usr/local/lib/python2.7/site-packages
2. Liste paketleri kök tarafından oluşturun:`ls -l | grep root`
3. Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`
4. Python yeniden yükleyin.

## <a name="azure-iot-hub-issues"></a>Azure IOT hub'ı sorunları
Başarılı bir şekilde Azure IOT hub'ınıza sağladığınız varsa `azure-cli`, ve IOT hub'ınıza bağlanan aygıtları yönetmek için aşağıdaki araçları deneyin bir aracı gerekir:

### <a name="device-explorer"></a>Cihaz Gezgini
[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve Azure IOT hub'ınıza bağlanır. Aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):

- _Cihaz Kimlik Yönetimi_ sağlamak ve IOT hub'ınıza kayıtlı cihazları yönetmek için.
- _Cihaz bulut alma_ cihazınızın IOT hub'ına gönderilen iletileri izleyebilmek.
- _Bulut cihaz Gönder_ IOT hub'ından aygıtlarınıza iletileri gönderebilmesi.

Yapılandırma, `IoT hub connection string` tüm özellikleri kullanmak için bu aracı içinde.

### <a name="iot-hub-explorer"></a>IOT hub'ı Gezgini
[IOT hub'ı Explorer](https://github.com/Azure/iothub-explorer) aygıt istemcileri yönetmek için bir örnek çok platformlu CLI aracıdır. Cihaz kimlik kayıt defterinde yönetmek, cihaz bulut iletilerini izlemek ve bulut-cihaz komutlarını göndermek için aracını kullanabilirsiniz.

Iothub explorer Aracı (ön) en son sürümünü yüklemek için komut satırı ortamınızda aşağıdaki komutu çalıştırın:

```bash
npm install -g iothub-explorer@latest
```

Tüm ıothub explorer komutları ve bunların parametreleri hakkında ek Yardım almak için aşağıdaki komutu kullanın:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure portalına
Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur. Kullanmak isteyebilirsiniz [Azure portal](../azure-portal-overview.md) sağlama Yardım, yönetmek ve Azure kaynaklarınızı hata ayıklamak için.

## <a name="azure-storage-issues"></a>Azure depolama sorunları
[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) çalışmak için kullanabileceğiniz bir Microsoft tek başına uygulamadır [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) Windows, macOS ve Linux veri. Bu aracı kullanarak tablonuza bağlanabilir ve içindeki verilerin bakın. Azure Storage sorunlarını gidermek için bu aracı kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bu sayfa yalnızca en sık karşılaşılan Intel Edison'u Seti içerir. Daha fazla sorun giderme için sorunları bildirmek için alt açıklamaları da bırakabilirsiniz.

Geri dönerek [Intel Edison (C) ile çalışmaya başlama](iot-hub-intel-edison-kit-c-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started