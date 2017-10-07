---
title: "aaaAzure işlevler kullanım ve uygulama hizmeti planları | Microsoft Docs"
description: "Azure işlevleri, olay denetimli iş yüklerinin toomeet hello gereksinimlerini nasıl ölçeklendirir anlayın."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Azure işlevleri tüketim ve uygulama hizmeti planları 

## <a name="introduction"></a>Giriş

Azure işlevlerinin iki farklı modda çalıştırabilirsiniz: Tüketim planı ve Azure uygulama hizmeti planı. kodunuzu çalışıyorsa, çıkışı gerekli toohandle yükü olarak ölçeklendirir ve kod çalışmadığı zaman sonra ölçeklendirir hello tüketim planı otomatik olarak işlem gücü ayırır. Bu nedenle, boşta VM'ler için toopay yok ve önceden tooreserve kapasitesine sahip değilseniz. Bu makalede hello tüketim plan üzerinde odaklanmıştır. Merhaba hello uygulama hizmeti planı nasıl çalıştığı hakkında daha fazla bilgi için bkz [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Azure işlevleriyle alışık değilseniz, hello bkz [Azure işlevlerine genel bakış](functions-overview.md).

Bir işlev uygulaması oluşturduğunuzda, bir barındırma planı yapılandırmalısınız işlevleri için bu hello uygulama içerir. Her iki modda hello örneği *Azure işlevleri konak* hello işlevleri yürütür. plan denetimleri Hello türü:

* Nasıl konak örnekleri çıkışı ölçeklenir.
* kullanılabilir tooeach konak hello kaynaklar.

Şu anda hello işlev uygulaması hello oluşturma sırasında hello planı türü seçmelisiniz. Daha sonra değiştiremezsiniz. 

Uygulama hizmeti planı hello üzerinde katmanları arasında ölçeklendirebilirsiniz. Merhaba tüketim plan üzerinde Azure işlevleri, tüm kaynak ayırma otomatik olarak yönetir.

## <a name="consumption-plan"></a>Tüketim planı

Tüketim planı kullanırken, örnekleri hello Azure işlevleri konağının dinamik olarak eklenir ve hello gelen olayların sayısına göre kaldırıldı. Bu plan otomatik olarak ölçeklendirir ve yalnızca işlevlerinizi çalıştırırken işlem kaynakları için ücretlendirilirsiniz. Tüketim plan üzerinde bir işlev en fazla 10 dakika için çalıştırabilirsiniz. 

