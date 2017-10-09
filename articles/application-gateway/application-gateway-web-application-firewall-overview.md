---
title: "aaaIntroduction tooweb uygulaması Güvenlik Duvarı (WAF) Azure uygulama ağ geçidi için | Microsoft Docs"
description: "Bu sayfada Application Gateway için web uygulaması güvenlik duvarı (WAF) ile ilgili genel bir bakış sağlanmaktadır"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>Web uygulaması güvenlik duvarı (WAF)

Web uygulaması güvenlik duvarı (WAF), web uygulamalarınızda açıklardan yararlanmaya ve güvenlik açıklarına karşı merkezi koruma sağlayan bir Application Gateway özelliğidir. 

Web uygulaması güvenlik duvarı kuralları hello temel [OWASP çekirdek kural kümeleri](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 veya 2.2.9. Web uygulamaları, bilinen yaygın güvenlik açıklarından yararlanan kötü amaçlı saldırıların giderek daha fazla hedefi olmaktadır. SQL ekleme saldırıları bu açıkları arasında ortak olan, siteler arası komut dosyası tooname birkaç saldırıları. Uygulama kodundaki böyle saldırılarını önleme zor olabilir ve düzeltme eki uygulama ve hello uygulama topolojisinin birden çok katmanına izleme sıkı bakımını gerektirebilir. Bir merkezi web uygulaması Güvenlik Duvarı güvenlik yönetimi daha kolay hale getirir ve tooapplication Yöneticiler tehditleri veya yetkisiz erişimlere karşı daha iyi güvence verir. WAF Çözüm Merkezi bir konumda her tek tek web uygulamalarının güvenliğini sağlama karşı bilinen bir güvenlik açığı düzeltme eki uygulama tarafından tooa güvenlik tehdidi daha hızlı ayrıca tepki. Mevcut uygulama ağ geçitleri dönüştürülmüş tooa web uygulaması Güvenlik Duvarı etkin uygulama ağ geçidi kolayca olabilir.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

Uygulama ağ geçidi, birden çok Web siteleri ve güvenlik geliştirmeleri bir uygulama teslim denetleyici ve teklifleri SSL sonlandırma, tanımlama bilgisi tabanlı oturum benzeşimi, hepsini bir kez deneme yük dağıtımı, içerik tabanlı yönlendirme, özelliği toohost çalışır. Uygulama ağ geçidi tarafından sunulan güvenlik geliştirmeleri SSL İlkesi Yönetimi, son tooend SSL desteği içerir. Uygulama güvenliği artık doğrudan hello ADC görüşlerden tümleştirilmekte WAF (web uygulaması güvenlik duvarı) tarafından güçlendirilmiş. Bu bir kolay tooconfigure merkezi bir konum toomanage sağlar ve web uygulamalarınızın ortak web güvenlik açıklarına karşı koruma.

## <a name="benefits"></a>Avantajlar

Merhaba, uygulama ağ geçidi ve web uygulaması güvenlik duvarı sağlamak hello çekirdek avantajları şunlardır:

### <a name="protection"></a>Koruma

* Web uygulamanızı web Güvenlik Açıkları ve değişikliği toobackend kodu olmadan saldırılara karşı koruma.

* Birden çok web korumak hello uygulamasını aynı anda bir uygulama ağ geçidi. Uygulama ağ geçidi too20 Web sitelerinin tüm WAF web saldırılarına karşı korumalı tek bir ağ geçidi arkasında barındırma destekler.

### <a name="monitoring"></a>İzleme

* Gerçek zamanlı bir WAF günlüğü kullanarak web uygulamanızı saldırılara karşı izleyin. Bu günlük tümleşiktir [Azure İzleyici](../monitoring-and-diagnostics/monitoring-overview.md) tootrack WAF uyarıları günlüğe kaydeder ve kolayca eğilimlerini izleyin.

* WAF yakında Azure Güvenlik Merkezi ile tümleştirilecektir. Azure Güvenlik Merkezi, tüm Azure kaynaklarınızın güvenlik durumunu hello merkezi bir görünümünü sağlar.

### <a name="customization"></a>Özelleştirme

* Merhaba özelliği toocustomize WAF kurallar ve kural uygulama gereksinimlerinizi toosuit grupları ve hatalı pozitif sonuç ortadan kaldırmak.

## <a name="features"></a>Özellikler

Web uygulaması güvenlik duvarı CRS 3.0 ile varsayılan olarak önceden yapılandırılmış olarak gelir veya toouse 2.2.9 seçebilirsiniz. CRS 3.0, 2.2.9 sürümüne göre daha az hatalı pozitif sonuç verir. özelliği çok hello[kuralları toosuit gereksinimlerinizi özelleştirme](application-gateway-customize-waf-rules-portal.md) sağlanır. Hangi web uygulaması güvenlik duvarı korur hello ortak web güvenlik açıkları bazıları içerir:

* SQL ekleme koruması
* Siteler arası komut dosyası koruması
* Komut ekleme, HTTP isteği kaçakçılığı, HTTP yanıtı bölme ve uzak dosya ekleme saldırıcı gibi Yaygın Web Saldırıları Koruması
* HTTP protokolü ihlallerine karşı koruma
* Eksik konak kullanıcısı-aracısı ve kabul üst bilgileri gibi HTTP protokolü anormalliklerine karşı koruma
* Robotlar, gezginler ve tarayıcıları önleme
* Yaygın yanlış uygulama yapılandırmalarını (i.e. Apache, IIS vb.) algılama

Kuralları daha ayrıntılı bir listesi ve bunların korumaları hello aşağıdaki görmek için [çekirdek kural kümeleri](#core-rule-sets).

### <a name="core-rule-sets"></a>Çekirdek kural kümeleri

Application Gateway CRS 3.0 ve CRS 2.2.9 şeklinde iki kural kümesini destekler. Bu çekirdek kural kümeleri, web uygulamalarınızı kötü amaçlı etkinliğe karşı koruyan kurallar içeren koleksiyonlardır.

#### <a name="owasp30"></a>OWASP_3.0

sağlanan hello 3.0 çekirdek kural kümesi, aşağıdaki tablonun hello gösterildiği gibi 13 kuralı grupları vardır. Bu kural gruplarının her biri devre dışı bırakılabilen birden çok kural içerir.

|RuleGroup|Açıklama|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|Bilinen istenmeyen posta gönderenlerin veya kötü amaçlı etkinlik karşı kuralları tooprotect içerir.|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|Kuralları toolock yöntemleri aşağı içerir (PUT, PATCH <..)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| Hizmet Reddi (DoS) saldırılarına karşı kuralları tooprotect içerir.|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| Bağlantı noktası ve ortam tarayıcılar karşı kuralları tooprotect içerir.|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|Protokol ve sorunları kodlama karşı kuralları tooprotect içerir.|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|Üstbilgi ekleme, kaçakçılığı istek ve yanıt bölme karşı kuralları tooprotect içerir|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|Dosya ve yol saldırılarına karşı kuralları tooprotect içerir.|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|Kuralları tooprotect uzak dosya ekleme (RFI) karşı içerir|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|Kuralları tooprotect içeren yeniden uzaktan kod yürütme.|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|PHP ekleme saldırılarına karşı kuralları tooprotect içerir.|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|Siteler arası betik oluşturmaya karşı korumaya yönelik kurallar içerir.|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|SQL ekleme saldırılarına karşı korumaya yönelik kurallar içerir.|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|Oturum Fixation saldırılarına karşı kuralları tooprotect içerir.|

#### <a name="owasp229"></a>OWASP_2.2.9

sağlanan hello 2.2.9 çekirdek kural kümesi, aşağıdaki tablonun hello gösterildiği gibi 10 kuralı grupları vardır. Bu kural gruplarının her biri devre dışı bırakılabilen birden çok kural içerir.

|RuleGroup|Açıklama|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|Kuralları tooprotect protokolü ihlali (geçersiz karakter, bir istek gövdesi, vb. ile GET.) karşı içerir|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|Kuralları tooprotect karşı yanlış üst bilgileri içerir.|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|Bağımsız değişken veya sınırlamaları aşan dosyalar karşı kuralları tooprotect içerir.|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|Kısıtlı yöntemleri, üstbilgiler ve dosya türleri karşı kuralları tooprotect içerir. |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|Web gezginleri ve tarayıcılar karşı kuralları tooprotect içerir.|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|Kuralları tooprotect (oturum fixation, uzak dosya ekleme, PHP ekleme, vb.) genel saldırılarına karşı içerir|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|SQL ekleme saldırılarına karşı kuralları tooprotect içerir|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|Site komut dosyası çapraz kuralları tooprotect karşı içerir.|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|Bir kural tooprotect yolu geçişi saldırılarına karşı içerir|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|Kuralları tooprotect arka kapı Truva atı karşı içerir.|

### <a name="waf-modes"></a>WAF Modları

Uygulama ağ geçidi WAF iki moddan aşağıdaki hello içinde yapılandırılmış toorun olabilir:

* **Algılama modunu** – algılama modunda, uygulama ağ geçidi WAF yapılandırılmış toorun izler ve tüm tehdit uyarıları tooa günlük dosyasına kaydeder. Tanıları günlüğe kaydetmek uygulama ağ geçidi için açık hello kullanarak **tanılama** bölümü. WAF hello tooensure etmeniz günlük seçili ve açık. Algılama modunda çalışırken, web uygulaması güvenlik duvarı gelen istekleri engellemez.
* **Engelleme modu** – önleme modunda uygulama ağ geçidi yapılandırılmış toorun etkin bir şekilde yetkisiz erişim ve onun kuralları tarafından algılanan saldırıları engeller. Merhaba saldırgan 403 yetkisiz erişim özel durumu alır ve hello bağlantısı sonlandırıldı. Engelleme modu toolog bu tür saldırıları hello WAF günlüklerinde devam eder.

### <a name="application-gateway-waf-reports"></a>WAF İzleme

Uygulama ağ geçidiniz Hello durumunu izlemeye önemlidir. Merhaba, koruduğu web uygulaması güvenlik duvarı ve hello uygulamalarınızın durumunu izleme sağlanan günlüğe kaydetme ve Azure monitör, Azure Güvenlik Merkezi (yakında) ve günlük analizi ile tümleştirme yoluyla.

![tanılama](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Azure İzleyici

Her uygulama ağ geçidi günlüğü [Azure İzleyici](../monitoring-and-diagnostics/monitoring-overview.md) ile tümleştirilir.  Bu, WAF uyarıları ve günlükleri tootrack tanı bilgilerini sağlar.  Bu özellik hello uygulama ağ geçidi kaynağı hello portalında hello altında içinde sağlanan **tanılama** sekmesinde veya Azure İzleyicisi Merhaba doğrudan hizmet. Uygulama ağ geçidi için tanılama günlüklerini etkinleştirme hakkında daha fazla ziyaret toolearn [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Azure Güvenlik Merkezi

[Azure Güvenlik Merkezi](../security-center/security-center-intro.md) hello Azure kaynaklarınızın güvenlik engellemek, algılamak, artırılmış görünürlük aracılığı ile toothreats yanıt ve üzerinden denetlemesine yardımcı olur. Application Gateway artık [Azure Güvenlik Merkezi ile tümleşiktir](application-gateway-integration-security-center.md). Azure Güvenlik Merkezi, ortam korumasız toodetect web uygulamalarınızın tarar. Bunu şimdi uygulama ağ geçidi WAF tooprotect bu güvenlik açığından kaynakları önerilerde bulunur. Bu gibi durumlarda, uygulama ağ geçidi WAF doğrudan Azure Güvenlik Merkezi hello oluşturabilirsiniz.  Bu WAF örnekler Azure Güvenlik Merkezi ile tümleşiktir ve raporlama için tooAzure Güvenlik Merkezi uyarıları ve durum bilgilerini geri gönderir.

![Şekil 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>Günlüğe kaydetme

Application Gateway WAF, algıladığı her tehdit için ayrıntılı raporlar sağlar. Günlük kaydı Azure Tanılama günlükleri ile tümleştirilir ve uyarılar json biçiminde kaydedilir. Bu günlükler [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) ile tümleştirilebilir.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>Application Gateway WAF SKU fiyatlandırması

Web uygulaması güvenlik duvarı yeni bir WAF SKU altında bulunur. Bu SKU yalnızca Azure Resource Manager modelinde sağlama ve hello Klasik dağıtım modeli altında kullanılabilir. Ayrıca WAF SKU sadece orta ve büyük uygulama ağ geçidi örnek boyutlarında gelir. Uygulama ağ geçidi için tüm hello sınırları toohello WAF SKU de geçerlidir. Fiyatlandırma, saatlik ağ geçidi örneği ücretine ve veri işleme ücretine bağlıdır. WAF SKU’su için saatlik ağ geçidi fiyatlandırması, Standart SKU ücretlerinden farklıdır ve [Application Gateway fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/application-gateway/) bölümünde bulunabilir. Veri işleme ücretleri kalır hello aynı. Kural başına veya kural grubu başına ücret yoktur. Birden çok web uygulamaları koruyabilir hello aynı web uygulaması güvenlik duvarı ve birden çok uygulamalarını desteklemek için hiçbir ek ücret vardır. 

WAF için fatura 5/5/2017 WAF SKU ağ geçitleri devam standart ücretleri temel alınarak toobe sonra hello kadar etkili bir şekilde başlatır.

## <a name="next-steps"></a>Sonraki adımlar

WAF hello özellikleri hakkında daha fazla öğrenme sonra ziyaret [nasıl tooconfigure web uygulaması Güvenlik Duvarı'nı uygulama ağ geçidi](application-gateway-web-application-firewall-portal.md).

