---
title: "Visual Studio bulut Hizmetleri uygulamalarında hata ayıklama için öykünücüsü hızlı kurulumu | Microsoft Docs"
description: "Visual Studio öykünücüsü Express'te etkinleştirmek için C++ yeniden dağıtılabilir yükleme açıklanmaktadır"
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
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a>Bulut Hizmetleri VS 2017 uygulamada hata ayıklamak için emulator Express kullanma
Bu makalede Emulator Express VS 2017 bulut Hizmetleri uygulamalarında hata ayıklama için nasıl kullanılacağı açıklanmaktadır.

## <a name="background-context"></a>Arka plan bağlamı
Öykünücü Express varsayılan olarak, bulut Hizmetleri Web ve çalışan rolleri Visual Studio'da hata ayıklama için kullanılır. Bu ayar, bulut Hizmetleri proje özellikleri sayfasında belirtilir.

![Açık proje özellikleri][0]

![Öykünücü express varsayılan olarak seçilir][1]

[Visual C++ yeniden dağıtılabilir] [ Visual C++ Redistributable] express Visual Studio öykünücüsü tarafından gereklidir. Şu anda Azure yüküyle yüklenmedi. Bulut Hizmetleri uygulamalarında hata ayıklamak için F5 hareketi bu bileşeni yüklemek ve hata ayıklama ile devam etmek için Visual Studio sorar.

![C++ yeniden dağıtılabilir yükleme sor][2]

C++ yeniden dağıtılabilir yüklemek için Evet'i tıklatın.

![C++ yeniden dağıtılabilir yükleme][3]

Hata ayıklama oturumları yeniden başlatmak için F5 tuşuna basın.

![Hata ayıklama başlatılamıyor][4]

![Başarılı hata ayıklama][5]

> Not: Visual C++ yeniden dağıtılabilir bir kez deneme yüklemektir. Azure SDK'ın eski bir sürümden yükseltme olan ve Emulator Express yüklediyseniz, bu sorunla karşılaştığınızda olmaz.
> 
> 

## <a name="manual-workaround"></a>El ile geçici çözüm
Ayrıca yükleyebilirsiniz [Visual C++ yeniden dağıtılabilir] [ Visual C++ Redistributable] el ile ve aynı etkiye nasıl sisteminizde yüklü Visual Studio gibi uygulanır.

[VCRedist_x86.exe][vcredist_x86.exe]

[VCRedist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Sonraki Adımlar
Visual Studio bulut Hizmetleri uygulamalarınızda hata ayıklamak için Azure bilgisayar öykünücüsü kullanma hakkında daha fazla bilgi edinin: [kullanarak çalıştırın ve bir bulut hizmeti yerel makinede hata ayıklamak için Emulator Express][Using Emulator Express to run and debug a cloud service on a local machine]

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
