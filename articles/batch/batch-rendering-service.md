---
title: "aaaUse hello Azure toplu işleme hizmeti toorender hello bulutta | Microsoft Docs"
description: "İşleri, doğrudan Maya üzerinden veya kullanım başına ödeme temelinde Azure sanal makinelerinde işleyin."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a>Toplu işleme hizmeti Hello ile çalışmaya başlama

Hello Azure toplu işleme hizmeti kullanım başına ödeme temelinde bulut ölçekli işleme yetenekleri sunar. Merhaba toplu işleme hizmeti iş planlama ve çağrısı yönetme hataları ve yeniden deneme ve işleme işinizi otomatik olarak ölçeklendirme işler. Hello toplu işleme hizmeti Autodesk Maya, 3ds desteklediği en fazla ve yakında diğer uygulamalar için destek ile Arnold. Merhaba toplu Maya 2017 için eklenti kolay toostart işleme iş Azure üzerinde masaüstünüzden sağ kolaylaştırır. 

## <a name="supported-applications"></a>Desteklenen uygulamalar

Merhaba toplu işleme Hizmet şu anda uygulamaları aşağıdaki hello destekler:

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>Ön koşullar

Toplu işleme toouse hello hizmeti, aşağıdakiler gerekir:

- Bir [Azure hesabı](https://azure.microsoft.com/free/). 
- **Bir Azure Batch hesabı.** Hello Azure portalında bir Batch hesabı oluşturma konusunda yönergeler için bkz: [hello Azure portal ile bir toplu işlem hesabı oluşturun](batch-account-create-portal.md).
- **Bir Azure Depolama hesabı.** Merhaba varlıklar oluşturma işlemi için kullanılan Azure depolama alanında depolanır. Batch hesabınızı ayarlarken otomatik olarak bir depolama hesabı oluşturabilirsiniz. Ayrıca mevcut bir depolama hesabını kullanabilirsiniz. Depolama hesapları hakkında daha fazla toolearn bkz [nasıl toocreate, yönetme veya hello Azure portalında bir depolama hesabını silme](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

toouse hello toplu Maya eklenti, gerekir:

- **Maya 2017**
- **Arnold for Maya**

Merhaba de kullanabilirsiniz [Azure portal](https://portal.azure.com) toocreate havuzları 3ds Maya ile önceden yapılandırılmış sanal makinelerin en fazla ve Arnold. Uygulama günlüklerini yükleyerek ve RDP veya SSH kullanarak tooindividual VM'ler uzaktan bağlanarak başarısız görevlerin tanılamak ve hello portal toomonitor işleri kullanın.

## <a name="basic-batch-concepts"></a>Temel Batch kavramları

Merhaba toplu işleme hizmeti kullanmaya başlamadan önce işlem düğümleri, havuzlar ve işler de dahil olmak üzere birkaç toplu, kavramlarını yararlı toobe var. Azure Batch hakkında daha fazla genel olarak, bkz: toolearn [toplu işlemle doğası gereği paralel iş yüklerini çalıştırmak](batch-technical-overview.md).

### <a name="pools"></a>Havuzlar

Batch, işleme gibi işlem yoğunluklu çalışmaları bir **işlem düğümü** **havuzu** üzerinde gerçekleştirmeye yönelik bir platform hizmetidir. Bir havuzdaki her işlem düğümü, Linux veya Windows çalıştıran bir Azure sanal makinesidir (VM). 

Merhaba Batch havuzları ve işlem düğümleri hakkında daha fazla bilgi için bkz: [havuzu](batch-api-basics.md#pool) ve [işlem düğümü](batch-api-basics.md#compute-node) bölümler [geliştirme büyük ölçekli paralel işlem çözümleri toplu ile](batch-api-basics.md).

### <a name="jobs"></a>İşler

Bir toplu **iş** hello üzerinde çalışan görevleri koleksiyonu işlem düğümleri havuzunda değil. Bir işleme iş gönderdiğinizde, toplu hello iş görevlere böler ve hello görevleri toohello işlem düğümlerine hello havuzu toorun dağıtır.

Merhaba toplu işlemler hakkında daha fazla bilgi için bkz: [iş](batch-api-basics.md#job) bölümüne [geliştirme büyük ölçekli paralel işlem çözümleri yığın](batch-api-basics.md).

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a>Merhaba toplu eklenti Maya toosubmit işleme iş kullanın

Merhaba Maya için eklenti toplu iş toohello hizmet Maya sağ toplu işleme gönderebilirsiniz. Aşağıdaki bölümlerde hello nasıl tooconfigure hello eklenti işleminden hello ve ardından göndermek açıklanmaktadır. 

### <a name="load-hello-batch-plug-in-in-maya"></a>Merhaba toplu iş içinde Maya eklentisini yükleme

Merhaba toplu eklenti edinilebilir [GitHub](https://github.com/Azure/azure-batch-maya/releases). Tercih ettiğiniz Hello arşiv tooa dizini sıkıştırmasını açın. Doğrudan hello hello eklenti yükleyebilir *azure_batch_maya* dizini.

tooload hello Maya içinde eklenti:

1. Maya’yı çalıştırın.
2. **Pencere** > **Ayarlar/Tercihler** > **Eklenti Yöneticisi**’ni açın.
3. **Gözat**’a tıklayın.
4. Tooand seçin gidin *azure_batch_maya/plug-in/AzureBatch.py*.

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a>Erişim tooyour Batch ve Storage hesaplarını kimlik doğrulaması

toouse hello eklentisi, Azure Batch ve Azure depolama hesabı anahtarlarını kullanarak tooauthenticate gerekir. tooretrieve hesabı anahtarlarınızı:

1. Görüntü hello Maya içinde eklenti ve select hello **Config** sekmesi.
2. Toohello gidin [Azure portal](https://portal.azure.com).
3. Seçin **toplu işlem hesaplarını** hello sol taraftaki menüden. Gerekirse, **Diğer Hizmetler**’e tıklayıp _Batch_ filtresi uygulayın.
4. İstenen hello toplu işlem hesabı hello listesinde bulun.
5. Select hello **anahtarları** menü öğesi toodisplay hesap adı, hesap URL'si ve erişim anahtarları:
    - Merhaba Batch hesabı URL'si hello yapıştırma **hizmet** hello toplu eklenti alanındaki.
    - Merhaba içine yapıştırma hello hesap adı **toplu işlem hesabı** alan.
    - Merhaba içine yapıştırma hello birincil hesap anahtarı **toplu anahtar** alan.
7. Depolama hesaplarını hello sol taraftaki menüden seçin. Gerekirse, **Diğer Hizmetler**’e tıklayıp _Depolama_ filtresi uygulayın.
8. İstenen hello depolama hesabı hello listesinde bulun.
9. Select hello **erişim tuşları** menü öğesi toodisplay hello depolama hesabı adı ve anahtarları.
    - Yapıştır hello depolama hesabı adı hello içine **depolama hesabı** hello toplu eklenti alanındaki.
    - Merhaba içine yapıştırma hello birincil hesap anahtarı **depolama anahtarı** alan.
10. Tıklatın **kimlik doğrulama** eklenti hello tooensure, her iki hesap erişebilir.

Başarıyla doğrulandıktan sonra hello Eklenti kümeleri durumu alanı çok hello**kimlik doğrulaması yapılmış**: 

![Batch ve Depolama hesaplarınız için kimlik doğrulaması](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>İşleme işi için havuz yapılandırma

Batch ve Storage hesaplarınızın kimliğini doğruladıktan sonra, işleme işinize yönelik bir havuz oluşturun. Merhaba eklenti seçimlerinizi oturumları arasında kaydeder. Tercih edilen yapılandırmanızı ayarladıktan sonra toomodify gerekmez, bu değiştirilmediği sürece.

Merhaba aşağıdaki bölümlerde, hello kullanılabilir seçenekler, hello üzerinde kullanılabilir size rehberlik **gönderme** sekmesi:

#### <a name="specify-a-new-or-existing-pool"></a>Yeni veya var olan bir havuzu belirtme

hangi toorun hello işleme işi, select hello havuzunda a toospecify **gönderme** sekmesi. Bu sekme bir havuz oluşturma veya var olan bir havuzu seçme seçeneklerini sunar:

- Yapabilecekleriniz **otomatik sağlama bu iş için bir havuz** (Merhaba varsayılan seçenek). Bu seçeneği seçtiğinizde, toplu hello geçerli iş için özel olarak hello havuz oluşturur ve hello işlemek, işi siler hello havuzuna otomatik olarak tamamlanır. Bir tek işleme iş toocomplete varsa, bu en iyi bir seçenektir.
- **Var olan kalıcı havuzu yeniden kullanabilirsiniz**. Boşta var olan bir havuzu varsa, bu havuzu için çalışan hello işleme işi hello aşağı açılır listeden seçerek belirtebilirsiniz. Var olan bir kalıcı havuzu yeniden hello gereken süre tooprovision hello havuzu kaydeder.  
- **Yeni bir kalıcı havuz oluşturabilirsiniz**. Bu seçeneğin belirlenmesi hello işi çalıştırmak için yeni bir havuz oluşturur. Böylece gelecekteki işleri yeniden hello iş tamamlandıktan sonra hello havuzu silmez. İşlerini işlemek sürekli gerek toorun gerektiğinde bu seçeneği seçin. Sonraki işlere seçtiğiniz **varolan kalıcı havuzunu yeniden** toouse hello hello ilk iş için oluşturulan kalıcı havuzu.

![Havuz, işletim sistemi görüntüsü, VM boyutu ve lisans belirtme](./media/batch-rendering-service/submit.png)

Merhaba nasıl Azure VM'ler için Ücret tahakkuk daha fazla bilgi için bkz: [Linux fiyatlandırma SSS](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) ve [Windows fiyatlandırma hakkında SSS](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).

#### <a name="specify-hello-os-image-tooprovision"></a>Merhaba işletim sistemi görüntüsü tooprovision belirtin

İşletim sistemi görüntüsü toouse tooprovision işlem düğümleri hello türü hello hello havuzunda belirtebilirsiniz **Env** (ortamı) sekmesi. Toplu işlerini işlemeye görüntü seçenekleri aşağıdaki hello şu anda destekler:

|İşletim Sistemi  |Görüntü  |
|---------|---------|
|Linux     |Batch CentOS Önizlemesi |
|Windows     |Batch Windows Önizlemesi |

#### <a name="choose-a-vm-size"></a>VM boyutu seçme

Merhaba üzerinde hello VM boyutu belirtebilirsiniz **Env** sekmesi. Kullanılabilir VM boyutları hakkında daha fazla bilgi için bkz. [Azure’da Linux VM boyutları](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) ve [Azure’da Windows VM boyutları](https://docs.microsoft.com/azure/virtual-machines/windows/sizes). 

![Merhaba Env sekmesinde Hello VM işletim sistemi görüntüsü ve boyutunu belirtin](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>Lisanslama seçeneklerini belirtme

Merhaba üzerinde toouse istediğiniz hello lisansları belirtebilirsiniz **Env** sekmesi. Seçeneklere şunlar dahildir:

- Varsayılan olarak etkin olan **Maya**.
- **ARNOLD**, Arnold Maya hello etkin işleme altyapısı olarak algılanırsa, etkin.

 Toorender kendi lisansınızı kullanmak istiyorsanız, hello uygun ortam değişkenleri toohello tablo ekleyerek, lisans bitiş noktası yapılandırabilirsiniz. Bunu yaparsanız emin toodeselect hello varsayılan lisans seçenekleri olabilir.

> [!IMPORTANT]
> VM'ler hello havuzunda çalışırken hello VM'ler değil şu anda kullanıldığından işleme için bile hello lisansları kullanım için faturalandırılır. tooavoid ek giderleri gidin toohello **havuzları** sekmesinde ve hazır toorun olana kadar hello havuzu too0 düğümleri başka bir işleme iş yeniden boyutlandırın. 
>
>

#### <a name="manage-persistent-pools"></a>Kalıcı havuzları yönetme

Merhaba üzerinde var olan bir kalıcı havuzu yönetebilirsiniz **havuzları** sekmesi. Bir havuzu hello listeden seçerek hello hello havuzunun geçerli durumu görüntüler.

Merhaba gelen **havuzları** sekmesinde de hello havuzunu silme ve VM hello havuzunda hello sayısı yeniden boyutlandırın. İş yükleri arasında herhangi bir maliyet havuzu too0 düğümleri tooavoid yeniden boyutlandırabilirsiniz.

![Havuzları görüntüleme, yeniden boyutlandırma ve silme](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>İşleme işini göndermek üzere yapılandırma

Merhaba işleme iş hello havuzu için başlangıç parametreleri belirledikten sonra hello işin kendisinin yapılandırın. 

#### <a name="specify-scene-parameters"></a>Sahne parametrelerini belirtme

Hello toplu eklentisi şu anda kullanmakta olduğunuz hangi işleme altyapısı içinde Maya algılar ve görüntüler hello uygun işlemek hello ayarlarını **gönderme** sekmesi. Bu ayarlar hello başlangıç çerçevesi, son çerçeve, çıktı öneki ve çerçeve adım içerir. Merhaba eklenti farklı ayarlar belirterek hello Sahne dosya oluşturma ayarlarını geçersiz kılabilirsiniz. Tooreupload hello Sahne dosya gerek kalmadan bir proje işi temelinde değişiklik yapabilmek eklenti ayarlarını toohello yaptığınız değişiklikler kalıcı arka toohello Sahne dosya işleme ayarları olmayan.

Merhaba eklenti hello Maya içinde seçili altyapısı oluşturmak isteyip desteklenmiyor konusunda sizi uyarır.

Yeni Sahne Hello eklenti açıkken yüklerseniz, hello tıklatın **yenileme** düğme toomake emin hello ayarları güncelleştirilir.

#### <a name="resolve-asset-paths"></a>Varlık yollarını çözümleme

Merhaba eklenti yüklediğinizde, tüm dış dosyası başvuruları hello Sahne dosya tarar. Bu başvuruları hello görüntülenen **varlıklar** sekmesi. Başvurulan bir yolu çözümlenemiyor hello eklenti toolocate hello dahil olmak üzere birkaç varsayılan konumları dosyasında çalışır:

- Merhaba Sahne dosyasının Hello konumu 
- Merhaba geçerli projenin _sourceimages_ dizini
- Merhaba geçerli çalışma dizini. 

Merhaba varlık yine bulunamazsa, bir uyarı simgesiyle listelenir:

![Eksik varlıklar bir uyarı simgesi ile gösterilir](./media/batch-rendering-service/missing_assets.png)

Çözümlenmemiş dosya başvurusu hello konumunu biliyorsanız, simge toobe tooadd bir arama yolu istenir uyarı hello tıklatabilirsiniz. ardından eklenti Hello bu arama yolu tooattempt tooresolve eksik tüm varlıkları kullanır. Dilediğiniz sayıda arama yolu ekleyebilirsiniz.

Bir başvuru çözümlendiğinde yeşil ışık simgesiyle listelenir:

![Çözümlenen varlıklar yeşil ışık simgesi gösterir](./media/batch-rendering-service/found_assets.png)

Sahne diğer dosyaları gerektiriyorsa, bu hello eklenti değil algıladı, ek dosya veya dizinlerin ekleyebilirsiniz. Kullanım hello **dosyaları Ekle** ve **Dizin Ekle** düğmeler. Yeni bir Sahne Hello eklenti açıkken yüklerseniz, emin tooclick olması **yenileme** tooupdate hello Sahne'nın başvuruları.

#### <a name="upload-assets-tooan-asset-project"></a>Varlıklar tooan varlık proje karşıya yükle

Ne zaman bir işleme iş hello gönderdiğiniz hello görüntülenen dosyalar başvurulan **varlıklar** sekmesinde otomatik olarak karşıya yüklenen tooAzure varlık proje olarak depolama şunlardır. Hello kullanarak hello varlık dosyaları işleme iş bağımsız olarak yükleyebilirsiniz **karşıya** hello düğmesinde **varlıklar** hello belirtilen sekmesini hello varlık proje adı **proje**alan ve hello geçerli Maya proje sonra varsayılan olarak adlandırılır. Varlık dosyaları karşıya, hello yerel dosya yapısı korunur. 

Karşıya yüklenen varlıklara herhangi bir sayıda işleme işi başvurabilir. Merhaba Sahne dahil edilen olup olmadığına bakılmaksızın tüm karşıya yüklenen varlıkları hello varlık projeye başvuruda bulunan kullanılabilir tooany iş içerir. sonraki işinizi hello hello adını değiştir başvurduğu toochange hello varlık proje **proje** hello alanındaki **varlıklar** sekmesi. Karşıya yükleme gelen tooexclude istediğiniz başvurulan dosyalar varsa bunların seçimini kaldırmak hello listeleme yanında yeşil hello düğmesini kullanarak.

#### <a name="submit-and-monitor-hello-render-job"></a>Gönderme ve İzleyicisi Merhaba işi oluşturma

Merhaba eklenti hello işleme iş yapılandırdıktan sonra hello tıklatın **işi Gönder** hello düğmesinde **gönderme** toosubmit hello iş tooBatch sekmesinde:

![Merhaba işleme işi gönderin](./media/batch-rendering-service/submit_job.png)

Merhaba gelen sürmekte olan bir iş izleyebilirsiniz **işleri** hello eklenti sekmesinde. Bir iş hello listesi toodisplay hello geçerli durumundan hello işin seçin. Ayrıca, bu sekme toocancel kullanın ve işleri, yanı sıra toodownload hello çıkış ve Günlükler işleme silin. 

toodownload çıkışları değiştirme hello **çıkarır** alan tooset hello istenen hedef dizini. Merhaba dişli simgesi toostart hello iş izleyen ve ilerledikçe çıkışları indirmeleri bir arka plan işlemi tıklatın: 

![İş durumunu görüntüleme ve çıktıları indirme](./media/batch-rendering-service/jobs.png)

Merhaba indirme işlemi kesintiye uğratmadan Maya kapatabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

Toplu işlem hakkında daha fazla toolearn bkz [toplu işlemle doğası gereği paralel iş yüklerini çalıştırmak](batch-technical-overview.md).
