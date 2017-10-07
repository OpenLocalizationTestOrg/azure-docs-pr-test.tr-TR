---
title: "aaaAzure takım veri bilimi işlemine genel bakış | Microsoft Docs"
description: "Bir veri bilimi Metodoloji toodeliver Tahmine dayalı analiz çözümleri sağlar ve akıllı uygulamalar."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a>Takım veri bilimi işlemine genel bakış

Merhaba takım veri bilimi işlem (TDSP) olan bir Çevik, yinelemeli veri bilimi Metodoloji toodeliver Tahmine dayalı analiz çözümleri ve akıllı uygulamalar verimli bir şekilde. TDSP yardımcı takım işbirliği geliştirmek ve öğrenme. Merhaba en iyi yöntemler ve veri bilimi girişimleri başarılı uyarlamasını hello kolaylaştıran yapılarda Microsoft ve diğerleri hello endüstri distillation içerir. Merhaba toohelp şirketler tamamen kendi analytics programının hello faydaları hayata geçirmek hedeftir.

Bu makalede TDSP ve ana bileşenlerini genel bir bakış sağlar. Çeşitli araçları ile genel açıklamasını buraya hello işleminin uygulanabilir sunuyoruz. Ek bağlantılı konulardaki hello proje görevleri ve rolleri hello işlem hello çevriminin ilgili daha ayrıntılı bir açıklaması sağlanır. Tooimplement hello Microsoft araçları ve altyapısı tooimplement hello TDSP bizim ekiplerde kullandığımızı belirli bir dizi kullanılarak TDSP de nasıl sağlandığını konusunda yönergeler.

## <a name="key-components-of-hello-tdsp"></a>Merhaba TDSP anahtar bileşenleri

TDSP anahtar bileşenleri aşağıdaki Merhaba şunları kapsar:

- A **veri bilimi yaşam döngüsü** tanımı
- A **standartlaştırılmış Proje yapısı**
- **Altyapı ve kaynakları** veri bilimi projeleri için
- **Araçlar ve yardımcı programlar** proje yürütme için


## <a name="data-science-lifecycle"></a>Veri bilimi yaşam döngüsü

Merhaba takım veri bilimi işlem (TDSP) veri bilimi projelerinizi yaşam döngüsü toostructure hello geliştirilmesini sağlar. Merhaba yaşam döngüsü hello adımları, bunlar çalıştırıldığında izleyen projeleri genellikle başlangıç toofinish özetlenmektedir.

Başka bir veri bilimi yaşam döngüsü, gibi kullanıyorsanız [NET-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) veya, kuruluşun kendi özel işlem kullanmaya devam edebilirsiniz görev tabanlı TDSP bu geliştirme hello bağlamında hello yaşam döngüleri. Yüksek düzeyde, bu farklı yöntemlerini çok ortaktır. 

Bu yaşam döngüsü, akıllı uygulamaların bir parçası gönderilen veri bilimi projeleri için tasarlanmıştır. Bu uygulamalar, Tahmine dayalı analiz için makine öğrenme veya yapay zeka modelleri dağıtın. Ayrıca keşif veri bilimi projeleri veya geçici analytics projeleri bu işlemi kullanmak yararlı olabilir. Ancak bu gibi durumlarda açıklanan hello adımlardan bazıları gerekli.    

Merhaba TDSP yaşam döngüsü yinelemeli olarak yürütülen beş temel aşamadan oluşur:

* **İş anlama**
* **Veri alımı ve anlama**
* **Modelleme**
* **Dağıtım**
* **Müşteri kabulü**

Görsel bir hello işte **takım veri bilimi işlemi yaşam döngüsü**. 

![TDSP yaşam döngüsü](./media/data-science-process-overview/tdsp-lifecycle.png) 

Merhaba hedefleri, görevleri ve TDSP hello çevriminin her aşaması için belgeleri yapılar hello açıklanan [takım veri bilimi işlemi yaşam döngüsü](data-science-process-lifecycle.md) konu. Bu görevler ve yapıları proje rolleri ile ilişkilidir:

- Çözümü Mimarı
- Proje Yöneticisi
- Veri uzmanı
- Proje lideri 

Merhaba Aşağıdaki diyagramda hello görevlerinde (mavi) ve bu rolleri (üzerinde hello dikey eksen) her aşaması hello yaşam döngüsü (üzerinde hello yatay eksen) ile ilişkili yapıları (yeşil içinde) kılavuz görünümünü sağlar. 

