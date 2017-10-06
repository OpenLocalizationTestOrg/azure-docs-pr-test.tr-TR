---
title: "aaaAzure SDK .NET 2.8 sürüm notları"
description: "2.8 .NET için Azure SDK sürüm notları"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>2.8, 2.8.1 ile ve 2.8.2 .NET için Azure SDK
## <a name="overview"></a>Genel Bakış
.NET 2.8, 2.8.1 ile ve 2.8.2 yayımları için bu makale (, bilinen sorunlar ve önemli değişiklikler içeren) hello sürüm notları hello Azure SDK'sı içerir. 

Yeni özellikler ve bu sürümde yapılan güncelleştirmeler tam listesi için bkz: Merhaba [Visual Studio 2013 ve Visual Studio 2015 için Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) duyuru. 

## <a name="azure-sdk-for-net-28"></a>.NET 2.8 için Azure SDK
### <a name="download-azure-sdk-for-net-28"></a>2.8 .NET için Azure SDK'sını indirin
[Visual Studio 2015 için 2.8 .NET için Azure SDK](http://go.microsoft.com/fwlink/?LinkId=699285) 

[Visual Studio 2013 için 2.8 .NET için Azure SDK](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>.NET 4.5.2 desteği
#### <a name="known-issues"></a>Bilinen sorunlar
Azure .NET SDK 2.8 bulut hizmet paketleri, 4.5.2 toocreate .NET sağlar. Ancak 4.5.2 .NET framework konuk işletim sistemi görüntüleri Ocak 2016 konuk işletim sistemi kadar yayın hello varsayılan olarak yüklenmez. Bu, .NET 4.5.2 önce framework bir ayrı konuk işletim sistemi sürümü – Kasım 2015-02 kullanılabilir olacak. Merhaba bkz [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](../cloud-services/cloud-services-guestos-update-matrix.md) hello görüntü yayımlandığında sayfa tootrack.  Merhaba Kasım 2015-02 görüntü sunulduktan sonra bulut hizmeti yapılandırma dosyasının (.cscfg) dosyanızı güncelleştirerek, görüntü toouse seçebilirsiniz. Hello hizmet yapılandırmasında dosya hello ServiceConfiguration öğesi toohello dize hello osVersion özniteliğini Ayarla "WA-GUEST-OS-4.26_201511-02". Bu görüntü toouse tooopt seçerseniz, Otomatik Güncelleştirmeler toohello konuk işletim sistemi artık alırsınız. tooget hello otomatik güncelleştirmeler hello osVersion çok ayarlanmalıdır "*" ve .NET 4.5.2 yalnızca Ocak 2016 Otomatik Güncelleştirmeler aracılığıyla kullanılabilir olacaktır.

### <a name="azure-data-factory"></a>Azure Data Factory
#### <a name="known-issues"></a>Bilinen sorunlar
Sırasında bir **veri fabrikası şablonu** proje oluşturma ilgili örnek veriler, azure power shell betiği başarısız 0.9.8 sonra azure power shell sürüm hello makinede yüklü olması durumunda olabilir.

Sırada toosuccessfully bu tür bir proje oluşturun, yüklemeniz gereken [azure power shell sürüm 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).

### <a name="azure-resource-manager-tools"></a>Azure Kaynak Yöneticisi Araçları
#### <a name="breaking-changes"></a>Yeni değişiklikler
Merhaba hello Azure kaynak grubu projesi tarafından sağlanan PowerShell Betiği bu yayın toowork hello yeni Azure PowerShell cmdlet'leri sürüm 1.0 ile güncelleştirilmiştir.  Bu yeni betik gelen Visual Studio ile Merhaba SDK önceki too2.8 sürümünü kullanırken çalışmaz.  

Kullanarak hello zaman 2.8 SDK hello SDK önceki sürümlerinde oluşturulan projeleri betiklerinden gelen Visual Studio içinde çalışmaz.  Tüm betikler, Visual Studio dışında toowork hello uygun hello Azure PowerShell cmdlet'lerini sürümü ile devam eder.  

Merhaba 2.8 SDK hello Azure PowerShell cmdlet'lerini 1.0 sürümünü gerektirir.  Diğer tüm hello SDK sürümleri hello Azure PowerShell cmdlet'lerini 0.9.8 sürümünü gerektirir.  Daha fazla bilgi için bkz: [bu](http://go.microsoft.com/fwlink/?LinkID=623011) blogu.

### <a name="web-tools-extensions"></a>Web uzantılarının araçları
#### <a name="known-issues"></a>Bilinen sorunlar
bilinen sorunlar aşağıdaki hello yayın aşağıdaki hello ele alınacaktır.

* Uygulama hizmeti ile ilgili Bulut ve Sunucu Gezgini hareketi (gibi Azure Çin ya da Azure yığın Müşteriler) üretim dışı ortamlar için çalışmaz. Yayımlama Hello indirme müşteriler bu etkilenen alanlarda hello Azure portal profilinden Yayımlama özelliğini etkinleştirin. Gelecek sürümlerinden hareketleri "Hata ayıklayıcı Ekle" ve "Akış günlüklerini görüntüle" gibi Azure Çin ve yığın müşteriler için onarın. 
* Müşteriler, uygulama hizmet Doğu ABD dışındaki bir bölgede hello App Insights dağıtmakta olduğunuz toowhich örneği olduğunda oluşturma olduğundan sırasında hatalar görebilirsiniz. Bu senaryolarda hello Portalı'nda bir uygulama hizmeti oluşturma ve hello indirme yayımlama profili yayımlama senaryoları etkinleştirir. 

### <a name="azure-hdinsight-tools"></a>Azure Hdınsight araçları
#### <a name="new-updates"></a>Yeni güncelleştirmeler
* Hive sorgunuzu neredeyse hiçbir ek yükü ile Merhaba kümede HiveServer2 aracılığıyla yürütme ve gerçek zamanlı hello iş günlükleri bakın.
* Hello kullanarak yeni Hive görev yürütme daha derin, işinizi derinliklerine görünümü, diğer ayrıntıları bulmak ve olası sorunları.

Bilgi için bkz: [Visual Studio 2013 ve Visual Studio 2015 için Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/). 

## <a name="azure-sdk-for-net-281"></a>.NET için Azure SDK 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Visual Studio 2013 ve Visual Studio 2015 için bilinen sorunlar
1. Tetiklenen WebJob yayımlar tooslots Göster ve hata ve kümesi bir zamanlama, ancak hello WebJob tooAzure gönderir olmaz. Zamanlanmış işi gerekli kullanmaya başlayan müşteriler, daha sonra hello Azure Portal tooset hello çizelgesi hello Web işi için kullanabilirsiniz. 
2. Python müşterileri hata ayıklayıcı sorunlarla karşılaşabilirsiniz. Hizmet takım bunun için bir düzeltme sunmak ancak müşteriler etkilenir, lütfen Microsoft hello forumlarında veya hello duyuru blogunda bilmek veya Sürüm Notları Açıklamalar bölümüne sağlar. 
3. Uygulama hataları sağlama hizmeti (örneğin, Güney Hindistan) belirli bölgelerdeki müşterilere karşılaşırsınız. Bu hello portalı ile tutarlı ve bu sorunla karşılaşan müşteriler hello Azure portal toorequest erişim toopublish toothese coğrafi-bölgeleri kullanabilirsiniz. Azure portal sağlama hello kullanarak erişim toothese bölge istediklerinde sonra çalışması gerekir. 

## <a name="azure-sdk-for-net-282"></a>.NET 2.8.2 için Azure SDK
Merhaba 2.8.2 araçları Hello yüklemesinden müşteriler sorunu aşağıdaki hello karşılaşabilirsiniz.         

* Windows 10 kullanıyorsanız ve Internet Explorer yüklü olmayan bir "Internet Explorer bulunamadı" hatası alabilirsiniz.
  tooresolve hello sorun, Internet Explorer hello Ekle kullanarak yükleyin/Windows bileşenleri iletişim Kaldır.

Bu sorunu gözlemlerseniz, hello gönderme bir gülümseme gönderme özelliği tooreport kullanın.

Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) gönderin.

## <a name="other-updates"></a>Diğer güncelleştirmeler
Diğer güncelleştirmeler için bkz: [Azure SDK 2.8 duyuru post](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="also-see"></a>Ayrıca bkz.
[Azure SDK 2.8 duyuru post](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[Destek ve devre dışı bırakma bilgi hello .NET ve API'ler için Azure SDK'sı için](https://msdn.microsoft.com/library/azure/dn479282.aspx)

