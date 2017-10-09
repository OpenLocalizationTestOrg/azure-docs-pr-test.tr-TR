---
title: "OMS günlük analizi aaaCreating uyarılar | Microsoft Docs"
description: "Günlük analizi uyarılarını OMS deponuzun önemli bilgileri tanımlamak ve önceden sorunları size bildiren veya Eylemler tooattempt toocorrect çağırma bunları.  Bu makalede nasıl toocreate bir uyarı kuralı ve ayrıntıları hello farklı eylemlerini yapabilecekleri açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a>Günlük analizi uyarı kurallarında ile çalışma
Uyarılar, günlük aramaları düzenli aralıklarla otomatik olarak çalışacak uyarı kuralları tarafından oluşturulur.  Merhaba sonuçları belirli ölçütlere uyan varsa bunlar bir uyarı kaydı oluşturun.  Merhaba kuralı daha sonra otomatik olarak bir çalıştırabilirsiniz veya daha fazla Eylemler tooproactively hello uyarı bildiren veya başka bir işlem çağırma.   

Bu makalede hello işlemleri toocreate ve hello OMS portalı kullanarak uyarı kuralları düzenleyin.  Merhaba farklı ayarlar ve nasıl tooimplement mantığı gerekli hakkında daha fazla ayrıntı için bkz: [günlük analizi anlama uyarıları](log-analytics-alerts.md).

>[!NOTE]
> Şu anda oluşturamaz veya hello Azure portal kullanarak bir uyarı kuralı değiştirin. 

## <a name="create-an-alert-rule"></a>Bir uyarı kuralı oluştur

bir günlük oluşturarak başlayın Hello OMS portalı kullanarak bir uyarı kuralı toocreate hello uyarı çağıracağı hello kayıtlarını arayın.  Merhaba **uyarı** düğmesini sonra kullanılabilir olacak oluşturmak ve hello uyarı kuralı yapılandırmak için.

>[!NOTE]
> En fazla 250 uyarı kuralları şu anda bir OMS çalışma alanında oluşturulabilir. 

