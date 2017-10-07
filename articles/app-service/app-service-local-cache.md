---
title: "aaaAzure uygulama hizmeti yerel önbelleğinden genel bakış | Microsoft Docs"
description: "Bu makalede nasıl tooenable, yeniden boyutlandırma ve sorgu hello Azure uygulama hizmeti yerel önbelleğinden özelliği durumunu hello açıklanır"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Azure uygulama hizmeti yerel önbelleğinden genel bakış
Azure web uygulaması içerik Azure depolama alanında depolanır ve yukarı içerik paylaşımı sağlam bir şekilde ortaya. Bu tasarım çeşitli uygulamaları ile hedeflenen toowork olup öznitelikleri aşağıdaki hello içerir:  

* Merhaba içeriği birden çok sanal makine (VM) örneği hello web uygulaması arasında paylaşılır.
* Merhaba içerik dayanıklı ve web uygulamaları çalıştırılarak değiştirilebilir.
* Günlük dosyaları ve tanılama veri dosyalarını hello altında kullanılabilir aynı paylaşılan içerik klasörü.
* İçerik klasörünü güncelleştirmeleri hello doğrudan yeni içerik yayımlama. Hemen aynı hello SCM Web sitesi aracılığıyla içerik ve (genellikle ASP.NET gibi bazı teknolojiler bazı dosya değişiklikleri tooget hello son içerik üzerinde web uygulaması yeniden başlatma) çalışan web uygulaması hello görünüm hello kullanabilirsiniz.

Birçok web uygulamaları bir ya da bu özelliklerin tümü, kullansa da, bazı web uygulamaları, yüksek kullanılabilirlik ile çalıştırabilirsiniz bir yüksek performanslı, salt okunur içerik deposu yeterlidir. Bu uygulamalar, belirli bir yerel önbelleği VM örneğinden yararlı olabilir.

Hello Azure uygulama hizmeti yerel önbelleğinden özelliği içeriğinizi web rolü görünümünü sağlar. Bu içerik, site başlangıçta zaman uyumsuz olarak oluşturulan depolama içeriğinizi yazma ancak atma önbelleğidir. Merhaba önbelleği hazır olduğunda, hello hello önbelleğe alınmış içeriği karşı anahtarlı toorun sitedir. Yerel önbelleğine çalışan web uygulamalarını hello aşağıdaki faydaları vardır:

* Azure Storage içeriğine eriştiğinde oluşan bilmez toolatencies oldukları.
* Planlanan bilmez toohello yükseltmeleri veya Planlanmamış kapalı kalma süreleri ve Azure Storage ile Merhaba içerik Paylaşımı hizmet sunucularda ortaya diğer kesintilere oldukları.
* Toostorage paylaşımı değişiklikleri nedeniyle daha az uygulama yeniden başlatma sahiptirler.

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>Nasıl yerel önbelleği uygulama hizmeti hello davranışını değiştirir
* Hello yerel önbelleği hello /site ve /siteextensions klasörleri hello web uygulamasının bir kopyasıdır. Web uygulaması başlangıç hello yerel VM örneğindeki oluşturulur. Merhaba web uygulaması başına hello yerel önbellek boyutunu sınırlıdır too300 MB varsayılan, ancak bunu too2 GB artırabilirsiniz.
* Merhaba yerel önbellek okuma-yazma. Ancak, başlangıç web uygulaması sanal makineleri taşıdığında veya yeniden değişiklikler atılacak. Merhaba içerik deposunda kritik verileri depolayan uygulamalar için yerel önbelleği kullanmamanız gerekir.
* Şu anda yaptıkları gibi web uygulamaları toowrite günlük dosyaları ve tanılama veri devam edebilirsiniz. Günlük dosyaları ve verileri, ancak yerel olarak hello VM üzerinde depolanır. Düzenli aralıklarla toohello paylaşılan içerik deposu sonra kopyalanırlar. Merhaba kopyalama toohello paylaşılan içerik deposu olduğu iyi çaba--yazma geri tooa VM örneğinin ani kilitlenme kaybolmuş olabilir.
* Merhaba LogFiles ve veri klasörlerin yerel önbelleği kullanan web uygulamaları için başlangıç klasörü yapısı içinde bir değişiklik yoktur. Merhaba adlandırma deseni "benzersiz tanımlayıcı" + zaman damgası izleyen hello depolama LogFiles ve veri klasörleri şimdi alt klasörler var. Her hello klasörlerinin burada hello web uygulaması çalıştıran veya çalıştırıldı tooa VM örneğine karşılık gelir.  
* Yayımlama değişiklikleri toohello web uygulaması yayımlama hello mekanizmaları kanalıyla toohello paylaşılan içerik deposu yayımlar. İçerik toobe dayanıklı hello yayımlanan istiyoruz tasarım gereği olmasıdır. Merhaba web uygulamasının toorefresh hello yerel önbellek, yeniden toobe gerekir. Bu bir aşırı adım gibi görünüyor? toomake hello yaşam döngüsü sorunsuz, bu makalenin sonraki bölümlerinde hello bilgileri görürsünüz.
* D:\Home toohello yerel önbelleği işaret. D:\Local toohello geçici VM belirli depolama işaret eden devam eder.
* Merhaba varsayılan içerik görünümü hello SCM site paylaşılan içerik deposu, hello toobe devam eder.

