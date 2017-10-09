---
title: Merhaba JavaScript API kullanarak raporlarla aaaInteract | Microsoft Docs
description: "Power BI Embedded, hello JavaScript API kullanarak raporlarla etkileşim"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>Merhaba JavaScript API kullanarak Power BI raporları ile etkileşim
tooeasily katıştırmak Power BI raporları uygulamalarınıza hello Power BI JavaScript API sağlar. Merhaba API uygulamalarınızı programlı olarak farklı rapor öğeleri sayfa ve filtreleri gibi etkileşim kurabilirsiniz. Bu etkileşim Power BI raporlarını uygulamanızın daha tümleşik bir parçası yapar.

Uygulamanızda barındırılan IFRAME Merhaba uygulaması bir parçası olarak kullanarak bir Power BI raporu ekleme. Görüntü aşağıdaki hello görebileceğiniz gibi hello IFRAME uygulama ve hello rapor arasında sınırı görevi görür. 

![Javascript API’si olmadan Power BI embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

işlem çok daha kolay katıştırma hello Hello IFRAME yapar, ancak hello JavaScript API hello rapor ve uygulamanızı birbirleriyle etkileşime giremezler. Bu etkileşimi eksikliği bunu hello rapor gerçekten hello uygulamanın parçası değil gibi eşitleyerek duruma getirebilirsiniz. gerçekten Hello rapor ve uygulama İleri ve geri toocommunicate görüntü aşağıdaki hello olduğu gibi gerekir.

![Javascript API’si ile Power BI embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

Merhaba Power BI JavaScript API hello IFRAME sınır güvenli bir şekilde geçirebilir toowrite kod etkinleştirir. Bu etkinleştirir, uygulama tooprogrammatically bir eylemi gerçekleştirir bir rapor ve kullanıcıların hello rapor içinde açmak eylemlerine olayları için toolisten.

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>Power BI JavaScript API hello ile neler yapabileceğiniz?
Merhaba JavaScript API ile raporlarını yönetme, bir raporda toopages gidin, bir raporu filtreleme ve olayları katıştırma işlemek. Merhaba Aşağıdaki diyagramda hello API hello yapısını gösterir.

![Power BI JavaScript API’si diyagramı](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>Raporları yönetme
Merhaba Javascript API hello rapor ve sayfa düzeyinde toomanage davranışı etkinleştirir:

* Belirli bir Power BI rapor uygulamanızda güvenli bir şekilde ekleme - hello deneyin [demo uygulama ekleme](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * Erişim belirteci ayarlama
* Merhaba rapor yapılandırın
  * Etkinleştirme ve hello filtre bölmesi ve sayfa gezinti bölmesinde devre dışı bırak - hello deneyin [güncelleştirme ayarları demo uygulaması](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * Sayfalar ve filtreleri için varsayılan değerleri ayarlamak - hello deneyin [kümesi Varsayılanları Tanıtımı](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* Tam ekran moduna giriş ve çıkış

[Bir raporu ekleme hakkında daha fazla bilgi edinin](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>Bir rapordaki toopages gidin
Merhaba JavaScript API enbales bir rapor ve tooset hello geçerli sayfada, toodiscover tüm sayfaları. Merhaba deneyin [Gezinti demo uygulaması](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).

[Sayfa gezintisi hakkında daha fazla bilgi edinin](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>Bir raporu filtreleme
Merhaba JavaScript API temel ve Gelişmiş filtreleme katıştırılmış raporlar ve rapor sayfaları için özellikleri sağlar. Merhaba deneyin [demo uygulama filtreleme](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), bazı tanıtım kodu buraya gözden geçirin.  

#### <a name="basic-filters"></a>Temel filtreler
Temel bir filtre bir sütun veya hiyerarşi düzeyi yerleştirilir ve değerleri tooinclude veya hariç tutma listesini içerir.

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>Gelişmiş filtreler
Gelişmiş filtreleri kullanma hello mantıksal işleci veya OR ve her biri kendi işleç ve değer bir veya iki koşulları kabul edin. Desteklenen koşullar şunlardır:

* None
* LessThan
* LessThanOrEqual
* GreaterThan
* GreaterThanOrEqual
* Contains
* DoesNotContain
* StartsWith
* DoesNotStartWith
* Is
* IsNot
* IsBlank
* IsNotBlank

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[Filtreleme hakkında daha fazla bilgi edinin](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>Olayları işleme
Ayrıca hello IFRAME toosending bilgileri, uygulamanız da hello IFRAME gelen olayların aşağıdaki hello hakkında bilgi alabilirsiniz:

* Embed
  * loaded
  * error
* Reports
  * pageChanged
  * dataSelected (yakında)

[Olayları işleme hakkında daha fazla bilgi edinin](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>Sonraki adımlar
Merhaba Power BI JavaScript API hakkında daha fazla bilgi için bağlantılar aşağıdaki hello denetleyin:

* [JavaScript API’si Wiki](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [Nesne modeli başvurusu](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* Örnekler
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [Canlı tanıtım](https://microsoft.github.io/PowerBI-JavaScript/demo/)

