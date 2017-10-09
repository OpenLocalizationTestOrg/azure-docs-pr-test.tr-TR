---
title: "aaaLogic uygulama sınırları ve yapılandırması | Microsoft Docs"
description: "Genel Bakış hello hizmet sınırları ve yapılandırma değerlerini mantığı uygulamaları için kullanılabilir."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 739509afe5c9a7b7e946ba3571951264127e5297
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-app-limits-and-configuration"></a>Logic Apps sınırları ve yapılandırma

Aşağıda Azure Logic Apps için hello geçerli sınırlarını ve yapılandırma ayrıntıları hakkında bilgi verilmektedir.

## <a name="limits"></a>Sınırlar

### <a name="http-request-limits"></a>HTTP istek sınırları

Tek bir HTTP isteği ve/veya bağlayıcı çağrı için sınırları şunlardır.

#### <a name="timeout"></a>Zaman aşımı

|Ad|Sınır|Notlar|
|----|----|----|
|İstek zaman aşımı|120 saniye|Bir [zaman uyumsuz desen](../logic-apps/logic-apps-create-api-app.md) veya [döngü kadar](logic-apps-loops-and-scopes.md) gerektiğinde dengeleyebilirsiniz|

#### <a name="message-size"></a>İleti boyutu

|Ad|Sınır|Notlar|
|----|----|----|
|İleti boyutu|100 MB|Bazı bağlayıcılar ve API 100 MB desteklemeyebilir |
|İfade değerlendirme sınırı|131.072 karakterleri|`@concat()`, `@base64()`, `string` bu sınırdan daha uzun olamaz|

#### <a name="retry-policy"></a>Yeniden deneme ilkesi