## <a name="enable-local-cache-in-app-service"></a>Uygulama hizmeti yerel önbellekteki etkinleştir
Yerel önbelleği ayrılmış uygulama ayarları bir bileşimini kullanarak yapılandırın. Yöntemler aşağıdaki hello kullanarak bu uygulama ayarları yapılandırabilirsiniz:

* [Azure portal](#Configure-Local-Cache-Portal)
* [Azure Resource Manager](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak yerel önbelleği yapılandırma
<a name="Configure-Local-Cache-Portal"></a>

Bu uygulama ayarını kullanarak bir web-uygulama başına temelinde yerel önbelleği etkinleştir:`WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Azure portal uygulaması ayarları: yerel önbelleği](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>Azure Kaynak Yöneticisi'ni kullanarak yerel önbelleği yapılandırma
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>Yerel önbellekteki Hello boyutu ayarını değiştirme
Varsayılan olarak, hello yerel önbellek boyutu olan **300 MB**. Öğesinden kopyalanan /siteextensions klasörleri içerik deposu yanı sıra tüm günlükleri ve veri klasörleri yerel olarak oluşturulan hello ve bu hello /site içerir. tooincrease bu sınırlama, hello uygulama ayarı kullanmak `WEBSITE_LOCAL_CACHE_SIZEINMB`. Merhaba boyutunu artırabilir çok yukarı**2 GB** (2000 MB) web uygulaması başına.

## <a name="best-practices-for-using-app-service-local-cache"></a>Uygulama hizmeti yerel önbelleğinden kullanmak için en iyi uygulamalar
Merhaba birlikte yerel önbelleği kullanmanızı öneririz [hazırlama ortamlarını](../app-service-web/web-sites-staged-publishing.md) özelliği.

* Merhaba eklemek *Yapışkan* uygulama ayarı `WEBSITE_LOCAL_CACHE_OPTION` hello değerle `Always` tooyour **üretim** yuvası. Kullanıyorsanız, `WEBSITE_LOCAL_CACHE_SIZEINMB`, ayrıca bir Yapışkan ayarı tooyour üretim yuvasına ekleyin.
* Oluşturma bir **hazırlama** yuva ve tooyour hazırlama yuvası yayımlayın. Tipik olarak yuva toouse yerel önbelleği tooenable hello üretim yuvası için yerel önbelleği hello yararları alırsanız hazırlama için sorunsuz bir derleme, dağıtma, test ömrü hazırlama hello ayarlamanız gerekmez.
* Sitenizi hazırlama yuvası karşı test edin.  
* Hazır olduğunuzda, sorun bir [takas işlemi](../app-service-web/web-sites-staged-publishing.md#Swap) arasında hazırlama ve üretim yuvalarını.  
* Ad ve Yapışkan tooa yuvası Yapışkan ayarları içerir. Bu nedenle üretime Hello hazırlama yuvası takas, hello yerel önbellek uygulama ayarlarını devralır. Merhaba, yeni yuva hello yerel önbelleğe karşı birkaç dakika sonra çalışacak ve yuva Isınma bir parçası olarak değiştirme işleminden sonra warmed üretim takas. Merhaba yuva değiştirmenin tamamlandığında, bu nedenle, üretim yuvası hello yerel önbelleğe karşı çalıştırırsınız.

## <a name="frequently-asked-questions-faq"></a>Sık sorulan sorular (SSS)
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>Yerel önbelleği toomy web uygulaması geçerli olup olmadığını nasıl anlayabilirim?
Web uygulamanızı yüksek performanslı, güvenilir bir içerik deposu gerekir, hello içerik deposu toowrite kritik verilerin çalışma zamanında kullanmaz ve toplam boyutu 2 GB'tan daha az ise, hello yanıt "Evet" değil! /site ve /siteextensions klasörlerinizi tooget hello toplam boyutu, hello site uzantısı "Azure Web Apps Disk kullanımı" kullanabilirsiniz.  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>Sitem bir toousing yerel önbelleği geçirdi nasıl anlayabilirim?
Hazırlama ortamlarını ile Merhaba yerel önbelleği özelliğini kullanıyorsanız hello değiştirme işlemi yerel önbelleği warmed tamamlanmayacak. siteniz yerel önbelleğe karşı çalışıyorsa toocheck hello çalışan işlem ortam değişkeni kontrol edebilirsiniz `WEBSITE_LOCALCACHE_READY`. Merhaba üzerinde Hello yönergeleri kullanın [çalışan işlem ortam değişkeni](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) sayfa tooaccess hello birden çok örneği üzerinde çalışan işlem ortam değişkeni.  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>Henüz yeni değişiklikleri yayımladığınız, ancak web Uygulamam toohave görünmüyor bunları. Neden?
Daha sonra web uygulamanızı yerel önbelleği kullanıyorsa, site tooget hello en son değişiklikleri toorestart gerekir. Toopublish değişiklikleri tooa üretim sitesini istiyor mu? Merhaba yuvası seçenekleri hello önceki bölümdeki en iyi yöntemler konusuna bakın.

### <a name="where-are-my-logs"></a>My günlükleri nerede?
Yerel önbelleği ile günlükleri ve veri klasörleri biraz farklı görünüyor. Ancak, Merhaba, alt klasörler kalır yapısını aynı Merhaba, hello alt hello bir alt klasörü altında nestled dışında biçimlendirmek "VM tanımlayıcısı" + zaman damgası.

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>Yerel önbellek etkin olan, ancak web Uygulamam yeniden. Bunun nedeni nedir? I sık sık uygulama yeniden başlatma ile yerel önbelleği Yardım zorlayıcı.
Yerel önbelleği depolama ile ilgili web uygulaması yeniden önlemeye yardımcı olur. Ancak, web uygulamanızı yeniden başlatmalar hello VM planlanmış altyapısını yükseltmeler sırasında uygulanabilecek hala. Merhaba yerel önbelleği etkin deneyimi genel uygulama yeniden başlatılmadan daha az olmalıdır.

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>Yerel önbelleği herhangi hariç mu engeller dizinleri toohello daha hızlı yerel diske kopyalanır?
Merhaba depolama içeriği kopyalar hello adımının bir parçası depo adlı herhangi bir klasör edilmeyecek. Bu site içeriğiniz gün tooday işleminde hello web uygulamasının ihtiyaç olmayan bir kaynak denetimi deponuza burada içerebilir senaryolarında yardımcı olur. 
