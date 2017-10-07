---
title: "aaaCloud Cruiser ve Microsoft Azure fatura API tümleştirme | Microsoft Docs"
description: "Benzersiz bir perspektif Microsoft Azure fatura ortağında bulut Cruiser deneyimlerini hello Azure faturalama API'leri kendi üründe tümleştirme sağlar.  Bu, özellikle kullanarak/bulut Cruiser Microsoft Azure Pack için çalışırken ilginizi çekiyor mu Azure ve bulut Cruiser müşteriler için kullanışlıdır."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a>Cruiser ve Microsoft Azure API tümleştirme faturalama bulut
Bu makalede nasıl maliyet benzetimi ve analiz yeni Microsoft Azure fatura API'leri için iş akışı içinde bulut Cruiser kullanılabilir hello'den toplanan hello bilgiler açıklanmaktadır.

## <a name="azure-ratecard-api"></a>Azure RateCard API
Merhaba RateCard API Azure'dan oranı hakkında bilgi sağlar. Merhaba doğru kimlik bilgileriyle kimlik doğrulandıktan sonra hello API toocollect Azure üzerinde kullanılabilen, teklif kimliğiyle ilişkili hello oranları birlikte hello hizmetler hakkındaki meta verileri sorgulayabilir.

Merhaba hello API'sinden hello fiyatları hello A0 (Windows) gösteren bir örnek yanıt aşağıdadır örneği:

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a>Cruiser'ın arabirimi tooAzure RateCard API bulut
Bulut Cruiser hello RateCard API bilgilerini farklı yollarla yararlanabilirsiniz. Bu makale için nasıl bu kullanılan toomake Iaas iş yükü maliyet benzetimi ve analiz olabilir göstereceğiz.

toodemonstrate bu kullanım örneği, Microsoft Azure Pack (WAP) üzerinde çalışan çeşitli örneklerinin bir iş yükü düşünün. Merhaba hedef Azure ve bu tür geçiş yapmanın tahmin hello maliyetleri aynı bu iş yüküne toosimulate olduğu. İçinde bu benzetim toocreate sipariş, gerçekleştirilen iki ana görevleri toobe vardır:

1. **Alma ve işlem hello hizmet hello RateCard API ' toplanan bilgilerin.** Bu görev ayrıca hello extract hello RateCard API öğesinden dönüştürülmüş ve yayımlanan tooa yeni oranı plan olduğu hello çalışma kitapları üzerinde gerçekleştirilir. Bu yeni oranı planının hello benzetimleri tooestimate üzerinde kullanılacak Azure fiyatlar hello.
2. **WAP Hizmetleri ve Iaas için Azure services normalleştirin.** Varsayılan olarak, WAP Hizmetleri tabanlı kaynakların (CPU, bellek boyutu, Disk boyutu, vb.) Azure Hizmetleri örnek boyutu (A0, A1, A2, vb.) dayanır. Bu ilk görev bulut Cruiser'ın ETL altyapısı tarafından gerçekleştirilen, bu kaynakları örnek boyutları, benzer tooAzure örneği Hizmetleri burada gönderilebilir çalışma kitaplarını çağrılır.

### <a name="import-data-from-hello-ratecard-api"></a>Merhaba RateCard API verileri alın
Bulut Cruiser çalışma kitaplarını hello RateCard API bir otomatik şekilde toocollect ve işlem bilgilerini sağlayın.  ETL (ayıklama dönüştürme yük) çalışma kitaplarını tooconfigure hello koleksiyonu, dönüştürme ve veri yayımlama hello bulut Cruiser veritabanına izin verilir.

Her çalışma kitabı toocorrelate bilgilerinden farklı kaynaklar toocomplement izin verme, bir veya birden çok koleksiyon sahip veya hello kullanım verilerini kullanmasıdır. iki ekran görüntüleri Göster nasıl aşağıdaki hello yeni bir toocreate *koleksiyonu* varolan bir çalışma kitabını ve hello bilgi alma *koleksiyonu* hello RateCard API öğesinden:

![Şekil 1 - yeni bir koleksiyon oluşturma][1]

![Şekil 2 - hello yeni koleksiyon verileri alın][2]

