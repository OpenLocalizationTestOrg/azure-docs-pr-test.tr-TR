---
title: "Azure Stream Analytics & AzureML işlevleriyle ölçeklendirme aaaJob | Microsoft Docs"
description: "Nasıl tooproperly ölçeklendirme akış analizi işleri (bölümlendirme, SU miktar ve daha fazla) öğrenin Azure Machine Learning işlevleri kullanırken."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>Stream Analytics işiniz Azure Machine Learning işlevlerini ölçeklendirme
Bu genellikle bir akış analizi işi oldukça kolay tooset ve bazı örnek veriler üzerinden çalıştırın. Biz toorun gerektiğinde biz ne yapması gerektiğini daha yüksek veri birimi ile aynı işi hello? Bize nasıl tooconfigure hello Stream Analytics işi onu ölçeklendirir böylece toounderstand gerektirir. Bu belgede, biz Machine Learning işlevleri işleriyle hello özel yönleri ölçeklendirme Stream Analytics üzerinde odaklanır. Tooscale akış analizi işleri genel hello makalesine bakın nasıl bilgi [işlerini ölçeklendirme](stream-analytics-scale-jobs.md).

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>Bir Azure Machine Learning işlevinde Stream Analytics nedir?
Stream Analytics Machine Learning işlevinde hello Stream Analytics sorgu dili normal işlev çağrısında gibi kullanılabilir. Ancak, hello Sahne hello işlev çağrıları gerçekten Azure Machine Learning Web hizmeti isteklerinin aynıdır. Machine Learning web hizmetleri Mini toplu olarak adlandırılan "birden çok satır toplu işleme" Destek, hello aynı hizmeti API çağrısı, tooimprove web genel üretilen işi. Lütfen daha fazla ayrıntı için makaleler hello bakın; [Stream Analytics azure Machine Learning işlevlerde](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/) ve [Azure Machine Learning Web Hizmetleri](../machine-learning/machine-learning-consume-web-services.md).

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>Akış analizi işi Machine Learning işlevleri ile yapılandırma
Stream Analytics işi için Machine Learning işlevi yapılandırırken, iki parametre tooconsider, hello Machine Learning işlev çağrılarını ve akış birimleri (SUs) hello Stream Analytics işi için sağlanan hello hello toplu iş boyutu vardır. toodetermine hello uygun değerleri bunlar için önce bir karar verimlilik, gecikme süresi arasında diğer bir deyişle, hello Stream Analytics işi gecikmesi ve her SU verimini yapılması gerekir. Ek SUs çalışan hello işi hello maliyetini artırsa SUs her zaman tooa iş tooincrease iyi bölümlenmiş bir akış analizi sorgu verimini eklenebilir.

Bu nedenle önemli toodetermine hello olan *dayanıklılık* gecikme Stream Analytics işi çalışır. Azure Machine Learning hizmet istekleri çalışmasını ek gecikme hello Stream Analytics işi hello gecikme bileşik toplu iş boyutu ile doğal olarak artar. Merhaba üzerinde toplu iş boyutu artırmayı diğer yandan, hello Stream Analytics işi tooprocess sağlar * hello ile daha fazla olay *aynı numarası* Machine Learning web hizmeti istekleri. Genellikle hello artış Machine Learning web hizmeti gecikme toplu iş boyutu alt doğrusal toohello çıktığını olduğundan, önemli tooconsider hello Machine Learning web hizmeti belirli bir durumda en ekonomik toplu iş boyutu dur. Merhaba varsayılan toplu iş boyutu hello web hizmeti isteklerinin 1000'dir ve hello kullanarak ya da değiştirilebilir [Stream Analytics REST API](https://msdn.microsoft.com/library/mt653706.aspx "Stream Analytics REST API") veya hello [PowerShell istemci Akış analizi için](stream-analytics-monitor-and-manage-jobs-use-powershell.md "akış analizi için PowerShell istemcisi").

Bir toplu iş boyutu belirlendikten sonra hello miktarını akış birimler (SUs) belirlendiği, temel hello olayların sayısına hello işlevi saniyede tooprocess gerekiyor. Akış birimleri hakkında daha fazla bilgi için bkz: [Stream Analytics işlerini ölçeklendirme](stream-analytics-scale-jobs.md).