|Ad|Sınır|Notlar|
|----|----|----|
|Yeniden deneme sayısı|10| Varsayılan 4'tür. Merhaba ile yapılandırabilirsiniz [İlkesi parametre yeniden deneyin](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|
|En uzun gecikme yeniden deneyin|1 saat|Merhaba ile yapılandırabilirsiniz [İlkesi parametre yeniden deneyin](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|
|Yeniden deneme Min gecikmesi|5 saniye|Merhaba ile yapılandırabilirsiniz [İlkesi parametre yeniden deneyin](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|

### <a name="run-duration-and-retention"></a>Çalışma süresi ve bekletme

Çalıştıran tek bir mantıksal uygulama için hello sınırları şunlardır.

|Ad|Sınır|Notlar|
|----|----|----|
|Çalışma süresi|90 gün||
|Depolama bekletme|90 gün|Çalıştırma başlangıç zamanı hello başlatma|
|En az yinelenme aralığı|1 saniye|| logic apps ile App Service planı 15 saniye
|En fazla yineleme aralığı|500 gün||

Normal işlem akışında süresi veya depolama bekletme sınırları çalıştırmak tooexceed bekliyorsanız [Bize Ulaşın](mailto://logicappsemail@microsoft.com) böylece gereksinimlerinizle yardımcı olabiliriz.


### <a name="looping-and-debatching-limits"></a>Döngü ve sınırları debatching

Çalıştıran tek bir mantıksal uygulama için sınırları şunlardır.

|Ad|Sınır|Notlar|
|----|----|----|
|ForEach öğeleri|100,000|Merhaba kullanabilirsiniz [sorgu eylem](../connectors/connectors-native-query.md) gerektiği gibi toofilter büyük diziler|
|Kadar yineleme|5,000||
|SplitOn öğeleri|100,000||
|ForEach paralellik|50| Varsayılan 20'dir. Ekleyerek tooa sıralı foreach ayarlayabilirsiniz `"operationOptions": "Sequential"` toohello `foreach` eylem veya belirli düzeyde paralellik kullanma`runtimeConfiguration`|


### <a name="throughput-limits"></a>İşleme sınırları

Bir tek mantığı uygulama örneği için sınırları şunlardır. 

|Ad|Sınır|Notlar|
|----|----|----|
|Eylemler yürütmeleri 5 dakika başına |100,000|İş yükü gerektiği gibi birden çok uygulama arasında dağıtabilirsiniz|
|Eylemler eşzamanlı giden çağrıları |~2,500|Eşzamanlı istek sayısını azaltın veya gerektiği gibi hello süresini azaltın|
|Çalışma zamanı, bitiş noktası eşzamanlı gelen çağrıları |~1,000|Eşzamanlı istek sayısını azaltın veya gerektiği gibi hello süresini azaltın|
|Çalışma zamanı uç noktası 5 dakika başına çağrı okuma |60,000|İş yükü gerektiği gibi birden çok uygulama arasında dağıtabilirsiniz|
|Çalışma zamanı endpoint çağırma 5 dakika başına çağrı |45,000|İş yükü gerektiği gibi birden çok uygulama arasında dağıtabilirsiniz|

Bir süre için bu sınırı aşabilir bu sınırı normal işleme veya istek toorun yük testi tooexceed bekliyorsanız [Bize Ulaşın](mailto://logicappsemail@microsoft.com) böylece gereksinimlerinizle yardımcı olabiliriz.

### <a name="definition-limits"></a>Tanımı sınırları

Bir tek mantıksal uygulama tanımını sınırlarını şunlardır.

|Ad|Sınır|Notlar|
|----|----|----|
|İş akışı başına Eylemler|500|İç içe geçmiş iş akışları tooextend gerektiğinde bu sınırı ekleyebilirsiniz.|
|Eylem iç içe geçirme derinliği izin verilen|8|İç içe geçmiş iş akışları tooextend gerektiğinde bu sınırı ekleyebilirsiniz.|
|Her Abonelikteki bölge başına iş akışları|1000||
|İş akışı başına Tetikleyicileri|10||
|Anahtar kapsam durumlarda sınırı|25||
|İş akışı başına değişkenleri sayısı|250||
|İfade başına en fazla karakter|8,192||
|Max `trackedProperties` karakter cinsinden boyut|16,000|
|`action`/`trigger`ad sınırı|80||
|`description`uzunluk sınırı|256||
|`parameters`sınırı|50||
|`outputs`sınırı|10||

### <a name="integration-account-limits"></a>Tümleştirme hesabı sınırları

Yapıları toointegration hesabı eklenen için sınırları aşağıda verilmiştir

|Ad|Sınır|Notlar|
|----|----|----|
|Şema|8 MB|Kullanabileceğiniz [URI blob](logic-apps-enterprise-integration-schemas.md) tooupload 2 MB'den büyük dosyaları |
|Harita (XSLT dosyası)|2 MB| |
|Çalışma zamanı uç noktası 5 dakika başına çağrı okuma |60,000|İş yükü gerektiği gibi birden fazla hesap dağıtabilirsiniz|
|Çalışma zamanı endpoint çağırma 5 dakika başına çağrı |45,000|İş yükü gerektiği gibi birden fazla hesap dağıtabilirsiniz|
|Çalışma zamanı uç noktası 5 dakika başına çağrı izleme |45,000|İş yükü gerektiği gibi birden fazla hesap dağıtabilirsiniz|
|Çalışma zamanı endpoint eşzamanlı çağrıları engelleme |~1,000|Eşzamanlı istek sayısını azaltın veya gerektiği gibi hello süresini azaltın|

### <a name="b2b-protocols-as2-x12-edifact-message-size"></a>B2B protokolleri (AS2, X12, EDIFACT) boyutu iletisi

Şunlardır B2B protokolleri için hello sınırları

|Ad|Sınır|Notlar|
|----|----|----|
|AS2|50 MB|Geçerli toodecode ve kodlama|
|X12|50 MB|Geçerli toodecode ve kodlama|
|EDIFACT|50 MB|Geçerli toodecode ve kodlama|

## <a name="configuration"></a>Yapılandırma

### <a name="ip-address"></a>IP Adresi

#### <a name="logic-app-service"></a>Mantıksal uygulama hizmeti

Bir mantık uygulamasından doğrudan yapılan çağrıları (diğer bir deyişle, aracılığıyla [HTTP](../connectors/connectors-native-http.md) veya [HTTP + Swagger](../connectors/connectors-native-http-swagger.md)) veya hello listesi aşağıdaki hello belirtilen IP adresi alınması diğer HTTP istekleri:

|Mantıksal uygulama bölgesi|Giden IP|
|-----|----|
|Avustralya Doğu|13.75.153.66, 104.210.89.222, 104.210.89.244, 13.75.149.4, 104.210.91.55, 104.210.90.241|
|Avustralya Güneydoğu|13.73.115.153, 40.115.78.70, 40.115.78.237, 13.73.114.207, 13.77.3.139, 13.70.159.205|
|Güney Brezilya|191.235.86.199, 191.235.95.229, 191.235.94.220, 191.235.82.221, 191.235.91.7, 191.234.182.26|
|Orta Kanada|52.233.29.92, 52.228.39.241, 52.228.39.244|
|Doğu Kanada|52.232.128.155, 52.229.120.45, 52.229.126.25|
|Orta Hindistan|52.172.157.194, 52.172.184.192, 52.172.191.194, 52.172.154.168, 52.172.186.159, 52.172.185.79|
|Orta ABD|13.67.236.76, 40.77.111.254, 40.77.31.87, 13.67.236.125, 104.208.25.27, 40.122.170.198|
|Doğu Asya|168.63.200.173, 13.75.89.159, 23.97.68.172, 13.75.94.173, 40.83.127.19, 52.175.33.254|
|Doğu ABD|137.135.106.54, 40.117.99.79, 40.117.100.228, 13.92.98.111, 40.121.91.41, 40.114.82.191|
|Doğu ABD 2|40.84.25.234, 40.79.44.7, 40.84.59.136, 40.84.30.147, 104.208.155.200, 104.208.158.174|
|Japonya Doğu|13.71.146.140, 13.78.84.187, 13.78.62.130, 13.71.158.3, 13.73.4.207, 13.71.158.120|
|Japonya Batı|40.74.140.173, 40.74.81.13, 40.74.85.215, 40.74.140.4, 104.214.137.243, 138.91.26.45|
|Orta Kuzey ABD|168.62.249.81, 157.56.12.202, 65.52.211.164, 168.62.248.37, 157.55.210.61, 157.55.212.238|
|Kuzey Avrupa|13.79.173.49, 52.169.218.253, 52.169.220.174, 40.113.12.95, 52.178.165.215, 52.178.166.21|
|Orta Güney ABD|13.65.98.39, 13.84.41.46, 13.84.43.45, 104.210.144.48, 13.65.82.17, 13.66.52.232|
|Güneydoğu Asya|52.163.93.214, 52.187.65.81, 52.187.65.155, 13.76.133.155, 52.163.228.93, 52.163.230.166|
|Güney Hindistan|52.172.9.47, 52.172.49.43, 52.172.51.140, 52.172.50.24, 52.172.55.231, 52.172.52.0|
|Batı Avrupa|13.95.155.53, 52.174.54.218, 52.174.49.6, 40.68.222.65, 40.68.209.23, 13.95.147.65|
|Batı Hindistan|104.211.164.112, 104.211.165.81, 104.211.164.25, 104.211.164.80, 104.211.162.205, 104.211.164.136|
|Batı ABD|52.160.90.237, 138.91.188.137, 13.91.252.184, 52.160.92.112, 40.118.244.241, 40.118.241.243|
|Birleşik Krallık Güney|51.140.74.14, 51.140.73.85, 51.140.78.44|
|Birleşik Krallık Batı|51.141.54.185, 51.141.45.238, 51.141.47.136|

#### <a name="connectors"></a>Bağlayıcılar

Yapılan çağrıları bir [bağlayıcı](../connectors/apis-list.md) hello listesi aşağıdaki hello belirtilen IP adresi gelir:

|Mantıksal uygulama bölgesi|Giden IP|
|-----|----|
|Avustralya Doğu|40.126.251.213|
|Avustralya Güneydoğu|40.127.80.34|
|Güney Brezilya|191.232.38.129|
|Orta Kanada|52.233.31.197, 52.228.42.205, 52.228.33.76, 52.228.34.13|
|Doğu Kanada|52.229.123.98, 52.229.120.178, 52.229.126.202, 52.229.120.52|
|Orta Hindistan|104.211.98.164|
|Orta ABD|40.122.49.51|
|Doğu Asya|23.99.116.181|
|Doğu ABD|191.237.41.52|
|Doğu ABD 2|104.208.233.100|
|Japonya Doğu|40.115.186.96|
|Japonya Batı|40.74.130.77|
|Orta Kuzey ABD|65.52.218.230|
|Kuzey Avrupa|104.45.93.9|
|Orta Güney ABD|104.214.70.191|
|Güneydoğu Asya|13.76.231.68|
|Güney Hindistan|104.211.227.225|
|Batı Avrupa|40.115.50.13|
|Batı Hindistan|104.211.161.203|
|Batı ABD|104.40.51.248|
|Birleşik Krallık Güney|51.140.80.51|
|Birleşik Krallık Batı|51.141.47.105|


## <a name="next-steps"></a>Sonraki Adımlar  

- Logic Apps ile başlatılan tooget izleyin hello [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md) Öğreticisi.  
- [Sık rastlanan örnekleri ve senaryoları inceleyin](../logic-apps/logic-apps-examples-and-scenarios.md)
- [Logic Apps ile iş süreçlerini otomatik hale getirebilirsiniz](http://channel9.msdn.com/Events/Build/2016/T694) 
- [Bilgi nasıl tooIntegrate sistemlerinizi Logic Apps ile](http://channel9.msdn.com/Events/Build/2016/P462)
