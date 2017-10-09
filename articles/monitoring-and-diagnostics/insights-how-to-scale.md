---
title: "aaaScale örnek sayısını elle veya otomatik ölçeklendirme Azure portalıyla | Microsoft Docs"
description: "Bilgi nasıl tooscale Azure hizmetlerinizi."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>Örnek sayısı el ile veya otomatik olarak ölçeklendirme
Merhaba, [Azure Portal](https://portal.azure.com/), hizmetinizin hello örnek sayısı el ile ayarlayabilirsiniz veya, otomatik olarak ölçeklendirme toohave tabanlı isteğe bağlı parametreler ayarlayabilirsiniz. Bu genellikle başvurulan tooas olan *ölçeğini* veya *içinde ölçeklendirmek*.

Örnek sayısına göre ölçeklendirme önce tarafından ölçeklendirme etkilenir düşünmelisiniz **fiyatlandırma katmanı** toplama tooinstance sayısı. Farklı fiyatlandırma katmanlarına sahip farklı numaraları çekirdek ve bellek ve bu nedenle bunlar olacaktır hello daha iyi performans örnekleri aynı sayıda (olduğu *ölçeği* veya *ölçeklendirmeyi azaltın*). Bu makalede özellikle kapsayan *içinde ölçeklendirmek* ve *çıkışı*.

Merhaba Portalı'nda ölçeklendirebilirsiniz ve hello de kullanabilirsiniz [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) veya [.NET SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust el ile veya otomatik olarak ölçeklendirin.

> [!NOTE]
> Bu makalede nasıl hello portalında ayarını otomatik ölçeklendirme bir toocreate [http://portal.azure.com](http://portal.azure.com). Bu Portalı'nda oluşturulan otomatik ölçeklendirme ayarlarını olamaz hello Klasik portal düzenlenebilir ([http://manage.windowsazure.com](http://manage.windowsazure.com)).
> 
> 

## <a name="scaling-manually"></a>El ile ölçeklendirme
1. Merhaba, [Azure Portal](https://portal.azure.com/), tıklatın **Gözat**, istediğiniz tooscale, gibi toohello kaynak gidin bir **uygulama hizmeti planı**.
2. Tıklatın **ayarlar > Ölçek genişletme (uygulama hizmeti planı).**
3. Merhaba hello üstündeki **ölçek** dikey penceresinde hello hizmetinin otomatik ölçeklendirme eylemleri geçmişini görebilirsiniz.
   
    ![Ölçek dikey penceresi](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > Otomatik ölçeklendirme tarafından gerçekleştirilen eylemler Bu grafikte gösterir. Merhaba örnek sayısı el ile ayarlarsanız bu grafikte hello değişiklik yansıtılmaz.
   > 
   > 
4. Merhaba numarasını el ile ayarlayabilirsiniz **örnekleri** kaydırıcı ile.
5. Merhaba tıklatın **kaydetmek** komutunu olması toothat örneklerinin sayısını hemen ölçeklendirilmiş.

## <a name="scaling-based-on-a-pre-set-metric"></a>Üzerinde önceden ayarlanmış bir ölçümü tabanlı ölçeklendirme
Merhaba sayısının üzerinde bir ölçümü tabanlı tooautomatically ayarlamak istiyorsanız, hello istediğiniz ölçümü seçin hello **göre Ölçeklendirmeniz** açılır. Örneğin, bir **uygulama hizmeti planı** tarafından ölçeklendirebilirsiniz **CPU yüzdesi**.

1. Ölçüm seçtiğinizde kaydırıcıyı elde edersiniz ve/veya, metin kutuları tooenter hello örnek sayısı arasında tooscale istiyor:
   
    ![Ölçek dikey CPU yüzdesi](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    Otomatik ölçeklendirme, hizmetinizin altında veya olsun, yük ayarlamak hello sınırları üzerinde hiçbir zaman olur.
2. İkinci olarak, hello ölçüm hello hedef aralığı seçin. Örneğin, seçtiğiniz **CPU yüzdesi**, bir hedef için ortalama CPU hello tüm hello örnekleri arasında hizmetinizi ayarlayabilirsiniz. Hello ortalama CPU tanımladığınız hello maksimum aştığında genişletme olacağını, hello ortalama CPU hello minimum bırakır her bir ölçek benzer şekilde, gerçekleşecek.
3. Merhaba tıklatın **kaydetmek** komutu. Otomatik ölçeklendirme, ölçüm için hello örnek aralığı ve hedef olduğundan emin her birkaç dakika toomake kontrol eder. Hizmetinizi ek trafiği aldığında, herhangi bir şey yapmadan daha fazla örnekleri alırsınız.

## <a name="scale-based-on-other-metrics"></a>Diğer ölçümleri temel ölçek
Temel alınarak ölçümleri hello görünür hello hazır dışında ölçeklendirebilirsiniz **göre Ölçeklendirmeniz** açılan listesinde ve hatta ölçek genişletme karmaşık kümesine sahiptir ve ölçeklendirme kuralları.

### <a name="adding-or-changing-a-rule"></a>Ekleme veya bir kural değiştirme
1. Merhaba seçin **zamanlama ve performans kuralları** hello içinde **göre Ölçeklendirmeniz** açılır: ![performans kuralları](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. Üzerinde daha önce sahip olduğunuz otomatik ölçeklendirme, sahip olduğunuz hello kesin kurallar görünümünü görürsünüz.
3. tooscale tabanlı üzerinde başka bir ölçüm tıklatın hello **Kuralı Ekle** satır. Biri de tıklayabilirsiniz hello varolan satırları toochange hello ölçüm gelen, daha önce tooscale tarafından istediğiniz toohello ölçüm sahip.
   ![Kural Ekle](./media/insights-how-to-scale/Insights_AddRule.png)
4. Şimdi tarafından tooscale istediğiniz ölçüm tooselect gerekir. Bir ölçü yok seçerken olduğunda birkaç şey tooconsider:
   
   * Merhaba *kaynak* hello ölçüm gelir. Genellikle, bu olması hello ölçeklendirme hello kaynak ile aynı. Ancak, bir depolama kuyruğu hello derinliği tarafından tooscale istiyorsanız, hello kaynak tarafından tooscale istediğiniz hello sıra değil.
   * Merhaba *ölçüm adı* kendisi.
   * Merhaba *zaman toplama* hello ölçüsünün. Bu nasıl hello veri birleştirme hello numarasıdır *süresi*.
5. Ölçüm seçtikten sonra hello ölçüm ve hello işleci hello eşiğini seçin. Örneğin, diyebilirsiniz **büyük** **% 80**.
6. Merhaba eylemini seçin tootake istiyor. Birkaç farklı türde eylemler vardır:
   
   * Artırma veya azaltma tarafından - bu ekleme veya hello kaldırma **değeri** tanımladığınız örneklerinin sayısı
   * Artırma veya azaltma yüzde - bu bir yüzde hello örnek sayısı değiştirir. Örneğin, hello 25 koyabilirsiniz **değeri** alanında ve şu anda 8 örnekleri olsaydı, 2 eklenir.
   * Artırma veya azaltma çok - bu hello örnek sayısı toohello ayarlar **değeri** tanımlarsınız.
7. Son olarak, aşağı - bu kural hello önceki ölçek eylemi tooscale sonra yeniden ne kadar beklemesi gerektiğini cool seçebilirsiniz.
8. Kural yapılandırdıktan sonra isabet **Tamam**.
9. Tüm istediğiniz hello kuralları yapılandırdıktan sonra emin toohit hello olması **kaydetmek** komutu.

### <a name="scaling-with-multiple-steps"></a>Birden çok adımı ile ölçeklendirme
Merhaba yukarıdaki oldukça temel olarak gösterilebilir. Toobe Yukarı (veya aşağı) ölçeklendirme hakkında daha agresif istiyorsanız, ancak, hatta birden fazla ölçek kuralları Merhaba aynı ekleyebileceğiniz ölçüm. Örneğin, CPU yüzdesi iki ölçek kurallar tanımlayabilirsiniz:

1. CPU yüzdesi % 60 ise 1 örneği tarafından ölçeğini genişletme
2. CPU yüzdesi % 85 ise 3 örnekleri tarafından ölçeğini genişletme

![Birden fazla ölçek kuralı](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

Bu ek kuralıyla bir ölçek eylemi önce % 85 yük aşarsa, bir yerine iki ek örnekleri alırsınız.

## <a name="scale-based-on-a-schedule"></a>Bir zamanlamaya göre ölçeği
Ölçek kuralı oluşturduğunuzda, varsayılan olarak, bu her zaman uygular. Hello profil başlığındaki tıklattığınızda, görebilirsiniz:

![Profil](./media/insights-how-to-scale/Insights_Profile.png)

Ancak, toohave daha agresif daha hello gün veya hello hafta sırasında hello hafta sonlarında ölçeklendirme isteyebilirsiniz. Hizmetinizi çalışma saatleri tamamen devre dışı bile kapatmak.

1. toodo Bu, sahip olduğunuz hello profili seçin **yineleme** yerine **her zaman,** ve hello zaman hello profil tooapply istediğinizi seçin.
2. Örneğin, toohave hello hello hafta sırasında geçerli bir profil **gün** açılır işaretini **Cumartesi** ve **Pazar**.
3. toohave hello daytime, ayarlanmış hello sırasında geçerli bir profil **başlangıç zamanı** toostart adresindeki istediğiniz toohello saati.
   
    ![Varsayılan yineleme](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. **Tamam** düğmesine tıklayın.
5. Ardından, diğer saatlerde tooapply istediğiniz tooadd hello profil gerekir. Merhaba tıklatın **eklemek profili** satır.
    ![İş devre dışı](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. Yeni, ikinci, profil adı, örneğin çağırabilirsiniz **kapalı iş**.
7. Ardından **yineleme** yeniden ve bu süre boyunca istediğiniz hello örnek sayısı aralığı seçin.
8. Merhaba varsayılan profili hello seçerken **gün** çok ve hello bu profili tooapply istediğiniz **başlangıç zamanı** hello gün sırasında.
   
   > [!NOTE]
   > Otomatik ölçeklendirme hello Yaz Saati kuralları hangisi için kullanacağınız **saat dilimi** seçin. Merhaba UTC uzaklığı hello temel saat dilimi konumu, değil hello gün ışığından yararlanma UTC uzaklığı gösterir ancak günışığından sırasında.
   > 
   > 
9. **Tamam** düğmesine tıklayın.
10. Şimdi, kuralları tooadd ihtiyacınız olacak, ikinci bir profil sırasında tooapply istiyor. Tıklatın **Kuralı Ekle**, ve ardından aynı kural hello varsayılan profili sırasında sahip hello oluşturabilir.
    
    ![Kural toooff iş ekleme](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. Emin toocreate ölçek genişletme ve ölçek için her iki kural olmalıdır, veya başka hello sırasında profili hello örnek sayısı yalnızca büyütür (azaltın veya).
12. Son olarak, tıklatın **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
* [İzleme hizmeti ölçümleri](insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.
* [İzleme ve tanılama](insights-how-to-use-diagnostics.md) toocollect ayrıntılı hizmetinizi yüksek sıklıkta ölçümleri.
* İşletimsel olaylar gerçekleştiğinde ya da ölçümler bir eşiği aştığında [uyarı bildirimleri alın](insights-receive-alert-notifications.md).
* [Uygulama performansı izleme](../application-insights/app-insights-azure-web-apps.md) tam olarak kodunuzu hello bulutta nasıl gerçekleştiriyor toounderstand istiyorsanız.
* [Olayları ve etkinlik günlüğü görüntüle](insights-debugging-with-events.md) toolearn her şeyi içeren hizmetinizi gerçekleştirilmedi.
* [Kullanılabilirlik ve yanıt hızını herhangi bir web sayfası izleme](../application-insights/app-insights-monitor-web-app-availability.md) , sayfanızın aşağı olup olmadığını öğrenmek için Application Insights ile.

