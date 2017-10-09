---
title: "Günlük analizi aaaCustom alanları | Microsoft Docs"
description: "Günlük analizi Hello özel alanlar özelliği sağlar, toocreate kendi aranabilir alanlara OMS verilerden toplanan kaydının toohello özellikleri ekleyin.  Bu makalede hello işlem toocreate özel bir alan açıklar ve örnek olay ile ayrıntılı bilgi sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a>Günlük analizi içinde özel alanlar
Merhaba **özel alanlar** özelliği günlük analizi olanağı sağlar, tooextend kaydına hello OMS deposu kendi aranabilir alanlar ekleyerek.  Özel alanlar hello diğer özellikleri ayıklanan verilerinden otomatik olarak doldurulur aynı kaydı.

![Özel alanlarına genel bakış](media/log-analytics-custom-fields/overview.png)

Örneğin, aşağıdaki hello örnek kaydı hello olay açıklamasında kaçınma yararlı veri yok.  Bu verileri ayrı özelliklerini ayıklama sıralama ve filtreleme gibi eylemlere için kullanılabilir yapar.

![Günlük Ara düğmesi](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> Hello Önizleme'de, sınırlı too100 özel alanlar çalışma alanınızdaki bağlıdır.  Bu özellik genel kullanılabilirlik ulaştığında bu sınırı genişletilir.
> 
> 

## <a name="creating-a-custom-field"></a>Özel bir alan oluşturma
Özel bir alan oluşturduğunuzda, günlük analizi değerini hangi veri toouse toopopulate anlamanız gerekir.  Bir teknolojisini kullanan FlashExtract adlı Microsoft Research tooquickly bu verileri tanımlamak.  Tooprovide açık yönergeler, ilgili hello verileri günlük analizi öğrenir gerektiren yerine sağladığınız örneklerle tooextract istiyor.

Aşağıdaki bölümlerde hello özel alan oluşturmak için hello yordamını sağlar.  Merhaba bu makalenin alt örnek ayıklama bir kılavuz ' dir.

> [!NOTE]
> Merhaba özel alan hello özel alan oluşturulduktan sonra toplanan kayıtları yalnızca görünür ölçütleri toohello OMS veri deposuna eklendi eşleşen hello belirtilen kayıtları olarak doldurulur.  Merhaba özel alan oluşturulduğunda zaten olan hello veri deposunda toorecords eklenmedi.
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a>Adım 1 – hello özel alan olacaktır tanımla kayıtları
Merhaba ilk adımı hello özel alan alırsınız tooidentify hello kayıtları oluşturur.  İle başlayan bir [standart günlük arama](log-analytics-log-searches.md) ve günlük analizi bilgi edineceksiniz hello modeli olarak kayıt tooact seçin.  Özel bir alana tooextract veri giderek belirttiğinizde, hello **alan ayıklama Sihirbazı** burada doğrulamak ve hello ölçütü iyileştirin açılır.

1. Çok Git**günlük arama** ve bir [sorgu tooretrieve hello kayıtları](log-analytics-log-searches.md) hello özel alan olacaktır.
2. Günlük analizi tooact veri toopopulate hello özel alan ayıklanması için model olarak kullanacağı bir kayıt seçin.  Bu kayıttaki tooextract istediğiniz ve günlük analizi tüm benzer kayıtları için bu bilgileri toodetermine hello mantığı toopopulate hello özel alan kullanacağı hello verileri tanımlayacak.
3. Merhaba düğmesi toohello hello seçin ve kayıt herhangi bir metin özelliği solundaki tıklatın **ayıklamak alanlardan**.
4. Merhaba **alan ayıklama Sihirbazı açıldığında**, ve seçtiğiniz hello kayıt hello görüntülenir **ana örnek** sütun.  Hello özel alan, seçili hello özelliklerinde değerlerini aynı hello olan kayıtları için tanımlanır.  
5. Merhaba seçimi tam istediğinizi ise, ek alanlar toonarrow hello ölçütü seçin.  Merhaba ölçütlerine sipariş toochange hello alan değerlerini içinde iptal edin ve istediğiniz hello ölçütlerle eşleşen başka bir kayıt seçin.

### <a name="step-2---perform-initial-extract"></a>2. adım - ilk extract yapar.
Merhaba özel alan olacaktır hello kayıtları tanımladıktan sonra tooextract istediğiniz hello verileri tanımlamak.  Günlük analizi bu bilgileri tooidentify benzer desenleri benzer kayıtlarını kullanır.  Bundan sonra hello adımda hello sonuçları mümkün toovalidate olması ve ayrıntılı günlük analizi toouse kendi analiz için bilgi sağlayan.

1. Toopopulate hello özel alan istediğiniz hello örnek kayıt Hello metinde vurgulayın.  Ardından bir iletişim kutusu tooprovide ile Merhaba alan ve tooperform hello ilk ayıklamak için bir ad sunulur.  Merhaba karakter  **\_CF** otomatik olarak eklenir.
2. Tıklatın **ayıklamak** tooperform toplanan kayıtları analizini.  
3. Merhaba **Özet** ve **arama sonuçları** bölümleri doğruluğunu inceleyebilirsiniz şekilde hello extract hello sonuçları görüntülenir.  **Özet** hello kullanılan ölçütleri tooidentify kaydeder ve sayı her tanımlanan hello veri değerleri için görüntüler.  **Arama sonuçlarında** hello ölçütlerle eşleşen kayıtları ayrıntılı bir listesini sağlar.

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a>Adım 3 – hello extract doğruluğunu onaylamak ve özel alan oluşturma
Merhaba ilk extract gerçekleştirdikten sonra günlük analizi zaten toplanan verilere dayalı sonuçlarını görüntüler.  Daha sonra Hello sonuçları doğru bakarsanız ile başka hiçbir iş hello özel alan oluşturabilirsiniz.  Aksi durumda, böylece günlük analizi, mantığını artırabilir hello sonuçları geliştirebilirsiniz.

1. Hello hello ilk extract herhangi bir değer doğru değilse, ardından **Düzenle** simgesi sonraki tooan yanlış kayıt ve seçin **bu Vurgu değiştirmek** sipariş toomodify hello seçimdeki.
2. Merhaba kopyalanan toohello giriştir **ek örnekler** bölüm hello altında **ana örnek**.  Merhaba Vurgu ayarlayabilirsiniz burada toohelp günlük analizi, yapmış hello seçimi anlama.
3. Tıklatın **ayıklamak** toouse tüm hello varolan bu yeni bilgi tooevaluate kaydeder.  Merhaba sonuçları, bir yalnızca değiştirdiğiniz bu yeni Intelligence üzerinde temel hello dışında kayıtlar için değiştirilebilir.
4. Merhaba tüm kayıtları doğru ayıklamak kadar tooadd düzeltmeleri hello veri toopopulate hello yeni özel alan tanımlamak devam edin.
5. Tıklatın **Kaydet ayıklamak** hello Sonuçlardan memnun olduğunda.  Hello özel alan şimdi tanımlı, ancak bunu henüz tooany kayıtları eklenmeyecek.
6. Bekleme hello eşleşen yeni kayıtlar için belirtilen ölçütleri toobe toplanan ve hello günlük arama yeniden çalıştırın. Yeni kayıtlar hello özel alan olması gerekir.
7. Herhangi bir kayıt özelliği gibi Hello özel alan kullanın.  Tooaggregate ve grup verilerini kullanır ve hatta tooproduce yeni Öngörüler kullanın.

## <a name="viewing-custom-fields"></a>Özel alanları görüntüleme
Merhaba gelen yönetim grubunuzdaki tüm özel alanların listesini görüntüleyebilirsiniz **ayarları** hello OMS Pano parçasına.  Seçin **veri** ve ardından **özel alanlar** çalışma alanınızdaki tüm özel alanlar listesi.  

![Özel alanlar](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a>Özel bir alan kaldırma
Özel bir alan iki yolu tooremove vardır.  Merhaba ilk hello olan **kaldırmak** yukarıda açıklandığı gibi hello tam listesi görüntülerken, her bir alan için seçeneği.  Merhaba diğer hello alanı kaydı ve tıklatın hello düğmesi toohello sol tooretrieve yöntemidir.  Başlangıç menüsünden bir seçenek tooremove hello özel alan gerekir.

## <a name="sample-walkthrough"></a>Örnek gözden geçirme
Merhaba aşağıdaki bölümde özel bir alan oluşturma tam bir örnek anlatılmaktadır.  Bu örnek, bir hizmetin durumunu değiştirme belirten Windows olayları hello hizmet adını ayıklar.  Bu Windows bilgisayarlarda hello sistem günlüğüne hizmet denetimi yöneticisi tarafından oluşturulan olayları kullanır.  Bu örnek toofollow istiyorsanız olmalıdır [hello sistem günlüğü için bilgi Olay toplama](log-analytics-data-sources-windows-events.md).

Biz hello sorgu tooreturn aşağıdaki hizmet denetimi yöneticisinden olay başlayan veya durdurulan bir hizmeti gösterir hello olay olan Kimliğini 7036 olan tüm olayları girin.

![Sorgu](media/log-analytics-custom-fields/query.png)

Biz sonra olay kimliği 7036 içeren herhangi bir kayıt seçin.

![Kaynak kaydı](media/log-analytics-custom-fields/source-record.png)

Hello görünür hello hizmet adı istiyoruz **RenderedDescription** özelliği ve select hello düğmesine bir sonraki toothis özelliği.

![Alanları ayıklayın](media/log-analytics-custom-fields/extract-fields.png)

Merhaba **alan ayıklama Sihirbazı** açılır ve hello **EventLog** ve **EventID** alanları hello seçili **ana örnek** sütun.  Bu, o hello özel alan hello sistem günlüğüne bir olay kimliği 7036 olay için tanımlanan gösterir.  Bu, diğer alanlar tooselect gerekmez için yeterlidir.

![Ana örneği](media/log-analytics-custom-fields/main-example.png)

Biz hello hello hizmetinde hello adını vurgulayın **RenderedDescription** özelliği ve kullanım **hizmet** tooidentify hello hizmet adı.  Merhaba özel alan çağrılabilir **Service_CF**.

![Alan başlığı](media/log-analytics-custom-fields/field-title.png)

Merhaba hizmet adının doğru başkaları için ancak bazı kayıtlar tanımlanmasını bakın.   Merhaba **arama sonuçları** hello hello adı kısmı Göster **WMI Performans bağdaştırıcısı** seçili değildi.  Merhaba **Özet** dört kayıtlar gösterir **DPRMA** hizmet yanlış dahil ek bir sözcük ve tanımlanan iki kayıt **Modül Yükleyicisi** yerine**Windows Modül Yükleyicisi**.  

![Arama sonuçları](media/log-analytics-custom-fields/search-results-01.png)

Biz ile Merhaba Başlat **WMI Performans bağdaştırıcısı** kaydı.  Biz, düzenleme simgesine tıklayın ve ardından **bu Vurgu değiştirme**.  

![Vurgu değiştirme](media/log-analytics-custom-fields/modify-highlight.png)

Biz hello Vurgu tooinclude hello word artırmak **WMI** hello extract yeniden çalıştırın.  

![Ek örnek](media/log-analytics-custom-fields/additional-example-01.png)

Bu hello görebiliriz girişlerinde **WMI Performans bağdaştırıcısı** düzeltildi, ve günlük analizi de bilgi toocorrect hello kayıt için kullanılan **Windows Modülü Yükleyicisi**.  Hello görebiliriz **Özet** rağmen bölüm **DPMRA** hala doğru tanımlanamadı.

![Arama sonuçları](media/log-analytics-custom-fields/search-results-02.png)

Biz hello DPMRA hizmetini tooa kaydıyla kaydırın ve aynı kayıt toocorrect işlemi hello kullanın.

![Ek örnek](media/log-analytics-custom-fields/additional-example-02.png)

 Biz hello ayıklama çalıştırdığınızda, tüm sonuçları şimdi doğruluğunu görebiliriz.

![Arama sonuçları](media/log-analytics-custom-fields/search-results-03.png)

Görebiliriz **Service_CF** oluşturuldu ancak henüz tooany kayıtları eklenmez.

![İlk sayımı](media/log-analytics-custom-fields/initial-count.png)

Bu nedenle yeni bir süre geçtikten sonra olayları toplanır, hello görebiliriz **Service_CF** alan bizim ölçütleriyle eşleşen toorecords eklenmiş.

![Son sonuçları](media/log-analytics-custom-fields/final-results.png)

Biz, artık herhangi bir kayıt özelliği gibi hello özel alan kullanabilirsiniz.  tooillustrate bunu hello yeni gruplar bir sorgu oluşturuyoruz **Service_CF** hangi hizmetlerin hello en etkin olan alan tooinspect.

![Sorgu tarafından Grup](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) özel alanlar için ölçüt kullanarak toobuild sorgular.
* İzleyici [özel günlük dosyalarını](log-analytics-data-sources-custom-logs.md) , özel alanlar kullanarak ayrıştırılamıyor.

