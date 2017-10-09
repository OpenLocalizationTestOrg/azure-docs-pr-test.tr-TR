---
title: "bir Azure Storage hesabı aaaHow toomonitor | Microsoft Docs"
description: "Nasıl toomonitor kullanarak bir depolama hesabı azure'da hello Azure portal hakkında bilgi edinin."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 9a939e0b5db687c1b7b7857399321f681df2056a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>İzleyici bir depolama hesabında hello Azure portalı

[Azure Storage Analytics](../storage-analytics.md) tabloları ve tüm depolama hizmetleri ve günlükleri BLOB, kuyruklar, ölçümleri sağlar. Merhaba kullanabilirsiniz [Azure portal](https://portal.azure.com) tooconfigure hangi ölçümleri ve günlükleri hesabınız için kaydedilen ve ölçümleri verilerinizi görsel gösterimi sağlamak grafikleri yapılandırın.

> [!NOTE]
> Hello Azure portal izleme verileri inceleniyor ile ilişkili maliyetleri vardır. Daha fazla bilgi için bkz: [depolama çözümlemeleri ve faturalama](/rest/api/storageservices/Storage-Analytics-and-Billing).
>
> Azure File storage şu anda Storage Analytics ölçümleri destekliyor, ancak henüz günlük kaydını desteklemiyor.
>
> Bir çoğaltma türü, bölge olarak yedekli depolama (ZRS) şu anda depolama hesaplarıyla hello ölçümleri veya etkin bir günlüğe kaydetme özelliğine sahip değilsiniz.
> 
> Kapsamlı bir kılavuz depolama çözümlemeleri ve diğer araçları tooidentify kullanma hakkında bilgi için tanılama ve Azure Storage ile ilgili sorunları giderme bkz [izleme, tanılama ve Microsoft Azure Storage sorun giderme](../storage-monitoring-diagnosing-troubleshooting.md).
>

## <a name="configure-monitoring-for-a-storage-account"></a>Bir depolama hesabı için izlemeyi Yapılandır

1. Merhaba, [Azure portal](https://portal.azure.com)seçin **depolama hesapları**, sonra da hello depolama hesabı adı tooopen hello hesap Panosu.
1. Seçin **tanılama** hello içinde **izleme** hello menü dikey bölümü.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. Select hello **türü** her ölçümleri verilerin **hizmet** toomonitor istiyor ve hello **Bekletme İlkesi** hello veriler için. Ayrıca ayarlayarak izleme devre dışı bırakabilirsiniz **durum** çok**devre dışı**.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   Her hizmet için etkinleştirebilirsiniz ölçümleri her ikisi de yeni depolama hesapları için varsayılan olarak etkinleştirilen iki tür vardır:

   * **Birleşik**: giriş/çıkış, kullanılabilirlik, gecikme ve başarı yüzdeleri gibi ölçümleri toplar. Bu ölçümler hello blob, kuyruk, tablo ve Dosya Hizmetleri için toplanır.
   * **API başına**: ek toohello toplama ölçümlerini, hello Azure depolama hizmeti API'si her depolama işlem ölçümlerini aynı kümesini toplar hello.

   tooset hello veri bekletme ilkesi, taşıma hello **bekletme (gün)** kaydırıcı veya hello 1 too365 gelen veri tooretain gün sayısını girin. Yeni depolama hesapları için Hello varsayılan yedi gündür. Tooset bir bekletme ilkesi istemiyorsanız sıfır girin. Bekletme İlkesi yok ise, izleme verilerini tooyou toodelete hello olur.

   > [!WARNING]
   > Ölçüm verilerini el ile sildiğinizde ücretlendirilirsiniz. Eski analiz verileri (veri bekletme ilkeniz eski) herhangi bir ücret ödemeden hello sistem tarafından silinir. Tooretain depolama analiz verileri hesabınız için ne kadar süreyle istediğinize bağlı bir bekletme ilkesi ayarı öneririz. Bkz: [ne yapmak tabi storage ölçümleri etkinleştirdiğinizde ücretlendirilen?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) daha fazla bilgi için.
   >

1. Merhaba İzleme yapılandırmasını tamamladığınızda, seçin **kaydetmek**.

Varsayılan bir ölçümleri hello bireysel hizmet Kanatlar (blob, kuyruk, tablo ve dosya) yanı sıra hello depolama hesabı dikey grafiklerinde görüntülenir. Bir hizmet için ölçümleri etkinleştirdikten sonra kendi grafiklerinde veri tooappear tooan saattir yukarı sürebilir. Seçebileceğiniz **Düzenle** üzerinde herhangi bir ölçümü grafik çok[hangi ölçümlerini yapılandırma](#how-to-customize-metrics-charts) hello grafikte görüntülenen.

Ölçümleri toplama ve günlüğe kaydetme ayarlayarak devre dışı bırakabilirsiniz **durum** çok**devre dışı**.

> [!NOTE]
> Azure depolama kullanan [tablo depolama](../common/storage-introduction.md#table-storage) toostore hello ölçümleri depolama hesabı ve hesabınızda tablolardaki depoları hello ölçümleri. Daha fazla bilgi için bkz. [Ölçümleri nasıl depolandığını](../common/storage-analytics.md#how-metrics-are-stored).
>

## <a name="customize-metrics-charts"></a>Ölçümler grafiklerde özelleştirme

Aşağıdaki yordam toochoose hello hangi depolama ölçümleri tooview ölçümleri grafik kullanın. 

1. Hello Azure portalında bir depolama ölçüm grafik görüntüleyerek başlatın. Merhaba grafiklerde bulabilirsiniz **depolama hesabı dikey** ve hello **ölçümleri** dikey bir bireysel hizmet (blob, kuyruk, tablo, dosya).

   Bu örnekte, biz hello üzerinde görünür grafiği aşağıdaki hello çalışmak **depolama hesabı dikey**:

   ![Azure portalında grafiği seçimi](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. Ardından, hello grafik tooopen hello içinde herhangi bir yere tıklayın **ölçüm** dikey. Seçin **grafiği Düzenle** tooopen hello **grafiği Düzenle** dikey.

   ![Grafik düğmesini grafik dikey Düzenle](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. Merhaba üzerinde **grafiği Düzenle** dikey penceresinde, select hello **zaman aralığı** hello ölçümleri toodisplay hello grafik ve Merhaba, **hizmet** (blob, kuyruk, tablo, dosya) istediğinizden, ölçümleri toodisplay. Burada size toodisplay hello Geçen haftaki ölçümleri hello blob hizmeti için seçtiğiniz:

   ![Merhaba grafiği Düzenle dikey penceresinde zaman aralığı ve hizmet seçimi](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. Select hello tek **ölçümleri** gibi hello grafikte görüntülenen, ardından **Tamam**. Örneğin, burada size toodisplay hello seçmiş olduğunuz *ContainerCount* ve *ObjectCount* ölçümleri:

   ![Grafiği Düzenle dikey tek tek ölçüm seçim](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

Grafik ayarlarınızı değil hello koleksiyon, toplama veya izleme verilerinin hello depolama hesabındaki depolama etkiler, yalnızca ölçüm verilerinin görüntülenmesi hello.

### <a name="metrics-availability-in-charts"></a>Ölçümleri kullanılabilirlik grafiklerinde

hangi hizmette hello açılan seçtiğiniz kullanılabilir ölçümler değişiklik Hello listesini temel ve düzenlediğiniz hello grafik hello birim türü. Örneğin, yüzde ölçümleri gibi seçebilirsiniz *PercentNetworkError* ve *PercentThrottlingError* yalnızca birimleri yüzde olarak gösteren bir grafik düzenliyorsanız:

![İstek hata yüzdesi grafik hello Azure portalı](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>Ölçümleri çözümleme

Merhaba ölçümleri tanılamada seçili hesabınız için kullanılabilir olan hello ölçümleri hello çözünürlüğünü belirler:

* **Birleşik** izleme giriş/çıkış, kullanılabilirlik, gecikme ve başarı yüzdeleri gibi ölçümleri sağlar. Bu ölçümler hello blob, tablo, dosya ve kuyruk Hizmetleri toplanır.
* **API başına** yüksekse çözümleme tek depolama işlemleri için kullanılabilir ölçümleri ayrıca toohello hizmet düzeyi toplamalar sağlar.

## <a name="configure-metrics-alerts"></a>Ölçümleri uyarılarını yapılandırma

Uyarıları toonotify oluşturmak için depolama kaynak ölçümleri eşiklerine olduğunda.

1. tooopen hello **uyarı kuralları dikey**, toohello aşağı **izleme** hello bölümünü **menü dikey** seçip **uyarı kuralları**.
1. Seçin **uyarı Ekle** tooopen hello **uyarı kuralı eklemek** dikey penceresi
1. Seçin bir **kaynak** (blob, dosya, kuyruk, tablo) açılan hello ve girin bir **adı** ve **açıklama** , yeni bir uyarı kuralı.
1. Select hello **ölçüm** tooadd bir uyarı bir uyarı için istediğinizi **koşulu**ve bir **eşik**. Merhaba eşik birim türü değişiklikleri hello ölçüm bağlı olarak seçtiğiniz. Örneğin, "count" Merhaba birim için türüdür *ContainerCount*, hello birimi hello için sırasında *PercentNetworkError* ölçümüdür yüzdesi.
1. Select hello **süresi**. Ulaşmak veya aşan ölçümleri eşik hello dönem içinde bir uyarıyı tetikleyecek hello.
1. (İsteğe bağlı) Yapılandırma **e-posta** ve **Web kancası** bildirimleri. Web kancası hakkında daha fazla bilgi için bkz: [bir Web kancası Azure ölçüm uyarıyı yapılandırmak](../../monitoring-and-diagnostics/insights-webhooks-alerts.md). E-posta veya Web kancası bildirimleri yapılandırmazsanız, uyarıları yalnızca hello Azure portalında görünür.

!['Bir uyarı kuralı Ekle' dikey penceresinde hello Azure portalı](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>Ölçümler grafiklerde toohello portal Pano Ekle

Herhangi bir depolama hesapları tooyour portalı panonuza için Azure Storage ölçümleri grafikleri ekleyebilirsiniz.

1. Select tıklatın **düzenleme Pano** hello panonuz görüntülerken [Azure portal](https://portal.azure.com).
1. Merhaba, **döşeme galeri**seçin **Bul bölmeleri tarafından** > **türü**.
1. Seçin **türü** > **depolama hesapları**.
1. İçinde **kaynakları**, ölçümleri tooadd toohello Pano istediğiniz hello depolama hesabını seçin.
1. Seçin **kategorileri** > **izleme**.
1. Sürükle ve bırak hello grafik döşeme panonuz görüntülenmesini istediğiniz hello ölçümü için üzerine. Merhaba panosunda görüntülenen tüm ölçümleri istediğiniz için yineleyin. Merhaba, görüntü aşağıdaki hello "BLOB'lar - toplam istek" grafik örnek olarak vurgulanır, ancak tüm hello grafikler panonuz yerleştirme için kullanılabilir.

   ![Azure portalında döşeme Galerisi](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. Seçin **özelleştirme Bitti** ekleme grafikleri bittiğinde hello panonun hello üstüne yakın.

Grafikler tooyour Pano ekledikten sonra daha fazla bunları açıklandığı gibi özelleştirebilirsiniz [ölçümler grafiklerde özelleştirme](#how-to-customize-metrics-charts).

## <a name="configure-logging"></a>Günlük tutmayı yapılandırma

Azure Storage toosave tanılama günlükleri için okuma, yazma ve silme istekleri hello blob, tablo ve kuyruk Hizmetleri için söyleyebilirsiniz. ayarladığınız hello veri bekletme ilkesi toothese günlükleri de geçerlidir.

> [!NOTE]
> Azure File storage şu anda Storage Analytics ölçümleri destekliyor, ancak henüz günlük kaydını desteklemiyor.
>

1. Merhaba, [Azure portal](https://portal.azure.com)seçin **depolama hesapları**, sonra hello depolama hesabı tooopen hello depolama hesabı dikey penceresinde hello adı.
1. Seçin **tanılama** hello içinde **izleme** hello menü dikey bölümü.

    ![Hello Azure portal'ın tanılama menü öğesi izleme altında.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. Olun **durum** çok ayarlanır**üzerinde**ve select hello **Hizmetleri** tooenable günlüğe kaydetme için istediğiniz.

    ![Hello Azure portalında oturum açmayı Yapılandır.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. **Kaydet** düğmesine tıklayın.

Merhaba tanılama günlükleri, depolama hesabınızdaki $logs adlı blob kapsayıcısında kaydedilir. Hello gibi bir Depolama Gezgini kullanarak hello günlük verilerini görüntüleyebilir [Microsoft Storage Gezgini](http://storageexplorer.com), veya program aracılığıyla hello depolama istemci kitaplığı veya PowerShell kullanarak.

Merhaba $logs kapsayıcı erişme hakkında daha fazla bilgi için bkz: [depolama günlüğünü etkinleştirme ve erişim günlüğü verilerini](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).

## <a name="next-steps"></a>Sonraki adımlar

* İlgili diğer ayrıntıları bulmak [günlüğe kaydetme ve faturalama ölçümleri](../storage-analytics.md) depolama çözümlemeleri için.
* [Azure Storage ölçümleri ve görünüm ölçüm verilerini etkinleştirme](../storage-enable-and-view-metrics.md) PowerShell kullanarak ve C# ile programlı olarak.
