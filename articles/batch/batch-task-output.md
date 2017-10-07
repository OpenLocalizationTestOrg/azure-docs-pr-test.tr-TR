---
title: "aaaPersist sonuçları veya günlüklerinden tamamlanan işler ve görevler tooa veri deposu - Azure Batch | Microsoft Docs"
description: "Toplu iş görevlerini ve işleri kalıcı çıktı verileri için farklı seçenekler hakkında bilgi edinin. Veri depolama tooAzure veya tooanother veri kalıcı depolar."
services: batch
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0b11e387f1694e1ce3e9573db7f6013f0154cad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-output"></a>İş ve görev çıktılarını kalıcı hale getirme

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Görev çıktısı ortak bazı örnekleri şunlardır:

- Merhaba görev işlemleri veri girdikten sonra oluşturulan dosyaları.
- Görev Yürütme ile ilişkili günlük dosyaları. 

Bu makalede her seçeneği en uygun olan kalıcı görev çıktısını ve hello senaryoları için çeşitli seçenekler açıklanmaktadır.   

## <a name="about-hello-batch-file-conventions-standard"></a>Merhaba toplu iş dosyası kuralları standart hakkında

Toplu Görev çıkış dosyalarını Azure storage'da adlandırma kuralları isteğe bağlı bir kümesini tanımlar. Merhaba [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) bu kuralları açıklar. Merhaba dosyası kuralları standart hello hedef kapsayıcı ve blob Azure storage'da hello iş ve görev hello adlarına göre bir verilen çıkış dosyasının yolu hello adını belirler.

Bu, tooyou toouse hello dosyası kuralları çıkış veri dosyalarınızı adlandırmak için standart karar olup olmadığını gösterir. Ancak, istediğiniz hello Hedef kapsayıcıyı ve blob adı verebilirsiniz. Merhaba dosyası kuralları standart çıktı dosyalarını adlandırma için kullandığınız sonra çıktı dosyalarınızı hello görüntülenmek için kullanılabilir [Azure portal][portal].

Merhaba dosyası kuralları standart kullanabileceğiniz birkaç farklı yolu vardır:

- Merhaba Batch hizmeti API toopersist çıktı dosyaları kullanıyorsanız, tooname hedef kapsayıcılar ve bloblar toohello dosyası kuralları standart göre seçebilirsiniz. Merhaba Batch hizmeti API'si, istemci kodu toopersist çıktı dosyalarını görev uygulamanızı değiştirmeden sağlar.
- .NET ile geliştiriyorsanız hello kullanabilirsiniz [.NET için Azure toplu işlem dosyası kuralları Kitaplığı][nuget_package]. Bu kitaplığı kullanarak bir avantajı tootheir kimliği veya amaca göre çıktı dosyaları sorgulama destekliyorsa olmasıdır. Merhaba yerleşik Sorgulama işlevi kolay tooaccess çıktı dosyalarını bir istemci uygulaması veya diğer görevler kolaylaştırır. Ancak, görev uygulamanızı değiştirilmiş toocall dosyası kuralları kitaplığı olmalıdır. Daha fazla bilgi için bkz: hello başvurusu hello için [dosyası kuralları kitaplığı için .NET](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.aspx).
- .NET dışında bir dil ile geliştiriyorsanız hello dosyası kuralları uygulamanızda standart uygulayabilirsiniz.

## <a name="design-considerations-for-persisting-output"></a>Kalıcı çıktı için tasarım konuları 

Batch çözümünüzü tasarlarken, ilgili toojob hello aşağıdaki Etkenler ve görev çıktıları verilebilir göz önünde bulundurun.

* **İşlem düğümü ömrü**: düğümleri genellikle geçici, özellikle otomatik ölçeklendirme özellikli havuzlarında işlem. Bir düğüm üzerinde çalışan bir görev çıktısını yalnızca hello düğüm var ve yalnızca hello dosya saklama dönemi içinde hello görev için ayarladığınız sırada kullanılabilir. Bir görev hello görev tamamlandıktan sonra gerekli olabilecek bir çıktı oluşturursa hello görev çıktısı, dosyaları tooa dayanıklı depolama Azure depolama gibi yüklemeniz gerekir.

* **Çıktı depolama**: görev çıktısı için bir veri deposu olarak Azure Storage önerilir, ancak herhangi dayanıklı bir depolama alanı kullanabilirsiniz. Görev çıktı tooAzure yazma depolama Batch hizmeti API'si hello tümleştirilmiştir. Başka bir form dayanıklı depolama kullanırsanız, toowrite hello uygulama mantığını toopersist görev çıktısı kendiniz gerekir.   

