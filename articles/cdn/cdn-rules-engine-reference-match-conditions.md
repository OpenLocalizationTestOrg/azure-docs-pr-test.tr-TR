---
title: "aaaAzure CDN kurallar altyapısı eşleşme koşullar | Microsoft Docs"
description: "Azure CDN başvuru belgelerine altyapısı eşleşme koşulları ve özellikleri kuralları."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 5e79f8f0c75a646e13bf315c492b9f2a9defc396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-match-conditions"></a>Azure CDN kurallar altyapısı eşleşen koşulları
Bu konuda listeleri ayrıntılı açıklamaları hello kullanılabilir eşleşme koşullar Azure içerik teslim ağı (CDN) için [kurallar altyapısı](cdn-rules-engine.md).

Merhaba ikinci bir kural hello eşleşme koşul parçasıdır. Bir eşleşme koşulu, belirli türde bir özellik kümesi gerçekleştirilecek istekler tanımlar.

Örneğin, belirli bir konumdaki içerik kullanılan toofilter isteklerini belirli bir IP adresi ya da ülke veya üst bilgileri tarafından oluşturulan istekler olabilir.

## <a name="always"></a>Her zaman

Merhaba her zaman eşleştirme özellikleri tooall istekleri varsayılan ayarlar tasarlanmış tooapply bir durumdur.

## <a name="device"></a>Cihaz