1. Merhaba OMS genel bakış sayfasında, **günlük arama**.
2. Yeni bir günlük arama sorgusu oluşturun ya da kaydedilmiş günlük Ara'yı seçin. 
3. Tıklatın **uyarı** hello sayfa tooopen hello hello üstündeki **uyarı kuralı Ekle** ekran.
4. Merhaba uyarı kuralı bilgileri kullanarak yapılandırma [uyarı kuralları ayrıntılarını](#details-of-alert-rules) aşağıda.
6. Tıklatın **kaydetmek** toocomplete hello uyarı kuralı.  Çalıştırdıktan hemen başlar.


## <a name="edit-an-alert-rule"></a>Bir uyarı kuralını Düzenle
Tüm uyarı kuralları listesi hello alabilirsiniz **uyarıları** günlük analizi menüde **ayarları**.  

![Uyarıları yönetme](./media/log-analytics-alerts/configure.png)

1. Merhaba OMS konsol select hello içinde **ayarları** döşeme.
2. Seçin **uyarıları**.

Bu görünümden birden çok eylemleri gerçekleştirebilirsiniz.

* Bir kural seçerek devre dışı **kapalı** sonraki tooit.
* Bir uyarı kuralı hello Kurşun Kalem simgesini sonraki tooit tıklayarak düzenleyin.
* Bir uyarı kuralı hello tıklatarak kaldırın **X** simgesi sonraki tooit. 

## <a name="details-of-alert-rules"></a>Uyarı kurallarının ayrıntıları
Oluşturduğunuzda veya bir uyarı kuralı hello OMS portalında Düzenle hello ile çalışma **uyarı kuralı Ekle** veya **uyarı kuralını Düzenle** sayfası.  tabloları aşağıdaki hello bu ekran hello alanları tanımlayın.

![Uyarı kuralı](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a>Uyarı bilgileri
Bunlar hello uyarı kuralı ve oluşturduğu hello uyarılar için temel ayarlarıdır.

| Özellik | Açıklama |
|:--- |:---|
| Ad | Benzersiz adı tooidentify hello uyarı kuralı. Bu ad hello kural tarafından oluşturulan uyarıların herhangi birisi dahil edilir.  |
| Açıklama | Merhaba uyarı kuralı isteğe bağlı bir açıklama. |
| Önem Derecesi |Bu kural tarafından oluşturulan uyarı önem derecesi. |

### <a name="search-query-and-time-window"></a>Arama sorgu ve zaman penceresi
Merhaba arama sorgu ve zaman penceresi, herhangi bir uyarı oluşturduysanız, değerlendirilen toodetermine hello kayıtları döndürür.

| Özellik | Açıklama |
|:--- |:---|
| Arama sorgusu | Çalıştırılacak hello sorgu budur.  bir uyarı oluşturulup oluşturulmadığını bu sorgu tarafından döndürülen hello kayıtları kullanılan toodetermine olacaktır.<br><br>Seçin **kullanım geçerli arama sorgusunu** toouse hello geçerli sorgu veya varolan kaydedilmiş aramayı hello listeden seçin.  Merhaba sorgu sözdizimi hello metin kutusuna, gerekirse değiştirebileceğiniz sağlanır. |
| Zaman penceresi |Merhaba sorgu Hello zaman aralığını belirtir.  Merhaba sorgu bu hello aralığında geçerli saati oluşturulan kayıtları döndürür.  Bu, 5 dakika ile 24 saat arasında herhangi bir değer olabilir.  Büyük veya ona eşit toohello uyarı sıklığı olmalıdır.  <br><br> Örneğin, Hello zaman penceresi too60 dakika ve hello sorgu ayarlanmış 13: 15'te çalıştırılırsa, yalnızca saat 12: 15'e ve 13: 15'te arasında oluşturulan kayıtları döndürülür. |

Merhaba zaman penceresi için uyarı kuralı hello sağladığınızda, o zaman penceresi için hello arama ölçütleriyle eşleşen mevcut kayıtları hello sayısı görüntülenir.  Bu size verecektir hello sıklığı belirlemenize yardımcı olabilir hello beklediğiniz sonuç sayısı.

### <a name="schedule"></a>Zamanlama
Ne sıklıkta hello arama sorgusu çalıştırılan tanımlar.

| Özellik | Açıklama |
|:--- |:---|
| Uyarı sıklığı | Ne sıklıkta hello sorgu çalıştırılması gerektiğini belirtir. 5 dakika ile 24 saat arasında herhangi bir değer olabilir. Merhaba zaman penceresi'den küçük eşit tooor olmalıdır.  Merhaba değeri hello zaman penceresi'den büyükse, eksik kayıtları riski oluşur.<br><br>Örneğin, 30 dakikalık bir zaman penceresi ve 60 dakika sıklığını göz önünde bulundurun.  Merhaba sorgu 1: 00'dan çalıştırırsanız, 12:30 ve 1:00 arasında kayıt döndürür.  Merhaba hello sorguyu çalıştırabilir sonraki 2:00 kayıtlar 1:30 ve 2:00 arasında ne zaman döndürecektir saattir.  1:00-1:30 arasında oluşturulan kayıtları hiçbir zaman değerlendirilmesi. |


### <a name="generate-alert-based-on"></a>Temel uyarı oluştur
Hello hello arama sorgusu toodetermine bir uyarı durumunda hello sonuçlarını karşı değerlendirilecek ölçütleri oluşturulması gerektiğini tanımlar.  Bu ayrıntılar seçtiğiniz uyarı kuralı hello türüne bağlı olarak farklı olacaktır.  Farklı uyarı kuralı türlerinden Merhaba ayrıntılarını alabilirsiniz [günlük analizi anlama uyarıları](log-analytics-alerts.md).

| Özellik | Açıklama |
|:--- |:---|
| Uyarıları bastırma | Gizleme hello uyarı kuralı için etkinleştirdiğinizde, Eylemler hello kuralı için yeni bir uyarı oluşturduktan sonra tanımlı bir süre için devre dışı bırakılır. Merhaba kuralı hala çalışıyor ve hello ölçütü karşılanırsa uyarı kayıtları oluşturursunuz. Yinelenen eylemler çalıştırmadan toocorrect hello sorunu zaman tooallow budur. |

#### <a name="number-of-results-alert-rules"></a>Sonuçları uyarı kuralları sayısı

| Özellik | Açıklama |
|:--- |:---|
| Sonuç sayısı |Merhaba hello sorgu tarafından döndürülen kayıt sayısını ya da ise bir uyarı oluşturulur **büyük** veya **değerinden** hello sağladığınız değeri.  |

#### <a name="metric-measurement-alert-rules"></a>Ölçüm ölçüm uyarı kuralları

| Özellik | Açıklama |
|:--- |:---|
| Toplam değeri | Hello sonuçlarında birleşik her değer toobe aşması gereken Eşiği değeri bir ihlal olarak kabul. |
| Dayalı tetikleyici Uyarısı | oluşturulan bir uyarı toobe ihlallerini Hello sayısı.  Belirtebilirsiniz **toplam ihlal** ihlallerini hello sonuçları arasında herhangi bir birleşimini ayarlamak veya **ardışık ihlallerini** ihlallerini hello toorequire ardışık örnekler içinde gerçekleşmesi gerekir. |

### <a name="actions"></a>Eylemler
Uyarı kuralları her zaman oluşturacak bir [uyarı kaydı](#alert-records) hello eşiği karşılanıyorsa zaman.  Ayrıca bir tanımlayabilirsiniz veya daha fazla yanıtları toobe bir e-posta gönderme veya bir runbook'u başlatma gibi çalıştırın.



#### <a name="email-actions"></a>E-posta Eylemler
E-posta Eylemler hello uyarı tooone veya daha fazla alıcı hello ayrıntılarını içeren bir e-posta gönderin.

| Özellik | Açıklama |
|:--- |:---|
| E-posta ile bildirim |Belirtin **Evet** hello uyarı tetiklendiğinde gönderilen e-posta toobe istiyorsanız. |
| Konu |Merhaba e-postayla konu.  Merhaba hello posta gövdesini değiştiremezsiniz. |
| Alıcıları |Tüm e-posta alıcıları adresleri.  Noktalı virgül (;) birden fazla adres sonra ayrı hello adresleri belirtirseniz. |

#### <a name="webhook-actions"></a>Web kancası eylemleri
Web kancası eylemleri tooinvoke bir dış işlem tek bir HTTP POST isteği üzerinden izin verin.

| Özellik | Açıklama |
|:--- |:---|
| Web Kancası |Belirtin **Evet** hello uyarı tetiklendiğinde toocall bir Web kancası istiyorsanız. |
| Web kancası URL'si |Merhaba Web kancası URL'si Hello. |
| Özel JSON yükünü dahil et |Özel bir yükü tooreplace hello varsayılan yükünü istiyorsanız bu seçeneği seçin. |
| Özel JSON yükünüzü girin |Merhaba hello Web kancası için özel yükü.  Ayrıntılar için önceki bölüme bakın. |

#### <a name="runbook-actions"></a>Runbook eylemleri
Runbook eylemleri, Azure Automation'da bir runbook başlatın. 

>[!NOTE]
> Merhaba Otomasyon çözümünü etkin Bu eylem toobe için çalışma alanınızdaki yüklü olması gerekir. 


| Özellik | Açıklama |
|:--- |:---|
| Runbook | Belirtin **Evet** hello uyarı tetiklendiğinde toostart bir Azure Otomasyonu runbook'u istiyorsanız.  |
| Otomasyon hesabı | Merhaba runbook'lar seçildiği Otomasyon hesabı belirtir.  Bu toohello çalışma bağlanan hello eylem hesabıdır. |
| Bir runbook seçin | Merhaba runbook bir uyarı oluşturulduğunda, toostart istediğinizi seçin. |
| Üzerinde çalışır | Seçin **Azure** toorun hello runbook hello bulutta.  Seçin **karma çalışanı** toorun hello runbook ile bir aracı üzerinde [karma Runbook çalışanı](../automation/automation-hybrid-runbook-worker.md ) yüklü.  |




## <a name="next-steps"></a>Sonraki adımlar
* Merhaba yüklemek [uyarı yönetimi çözümü](log-analytics-solution-alert-management.md) günlük analizi ile birlikte uyarıları oluşturulan tooanalyze uyarıların toplanan System Center Operations Manager (SCOM).
* Daha fazla bilgi edinin [oturum aramaları](log-analytics-log-searches.md) uyarılar oluşturabilir.
* İzlenecek yollar için tamamlamak [bir webook yapılandırma](log-analytics-alerts-webhooks.md) bir uyarı kuralı ile.  
* Öğrenin nasıl toowrite [Azure automation'daki runbook'lar](https://azure.microsoft.com/documentation/services/automation) tooremediate sorunları uyarıları ile tanımlanır.

