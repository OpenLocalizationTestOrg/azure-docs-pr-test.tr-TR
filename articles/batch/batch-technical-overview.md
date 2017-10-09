---
title: "Merhaba bulutta aaaAzure toplu çalışan büyük ölçekli paralel işlem çözümleri | Microsoft Docs"
description: "Büyük ölçekli paralel ve HPC iş yükleri için Hello Azure Batch hizmetini kullanma hakkında bilgi edinin"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a>Batch ile doğası gereği paralel iş yüklerini çalıştırın

Azure Batch, büyük ölçekli paralel ve yüksek performanslı bilgi (HPC) uygulamalarında hello bulutta verimli bir şekilde çalıştırmak için bir platform hizmetidir. Azure toplu işlem yoğunluklu iş toorun yönetilen sanal makineler koleksiyonunda zamanlar ve ölçek kaynakları toomeet hello işleriniz ihtiyaçlarını işlem otomatik olarak.

Azure Batch ile kolayca Azure işlem kaynakları tooexecute uygulamalarınızı paralel olarak ve ölçekte tanımlayabilirsiniz. Hiçbir gerek toomanually yoktur oluşturmak, yapılandırmak ve HPC Kümesi, tek tek sanal makineleri, sanal ağlar veya karmaşık iş yönetmek ve görev zamanlama altyapısını. Azure Batch bu görevleri sizin için otomatikleştirir ya da basitleştirir.

## <a name="use-cases-for-batch"></a>Batch için örnek kullanma
Batch, *toplu işleme* veya *toplu bilgi işlem* için kullanılan bir Azure hizmetidir; bazı istenen sonuçları almak için büyük miktarlarda benzer görev çalıştırır. Toplu bilgi işlem, düzenli olarak büyük miktarlarda veriyi işleyen, dönüştüren ve analiz eden kuruluşlar tarafından yaygın olarak kullanılır.

Toplu işlem, doğası gereği paralel ("utandırıcı derecede paralel" olarak da bilinir) uygulamalar ve iş yükleriyle düzgün çalışır. Doğası gereği paralel iş yükleri, çalışmayı aynı anda birden çok bilgisayarda gerçekleştiren birden çok göreve kolayca ayrılır.

![Paralel görevler][1]<br/>

Bu teknik kullanılarak yaygın olarak işlenen iş yüklerinin bazı örnekleri şunlardır:

* Finansal risk modelleme
* İklim ve hidroloji veri analizi
* Görüntü işleme ve analizi
* Medya kodlama ve kodlama dönüştürme
* Genetik dizi analizi
* Mühendislik gerilimi analizi
* Yazılım testi

Toplu da hello sonunda azalan adımla paralel hesaplamalar ve daha karmaşık HPC iş yükleri gibi yürütme [ileti geçirme arabirimi (MPI)](batch-mpi.md) uygulamalar.

Azure’deki Batch ve diğer HPC çözüm seçenekleri arasında bir karşılaştırma için bkz. [ Batch ve HPC çözümleri](batch-hpc-solutions.md).

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a>Senaryo: Paralel iş yükünü ölçeklendirme
Merhaba Batch hizmeti ile Merhaba Batch API'lerini toointeract kullanan ortak çözüm, paralel işi aslında--hello--işlem düğümlerinin havuzunda 3B görüntülerin işlenmesi gibi ölçeklendirmeyi kapsar. Bu işlem düğümü havuzu oluşturacak, "işleme çiftliği" olabilir onlarca, yüzlerce veya hatta binlerce çekirdek tooyour işleme işi, örneğin sağlar.

Merhaba Aşağıdaki diyagramda bir ortak toplu iş akışı, bir istemci uygulaması ile gösterir veya toplu toorun paralel iş yükünü kullanarak hizmet barındırılabilir.

![Batch çözümü iş akışı][2]

Bu ortak senaryoda, uygulama veya hizmet Azure Batch bir hesaplama iş yükünü hello aşağıdaki adımları gerçekleştirerek işler:

