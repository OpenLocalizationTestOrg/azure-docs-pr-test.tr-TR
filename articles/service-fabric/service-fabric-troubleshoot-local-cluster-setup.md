---
title: "aaaTroubleshoot, yerel Service Fabric kümesi Kurulumu | Microsoft Docs"
description: "Bu makalede, yerel geliştirme kümeniz sorun giderme önerileri bir dizi kapsar"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Yerel geliştirme Küme kurulumu sorunlarını giderme
Yerel Azure Service Fabric geliştirme kümenizle etkileşim sırasında bir sorun çalıştırırsanız, olası çözümler için öneriler aşağıdaki hello gözden geçirin.

## <a name="cluster-setup-failures"></a>Küme kurulumu hataları
### <a name="cannot-clean-up-service-fabric-logs"></a>Service Fabric günlüklerini temizleyemiyor
#### <a name="problem"></a>Sorun
Merhaba DevClusterSetup komut dosyası çalıştırılırken, bu gibi bir hata görürsünüz:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Çözüm
Geçerli PowerShell penceresinde hello kapatıp yönetici olarak yeni bir PowerShell penceresi açın. Artık hello komut dosyasını çalıştırmak mümkün toosuccessfully olması gerekir.

## <a name="cluster-connection-failures"></a>Küme bağlantı hataları
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Service Fabric PowerShell cmdlet'leri Azure PowerShell'de tanınmıyor.
#### <a name="problem"></a>Sorun
Toorun herhangi birini hello Service Fabric PowerShell cmdlet'leri gibi deneyin, `Connect-ServiceFabricCluster` bir Azure PowerShell penceresinde, o hello cmdlet tanınmıyor belirten başarısız olur. Merhaba Service Fabric cmdlet'leri yalnızca çalışır ancak 64-bit ortamlarda hello neden Azure PowerShell hello 32 bit sürümünde Windows PowerShell (hatta 64-bit işletim sistemi sürümleri), kullanmasıdır.

#### <a name="solution"></a>Çözüm
Her zaman Windows Powershell'den doğrudan Service Fabric cmdlet'lerini çalıştırın.

> [!NOTE]
> Bu artık gerçekleşmesi gereken şekilde hello Azure PowerShell'in en son sürümünü özel bir kısayol oluşturmaz.
> 
> 

### <a name="type-initialization-exception"></a>Tür başlatma özel durumu oluştu
#### <a name="problem"></a>Sorun
PowerShell toohello kümeye bağlanırken hello hata Typeınitializationexception System.Fabric.Common.AppTrace için bkz.

#### <a name="solution"></a>Çözüm
Path değişkeni yükleme sırasında düzgün ayarlanmadı. Windows oturumunu kapatmanız ve yeniden oturum açın. Bu yolunuzu yeniler.

### <a name="cluster-connection-fails-with-object-is-closed"></a>"Nesnesi kapalı" Küme bağlantı başarısız
#### <a name="problem"></a>Sorun
Bir arama tooConnect-ServiceFabricCluster şuna benzer bir hata ile başarısız olur:

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Çözüm
Geçerli PowerShell penceresinde hello kapatıp yönetici olarak yeni bir PowerShell penceresi açın. Şimdi görüntüleyebiliyor olmalısınız toosuccessfully bağlanın.

### <a name="fabric-connection-denied-exception"></a>Doku bağlantı reddedildi özel durumu
#### <a name="problem"></a>Sorun
Visual Studio'da hata ayıklama sırasında bir FabricConnectionDeniedException hatası alırsınız.

#### <a name="solution"></a>Çözüm
Bu hata genellikle, toostart hizmeti ana bilgisayar işlemi el ile Merhaba Service Fabric çalışma zamanı toostart izin vermek yerine çalıştığınızda oluşur, sizin için.

Çözümünüzdeki başlangıç projesi olarak ayarla tüm hizmet projeleri yok emin olun. Yalnızca Service Fabric uygulaması projeleri başlangıç projesi ayarlanmalıdır.

> [!TIP]
> Kurulum aşağıdaki olduğunda yerel kümenizdeki toobehave aşırı başlar, hello yerel Küme Yöneticisi sistemi Tepsisi uygulaması kullanarak sıfırlayabilirsiniz. Bu kaldırır, mevcut küme hello ve yeni bir tane kurun. Tüm dağıtılan uygulamaları ve ilişkili veriler kaldırılır unutmayın.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [Anlama ve sistem durumu raporlarını kümenizle sorun giderme](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md)

