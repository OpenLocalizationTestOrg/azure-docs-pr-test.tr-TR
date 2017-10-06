---
title: "aaaAzure SDK .NET 2.9 sürüm notları"
description: ".NET 2.9 için Azure SDK sürüm notları"
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
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>.NET 2.9 için Azure SDK sürüm notları

Bu konu için .NET 2.9 ve Azure SDK'sının 2.9.6 sürümleri için sürüm notları içerir.

##<a name="azure-sdk-for-net-296-release-summary"></a>.NET 2.9.6 için Azure SDK sürüm özeti

Yayın Tarihi: 11/16/2016
 
Hiçbir en son değişiklikleri toohello Azure SDK 2.9 sunulan bu sürümde. Bu SDK mevcut bulut hizmeti projeleri ile de hiçbir gereken yükseltme işlemi tooleverage yoktur.

### <a name="visual-studio-2017-release-candidate"></a>Visual Studio 2017 Sürüm Adayı

- Visual Studio 2017 RC'de bu hello Azure SDK'sı sürüm .NET için Azure iş yükü hello yerleşik olarak bulunur. Toodo Azure geliştirme gereken tüm hello araçları Visual Studio 2017 RC ileriye dönük bir parçası olur. Visual Studio 2015 ve Visual Studio 2013 için hello SDK Webpı kullanılabilir olmaya devam eder. Visual Studio 2017 son bir ürün olarak bıraktığında biz Azure SDK'sı .NET sürümleri için Visual Studio 2013 için sona erdirme. Bu bağlantıyı toodownload Visual Studio 2017 RC izleyin: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Azure Tanılama

- Değiştirilen hello davranışı tooonly bulut Hizmetleri tanılama depolama bağlantı dizesi için bir belirteç değiştirilmiştir hello anahtarla bir kısmi bağlantı dizesi depolar. kendi erişim denetlenebilir şekilde hello gerçek depolama anahtarı artık hello kullanıcı profili klasöründe depolanır. Visual Studio yerel hata ayıklama ve yayımlama işlemi için kullanıcı profili klasöründen hello depolama anahtarı okur. 
- Yanıt toohello değişiklik yukarıda açıklanan Visual Studio Online ekip Gelişmiş hello Azure Cloud Services Dağıtımı görev şablonu kullanıcılar tooAzure içinde sürekli tümleştirme yayımlarken tanılama uzantısını ayarlamak için hello depolama anahtarı belirtebilirsiniz şekilde ve dağıtım.
- Bu olası toostore güvenli bağlantı dizesi ve simgeleştirme için Azure tanılama (WAD), environements arasında yapılandırma sorunlarını çözmek toohelp yaptık.
 
### <a name="windows-server-2016-virtual-machines"></a>Windows Server 2016 sanal makineler

- Visual Studio şimdi dağıtma bulut Hizmetleri tooOS ailesi 5 (Windows Server 2016) sanal makineleri destekler. Mevcut bulut hizmetlerini ayarları tootarget değiştirebilirsiniz yeni işletim sistemi ailesi hello. .Net 4.6 ya da daha yüksek kullanarak toocreate hello hizmet seçerseniz yeni bulut Hizmetleri, oluştururken, varsayılan olarak hello hizmet toouse işletim sistemi ailesi 5 alır.  Daha fazla bilgi için hello gözden geçirebilirsiniz [konuk işletim sistemi ailesi destek tablo](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).

#### <a name="known-issues"></a>Bilinen sorunlar

- Azure .NET SDK 2.9.6 sunulan desteklenmeyen .NET çerçeveleri (örneğin, .NET 4.6) tooany işletim sistemi ailesi kullanarak projeleri dağıtılmasını engelleyen bir kısıtlama < 5. Geçici bir çözüm sağlanmaktadır [burada](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).

 
### <a name="azure-in-role-cache"></a>Azure rol içi önbellek 

- Azure rol içi önbelleği uçları 30 Kasım 2016 desteği. Daha fazla ayrıntı için tıklatın [burada](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Azure yığını için Azure Resource Manager şablonları

- Azure Resource Manager şablonlarınızı dağıtım hedefi olarak biz Azure yığın ekledik.


## <a name="azure-sdk-for-net-29-summary"></a>.NET 2.9 özeti için Azure SDK'sı

## <a name="overview"></a>Genel Bakış
Bu belge .NET 2.9 yayımı için Azure SDK'sı hello hello sürüm notları içeriyor. 

Merhaba bu sürümde güncelleştirmeler hakkında ayrıntılı bilgi için bkz [Azure SDK 2.9 duyuru post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Visual Studio 2015 güncelleştirme 2 ve Visual Studio "15" için Azure SDK 2.9 Önizleme
Bu güncelleştirme, aşağıdaki hata düzeltmeleri hello içerir:

* İlgili tooREST API İstemci oluşturma sorunu içinde hangi hello dizesinde "Bilinmeyen tür" Merhaba hello kod gen klasörün adını ve/veya oluşturulan hello koda bırakılan hello ad hello adı olarak görünür.
* İlgili tooScheduled WebJobs hangi hello toohello Zamanlayıcı sağlama işlemini geçirilen toobe başarısız kimlik doğrulama bilgilerini verin.

Bu güncelleştirme, yeni bir özellik aşağıdaki hello içerir:

* Uygulama hizmeti sağlama iletişim hello hello "Hizmetler" sekmesinde ikincil uygulama hizmetleri için destek. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Visual Studio 2015 güncelleştirme 2 için Azure Data Lake araçları
Bu güncelleştirmeleri hello aşağıdakileri içerir:

* **Azure Data Lake Araçları** için Visual Studio şimdi .NET sürüm için Azure SDK'sı hello içine birleştirilir. Azure SDK'yı yüklediğinizde hello aracı otomatik olarak yüklenir. 
  
    Merhaba aracı sık güncelleştirilen, Git [burada](http://aka.ms/datalaketool) tooget hello güncelleştirmeler.
* **Sunucu Gezgini** şimdi tooview tüm sağlar ve bazı U-SQL meta verileri varlıklar oluşturun. Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blogu.

## <a name="hdinsight-tools"></a>Hdınsight araçları
**Hdınsight Araçları** destekler Hdınsight sürüm 3.3 Tez grafiklerinde ve başka bir dilde gösteren dahil olmak üzere, düzeltmeleri şimdi Visual Studio için.

## <a name="azure-resource-manager"></a>Azure Resource Manager
Bu sürüm ekler [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) için Resource Manager şablonları destekler.

## <a name="see-also"></a>Ayrıca bkz.
[Azure SDK 2.9 duyuru post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

