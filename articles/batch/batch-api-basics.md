---
title: "Geliştiriciler için Azure batch aaaOverview | Microsoft Docs"
description: "Merhaba hello Batch hizmeti özelliklerini ve API'lerini geliştirme açısından öğrenin."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 416b95f8-2d7b-4111-8012-679b0f60d204
ms.service: batch
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3da9d82572b28d05d1923166bd08c26725ca3316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>Batch içe büyük ölçekli paralel işlem çözümleri geliştirme

Bu genel bakışta hello çekirdek hello Azure Batch Hizmeti bileşenlerinin biz hello birincil hizmetler ele alınmaktadır ve çözümleri işlem kaynaklarını Batch geliştiricilerinin büyük ölçekli paralel toobuild kullanabilirsiniz.

Dağıtılmış hesaplama Uygulama geliştirirken mı hizmetine doğrudan sorunları [REST API] [ batch_rest_api] çağrıları kullanan bir hello [Batch SDK'ları](batch-apis-tools.md#azure-accounts-for-batch-development), kullanacağınız Çoğu hello kaynakları ve bu makalede ele alınan özellikleri.

> [!TIP]
> Bir üst düzey giriş toohello için Batch hizmeti, bkz: [Azure Batch temel bilgileri](batch-technical-overview.md).
>
>

## <a name="batch-service-workflow"></a>Batch hizmeti iş akışı
Merhaba aşağıdaki üst düzey iş akışı tipik neredeyse tüm uygulamalar ve paralel iş yüklerini işlemek için hello Batch hizmetini kullanan hizmetler:

1. Merhaba karşıya **veri dosyalarını** tooprocess tooan istediğiniz [Azure Storage] [ azure_storage] hesabı. Toplu Azure Blob depolama alanına erişim için yerleşik destek içerir ve görevleriniz bu dosyaları çok indirebilirsiniz[işlem düğümleri](#compute-node) hello görevler çalıştırıldığında.
2. Merhaba karşıya **uygulama dosyalarını** , görevlerinizin çalıştıracağı. Bu dosyalar ikili dosyaları veya komut dosyaları ve onların bağımlılıkları olabilir ve hello görevler tarafından yürütülür. Görevleriniz bu dosyaları Storage hesabınızdan yükleyebilirsiniz ya da hello kullanabilirsiniz [uygulama paketleri](#application-packages) uygulama yönetimi ve dağıtımı için Toplu özellik.
3. Bir işlem düğümleri [havuzu](#pool) oluşturun. Bir havuz oluşturduğunuzda hello hello havuzu, boyutu ve hello işletim sistemi için işlem düğümü sayısını belirtin. İşinizdeki her görev çalıştığında, atanan havuzunuzdaki hello düğümlerin birinde tooexecute.
4. Bir [iş](#job) oluşturun. İş bir görev koleksiyonunu yönetir. Burada, işin görevlerinin çalışacağı her iş tooa belirli bir havuzu ilişkilendirin.
5. Ekleme [görevleri](#task) toohello işi. Her görev Merhaba uygulaması ya da depolama hesabınızdan indirdiği tooprocess hello veri dosyalarını karşıya komut dosyasını çalıştırır. Her görev tamamlandığında, çıkış tooAzure depolama karşıya yükleyebilirsiniz.
6. İşin ilerleme durumunu izleyin ve hello görev çıktısını Azure Depolama'dan alın.

Merhaba aşağıdaki bölümlerde bu ele almaktadır ve dağıtılmış hesaplama senaryonuzu olanaklı diğer kaynakları batch hello.

> [!NOTE]
> Gereksinim duyduğunuz bir [Batch hesabı](#account) toouse hello Batch hizmeti. Ayrıca, Batch çözümlerinin çoğunda dosya depolama ve alma işlemleri için bir [Azure Depolama][azure_storage] hesabı kullanılır. Batch şu anda yalnızca hello destekler **genel amaçlı** 5. adımda açıklandığı gibi depolama hesabı türü, [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) içinde [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).
>
>

## <a name="batch-service-resources"></a>Batch hizmet kaynakları
Aşağıdaki kaynaklardan--hesaplar, hello bazıları hesaplamak için düğümleri, havuzlar, işler ve görevler--hello Batch hizmetini kullanan tüm çözümler için gereklidir. İş zamanlamaları ve uygulama paketleri gibi diğer özellikler de faydalıdır, ancak isteğe bağlıdır.

* [Hesap](#account)
* [İşlem düğümü](#compute-node)
* [Havuz](#pool)
* [İş](#job)

  * [İş zamanlamaları](#scheduled-jobs)
* [Görev](#task)

  * [Başlangıç görevi](#start-task)
  * [İş yöneticisi görevi](#job-manager-task)
  * [İş hazırlama ve bırakma görevleri](#job-preparation-and-release-tasks)
  * [Çok örnekli görev (MPI)](#multi-instance-tasks)
  * [Görev bağımlılıkları](#task-dependencies)
* [Uygulama paketleri](#application-packages)

## <a name="account"></a>Hesap
Batch hesabı Batch hizmeti hello içinde benzersiz şekilde tanımlanan bir varlıktır. Tüm işlemler bir Batch hesabıyla ilişkilendirilir.

Hello kullanarak bir Azure Batch hesabı oluşturma [Azure portal](batch-account-create-portal.md) veya programlı olarak gibi hello ile [Batch yönetimi .NET kitaplığı](batch-management-dotnet.md). Merhaba hesap oluştururken, bir Azure depolama hesabı ilişkilendirebilirsiniz.

### <a name="pool-allocation-mode"></a>Havuz ayırma modu

Bir Batch hesabı oluşturduğunuzda, işlem düğümleri [havuzlarının](#pool) nasıl ayrılacağını belirtebilirsiniz. Azure Batch tarafından yönetilen bir abonelikte işlem düğümleri havuzlarının tooallocate seçebilir veya kendi abonelikte tahsis edebilirsiniz. Merhaba *havuzu ayırma modu* hello hesap için özelliği belirler havuzları burada ayrılır. 

ayırma modu toouse havuz toodecide, senaryonuza en uygun göz önünde bulundurun:

* **Batch hizmeti**: Batch hizmeti olduğundan, havuzları ayrılır abonelikleri Azure tarafından yönetilen hello görünümlerde arkasında hello varsayılan havuzu ayırma modu,. Merhaba Batch hizmeti havuzu ayırma modu hakkında aşağıdaki önemli noktaları göz önünde bulundurun:

    - Bulut hizmeti ve sanal makine havuzları Hello Batch hizmeti havuzu ayırma modu destekler.
    - Merhaba Batch hizmeti havuzu ayırma modunu destekleyen her iki paylaşılan anahtar kimlik doğrulaması veya [Azure Active Directory kimlik doğrulaması](batch-aad-auth.md) (Azure AD). 
    - Ya da ayrılmış veya düşük öncelikli işlem düğümleri havuzları hello Batch hizmeti havuzu ayırma moduyla ayrılan kullanabilirsiniz.
    - Merhaba Batch hizmeti havuzu ayırma modu toocreate Azure sanal makine özel VM görüntüleri havuzlarından düşünüyorsanız veya toouse bir sanal ağ planlıyorsanız kullanmayın. Hesabınızı hello kullanıcı abonelik havuzu ayırma moduyla oluşturun.
    - Sanal makine havuzları hello Batch hizmeti havuzu ayırma modu kullanılarak oluşturulmuş bir hesap sağlanan oluşturulur, gelen [Azure Virtual Machines Marketi] [ vm_marketplace] görüntüler.

* **Kullanıcı aboneliği**: hello kullanıcı abonelik havuzu ayırma moduyla, Batch havuzları hello hello hesabın oluşturulduğu Azure abonelik ayrılır. Merhaba kullanıcı abonelik havuzu ayırma modu hakkında aşağıdaki önemli noktaları göz önünde bulundurun:
     
    - Merhaba kullanıcı abonelik havuzu ayırma modu yalnızca sanal makine havuzları destekler. Cloud Services havuzlarını desteklemez.
    - Sanal makine havuzlarıyla toocreate sanal makine havuzları özel VM görüntüleri veya toouse bir sanal ağ hello kullanıcı abonelik havuzu ayırma modu kullanmanız gerekir.  
    - Kullanmalısınız [Azure Active Directory kimlik doğrulaması](batch-aad-auth.md) havuzlarıyla hello kullanıcı abonelikte ayrılır. 
    - Merhaba havuzu ayırma modu tooUser abonelik ayarlarsanız, toplu işlem hesabı için bir Azure anahtar kasası ayarlamanız gerekir. 
    - Yalnızca adanmış bir işlem düğümleri havuzları hello kullanıcı abonelik havuzu ayırma modu kullanılarak oluşturulmuş bir hesap kullanabilirsiniz. Düşük öncelikli düğümler desteklenmez.
    - Bir hesap hello kullanıcı abonelik havuzu ayırma modu ile sağlanan sanal makine havuzları herhangi birinden oluşturulabilir [Azure Virtual Machines Marketi] [ vm_marketplace] görüntüleri veya özel, görüntüleri sağlar.

Aşağıdaki tablonun hello hello Batch hizmeti ve kullanıcı abonelik havuzu ayırma modları karşılaştırır.

| **Havuz ayırma modu**                 | **Batch Hizmeti**                                                                                       | **Kullanıcı Aboneliği**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Havuzların ayrıldığı yer**               | Azure tarafından yönetilen bir abonelik                                                                           | Merhaba kullanıcı aboneliği hello toplu işlem hesabı oluşturulur                        |
| **Desteklenen yapılandırmalar**             | <ul><li>Bulut Hizmeti Yapılandırması</li><li>Sanal Makine Yapılandırması (Linux ve Windows)</li></ul> | <ul><li>Sanal Makine Yapılandırması (Linux ve Windows)</li></ul>                |
| **Desteklenen VM görüntüleri**                  | <ul><li>Microsoft Azure Market görüntüleri</li></ul>                                                              | <ul><li>Microsoft Azure Market görüntüleri</li><li>Özel görüntüler</li></ul>                   |
| **Desteklenen işlem düğümü türleri**         | <ul><li>Ayrılmış düğümler</li><li>Düşük öncelikli düğümler</li></ul>                                            | <ul><li>Ayrılmış düğümler</li></ul>                                                  |
| **Desteklenen kimlik doğrulaması**             | <ul><li>Paylaşılan Anahtar</li><li>Azure AD</li></ul>                                                           | <ul><li>Azure AD</li></ul>                                                         |
| **Azure Key Vault gereksinimi**             | Hayır                                                                                                      | Evet                                                                                |
| **Çekirdek kota**                           | Batch çekirdek kotasına göre belirlenir                                                                          | Abonelik çekirdek kotasına göre belirlenir                                              |
| **Azure Sanal Ağ desteği** | Bulut hizmeti yapılandırması Hello ile oluşturulan havuzu                                                      | Sanal Makine Yapılandırması Hello ile oluşturulan havuzu                               |
| **Desteklenen sanal ağ dağıtım modeli**      | Klasik dağıtım modeli kullanılarak oluşturulmuş sanal ağlar                                                             | Merhaba Klasik dağıtım modeli veya Azure Resource Manager ile oluşturulan sanal ağlar |

## <a name="azure-storage-account"></a>Azure Storage hesabı

Batch çözümlerinin çoğu, kaynak dosyalarını ve çıkış dosyalarını depolamak için Azure Depolama kullanır.  

Toplu 5. adımda açıklandığı gibi yalnızca hello genel amaçlı depolama hesabı türü, şu anda destekler [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) içinde [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md). Batch görevleriniz (standart görevler, başlangıç görevleri, iş hazırlama görevleri ve iş sürüm görevleri dahil), yalnızca genel amaçlı depolama hesaplarında yer alan kaynak dosyalarını belirtmelidir.


## <a name="compute-node"></a>İşlem düğümü
Bir işlem düğümünde bir Azure sanal makine (VM) ya da bulut hizmeti ayrılmış tooprocessing, uygulama İş yükünüzün bir kısmını olduğundan VM ' dir. bir düğümün başlangıç boyutu hello sayısını CPU çekirdekleri, bellek kapasitesi ve toohello düğüme ayrılan yerel dosya sistemi boyutunu belirler. Azure bulut Hizmetleri, hello görüntülerden kullanarak Windows veya Linux düğümleri havuzları oluşturabilirsiniz [Azure Virtual Machines Marketi][vm_marketplace], veya hazırlamanız özel görüntüler. Merhaba aşağıdakilere bakın [havuzu](#pool) bölümde bu seçenekler hakkında daha fazla bilgi için.

Düğümler, herhangi bir yürütülebilir dosya veya hello düğümünün hello işletim sistemi ortamı tarafından desteklenen betik çalıştırabilir. Buna Windows için \*.exe, \*.cmd, \*.bat ve PowerShell komut dosyaları ile Linux için ikili dosyalar, kabuk ve Python komut dosyaları dahildir.

Batch içindeki tüm işlem düğümleri ayrıca şunları içerir:

* Standart bir [klasör yapısı](#files-and-directories) ve görevlere göre başvurulabilen ilişkili [ortam değişkenleri](#environment-settings-for-tasks).
* **Güvenlik Duvarı** ayarları yapılandırılmış toocontrol erişim.
* [Uzaktan erişim](#connecting-to-compute-nodes) tooboth (Uzak Masaüstü Protokolü (RDP)) Windows ve Linux (güvenli Kabuk (SSH)) düğüm.

## <a name="pool"></a>Havuz
Havuz, uygulamanızın üzerinde çalıştığı bir düğüm koleksiyonudur. Merhaba iş toobe bitti belirttiğinizde hello havuzu el ile sizin tarafınızdan veya hello Batch hizmeti tarafından otomatik olarak oluşturulabilir. Oluşturun ve uygulamanızı hello kaynak gereksinimlerini karşılayan bir havuz yönetin. Bir havuzu içinde oluşturulduğu yalnızca hello Batch hesabı tarafından kullanılabilir. Bir Batch hesabı birden fazla havuza sahip olabilir.

Azure Batch havuzları hello temel Azure işlem platformu üzerine oluşturulur oluşturun. Büyük ölçekli ayırma, uygulama yüklemesi, veri dağıtımı, sistem durumu izleme ve hello havuzdaki işlem düğümü sayısının esnek şekilde ayarlanmasını sağlayın ([ölçeklendirme](#scaling-compute-resources)).

Tooa havuza eklenen her düğüme benzersiz bir ad ve IP adresi atanır. Bir düğüm havuzdan kaldırıldığında toohello işletim sistemi ya da dosyalara yapılan tüm değişiklikler kaybedilir ve ad ve IP adresi gelecekte kullanım için boşta kalır. Bir düğüm havuzdan ayrıldığında ömrü sona erer.

Bir havuz oluşturduğunuzda aşağıdaki öznitelikleri hello belirtebilirsiniz. Itanium tabanlı sistemler için hello havuzu ayırma modu hello toplu olarak bağlı olarak bazı ayarları, farklı [hesap](#account):

- İşlem düğümü işletim sistemi ve sürümü
- İşlem düğümü türü ve hedef düğüm sayısı
- Merhaba işlem düğümlerinin boyutu
- Ölçeklendirme ilkesi
- Görev zamanlama ilkesi
- İşlem düğümlerinin iletişim durumu
- İşlem düğümleri için başlangıç görevleri
- Uygulama paketleri
- Ağ yapılandırması

Bu ayarların her biri aşağıdaki bölümlerde hello daha ayrıntılı açıklanmıştır.

> [!IMPORTANT]
> Toplu işlem hesaplarını Hello Batch hizmeti havuzu ayırma moduyla oluşturulan çekirdek toplu işlem hesabı ile Merhaba sayısını sınırlayan bir varsayılan kota sahip. Çekirdek sayısı Hello toohello işlem düğümü sayısını karşılık gelir. Merhaba varsayılan kotalar ve yönergeleri hakkında çok bulabileceğiniz[kota artırma](batch-quota-limit.md#increase-a-quota) içinde [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md). Havuzunuzu, düğümlerin hedef sayısını elde değil hello çekirdek kotası hello neden olabilir.
>
>Toplu işlem hesaplarını Hello kullanıcı abonelik havuzu ayırma moduyla oluşturulan hello Batch Hizmeti kotaları Gözlemleme. Bunun yerine, hello paylaştıkları hello için çekirdek kota belirtilen abonelik. Daha fazla bilgi için [Azure aboneliği ve hizmet limitleri, kotalar ve kısıtlamalar](../azure-subscription-service-limits.md) sayfasındaki [Sanal Makine limitleri](../azure-subscription-service-limits.md#virtual-machines-limits) bölümüne bakın.
>
>

### <a name="compute-node-operating-system-and-version"></a>İşlem düğümü işletim sistemi ve sürümü

Bir Batch havuzu oluşturduğunuzda, hello Azure sanal makine yapılandırma ve işletim sistemi hello havuzundaki her işlem düğümünde toorun istediğiniz hello türünü belirtebilirsiniz. Merhaba iki yapılandırmaları toplu işlemde kullanılabilir türleri şunlardır:

- Merhaba **sanal makine yapılandırması**, hello havuzun belirten Azure sanal makinelerden oluşur. Bu VM'ler Linux veya Windows görüntülerinden oluşturulabilir. 

    Sanal Makine Yapılandırması hello üzerinde dayalı bir havuz oluşturduğunuzda yalnızca hello boyutu hello düğümlerinin ve hello kullanılan görüntüleri toocreate hello kaynağını bunları, aynı zamanda hello belirtmeniz gerekir **sanal makine görüntü başvurusunu** ve hello Toplu **düğümü aracı SKU'sunu** toobe hello düğümlerinde yüklü. Bu havuz özelliklerini belirtme hakkında daha fazla bilgi için bkz. [Azure Batch havuzlarında Linux işlem düğümlerini hazırlama](batch-linux-nodes.md).

- Merhaba **Cloud Services Yapılandırması**, o hello havuzu belirten Azure Cloud Services düğümleri oluşur. Cloud Services *yalnızca* Windows işlem düğümleri sunar.

    Cloud Services yapılandırması havuzları için kullanılabilen işletim sistemleri hello listelenen [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](../cloud-services/cloud-services-guestos-update-matrix.md). Cloud Services düğümleri içeren bir havuz oluşturduğunuzda toospecify hello düğüm boyutu gerekir ve kendi *işletim sistemi ailesi*. Bulut Hizmetleri, dağıtılan tooAzure Windows üzerinde çalışan sanal makinelere daha hızlı bir şekilde oluşturulur. Windows işlem düğümlerinden oluşan havuzlar oluşturmak istiyorsanız, Cloud Services'ın dağıtım süresi açısından daha iyi bir performans sunduğunu görebilirsiniz.

    * Merhaba *işletim sistemi ailesi* hello işletim sistemi ile hangi .NET sürümlerinin yüklendiğini de belirler.
    * Cloud Services dahilindeki çalışan rollerinde olduğu belirttiğiniz gibi bir *işletim sistemi sürümü* (Merhaba çalışan rolleri hakkında daha fazla bilgi için bkz: [aşamayla ilgili bulut Hizmetleri](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services) hello bölümünde [bulut Hizmetleri Genel Bakış](../cloud-services/cloud-services-choose-me.md)).
    * Çalışan rollerinde olduğu gibi belirttiğiniz olan öneririz gibi `*` hello için *işletim sistemi sürümü* hello düğümler otomatik olarak yükseltilmesi ve yayımlanan toonewly sürümleri gerekli iş toocater yoktur. belirli bir işletim sistemi sürümünün seçildiği birincil kullanım durumu hello güncelleştirilmiş hello sürüm toobe izin vermeden önce test toobe gerçekleştirilen geriye dönük uyumluluk sağlar tooensure uygulama uyumluluğu ' dir. Doğrulama sonrasında hello *işletim sistemi sürümü* hello havuzu güncelleştirilebilir ve hello yeni işletim sistemi görüntüsü yüklenebilir--çalışan tüm görevler kesintiye yeniden kuyruğa ve.

Bir havuz oluşturduğunuzda tooselect hello uygun ihtiyacınız **nodeAgentSkuId**hello işletim sistemi, VHD hello temel görüntünün bağlı olarak. İşletim sistemi görüntüsü başvurular arama hello tarafından kullanılabilir düğüm Aracısı SKU ID tootheir eşlemesi alabilir [liste desteklenen düğüm Aracısı SKU](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus) işlemi.

Merhaba bkz [hesap](#account) bir Batch hesabı oluşturduğunuzda hello havuzu ayırma modunu ayarlama hakkında daha fazla bilgi için bölüm.

#### <a name="custom-images-for-virtual-machine-pools"></a>Sanal Makine havuzları için özel görüntüler

toouse özel görüntü tooprovision sanal makine havuzları, Batch hesabınıza hello kullanıcı abonelik havuzu ayırma moduyla oluşturun. Bu modda, Batch havuzları hello hesabının bulunduğu hello aboneliğinize ayrılır. Merhaba bkz [hesap](#account) bir Batch hesabı oluşturduğunuzda hello havuzu ayırma modunu ayarlama hakkında daha fazla bilgi için bölüm.

özel görüntü toouse, genelleme tarafından tooprepare hello görüntü gerekir. Azure VM'lerin özel Linux görüntüleri hazırlama hakkında daha fazla bilgi için bkz: [Azure Linux VM'de toouse bir şablon olarak yakalama](../virtual-machines/linux/capture-image-nodejs.md). Azure sanal makinelerinden özel Windows görüntüleri hazırlama hakkında daha fazla bilgi için bkz. [Azure PowerShell ile özel VM görüntüleri oluşturma](../virtual-machines/windows/tutorial-custom-images.md). 

> [!IMPORTANT]
> Özel görüntünüzü hazırlanırken hello aşağıdakileri göz önünde bulundurun:
> - Toplu havuzlarınızı mu tooprovision kullandığınız bu hello temel işletim sistemi görüntüsü olun hello özel betik uzantısı gibi Azure uzantıları herhangi bir önceden yüklemediyseniz. Merhaba görüntü önceden yüklenmiş bir uzantısı içeriyorsa, Azure hello VM dağıtma sorunlarla karşılaşabilirsiniz.
> - Merhaba toplu işlem düğüm Aracısı şu anda hello varsayılan geçici sürücü bekliyor olarak kullandığı varsayılan geçici sürücü hello sağlamak, hello temel işletim sistemi görüntü emin olun.
>
>

özel görüntü kullanarak bir sanal makine yapılandırması havuzu toocreate tane gerekecektir veya daha fazla standart Azure depolama özel VHD görüntülerinizi toostore hesapları. Özel görüntüler blob olarak depolanır. özel bir havuz oluşturduğunuzda görüntüleri tooreference belirtin hello hello özel görüntü VHD BLOB hello için URI [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk) hello özelliğinin [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf) özelliği.

Depolama hesaplarınızı ölçütleri aşağıdaki hello karşıladığından emin olun:   

- içeren hello özel görüntü VHD BLOB'ları içinde toobe gereksinim hello depolama hesapları aynı abonelik toplu işlem hesabı (Merhaba kullanıcı abonelik) hello gibi hello.
- Merhaba belirtilen depolama hesapları gereksinim hello toobe hello toplu işlem hesabı ile aynı bölgeye.
- Şu anda yalnızca genel amaçlı standart depolama hesapları desteklenmektedir. Azure Premium depolama hello gelecekte desteklenecektir.
- Birden fazla özel VHD blobuna sahip tek bir depolama hesabı veya her birinde tek blob bulunan birden fazla depolama hesabı belirtebilirsiniz. Toouse öneririz daha iyi bir performans tooget birden çok depolama hesapları.
- Linux VM örnekleri too40 veya 20 Windows VM örnekleri bir benzersiz özel görüntü VHD blob destekler. Merhaba VHD blob toocreate daha fazla sanal makineleri havuzlarıyla toocreate kopyalarını gerekir. Örneğin, 200 Windows VM'ler havuzuyla Merhaba belirtilen 10 benzersiz VHD bloblarının gereken **osDisk** özelliği.

toocreate hello Azure portal kullanarak özel bir görüntü havuzundan:

1. Tooyour Batch hesabında hello Azure portalına gidin.
2. Merhaba üzerinde **ayarları** dikey penceresinde, select hello **havuzları** menü öğesi.
3. Merhaba üzerinde **havuzları** dikey penceresinde, select hello **Ekle** hello; komutu **havuzu ekleme** dikey penceresinde görüntülenir.
4. Seçin **özel görüntü (Linux/Windows)** hello gelen **görüntü türü** açılır. Merhaba portal görüntüler hello **özel görüntü** Seçici. Bir veya daha fazla VHD hello seçin aynı kapsayıcı ve tıklatın hello **seçin** düğmesi. 
    Birden çok VHD farklı depolama hesapları ve farklı kapsayıcılar desteği hello gelecekteki eklenir.
5. Select hello doğru **teklif/yayımcı/Sku** özel Vhd'lerinizi için istenen hello seçin **önbelleğe alma** modu sonra tüm doldurun hello hello havuzu için başka parametre.
6. toocheck özel bir görüntü üzerinde bir havuzu dayanıyorsa hello bkz **işletim sistemi** hello kaynak Özet bölümündeki hello özelliği **havuzu** dikey. Bu özellik başlangıç değeri olmalıdır **özel VM görüntüsü**.
7. Bir havuzuyla ilişkili tüm özel VHD'leri hello havuzunun üzerinde görüntülenen **özellikleri** dikey.

### <a name="compute-node-type-and-target-number-of-nodes"></a>İşlem düğümü türü ve hedef düğüm sayısı

Bir havuz oluşturduğunuzda, istediğiniz ve hedef sayısıyla her biri için hello işlem düğümleri türlerini belirtebilirsiniz. işlem düğümleri Hello iki türleri şunlardır:

- **Adanmış işlem düğümleri.** Adanmış bir işlem düğümleri, iş yükleriniz için ayrılmıştır. Düşük öncelikli düğümlerinden daha daha pahalı, ancak bunlar garanti toonever etkisiz.

- **Düşük öncelikli işlem düğümleri.** Düşük öncelikli düğümleri fazlalık kapasite içinde Azure toorun toplu iş yüklerinizi yararlanın. Düşük öncelikli düğümlerin saatlik maliyeti, adanmış düğümlerden daha düşüktür ve bu düğümler çok fazla işlem gücü gerektiren iş yüklerini etkinleştirir. Daha fazla bilgi için bkz. [Batch ile düşük öncelikli VM’ler kullanma](batch-low-pri-vms.md).

    Azure’daki fazla kapasite yetersiz olduğunda, düşük öncelikli işlem düğümleri etkisiz hale getirilebilir. Bir düğüm görevleri çalıştırılırken geçersiz kılınırsa, başlangıç görevleri yeniden kuyruğa ve işlem düğümü yeniden kullanılabilir hale geldikten sonra yeniden çalıştırın. Düşük öncelikli düğümleri burada hello iş tamamlanma zamanı esnek ve hello iş birçok düğümüne dağıtılmış iş yükleri için iyi bir seçenek olan. Senaryonuz için toouse düşük öncelikli düğümleri karar vermeden önce işlerinizi nedeniyle kesildi emin olun toopreemption minimal ve kolay toorecreate olacaktır.

    Düşük öncelikli işlem düğümleri yalnızca çok hello havuzu ayırma modu ile oluşturulan toplu hesaplar için kullanılabilir**Batch hizmeti**.

Her iki düşük öncelik ve ayrılmış işlem düğümleri hello bulunabilir aynı havuzu. Her düğüm türünü &mdash; düşük öncelik ve ayrılmış &mdash; kendisi için belirtebilirsiniz hello istenen düğüm sayısını kendi hedef ayarı vardır. 
    
Merhaba, işlem düğümleri başvurulan tooas sayısıdır bir *hedef* bazı durumlarda havuzunuz hello istenen düğüm sayısını ulaşmayabileceğinden. Merhaba erişirse, örneğin, bir havuz hello hedef elde edemezsiniz [çekirdek kotası](batch-quota-limit.md) , toplu işlemi için hesap ilk. Ya da hello havuzu değil elde hello hedef bir otomatik ölçeklendirme uyguladıysanız hello en fazla düğüm sayısını sınırlayan formül toohello havuzu.

Hem düşük öncelikli hem de adanmış işlem düğümlerinin fiyatlandırma bilgileri için bkz. [Batch Fiyatlandırması](https://azure.microsoft.com/pricing/details/batch/).

### <a name="size-of-hello-compute-nodes"></a>Merhaba işlem düğümlerinin boyutu

**Cloud Services Yapılandırması** işlem düğümü boyutları [Cloud Services Boyutları](../cloud-services/cloud-services-sizes-specs.md) içinde listelenmiştir. Batch hizmeti `ExtraSmall`, `STANDARD_A1_V2` ve `STANDARD_A2_V2` dışında tüm Cloud Services boyutlarını destekler.

**Sanal Makine Yapılandırması** işlem düğümü boyutları [Azure’da sanal makine boyutları](../virtual-machines/linux/sizes.md) (Linux) ve [Azure’da sanal makine boyutları](../virtual-machines/windows/sizes.md) (Windows) içinde listelenmiştir. Batch `STANDARD_A0` ve premium depolama alanına sahip olanlar (`STANDARD_GS`, `STANDARD_DS` ve `STANDARD_DSV2` serisi) dışında tüm Azure sanal makinelerini destekler.

Bir işlem düğüm boyutu seçerken, hello özellikleri ve hello düğümlerinde çalıştıracaksınız hello uygulamaların gereksinimlerini göz önünde bulundurun. Yönlerini hello uygulama birden çok iş parçacıklı olup olmadığı ve içereceği tükettiği ne kadar bellek yardımcı olabilecek gibi hello en uygun ve ekonomik düğüm boyutunu belirler. Bir görev varsayarak düğüm boyutu bir düğümde aynı anda çalışacak tipik tooselect olur. Ancak, olası toohave olan birden çok görev (ve dolayısıyla Uygulama örneğinin) [paralel olarak çalışan](batch-parallel-node-tasks.md) iş yürütme sırasında işlem düğümleri üzerinde. Bu durumda, ortak toochoose büyük düğüm boyutu tooaccommodate artan hello isteğe bağlı paralel görev yürütme olur. Daha fazla bilgi için bkz. [Görev zamanlama ilkesi](#task-scheduling-policy).

Bir havuzdaki hello düğümleri aynı hello tümü boyutu. Farklı sistem gereksinimleri toorun uygulamalarla düşündüğünüz ve/veya yük düzeylerine, ayrı havuzlar kullanmanızı öneririz.

### <a name="scaling-policy"></a>Ölçeklendirme ilkesi

Dinamik iş yükleri için yazma ve uygulayabileceğiniz bir [otomatik ölçeklendirme formülü](#scaling-compute-resources) tooa havuzu. Merhaba Batch hizmeti düzenli aralıklarla değerlendirir ve hello çeşitli havuz, iş ve belirtebileceğiniz görev parametreleri göre hello havuz içindeki düğüm sayısını ayarlar.

### <a name="task-scheduling-policy"></a>Görev zamanlama ilkesi

Merhaba [düğüm başına maksimum görev](batch-parallel-node-tasks.md) yapılandırma seçeneği hello havuzundaki her işlem düğümü üzerinde paralel olarak çalışan görevler hello sayısını belirler.

Merhaba varsayılan yapılandırma bir düğümde bir seferde bir görev çalışır, ancak bir düğümde aynı anda yürütülen iki veya daha fazla görev yararlı toohave olduğu senaryolar vardır belirtir. Merhaba bkz [Örnek senaryo](batch-parallel-node-tasks.md#example-scenario) hello içinde [eşzamanlı düğüm görevleri](batch-parallel-node-tasks.md) nasıl, avantajını düğümü başına birden fazla görevden makale toosee.

Ayrıca belirtebilirsiniz bir *Dolgu türü* toplu hello görevleri bir havuzdaki tüm düğümlere eşit olarak yayılır veya görevler tooanother düğümünü atamadan önce her düğüm hello en fazla sayıda görev ile paketleri olup olmadığını belirler.

### <a name="communication-status-for-compute-nodes"></a>İşlem düğümlerinin iletişim durumu

Çoğu senaryoda görevler bağımsız olarak çalışır ve birbiriyle toocommunicate gerekmez. Ancak, [MPI senaryolarında](batch-mpi.md) olduğu gibi içinde görevlerin iletişim kurması gereken bazı uygulamalar olabilir.

Bir havuz tooallow yapılandırabilirsiniz **düğümler arası iletişim**, böylece havuzdaki düğümlerin çalışma zamanında iletişim kurabilir. Düğümler arası iletişim etkinleştirildiğinde, Cloud Services havuzlarındaki düğümler 1100'den büyük bağlantı noktaları üzerinde birbiriyle iletişim kurabilir ve Sanal Makine Yapılandırması havuzları hiçbir bağlantı noktası üzerinde trafiği kısıtlamaz.

Düğümler arası iletişimin etkinleştirilmesi de hello hello kümelerdeki düğümlerin yerleşimini etkiler ve dağıtım kısıtlamaları nedeniyle hello en fazla bir havuzdaki düğüm sayısını sınırlayabilir unutmayın. Uygulamanız düğümler arasında iletişim gerektirmiyorsa, veri merkezleri tooenable artan paralel işleme gücünü ve hello Batch hizmeti potansiyel olarak çok sayıda düğümü birçok kümeden toohello havuza ayırabilir.

### <a name="start-tasks-for-compute-nodes"></a>İşlem düğümleri için başlangıç görevleri

İsteğe bağlı Hello *başlangıç görevi* bu düğüme hello havuzuna katılır ve her zaman bir düğümün yeniden başlatıldığı ya da her bir düğümde yürütür. Hello başlangıç görevi özellikle hello görevlerinizi hello işlem düğümlerinde çalışan hello uygulamaları yükleme gibi görevlerini yürütülmesi için işlem düğümlerinin hazırlanmasında yararlıdır.

### <a name="application-packages"></a>Uygulama paketleri

Belirleyebileceğiniz [uygulama paketleri](#application-packages) toodeploy toohello havuzunda işlem düğümlerini hello. Uygulama paketleri, Basitleştirilmiş Dağıtım ve sürüm oluşturma, görevleri çalıştırmak hello uygulamaların sağlar. Havuz için belirttiğiniz uygulama paketleri, bir düğüm her yeniden başlatıldığında veya görüntüsü yeniden oluşturduğunda o havuza katılan her düğüme yüklenir.

> [!NOTE]
> Uygulama paketleri 5 Temmuz 2017’den sonra oluşturulmuş tüm Batch havuzlarında desteklenir. Bunlar yalnızca hello havuzu, bir bulut Hizmeti Yapılandırması kullanılarak oluşturulduysa 10 Mart 2016 ve 5 Temmuz 2017 arasında oluşturulan Batch havuzu üzerinde desteklenir. Önceki too10 Mart 2016 oluşturulan batch havuzları, uygulama paketleri desteklemez. Uygulama hakkında daha fazla bilgi toodeploy uygulamaları tooyour toplu düğümleriniz paketleri için bkz: [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md).
>
>

### <a name="network-configuration"></a>Ağ yapılandırması

Bir Azure hello alt ağ belirtebilir [sanal ağ (VNet)](../virtual-network/virtual-networks-overview.md) hangi hello havuzun işlem düğümleri oluşturulmalıdır. Merhaba bkz [havuzu Ağ Yapılandırması](#pool-network-configuration) daha fazla bilgi için bölüm.


## <a name="job"></a>İş
İş bir görev koleksiyonudur. Bu, bir havuzdaki hello işlem düğümleri üzerindeki görevleri tarafından hesaplamanın nasıl gerçekleştirildiğini yönetir.

* Merhaba işini belirtir hello **havuzu** hangi hello çalıştırmak toobe iştir. Her iş için yeni havuz oluşturabilir veya çok sayıda iş için bir havuz kullanabilirsiniz. Bir iş zamanlaması ile ilişkili her iş için veya bir iş zamanlaması ile ilişkili tüm işler için havuz oluşturabilirsiniz.
* İsteğe bağlı bir **iş önceliği** belirtebilirsiniz. Bir işi devam eden işler daha yüksek önceliğe sahip gönderildiğinde hello yüksek öncelikli işin hello görevlerde hello düşük öncelikli işler için görevler önünde hello kuyruğa eklenir. Çalışmakta olan düşük öncelikli işlerdeki görevler engellenmez.
* İş kullanabilirsiniz **kısıtlamaları** toospecify işleriniz için belirli sınırları:

    Ayarlayabileceğiniz bir **maksimum duvar saati**, böylece bir iş belirtilen hello maksimum duvar saati süresinden daha uzun süre çalışırsa, hello iş ve tüm görevleri sonlandırılır.

    Batch başarısız olan görevleri algılayabilir ve sonra yeniden deneyebilir. Merhaba belirtebilirsiniz **görev yeniden deneme sayısı** bir görevin kısıtlama olarak *her zaman* veya *hiçbir zaman* denenecek. Bir görevin yeniden denenmesi yeniden kuyruğa toobe yeniden çalıştırmak bu hello görev olduğu anlamına gelir.
* İstemci uygulamanızı görevleri tooa iş ekleyebilir veya belirleyebileceğiniz bir [iş yöneticisi görevi](#job-manager-task). İşlem düğümleri hello havuzunda hello iş yöneticisi görevi hello birinde çalıştırılan görevle birlikte, bir iş yöneticisi görevi bir iş için gerekli toocreate hello gerekli görevleri hello bilgilerini içerir. Merhaba iş yöneticisi görevi işlenir hello iş oluşturulur ve başarısız olursa yeniden hemen özellikle Batch tarafından kuyruğa alınır. Bir iş yöneticisi görevi, *gerekli* tarafından oluşturulan işleri için bir [iş zamanlaması](#scheduled-jobs) hello iş örneği oluşturulmadan hello tek yolu toodefine hello görevleri olduğundan.
* Merhaba işindeki tüm görevler tamamlandığında varsayılan olarak, işleri hello etkin durumda kalır. Böylece hello işteki tüm görevler tamamlandığında hello iş otomatik olarak sonlandırılmadan bu davranışı değiştirebilirsiniz. Set hello işin **onAllTasksComplete** özelliği ([OnAllTasksComplete] [ net_onalltaskscomplete] Batch .NET içindeki) çok*terminatejob* tooautomatically tüm görevleri tamamlandı hello durumda olduğunda hello işi sonlandırır.

    Merhaba Batch hizmeti bir işlemle dikkate Not *hiçbir* görevleri toohave tüm görevleri tamamlandı. Bu nedenle, bu seçenek genellikle [iş yöneticisi görevi](#job-manager-task) ile kullanılır. Bir iş yöneticisi olmadan toouse otomatik işini sonlandırma istiyorsanız, yeni bir işin başlangıçta ayarlamalısınız **onAllTasksComplete** özelliği çok*noaction*, çok ayarlamak*terminatejob* yalnızca görevleri toohello iş eklemeyi tamamladıktan sonra.

### <a name="job-priority"></a>İş önceliği
Batch'de oluşturduğunuz bir öncelik toojobs atayabilirsiniz. Merhaba Batch hizmeti bir hesaptaki iş zamanlama hello iş toodetermine hello siparişi hello öncelik değerini kullanır (Bu toobe ile kafası değil bir [zamanlanmış işi](#scheduled-jobs)). Merhaba öncelik değerleri -1000 too1000 aralığı, -1000 ile olmasına hello en düşük öncelik ve 1000 olan en yüksek hello. bir işin çağrısı hello tooupdate hello öncelik [güncelleştirme işi hello özelliklerine] [ rest_update_job] işlemini (Batch REST) veya hello değiştirmek [CloudJob.Priority] [ net_cloudjob_priority] özelliğini (Batch .NET).

Merhaba içinde aynı, daha yüksek öncelikli hesabı işlerin sahip öncelik düşük öncelikli işlere göre zamanlama üstünlüğü. Bir hesaptaki yüksek öncelik değerine sahip iş farklı bir hesaptaki düşük öncelik değerine sahip başka bir işe karşı zamanlama üstünlüğüne sahip değildir.

Havuzlardaki iş zamanlaması bağımsızdır. Farklı havuzlar arasında, ilişkili havuzunda boşta düğüm eksikliği olması durumunda yüksek öncelikli işin önce zamanlanacağı kesin değildir. Hello aynı havuz, işler hello ile aynı öncelik düzeyine sahip zamanlanma şansı eşittir.

### <a name="scheduled-jobs"></a>Zamanlanan işler
[İş zamanlamaları] [ rest_job_schedules] hello Batch hizmetinde yinelenen işler toocreate etkinleştirin. Bir iş zamanlaması zaman toorun işler ve Çalıştır hello işleri toobe hello özelliklerini içerir belirtir. Hello zamanlama--hello süresini ne kadar süreyle belirtebilirsiniz ve ne zaman hello zamanlaması etkin değildir ve dönem zamanlanan işleri sırasında hello ne sıklıkta oluşturulur.

## <a name="task"></a>Görev
Görev bir işle ilişkili hesaplama birimidir. Bir düğüm üzerinde çalışır. Görevler tooa düğümü yürütme için atanan veya bir düğüm serbest kalana kadar kuyruğa alınır. Basitçe, bir görev bir veya daha fazla program ya da komut dosyaları bitti gereksinim duyduğunuz bir işlem düğümü tooperform hello iş üzerinde çalışır.

Bir görev oluşturduğunuzda aşağıdakileri belirtebilirsiniz:

* Merhaba **komut satırı** hello görev için. Uygulama veya betik hello işlem düğümü üzerinde çalıştıran hello komut satırı budur.

    Komut satırı hello toonote gerçekte bir kabuk altında çalışmaz önemlidir. Bu nedenle, onu yerel olarak gibi Kabuk özelliklerinden alamıyor [ortam değişkeni](#environment-settings-for-tasks) genişletme (Bu hello içerir `PATH`). tootake avantajı gibi özelliklerini, hello Kabuk hello komut satırında--Örneğin, başlatarak çağırmanız gerekir `cmd.exe` Windows düğümlerinde veya `/bin/sh` Linux üzerinde:

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    Görevlerinizi toorun gerekiyorsa bir uygulama veya kullanımda olmayan betik hello düğümün `PATH` veya başvuru ortamı değişkenlerinde, açıkça hello görev komut satırı kabuğu hello çağırma.
* **Kaynak dosyaları** işlenen hello veri toobe içerir. Merhaba görevin komut satırı yürütülmeden önce bu otomatik olarak kopyalanan toohello düğümü genel amaçlı bir Azure depolama hesabındaki Blob depolamadan dosyalarıdır. Daha fazla bilgi için hello bölümlere bakın [başlangıç görevi](#start-task) ve [dosyaları ve dizinleri](#files-and-directories).
* Merhaba **ortam değişkenleri** , uygulamanız tarafından gereklidir. Daha fazla bilgi için bkz: Merhaba [görevler için ortam ayarları](#environment-settings-for-tasks) bölümü.
* Merhaba **kısıtlamaları** altında hangi hello görev yürütülecek. Örneğin, hello en uzun süre kısıtlamalarını içermek hello görev toorun, hello en fazla kaç kez başarısız görevi yeniden, izin verilen ve hello maksimum saat hello görevin çalışma dizinindeki dosyaları korunur.
* **Uygulama paketleri** toodeploy toohello işlem düğümü üzerinde hangi hello görevdir zamanlanmış toorun. [Uygulama paketleri](#application-packages) Basitleştirilmiş Dağıtım ve sürüm oluşturma, görevleri çalıştırmak hello uygulamaların sağlar. Görev düzeyi uygulama paketleri Burada farklı işleri bir havuzu üzerinde çalışır ve bir iş tamamlandığında hello havuzu silinmez paylaşılan havuzu ortamlarda kullanışlıdır. İşinizi hello havuzunda düğümleri'den daha az görev varsa, görev uygulama paketleri bir uygulamanız görevleri çalıştırmak dağıtılan yalnızca toohello düğümleri olduğundan veri aktarımını en aza indirebilirsiniz.

Ayrıca bir düğümde tooperform hesaplama tanımladığınız tootasks hello aşağıdaki özel görevler de hello Batch hizmeti tarafından sağlanır:

* [Başlangıç görevi](#start-task)
* [İş yöneticisi görevi](#job-manager-task)
* [İş hazırlama ve bırakma görevleri](#job-preparation-and-release-tasks)
* [Çok örnekli görevler (MPI)](#multi-instance-tasks)
* [Görev bağımlılıkları](#task-dependencies)

### <a name="start-task"></a>Başlangıç görevi
İlişkilendirerek bir **başlangıç görevi** bir havuz ile işletim ortamı düğümlerinin hello hazırlayabilirsiniz. Örneğin, görevlerinizin çalıştığı hello uygulamaları yüklemeye veya arka plan işlemlerini başlatma gibi eylemleri gerçekleştirebilirsiniz. bir düğüm her başlatıldığında hello havuzda kaldığı sürece hello düğümü zaman dahil olmak üzere ilk toohello havuzu ve ne zaman onu yeniden başlatıldığı ya da eklenen için hello başlangıç görevi çalıştırır.

Merhaba başlangıç görevinin birincil avantajı, bir işlem düğümünde gerekli tooconfigure hello bilgilerini içeren ve böylelikle görev yürütmede gereken hello uygulamaları yüklemek ' dir. Bu nedenle, bir havuzdaki düğümlerin hello sayısını artırmayı hello yeni hedef düğüm sayısını belirtmek kadar kolaydır. Hello başlangıç görevi gerekli tooconfigure hello yeni düğümler ve görevleri kabul etmek için hazırlanın hello Batch hizmeti hello bilgiler sağlar.

Herhangi bir Azure Batch görev ile bir listesini belirtebilirsiniz gibi **kaynak dosyaları** içinde [Azure Storage][azure_storage], ayrıca tooa **komut satırı** toobe yürütülebilir. Merhaba Batch hizmeti, ilk hello kaynak dosyaları toohello düğüm Azure Depolama'ya kopyalar ve hello komut satırını çalıştırır. Bir havuz başlangıç görevinde hello dosya listesi genellikle hello görev uygulamasını ve onun bağımlılıklarını içerir.

Ancak, hello başlangıç görevi hello işlem düğümü üzerinde çalışan tüm görevler tarafından kullanılan başvuru veri toobe de içerebilir. Örneğin, bir başlangıç görevinin komut satırı gerçekleştirebilir bir `robocopy` (hangi kaynak dosya olarak belirtildi ve toohello düğüme indirilir) işlemi toocopy uygulama dosyalarından hello Başlat görevin [çalışma dizini](#files-and-directories) toohello [paylaşılan klasör](#files-and-directories), ve ardından bir MSI çalıştırın veya `setup.exe`.

Merhaba Batch hizmeti toowait hello başlangıç görevi toocomplete için için genelde istenen düğüm atanan hazır toobe görevleri hello belirlemeden önce ancak bunu yapılandırabilirsiniz.

Bir işlem düğümünde başlangıç görevi başarısız olursa, ardından hello hello düğümü güncelleştirilmiş tooreflect hello hata durumudur ve hello düğüm herhangi bir görevi atanmadı. Bir başlangıç görevi, depolamadan kaynak dosya kopyalamada bir sorun olduğunda ya da komut satırı tarafından yürütülen hello işlemin sıfır olmayan çıkış kodu döndürmesi durumunda başarısız olabilir.

Eklemek veya var olan bir havuzu hello başlangıç görevi güncelleştirmek, işlem düğümlerini hello başlangıç görevi uygulanan toobe toohello düğümlerin yeniden başlatılması gerekir.

>[!NOTE]
> Merhaba toplam boyutu bir başlangıç görevi küçük veya buna eşit olmalıdır kaynak dosyaları ve ortam değişkenleri dahil, too32768 karakteri. Başlangıç görevi bu gereksinimleri karşıladığından emin tooensure iki yaklaşımdan birini kullanabilirsiniz:
>
> 1. Batch havuzundaki her düğüm genelinde uygulama paketleri toodistribute uygulamalar veya veri kullanabilirsiniz. Uygulama paketleri hakkında daha fazla bilgi için bkz: [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md).
> 2. El ile uygulama dosyalarınızı içeren bir sıkıştırılmış arşiv oluşturabilirsiniz. Sıkıştırılmış arşivi tooAzure depolama blob olarak yükleyin. Daraltılmış hello arşiv başlangıç göreviniz için bir kaynak dosya olarak belirtin. Başlangıç göreviniz hello komut satırını çalıştırmadan önce hello arşiv hello komut satırından sıkıştırmasını açın. 
>
>    toounzip hello Arşiv, tercih ettiğiniz aracı arşivleme hello kullanabilirsiniz. Merhaba başlangıç görevi için kaynak dosyası olarak toounzip hello arşivi kullanmak tooinclude hello Aracı gerekir.
>
>

### <a name="job-manager-task"></a>İş yöneticisi görevi
Tipik olarak kullandığınız bir **iş yöneticisi görevi** toocontrol ve/veya İzleyici işi yürütme--Örneğin, toocreate bir iş için hello görevler gönderebilir, ek görevleri toorun belirlemek ve çalışmanın ne zaman tamamlandığını belirlemek. Ancak, bir iş yöneticisi görevi, şu kısıtlı toothese etkinlikleri değil. Merhaba iş için gereken tüm eylemleri gerçekleştirebilen tam kapsamlı bir görevdir. Örneğin, bir iş yöneticisi görevi parametre olarak belirtilen bir dosyayı indirebilir, dosyanın içeriğini hello çözümlemek ve bu içeriğe göre ek görevler gönderebilir.

Bir iş yöneticisi görevi diğer tüm görevlerden önce başlatılır. Hello aşağıdaki özellikleri sağlar:

* Merhaba iş oluşturulduğunda hello Batch hizmeti tarafından bir görev olarak otomatik olarak gönderilir.
* Bunu işteki diğer görevler hello önce zamanlanmış tooexecute değil.
* Merhaba son toobe hello havuzu küçültülürken havuzundan kaldırıldı, ilişkili düğümdür.
* Görevin sonlandırılması bağlı toohello sonlandırma hello işteki tüm görevlerin olabilir.
* Yeniden toobe gerektiğinde iş yöneticisi görevi hello en yüksek öncelik verilir. Boş bir düğüm kullanılabilir durumda değilse, hello Batch hizmeti odada hello havuzu toomake hello iş yöneticisi görevi toorun için çalışan diğer görevlerden hello birini sonlandırabilir.
* Bir işteki iş yöneticisi görevi hello ', diğer işlerin görevleri üzerinde önceliği yoktur. İşlerde, yalnızca iş düzeyinde öncelikler gözetilir.

### <a name="job-preparation-and-release-tasks"></a>İş hazırlama ve bırakma görevleri
Batch, iş öncesi yürütme kurulumu için iş hazırlama görevleri sağlar. İş bırakma görevleri iş sonrası bakım ve temizlemeye yöneliktir.

* **İş hazırlama görevi**: Zamanlanmış toorun görevlerdir tüm işlem düğümlerinde iş hazırlama görevi çalıştırır, diğer iş görevlerinden herhangi bir hello önce yürütülür. Tüm görevler tarafından paylaşılan ancak benzersiz toohello örneğin iş bir iş hazırlama görevi toocopy verileri kullanabilirsiniz.
* **İş bırakma görevi**: bir iş tamamlandığında, bir iş bırakma görevi hello havuzun en az bir görev yürütmüş her düğümünde çalıştırılır. Örneğin bir hello iş hazırlama görevi tarafından kopyalanan iş yayın görev toodelete veri ya da tanılama günlük verilerini toocompress ve karşıya yükleme kullanabilirsiniz.

Hem iş hazırlama ve bırakma görevleri hello görev çağrıldığında toospecify komut satırı toorun sağlar. Bunlar dosya indirme, yükseltilmiş yürütme, özel ortam değişkenleri, en uzun yürütme süresi, yeniden deneme sayısı ve dosyayı elde tutma süresi gibi özellikler sağlar.

İş hazırlama ve bırakma görevleri hakkında daha fazla bilgi için bkz. [Azure Batch işlem düğümlerinde iş hazırlama ve tamamlama görevlerini çalıştırma](batch-job-prep-release.md).

### <a name="multi-instance-task"></a>Çok örnekli görev
A [çok örnekli görev](batch-mpi.md) aynı anda birden fazla işlem düğümü üzerinde yapılandırılmış toorun olan bir görevdir. Çok örnekli görevlerle, yüksek performanslı etkinleştirebilirsiniz bir grup işlem düğümünün olan gerektiren bilgi işlem senaryolarına ayrılan birlikte tek bir iş yükünü (gibi ileti geçirme arabirimi (MPI)) tooprocess.

Merhaba Batch .NET kitaplığını kullanarak MPI işlerini Batch'de çalıştırma hakkında ayrıntılı bilgi için kullanıma [kullanımı çok örnekli görevler toorun ileti geçirme arabirimi (MPI) Azure Batch uygulamalarda](batch-mpi.md).

### <a name="task-dependencies"></a>Görev bağımlılıkları
[Görev bağımlılıkları](batch-task-dependencies.md)hello adından da anlaşılacağı, bir görevin yürütülmesinin önce diğer görevlerin hello tamamlama bağlı toospecify izin verin. Bu özellik, bir "aşağı akış" görevi hello çıktı "Yukarı Akış" görevinin--veya bir Yukarı Akış görevi, aşağı akış görevi tarafından istenen bazı başlatma işlemlerini gerçekleştirdiğinde tüketir durumlar için destek sağlar. toouse bu özellik, Batch işinizde ilk etkinleştir görev bağımlılıkları gerekir. Ardından, başka bir bağlı her görev için (veya diğer birçok), görevin bağımlı hello görevlerini belirtin.

Görev bağımlılıkları ile Merhaba aşağıdaki gibi senaryoları yapılandırabilirsiniz:

* *görevB* *görevA* ’ya bağlıdır (*görevB*, *görevA* tamamlanana kadar yürütülmeye başlamaz).
* *görevC* hem *görevA* hem de *görevB* ’ye bağlıdır.
* *görevD* yürütülmeden önce bir dizi göreve (örneğin görev *1* ile *10* arası) bağlıdır.

Kullanıma [görev bağımlılıkları Azure Batch](batch-task-dependencies.md) ve hello [Github_samples] [ github_sample_taskdeps] hello kod örneğinde [azure-batch-samples] [ github_samples] Bu özellik hakkında daha kapsamlı bilgi için GitHub depo.

## <a name="environment-settings-for-tasks"></a>Görevler için ortam ayarları
Merhaba Batch hizmeti tarafından yürütülen her görev, işlem düğümlerinde ayarlar erişim tooenvironment değişkeni yok. Bu ortam değişkenleri Batch hizmeti hello tarafından tanımlanan içerir ([hizmet tanımlı][msdn_env_vars]) ve görevleriniz için tanımladığınız özel ortam değişkenleri. Merhaba uygulamalar ve görevlerinizi yürütme komut dosyaları yürütme sırasında erişim toothese ortam değişkenleri vardır.

Merhaba doldurarak hello görev ya da iş düzeyinde özel ortam değişkenleri ayarlayabilirsiniz *ortam ayarlarını* bu varlıkların özelliği. Örneğin, hello bkz [görev tooa işi eklemek] [ rest_add_task] işlemini (Batch REST API'si) ya da hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] ve [ CloudJob.CommonEnvironmentSettings] [ net_job_env] Batch .NET özellikleri.

İstemci uygulamanız veya hizmetiniz bir görevin ortam değişkenleri, hem hizmet tanımlı hem de özel hello kullanarak elde edebilirsiniz [bir görev hakkında bilgi alma] [ rest_get_task_info] işlemini (Batch REST) ya da erişme Merhaba [CloudTask.EnvironmentSettings] [ net_cloudtask_env] özelliğini (Batch .NET). Bir işlem düğümünde yürütülen işlemler bu erişebilir ve diğer ortam değişkenleri hello düğümünde kullanarak tanıdık hello `%VARIABLE_NAME%` (Windows) veya `$VARIABLE_NAME` (Linux) söz dizimi.

[İşlem düğümü ortam değişkenleri][msdn_env_vars] içinde hizmet tarafından tanımlanan tüm ortam değişkenlerinin tam listesini bulabilirsiniz.

## <a name="files-and-directories"></a>Dosyalar ve dizinler
Her görev, altında sıfır veya daha fazla dosya ve dizin oluşturduğu bir *çalışma dizinine* sahiptir. Bu çalışma dizini, işler, hello veri hello görev tarafından çalıştırılan hello program depolamak için kullanılabilir ve gerçekleştirdiği hello işlenmesini hello çıktı. Tüm dosya ve dizinlerin bir görevin hello görev kullanıcısına aittir.

Merhaba Batch hizmeti sunan hello hello olarak bir düğümdeki dosya sisteminin bir bölümünü *kök dizini*. Görevler, hello başvurarak hello kök dizine erişebilir `AZ_BATCH_NODE_ROOT_DIR` ortam değişkeni. Ortam değişkenlerini kullanma hakkında daha fazla bilgi için bkz. [Görevler için ortam ayarları](#environment-settings-for-tasks).

Merhaba kök dizin aşağıdaki dizin yapısını hello içerir:

![İşlem düğümü dizin yapısı][1]

* **Paylaşılan**: Bu dizin çok okuma/yazma erişimi sağlar*tüm* bir düğümde çalışan görevler. Hello düğümü üzerinde çalışan herhangi bir görev oluşturma, okuma, güncelleştirme ve bu dizindeki dosyaları silin. Görevler, hello başvurarak bu dizine erişebilir `AZ_BATCH_NODE_SHARED_DIR` ortam değişkeni.
* **başlangıç**: Bu dizin, bir başlangıç görevi tarafından çalışma dizini olarak kullanılır. Tüm hello başlangıç görevi tarafından indirilen toohello düğümü hello dosyalar buraya depolanır. Hello başlangıç görevi oluşturma, okuma, güncelleştirme ve bu dizin altında dosya silin. Görevler, hello başvurarak bu dizine erişebilir `AZ_BATCH_NODE_STARTUP_DIR` ortam değişkeni.
* **Görevleri**: hello düğümde çalışan her görev için bir dizin oluşturulur. Merhaba başvurarak erişilen `AZ_BATCH_TASK_DIR` ortam değişkeni.

    Her bir görev dizininde Batch hizmeti hello bir çalışma dizini oluşturur (`wd`) dizinin benzersiz yolu hello tarafından belirtilen `AZ_BATCH_TASK_WORKING_DIR` ortam değişkeni. Bu dizine okuma/yazma erişimi toohello görevi sağlar. Hello görev oluşturma, okuma, güncelleştirme ve bu dizin altında dosya silin. Bu dizin üzerinde hello göre tutulur *RetentionTime* hello görev için belirtilmiş kısıtlaması.

    `stdout.txt`ve `stderr.txt`: Bu dosyalar hello görev hello yürütülmesi sırasında toohello görev klasörüne yazılır.

> [!IMPORTANT]
> Bir düğüm hello havuzdan kaldırıldığında *tüm* hello hello düğümde depolanan dosyalar silinir.
>
>

## <a name="application-packages"></a>Uygulama paketleri
Merhaba [uygulama paketleri](batch-application-packages.md) özelliği, toohello havuzlarınızdaki işlem düğümlerine kolay yönetim ve uygulamalarının dağıtımını sağlar. Karşıya yükleme ve bunların ikili dosyaları gibi görevleriniz tarafından uygulamaları çalıştırmak hello birden fazla sürümünü yönetmek ve dosyaları destekler. Ardından bir otomatik olarak dağıtabilir veya daha fazla bu uygulamaları toohello havuzunuzdaki düğümlerden işlem.

Uygulama paketleri hello havuzu ve görev düzeyinde belirtebilirsiniz. Havuz uygulama paketleri belirttiğinizde, hello hello havuzun dağıtılan tooevery düğümünde uygulamasıdır. Görev uygulama paketleri belirttiğinizde, zamanlanmış toorun en az bir hello işin görevlerinin olan dağıtılan yalnızca toonodes hello uygulama, yalnızca hello önce görevin komut satırı çalıştırılır.

Toplu işler, uygulama paketlerinizi Azure Storage toostore ile çalışma ayrıntılarını hello ve böylece hem kod hem de yönetim yükünü basit bunları toocompute düğümleri dağıtabilirsiniz.

toofind hello uygulama paketi özelliği hakkında daha fazla bilgi, kullanıma [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md).

> [!NOTE]
> Havuz uygulama paketleri tooan eklerseniz *varolan* havuzu, dağıtılan toobe toohello düğümleri hello uygulama paketleri için işlem düğümleri yeniden başlatılması gerekir.
>
>

## <a name="pool-and-compute-node-lifetime"></a>Havuz ve işlem düğümü ömrü
Azure Batch çözümünüzü tasarlarken, havuzları oluşturulur ve bu havuzlardaki düğümleri tutulacağına ne kadar süre işlem toomake ve hakkında bir tasarım kararı vardır.

Merhaba spektrumun bir ucunda gönderdiğiniz her iş için bir havuz oluşturabilir ve görevleri yürütülmesi biter bitmez hello havuzunu silin. Merhaba düğümleri yalnızca gerekli ve boşta hemen kapandığında ayrıldığından bu kullanımını en üst düzeye çıkarır. Bu anlamına gelmekle birlikte hello iş ayrılan hello düğümleri toobe için beklemesi gereken, görevler düğümleri ayrılmış, tek tek kullanılabilir, hemen çalıştırılmak üzere zamanlandığını ve hello önemli toonote olduğu başlangıç görevi tamamlandı. Toplu mu *değil* görevleri toohello düğümleri atamadan önce havuzdaki tüm düğümlerin kullanılabilir olmasını bekleyin. Böylece kullanılabilir tüm düğümlerden en iyi şekilde faydalanılmasını sağlar.

Merhaba hello spektrumun diğer ucundaki işlerin hemen başlatılması hello en yüksek önceliğe sahipse, bir havuz oluşturabilir ve işler gönderilmeden önce düğümlerinden kullanılabilir hale getirebilirsiniz. Bu senaryoda, görevleri hemen başlayabilir ancak düğümleri kalmaya devam boşta kendileri için beklenirken toobe atanmış.

Değişken ancak devam eden bir yükü işlemek için genellikle birleştirilmiş bir yaklaşım kullanılır. Birden çok iş gönderilir ancak düğüm sayısını hello yukarı veya aşağı toohello iş yüküne according ölçeklendirebilirsiniz bir havuza sahip olabilir (bakın [işlem kaynaklarını ölçeklendirme](#scaling-compute-resources) bölümden hello içinde). Mevcut yüke bağlı olarak reaktif bir şekilde ya da yük öngörülebiliyorsa proaktif olarak bu işlemi yapabilirsiniz.

## <a name="virtual-network-vnet-and-firewall-configuration"></a>Sanal ağ ve güvenlik duvarı yapılandırması 

Azure toplu işlem düğümleri havuzu sağladığınızda hello havuzu Azure alt ağ ile ilişkilendirebilirsiniz [sanal ağ (VNet)](../virtual-network/virtual-networks-overview.md). alt ağ ile bir VNet oluşturma hakkında daha fazla toolearn bkz [alt ağ ile bir Azure sanal ağı oluşturmak](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). 

 * Merhaba bir havuzuyla ilişkili VNet olması gerekir:

   * İçinde aynı Azure hello **bölge** hello Azure Batch hesabı olarak.
   * İçinde aynı hello **abonelik** hello Azure Batch hesabı olarak.

* nasıl havuzları hello toplu işlem hesabı için ayrılan üzerinde desteklenen VNet Hello türüne bağlıdır:

    - Merhaba havuzu ayırma modu Batch hesabınıza tooBatch hizmet ayarlanmış sonra hello ile oluşturulan bir VNet yalnızca toopools atayabilirsiniz **Cloud Services Yapılandırması**. Ayrıca, VNet hello Klasik dağıtım modeli kullanılarak oluşturulmuş gerekir hello belirtilmiş. Hello Azure Resource Manager dağıtım modeli kullanılarak oluşturulmuş sanal ağlar desteklenmez.
 
    - Merhaba havuzu ayırma modu, toplu işlem hesabı için abonelik tooUser ayarlanmış sonra hello ile oluşturulan bir VNet yalnızca toopools atayabilirsiniz **sanal makine yapılandırması**. Merhaba ile oluşturulan havuzu **bulut Hizmeti Yapılandırması** desteklenmez. Merhaba hello Azure Resource Manager dağıtım modeli veya hello Klasik dağıtım modeli ile ilişkili sanal ağ oluşturulabilir.

    VNet destek özetlemeye bir tablo için hello bkz toopool ayırma modu according [havuzu ayırma modu](#pool-allocation-mode) bölümü.

* Merhaba havuzu ayırma modu Batch hesabınıza tooBatch hizmet ayarlanırsa hello toplu hizmet asıl tooaccess izinlerini VNet hello sağlamanız gerekir. Merhaba VNet hello atamanız gerekir [Classic Virtual Machine Contributor Role-Based erişim denetimi (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor) rol toohello toplu hizmet sorumlusu. Merhaba RBAC rolü sağlanmamış belirtilmişse, hello Batch hizmeti 400 (Hatalı istek) döndürür. Merhaba rolünde hello Azure portal tooadd:

    1. Select hello **VNet**, ardından **erişim denetimi (IAM)** > **rolleri** > **sanal makine Katılımcısı**  >  **Eklemek**.
    2. Merhaba üzerinde **izinleri eklemek** dikey penceresinde, select hello **sanal makine Katılımcısı** rol.
    3. Merhaba üzerinde **izinleri eklemek** dikey penceresinde, Batch API'sini hello arayın. Merhaba API bulana kadar bu dizelerin her biri için sırayla arayın:
        1. **MicrosoftAzureBatch**.
        2. **Microsoft Azure Batch**. Daha yeni Azure AD kiracıları bu adı kullanıyor olabilir.
        3. **ddbf3205-c6bd-46ae-8127-60eb93363864** hello toplu API hello kimliğidir. 
    3. Merhaba toplu API hizmet sorumlusu seçin. 
    4. **Kaydet** düğmesine tıklayın.

        ![VM katkıda bulunan rolü tooBatch hizmet sorumlusu atayın](./media/batch-api-basics/iam-add-role.png)


* Merhaba belirtilen alt ağ yeterli olması gerektiğini ücretsiz **IP adreslerini** tooaccommodate hello hedef düğümleri toplam sayısı; diğer bir deyişle, hello toplamını hello `targetDedicatedNodes` ve `targetLowPriorityNodes` hello havuzunun özelliklerini. Merhaba alt yetecek kadar boş IP adresi yoksa, hello Batch hizmeti, kısmen hello hello havuzdaki işlem düğümleri ayırır ve bir yeniden boyutlandırma hatası döndürür.

* alt ağ hello Batch hizmeti toobe gelen iletişimi mümkün tooschedule görevleri hello işlem düğümlerinde izin vermelidir Hello belirtilmiş. İletişim toohello işlem düğümleri tarafından reddedilir bir **ağ güvenlik grubu (NSG)** hello Batch hizmeti çok hello işlem düğümleri hello durumunu ayarlar sonra VNet, hello ile ilişkili**kullanılamaz**.

* Merhaba VNet ilişkilendirilen belirtilmişse **ağ güvenlik grupları (Nsg'ler)** ve/veya bir **Güvenlik Duvarı**, sonra da gelen iletişimi için birkaç ayrılmış sistem bağlantı noktalarının etkinleştirilmesi gerekir:

- Sanal makine yapılandırmasıyla oluşturulan havuzlar için 29876 ve 29877 numaralı bağlantı noktalarına ek olarak Linux için 22 numaralı ve Windows için de 3389 numaralı bağlantı noktalarını etkinleştirin. 
- Bulut hizmeti yapılandırmasıyla oluşturulan havuzlar için 10100, 20100 ve 30100 numaralı bağlantı noktalarını etkinleştirin. 
- Depolama bağlantı noktası 443 üzerinden giden bağlantılar tooAzure etkinleştirin. Ayrıca, Azure Depolama uç noktanızın sanal ağınızda kullanılan özel DNS sunucuları tarafından çözümlenebildiğinden emin olun. Özellikle, bir URL hello formun `<account>.table.core.windows.net` çözümlenebilir olmalıdır.

    Merhaba aşağıdaki tabloda açıklanmaktadır hello gelen tooenable hello sanal makine yapılandırması ile oluşturulan havuzları için gereken bağlantı noktaları:

    |    Hedef Bağlantı Noktaları    |    Kaynak IP adresi      |    Batch, NSG ekliyor mu?    |    Kullanılabilir VM toobe için gerekli mi?    |    Kullanıcı eylemi   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>Merhaba sanal makine yapılandırması ile oluşturulan havuzları: 29876, 29877</li><li>Merhaba bulut hizmeti yapılandırması ile oluşturulan havuzları: 10100, 20100, 30100</li></ul>         |    Yalnızca Batch hizmeti rolü IP adresleri |    Evet. Toplu Nsg'leri ağ arabirimleri (NIC) bağlı tooVMs hello düzeyinde ekler. Bu NSG'ler yalnızca Batch hizmeti rolü IP adreslerinden gelen trafiğe izin verir. Merhaba tüm web için bu bağlantı noktalarını açın olsa bile hello trafiği NIC hello engellenen |    Evet  |  Toplu iş yalnızca toplu IP adreslerine izin verdiğinden toospecify bir NSG gerekmez. <br /><br /> Ancak bir NSG belirtirseniz bu bağlantı noktalarının gelen trafiğe açık olduğundan emin olun. <br /><br /> Belirtirseniz * kaynak IP, nsg'deki hello gibi toplu Nsg'ler hala bağlı NIC tooVMs hello düzeyinde ekler.. |
    |    3389, 22               |    Hata ayıklama amacıyla, böylece hello VM uzaktan erişebilir kullanılan kullanıcı makineler.    |    Hayır                                    |    Hayır                     |    Toopermit uzaktan erişim (RDP/SSH) toohello VM istiyorsanız Nsg'ler ekleyin.   |                 

    Aşağıdaki tablonun hello tooenable toopermit erişim tooAzure depolama gereksinim hello giden bağlantı noktası açıklanmaktadır:

    |    Giden Bağlantı Noktaları    |    Hedef    |    Batch, NSG ekliyor mu?    |    Kullanılabilir VM toobe için gerekli mi?    |    Kullanıcı eylemi    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Azure Storage    |    Hayır    |    Evet    |    Tüm Nsg'ler eklerseniz, bu bağlantı noktası açık toooutbound trafiği olduğunu doğrulayın.    |


## <a name="scaling-compute-resources"></a>İşlem kaynaklarını ölçeklendirme
İle [otomatik ölçeklendirmeyi](batch-automatic-scaling.md), hello Batch hizmeti hello toohello mevcut iş yüküne ve kaynak kullanımını işlem senaryonuzun göre bir havuzdaki işlem düğümü sayısını dinamik olarak ayarlamasını sağlayabilirsiniz. Toolower hello böylece yalnızca hello kaynakları kullanarak uygulamanızı çalıştıran genel maliyeti, gerekir ve bu serbest olması gerekmez.

Bir [otomatik ölçeklendirme formülü](batch-automatic-scaling.md#automatic-scaling-formulas) yazıp bu formülü bir havuzla ilişkilendirerek otomatik ölçeklendirmeyi etkinleştirebilirsiniz. Merhaba Batch hizmeti hello formül toodetermine hello hedef düğüm sayısını hello havuzunda hello sonraki ölçeklendirme aralığı (sizin yapılandırabileceğiniz bir aralık) kullanır. Bunu oluşturduğunuzda ya da bir havuz üzerinde ölçeklendirmeyi daha sonra etkinleştirebilir hello bir havuz için otomatik ölçeklendirme ayarlarını belirtebilirsiniz. Hello ayarları ölçeklendirme özellikli bir havuz üzerinde ölçeklendirme da güncelleştirebilirsiniz.

Örnek olarak, bir iş yürütülen görevler toobe çok fazla sayıda gönderme belki de gerektirir. Merhaba hello geçerli kuyruğa alınmış görevlerin sayısı ve hello hello işteki hello görevlerin tamamlanma oranı temelinde hello havuzdaki düğüm sayısını ayarlayan bir ölçeklendirme formülü toohello havuzu atayabilirsiniz. Merhaba Batch hizmeti düzenli aralıklarla hello formülü değerlendirir ve hello havuz, iş yükü ve diğer formül ayarlarınıza göre yeniden boyutlandırır. Merhaba hizmeti çok sayıda kuyruğa alınmış görevlerin olduğunda gerektiğinde düğüm ekler ve hiçbir sıraya alınan ya da çalışmayan görevler olduğunda düğümleri kaldırır.

Ölçeklendirme formülü aşağıdaki ölçümleri hello üzerinde temel alabilir:

* **Zaman ölçümleri** belirtilen hello beş dakikada bir toplanan istatistikleri temel saat sayısı.
* **Kaynak ölçümleri** CPU kullanımı, bant genişliği kullanımı, bellek kullanımı ve düğüm sayısını temel alır.
* **Görev ölçümleri**; *Etkin* (kuyruğa alınmış) *Çalışıyor* veya *Tamamlandı* gibi görev durumlarını temel alır.

Otomatik ölçeklendirme bir havuzdaki işlem düğümleri hello sayısını azalttığında nasıl hello hello anda çalışan toohandle görevleri işlemi azaltmak dikkate almanız gerekir. tooaccommodate Bu, toplu sağlayan bir *düğüm ayırmasını kaldırma seçeneği* formüllerinize dahil edebileceğiniz. Örneğin, çalışmakta olan görevlerin hemen durdurulup, hemen durdurulup ve ardından başka bir düğümde yürütülmek yeniden kuyruğa veya hello düğüm hello havuzdan kaldırılmadan önce toofinish izin olduğunu belirtebilirsiniz.

Bir uygulamayı otomatik olarak ölçeklendirme hakkında daha fazla bilgi için bkz. [Azure Batch havuzunda işlem düğümlerini otomatik olarak ölçeklendirme](batch-automatic-scaling.md).

> [!TIP]
> toomaximize kaynak kullanımı işlem, bir işin hello sonunda hello hedef düğümleri toozero sayısını ayarlayın ancak çalışan görevler toofinish izin.
>
>

## <a name="security-with-certificates"></a>Sertifikalar ile güvenlik
Şifrelemek veya şifresini çözmek için başlangıç anahtarı gibi görevler için hassas bilgileri toouse sertifikaları genellikle gereken bir [Azure depolama hesabı][azure_storage]. toosupport Bu, düğümlere sertifikalar yükleyebilirsiniz. Şifrelenmiş parolalar tootasks komut satırı parametreleri aracılığıyla düğümlere geçirilir ya hello görev kaynaklarından birine eklenir ve yüklü hello sertifikaları kullanılan toodecrypt olabilir bunları.

Merhaba kullandığınız [sertifika Ekle] [ rest_add_cert] işlemini (Batch REST) ya da [CertificateOperations.CreateCertificate] [ net_create_cert] yöntemini (Batch .NET) tooadd sertifika tooa toplu işlem hesabı. Bu gibi durumlarda, hello sertifika sonra yeni veya mevcut bir havuzla ilişkilendirebilirsiniz. Bir sertifika bir havuzla ilişkilendirildiğinde, Batch hizmeti hello hello sertifikayı hello havuzdaki her düğüme yükler. Merhaba düğüm, (Merhaba başlangıç görevi ve iş yöneticisi görevi dahil) herhangi bir görevi başlatmadan önce başlatıldığında hello Batch hizmeti hello uygun sertifikaları yükler.

Sertifikaları tooan eklerseniz *varolan* havuzu, uygulanan toobe toohello düğümleri hello sertifikaları için işlem düğümleri yeniden başlatılması gerekir.

## <a name="error-handling"></a>Hata işleme
Gerekli toohandle bulabileceğiniz içinde Batch çözümündeki görev ve uygulama hataları.

### <a name="task-failure-handling"></a>Görev hatası işleme
Görev hataları kategorileri şunlardır:

* **Ön işleme hataları**

    Toostart bir görev başarısız olursa, önceden işleme hatasını hello görev için ayarlanır.  

    İşleme hataları önceden hello görevin kaynak dosyalarının taşınmış olması, hello depolama hesabı artık mevcut değil ya da başka bir sorunla karşılaşıldı önlenmiş hello olarak başarılı kopyalanmasını toohello düğümü dosyaları ortaya çıkabilir.

* **Karşıya dosya yükleme hataları**

    Bir görev için belirtilen dosya karşıya yükleme için herhangi bir nedenle başarısız olursa, bir dosya karşıya yükleme hatası hello görev için ayarlanır.

    Dosya karşıya yükleme dosyalarının başarıyla kopyalanmasını hello Azure depolamaya erişme geçersiz ya da hello depolama hesabı artık kullanılabilir değilse yazma izinleri sağlamaz veya başka bir sorun varsa sağlanan SAS engelleyen karşılaştıysanız hello hatalar oluşabilir Merhaba düğümü.    

* **Uygulama hataları**

    Merhaba görevin komut satırı tarafından belirtilen hello işlem de başarısız olabilir. Merhaba işlem hello görev tarafından yürütülen hello işlemi tarafından sıfır olmayan çıkış kodu döndürüldüğünde başarısız toohave kabul edilir (bkz *Görev çıkış kodları* hello sonraki bölümde).

    Uygulama hataları için toplu yapılandırabilirsiniz tooautomatically yeniden deneme hello görev tooa yukarı kaç kez belirtilmiş.

* **Kısıtlama hataları**

    Merhaba hello iş ya da görev için maksimum yürütme süresini belirleyen bir kısıtlama ayarlayabilirsiniz *maxWallClockTime*. Bu, tooprogress başarısız görevlerin sonlandırılması için faydalı olabilir.

    Merhaba en uzun süreyi aştığında hello görev olarak işaretlenmiş *tamamlandı*, ancak hello çıkış kodu çok ayarlamak`0xC000013A` ve hello *schedulingError* alanı olarak işaretlenmiş `{ category:"ServerError", code="TaskEnded"}`.

### <a name="debugging-application-failures"></a>Uygulama hatalarını ayıklama
* `stderr` ve `stdout`

    Yürütme sırasında bir uygulama tootroubleshoot sorunları kullanabileceğiniz tanılama çıktıları üretebilir. Hello belirtildiği gibi bölümüne [dosyaları ve dizinleri](#files-and-directories), hello Batch hizmeti Yazar standart çıktı ve standart hata çok çıktı`stdout.txt` ve `stderr.txt` hello hello görev dizininde dosyalarda işlem düğümü. Bu dosyalar hello Azure portal veya hello Batch SDK'ları toodownload birini kullanabilirsiniz. Örneğin, bunlar ve diğer dosyaları kullanarak sorun giderme amacıyla alabilirsiniz [ComputeNode.GetNodeFile] [ net_getfile_node] ve [CloudTask.GetNodeFile] [ net_getfile_task] hello Batch .NET Kitaplığı'nda.

* **Görev çıkış kodları**

    Daha önce belirtildiği gibi bir görev hello görev tarafından yürütülen hello işlem sıfır olmayan çıkış kodu döndürürse hello Batch hizmeti tarafından başarısız olarak işaretlenir. Bir görev bir işlemi yürüttüğünde Batch hello görevin çıkış kodu özelliğini hello ile doldurur *dönüş kodu hello işleminin*. Bir görevin çıkış kodu önemli toonote olan **değil** hello Batch hizmeti tarafından belirlenir. Bir görevin çıkış kodu hello işlemin kendisi ya da yürütülen hello işlemi hello işletim sistemine göre belirlenir.

### <a name="accounting-for-task-failures-or-interruptions"></a>Görev hataları veya kesintilerinin sebepleri
Görevler zaman zaman başarısız olabilir veya kesintiye uğrayabilir. Merhaba görevin kendisi başarısız olabilir, hangi hello üzerinde görevin çalıştığı hello düğüm yeniden başlatılabilir ya da hello havuzun ayırmayı kaldırma İlkesi bekleniyor olmadan hemen kümesi tooremove düğüm olması durumunda hello düğüm hello havuzundan bir yeniden boyutlandırma işlemi sırasında Kaldırılabilir görevleri toofinish. Tüm durumlarda hello görev otomatik olarak toplu işi tarafından başka bir düğümde yürütülmek yeniden kuyruğa.

Ayrıca bir aralıklı sorunun toocause görev toohang mümkündür veya çok uzun tooexecute alın. Bir görev için başlangıç maksimum yürütme aralığı ayarlayabilirsiniz. Merhaba maksimum yürütme aralığı aşılırsa hello Batch hizmeti hello görev uygulamasını kesintiye uğratır.

### <a name="connecting-toocompute-nodes"></a>Toocompute düğümlerini bağlayan
Ek hata ayıklama ve tooa işlem düğümünde uzaktan oturum açarak sorun giderme işlemlerini gerçekleştirebilirsiniz. Windows düğümleri için hello Azure portal toodownload bir Uzak Masaüstü Protokolü (RDP) dosyası kullanın ve Linux düğümleri için güvenli Kabuk (SSH) bağlantı bilgilerini alın. Ayrıca ile örneğin hello Batch API'lerini kullanarak bunu yapabilirsiniz [Batch .NET] [ net_rdpfile] veya [Batch Python](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh).

> [!IMPORTANT]
> RDP veya SSH aracılığıyla tooconnect tooa düğümü, hello düğümde bir kullanıcı ilk oluşturmanız gerekir. toodo bunu hello Azure portalını kullanabilirsiniz [bir kullanıcı hesabı tooa düğüm eklemek] [ rest_create_user] hello Batch REST API'si kullanarak hello çağrısı [ComputeNode.CreateComputeNodeUser] [ net_create_user] Batch .NET veya çağrı hello yöntemini [add_user] [ py_add_user] hello Batch Python modülünde yöntemi.
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>Sorunlu işlem düğümleriyle ilgili sorunları giderme
Burada bazı görevlerinizin başarısız olduğu durumlarda, Batch istemci uygulamanız veya hizmetiniz başarısız hello görevleri tooidentify hatalı davranan düğümü hello meta verilerini inceleyebilirsiniz. Bir havuzdaki her düğüme benzersiz bir kimlik verilir ve bir görevin çalıştığı hello düğüm hello görev meta verilerine eklenir. Bir sorun düğümünü tanımladıktan sonra bununla birkaç eylem gerçekleştirebilirsiniz:

* **Merhaba düğümü yeniden başlatma** ([REST][rest_reboot] | [.NET][net_reboot])

    Yeniden başlatma hello düğümü bazen takılan veya çöken işlemler gibi görünmeyen sorunları temizleyebilir. Merhaba düğüm başlatıldığında havuzunuz bir başlangıç görevi kullanıyorsa ya da işiniz iş hazırlama görevi kullanıyorsa, bunlar yürütülür olduğunu unutmayın.
* **Merhaba düğümün görüntüsünü yeniden oluşturma** ([REST][rest_reimage] | [.NET][net_reimage])

    Bu hello işletim sistemi hello düğüme yeniden yükler. Düğümün yeniden başlatılmasıyla gibi başlatma ve görevleri hello düğümün görüntüsünün yeniden oluşturulmasının sonra iş hazırlama görevleri yeniden çalıştırılır.
* **Merhaba düğümü hello havuzundan kaldırmak** ([REST][rest_remove] | [.NET][net_remove])

    Bazen, gerekli toocompletely Kaldır hello hello havuzundan düğümdür.
* **Merhaba düğümde görev zamanlamayı devre dışı** ([REST][rest_offline] | [.NET][net_offline])

    Bu etkili bir şekilde hello düğümü çevrimdışı böylece başka görev tooit atanmış, ancak hello düğümü tooremain çalışmasını sağlar ve hello havuzunda alır. Bu, tooperform ayrıntılı araştırma hello neden hello hatalar hello başarısız olan görevin verilerini kaybetmeden ve hello düğüm başka görev hatalarına neden olmadan sağlar. Örneğin, ardından hello düğümde görev zamanlamayı devre dışı bırakabilirsiniz [uzaktan oturum](#connecting-to-compute-nodes) tooexamine düğümün olay günlüklerini hello veya diğer sorun giderme gerçekleştirir. Araştırmanızı bitirdikten sonra daha sonra yeniden çevrimiçi hello düğümü görev zamanlamayı getirebilir ([REST][rest_online] | [.NET] [ net_online]), ya da hello birini daha önce bahsedilen başka eylemler gerçekleştirebilir.

> [!IMPORTANT]
> Bu bölümde açıklanan her bir eylemde ile yeniden başlatma, yeniden görüntü oluşturma, kaldırma ve devre dışı bırak görev zamanlamayı olduğunuz nasıl şu anda hello düğümde çalışan görevler işlenir hello eylemi gerçekleştirdiğinizde mümkün toospecify. Örneğin, devre dışı bıraktığınızda, belirtebilirsiniz hello Batch .NET istemci kitaplığını kullanarak bir düğümde görev zamanlamayı bir [sonlandırma] [ net_offline_option] numaralandırma değeri toospecify çok olup olmadığını**Sonlandır** , çalışan görevleri **Disablecomputenodeschedulingoption** diğer düğümlerde zamanlama için veya hello eylemi gerçekleştirmeden önce çalışan görevlerin toocomplete izin ver (**Net_offline_option**).
>
>

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba hakkında bilgi edinin [Batch API'lerini ve araçları](batch-apis-tools.md) Batch çözümleri oluşturmak için kullanılabilir.
* Örnek bir Batch uygulaması içindeki adım adım rehberlik [.NET için Azure Batch kitaplığını hello ile çalışmaya başlama](batch-dotnet-get-started.md). Ayrıca bir [Python sürümü](batch-python-tutorial.md) işlem düğümleri hello öğreticinin bir iş yükü Linux üzerinde çalışır.
* Karşıdan yükle ve hello yapı [Batch Gezgini] [ github_batchexplorer] Batch çözümlerinizi geliştirirken kullanmak için örnek proje. Merhaba Batch Explorer kullanarak, hello aşağıdakileri ve daha fazlasını gerçekleştirebilirsiniz:

  * Batch hesabınızdaki havuzlar, işler ve görevleri izleme ve düzenleme
  * Düğümlerden `stdout.txt`, `stderr.txt` ve diğer dosyaları indirme
  * Düğümlerde kullanıcı oluşturma ve uzaktan oturum açma için RDP dosyalarını indirme
* Nasıl çok öğrenin[Linux işlem düğümleri havuzları oluşturma](batch-linux-nodes.md).
* Merhaba ziyaret [Azure Batch forumunu] [ batch_forum] konusuna bakın. Merhaba forum, iyi bir yerleştirin tooask sorular, yeni ya da toplu kullanarak Uzman olmanıza ' dir.

[1]: ./media/batch-api-basics/node-folder-structure.png

[azure_storage]: https://azure.microsoft.com/services/storage/
[batch_forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch
[cloud_service_sizes]: ../cloud-services/cloud-services-sizes-specs.md
[msmpi]: https://msdn.microsoft.com/library/bb524831.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_sample_taskdeps]:  https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch_net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[msdn_env_vars]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[net_cloudjob_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobmanagertask.aspx
[net_cloudjob_priority]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.priority.aspx
[net_cloudpool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_cloudtask_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.environmentsettings.aspx
[net_create_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.createcertificate.aspx
[net_create_user]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.createcomputenodeuser.aspx
[net_getfile_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getnodefile.aspx
[net_getfile_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.getnodefile.aspx
[net_job_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.commonenvironmentsettings.aspx
[net_multiinstancesettings]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_onalltaskscomplete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.onalltaskscomplete.aspx
[net_rdp]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getrdpfile.aspx
[net_reboot]: https://msdn.microsoft.com/library/azure/mt631495.aspx
[net_reimage]: https://msdn.microsoft.com/library/azure/mt631496.aspx
[net_remove]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.removefrompoolasync.aspx
[net_offline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.disableschedulingasync.aspx
[net_online]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.enableschedulingasync.aspx
[net_offline_option]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.disablecomputenodeschedulingoption.aspx
[net_rdpfile]: https://msdn.microsoft.com/library/azure/Mt272127.aspx
[vnet]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_netconf

[py_add_user]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.ComputeNodeOperations.add_user

[batch_rest_api]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[rest_add_job]: https://msdn.microsoft.com/library/azure/mt282178.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_cert]: https://msdn.microsoft.com/library/azure/dn820169.aspx
[rest_add_task]: https://msdn.microsoft.com/library/azure/dn820105.aspx
[rest_create_user]: https://msdn.microsoft.com/library/azure/dn820137.aspx
[rest_get_task_info]: https://msdn.microsoft.com/library/azure/dn820133.aspx
[rest_job_schedules]: https://msdn.microsoft.com/library/azure/mt282179.aspx
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx
[rest_multiinstancesettings]: https://msdn.microsoft.com/library/azure/dn820105.aspx#multiInstanceSettings
[rest_update_job]: https://msdn.microsoft.com/library/azure/dn820162.aspx
[rest_rdp]: https://msdn.microsoft.com/library/azure/dn820120.aspx
[rest_reboot]: https://msdn.microsoft.com/library/azure/dn820171.aspx
[rest_reimage]: https://msdn.microsoft.com/library/azure/dn820157.aspx
[rest_remove]: https://msdn.microsoft.com/library/azure/dn820194.aspx
[rest_offline]: https://msdn.microsoft.com/library/azure/mt637904.aspx
[rest_online]: https://msdn.microsoft.com/library/azure/mt637907.aspx

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