Genel olarak, olduğunu 20 eş zamanlı bağlantı toohello Machine Learning web hizmeti her 6 SUs için 1 SU işleri ve 3 SU işleri 20 eş zamanlı bağlantı de alırsınız dışında.  Örneğin, saniye başına 200.000 olayları hello giriş verisi oranı ise ve hello toplu iş boyutu sol toohello 1000 hello elde edilen web hizmeti gecikme 1000 olayları Mini toplu ile 200 MS varsayılandır. Başka bir deyişle, her bağlantı 5 toohello Machine Learning web hizmeti bir saniyede isteğinde bulunabilir. 20 bağlantılarla hello Stream Analytics işi 20.000 olayları 200 MS ve bu nedenle 100.000 olayları bir saniyede işleyebilir. Bu nedenle tooprocess 200.000 olayları saniyede hello Stream Analytics işi 40 eşzamanlı bağlantı too12 SUs gelen gerekir. Merhaba Stream Analytics işi toohello Machine Learning web hizmeti uç noktası hello isteklerinden Hello diyagramda gösterilmiştir – her 6 SUs sırasında en fazla 20 eş zamanlı bağlantı tooMachine Learning web hizmeti vardır.

![Stream Analytics Machine Learning işlevleri 2 iş örnek ile ölçek](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "Machine Learning işlevleri 2 iş örnek ile ölçek akış analizi")

Genel olarak, ***B*** toplu iş boyutu için ***L*** hello web hizmeti gecikme süresi için milisaniye cinsinden toplu iş boyutu B, Stream Analytics işi ile verimini hello ***N*** SUs değil:

![Ölçeklendirme Machine Learning işlevleri formülü olan Stream Analytics](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "ölçeklendirme Machine Learning işlevleri formülü olan akış analizi")

Bir sağlayabildiği hello 'en fazla eş zamanlı çağrılarını' hello Machine Learning web hizmeti yan olabilir, bu toohello en büyük değeri (şu anda 200) tooset önermiştir.

Bu ayar hakkında daha fazla bilgi için lütfen hello gözden [Machine Learning Web Hizmetleri için ölçeklendirme makalesine](../machine-learning/machine-learning-scaling-webservice.md).

## <a name="example--sentiment-analysis"></a>Örnek – düşünceleri çözümleme
Merhaba aşağıdaki örnekte bir akış analizi işi hello düşünceleri analiz Machine Learning işlevi ile hello açıklandığı gibi içerir [Stream Analytics Machine Learning tümleştirme Öğreticisi](stream-analytics-machine-learning-integration-tutorial.md).

Merhaba sorgusu hello tarafından izlenen bir basit tam olarak bölümlenmiş sorgudur **düşünceleri** aşağıda gösterildiği gibi işlev:

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

Senaryo aşağıdaki hello düşünün; saniye başına 10.000 tweet'leri verimi ile akış analizi işi tooperform düşünceleri hello tweet'leri (olayları) analizini oluşturulması gerekir. 1 SU kullanarak, bu akış analizi işi mümkün toohandle hello trafik olabilir? Merhaba varsayılan toplu iş boyutu 1000 hello işin kullanarak mümkün tookeep yukarı hello giriş olmalıdır. Daha fazla hello Machine Learning işlevi hello genel varsayılan gecikmeyle hello düşünceleri analiz Machine Learning web hizmeti (varsayılan toplu iş boyutu 1000) olan gecikme saniyesi birden fazla oluşturması eklendi. Merhaba Stream Analytics iş **genel** veya uçtan uca gecikme süresi genellikle birkaç saniye olacaktır. Bu akış analizi işi, daha ayrıntılı göz *özellikle* hello Machine Learning işlev çağrıları. Merhaba toplu iş boyutu 1000 sahip olmak, 10.000 olayları verimini yaklaşık 10 istekleri tooweb hizmetin zaman alır. Hatta 1 SU ile yeterli eşzamanlı bağlantı tooaccommodate vardır bu trafiği giriş.

Ancak ne 100 x hello giriş olay hızı artırır ve hello Stream Analytics işi tooprocess 1.000.000 tweet'leri saniyede gerekiyor? İki seçenek vardır:

1. Merhaba toplu iş boyutunu artırın veya
2. Bölüm hello Giriş akışı tooprocess hello olayları paralel

Merhaba ilk seçeneğiyle iş hello **gecikme** artmasına neden olur.

Merhaba ikinci seçeneği ile daha fazla SUs sağlanan toobe gerekir ve bu nedenle daha fazla eşzamanlı Machine Learning web hizmeti isteklerinin oluşturmak. Merhaba iş yani **maliyet** artmasına neden olur.

Merhaba düşünceleri analiz Machine Learning web hizmeti Hello gecikme 200 MS 1000 olay toplu işlemler için veya aşağıda 5.000 olay toplu işleri, 10.000 olay toplu işlemler için 300ms veya 500ms 25.000 olay toplu işlemler için 250ms olduğunu varsayın.

