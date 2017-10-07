---
title: "Azure mikro hizmetler için bir geliştirme ortamı kurma aaaSet | Microsoft Docs"
description: "Merhaba çalışma zamanı, SDK ve araçları yükleyip yerel bir geliştirme kümesi oluşturun. Bu kurulumu tamamladıktan sonra hazır toobuild uygulamalar olur."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a>Geliştirme ortamınızı hazırlama
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild çalıştırıp [Azure Service Fabric uygulamaları] [ 1] geliştirme makinenizde hello çalışma zamanı, SDK'yı ve araçları yükleyin. Ayrıca tooenable hello SDK dahil hello Windows PowerShell betiklerinin yürütülmesi gerekir.

## <a name="prerequisites"></a>Ön koşullar
### <a name="supported-operating-system-versions"></a>Desteklenen işletim sistemi sürümleri
işletim sistemi sürümleri aşağıdaki hello geliştirme için desteklenir:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> Windows 7 varsayılan olarak yalnızca Windows PowerShell 2.0 içerir. Service Fabric PowerShell cmdlet’leri PowerShell 3.0 veya üzerini gerektirir. Yapabilecekleriniz [Windows PowerShell 5.0 indirme] [ powershell5-download] hello Microsoft Download Center gelen.
> 
> 

## <a name="install-hello-sdk-and-tools"></a>Merhaba SDK ve araçlarını yükleme
### <a name="toouse-visual-studio-2017"></a>Visual Studio 2017 toouse
Service Fabric araçları hello Azure geliştirme ve yönetim iş yükünü Visual Studio 2017'ın bir parçasıdır. Bu iş yükünü Visual Studio yüklemenizin bir parçası olarak etkinleştirin.
Ayrıca, Microsoft Azure Service Fabric Web Platformu Yükleyicisi'ni kullanarak SDK, tooinstall hello gerekir.

* [Merhaba Microsoft Azure Service Fabric SDK yükleme][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>Visual Studio 2015 toouse (Visual Studio 2015 güncelleştirme 2 veya sonrasını gerektirir)
Visual Studio 2015 için Service Fabric araçları hello hello Web Platformu yükleyicisi kullanılarak SDK ile birlikte yüklenir:

* [Merhaba Microsoft Azure Service Fabric SDK ve araçlarını yükleme][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>Yalnızca SDK'yı yükleme
Merhaba SDK yalnızca gereksiniminiz varsa, bu paketi yükleyebilirsiniz:
* [Merhaba Microsoft Azure Service Fabric SDK yükleme][core-sdk]

Merhaba geçerli sürümleri şunlardır:
* Service Fabric SDK 2.7.198
* Service Fabric çalışma zamanı 5.7.198
* Visual Studio 2015 1.7.50721 için Service Fabric Araçları
* Visual Studio 2017 Güncelleştirme 2, Visual Studio 1.6.20170504 için Service Fabric Araçlarını içerir
* Visual Studio 2017 Güncelleştirme 3 Önizleme 7, (15.3.0 Önizleme 7.0) Visual Studio 1.7.20170721 için Service Fabric Araçlarını içerir

Desteklenen sürümlerin listesi için bkz. [Service Fabric desteği](service-fabric-support.md)

## <a name="enable-powershell-script-execution"></a>PowerShell betik yürütmesini etkinleştirme
Service Fabric, yerel geliştirme merkezi oluşturmak ve Visual Studio'dan uygulamaları dağıtmak için Windows PowerShell betiklerini kullanır. Varsayılan olarak, Windows bu betiklerin çalışmasını engeller. tooenable bunları, PowerShell yürütme ilkenizi değiştirmeniz gerekir. Bir yönetici olarak PowerShell'i açın ve hello aşağıdaki komutu girin:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Sonraki adımlar
Artık geliştirme ortamınızı ayarlamayı tamamladığınıza göre, uygulama derlemeye ve çalıştırmaya başlayın.

* [Visual Studio'da ilk Service Fabric uygulamanızı oluşturma](service-fabric-create-your-first-application-in-visual-studio.md)
* [Bilgi nasıl toodeploy ve yerel kümenizdeki uygulamaları yönetme](service-fabric-get-started-with-a-local-cluster.md)
* [Programlama modelleri hello hakkında bilgi edinin: Reliable Services ve Reliable Actors](service-fabric-choose-framework.md)
* [Service Fabric Hello github'daki kod örnekleri denetleyin](https://aka.ms/servicefabricsamples)
* [Service Fabric Explorer kullanarak kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md)
* [Merhaba Service Fabric yolu tooget geniş kapsamlı bilgi toohello platform öğrenme izleyin](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* [Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric kampanya sayfası"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI bağlantısı"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI bağlantısı"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI bağlantısı"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
