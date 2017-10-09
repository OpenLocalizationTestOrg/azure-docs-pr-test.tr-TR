---
title: "aaaLoad dengeleyici özel araştırmalar ve izleme sistem durumu | Microsoft Docs"
description: "Yük dengeleyicinin arkasındaki Azure yük dengeleyici toomonitor örnekleri için nasıl toouse özel yoklamaları öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a>Yük dengeleyici araştırmalarını anlama

Azure yük dengeleyici araştırmalar kullanarak hello yetenek toomonitor hello sunucu örneklerinin durumunu sunar. Bir araştırma toorespond başarısız olduğunda, yük dengeleyici yeni bağlantıları toohello sağlıksız örnek gönderme durdurur. Merhaba varolan bağlantılar etkilenmez ve yeni bağlantılar toohealthy örnekleri gönderilir.

Bulut hizmeti rollerinizi (çalışan rolleri ve web rolleri) bir konuk Aracısı araştırma izlemek için kullanın. Sanal makineler yük dengeleyici arkasında kullandığınızda, TCP veya HTTP özel araştırmalara yapılandırılması gerekir.

## <a name="understand-probe-count-and-timeout"></a>Araştırma sayısı ve zaman aşımı anlama

Araştırma davranışı bağlıdır:

* en fazla olarak etiketli bir örnek toobe izin başarılı araştırmalar Hello sayısı.
* Aşağı olarak etiketli bir örnek toobe neden başarısız araştırmalar Hello sayısı.

Merhaba zaman aşımı ve sıklığı değeri SuccessFailCount ayarlanmış bir örneği çalışıyor veya çalışmıyor onaylanan toobe olup olmadığını belirler. Hello Azure portal, hello zaman aşımı tootwo kez hello hello sıklığı değerini ayarlanır.

Merhaba araştırma yapılandırma tüm örneklerinin yük dengeli bir uç nokta (diğer bir deyişle, yük dengeli kümesi) olmalıdır hello aynı. Bu farklı araştırma yapılandırma olamaz anlamına gelir. aynı barındırılan hizmetin belirli uç noktası bileşimi için her bir rol örneği veya hello sanal makine için. Örneğin, her bir örneği aynı yerel bağlantı noktaları ve zaman aşımlarına olması gerekir.

> [!IMPORTANT]
> Bir yük dengeleyici araştırması hello IP adresi 168.63.129.16 kullanır. Bu genel IP adresi iletişimi toointernal platform kaynakları hello Getir-bilgisayarınızı-kendi-IP Azure sanal ağı senaryosu için kolaylaştırır. Merhaba sanal genel IP adresi 168.63.129.16 tüm bölgelerde kullanılır ve değişmez. Tüm yerel güvenlik duvarı ilkeleri bu IP adresine izin öneririz. Yalnızca hello iç Azure platformu bu adresi bir iletiden kaynağı bir güvenlik riski düşünülmemelidir. Bunu yaparsanız, çeşitli yapılandırma gibi senaryolarda beklenmeyen davranışlara olacaktır hello 168.63.129.16 ve IP adreslerini yinelenen aynı IP adresi aralığı.

## <a name="learn-about-hello-types-of-probes"></a>Araştırmalar Hello türleri hakkında bilgi edinin

### <a name="guest-agent-probe"></a>Konuk aracı araştırması

Bu araştırma yalnızca Azure bulut Hizmetleri için kullanılabilir. Yük Dengeleyici hello Konuk Aracısı hello sanal makine içinde kullanır ve dinler ve örneği hello hazır durumda olan bir HTTP 200 Tamam Yanıtla yalnızca hello zaman yanıt (diğer bir deyişle, içinde başka durum geri dönüştürme ya da durdurma meşgul gibi).

