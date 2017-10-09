---
title: "aaaAzure SDK .NET 3.0 sürüm notları | Microsoft Docs"
description: ".NET 3.0 için Azure SDK sürüm notları"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>.NET 3.0 için Azure SDK sürüm notları

Bu konu, .NET için Sürüm Notları'hello Azure SDK'ın 3.0 sürümü için içerir.

##<a name="azure-sdk-for-net-30-release-summary"></a>.NET 3.0 sürüm özeti için Azure SDK'sı

Yayın Tarihi: 07/03/2017
 
Hiçbir en son değişiklikleri toohello Azure SDK 3.0 sunulan bu sürümde. Bu SDK mevcut bulut hizmeti projeleri ile de hiçbir gereken yükseltme işlemi tooleverage yoktur. bir yükseltme işlemi, Azure SDK 3.0 gerektirmeden Azure SDK 3.0 hello tooallow kullanımını yükler toohello Azure SDK 2.9 aynı dizine. Çoğu hello bileşenleri hello ana sürüm 2.9 değiştirilmemesi ancak bunun yerine yalnızca hello yapı numarası güncelleştirildi.

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- Visual Studio 2017 ' bu sürümü hello Azure SDK'sı, .NET için toohello Azure iş yükü yerleşik olarak bulunur. Toodo Azure geliştirme gereken tüm hello araçları Visual Studio ileride 2017 bir parçası olur. Visual Studio 2015 için hello SDK Webpı kullanılabilir olmaya devam eder. Visual Studio 2017 yayımlanan göre Biz Visual Studio 2013 için .NET sürümleri için Azure SDK'sı sonlandırdıktan.

### <a name="azure-diagnostics"></a>Azure Tanılama

- Değiştirilen hello davranışı tooonly bulut Hizmetleri tanılama depolama bağlantı dizesi için bir belirteç değiştirilmiştir hello anahtarla bir kısmi bağlantı dizesi depolar. kendi erişim denetlenebilir şekilde hello gerçek depolama anahtarı artık hello kullanıcı profili klasöründe depolanır. Visual Studio yerel hata ayıklama ve yayımlama işlemi için kullanıcı profili klasöründen hello depolama anahtarı okur. 
- Yanıt toohello değişiklik yukarıda açıklanan Visual Studio Online ekip Gelişmiş hello Azure Cloud Services Dağıtımı görev şablonu kullanıcılar tooAzure içinde sürekli tümleştirme yayımlarken tanılama uzantısını ayarlamak için hello depolama anahtarı belirtebilirsiniz şekilde ve dağıtım.
- Bu olası toostore güvenli bağlantı dizesi ve simgeleştirme için Azure tanılama (WAD), environements arasında yapılandırma sorunlarını çözmek toohelp yaptık.
 
### <a name="windows-server-2016-virtual-machines"></a>Windows Server 2016 sanal makineler

- Visual Studio şimdi dağıtma bulut Hizmetleri tooOS ailesi 5 (Windows Server 2016) sanal makineleri destekler. Mevcut bulut hizmetlerini ayarları tootarget değiştirebilirsiniz yeni işletim sistemi ailesi hello. .Net 4.6 ya da daha yüksek kullanarak toocreate hello hizmet seçerseniz yeni bulut Hizmetleri, oluştururken, varsayılan olarak hello hizmet toouse işletim sistemi ailesi 5 alır.  Daha fazla bilgi için hello gözden geçirebilirsiniz [konuk işletim sistemi ailesi destek tablo](../cloud-services/cloud-services-guestos-update-matrix.md).

### <a name="known-issues"></a>Bilinen sorunlar

- Azure .NET SDK 3.0 bir sorun, Visual Studio 2017 Visual Studio 2015 ile yan yana yapılandırmasında kaldırırken kullanıma sunuldu.  Hello Azure SDK'sı için Visual Studio 2015 yüklü varsa, Microsoft Azure Storage öykünücüsü hello ve Microsoft Azure işlem öykünücüsü, Visual Studio 2017'i kaldırırsanız kaldırılacak.  Bu oluşturma ve Visual Studio 2015 yeni bulut Hizmetleri projelerinde hata ayıklama sırasında bir hata oluşturur. İçinde bu sorunu toofix sipariş, hello Web Platformu Yükleyicisi'nden hello Azure SDK'sını yeniden yükleyin.  Merhaba sorun çözümlenir gelecekteki bir Visual Studio 2017 güncelleştirme.  .

 
### <a name="azure-in-role-cache"></a>Azure rol içi önbellek 

- Azure rol içi önbelleği için destek, 30 Kasım 2016 tarihinde sona erdi. Daha fazla ayrıntı için tıklatın [burada](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).




