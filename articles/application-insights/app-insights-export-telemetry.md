---
title: Application Insights telemetrisini aaaContinuous verilmesini | Microsoft Docs
description: "Microsoft Azure tanılama ve kullanım verileri toostorage dışarı aktarın ve buradan indirin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a>Application Insights telemetrisini dışarı aktarma
Tookeep telemetrinizi hello standart tutma süresinden daha uzun süre istiyorsunuz? Veya özelleştirilmiş bir şekilde işlemek? Sürekli verme bunun için idealdir. Merhaba Application Insights portalında görmek hello olayları Microsoft Azure'un dışarı aktarılan toostorage JSON biçiminde olabilir. Buradan, verilerinizi indirin ve size kod yazma tooprocess gerekir.  

Sürekli verme özelliğini kullanarak ek bir ücret maruz kalabilirsiniz. Denetleyin, [fiyatlandırma modeli](http://azure.microsoft.com/pricing/details/application-insights/).

Sürekli verme ayarlamadan önce tooconsider isteyebilirsiniz bazı alternatifleri vardır:

* Merhaba dışa aktarma düğmesi ölçümleri veya Ara dikey penceresinde hello üstündeki tablolar ve grafikler tooan Excel elektronik tablosu aktarmanıza olanak tanır.

* [Analytics](app-insights-analytics.md) telemetri için güçlü sorgu dili sağlar. Ayrıca sonuçlarını dışarı aktarabilirsiniz.
* Çok arıyorsanız[Power BI verilerinizi keşfedin](app-insights-export-power-bi.md), bunu sürekli verme kullanmadan yapabilirsiniz.
* Merhaba [veri erişim REST API](https://dev.applicationinsights.io/) siz telemetrinize programlı erişim sağlar.

Sürekli verme (burada, kalarak için istediğiniz sürece), veri toostorage kopyaladıktan sonra hello normal Application Insights'ta hala kullanılabilir olduğundan [saklama dönemi](app-insights-data-retention-privacy.md).

## <a name="setup"></a>Sürekli bir dışarı aktarma oluşturma
1. Merhaba, uygulamanız için Application Insights kaynağı, sürekli verme açın ve seçin **Ekle**:

    ![Aşağı kaydırın ve sürekli ver](./media/app-insights-export-telemetry/01-export.png)

2. Veri türleri Hello telemetri seçin tooexport istiyor.

3. Oluşturma veya seçme bir [Azure depolama hesabı](../storage/common/storage-introduction.md) toostore hello veri istediğiniz.

    > [!Warning]
    > Varsayılan olarak, toohello hello depolama konumu ayarlanacak Application Insights kaynağınıza aynı coğrafi bölgede. Farklı bir bölgede depolarsanız, aktarım ödemelere maruz kalabilirsiniz.

    ![Dışarı aktarmak, hedef depolama hesabı Ekle'yi ve ardından yeni bir depolama alanı oluşturmak veya mevcut deposunu seçin](./media/app-insights-export-telemetry/02-add.png)

4. Oluşturma veya hello depolama alanında bir kapsayıcı seçin:

    ![Seç olay türleri](./media/app-insights-export-telemetry/create-container.png)

Dışa aktarma oluşturduktan sonra olmaya başlar. Yalnızca hello verme oluşturduktan sonra ulaşan Veri Al

Yaklaşık bir saat hello depolama birimindeki verileri görüntülenmeden önce bir gecikme olabilir.

### <a name="tooedit-continuous-export"></a>tooedit sürekli dışarı aktarma

Toochange hello olay türleri istiyorsanız, daha sonra yalnızca hello verme düzenleyin:

![Seç olay türleri](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a>toostop sürekli dışarı aktarma

toostop hello verme tıklatın devre dışı bırakın. Etkinleştirme yeniden tıklattığınızda hello verme yeni verilerle yeniden başlatılır. Dışarı aktarma devre dışıyken hello Portalı'nda gelen hello verileri alamazsınız.

toostop hello verme kalıcı olarak silin. Bunun yapılması, veri depolama biriminden silmez.

### <a name="cant-add-or-change-an-export"></a>Ekleyemez veya verme değiştirmek mi?
* tooadd ya da değişiklik dışarı sahibi, katkıda bulunan veya uygulama Öngörüler katkıda erişim hakları gerekir. [Rolleri hakkında bilgi edinin][roles].

## <a name="analyze"></a>Hangi olayların alıyorum?
Biz hesaplamak konum verileri hello istemci IP adresinden eklediğimiz hello dışarı aktarılan verileri uygulamanızdan aldığımız hello ham telemetri olmasıdır.

Tarafından atılan veri [örnekleme](app-insights-sampling.md) dışarı hello veri bulunmaz.

Hesaplanan diğer ölçümleri dahil edilmez. Örneğin, ortalama CPU kullanımı verme yok ancak hello ortalama hesaplanan hello ham telemetri verme.

Merhaba verileri de herhangi hello sonuçlarını içerir [kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md) ayarlamış olduğunuz.

> [!NOTE]
> **Örnekleme.** Uygulamanız çok miktarda veri gönderiyorsa, hello örnekleme özelliği çalışır ve yalnızca bir kesir oluşturulan hello telemetri gönderin. [Örnekleme hakkında daha fazla bilgi edinin.](app-insights-sampling.md)
>
>

## <a name="get"></a>Merhaba veri inceleyin.
Merhaba depolama hello portalında doğrudan inceleyebilirsiniz. Tıklatın **Gözat**, depolama hesabınızı seçin ve ardından açın **kapsayıcıları**.

Visual Studio'da Azure depolama tooinspect açmak **Görünüm**, **Cloud Explorer**. (Bu menü komutu yoksa tooinstall hello Azure SDK'sı gerekir: açık hello **yeni proje** iletişim kutusunda, Visual C# ' ı genişletin / Bulut ve **.NET için Microsoft Azure SDK almak**.)

Blob deposu açtığınızda, blob dosya kümesini içeren bir kapsayıcı göreceksiniz. Merhaba, Application Insights kaynağı adı, izleme anahtarı, telemetri-türü/tarih/saat türetilen her dosyanın URI. (Merhaba kaynak adının tamamen küçük harflerden ve tire hello izleme anahtarı atlar.)

![Uygun bir araçla Hello blob deposu inceleyin.](./media/app-insights-export-telemetry/04-data.png)

Başlangıç tarihi ve saati UTC ve hello telemetri hello deposunda borç - değil hello zaman oluşturulduğu zaman. Kod toodownload hello verileri yazarsanız, bu nedenle onu doğrusal olarak hello verilerine taşıyabilirsiniz.

Merhaba biçiminde hello yolu şöyledir:

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

Burada

* `blobCreationTimeUtc`depolama alanı hazırlama blob hello iç oluşturulduğu süresi
* `blobDeliveryTimeUtc`blob kopyalanan toohello verme hedef depolama olduğunda başlangıç zamanı

## <a name="format"></a>Veri biçimi
* Her bir blob birden çok içeren bir metin dosyasıdır ' \n'-separated satır. Bir süre kabaca yarım bir dakika boyunca işlenen hello telemetri içerir.
* Her satır bir istek veya sayfa görünümü gibi bir telemetri veri noktasını temsil eder.
* Her satır bir biçimlendirilmemiş bir JSON dosyasıdır. Toosit isterseniz ve yerinde stare, Visual Studio'da açın ve seçin, Gelişmiş biçim dosyasını düzenleyin:

![Görünüm hello telemetri uygun aracıyla](./media/app-insights-export-telemetry/06-json.png)

Süreler olduğunuz nerede 10 000 işaretlerini çizgilerine içinde 1ms =. Örneğin, bu değerleri 1ms süresini göster toosend isteği hello tarayıcısından 3ms ve 1.8s tooprocess hello sayfa hello tarayıcıda tooreceive:

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[Ayrıntılı veri başvuru hello özellik türleri ve değerleri için model.](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a>Merhaba veri işleme
Küçük bir ölçekte bazı kod toopull parçalayın verilerinizi yazma, elektronik tabloya okuyun ve benzeri. Örneğin:

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

Daha büyük bir kod örneği için bkz: [çalışan rolü kullanarak][exportasa].

## <a name="delete"></a>Eski verileri Sil
Lütfen depolama kapasitesi yönetme ve gerekirse hello eski verileri silmek için sorumlu olduğunu unutmayın.

## <a name="if-you-regenerate-your-storage-key"></a>Depolama anahtarınızı yeniden oluşturursanız...
Merhaba anahtar tooyour depolama değiştirirseniz, sürekli verme çalışmayı durdurur. Azure hesabınızda bir bildirim görürsünüz.

Merhaba sürekli Dışarı Aktar dikey penceresini açın ve dışa aktarma düzenleyin. Hello verme hedef düzenlemek, ancak yalnızca hello aynı depolama seçili bırakın. Tamam tooconfirm'ı tıklatın.

![Düzen hello sürekli verme, açın ve üç dışa aktarma hedefi kapatın.](./media/app-insights-export-telemetry/07-resetstore.png)

Merhaba sürekli verme yeniden başlatılır.

## <a name="export-samples"></a>Dışarı aktarma örnekleri

* [Akış analizi kullanarak tooSQL dışarı aktarma][exportasa]
* [Stream Analytics örnek 2](app-insights-export-stream-analytics.md)

Büyük ölçek üzerinde dikkate [Hdınsight](https://azure.microsoft.com/services/hdinsight/) -hello bulutta Hadoop kümeleri. Hdınsight çeşitli teknolojiler yönetmek ve büyük veri çözümleme sağlar ve Application Insights ' dışarı tooprocess veri kullanabilirsiniz.

## <a name="q--a"></a>Soru-Cevap
* *Ancak tüm istiyorum tek seferlik bir indirme bir grafik.*  

    Evet, bunu yapabilirsiniz. Merhaba dikey penceresinde Hello üstünde tıklatın **verileri dışa aktar**.
* *Bir verme ayarlayın, ancak my deposunda verisi yok.*

    Hello verme ayarladığınız bu yana Application Insights uygulamanızdan tüm telemetri aldınız mı? Yalnızca yeni verileri alırsınız.
* *I tooset verme yukarı denedi ancak erişim reddedildi*

    Kuruluşunuz tarafından Hello hesabına ait toobe hello sahipler veya katkıda bulunanlar grupların üyesi varsa.
* *Düz toomy kendi şirket içi depolama dışa aktarabilirsiniz?*

    Hayır, özür dileriz. Bizim verme Altyapısı şu anda yalnızca Azure storage ile şu anda çalışıyor.  
* *My deposunda put veri herhangi sınırı toohello miktarını var mı?*

    Hayır. Merhaba verme silene kadar biz verisi itmesi tutmak. Biz blob storage için hello dış sınırına ulaşıp ancak oldukça büyük durdurmanız. Bu, kullandığınız ne kadar depolama alanı tooyou toocontrol olur.  
* *Kaç tane BLOB'lar ı hello depolama alanında görmeniz gerekir?*

  * Her veri türü için (veri kullanılabiliyorsa) seçili tooexport, yeni blob dakikada oluşturulur.
  * Ayrıca, yüksek trafiğe sahip uygulamalar için ek bölüm birimleri ayrılır. Bu durumda her birimi dakikada bir blob oluşturur.
* *Merhaba anahtar toomy depolama yeniden veya hello kapsayıcısının hello adı değiştirildi ve hello verme artık çalışmıyor.*

    Merhaba verme düzenleyin ve hello dışarı aktarma hedefi dikey penceresini açın. Merhaba öncekiyle aynı depolama seçili bırakın ve Tamam tooconfirm'ı tıklatın. Dışarı aktarma yeniden başlatılır. Merhaba değişiklik hello son birkaç gün içinde ise, veri kaybı olmaz.
* *Merhaba verme duraklatabilir miyim?*

    Evet. Devre dışı bırak'ı tıklatın.

## <a name="code-samples"></a>Kod örnekleri

* [Akış analizi örneği](app-insights-export-stream-analytics.md)
* [Akış analizi kullanarak tooSQL dışarı aktarma][exportasa]
* [Ayrıntılı veri başvuru hello özellik türleri ve değerleri için model.](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
