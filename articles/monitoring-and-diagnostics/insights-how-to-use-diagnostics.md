---
title: "aaaEnable izleme ve Tanılama, Microsoft Azure | Microsoft Docs"
description: "Bilgi nasıl tooset tanılama Azure kaynaklarınız için ayarlama."
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
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>İzleme ve tanılamayı etkinleştirme
Merhaba, [Azure Portal](https://portal.azure.com), zengin, sık, izleme ve tanılama veri kaynaklarınızı hakkında yapılandırabilirsiniz. Merhaba de kullanabilirsiniz [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) veya [.NET SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure tanılama programlı olarak.

Tanılama, izleme ve ölçüm verilerini azure'da tercih ettiğiniz bir Storage hesabına kaydedilir. Bu toouse sağlar, hangi tooling tooread hello verileri, bir Depolama Gezgini istediğiniz tooPower BI toothird taraf araçları.

## <a name="when-you-create-a-resource"></a>Bir kaynak oluştururken
Çoğu Hizmetleri ilk bunları hello oluşturduğunuzda tooenable tanılama izin [Azure Portal](https://portal.azure.com).

1. Çok Git**yeni** ve ilgilendiğiniz hello kaynağı seçin.
2. Seçin **isteğe bağlı yapılandırma**.
    ![Tanılama dikey penceresi](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Seçin **tanılama**, tıklatıp **üzerinde**. Tanılama toobe kaydedilmesini istediğiniz toochoose hello depolama hesabı gerekir. Tooa depolama hesabına tanılama gönderdiğinizde, depolama ve işlemler için normal veri ücretleri temel alınarak.
4. Tıklatın **Tamam** ve hello kaynağı oluşturun.

## <a name="change-settings-for-an-existing-resource"></a>Mevcut bir kaynağı ayarlarını değiştirme
Bir kaynak oluşturmuş ve toochange hello tanılama ayarları (örneğin, veri toplama toochange hello düzey) istiyorsanız bu sağ taraf hello Azure Portal yapabilirsiniz.

1. Toohello kaynak gidin ve hello tıklayın **ayarları** komutu.
2. Seçin **tanılama**.
3. Merhaba **tanılama** dikey penceresinde tüm hello olası tanılama ve toplama veri kaynağı için izleme sahiptir. Bazı kaynaklar için de seçebilirsiniz bir **bekletme** İlkesi hello veriler için tooclean bunun depolama hesabınızdan.
    ![Depolama tanılama](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Ayarlarınızı seçtikten sonra hello tıklayın **kaydetmek** komutu. İlk kez Merhaba etkinleştiriyorsanız, veri tooshow yukarı izleme sırasında için biraz sürebilir.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Sanal makineler için veri toplama kategorileri
Her zaman hello en güncel bilgileri makinenizi hakkında böylece sanal makineler için tüm ölçümleri ve günlükleri bir dakikalık aralıklarla kaydedilir.

* **Temel ölçümleri** : sistem durumu ölçümleri işlemci ve bellek gibi sanal makinenize hakkında
* **Ağ ve web ölçümleri** : ölçümleri ağ bağlantıları ve web hizmetleri hakkında
* **.NET ölçümleri** : ölçümleri, sanal makine üzerinde çalışan hello .NET ve ASP.NET uygulamaları hakkında
* **SQL ölçümleri** : Microsoft SQL Hizmeti, kendi performans ölçümleri çalıştırıyorsanız
* **Windows olayı uygulama günlükleri** : toohello uygulama kanal gönderilen Windows olayları
* **Windows olayı sistem günlükleri** : toohello sistem kanalı gönderilen Windows olayları. Bu, tüm olayları da içerir [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Windows olayı güvenlik günlükleri** : toohello güvenlik kanalı gönderilen Windows olayları
* **Tanılama altyapı günlükleri** : hello tanılama koleksiyonu altyapı hakkında günlük kaydı
* **IIS günlüklerini** : IIS sunucunuzu hakkında günlükleri

Şu anda Linux belirli dağıtımları desteklenmez ve hello Konuk Aracısı hello sanal makineye yüklenmesi, unutmayın.

## <a name="next-steps"></a>Sonraki adımlar
* İşletimsel olaylar gerçekleştiğinde ya da ölçümler bir eşiği aştığında [uyarı bildirimleri alın](insights-receive-alert-notifications.md).
* [İzleme hizmeti ölçümleri](insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.
* [Örnek sayısı otomatik olarak ölçeklendirme](insights-how-to-scale.md) toomake emin hizmet ölçek tabanlı isteğe bağlı.
* [Uygulama performansı izleme](../application-insights/app-insights-azure-web-apps.md) tam olarak kodunuzu hello bulutta nasıl gerçekleştiriyor toounderstand istiyorsanız.
* [Olayları ve etkinlik günlüğü görüntüle](insights-debugging-with-events.md) toolearn her şeyi içeren hizmetinizi gerçekleştirilmedi.
* [Hizmet durumu izleme](insights-service-health.md) Azure performans düşüşünü ya da hizmet kesintilerine zaman karşılaştı çıkışı toofind.

