---
title: "aaaUse Azure Batch API'lerini ve araçları toodevelop büyük ölçekli paralel işlem çözümleri | Microsoft Docs"
description: "Merhaba API'leri ve hello Azure Batch hizmetiyle çözümleri geliştirmek için kullanılabilen araçlar hakkında bilgi edinin."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Batch API'lerine ve araçlarına genel bakış

Azure Batch ile paralel iş yüklerini işlemek genellikle yapılır program aracılığıyla hello birini kullanarak [Batch API'lerini](#batch-development-apis). İstemci uygulamanız veya hizmetiniz hello Batch API'lerini toocommunicate hello Batch hizmeti ile kullanabilirsiniz. Merhaba Batch API'lerini oluşturabilir ve işlem düğümü havuzlarını Yönet sanal makineleri veya Bulut Hizmetleri. Ardından bu düğümlerde işler ve görevler toorun zamanlayabilirsiniz. 

Verimli bir şekilde, kuruluşunuz için büyük ölçekli iş yüklerini işlemek veya bunlar işler ve görevler--istek üzerine veya planlı tek, yüzlerce veya hatta binlerce çalıştırabilmeniz için bir hizmet ön ucu tooyour müşteriler sağlayın. [Azure Data Factory](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json) gibi araçlarla yönetilen Azure Batch'i daha büyük bir iş akışının parçası olarak da kullanabilirsiniz.

> [!TIP]
> Hazır olduğunuzda toohello toplu işlem API toodig hello daha kapsamlı bir anlayış özelliklerine sağlar, hello denetleyin [geliştiriciler için Batch özelliklerine genel bakış](batch-api-basics.md).
> 
> 

## <a name="azure-accounts-for-batch-development"></a>Batch geliştirme için Azure hesapları
Batch çözümleri geliştirdiğinizde, Microsoft Azure hesapları aşağıdaki hello kullanacaksınız.

* **Azure hesabı ve aboneliği** -Henüz Azure aboneliğiniz yoksa [MSDN abone avantajlarınızı][msdn_benefits] etkinleştirebilir veya [ücretsiz Azure hesabı][free_account] için kaydolabilirsiniz. Hesap oluşturduğunuzda sizin için varsayılan bir abonelik oluşturulur.
* **Batch hesabı** - Havuzlar, işlem düğümleri, işler ve görevler gibi bir Azure Batch hesabıyla ilişkilendirilmiş Azure Batch kaynakları. Uygulamanızı hello Batch hizmeti karşı bir istekte bulunduğunda hello Azure toplu işlem hesabı adı, hello hesap hello URL'sini ve bir erişim anahtarı kullanarak hello isteğin kimliğini doğrular. Yapabilecekleriniz [Batch hesabı oluşturma](batch-account-create-portal.md) hello Azure Portalı'nda.
* **Depolama hesabı** - Batch’te [Azure Depolama][azure_storage] dosyalarıyla çalışmak için yerleşik destek bulunur. Neredeyse her Batch senaryosu, görevlerinizin çalıştığı hello programları ve işledikleri hello verileri hazırlama ve oluşturdukları Çıktı verilerinin hello depolama için Azure Blob Depolama kullanır. toocreate bir depolama hesabı bkz [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).

## <a name="batch-service-apis"></a>Batch hizmeti API’leri

Uygulamaları ve Hizmetleri doğrudan REST API çağrıları yayımlayabilir veya bir veya daha fazla istemci kitaplıkları toorun aşağıdaki hello kullanın ve Azure Batch iş yükü yönetebilirsiniz.

| API | API başvurusu | İndir | Öğretici | Kod örnekleri | Daha Fazla Bilgi |
| --- | --- | --- | --- | --- | --- |
| **Batch REST** |[MSDN][batch_rest] |Yok |- |- | [Desteklenen Sürümler](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **Batch .NET** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[Öğretici](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [Sürüm notları](http://aka.ms/batch-net-dataplane-changelog) |
| **Batch Python** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[Öğretici](batch-python-tutorial.md)|[GitHub][api_sample_python] | [Benioku](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Batch Node.js** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [Benioku](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Batch Java** |[github.io][api_java] |[Maven][api_java_jar] |- |[Benioku][api_sample_java] | [Benioku](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>Batch Yönetimi API’leri

Merhaba toplu işlemi için Azure Resource Manager API'leri tooBatch hesapları programlı erişim sağlar. Bu API'leri kullanarak, Batch hesaplarını, kotalarını ve uygulama paketlerini programlı olarak yönetebilirsiniz.  

| API | API başvurusu | İndir | Öğretici | Kod örnekleri |
| --- | --- | --- | --- | --- |
| **Batch Resource Manager REST** |[docs.microsoft.com][api_rest_mgmt] |Yok |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **Batch Resource Manager .NET** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [Öğretici](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Batch komut satırı araçları

Bu komut satırı araçları sağlayan Batch hizmeti ve toplu işlem yönetimi API'leri hello gibi aynı işlevselliği hello: 

* [Batch PowerShell cmdlet'leri][batch_ps]: hello Azure Batch cmdlet'leri hello [Azure PowerShell](/powershell/azure/overview) modülü PowerShell ile Batch kaynaklarını toomanage etkinleştirin.
* [Azure CLI](/cli/azure/overview): hello Azure komut satırı arabirimi (Azure CLI) olan hello Batch hizmeti ve toplu yönetim hizmeti de dahil olmak üzere çok sayıda Azure hizmetiyle etkileşim için Kabuk komutları sağlayan platformlar arası bir araç takımı. Bkz: [Azure CLI ile yönetme Batch kaynaklarını](batch-cli-get-started.md) toplu işlemle hello Azure CLI kullanma hakkında daha fazla bilgi için.

## <a name="other-tools-for-application-development"></a>Uygulama geliştirme için diğer araçlar

Batch uygulamalarınızı ve hizmetlerinizi oluşturmak ve bunlarda hata ayıklamak için yararlı olabilecek bazı ek araçlar şunlardır:

* [Azure portal][portal]: oluşturma, izlemek ve toplu havuzlar, işler ve görevler hello Azure'nın Sil portal'ın toplu Kanatlar. İşleriniz çalıştırın ve hatta dosyalarını hello işlem düğümleri, havuzlarınızı karşıdan yükleme sırasında bu ve diğer kaynakları hello durum bilgilerini görüntüleyebilirsiniz. Örneğin, sorun giderme sırasında başarısız bir görevin `stderr.txt` öğesini indirebilirsiniz. Ayrıca, Uzak Masaüstü (RDP) dosyalarını toocompute düğümler toolog kullanabileceğiniz indirebilirsiniz.
* [Azure Batch Gezgini][batch_explorer]: Batch Gezgini Azure portal hello gibi ancak tek başına bir Windows Presentation Foundation (WPF) istemci uygulaması benzer Batch kaynak yönetimi işlevselliği sağlar. Merhaba Batch .NET örnek uygulamalarından birini [GitHub][github_samples], Visual Studio 2015 ile veya yapı ve toobrowse kullanın ve geliştirme sırasında hello kaynakları Batch hesabınızda yönetmek kullanabilirsiniz ve Batch çözümlerinizi hata ayıklama. Görünüm işi, havuzu ve görev ayrıntılarını işlem düğümleri dosyalarını indirmek ve toonodes Batch Gezgini ile indirebilirsiniz Uzak Masaüstü (RDP) dosyalarını kullanarak uzaktan bağlanma.
* [Microsoft Azure Storage Gezgini][storage_explorer]: Batch çözümlerinizi geliştirdiğiniz ve kesinlikle olmadığında bir Azure Batch aracı hello Depolama Gezgini başka bir değerli bir araç toohave boştur.

## <a name="additional-resources"></a>Ek kaynaklar

- toolearn toplu uygulamanızdan olayları günlüğe kaydetmeyi hakkında bkz [oturum tanılama değerlendirme ve toplu çözümlerini izleme olaylarını](batch-diagnostics.md). Merhaba Batch hizmeti tarafından başlatılan olayları üzerinde bir başvuru için bkz: [toplu analizi](batch-analytics.md).
- İşlem düğümlerine yönelik ortam değişkenleri hakkında bilgi için bkz. [Azure Batch işlem düğümü ortam değişkenleri](batch-compute-node-environment-variables.md).

## <a name="next-steps"></a>Sonraki adımlar

* Okuma hello [geliştiriciler için Batch özelliklerine genel bakış](batch-api-basics.md), önemli bilgiler herkesin toouse toplu hazırlanıyor. Merhaba makale Batch uygulamanızı oluştururken kullanabileceğiniz birçok API özellikleri Batch hizmeti kaynak havuzları, düğümleri, işler ve görevler ve hello gibi hakkında daha ayrıntılı bilgi içerir.
* [.NET için Hello Azure Batch kitaplığını kullanmaya başlama](batch-dotnet-get-started.md) toolearn nasıl toouse C# ve Batch .NET kitaplığı tooexecute ortak bir toplu iş akışı kullanarak basit bir iş yükü hello. Bu makalede nasıl toouse hello Batch hizmeti öğrenme sırasında ilk duraklarınızdan biri olmalıdır. Ayrıca bir [Python sürümü](batch-python-tutorial.md) hello Öğreticisi.
* Merhaba karşıdan [github'daki kod örnekleri] [ github_samples] nasıl hem C# ve Python arabirim toplu tooschedule ve işlem örnek iş yükleri ile toosee.
* Merhaba denetleyin [Batch öğrenme yolu] [ learning_path] tooget hello kaynakları kullanılabilir tooyou yazarken hakkında bir fikir toowork toplu ile bilgi edinin.


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