1. Merhaba karşıya **giriş dosyaları** ve hello **uygulama** bu dosyaları tooyour Azure depolama hesabı işleyecek. Merhaba giriş dosyaları finansal modelleme verileri veya video dosyaları toobe kod çevrimi gibi uygulamanızın işleyeceği herhangi bir veri olabilir. Merhaba uygulama dosyaları, 3B işleme uygulaması veya medya dönüştürücü gibi hello verileri işlemek için kullanılan herhangi bir uygulama olabilir.
2. Bir toplu iş oluşturma **havuzu** Batch hesabınızın işlem düğümlerine ait görevlerinizi yürütecek hello sanal makineleri bu düğümler şunlardır. Hello gibi özellikleri belirtin [düğüm boyutu](../cloud-services/cloud-services-sizes-specs.md), kendi işletim sistemi ve hello düğümleri hello havuzu (#1. adımda karşıya hello uygulama) katıldığınızda hello uygulama tooinstall Azure Storage hello konum. Merhaba havuzu çok yapılandırabilirsiniz[otomatik olarak ölçeklendirme](batch-automatic-scaling.md) görevlerinizin oluşturduğu yanıt toohello iş yükü de. Otomatik ölçeklendirme-dinamik olarak hello hello havuzdaki işlem düğümleri sayısını ayarlar.
3. Bir toplu iş oluşturma **iş** toorun hello iş yüküne hello işlem düğümü havuzu oluşturacak. Proje oluşturduğunuzda, bunu Batch havuzuyla ilişkilendirirsiniz.
4. Ekleme **görevleri** toohello işi. Görevleri tooa iş eklediğinizde, hello Batch hizmeti hello görevleri hello hello havuzundaki işlem düğümlerinde yürütülmesi için otomatik olarak zamanlar. Her görev tooprocess hello giriş dosyaları karşıya Merhaba uygulaması kullanır.
   
   * 4a. Görev yürütülmeden önce tooprocess toohello işlem düğümü için atanmış olan hello verileri (Merhaba girdi dosyaları) indirebilir. Merhaba uygulaması zaten hello düğümde yüklenmişse değil (bkz. #2. adım), burada de bunun yerine indirilir. Merhaba yüklemeleri tamamlandığı zaman hello görevler atanmış düğümlerinde yürütün.
5. Merhaba görevleri çalıştırmak gibi toplu toomonitor hello ilerlemesini hello işi ve görevleri sorgulayabilirsiniz. İstemci uygulamanız veya hizmetiniz HTTPS üzerinden hello Batch hizmeti ile iletişim kurar. Binlerce işlem düğümünde çalışan görevler binlerce izleme olduğundan emin olun çok[hello Batch hizmetinin verimli bir şekilde sorgu](batch-efficient-list-queries.md).
6. Merhaba görevleri tamamlama gibi kendi sonuç veri tooAzure depolama karşıya yükleyebilirsiniz. Dosyaları doğrudan hello dosya sisteminden bir işlem düğümünde de alabilirsiniz.
7. İzlemenizi hello görevlerin tamamlandığını algıladığında, istemci uygulamanız veya hizmetiniz daha fazla işleme ya da değerlendirme için hello çıktı verilerini indirebilir.

Tutmak göz önünde bu yalnızca bir yolu toouse toplu ve bu senaryo, yalnızca birkaç kullanılabilir özellikleri açıklar. Örneğin, yürütebilir [birden çok görevi paralel](batch-parallel-node-tasks.md) her işlem düğümünde ve kullanabileceğiniz [iş hazırlama ve tamamlama görevlerini](batch-job-prep-release.md) tooprepare hello işleriniz için düğümleri ve daha sonra temizleme.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba Batch hizmeti üst düzey bir genel bakış sahip olduğunuza göre zaman toodig daha derin toolearn olduğunu nasıl tooprocess kullanabilirsiniz, işlem yoğunluklu paralel iş yükleri.

* Okuma hello [geliştiriciler için Batch özelliklerine genel bakış](batch-api-basics.md), önemli bilgiler herkesin toouse toplu hazırlanıyor. Merhaba makale Batch uygulamanızı oluştururken kullanabileceğiniz birçok API özellikleri Batch hizmeti kaynak havuzları, düğümleri, işler ve görevler ve hello gibi hakkında daha ayrıntılı bilgi içerir.
* Merhaba hakkında bilgi edinin [Batch API'lerini ve araçları](batch-apis-tools.md) Batch çözümleri oluşturmak için kullanılabilir.
* [.NET için Hello Azure Batch kitaplığını kullanmaya başlama](batch-dotnet-get-started.md) toolearn nasıl toouse C# ve Batch .NET kitaplığı tooexecute ortak bir toplu iş akışı kullanarak basit bir iş yükü hello. Bu makalede nasıl toouse hello Batch hizmeti öğrenme sırasında ilk duraklarınızdan biri olmalıdır. Ayrıca bir [Python sürümü](batch-python-tutorial.md) hello Öğreticisi.
* Merhaba karşıdan [github'daki kod örnekleri] [ github_samples] nasıl hem C# ve Python arabirim toplu tooschedule ve işlem örnek iş yükleri ile toosee.
* Merhaba denetleyin [Batch öğrenme yolu] [ learning_path] tooget hello kaynakları kullanılabilir tooyou yazarken hakkında bir fikir toowork toplu ile bilgi edinin.


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