* **Çıktı alma**: görev çıktısı kalıcı varsa, havuzdaki işlem düğümleri hello doğrudan ya da Azure Storage veya başka bir veri deposundan görev çıktısını alabilirsiniz. tooretrieve görev animasyonun çıktı bir işlem düğümden doğrudan hello dosya adı ve çıkış konumunu hello düğümde gerekir. Görev çıktı tooAzure depolama devam ederse, Azure Storage toodownload hello çıktı dosyaları hello Azure depolama SDK'sı ile Merhaba tam yolu toohello dosyasında gerekir.

* **Çıktı görüntüleme**: hello Azure portal ve select tooa Batch görevinde gidin zaman **dosyaları düğümde**hello görev ile ilişkili tüm dosyalar ile sunulan, yalnızca ilgilendiğiniz çıktı dosyaları hello. Yeniden, işlem düğümlerinde dosyaları yalnızca hello düğüm varsa ve yalnızca hello dosyayı elde tutma süresi içinde hello görev için ayarladığınız sırada kullanılabilir. tooview görev çıktısını tooAzure depolama kalıcı, hello Azure portalında veya Azure Storage istemci uygulamanın hello gibi kullanabilirsiniz [Azure Storage Gezgini][storage_explorer]. Azure storage'da veri hello portal ya da başka bir aracıyla tooview çıktı, hello dosyanın konumunu bilmeniz ve tooit doğrudan gidin.

## <a name="options-for-persisting-output"></a>Kalıcı çıkış seçenekleri

Senaryonuza bağlı olarak, toopersist görev çıktısını yapabileceğiniz birkaç farklı yaklaşım vardır:

- Merhaba Batch hizmeti API kullanın.  
- Merhaba toplu iş dosyası kuralları kitaplığı için .NET kullanın.  
- Merhaba, uygulamanızda standart toplu işlem dosyası kuralları uygular.
- Bir özel dosya taşıma çözüm uygulayabilirsiniz.

Aşağıdaki bölümlerde hello her iki yaklaşımın daha ayrıntılı açıklanmıştır.

### <a name="use-hello-batch-service-api"></a>Merhaba Batch hizmeti API'si kullanın

