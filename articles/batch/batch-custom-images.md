---
title: "aaaProvision Azure Batch havuzları özel görüntülerden | Microsoft Docs"
description: "Özel görüntü tooprovision havuzundan işlem hello yazılım içeren düğümler ve uygulamanız için gereken verileri toplu oluşturabilirsiniz. Özel resimler tooconfigure işlem düğümleri toorun toplu iş yüklerinizi verimli bir yoludur."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/07/2017
ms.author: tamram
ms.openlocfilehash: 5cb698ee90f7d3ec9ffe69fa4dc602132c3f7569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-custom-image-toocreate-a-pool-of-virtual-machines"></a>Özel görüntü toocreate sanal makinelerin bir havuzu kullanın

Azure Batch sanal makinelerin bir havuz oluşturduğunuzda, hello havuzundaki her işlem düğümü hello işletim sistemi sağlayan bir sanal makine (VM) görüntüsü belirtin. Azure Market görüntü veya hazırladığınız özel bir VHD görüntüsü sağlayarak, sanal makinelerin bir havuz oluşturabilirsiniz. Özel görüntü sağladığınızda, her işlem düğümü sağlanan hello zaman hello işletim sisteminin nasıl yapılandırıldığına üzerinde kontrol sahibidir. Özel görüntünüzü de uygulamaları içerir ve sağlandığından hemen işlem düğümü üzerinde hello kullanılabilir başvuru verileri.

Özel görüntü kullanarak, havuzun işlem düğümleri alınırken zaman kazandırır toorun Toplu İş yükünüzün hazır. Her zaman Azure Market görüntü kullanır ve bunu sağlandıktan sonra her işlem düğümünde yazılım yüklerseniz olsa da, bu yaklaşım özel görüntü kullanmaktan daha az verimli olabilir. 

Bazı nedenlerden toouse senaryonuz için yapılandırılan özel bir görüntü içerir gerek:

- **Merhaba işletim sistemi (OS) yapılandırma** hello işletim sisteminin özel bir yapılandırma hello özel görüntü üzerinde gerçekleştirilebilir. 
- **Büyük uygulamalar yükleyin.** Özel bir görüntüde uygulamaları yükleme, sağlandıktan sonra her işlem düğümünde yüklemeden daha daha verimli olur.
- **Önemli miktarda veri kopyalayın.** Merhaba veri kopyalanan toohello özel görüntü ise, yalnızca bir kez, zaman ve bant genişliği tasarrufu tooeach işlem düğümü yerine, kopyaladığınız toobe gerekir.
- **Merhaba VM hello Kurulum işlemi sırasında yeniden başlatın.** İşlem düğümü sayısını özellikle varsa, yeniden başlatılan hello VM zaman alan bir işlem olabilir.

## <a name="prerequisites"></a>Ön koşullar