![TDSP-roller-ve-görevleri](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a>Standartlaştırılmış Proje yapısı

Bir dizin yapısına paylaşabilir ve şablonları proje belgelerini kullanın. tüm projeleri sahip hello takım üyeleri toofind hakkında bilgi edinmek için kendi projelerine kolaylaştırır. Tüm kodu ve belgeler gibi Git, TFS veya alt sürüme tooenable takım işbirliği sürüm denetimi sistemini (VC) depolanır. İzleme görevleri ve izleme sistemi Jira gibi bir Çevik proje özelliklerinde, yarışı, Visual Studio Team Services sağlayan yakın hello kod tek tek özellikleri için izleme. Bu tür izleme ayrıca daha iyi tahminler maliyet takımlar tooobtain sağlar. Sürüm oluşturma, bilgi güvenliği ve işbirliği hello VC her proje için ayrı bir havuz oluşturma TDSP önerir. Merhaba hello kuruluş genelinde tüm projeleri yardımcı derleme kurumsal bilgi yapısı standartlaştırılmıştır.

Merhaba klasör yapısını ve standart konumlarda gerekli belgeler için şablonlar sağlar. Bu klasör yapısını veri keşfi ve özelliği ayıklama kodunu içeren ve bu modeli yineleme kayıt hello dosyaları düzenler. Bu şablonlar başkaları tarafından yapılan takım üyeleri toounderstand çalışmayı kolaylaştırır ve tooadd yeni üyeler tooteams. Kolay tooview ve güncelleştirme şablonların markdown biçiminde olur. Şablonları tooprovide denetim listeleri anahtar sorularla hello iyi tanımlanmış bir sorundur ve bu sonuçlara karşılayan beklenen hello kalite her proje tooinsure için kullanın. Örneklere şunlar dahildir:

- Proje kurucu toodocument hello problemini ve hello proje kapsamı
- veri raporları toodocument hello yapısı ve hello ham verileri istatistikleri
- Model raporları toodocument hello özellikleri türetilmiş
- Model performans ölçümleri ROC Eğriler veya MSE gibi


![TDSP dizinleri](./media/data-science-process-overview/tdsp-dir-structure.png)

Merhaba dizin yapısını gelen kopyalanmasını [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).

## <a name="infrastructure-and-resources-for-data-science-projects"></a>Altyapı ve veri bilimi projeleri için kaynakları

TDSP paylaşılan analizi ve depolama altyapısı gibi yönetme ile ilgili öneriler sağlar:

- veri kümelerini depolamak için bulut dosya sistemleri 
- veritabanları
- büyük veri kümeleri (Hadoop veya Spark) 
- Machine learning Hizmetleri. 

Hello analizi ve depolama altyapısı hello Bulut veya şirket içi olabilir. Ham ve işlenen veri kümeleri depolandığı budur. Bu Altyapı yeniden üretilebilir çözümleme sağlar. Ayrıca, tooinconsistencies ve gereksiz altyapı maliyetlerini artırabilir çoğaltma önler. Araçlar tooprovision paylaşılan kaynakları Merhaba, bunları izlemek ve her ekip üyesi tooconnect toothose kaynaklara güvenli bir şekilde olanak sağlanır. Ayrıca, iyi bir uygulama tutarlı bilgi işlem ortamı oluşturmak proje üyeleri sahip olabilir. Farklı ekip üyelerinin çoğaltabilir ve denemeler doğrulayın.

Birden fazla proje üzerinde çalıştığı ve çeşitli bulut analytics altyapı bileşenleri paylaşma bir ekibin bir örneği burada verilmiştir.

![TDSP altyapısı](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a>Araçlar ve yardımcı programlar proje yürütme için

Çoğu kuruluş işlemlerde Tanıtımı zordur. Araçlar tooimplement hello veri bilimi işlemi ve yaşam döngüsü kendi benimseme hello tutarlılığını artırmak alt hello engelleri tooand yardımcı sağlanır. TDSP TDSP toojump başlangıç benimseme ekip içinde ilk birtakım Araçlar ve komut dosyaları sağlar. Ayrıca, bazı veri keşfi ve temel modelleme gibi hello veri bilimi yaşam döngüsü hello ortak görevleri otomatikleştirmek yardımcı olur. Kişiler için Araçlar ve yardımcı programlar kendi ekibin paylaşılan kod havuzunda toocontribute paylaşılan sağlanan iyi tanımlanmış bir yapı yoktur. Bu kaynaklar, hello ekip veya hello kuruluş içindeki diğer projeler tarafından sonra yararlanılabilir. TDSP de araçlar ve yardımcı programlar toohello tamamını topluluk tooenable hello katkı planlar. Merhaba TDSP yardımcı programları gelen kopyalanmasını [Github](https://github.com/Azure/Azure-TDSP-Utilities).


## <a name="next-steps"></a>Sonraki adımlar

[Takım veri bilimi işlemi: Roller ve görevler](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) hello anahtar personel rolleri ve bu işlemi standartlaştıran veri bilimi ekibin ilişkilendirilen görevlerinin özetlenmektedir. 
