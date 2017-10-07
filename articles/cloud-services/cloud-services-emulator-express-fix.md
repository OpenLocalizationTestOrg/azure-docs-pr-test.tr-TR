---
title: "aaaSetup öykünücüsü toodebug bulut Hizmetleri uygulamalarında Visual Studio express | Microsoft Docs"
description: "Nasıl tooinstall hello C++ yeniden dağıtılabilir tooenable Visual Studio öykünücüsü Express'te açıklar"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a>VS 2017 toodebug bulut Hizmetleri uygulama emulator Express kullanın
Bu makalede açıklanır nasıl toouse Emulator Express toodebug bulut Hizmetleri uygulamalarında VS 2017.

## <a name="background-context"></a>Arka plan bağlamı
Öykünücü Express varsayılan olarak, bulut Hizmetleri Web ve çalışan rolleri Visual Studio'da hata ayıklama için kullanılır. Bu ayar hello bulut Hizmetleri proje özellikleri sayfasında belirtilir.

![Açık proje özellikleri][0]

![Öykünücü express varsayılan olarak seçilir][1]

Merhaba [Visual C++ yeniden dağıtılabilir] [ Visual C++ Redistributable] express Visual Studio öykünücüsü tarafından gereklidir. Şu anda Azure iş yükü hello ile yüklenmedi. F5'e bir bulut Hizmetleri uygulamaları toodebug hareket, Visual Studio ve bu bileşen tooinstall sor hata ayıklamaya devam edin.

![C++ yeniden dağıtılabilir yükleme sor][2]

Evet tooinstall C++ yeniden dağıtılabilir'i tıklatın.

![C++ yeniden dağıtılabilir yükleme][3]

Yeniden toolaunch hata ayıklama oturumları F5'e basın.

![Hata ayıklama başlatılamıyor][4]

![Başarılı hata ayıklama][5]

> Not: Visual C++ yeniden dağıtılabilir bir kez deneme yüklemektir. Azure SDK'ın eski bir sürümden yükseltme olan ve Emulator Express yüklediyseniz, bu sorunla karşılaştığınızda olmaz.
> 
> 

## <a name="manual-workaround"></a>El ile geçici çözüm
Merhaba de yükleyebilirsiniz [Visual C++ yeniden dağıtılabilir] [ Visual C++ Redistributable] el ile ve aynı etkiye nasıl sisteminizde yüklü Visual Studio gibi uygulanır.

[VCRedist_x86.exe][vcredist_x86.exe]

[VCRedist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Sonraki Adımlar
Visual Studio bulut Hizmetleri uygulamalarınızda Azure bilgisayar öykünücüsü toodebug kullanma hakkında daha fazla bilgi edinin: [Emulator Express kullanarak toorun ve bir bulut hizmeti yerel makinede hata ayıklama][Using Emulator Express toorun and debug a cloud service on a local machine]

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
