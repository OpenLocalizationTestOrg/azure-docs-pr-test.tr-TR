---
title: "bir Azure Otomasyonu Runbook'tan bir günlük analizi uyarısı aaaCalling | Microsoft Docs"
description: "Bu makalede hakkında genel bakış sağlanmaktadır tooinvoke bir Otomasyon runbook'u Microsoft OMS günlük analizi uyarıdan."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a>Bir OMS Log Analytics uyarısından Azure Otomasyonu runbook’u çağırma

Bir uyarı günlük analizi toocreate yapılandırıldığında sonuçları işlemci kullanımı ya da bir iş uygulaması belirli bir uygulama işlemi kritik toohello işlevselliğini uzun süren bir ani gibi bir belirli ölçütlere uyan varsa bir uyarı kaydı başarısız ve bu uyarı bir Otomasyon runbook'u bir girişim tooauto çalışma otomatik olarak ilgili bir olayın hello Windows olay günlüğüne yazar-hello sorunu düzeltin.  

İki seçenek toocall bir runbook hello uyarı yapılandırma, vardır.  Daha ayrıntılı belirtmek gerekirse:

1. Web kancası kullanma.
   * OMS çalışma alanınızı bağlantılı tooan Otomasyon hesabı değilse hello kullanılabilir tek seçenek budur.
   * Bir Otomasyon hesabı bağlı tooan OMS çalışma zaten varsa, bu seçenek kullanılabilir durumda kalır.  

2. Doğrudan bir runbook seçme.
   * Bu seçenek, yalnızca hello OMS çalışma bağlantılı tooan Otomasyon hesabı olduğunda kullanılabilir.  

## <a name="calling-a-runbook-using-a-webhook"></a>Web kancası kullanarak bir runbook çağırma

Bir Web kancası toostart belirli bir runbook tek bir HTTP isteği aracılığıyla Azure Otomasyonu'nda sağlar.  Merhaba yapılandırmadan önce [günlük analizi uyarı](../log-analytics/log-analytics-alerts.md#alert-rules) toocall hello runbook bir uyarı eylem, bir Web kancası kullanarak ihtiyacınız olacak toofirst bu yöntemi kullanarak çağrılacağı hello runbook için bir Web kancası oluşturun.  Gözden geçirin ve hello hello adımları [bir Web kancası oluşturma](automation-webhooks.md#creating-a-webhook) makalesi ve hello uyarı kuralı yapılandırılırken başvurabilmek toorecord hello Web kancası URL'si unutmayın.   

## <a name="calling-a-runbook-directly"></a>Doğrudan bir runbook çağırma

Merhaba Otomasyon sahip & Denetim sunumu yüklü ve hello Runbook eylemleri seçeneği hello uyarı için yapılandırırken, OMS çalışma yapılandırılmış varsa, tüm runbook'lardan hello görüntüleyebilirsiniz **bir runbook seçin** aşağı açılan liste ve yanıt toohello uyarısında toorun istediğiniz hello belirli runbook'u seçin.  Seçili hello runbook hello Azure Bulut veya karma runbook çalışanı bir çalışma alanında çalışabilir.  Hello uyarı oluşturulduğunda hello runbook seçeneği kullanılarak, bir Web kancası hello runbook için oluşturulur.  Toohello Otomasyon hesabı gidin ve seçilen hello runbook'un toohello Web kancası dikey gidin hello Web kancası görebilirsiniz.  Merhaba uyarı silerseniz, hello Web kancası silinmez, ancak hello kullanıcı hello Web kancası el ile silebilirsiniz.  Merhaba Web kancası silinmez, onu bir sorun değildir, yalnızca bir toobe sonunda gerekir yalnız bırakılmış öğesi sipariş toomaintain düzenli bir Otomasyon hesabı silindi.  

## <a name="characteristics-of-a-runbook-for-both-options"></a>Bir runbook’un özellikleri (her iki seçenek için)

Merhaba günlük analizi uyarıdan hello runbook'u çağırmak için iki yöntem uyarı kurallarını yapılandırmadan önce anladım toobe gereken farklı bir davranış özelliklerine sahiptir.  

* **Object** türünde **WebhookData** adlı bir runbook girdi parametreniz olmalıdır.  Zorunlu veya isteğe bağlı olabilir.  Bu giriş parametresinin kullanarak hello arama sonuçları toohello runbook'u Hello uyarı geçirir.

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  Kod tooconvert hello WebhookData tooa PowerShell nesnesi olması gerekir.

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    *$SearchResults* nesnelerinin bir dizisi olacaktır; her nesne bir arama sonucu değerlerle hello alanları içerir

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a>Merhaba Web kancası seçeneği ve runbook seçeneği arasındaki WebhookData tutarsızlıklar

