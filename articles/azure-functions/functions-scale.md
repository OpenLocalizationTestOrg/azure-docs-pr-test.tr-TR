---
title: "Azure işlevleri tüketim ve uygulama hizmeti planları | Microsoft Docs"
description: "Olay kaynaklı iş yüklerinizin gereksinimlerini karşılamak için nasıl Azure işlevleri ölçeklendirir anlayın."
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
ms.openlocfilehash: 70e77e09b2e2116153159167af61776398904a3c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Azure işlevleri tüketim ve uygulama hizmeti planları 

## <a name="introduction"></a>Giriş

Azure işlevlerinin iki farklı modda çalıştırabilirsiniz: Tüketim planı ve Azure uygulama hizmeti planı. Kodunuzu çalışıyorsa, çıkışı yükü işlemek için gerekli olan ölçeklendirir ve kod çalışmadığı zaman sonra ölçeklendirir tüketim planı otomatik olarak işlem gücü ayırır. Bu nedenle, boşta VM'ler için ödeme gerekmez ve yedek kapasite önceden gerekmez. Bu makalede tüketim plan üzerinde odaklanmıştır. Uygulama hizmeti planı nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Azure işlevleriyle alışık değilseniz, bkz: [Azure işlevlerine genel bakış](functions-overview.md).

Bir işlev uygulaması oluşturduğunuzda, uygulamayı içeren işlevleri için bir barındırma planı yapılandırmanız gerekir. Her iki modda örneği *Azure işlevleri konak* işlevleri yürütür. Plan denetimleri türü:

* Nasıl konak örnekleri çıkışı ölçeklenir.
* Her ana bilgisayara kullanılabilir kaynaklar.

Şu anda, işlev uygulaması oluşturma sırasında planı türü seçmelisiniz. Daha sonra değiştiremezsiniz. 

Uygulama hizmeti planında katmanları arasında ölçeklendirebilirsiniz. Tüketim plan üzerinde Azure işlevleri, tüm kaynak ayırma otomatik olarak yönetir.

## <a name="consumption-plan"></a>Tüketim planı

Tüketim planı kullanırken, Azure işlevleri konak örnekleri dinamik olarak eklenir ve gelen olayların sayısına göre kaldırıldı. Bu plan otomatik olarak ölçeklendirir ve yalnızca işlevlerinizi çalıştırırken işlem kaynakları için ücretlendirilirsiniz. Tüketim plan üzerinde bir işlev en fazla 10 dakika için çalıştırabilirsiniz. 