- **Merhaba kullanıcı abonelik havuzu ayırma modu kullanılarak oluşturulmuş bir toplu işlem hesabı.** toouse özel görüntü tooprovision sanal makine havuzları oluşturmak Batch hesabınıza hello kullanıcı aboneliği ile [havuzu ayırma modu](batch-api-basics.md#pool-allocation-mode). Bu modda, Batch havuzları hello hesabının bulunduğu hello aboneliğinize ayrılır. Merhaba bkz [hesap](batch-api-basics.md#account) bölümüne [geliştirme büyük ölçekli paralel işlem çözümleri yığın](batch-api-basics.md) bir Batch hesabı oluşturduğunuzda hello havuzu ayırma modunu ayarlama hakkında daha fazla bilgi için.

- **Bir Azure Depolama hesabı.** özel görüntü kullanarak sanal makineleri havuzu toocreate, gereksinim duyduğunuz hello standart, genel amaçlı Azure depolama hesabı aynı abonelikte ve bölgede. Ardından, özel bir görüntü bir Azure sanal makineden oluşturursanız, burada hello VM'ın işletim sistemi diski bulunur ve toocreate ayrı bir depolama hesabı gerekmez hello görüntü toohello depolama hesabı kopyalayacak. 
    
## <a name="prepare-a-custom-image"></a>Özel görüntü hazırlama

tooprepare toplu ile kullanılmak üzere özel bir görüntü, Linux veya Windows varolan bir yüklemesini generalize gerekir. Bir işletim sistemi yüklemesi genelleme makine özgü bilgileri kaldırır. Merhaba, diğer bilgisayarlar veya sanal makineleri yüklü bir görüntü sonucudur.  

> [!IMPORTANT]
> Batch şu anda desteklemiyor Azure kullanarak yönetilen görüntüleri tooprovision bir havuzu. Merhaba özel görüntü bir havuzu Azure depolama alanında depolanmalıdır tooprovision kullanın. 
>
> Özel görüntünüzü hazırlık yaparken, aşağıdaki noktaları göz önünde hello tutun:
> - Toplu havuzlarınızı mu tooprovision kullandığınız bu hello temel işletim sistemi görüntüsü olun hello özel betik uzantısı gibi Azure uzantıları herhangi bir önceden yüklemediyseniz. Merhaba görüntü önceden yüklenmiş bir uzantısı içeriyorsa, Azure hello VM dağıtma sorunlarla karşılaşabilirsiniz.
> - Merhaba toplu işlem düğüm Aracısı şu anda hello varsayılan geçici sürücü bekliyor olarak kullandığı varsayılan geçici sürücü hello sağlamak, hello temel işletim sistemi görüntü emin olun.
>
>

Özel görüntü var olan tüm hazırlanan Windows veya Linux görüntüsü kullanabilirsiniz. Örneğin, yerel bir görüntü toouse istiyor ve yeniden hello görüntü tooan Azure depolama hesabı karşıya aynı abonelikte ve bölgede Batch hesabı kullanılarak olarak hello [AzCopy](../storage/storage-use-azcopy.md) veya başka bir karşıya yükleme aracı.

Ayrıca, özel bir görüntü yeni veya var olan bir Azure VM'den hazırlayabilirsiniz. Yeni bir VM oluşturuyorsanız, bir Azure Market görüntüsü için özel görüntünüzü hello temel görüntü kullanın ve sonra özelleştirebilirsiniz. toocustomize hello temel görüntü, bir Azure VM oluşturun ve uygulamalar veya veri tooit ekleyin. Ardından, özel görüntü olarak hello VM tooserve generalize ve tooAzure depolama kaydedin. 

bir Azure VM özel bir görüntüden tooprepare şu adımları izleyin:

1. Oluşturma bir **yönetilmeyen** Azure Market görüntüsünden Azure VM. Azure Market her ikisi için görüntüleri içeren [Windows](../virtual-machines/windows/quick-create-portal.md) ve [Linux](../virtual-machines/linux/quick-create-portal.md).
    
    3. adım hello VM oluşturma işlemi, üzerinde seçtiğinizden emin olun **Hayır** için **Depolama: yönetilen diskleri kullanmak** seçeneği. Ayrıca bu depolama hesabı, ayrıca Azure özel görüntünüzü kaydedeceği olduğu gibi hello VM'ın işletim sistemi diski, hello depolama hesabı adını not edin:

    ![Bir yönetilmeyen VM oluşturup Not hello depolama hesabı adı](media/batch-custom-images/vm-create-storage.png)
 
2. Merhaba, VM oluşturma işlemi tamamlayın ve bekleyin Azure tarafından ayrılan toobe. Bir VM hello çalışır durumda hello Azure portalında gösteren görüntü şöyledir:

    ![Market görüntüsünden bir VM oluşturma](media/batch-custom-images/vm-status-running.png)

3. Merhaba VM çalışmaya başladıktan sonra (Windows için) RDP veya SSH (için Linux) aracılığıyla tooit bağlayın. Gerekli yazılımları yükleyebilir veya istenen verileri kopyalayıp hello VM generalize. Açıklanan başlangıç adımları [Generalize hello VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized.md#generalize-the-vm). 
   
4. Çok olarak Hello adımları[tooAzure PowerShell oturum](../virtual-machines/windows/sa-copy-generalized.md#log-in-to-azure-powershell). Azure PowerShell tooinstall bkz [Azure PowerShell genel bakış](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.2.0). 

5. Ardından, hello çok adımları[Deallocate hello VM ve kümesi hello durumu toogeneralized](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized#deallocate-the-vm-and-set-the-state-to-generalized). 

    Hello Azure portal'de, VM serbest bu hello dikkat edin:

    ![VM serbest bu hello emin olun](media/batch-custom-images/vm-status-deallocated.png)

6.  Oluşturun ve hello VM görüntü tooAzure depolama kaydedin hello kullanarak [Kaydet AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) PowerShell cmdlet'i. Açıklanan hello yönergeleri [oluşturma hello görüntü](../virtual-machines/windows/sa-copy-generalized.md#create-the-image).
    
    Merhaba VM görüntüsü hello VM oluşturulduğunda, bu yordamın 1. adımında gösterildiği gibi oluşturulan toohello Azure Storage hesabına kaydedilir. Merhaba Kaydet AzureRmVMImage cmdlet kaydeder hello görüntü toohello **sistem** bu depolama hesabı kapsayıcısında. Merhaba `-DestinationContainername` parametre adları bir sanal dizin hello içinde **sistem** kapsayıcı. Merhaba `-VHDNamePrefix` parametresi hello blob adı için bir önek belirtir. $A toohello blob adı bir tire ile önekidir. 

    Örneğin, şu parametreler hello ile Kaydet AzureRmVMImage çağrısı varsayın:  

        Save-AzureRmVMImage -ResourceGroupName sample-resource-group -Name vm-custom-image -DestinationContainerName batchimages -VHDNamePrefix custom -Path C:\Temp\Images\vm-custom-image.json

    Merhaba elde edilen görüntü toohello konumu ve burada gösterilen blob adı kaydedilir:

    ![Sistem kapsayıcısında kaydedilmiş VHD konumu](media/batch-custom-images/vhd-in-vm-storage-account.png)

    > [!NOTE]
    > Bir Azure yönetilmeyen VM birkaç depolama hesapları farklı amaçlar için oluşturur. Hello işletim sistemi diskinin hello zaman hello depolama kapsayıcısının hello adı not etmediniz, VM'nin oluşturulduğu ardından hello ilişkili depolama hesabı Bul içerir hello **sistem** kapsayıcı. Merhaba gidin **sistem** kapsayıcı toofind hello özel görüntü hello için belirttiğiniz hello değerleri kullanarak **Kaydet AzureRmVMImage** komutu.

## <a name="create-a-pool-from-a-custom-image-in-hello-portal"></a>Merhaba Portalı'nda özel bir görüntüden havuz oluşturma

Özel görüntünüzü kaydettikten sonra konumunu bilmeniz, bu görüntüden Batch havuzu oluşturabilirsiniz. Bu adımları toocreate bir havuzu hello Azure portal ' izleyin:

1. Tooyour Batch hesabında hello Azure portalına gidin. Bu hesap olmalıdır hello içeren hello özel görüntü aynı abonelikte ve bölgede hello depolama hesabı. 
2. Merhaba, **ayarları** sol, hello select hello penceresinde **havuzları** menü öğesi.
3. Merhaba, **havuzları** penceresinde, select hello **Ekle** komutu.
4. Merhaba üzerinde **havuzu Ekle** penceresinde, seçin **özel görüntü (Linux/Windows)** hello gelen **görüntü türü** açılır. Merhaba portal görüntüler hello **özel görüntü** Seçici. Özel görüntünüzü bulunduğu toohello depolama hesabına gidin ve seçin hello kapsayıcı istenen VHD'den hello. 
5. Select hello doğru **teklif/yayımcı/Sku** özel VHD için.
6. Merhaba kalan gerekli hello dahil ayarlarını belirtin **düğüm boyutu**, **ayrılmış düğümleri hedef**, ve **düşük öncelik düğümleri**, yanı sıra tüm isteğe bağlı ayarlar istenen.

    Örneğin, Microsoft Windows Server Datacenter 2016 özel görüntü için hello **havuzu Ekle** penceresi, aşağıda gösterildiği gibi görünür:

    ![Özel Windows görüntüsünü havuzu ekleme](media/batch-custom-images/add-pool-custom-image.png)
  
toocheck var olan bir havuzu özel bir görüntü üzerinde bağlı olup olmadığını görmek hello **işletim sistemi** hello kaynak Özet bölümündeki hello özelliği **havuzu** penceresi. Merhaba havuzu özel bir görüntüden oluşturduysanız, çok ayarlanır**özel VM görüntüsü**.

Bir havuzuyla ilişkili tüm özel VHD'leri hello havuzunun üzerinde görüntülenen **özellikleri** penceresi.
 
## <a name="next-steps"></a>Sonraki adımlar

- Toplu ayrıntılı bir bakış için bkz: [geliştirme büyük ölçekli paralel işlem çözümleri yığın](batch-api-basics.md).
- Batch hesabı oluşturma hakkında daha fazla bilgi için bkz: [hello Azure portal ile bir toplu işlem hesabı oluşturun](batch-account-create-portal.md).