* Bir uyarı toocall bir Web kancası yapılandırırken, bir runbook için oluşturduğunuz Web kancası URL'si girin ve hello tıklayın **Test Web kancası** düğmesi.  Merhaba elde edilen WebhookData toohello runbook ya da içermiyor gönderilen *. SearchResult* veya *. SearchResults*.

*  Merhaba uyarı tetikler ve hello Web kancası çağırır olduğunda bu uyarı kaydederseniz, WebhookData gönderilen toohello runbook hello içeren *. SearchResult*.
* Bir uyarı oluşturmak ve toocall (aynı zamanda bir Web kancası oluşturur) bir runbook yapılandırmak, ne zaman uyarı tetikleyicileri, gönderdiği içeren WebhookData toohello runbook hello *. SearchResults*.

Bu nedenle hello kodu yukarıdaki örnekte, tooget ihtiyacınız olacak *. SearchResult* hello uyarı bir Web kancası çağırır ve tooget gerekir *. SearchResults* hello uyarı bir runbook doğrudan çağırırsa.

## <a name="example-walkthrough"></a>Örnek kılavuz

Biz bu bir Windows hizmetini başlatır örnek grafik runbook aşağıdaki hello kullanarak nasıl çalıştığı gösterilmektedir.<br><br> ![Windows Hizmeti Grafiksel Runbook’unu Başlatma](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

Merhaba runbook'da türünde bir giriş parametresi **nesne** çağrılan **WebhookData** ve uyarı hello içeren geçirilen hello Web kancası veriler içeriyorsa *. SearchResults*.<br><br> ![Runbook girdi parametreleri](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)<br>

Bu örnek için günlük analizi iki özel alanlar, oluşturduğumuz *SvcDisplayName_CF* ve *SvcState_CF*, tooextract hello hizmet görünen adı ve hello hello hizmetin durumunu (yani çalışıyor veya durdurulmuştur) Merhaba olayından toohello sistem olay günlüğüne yazılır.  Daha sonra bir uyarı kuralı ile arama sorgusu aşağıdaki hello oluşturuyoruz: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` hello Windows sistem üzerinde hello Yazdırma Biriktiricisi hizmeti durdurulduğunda biz algılayabilmesi.  İlgilendiğiniz herhangi bir hizmeti olabilir, ancak bu örnek için biz Windows işletim sistemi hello ile birlikte hello önceden varolan hizmetlerden biri başvuruda bulunuyor.  Merhaba uyarı eylemi yapılandırılmış tooexecute Bu örnekte kullanılan runbook uygulamamız ve hello hedef sistemlerde etkinleştirildiği hello karma Runbook çalışanı üzerinde çalıştırın.   

Merhaba runbook kodunu aktivite **hizmet adından alma LA** hello JSON biçimli dize bir nesne türü ve filtre hello öğesinin içine dönüştürecek *SvcDisplayName_CF* hello tooextract hello görünen adı Windows hizmet ve bunu hangi hello hizmet toorestart denemeden önce durduruldu doğrular hello sonraki etkinliği üzerine geçirmek.  *SvcDisplayName_CF* olan bir [özel alan](../log-analytics/log-analytics-custom-fields.md) Bu örnek günlük analizi toodemonstrate oluşturulmuş.

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

Hello hizmet durduğunda, günlük analizi hello uyarı kuralında bir eşleşme algılar hello runbook tetiklenemedi ve hello uyarı bağlamı toohello runbook gönderin. Merhaba runbook eylemini alır ve bu nedenle girişimi toorestart hello hizmeti doğrulamak, kullanmaya doğru ve çıktı hello sonuçları tooverify hello hizmet durduruldu.     

Alternatif olarak Otomasyon hesabı bağlı tooyour OMS çalışma alanınız yoksa, bir Web kancası eylem tootrigger hello runbook'la hello uyarı kuralı yapılandırmak ve hello runbook tooconvert hello JSON biçimli dize ve filtresiniyapılandırmak*. SearchResult* daha önce bahsedilen hello yönergeleri izleyerek.    

## <a name="next-steps"></a>Sonraki adımlar

* Günlük analizi uyarılar hakkında daha fazla toolearn ve nasıl toocreate, bkz: [günlük analizi uyarılarını](../log-analytics/log-analytics-alerts.md).

* bir Web kancası kullanarak tootrigger runbook'ları nasıl görürüm toounderstand [Azure Otomasyonu Web kancası](automation-webhooks.md).