> [!NOTE]
> Merhaba varsayılan zaman aşımı işlevler tüketim planınız için 5 dakikadır. Merhaba değeri hello özelliğini değiştirerek hello işlev uygulaması artan too10 dakika olabilir `functionTimeout` içinde [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

Faturalama yürütme süresi ve kullanılan bellek temel alır ve bir işlev uygulaması içinde tüm işlevleri üzerinden toplanır. Daha fazla bilgi için bkz: Merhaba [Azure fiyatlandırma sayfası işlevleri].

Hello tüketim planı hello varsayılandır ve hello aşağıdaki avantajları sunar:
- Yalnızca işlevlerinizi çalışmadığı zaman ücret ödersiniz.
- Otomatik ölçeklendirme, bile yüksek dönemlerde yük.

## <a name="app-service-plan"></a>App Service planı

Merhaba uygulama hizmeti planı, temel, standart ve Premium SKU'ları benzer tooWeb uygulamalar üzerinde özel VM'ler işlevi uygulamalarınızı çalıştırın. Özel VM'ler ayrılmış tooyour App Service, hello işlevleri ana her zaman çalışan başka bir deyişle, uygulamalardır.

Aşağıdaki durumlarda hello uygulama hizmeti planında göz önünde bulundurun:
- Diğer uygulama hizmet örneği zaten çalıştıran var olan, az VM'ye sahip.
- Sürekli olarak veya sürekli olarak neredeyse işlevi uygulamaları toorun bekler.
- Merhaba tüketim plan üzerinde sağlanan değerinden daha fazla CPU veya bellek seçenekleri gerekir.
- Merhaba maksimum yürütme hello tüketim plan üzerinde izin verilen süreden daha uzun toorun gerekir.

Bir VM çalışma zamanı ve bellek boyutu maliyetinden ayrıştırır. Sonuç olarak, en fazla tahsis hello VM örneği hello maliyetini ücret ödersiniz olmaz. Merhaba hello uygulama hizmeti planı nasıl çalıştığı hakkında daha fazla bilgi için bkz [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Bir uygulama hizmeti planı ile elle çıkışı daha fazla VM örnekleri ekleyerek ölçeklendirebilirsiniz veya otomatik ölçeklendirme etkinleştirebilirsiniz. Daha fazla bilgi için bkz: [örnek sayısı el ile veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). Aynı zamanda farklı bir uygulama hizmeti planı seçerek ölçeği artırabilirsiniz. Daha fazla bilgi için bkz: [Azure bir uygulamada ölçeklendirin](../app-service-web/web-sites-scale.md). Bir uygulama hizmeti planı toorun JavaScript işlevleri planlıyorsanız, daha az çekirdeğe sahip bir plan seçmeniz gerekir. Daha fazla bilgi için bkz: Merhaba [işlevleri için JavaScript başvurusu](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
###Her zaman açık

Bir uygulama hizmeti planı çalıştırırsanız, hello etkinleştirmelisiniz **her zaman açık** işlevi uygulamanızın düzgün çalıştığını ayarını. Bir uygulama hizmeti planı yalnızca HTTP Tetikleyicileri "işlevlerinizi uyandırmak şekilde" Merhaba işlevleri çalışma zamanı boşta kalma birkaç dakika sonra geçer. Web işleri her zaman etkin olması gerekir benzer toohow budur. 

Her zaman açık yalnızca bir uygulama hizmeti planı üzerinde kullanılabilir. Tüketim plan üzerinde hello platform işlev uygulamalarının otomatik olarak etkinleştirir.

## <a name="storage-account-requirements"></a>Depolama hesabı gereksinimleri

Ya tüketimini planı ya da bir uygulama hizmeti planı, bir işlev uygulaması Azure Blob, kuyruk ve tablo depolama destekleyen bir Azure depolama hesabı gerektirir. Dahili olarak, Azure işlevleri Tetikleyicileri yönetme ve işlev yürütmeleri günlüğü gibi işlemler için Azure Storage kullanır. Bazı depolama hesapları, kuyruklar ve tablolar, yalnızca blob depolama hesapları (premium depolama dahil) ve bölge olarak yedekli depolama çoğaltma ile genel amaçlı depolama hesapları gibi desteklemez. Bu hesapları hello filtrelenir **depolama hesabı** bir işlev uygulaması oluştururken dikey.

Depolama hesabı türleri hakkında daha fazla toolearn bkz [hello Azure Storage hizmetlerine giriş](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-hello-consumption-plan-works"></a>Merhaba tüketim planı nasıl çalışır?

Merhaba tüketim planı hello işlevleri konak işlevleri üzerinde tetiklenen olayların hello sayısına dayalı olarak, ek örneklerini ekleyerek CPU ve bellek kaynakları otomatik olarak ölçeklendirir. Her hello işlevleri konak sınırlı too1.5 GB bellek örneğidir.

Kullandığınızda barındırma planı tüketim Merhaba, işlevi kod dosyaları hello ana depolama hesabındaki Azure dosya paylaşımları üzerinde depolanır. Merhaba ana depolama hesabını sildiğinizde, bu içeriği silinir ve kurtarılamaz.

> [!NOTE]
> Tüketim plan üzerinde bir blob tetikleyici kullanırken, olabilir tooa 10 dakikalık gecikme bir işlev uygulaması boşta geçti, yeni BLOB'lar işlenirken. Merhaba işlev uygulaması çalışmaya başladıktan sonra BLOB'ları hemen işlenir. Bu ilk tooavoid gecikme, aşağıdaki seçenekleri şu hello birini göz önünde bulundurun:
> - Always On özellikli ile bir uygulama hizmeti planını kullan.
> - Başka bir mekanizma tootrigger hello blob hello blob adı içeren bir kuyruk iletisi gibi işlemleri kullanın. Bir örnek için bkz: [sıra tetikleyicisi blob ile girişi bağlamayı](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Çalışma zamanı ölçeklendirme

Azure işlevlerini kullanan hello adlı bir bileşen *ölçek denetleyicisi* toomonitor hello olaylarının hızı ve belirlemek olup olmadığını tooscale out veya ölçeklendirmeyi azaltın. Merhaba ölçek denetleyicisi her tetikleyici türü için buluşsal yöntemler kullanır. Örneğin, bir Azure kuyruk depolama tetikleyicisi kullanırken hello sırası uzunluğu ve hello eski kuyruk iletisi hello yaşını göre ölçeklendirir.

Merhaba işlev uygulaması Hello ölçek birimidir. Merhaba işlev uygulaması çıkışı ölçeklenir, daha fazla kaynaklardır hello Azure işlevleri konak birden çok örneğini toorun ayrılmış. Buna karşılık, talep azalır işlem gibi hello ölçek denetleyicisi işlevi ana bilgisayar örneklerini kaldırır. bir işlev uygulaması içinde hiçbir işlevleri çalıştırırken hello örneklerinin sayısını toozero sonunda ölçeklendirilir.

![İzleme olayları ve örnekleri oluşturma ölçek denetleyicisi](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Faturalandırma modeli

Merhaba tüketim planı hello üzerinde ayrıntılı olarak açıklanmıştır faturalama [Azure fiyatlandırma sayfası işlevleri]. Kullanım hello işlevi uygulama düzeyinde toplanır ve işlev kodunu çalıştıran hello zaman sayar. Merhaba, faturalandırma için birimler şunlardır: 
* **Kaynak tüketimini gigabayt (GB-s) saniye**. Bellek boyutu ve bir işlev uygulaması içinde tüm işlevleri için yürütme süresi bileşimini olarak hesaplanır. 
* **Yürütmeleri**. Bir işlev bağlama tarafından tetiklenen yanıt tooan olay yürütülür her zaman sayılır.

[Azure fiyatlandırma sayfası işlevleri]: https://azure.microsoft.com/pricing/details/functions