> [!NOTE]
> Tüketim planı işlevleri için varsayılan zaman aşımı 5 dakikadır. Değer 10 dakika için işlev uygulaması özelliğini değiştirerek artırılabilir `functionTimeout` içinde [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

Faturalama yürütme süresi ve kullanılan bellek temel alır ve bir işlev uygulaması içinde tüm işlevleri üzerinden toplanır. Daha fazla bilgi için bkz: [Azure fiyatlandırma sayfası işlevleri].

Tüketim planı varsayılandır ve aşağıdaki avantajları sunar:
- Yalnızca işlevlerinizi çalışmadığı zaman ücret ödersiniz.
- Otomatik ölçeklendirme, bile yüksek dönemlerde yük.

## <a name="app-service-plan"></a>App Service planı

Uygulama hizmeti planında işlevi uygulamalarınızı özel VM'ler temel, standart ve Premium SKU'ları, Web uygulamaları için benzer üzerinde çalıştırın. Ayrılmış sanal işlevleri ana her zaman çalışan anlamına gelir, uygulama hizmeti uygulamalarınız için ayrılır.

Aşağıdaki durumlarda bir uygulama hizmeti planı göz önünde bulundurun:
- Diğer uygulama hizmet örneği zaten çalıştıran var olan, az VM'ye sahip.
- Sürekli veya neredeyse sürekli olarak çalıştırmak için işlevi uygulamalarınızı bekler.
- Tüketim plan üzerinde sağlanan değerinden daha fazla CPU veya bellek seçenekleri gerekir.
- Tüketim plan üzerinde izin verilen en fazla yürütme süresini daha uzun çalıştırmanız gerekir.

Bir VM çalışma zamanı ve bellek boyutu maliyetinden ayrıştırır. Sonuç olarak, en fazla tahsis VM örneği maliyetini ücret ödersiniz olmaz. Uygulama hizmeti planı nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Bir uygulama hizmeti planı ile elle çıkışı daha fazla VM örnekleri ekleyerek ölçeklendirebilirsiniz veya otomatik ölçeklendirme etkinleştirebilirsiniz. Daha fazla bilgi için bkz: [örnek sayısı el ile veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). Aynı zamanda farklı bir uygulama hizmeti planı seçerek ölçeği artırabilirsiniz. Daha fazla bilgi için bkz: [Azure bir uygulamada ölçeklendirin](../app-service-web/web-sites-scale.md). Bir uygulama hizmeti planı JavaScript işlevleri çalıştırmayı planlıyorsanız, daha az çekirdeğe sahip bir plan seçmeniz gerekir. Daha fazla bilgi için bkz: [işlevleri için JavaScript başvurusu](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: the portal links to this section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
###Her zaman açık

Bir uygulama hizmeti planı çalıştırırsanız, etkinleştirmelisiniz **her zaman açık** işlevi uygulamanızın düzgün çalıştığını ayarını. Bir uygulama hizmeti planı yalnızca HTTP Tetikleyicileri "işlevlerinizi uyandırmak şekilde" işlevleri çalışma zamanı boşta kalma birkaç dakika sonra geçer. Bu, nasıl Web işleri her zaman etkin olması gerekir için benzer. 

Her zaman açık yalnızca bir uygulama hizmeti planı üzerinde kullanılabilir. Tüketim plan üzerinde platform işlev uygulamalarının otomatik olarak etkinleştirir.

## <a name="storage-account-requirements"></a>Depolama hesabı gereksinimleri

Ya tüketimini planı ya da bir uygulama hizmeti planı, bir işlev uygulaması Azure Blob, kuyruk ve tablo depolama destekleyen bir Azure depolama hesabı gerektirir. Dahili olarak, Azure işlevleri Tetikleyicileri yönetme ve işlev yürütmeleri günlüğü gibi işlemler için Azure Storage kullanır. Bazı depolama hesapları, kuyruklar ve tablolar, yalnızca blob depolama hesapları (premium depolama dahil) ve bölge olarak yedekli depolama çoğaltma ile genel amaçlı depolama hesapları gibi desteklemez. Bu hesapları filtre **depolama hesabı** bir işlev uygulaması oluştururken dikey.

Depolama hesabı türleri hakkında daha fazla bilgi için bkz: [Azure Storage hizmetlerine giriş](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-the-consumption-plan-works"></a>Tüketim planı nasıl çalışır?

Tüketim planı işlevleri üzerinde tetiklenen olayların sayısına dayalı işlevler konak ek örneklerini ekleyerek CPU ve bellek kaynakları otomatik olarak ölçeklendirir. İşlevler konak her örneği için 1,5 GB bellek sınırlıdır.

Barındırma planı tüketimini kullandığınızda işlevi kod dosyaları Azure dosya paylaşımlarının ana depolama hesabında depolanır. Ana depolama hesabı sildiğinizde, bu içeriği silinir ve kurtarılamaz.

> [!NOTE]
> Tüketim plan üzerinde bir blob tetikleyici kullanırken olabilir en fazla 10 dakikalık bir gecikmeyle bir işlev uygulaması boşta geçti, yeni BLOB'lar işleme. İşlev uygulaması çalışmaya başladıktan sonra BLOB'ları hemen işlenir. Bu ilk gecikmeyi önlemek için aşağıdaki seçeneklerden birini göz önünde bulundurun:
> - Always On özellikli ile bir uygulama hizmeti planını kullan.
> - Başka bir mekanizma, blob adı içeren bir kuyruk iletisi gibi işleme blob tetiklemek için kullanın. Bir örnek için bkz: [sıra tetikleyicisi blob ile girişi bağlamayı](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Çalışma zamanı ölçeklendirme

Azure işlevlerini kullanan adlı bir bileşen *ölçek denetleyicisi* olaylarının hızı izlemek ve ölçeğini veya ölçeklendirmeyi azaltın belirlemek için. Ölçek denetleyicisi her tetikleyici türü için buluşsal yöntemler kullanır. Örneğin, bir Azure kuyruk depolama tetikleyicisi kullanırken, kuyruk uzunluğu ve eski kuyruk iletisini yaşını göre ölçeklendirir.

İşlev uygulaması ölçek birimidir. İşlev uygulaması çıkışı ölçeklenir, daha fazla kaynak Azure işlevleri ana bilgisayarın birden çok örneği çalıştırmak için ayrılır. Buna karşılık, talep azalır işlem gibi ölçek denetleyicisi işlevi ana bilgisayar örneklerini kaldırır. Bir işlev uygulaması içinde hiçbir işlevleri çalıştırırken örneklerinin sayısını sonunda sıfır olarak ölçeklendirilir.

![İzleme olayları ve örnekleri oluşturma ölçek denetleyicisi](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Faturalandırma modeli

Tüketim plan üzerinde ayrıntılı olarak açıklanmıştır faturalama [Azure fiyatlandırma sayfası işlevleri]. Kullanım işlevi uygulama düzeyinde toplanır ve işlev kodu çalıştığı zaman sayar. Faturalama birimleri şunlardır: 
* **Kaynak tüketimini gigabayt (GB-s) saniye**. Bellek boyutu ve bir işlev uygulaması içinde tüm işlevleri için yürütme süresi bileşimini olarak hesaplanır. 
* **Yürütmeleri**. Bir işlev bağlama tarafından tetiklenen bir olaya yanıt olarak yürütülen her zaman sayılır.

[Azure fiyatlandırma sayfası işlevleri]: https://azure.microsoft.com/pricing/details/functions