Daha fazla bilgi için bkz: [yapılandırma hello Hizmet tanım dosyasını (csdef) sistem durumu araştırmalarının](https://msdn.microsoft.com/library/azure/ee758710.aspx) veya [bulut Hizmetleri için bir Internet'e yönelik Yük Dengeleyici oluşturmaya başlamak](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a>Bir örneği sağlıksız olarak işaretlemek Konuk aracı araştırması ne yapar?

HTTP 200 Tamam toorespond Hello Konuk Aracısı başarısız olursa, hello yük dengeleyici işaretleri örneği yanıt olarak ve trafik toothat örneği gönderme durduğunda hello. Merhaba yük dengeleyici tooping hello örneği devam eder. Bir HTTP 200 ile Merhaba Konuk aracısı yanıt verirse, hello yük dengeleyici trafiği toothat örneğini yeniden gönderir.

Web rolü kullandığınızda, hello Web sitesi kodu genellikle hello Azure dokusunu veya konuk aracısı tarafından izlenmeyen w3wp.exe çalıştırır. Bu w3wp.exe (örneğin, HTTP 500 yanıtları)'de hataları bildirilen toohello Konuk Aracısı olmaz ve hello yük dengeleyici döndürme dışında bu örneği olmayacak anlamına gelir.

### <a name="http-custom-probe"></a>HTTP özel araştırma

Merhaba özel HTTP yük dengeleyici araştırmasını hello rol örneği kendi özel mantık toodetermine hello durumunu oluşturabileceğiniz anlamı hello varsayılan Konuk Aracısı araştırma, geçersiz kılar. Merhaba yük dengeleyici uç noktanızı varsayılan olarak 15 dakikada araştırmaları. Merhaba zaman aşımı süresini (varsayılan olarak 31 saniye) içindeki bir HTTP 200 ile yanıt verirse hello örneği hello yük dengeleyici döndürme toobe olarak kabul edilir.

Bu yük dengeleyici döndürme kendi mantığı tooremove örneklerden tooimplement istediğiniz durumlarda yararlı olabilir. Örneğin, % 90 CPU ise ve 200 olmayan durum döndürür tooremove örneği karar. W3wp.exe kullanan web rolleri varsa, bu da otomatik al anlamına gelir, Web sitesini, Web sitesi kodunuzdaki hataları 200 olmayan durum toohello yük dengeleyici araştırmasını geri getireceğinden izleme.

> [!NOTE]
> Merhaba HTTP özel araştırma göreli yollar ve yalnızca HTTP protokolünü destekler. HTTPS desteklenmiyor.

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a>Bir örneği sağlıksız olarak işaretlemek bir HTTP özel araştırma ne yapar?

* Merhaba HTTP uygulama 200 (örneğin, 403, 404 veya 500) dışında bir HTTP yanıt kodunu döndürür. Uygulama hello pozitif bir bildirim budur örneği alınması gereken hizmet dışı hemen.
* Merhaba HTTP sunucusu hello zaman aşımı süresinden sonra hiç yanıt vermez. Ayarlanmış hello zaman aşımı değeri bağlı olarak, bu, birden çok araştırma istekleri hello araştırma çalışmıyor olarak işaretlenmiş önce yanıtlanmadan Git gelebilir (diğer bir deyişle, önce SuccessFailCount araştırmalar gönderilir).
* Merhaba sunucu TCP sıfırlama aracılığıyla hello bağlantıyı kapatır.

### <a name="tcp-custom-probe"></a>TCP özel araştırma

TCP araştırmalar üç yönlü el sıkışma hello tanımlanan bağlantı noktası ile gerçekleştirerek bir bağlantı başlatır.

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a>Bir örneği sağlıksız olarak işaretlemek TCP özel bir araştırma yapan nedir?

* Merhaba TCP sunucu hello zaman aşımı süresinden sonra hiç yanıt vermez. Çalışmıyor başarısız araştırma hello sayısına bağlıdır olarak hello yoklama zaman işaretlenen hello araştırma çalışmıyor olarak işaretlemek önce yanıtlanmadan yapılandırılmış toogo olduğunu ister.
* Merhaba araştırma hello rol örneğinden sıfırlama TCP alır.

Bir HTTP durum araştırması veya bir TCP araştırması yapılandırma hakkında daha fazla bilgi için bkz: [PowerShell kullanarak Kaynak Yöneticisi'nde bir Internet'e yönelik Yük Dengeleyici oluşturmaya başlamak](load-balancer-get-started-internet-arm-ps.md).

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a>Yük Dengeleyici döndürme uygulamasına geri sağlıklı örnekleri Ekle

TCP ve HTTP araştırmaları sağlıklı olarak kabul edilir ve hello rol örneği sağlıklı olduğunda olarak işaretleyin:

* Merhaba yük dengeleyici VM önyüklenir bir pozitif araştırma hello ilk zaman hello alır.
* Merhaba numarası (daha önce açıklanan) SuccessFailCount gerekli toomark hello rol örneği sağlıklı olarak olan başarılı araştırmalar hello değerini tanımlar. Rol örneği kaldırılmışsa, başarılı, art arda araştırmalar hello sayısı eşit veya SuccessFailCount toomark hello rol örneği çalışıyor olarak hello değerini aşıyor.

> [!NOTE]
> Rol örneği Hello durumunu dalgalı, hello yük dengeleyici artık hello rol örneği hello sağlam durumda geçirmeden önce bekler. Bu ilke tooprotect hello kullanıcı ve hello altyapısı gerçekleştirilir.

## <a name="use-log-analytics-for-load-balancer"></a>Yük Dengeleyici için günlük analizi kullanın

Kullanabileceğiniz [analytics yük dengeleyici için oturum](load-balancer-monitor-log.md) toocheck Merhaba, araştırma sistem durumu ve araştırma sayısı üzerinde. Günlüğe kaydetme, yük dengeleyici sistem durumu hakkında Power BI veya Azure operasyonel Öngörüler tooprovide istatistiklerle birlikte kullanılabilir.
