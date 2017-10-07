---
title: "otomatik ölçeklendirme Azure aaaGet Başlarken | Microsoft Docs"
description: "Bilgi nasıl tooscale kaynağınız azure'da."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a>Otomatik ölçeklendirme Azure kullanmaya başlama
Bu makalede nasıl hello Microsoft Azure Portalı'nda, kaynak için otomatik ölçeklendirme ayarlarını tooset.

Azure İzleyici otomatik ölçeklendirme yalnızca toovirtual makine ölçekleme kümeleri, bulut Hizmetleri, Azure uygulama hizmeti planları ve uygulama hizmeti ortamları geçerlidir. 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a>Merhaba otomatik ölçeklendirme ayarlarını aboneliğinizde Bul
Otomatik ölçeklendirme Azure İzleyicisi'nde geçerli olduğu tüm hello kaynakları bulabilir. Aşağıdaki adımları adım adım kılavuz hello kullan:

1. Açık hello [Azure portalı.][1]
2. Merhaba sol bölmede Hello Azure İzleyici simgesine tıklayın.
  ![Açık Azure İzleyicisi][2]
3. Tıklatın **otomatik ölçeklendirme** tooview hangi otomatik ölçeklendirme için tüm hello kaynakları geçerli otomatik ölçeklendirme durumlarıyla birlikte uygulanabilir.
  ![Otomatik ölçeklendirme Azure İzleyicisi'nde Bul][3]

Belirli bir kaynak grubunun, belirli kaynak türlerine veya belirli bir kaynak hello listesi tooselect kaynakları aşağı hello üst tooscope adresindeki hello Filtre bölmesini kullanın.

Her bir kaynağın hello geçerli örnek sayısına ve hello otomatik ölçeklendirme durum bulacaksınız. Merhaba otomatik ölçeklendirme Durum aşağıdakilerden biri olabilir:

- **Yapılandırılmamış**: otomatik ölçeklendirme henüz bu kaynak için etkinleştirdiğiniz değil.
- **Etkin**: Bu kaynak için otomatik ölçeklendirme etkin.
- **Devre dışı**: Bu kaynak için otomatik ölçeklendirme devre dışı bırakmış.

## <a name="create-your-first-autoscale-setting"></a>İlk otomatik ölçeklendirme ayarı oluşturun

Şimdi şimdi basit adım adım toocreate ilk otomatik ölçeklendirme ayarına gidin.

1. Açık hello **otomatik ölçeklendirme** dikey Azure İzleyici ve tooscale istediğiniz bir kaynak seçin. (Merhaba aşağıdaki adımlar bir web uygulaması ile ilişkili bir uygulama hizmeti planı kullanın. Yapabilecekleriniz [ilk ASP.NET web uygulamanızı 5 dakika içinde oluşturma.] [4])
2. Merhaba geçerli örnek sayısı 1 olduğuna dikkat edin. Tıklatın **etkinleştirmek otomatik ölçeklendirme**.
  ![Yeni web uygulaması için ölçek ayarı][5]
3. Merhaba ölçeği ayarlamak için bir ad sağlayın ve ardından **bir kural eklemek**. İçerik bölmesinde hello sağ tarafında olarak açın hello ölçek kuralı seçeneklerini dikkat edin. Varsayılan olarak, bu hello seçeneği tooscale örneğinizi sayısı 1 ile yüzde 70'hello hello kaynak CPU yüzdesini aşarsa, ayarlar. Kendi varsayılan değerlerinde bırakın ve tıklatın **Ekle**.
  ![Bir web uygulaması için ölçek ayar oluşturun][6]
4. İlk ölçek kuralı şimdi oluşturduğunuzu düşünün. UX önerir en iyi yöntemler ve bildiren bu hello unutmayın "toohave önerilen en az bir ölçek kuralında." toodo için:
  
    a. Tıklatın **bir kural eklemek**. 

    b. Ayarlama **işleci** çok**değerinden**.

    c. Ayarlama **eşik** çok**20**.

    d. Ayarlama **işlemi** çok**azaltmak sayısına göre**.

   Ölçek ayarını şimdi olmalıdır ölçek genişletme/ölçekler olduğunu içinde tabanlı CPU kullanımı.
   ![CPU üzerinde göre ölçeklendirin][8]
5. **Kaydet** düğmesine tıklayın.

Tebrikler! Web uygulamanızı CPU kullanımı dikkate alarak, ilk ölçek ayarı tooautoscale şimdi başarıyla oluşturdunuz.

> [!NOTE] 
> Merhaba adımlarıyla aynıdır ile bir sanal makine ölçek kullanmaya uygun tooget kümesi veya Bulut hizmet rolü.

## <a name="other-considerations"></a>Diğer konular
### <a name="scale-based-on-a-schedule"></a>Bir zamanlamaya göre ölçeği
Ayrıca CPU üzerinde temel tooscale, Ölçek farklı hello haftanın belirli günleri için ayarlayabilirsiniz.

1. Tıklatın **ölçek koşul Ekle**.
2. Merhaba ölçek modu ve hello kurallarının ayarlanması olduğu hello aynı hello varsayılan koşulu olarak.
3. Seçin **yineleyin belirli günleri** hello zamanlama için.
4. Merhaba gün ve hello ölçek koşul ne zaman uygulanacağını için hello başlangıç/bitiş saati seçin.

![Zamanlamaya göre ölçeği koşulu][9]
### <a name="scale-differently-on-specific-dates"></a>Farklı belirli tarihleri ölçeklendirme
Ayrıca CPU üzerinde temel tooscale, Ölçek farklı belirli tarihler için ayarlayabilirsiniz.

1. Tıklatın **ölçek koşul Ekle**.
2. Merhaba ölçek modu ve hello kurallarının ayarlanması olduğu hello aynı hello varsayılan koşulu olarak.
3. Seçin **belirt başlangıç/bitiş tarihlerini** hello zamanlama için.
4. Merhaba başlangıç/bitiş tarihleri ve hello ölçek koşul ne zaman uygulanacağını için hello başlangıç/bitiş saati seçin.

![Tarihleri temel alınarak ölçek koşulu][10]

### <a name="view-hello-scale-history-of-your-resource"></a>Kaynağınız hello ölçek geçmişini görüntüle
Kaynağınız yukarı veya aşağı ölçeklendirilir her bir olay hello etkinlik günlüğüne kaydedilir. Toohello geçerek son 24 saat hello kaynak hello ölçek geçmişini görüntüleyebilirsiniz **çalıştırma geçmişi** sekmesi.

![çalıştırma geçmişi][11]

Tooview hello tam ölçek geçmişi istiyorsanız (için yukarı too90 gün), select **toosee daha fazla ayrıntı burayı**. Hello etkinlik günlüğünde, kaynak ve kategori için önceden seçilmiş otomatik ölçeklendirme ile açılır.

### <a name="view-hello-scale-definition-of-your-resource"></a>Merhaba ölçek, kaynak tanımını görüntüleme
Otomatik ölçeklendirme bir Azure Resource Manager kaynaktır. Merhaba ölçek tanımı JSON'de toohello geçerek görüntüleyebileceğiniz **JSON** sekmesi.

![Ölçek tanımı][12]

JSON'da doğrudan gerekirse değişiklik yapabilirsiniz. Bunları kaydettikten sonra bu değişiklikleri yansıtılır.

### <a name="disable-autoscale-and-manually-scale-your-instances"></a>Otomatik ölçeklendirme devre dışı bırakın ve el ile örneklerinizi ölçeklendirin
Ne zaman toodisable geçerli ölçek ayarınız isterseniz ve elle kaynağınız ölçeklendirme kez olabilir.

Merhaba tıklatın **otomatik ölçeklendirme devre dışı bırakma** hello üst düğmesini.
![Otomatik ölçeklendirme devre dışı bırak][13]

> [!NOTE] 
> Bu seçenek yapılandırmanızı devre dışı bırakır. Ancak, otomatik ölçeklendirme yeniden etkinleştirildikten sonra tooit geri alabilirsiniz. 

Şimdi hello tooscale toomanually istediğiniz örneklerinin sayısını ayarlayabilirsiniz.

![El ile ölçek kümesi][14]

Tıklatarak tooAutoscale her zaman dönebilirsiniz **etkinleştirmek otomatik ölçeklendirme** ve ardından **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
- [Bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm otomatik ölçeklendirme altyapısı işlemler oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm başarısız otomatik ölçeklendirme ölçek/genişletme işlemleri oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