bir mobil aygıttan kendi özelliğe göre yapılan istekleri Hello aygıt eşleşme koşulu tanımlar.  Mobil cihaz algılama aracılığıyla gerçekleştirilir [WURFL](http://wurfl.sourceforge.net/).  WURFL yetenekleri ve onların CDN kurallar altyapısı değişkenleri aşağıda listelenmiştir.

> [!NOTE] 
> Merhaba değişkenleri aşağıdaki hello desteklenir **değiştirmek istemci isteği üstbilgisi** ve **değiştirme istemci yanıt üstbilgisi** özellikleri.

Özellik | Değişken | Açıklama | Örnek değerler
-----------|----------|-------------|----------------
Marka adı | % {wurfl_cap_brand_name} | Merhaba marka hello aygıtının adını belirten bir dize. | Samsung
Aygıt işletim sistemi | % {wurfl_cap_device_os} | Merhaba cihazda yüklü hello işletim sistemi gösteren bir dize. | İOS
Cihaz işletim sistemi sürümü | % {wurfl_cap_device_os_version} | Merhaba hello cihazda yüklü işletim sistemi hello sürüm numarasını gösterir bir dize. | 1.0.1
Çift yönü | % {wurfl_cap_dual_orientation} | Merhaba aygıt çift orientation destekleyip desteklemediğini belirten bir Boole değeri. | TRUE
HTML DTD tercih edilen | % {wurfl_cap_html_preferred_dtd} | HTML içeriği için hello mobil aygıtın tercih edilen belge türü tanımı (DTD) gösteren bir dize. | Yok<br/>xhtml_basic<br/>HTML5
Satır içi kullanım görüntüsü | % {wurfl_cap_image_inlining} | Merhaba aygıt Base64 destekleyip desteklemediğini belirten bir Boole değeri görüntüleri kodlanmış. | False
Android olduğu | % {wurfl_vcap_is_android} | Merhaba aygıt hello Android işletim sistemi kullanıp kullanmadığını belirten bir Boole değeri. | TRUE
İOS | % {wurfl_vcap_is_ios} | Merhaba cihaz iOS kullanıp kullanmadığını belirten bir Boole değeri. | False
Akıllı TV | % {wurfl_cap_is_smarttv} | Merhaba aygıt akıllı TV olup olmadığını belirten bir Boole değeri. | False
Smartphone olduğu | % {wurfl_vcap_is_smartphone} | Merhaba aygıt akıllı olup olmadığını belirten bir Boole değeri. | TRUE
Tablet olduğu | % {wurfl_cap_is_tablet} | Merhaba aygıt tablet olup olmadığını belirten bir Boole değeri. Bu bir işletim Sisteminden bağımsız açıklamasıdır. | TRUE
Kablosuz aygıt | % {wurfl_cap_is_wireless_device} | Merhaba aygıt kablosuz aygıt olarak kabul edilip edilmediğini belirten bir Boole değeri. | TRUE
Pazarlama adı | % {wurfl_cap_marketing_name} | Merhaba cihazın pazarlama adı belirten bir dize. | BlackBerry 8100 inci
Mobil tarayıcı | % {wurfl_cap_mobile_browser} | Merhaba tarayıcı belirten bir dize toorequest içerik hello aygıttan kullanılır. | Chrome
Mobil tarayıcı sürümü | % {wurfl_cap_mobile_browser_version} | Merhaba tarayıcı hello sürümünü belirten bir dize toorequest içerik hello aygıttan kullanılır. | 31
Model adı | % {wurfl_cap_model_name} | Hello cihazın model adını belirten dize. | S3
Aşamalı indirme | % {wurfl_cap_progressive_download} | Hala yüklenirken hello aygıt ses/video hello çalınmasını destekleyip desteklemediğini belirten bir Boole değeri. | TRUE
Sürüm tarihi | % {wurfl_cap_release_date} | Merhaba yıl ve ay cihaz üzerinde hangi hello edildi belirten bir dize toohello WURFL veritabanı eklendi.<br/><br/>Biçimi:`yyyy_mm` | 2013_december
Çözümleme yüksekliği | % {wurfl_cap_resolution_height} | Merhaba cihazın yüksekliğini piksel cinsinden belirten bir tamsayı. | 768
Çözümleme genişliği | % {wurfl_cap_resolution_width} | Merhaba cihazın genişliğini piksel cinsinden belirten bir tamsayı. | 1024


## <a name="location"></a>Konum

Bu koşullara uyan hello sahibinin konum temelinde tasarlanmış tooidentify isteği.

Ad | Amaç
-----|--------
Sayı olarak | Belirli bir ağdan kaynaklanan istekleri tanımlar.
Ülke | Belirtilen hello kaynaklanan istekleri tanımlayan ülkelerde.


## <a name="origin"></a>Kaynak

Bu koşullara uyan bu noktası tooCDN depolama veya müşteri kaynak sunucu tasarlanmış tooidentify isteklerdir.

Ad | Amaç
-----|--------
CDN kaynak | CDN depolama alanında depolanan içerik isteklerini tanımlar.
Müşteri kaynağı | Belirli bir müşteri kaynak sunucuda depolanan içerik isteklerini tanımlar.


## <a name="request"></a>İstek

Bu koşullara uyan özelliklerine göre tasarlanmış tooidentify isteği.

Ad | Amaç
-----|--------
İstemci IP adresi | Belirli bir IP adresinden kaynaklanan istekleri tanımlar.
Tanımlama bilgisi parametresi | Denetimleri hello belirtilen hello için her istek ile ilişkili tanımlama bilgisi değeri.
Tanımlama bilgisi parametresi Regex | Normal ifade hello tanımlama bilgilerini hello için her istek ile ilişkili belirtilen denetler.
Edge Cname | Tooa belirli kenar CNAME noktası istekleri tanımlar.
Başvuran etki alanı | Gelen başvurulan istekleri tanımlayan hello belirtilen hostname(s).
İstek üstbilgisi değişmez değeri | Belirtilen hello içeren istekleri tanımlayan üstbilgi kümesi tooa belirtilen değerleri.
İstek üstbilgisi Regex | Belirtilen hello içeren istekleri tanımlayan hello eşleşen üstbilgi kümesi tooa değeri belirtilen normal ifade.
İstek üstbilgisi joker karakter | Belirtilen hello içeren istekleri tanımlayan üstbilgi hello belirtilen desenle eşleşen tooa değeri ayarlayın.
İstek yöntemi | İstekleri tarafından HTTP yöntemleri tanımlar.
İstek düzeni | İstekleri kendi HTTP protokolü tarafından tanımlar.

## <a name="url"></a>URL

Bu koşullara uyan kendi URL tabanlı tasarlanmış tooidentify isteği.

Ad | Amaç
-----|--------
URL yolu dizini | İstekleri kendi göreli yoluna göre tanımlar.
URL yolu genişletme | İstekleri, dosya adı uzantısına göre tanımlar.
URL yolu dosya | İstekleri, dosya tanımlar.
URL yolu değişmez değeri | Bir istek karşılaştırır göreli yol toohello değeri belirtilen kullanıcının.
URL yolu Regex | Bir istek karşılaştırır göreli yol toohello normal ifade belirtilen kullanıcının.
URL yolu joker karakter | Bir isteğin göreli yol toohello belirtilen desen karşılaştırır.
URL sorgu değişmez değeri | Bir istek karşılaştırır sorgu dizesi toohello değeri belirtilen kullanıcının.
URL sorgu parametresi | Merhaba belirtilen sorgu dizesi parametresi belirtilen desenle eşleşen tooa değeri içeren istekleri tanımlar.
URL sorgu Regex | Merhaba belirtilen sorgu dizesi parametresi belirtilen normal ifadeyle eşleşen tooa değerini ayarlayın içeren istekleri tanımlar.
URL sorgu joker karakter | Karşılaştırır hello karşı hello isteğin sorgu dizesi değerleri belirtildi.


## <a name="next-steps"></a>Sonraki adımlar
* [Azure CDN'ye genel bakış](cdn-overview.md)
* [Kuralları altyapısı başvurusu](cdn-rules-engine-reference.md)
* [Kurallar altyapısı koşullu ifadeler](cdn-rules-engine-reference-conditional-expressions.md)
* [Kurallar altyapısı özellikleri](cdn-rules-engine-reference-features.md)
* [Merhaba kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma](cdn-rules-engine.md)

