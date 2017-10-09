---
title: "aaaAzure uygulama Insights Telemetri veri modeli - Telemetri bağlamı | Microsoft Docs"
description: "Uygulama Insights telemetri bağlamı veri modeli"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a>Telemetri bağlamı: Application Insights veri modeli

Her telemetri öğeyi kesin türü belirtilmiş bağlam alanları olabilir. Her alan belirli bir izleme senaryosu sağlar. Merhaba özel özellikler koleksiyonu toostore veya uygulamaya özgü özel bağlamsal bilgileri kullanın.


##<a name="application-version"></a>Uygulama sürümü

Hello uygulama içerik alanlarında her zaman hello telemetri gönderiyor hello uygulama hakkındaki bilgilerdir. Uygulama, kullanılan tooanalyze eğilim değişiklikler hello uygulama davranışına ve bağıntı toohello dağıtımları sürümüdür.

En fazla uzunluk: 1024


##<a name="client-ip-address"></a>İstemci IP adresi

Merhaba istemci aygıt Hello IP adresi. IPv4 ve IPv6 desteklenir. Telemetri bir hizmetten gönderildiğinde, hello konumu bağlam hello işlemi hello hizmetinde başlatılan hello kullanıcı hakkındadır. Application Insights hello coğrafi konum bilgileri hello istemci IP ayıklayın ve ardından kesme. Bu nedenle istemci IP kendisi tarafından son kullanıcı bilgilerinizle kullanılamaz. 

En fazla uzunluk: 46


##<a name="device-type"></a>Aygıt türü

Bu alan kullanılan hello aygıt hello son kullanıcı hello uygulamasının tooindicate hello türü kullanıyor. Bugün öncelikle toodistinguish JavaScript telemetri hello cihaz türünden 'Browser' sunucu tarafı telemetri 'PC' hello cihaz türüyle ile kullanılır.

En fazla uzunluk: 64


##<a name="operation-id"></a>İşlem kimliği

Merhaba kök işlemi benzersiz tanıtıcısı. Bu tanımlayıcı toogroup telemetri arasında birden çok bileşen sağlar. Bkz: [telemetri bağıntı](application-insights-correlation.md) Ayrıntılar için. Merhaba işlem kimliği, bir istek veya bir sayfa görünümü tarafından oluşturulur. Diğer tüm telemetri isteği ya da sayfa görünümü içeren hello için bu alan toohello değerini ayarlar. 

En fazla uzunluk: 128


##<a name="parent-operation-id"></a>Üst işlem kimliği

Merhaba telemetri öğesi'nin en yakın üst benzersiz tanıtıcısı hello. Bkz: [telemetri bağıntı](application-insights-correlation.md) Ayrıntılar için.

En fazla uzunluk: 128


##<a name="operation-name"></a>İşlem adı

Merhaba (Grup) hello işlemin adı. Merhaba işlem adı, bir istek veya bir sayfa görünümü tarafından oluşturulur. Diğer tüm telemetri öğeleri istek veya sayfa görünümü içeren hello için bu alan toohello değerini ayarlayın. İşlem adı işlemlerini (örneğin ' GET Home/Index') grubu için tüm hello telemetri öğeleri bulmak için kullanılır. "Bu sayfada oluşturulan hello tipik özel durumları nelerdir." gibi soruları kullanılan tooanswer bu bağlam özelliğidir

En fazla uzunluk: 1024


##<a name="synthetic-source-of-hello-operation"></a>Merhaba işlemin yapay kaynak

Yapay kaynağının adı. Birkaç telemetri hello uygulamasından yapay trafiği temsil edebilir. Web Gezgin dizin hello web sitesi, site kullanılabilirlik testleri veya Application Insights SDK kendisini gibi tanılama kitaplıklarından izlemeleri olabilir.

En fazla uzunluk: 1024


##<a name="session-id"></a>Oturum kimliği

Oturum kimliği - hello uygulama hello kullanıcının etkileşim hello örneği. Merhaba oturum bağlamı alanları her zaman hello son kullanıcı bilgilerdir. Telemetri bir hizmetten gönderildiğinde, hello oturum bağlamı hello işlemi hello hizmetinde başlatılan hello kullanıcı hakkındadır.

En fazla uzunluk: 64


##<a name="anonymous-user-id"></a>Anonim kullanıcı kimliği

Anonim kullanıcı kimliği. Merhaba son kullanıcı hello uygulamasının temsil eder. Telemetri bir hizmetten gönderildiğinde, hello kullanıcı bağlamı hello işlemi hello hizmetinde başlatılan hello kullanıcı hakkındadır.

[Örnekleme](app-insights-sampling.md) hello teknikleri toominimize hello toplanan telemetri miktarı biridir. Algoritma denemeleri tooeither örnekleme örnek giriş veya çıkış tüm hello telemetri bağıntılı. Anonim kullanıcı kimliği, puan nesil örnekleme için kullanılır. Bu nedenle anonim kullanıcı kimliği yeterince rastgele bir değeri olmalıdır. 

Anonim kullanıcı kimliği toostore kullanıcı adı kötüye hello alanının kullanmaktır. Kimliği doğrulanmış kullanıcı kimliği kullanın.

En fazla uzunluk: 128


##<a name="authenticated-user-id"></a>Kimliği doğrulanmış kullanıcı kimliği

Kimliği doğrulanmış kullanıcı kimliği. Anonim kullanıcı kimliği, bu alan ters Hello kolay bir ad ile Merhaba kullanıcıyı temsil eder. PII bilgilerini bu yana çoğu SDK'sı tarafından varsayılan olarak toplanmaz.

En fazla uzunluk: 1024


##<a name="account-id"></a>Hesap Kimliği

Çok kiracılı uygulamalara hello hesap kimliği veya adı, hangi hello kullanıcı ile hareket budur. Örnekler, abonelik kimliği için Azure portal veya blog adı blog platformu olabilir.

En fazla uzunluk: 1024


##<a name="cloud-role"></a>Bulut rolü

Merhaba rol hello uygulamanın adını, bir parçasıdır. Doğrudan azure toohello rol adını eşler. Ayrıca kullanılan toodistinguish tek bir uygulamanın parçası olan mikro hizmetler olabilir.

En fazla uzunluk: 256


##<a name="cloud-role-instance"></a>Bulut rol örneği

Merhaba uygulaması çalıştığı hello örneğinin adı. Bilgisayar adı şirket içi, Azure için örnek adı.

En fazla uzunluk: 256


##<a name="internal-sdk-version"></a>Dahili: SDK sürümü

SDK sürümü. Https://github.com/Microsoft/ApplicationInsights-Home/BLOB/master/SDK-AUTHORING.MD#SDK-Version-Specification bilgi için bkz.

En fazla uzunluk: 64


##<a name="internal-node-name"></a>Dahili: Düğüm adı

Bu alan, fatura amacıyla kullanılan hello düğüm adı temsil eder. Toooverride hello standart algılama düğümlerinin kullanın.

En fazla uzunluk: 256


## <a name="next-steps"></a>Sonraki adımlar

- Nasıl çok öğrenin[genişletmek ve filtre telemetri](app-insights-api-filtering-sampling.md).
- Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.
- Standart bağlam özellikleri koleksiyonunu denetleyin [yapılandırma](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).
