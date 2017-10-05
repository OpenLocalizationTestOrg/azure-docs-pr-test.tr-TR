---
title: "İzleme ve Tanılama, Microsoft Azure | Microsoft Docs"
description: "Azure kaynaklarınız için tanılama ayarlanacağını öğrenin."
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: b82bb1ab419831e803689edb2a2a7fe256dde5a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>İzleme ve tanılamayı etkinleştirme
İçinde [Azure Portal](https://portal.azure.com), zengin, sık, izleme ve tanılama veri kaynaklarınızı hakkında yapılandırabilirsiniz. Aynı zamanda [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) veya [.NET SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tanılama programlı olarak yapılandırmak için.

Tanılama, izleme ve ölçüm verilerini azure'da tercih ettiğiniz bir Storage hesabına kaydedilir. Bu, bir depolama Gezgini'nde, veri, istediğiniz herhangi bir araç Power BI için üçüncü taraf araçları okuma kullanmanıza olanak sağlar.

## <a name="when-you-create-a-resource"></a>Bir kaynak oluştururken
Çoğu Hizmetleri ilk bunları oluşturduğunuzda tanılamayı etkinleştirin izin [Azure Portal](https://portal.azure.com).

1. Git **yeni** ve ilgilendiğiniz kaynağı seçin.
2. Seçin **isteğe bağlı yapılandırma**.
    ![Tanılama dikey penceresi](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Seçin **tanılama**, tıklatıp **üzerinde**. Tanılama kaydedilmesini istediğiniz depolama hesabını seçin gerekecektir. Bir depolama hesabına tanılama gönderdiğinizde, depolama ve işlemler için normal veri ücretleri temel alınarak.
4. Tıklatın **Tamam** ve kaynağı oluşturun.

## <a name="change-settings-for-an-existing-resource"></a>Mevcut bir kaynağı ayarlarını değiştirme
Bir kaynak oluşturmuş ve (veri toplama düzeyi örneğin değiştirmek için) tanılama ayarlarını değiştirmek istiyorsanız, doğrudan Azure portalında yapabilirsiniz.

1. ' A tıklayın ve kaynak Git **ayarları** komutu.
2. Seçin **tanılama**.
3. **Tanılama** dikey penceresinde tüm olası tanılama ve izleme koleksiyonu veri kaynağı için vardır. Bazı kaynaklar için de seçebileceğiniz bir **bekletme** verilerin depolama hesabınızdan temizlemek için ilke.
    ![Depolama tanılama](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Ayarlarınızı seçtikten sonra tıklayın **kaydetmek** komutu. İzleme sırasında bu ilk kez etkinleştireceğiniz varsa gösterilmeye verileri için biraz sürebilir.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Sanal makineler için veri toplama kategorileri
Makinenizin hakkında her zaman en güncel bilgileri yaşayabilirsiniz sanal makineler için tüm ölçümleri ve günlükleri bir dakikalık aralıklarla kaydedilir.

* **Temel ölçümleri** : sistem durumu ölçümleri işlemci ve bellek gibi sanal makinenize hakkında
* **Ağ ve web ölçümleri** : ölçümleri ağ bağlantıları ve web hizmetleri hakkında
* **.NET ölçümleri** : ölçümleri, sanal makine üzerinde çalışan .NET ve ASP.NET uygulamaları hakkında
* **SQL ölçümleri** : Microsoft SQL Hizmeti, kendi performans ölçümleri çalıştırıyorsanız
* **Windows olayı uygulama günlükleri** : uygulama kanala gönderilir Windows olayları
* **Windows olayı sistem günlükleri** : Sistem kanala gönderilir Windows olayları. Bu, tüm olayları da içerir [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Windows olayı güvenlik günlükleri** : güvenlik kanala gönderilir Windows olayları
* **Tanılama altyapı günlükleri** : hakkında tanılama koleksiyonu altyapı günlüğe kaydetme
* **IIS günlüklerini** : IIS sunucunuzu hakkında günlükleri

Şu anda Linux belirli dağıtımları desteklenmez ve Konuk Aracısı sanal makineye yüklenmesi gerekir, unutmayın.

## <a name="next-steps"></a>Sonraki adımlar
* İşletimsel olaylar gerçekleştiğinde ya da ölçümler bir eşiği aştığında [uyarı bildirimleri alın](insights-receive-alert-notifications.md).
* [İzleme hizmeti ölçümleri](insights-how-to-customize-monitoring.md) hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin olmak için.
* [Örnek sayısı otomatik olarak ölçeklendirme](insights-how-to-scale.md) hizmet ölçek talebe dayalı emin olmak için.
* [Uygulama performansı izleme](../application-insights/app-insights-azure-web-apps.md) tam olarak kodunuzu bulutta nasıl gerçekleştiriyor anlamak istiyorsanız.
* [Olayları ve etkinlik günlüğü görüntüle](insights-debugging-with-events.md) hizmetinizi gerçekleştirilmedi her şeyi öğrenin.
* [Hizmet durumu izleme](insights-service-health.md) Azure performans düşüşünü ya da hizmet kesintilerine yaşandığında öğrenin.