1. Merhaba ilk seçeneği kullanılarak (**değil** daha fazla SUs sağlama), hello toplu iş boyutu artırılmasını çok**25.000**. Bu sırayla hello iş tooprocess 20 eş zamanlı bağlantı toohello Machine Learning web hizmeti ile 1.000.000 olayları (ile 500ms çağrı başına bir gecikme) olanak tanır. Bu nedenle hello Stream Analytics işi toohello düşünceleri işlevi hello Machine Learning web hizmeti isteklerinin gelen artırılmasını istekler son ek gecikme hello **200 MS** çok**500ms**. Ancak, bu toplu iş boyutu Not **olamaz** artırılmasını sonsuz hello Machine Learning web hizmetlerini gerektirdiği şekilde bir isteğin hello yükü boyutu 4 MB olması veya işlemin 100 saniye sonra web hizmeti isteği zaman aşımı daha küçük.
2. Merhaba toplu iş boyutu 200 MS web hizmeti gecikmeyle 1000 sol, her 20 eş zamanlı bağlantı toohello web hizmeti mümkün tooprocess 1000 * 20 * 5 olayları olacaktır Hello ikinci seçeneği kullanılarak, saniyede 100.000 =. Bu nedenle tooprocess 1.000.000 olayları ikinci, hello iş başına 60 SUs gerekir. Karşılaştırılan toohello ilk seçenek, Stream Analytics işi, diğer hizmet toplu istekleri sırayla web yapacağı bir artan maliyetini oluşturuluyor.

Aşağıdaki tablo hello Stream Analytics işi hello verimini için farklı SUs ve toplu boyutları (saniye başına etkinlik sayısı) içindir.

| Toplu iş boyutu (ML gecikme) | 500 (200 ms) | 1.000 (200 ms) | 5.000 (250ms) | 10.000 (300ms) | 25.000 (500ms) |
| --- | --- | --- | --- | --- | --- |
| **1 SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **3 SUs** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **6 SUs** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **12 SUs** |5,000 |10,000 |40,000 |60,000 |100,000 |
| **18 SUs** |7,500 |15,000 |60,000 |90,000 |150,000 |
| **24 SUs** |10,000 |20,000 |80,000 |120,000 |200,000 |
| **…** |… |… |… |… |… |
| **60 SUs** |25,000 |50,000 |200,000 |300,000 |500,000 |

Şimdi tarafından zaten nasıl akış analizi, Machine Learning işlevleri işe iyi anlamış olmanız. Büyük olasılıkla de olayları için toplu veri kaynakları ve her "çekme" veriler "çekme" döndürür akış analizi işleri Stream Analytics işi tooprocess hello anlamanız. Bu çekme modeli hello Machine Learning web hizmeti isteklerinin nasıl etkiler?

Normalde, Machine Learning işlevleri için ayarlarız hello toplu iş boyutu tam olarak her akış analizi işi "çekme" tarafından döndürülen olay sayısı hello bölünebilir olmayacaktır. Ne zaman hello Machine Learning web hizmeti "kısmi" toplu işleri çağrılacağı gerçekleşir. Bu yapılır toonot ek iş gecikme yükü çekme toopull birleştirmesi olaylarından doğurur.

## <a name="new-function-related-monitoring-metrics"></a>İşlevi ile ilgili yeni izleme ölçümleri
Hello İzleyicisi alanını akış analizi işi'de, üç ek işlevi ödemeyle ilgili ölçümlerini eklenmiştir. İŞLEV İSTEKLERİ, işlevi olayları ve başarısız işlev İSTEKLER hello aşağıda görüldüğü gibi olduklarını.

![Ölçeklendirme akış analizi Machine Learning işlevleri ölçümlerle](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "ölçeklendirme Machine Learning işlevleri ölçümlerle akış analizi")

Merhaba şu şekilde tanımlanır:

**İŞLEV İSTEKLERİ**: Merhaba işlevi istek sayısı.

**İŞLEV olayları**: hello sayı olayların hello içinde işlev istekleri.

**BAŞARISIZ işlev İSTEKLER**: Merhaba başarısız işleve istek sayısı.

## <a name="key-takeaways"></a>Anahtar paketler
toosummarize hello ana noktaları, sipariş tooscale Stream Analytics işi Machine Learning işlevlerle hello aşağıdaki öğeleri dikkate alınmalıdır:

1. Merhaba giriş olay hızı
2. Akış analizi işi hello için gecikme süresini Hello izin (ve böylece hello toplu iş boyutu hello Machine Learning web hizmeti istekleri)
3. Merhaba sağlanan akış analizi SUs ve Machine Learning web hizmeti isteklerinin (Merhaba ek işlevi ilişkili maliyetler) hello sayısı

Tam olarak bölümlenmiş bir akış analizi sorgu örnek olarak kullanılmıştır. Daha karmaşık bir sorgu gerekirse hello [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) hello Stream Analytics ekibinden Ek Yardım almak için mükemmel bir kaynaktır.

## <a name="next-steps"></a>Sonraki adımlar
Stream Analytics hakkında daha fazla toolearn bakın:

* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