Merhaba çalışma kitabına Hello verileri aldıktan sonra olası toocreate olan birden çok adımları ve dönüştürme işlemleri, toomodify ve model hello veri. Biz yalnızca altyapı olarak-hizmet (Iaas biz hello dönüştürme adımları tooremove gereksiz satır veya kayıtları kullanabilirsiniz) ilgilendiğiniz olduğundan, bu örnekte, Iaas dışında tooservices ilgili.

Merhaba aşağıdaki ekran görüntüsü hello dönüştürme adımları RateCard API'SİNDEN toplanan tooprocess hello verileri kullanılan gösterir:

![Şekil 3 - dönüştürme tooprocess toplanan verileri RateCard API'SİNDEN adımları][3]

### <a name="defining-new-services-and-rate-plans"></a>Yeni hizmetler ve oranı tanımlama planları
Bulut Cruiser üzerinde farklı şekillerde toodefine hizmetleri vardır. Merhaba seçeneklerden birini tooimport hello hello kullanım verilerinden hizmetleridir. Bu yöntem hello sağlayıcı tarafından hello Hizmetleri zaten tanımlandığı genel Bulutlar ile çalışırken, yaygın olarak kullanılır.

Ücret planı oranları veya geçerlilik tarihlerini ya da diğer seçenekler arasında müşteri grubunu göre uygulanan toodifferent Hizmetleri olabilir fiyatlar kümesidir. Oranı planları, aynı zamanda bulut Cruiser toocreate benzetimi veya "What-if" senaryolar, toounderstand kullanılabilir hizmetler değişiklikler iş yükü hello toplam maliyeti nasıl etkileyebilir.

Bu örnekte, bulut Cruiser hello RateCard API toodefine yeni hizmetleri hello hizmet bilgileri kullanacağız. Hello aynı şekilde, biz ilişkili hello oranları kullanabilirsiniz toohello Hizmetleri toocreate oranı yeni bir Plan bulut Cruiser üzerinde.

Sonunda hello hello dönüştürme işlemi, bu olası toocreate yeni bir adımdır ve yeni hizmetler ve ücretlerin hello RateCard API hello verilerden yayımlayın.

![Şekil 4 - Yeni hizmetler ve ücretlerin hello RateCard API hello verileri yayımlama][4]

### <a name="verify-azure-services-and-rates"></a>Azure Hizmetleri ve ücretlerin doğrulayın
Merhaba Hizmetleri ve ücretlerin yayımlandıktan sonra bulut Cruiser'ın alınan hizmet hello listesini doğrulayabilirsiniz *Hizmetleri* sekmesi:

![Şekil 5 - hello yeni hizmetler doğrulanıyor][5]

Merhaba üzerinde *oranı planları* sekmesinde hello hello hızı "AzureSimulation hello RateCard API ' alınan" olarak adlandırılan yeni oranı planı kontrol edebilirsiniz.

![Şekil 6 - yeni oranı planlamak ve ilişkili ücretleri hello doğrulanıyor][6]

### <a name="normalize-wap-and-azure-services"></a>WAP ve Azure Hizmetleri normalleştirin
Varsayılan olarak, WAP hesaplama, bellek ve ağ kaynaklarını hello kullanım dayanarak kullanım bilgileri sağlar. Bulut Cruiser içinde hizmetlerini doğrudan üzerinde hello ayırma veya bu kaynakların ölçülen kullanımı tanımlayabilirsiniz. Örneğin, CPU kullanımı, her bir saat ya da ücret hello GB tooan örneği ayrılan bellek için bir temel hızı ayarlayabilirsiniz.

Bu örnekte, sipariş toocompare maliyetleri WAP ve Azure arasında için eşlenen tooAzure Hizmetleri sonra olabilen paket içine WAP üzerinde tooaggregate hello kaynak kullanımı ihtiyacımız var. Bu dönüşüm kolayca hello çalışma kitaplarında uygulanabilir:

![Şekil 7 - WAP veri toonormalize Hizmetleri dönüştürme][7]

Merhaba çalışma kitabı son adımda Hello toopublish hello hello bulut Cruiser veritabanına verilerdir. Bu adım sırasında hello kullanım verilerini şimdi (yani toohello Azure Hizmetleri eşleştirme) Hizmetleri içine gruplanır ve toodefault oranları toocreate hello ücretleri bağlanır.

Bitiş hello çalışma kitabı sonra bir görev hello zamanlayıcıda ekleme ve hello sıklığı ve süresi hello çalışma kitabı toorun için belirterek hello veri hello işlenmesini otomatikleştirebilirsiniz.

![Şekil 8 - çalışma kitabı planlama][8]

### <a name="create-reports-for-workload-cost-simulation-analysis"></a>İş yükü maliyet benzetimi analiz için rapor oluşturma
Merhaba kullanım toplanır ve ücretleri hello bulut Cruiser veritabanına yüklenen sonra biz, biz işlemleriniz hello bulut Cruiser Öngörüler modülü toocreate hello iş yükü maliyet benzetimi yararlanabilirsiniz.

Sipariş toodemonstrate bu senaryo, rapor aşağıdaki hello oluşturduk:

![Maliyet karşılaştırma][9]

Hello üst grafik maliyet karşılaştırmasını hello fiyat WAP (mavi) ve Azure (mavi) arasında belirli her hizmet için çalışan hello yükünün karşılaştırma, hizmetleri tarafından gösterir.

Merhaba alt grafik gösterir hello departmanı göre ayrılmış ancak aynı veri. Bu her departman toorun hello maliyetlerini, iş yükü WAP ve Azure, hello tasarrufları çubuğunda (yeşil) arasındaki hello fark birlikte gösterilir.

## <a name="azure-usage-api"></a>Azure kullanım API'si
### <a name="introduction"></a>Giriş
Microsoft hello Azure kullanım API'si aboneleri tooprogrammatically çekme kullanım verileri toogain Öngörüler kendi tüketimi izin vererek, kısa süre önce kullanıma sunmuştur. Merhaba daha zengin veri kümesi bu API aracılığıyla kullanılabilir yararlanabilir bulut Cruiser müşteriler için harika haber budur.

Bulut Cruiser çeşitli şekillerde hello kullanım API'si ile Merhaba tümleştirme yararlanabilirsiniz. Merhaba ayrıntı düzeyi (saatlik kullanım bilgileri) ve kaynak meta veri bilgileri API sağlar hello kullanılabilir gerekli dataset toosupport esnek giderleri veya geri ödeme modelleri hello. 

Bu öğreticide, biz bulut Cruiser kullanım API'si bilgi hello nasıl yararlanabilir bir örnek sunacaktır. Daha açık belirtmek gerekirse, biz Azure üzerinde bir kaynak grubu oluşturmak, hello hesap yapısı için etiketler ilişkilendirin ve ardından çekme ve bulut Cruiser içine hello etiketi bilgi işlem hello süreci açıklar.

Merhaba son toobe mümkün toocreate raporları hello bir aşağıdaki gibi ve maliyet mümkün tooanalyze ve hello etiketlere göre doldurulmuş hello hesap yapısı göre tüketimi hedeftir.

![Şekil 10 - etiketleri kullanarak dökümleri raporla][10]

### <a name="microsoft-azure-tags"></a>Microsoft Azure etiketleri
Merhaba verileri hello Azure kullanım API kullanılabilir değil yalnızca tüketim bilgileri, aynı zamanda kendisiyle ilişkilendirilmiş herhangi bir etiket dahil olmak üzere kaynak meta verileri içerir. Etiketleri kaynaklarınızı kolay bir yolu tooorganize sağlar, ancak etkin sipariş toobe içinde tooensure gerekir:

* Sağlama zaman etiketleri doğru uygulanan toohello kaynaklardır
* Etiketler düzgün şekilde hello giderleri/geri ödeme işlemi tootie hello kullanım toohello kuruluş hesabı yapısına kullanılır.

Özellikle hello sağlamak veya yan şarj manuel bir işlem olduğunda bu gereksinimleri her ikisi de zorlu olabilir. Yanlış yazılan, eksik veya hatalı bile etiketleri müşterilerden yaygın şikayetlerinden alındığında etiketleri ve bu hatalar kullanarak ömrü yan oldukça zor şarj hello üzerinde yapabilirsiniz.

Merhaba ile yeni Azure kullanım API'si, bulut Cruiser bilgi etiketleme kaynak çekin ve çalışma kitapları olarak adlandırılan bir karmaşık ETL aracı aracılığıyla ortak bu etiketleme hataları düzeltin. Normal ifadeler ve veri bağıntı kullanarak dönüştürme bulut Cruiser yanlış etiketli kaynakları belirleyin ve hello doğru ilişkilendirmesini hello kaynakların hello tüketici sağlama hello doğru etiketleri, uygulayın.

Hello yan ücretlendirme, bulut Cruiser hello giderleri/geri ödeme işlemini otomatikleştiren ve hello etiketi bilgi tootie hello kullanım toohello uygun Tüketici (departman, bölme, proje, vb.) yararlanabilirsiniz. Bu Otomasyon büyük bir geliştirme sağlar ve tutarlı ve denetlenebilir doluyor işlem emin olabilirsiniz.

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a>Microsoft Azure üzerinde etiketlere sahip bir kaynak grubu oluşturma
Merhaba Bu öğreticinin ilk adımı toocreate hello Azure portalında bir kaynak grubunda olduğundan, sonra yeni etiketler tooassociate toohello kaynakları oluşturun. Bu örnekte, biz etiketleri aşağıdaki hello oluşturacağınız: departman, ortam, sahibi, proje.

Merhaba ekran görüntüsü aşağıda etiketleri hello kaynak grubuyla ilişkilendirilen bir örnek göstermektedir.

![Şekil 11 - Azure portalında ilişkili etiketlerle kaynak grubu][11]

Merhaba sonraki hello kullanım API'si bulut Cruiser toopull hello bilgileri adımdır. Merhaba kullanım API'si şu anda JSON biçiminde yanıtlar sağlar. Alınan hello veri örneği şöyledir:

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a>Merhaba kullanım API'si bulut Cruiser içine verileri alın
Bulut Cruiser çalışma kitaplarını hello kullanım API'si bir otomatik şekilde toocollect ve işlem bilgilerini sağlayın. ETL (ayıklama dönüştürme yük) çalışma kitabı tooconfigure hello koleksiyonu, dönüştürme ve veri yayımlama hello bulut Cruiser veritabanına sağlar.

Her çalışma kitabı bir veya birden çok koleksiyon olabilir. Bu, farklı kaynaklar toocomplement veya ayırma hello kullanım verilerini toocorrelate bilgileri sağlar. Bu örnekte, yeni bir sayfa hello Azure şablonu çalışma kitabında oluşturacağız (*UsageAPI)* ve yeni bir küme *koleksiyonu* hello kullanım API'si tooimport bilgileri.

![Şekil 3 - kullanım API'si verileri hello UsageAPI sayfasına alındı][12]

Bu çalışma kitabı zaten diğer sahip olmadığına dikkat edin sayfaları tooimport Azure hizmetlerinden (*ImportServices*) ve işlem hello faturalama API hello tüketim bilgileri (*PublishData*).

Merhaba kullanım API'si toopopulate hello sonraki kullanacağız *UsageAPI* sayfası ve hello hello faturalama API hello tüketim verilerle correlate hello bilgi *PublishData* sayfası.

### <a name="processing-hello-tag-information-from-hello-usage-api"></a>Merhaba kullanım API'si işlem hello etiketi bilgileri
Merhaba çalışma kitabına Hello verileri aldıktan sonra dönüştürme adımları hello oluşturacağız *UsageAPI* sipariş tooprocess hello hello API bilgilerinden içindeki sayfa. "JSON bölme" işlemci tooextract hello tek alandan etiketler sonra her birini (departman, proje, sahibi ve ortam) için alanları oluşturmak toouse ilk adımdır.

![Şekil 4 - hello etiket bilgilerini için yeni alanlar oluşturma][13]

Bildirim hello "Ağ" hizmet hello etiket bilgilerini (sarı kutusu) eksik, ancak biz hello parçası olup olmadığını doğrulayabilirsiniz hello bakarak aynı kaynak grubu *ResourceGroupName* alan. Merhaba etiketleri hello için diğer kaynaklar bu kaynak grubundan olduğundan biz etiketleri toothis kaynak hello işlemde daha sonra bu bilgileri tooapply hello kullanabilirsiniz.

Merhaba sonraki toocreate bir arama tablosu özellikle görüntüyle hello bilgilerinden hello etiketleri toohello adımdır *ResourceGroupName*. Bu arama tablosu hello sonraki adım tooenrich hello tüketim veri etiketi bilgilerle kullanılır.

### <a name="adding-hello-tag-information-toohello-consumption-data"></a>Merhaba etiketi bilgi toohello tüketim veri ekleme
Biz toohello atlayabilirsiniz artık *PublishData* sayfası, hangi işlemlerin hello hello faturalama API tüketim bilgileri ve hello etiketlerini ayıklanan hello alanlarını ekleyin. Bu işlem hello kullanarak hello önceki adımda oluşturulan hello arama tablosu bakarak gerçekleştirilir *ResourceGroupName* hello aramaları için başlangıç anahtarı olarak.

![Şekil 5 - hello hesap yapısı hello aramaları hello bilgileriyle doldurma][14]

Merhaba uygun hesap yapısı alanları hello "Ağ" hizmeti için uygulandığını eksik etiketleri hello ile Merhaba sorunu düzeltme dikkat edin. Biz de hello hesabı yapısı alanlarını kaynaklar için "Diğer" bizim hedef kaynak grubu dışında doldurulmuş, sipariş toodifferentiate hello üzerlerinde bildirir.

Şimdi biz tooadd bir adım toopublish hello kullanım verilerini yeterlidir. Bu adım sırasında bizim ücret planı tanımlanan her hizmet için uygun hızlarını hello hello elde edilen ücret hello veritabanına yüklenen ile uygulanan toohello kullanım bilgileri olacaktır.

Merhaba en iyi bölümü, yalnızca bu süreci toogo kez olmasıdır. Merhaba çalışma kitabı tamamlandığında tooadd yeterlidir, toohello Zamanlayıcı ve çalışacağı saatlik veya günlük Merhaba, zamanlanan saat. Ardından, yeni raporlar oluşturmak veya varolanları sipariş tooanalyze hello veri tooget anlamlı bilgiler bulut kullanımınıza özelleştirme, yalnızca bir konudur.

### <a name="next-steps"></a>Sonraki Adımlar
* Lütfen bulut Cruiser çalışma kitaplarını ve raporlar oluşturma hakkında ayrıntılı yönergeler başvurmak için tooCloud Cruiser çevrimiçi [belgelerine](http://docs.cloudcruiser.com/) (geçerli oturum açması gerekli).  Bulut Cruiser hakkında daha fazla bilgi için lütfen başvurun [ info@cloudcruiser.com ](mailto:info@cloudcruiser.com).
* Bkz: [Microsoft Azure kaynak tüketimini Öngörüler elde](billing-usage-rate-card-overview.md) hello Azure kaynak kullanımı ve RateCard API'leri genel bakış.
* Merhaba denetleyin [Azure faturalama REST API Başvurusu](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) hem API'ler hakkında daha fazla bilgi için Azure Resource Manager hello tarafından sağlanan API'leri hello kümesinin parçası olan.
* Bizim Microsoft Azure fatura API kod örnekleri sağ hello örnek koda toodive kullanmak isterseniz, denetleme [Azure Kod örnekleri](https://azure.microsoft.com/documentation/samples/?term=billing).

### <a name="learn-more"></a>Daha Fazla Bilgi Edinin
* Merhaba bkz [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md) makale toolearn hello Azure Resource Manager hakkında daha fazla bilgi.

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Şekil 1 - yeni bir koleksiyon oluşturma"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Şekil 2 - hello yeni koleksiyon verileri alın"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Şekil 3 - dönüştürme tooprocess toplanan verileri RateCard API'SİNDEN adımları"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Şekil 4 - Yeni hizmetler ve ücretlerin hello RateCard API hello verileri yayımlama"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Şekil 5 - hello yeni hizmetler doğrulanıyor"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Şekil 6 - yeni oranı planlamak ve ilişkili ücretleri hello doğrulanıyor"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Şekil 7 - WAP veri toonormalize Hizmetleri dönüştürme"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Şekil 8 - çalışma kitabı planlama"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Şekil 9 - hello iş yükü maliyet karşılaştırma senaryo için örnek raporu"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Şekil 10 - etiketleri kullanarak dökümleri raporla"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Şekil 11 - Azure portalında ilişkili etiketlerle kaynak grubu"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Şekil 12 - kullanım API'si verileri hello UsageAPI sayfasına alındı"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Şekil 13 - hello etiket bilgilerini için yeni alanlar oluşturma"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Şekil 14 - hello hesap yapısı hello aramaları hello bilgileriyle doldurma"