2017-05-01 sürümüyle hello Batch hizmeti için görev verileri Azure depolama alanında çıktı dosyaları belirtmek için destek ekler olduğunda, [görev tooa işi eklemek](https://docs.microsoft.com/rest/api/batchservice/add-a-task-to-a-job) veya [görevleri tooa iş koleksiyonu eklemek](https://docs.microsoft.com/rest/api/batchservice/add-a-collection-of-tasks-to-a-job).

Merhaba Batch hizmeti API'si kalıcı görev veri tooan hello sanal makine yapılandırması ile oluşturulan havuzlarından Azure depolama hesabı destekler. Merhaba Batch hizmeti API'si göreviniz çalıştıran Merhaba uygulaması değiştirmeden görev veri devam edebilir. İsteğe bağlı olarak toohello uyması [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) hello dosyalarını adlandırma için tooAzure depolama kalır. 

Çıkış hello Batch hizmeti API'si toopersist görev kullanın:

- Toplu iş görevleri ve iş yöneticisi görevleri hello sanal makine yapılandırması ile oluşturulan havuzlarında toopersist veri istiyor.
- Toopersist veri tooan Azure Storage kapsayıcısı rasgele bir ada sahip istiyor.
- Toopersist veri tooan Azure Storage kapsayıcısı according toohello adlı istediğiniz [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

> [!NOTE]
> Merhaba Batch hizmeti API'si hello bulut hizmeti yapılandırması ile oluşturulan havuzlarında çalışan görevler kalıcı verileri desteklemez. Merhaba cloud services yapılandırması çalıştıran havuzlarından çıktı kalıcı görev hakkında daha fazla bilgi için bkz: [iş ve görev veri tooAzure depolama hello toplu iş dosyası kuralları kitaplığı için .NET toopersist Sürdür](batch-task-output-file-conventions.md)
> 
> 

Merhaba Batch hizmeti API'si ile kalıcı görev çıktısını hakkında daha fazla bilgi için bkz: [hello Batch hizmeti API'si ile görev veri tooAzure depolama kalıcı](batch-task-output-files.md). Ayrıca bkz. hello [PersistOutputs] [github_persistoutputs] Örnek Proje nasıl toodurable depolama toouse hello toplu istemci kitaplığı için .NET toopersist görev çıktısını gösterir github'dan edinilebilir.

### <a name="use-hello-batch-file-conventions-library-for-net"></a>.NET için Hello toplu iş dosyası kuralları kitaplığını kullanma

C# ve .NET ile toplu çözümler derleme geliştiricileri hello kullanabilir [dosyası kuralları kitaplığı için .NET] [ nuget_package] toopersist görev veri tooan toohello göre Azure depolama hesabı [toplu iş dosyası Kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Hello dosyası kuralları kitaplığı taşıma çıktı dosyaları tooAzure depolama ve adlandırma hedef kapsayıcılar ve bloblar iyi bilinen bir şekilde işler.

Merhaba dosyası kuralları kitaplığı destekler, çıktı dosyalarını kimliği veya amaca göre sorgulama kolay toolocate yaparak bunları hello gerek olmadan dosya URI'ler tamamlayın. 

Merhaba toplu iş dosyası kuralları kitaplığı için .NET toopersist Görev çıkış kullanın:

- Merhaba görev çalışmaya devam ederken toostream veri tooAzure depolama istiyor.
- Merhaba bulut hizmet yapılandırması veya hello sanal makine yapılandırması ile oluşturulan havuzlarından toopersist veri istiyor.
- İstemci uygulamanız veya diğer görevler hello gereksinimlerini toolocate iş ve Görev çıkış dosyalarını Kimliğine göre veya amacına göre yükleyin. 
- İlk sonuçları tooperform onay işaret eden veya erken karşıya istiyor.
- Hello Azure portal tooview Görev çıkış istiyor.

.NET için kalıcı görev çıktısını hello dosyası kuralları Kitaplığı hakkında daha fazla bilgi için bkz: [iş ve görev veri tooAzure depolama hello toplu iş dosyası kuralları kitaplığı için .NET toopersist kalıcı ](batch-task-output-file-conventions.md). Ayrıca bkz. hello [PersistOutputs] [github_persistoutputs] Örnek Proje nasıl toodurable depolama toouse hello dosyası kuralları kitaplığı için .NET toopersist görev çıktısını gösterir github'dan edinilebilir.

Merhaba [PersistOutputs] [github_persistoutputs] Örnek Proje github'da nasıl toodurable depolama toouse hello toplu istemci kitaplığı için .NET toopersist görev çıktısını gösterir.

### <a name="implement-hello-batch-file-conventions-standard"></a>Merhaba toplu iş dosyası kuralları standart uygulama

.NET dışında bir dil kullanıyorsanız, hello uygulayabileceğiniz [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) kendi uygulamanızda. 

Tooimplement hello dosyası kuralları adlandırma standardı kendiniz kanıtlanmış adlandırma şeması istediğinizde ya da tooview görev çıktısını hello Azure portal'ın istediğinizde isteyebilirsiniz.

### <a name="implement-a-custom-file-movement-solution"></a>Bir özel dosya taşıma çözümü

Ayrıca kendi tam dosya taşıma çözümü uygulayabilirsiniz. Bu yaklaşımını durumlarda kullanın:

- Azure Storage dışındaki toopersist görev veri tooa veri deposu istiyor. tooupload dosyaları tooa veri deposu Azure SQL veya Azure DataLake gibi bir özel komut dosyası veya yürütülebilir tooupload toothat konum oluşturabilirsiniz. Ardından hello komut satırında birincil yürütülebilir dosyanın çalıştırdıktan sonra çağırabilirsiniz. Örneğin, bir Windows düğümünde, şu iki komutu deniyor olabilir:`doMyWork.exe && uploadMyFilesToSql.exe`
- İlk sonuçları tooperform onay işaret eden veya erken karşıya istiyor.
- Hata işleme üzerinde ayrıntılı denetim toomaintain istiyor. Örneğin, tooimplement toouse görev bağımlılık Eylemler tootake belirli isterseniz kendi çözüm belirli görev çıkış kodları üzerinde temel eylemleri karşıya yüklemek isteyebilirsiniz. Görev bağımlılık eylemleri hakkında daha fazla bilgi için bkz: [görev bağımlılıkları diğer görevlere bağlı toorun görevler oluşturma](batch-task-dependencies.md). 

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba Batch hizmeti API'si toopersist görev verilerini Hello yeni özellikleri kullanma keşfedin [hello Batch hizmeti API'si ile görev veri tooAzure depolama kalıcı](batch-task-output-files.md).
- .NET için Hello toplu iş dosyası kuralları kitaplığını kullanma hakkında bilgi edinin [iş ve görev veri tooAzure depolama hello toplu iş dosyası kuralları kitaplığı için .NET toopersist kalıcı ](batch-task-output-file-conventions.md).
- Merhaba [PersistOutputs] [github_persistoutputs] bkz nasıl toouse her ikisi de hello toplu istemci kitaplığı için .NET ve .NET toopersist görev için hello dosyası kuralları Kitaplığı gösteren GitHub üzerinde örnek proje çıktı toodurable depolama.

[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/
