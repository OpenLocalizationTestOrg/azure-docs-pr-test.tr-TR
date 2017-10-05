---
title: "Azure Batch Rendering hizmetini kullanarak bulutta işleme | Microsoft Docs"
description: "İşleri, doğrudan Maya üzerinden veya kullanım başına ödeme temelinde Azure sanal makinelerinde işleyin."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 4d22f92cafdbceee5213361d6d2b2f38904d12c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-the-batch-rendering-service"></a>Batch Rendering hizmetini kullanmaya başlama

Azure Batch Rendering hizmeti, kullanım başına ödeme temelinde bulut ölçekli işleme özellikleri sunar. Batch Rendering hizmeti, iş zamanlama ve kuyruğa alma işlerini gerçekleştirir, hata ve yeniden denemeleri yönetir ve işleme işiniz için otomatik ölçeklendirme yapar. Batch Rendering hizmeti, yakında eklenecek diğer uygulama desteklerinin yanı sıra Autodesk Maya, 3ds Max ve Arnold desteği sunar. Maya 2017 için Batch eklentisi, masaüstünüzden Azure’da bir işleme işi başlatmanızı kolaylaştırır. 

## <a name="supported-applications"></a>Desteklenen uygulamalar

Batch Rendering hizmeti şu anda aşağıdaki uygulamaları desteklemektedir:

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>Ön koşullar

Batch Rendering hizmetini kullanmak için şunlar gerekir:

- Bir [Azure hesabı](https://azure.microsoft.com/free/). 
- **Bir Azure Batch hesabı.** Azure portalında bir Batch hesabı oluşturmaya ilişkin yönergeler için bkz. [Azure portalıyla Batch hesabı oluşturma](batch-account-create-portal.md).
- **Bir Azure Depolama hesabı.** İşleme işiniz için kullanılan varlıklar Azure Depolama hizmetinde depolanır. Batch hesabınızı ayarlarken otomatik olarak bir depolama hesabı oluşturabilirsiniz. Ayrıca mevcut bir depolama hesabını kullanabilirsiniz. Depolama hesapları hakkında daha fazla bilgi almak için bkz. [Azure portalında depolama hesabı oluşturma, yönetme veya silme](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

Maya için Batch eklentisini kullanmak için şunlar gerekir:

- **Maya 2017**
- **Arnold for Maya**

Ayrıca [Azure portalını](https://portal.azure.com) kullanarak Maya, 3ds Max ve Arnold ile önceden yapılandırılmış bir sanal makine havuzu oluşturabilirsiniz. İşleri izlemek için portalı kullanabilir, uygulama günlüklerini indirerek ve RDP ya da SSH ile VM’lere uzaktan tek tek bağlanarak başarısız görevleri saptayabilirsiniz.

## <a name="basic-batch-concepts"></a>Temel Batch kavramları

Batch Rendering hizmetini kullanmaya başlamadan önce işlem düğümleri, havuzlar ve işler gibi birkaç Batch kavramının bilinmesi yararlıdır. Genel olarak Azure Batch hakkında daha fazla bilgi almak için bkz. [Batch ile doğası gereği paralel iş yüklerini çalıştırma](batch-technical-overview.md).

### <a name="pools"></a>Havuzlar

Batch, işleme gibi işlem yoğunluklu çalışmaları bir **işlem düğümü** **havuzu** üzerinde gerçekleştirmeye yönelik bir platform hizmetidir. Bir havuzdaki her işlem düğümü, Linux veya Windows çalıştıran bir Azure sanal makinesidir (VM). 

Batch havuzları ve işlem düğümleri hakkında daha fazla bilgi için, [Batch ile büyük ölçekli paralel işlem çözümleri geliştirme](batch-api-basics.md) makalesindeki [Havuz](batch-api-basics.md#pool) ve [İşlem düğümü](batch-api-basics.md#compute-node) bölümlerine bakın.

### <a name="jobs"></a>İşler

Batch **işi**, bir havuzdaki işlem düğümleri üzerinde çalışan görev koleksiyonudur. Bir işleme işi gönderdiğinizde, Batch bu işi görevlere böler ve görevleri çalışması için havuzdaki işlem düğümlerine dağıtır.

Batch işleri hakkında daha fazla bilgi için [Batch ile büyük ölçekli paralel işlem çözümleri geliştirme](batch-api-basics.md) makalesindeki [İş](batch-api-basics.md#job) bölümüne bakın.

## <a name="use-the-batch-plug-in-for-maya-to-submit-a-render-job"></a>Maya için Batch eklentisini kullanarak işleme işi gönderme

Maya için Batch eklentisi ile Maya’dan Batch Rendering hizmetine bir iş gönderebilirsiniz. Aşağıdaki bölümlerde, işi eklentiden yapılandırma ve sonra gönderme işlemi açıklanmaktadır. 

### <a name="load-the-batch-plug-in-in-maya"></a>Batch eklentisini Maya’ya yükleme

Batch eklentisi [GitHub](https://github.com/Azure/azure-batch-maya/releases) üzerinde kullanılabilir. Arşivi seçtiğiniz bir dizine çıkartın. Eklentiyi doğrudan *azure_batch_maya* dizininden yükleyebilirsiniz.

Eklentiyi Maya’ya yüklemek için:

1. Maya’yı çalıştırın.
2. **Pencere** > **Ayarlar/Tercihler** > **Eklenti Yöneticisi**’ni açın.
3. **Gözat**’a tıklayın.
4. *azure_batch_maya/plug-in/AzureBatch.py* dizinine gidip dosyayı seçin.

### <a name="authenticate-access-to-your-batch-and-storage-accounts"></a>Batch ve Depolama hesaplarınıza erişim için kimlik doğrulaması

Eklentiyi kullanmak için Azure Batch ve Azure Depolama hesap anahtarlarınızı kullanarak kimlik doğrulaması yapmanız gerekir. Hesap anahtarlarınızı almak için:

1. Eklentiyi Maya’da görüntüleyin ve **Yapılandır** sekmesini seçin.
2. [Azure portalına](https://portal.azure.com) gidin.
3. Soldaki menüden **Batch Hesapları**’nı seçin. Gerekirse, **Diğer Hizmetler**’e tıklayıp _Batch_ filtresi uygulayın.
4. İstediğiniz Batch hesabını listede bulun.
5. Hesap adı, hesap URL’si ve erişim anahtarlarını görüntülemek için **Anahtarlar** menü öğesini seçin:
    - Batch hesabı URL’sini Batch eklentisindeki **Hizmet** alanına yapıştırın.
    - Hesap adını **Batch hesabı** alanına yapıştırın.
    - Birincil hesap anahtarını **Batch anahtarı** alanına yapıştırın.
7. Soldaki menüden Depolama Hesapları’nı seçin. Gerekirse, **Diğer Hizmetler**’e tıklayıp _Depolama_ filtresi uygulayın.
8. İstediğiniz Depolama hesabını listede bulun.
9. Depolama hesabı adını ve anahtarlarını görüntülemek için **Erişim Anahtarları** menü öğesini seçin.
    - Depolama hesabı adını Batch eklentisindeki **Depolama Hesabı** alanına yapıştırın.
    - Birincil hesap anahtarını **Depolama Anahtarı** alanına yapıştırın.
10. Eklentinin her iki hesaba da erişebildiğinden emin olmak için **Kimliği Doğrula**’ya tıklayın.

Kimliği başarıyla doğruladıktan sonra eklenti, durum alanını **Kimliği Doğrulandı** olarak değiştirir: 

![Batch ve Depolama hesaplarınız için kimlik doğrulaması](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>İşleme işi için havuz yapılandırma

Batch ve Storage hesaplarınızın kimliğini doğruladıktan sonra, işleme işinize yönelik bir havuz oluşturun. Eklenti, seçimlerinizi oturumlar arasında kaydeder. Tercih ettiğiniz yapılandırmayı ayarladıktan sonra değişmediği sürece sizin değiştirmeniz gerekmez.

Aşağıdaki bölümlerde, **Gönder** sekmesinde bulunan seçeneklere ilişkin bilgi verilmektedir:

#### <a name="specify-a-new-or-existing-pool"></a>Yeni veya var olan bir havuzu belirtme

İşleme işinin çalıştırılacağı havuzu belirtmek için **Gönder** sekmesini seçin. Bu sekme bir havuz oluşturma veya var olan bir havuzu seçme seçeneklerini sunar:

- **Bu iş için bir havuzu otomatik sağlayabilirsiniz** (varsayılan seçenek). Bu seçeneği belirlediğinizde Batch, havuzu geçerli iş için özel olarak oluşturur ve işleme işi tamamlandığında havuzu otomatik olarak siler. Tamamlayacağınız tek bir işleme işi olduğunda bu en iyi seçenektir.
- **Var olan kalıcı havuzu yeniden kullanabilirsiniz**. Boşta olan bir havuzunuz varsa, açılır listeden seçerek işleme işini çalıştırmak için bu havuzu belirtebilirsiniz. Var olan bir kalıcı havuzun yeniden kullanılması, havuzu sağlamak için harcanan süreden tasarruf ettirir.  
- **Yeni bir kalıcı havuz oluşturabilirsiniz**. Bu seçeneğin belirlenmesi, işin çalıştırılması için yeni bir havuz oluşturur. İş tamamlandığında havuz silinmez, böylece gelecekteki işler için yeniden kullanabilirsiniz. İşleme işlerini çalıştırmaya yönelik sürekli bir gereksinimiz varsa bu seçeneği belirleyin. Sonraki işlerde **Var olan kalıcı havuzu yeniden kullan**’ı seçerek ilk iş için oluşturduğunuz kalıcı havuzu kullanabilirsiniz.

![Havuz, işletim sistemi görüntüsü, VM boyutu ve lisans belirtme](./media/batch-rendering-service/submit.png)

Azure VM'ler için ücretlerin nasıl tahakkuk ettiği hakkında daha fazla bilgi için bkz. [Linux Fiyatlandırma SSS](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) ve [Windows Fiyatlandırma SSS](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).

#### <a name="specify-the-os-image-to-provision"></a>Sağlanacak işletim sistemi görüntüsünü belirtme

Havuzda işlem düğümlerini sağlamak için kullanılacak işletim sistemi görüntüsünün türünü **Env** (Environment - Ortam) sekmesinde belirtebilirsiniz. Batch şu anda işleme işleri aşağıdaki görüntü seçeneklerini desteklemektedir:

|İşletim Sistemi  |Görüntü  |
|---------|---------|
|Linux     |Batch CentOS Önizlemesi |
|Windows     |Batch Windows Önizlemesi |

#### <a name="choose-a-vm-size"></a>VM boyutu seçme

VM boyutunu **Env** sekmesinden belirtebilirsiniz. Kullanılabilir VM boyutları hakkında daha fazla bilgi için bkz. [Azure’da Linux VM boyutları](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) ve [Azure’da Windows VM boyutları](https://docs.microsoft.com/azure/virtual-machines/windows/sizes). 

![Env sekmesinde VM işletim sistemi görüntüsünü ve boyutunu belirtme](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>Lisanslama seçeneklerini belirtme

Kullanmak istediğiniz lisansları **Env** sekmesinde belirtebilirsiniz. Seçeneklere şunlar dahildir:

- Varsayılan olarak etkin olan **Maya**.
- Maya’da etkin işleme altyapısı olarak Arnold algılanırsa etkinleştirilen **Arnold**.

 Kendi lisansınızı kullanarak işlemek istiyorsanız, tabloya uygun ortam değişkenlerini ekleyerek lisans uç noktanızı yapılandırabilirsiniz. Bunu yaparsanız varsayılan lisanslama seçeneklerini kaldırdığınızdan emin olun.

> [!IMPORTANT]
> VM’ler havuzda çalışırken, VM’ler o anda işleme için kullanılmıyor olsa bile, lisans kullanımı faturalandırılır. Ek ücretlerden kaçınmak için, başka bir işleme işi çalıştırmaya hazır olana kadar **Havuzlar** sekmesine gidip havuz boyutunu 0 düğüm olarak ayarlayabilirsiniz. 
>
>

#### <a name="manage-persistent-pools"></a>Kalıcı havuzları yönetme

Var olan bir kalıcı havuzu **Havuzlar** sekmesinden yönetebilirsiniz. Listeden bir havuz seçildiğinde, havuzun mevcut durumu gösterilir.

**Havuzlar** sekmesinden ayrıca havuzu silebilir ve havuzdaki VM sayısını yeniden boyutlandırabilirsiniz. İş yükleri arasında maliyetlerin oluşmasını önlemek için havuz boyutunu 0 düğüm olarak ayarlayabilirsiniz.

![Havuzları görüntüleme, yeniden boyutlandırma ve silme](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>İşleme işini göndermek üzere yapılandırma

İşleme işini çalıştıracak havuzun parametrelerini belirttikten sonra işin kendisini yapılandırın. 

#### <a name="specify-scene-parameters"></a>Sahne parametrelerini belirtme

Batch eklentisi Maya’da o anda hangi işleme altyapısını kullandığınızı algılar ve **Gönder** sekmesinde uygun işleme ayarlarını gösterir. Bu ayarlar başlangıç karesi, bitiş karesi, çıktı ön eki ve kare adımıdır. Eklentide farklı ayarlar belirterek sahne dosyası işleme ayarlarını geçersiz kılabilirsiniz. Eklenti ayarlarında yaptığınız değişiklikler sahne dosyası işleme ayarlarında kalıcı hale getirilmez; böylece, sahne dosyasını yeniden karşıya yüklemeye gerek olmadan iş bazında değişiklikler yapabilirsiniz.

Eklenti, Maya’da seçtiğiniz işleme altyapısının desteklenmemesi durumunda sizi uyarır.

Eklenti açıkken yeni bir sahne yüklerseniz **Yenile** düğmesine tıklayarak ayarların güncelleştirildiğinden emin olun.

#### <a name="resolve-asset-paths"></a>Varlık yollarını çözümleme

Eklentiyi yüklediğinizde, tüm dış dosya başvuruları için sahne dosyası taranır. Bu başvurular, **Varlıklar** sekmesinde gösterilir. Başvurulan bir yol çözümlenemiyorsa, eklenti aşağıdaki birkaç varsayılan konumda dosyayı bulmayı dener:

- Sahne dosyasının konumu 
- Geçerli projenin _sourceimages_ dizini
- Geçerli çalışma dizini. 

Varlık hala bulunamıyorsa bir uyarı simgesiyle listelenir:

![Eksik varlıklar bir uyarı simgesi ile gösterilir](./media/batch-rendering-service/missing_assets.png)

Çözümlenmemiş bir dosya başvurusunun konumunu biliyorsanız, bir arama yolu eklemek için sorulacak uyarı simgesine tıklayabilirsiniz. Bu durumda eklenti bu arama yolunu kullanarak eksik tüm varlıkları çözümlemeye çalışır. Dilediğiniz sayıda arama yolu ekleyebilirsiniz.

Bir başvuru çözümlendiğinde yeşil ışık simgesiyle listelenir:

![Çözümlenen varlıklar yeşil ışık simgesi gösterir](./media/batch-rendering-service/found_assets.png)

Sahneniz eklentinin algılamadığı başka dosyaları gerektiriyorsa, bu dosyaları veya dizinleri ekleyebilirsiniz. **Dosya Ekle** ve **Dizin Ekle** düğmelerini kullanın. Eklenti açıkken yeni bir sahne yüklerseniz, sahnenin başvurularını güncelleştirmek için **Yenile**’ye tıkladığınızdan emin olun.

#### <a name="upload-assets-to-an-asset-project"></a>Varlıkları bir varlık projesine yükleme

Bir işleme işi gönderdiğinizde, **Varlıklar** sekmesinde gösterilen başvurulmuş dosyalar bir varlık projesi olarak Azure Depolama'ya otomatik olarak yüklenir. **Varlıklar** sekmesindeki **Karşıya Yükle** düğmesini kullanarak, varlık dosyalarını bir işleme işinden bağımsız olarak da yükleyebilirsiniz. Varlık projesinin adı **Proje** alanında belirtilir ve varsayılan olarak geçerli Maya projesine göre adlandırılır. Varlık dosyaları karşıya yüklendiğinde yerel dosya yapısı korunur. 

Karşıya yüklenen varlıklara herhangi bir sayıda işleme işi başvurabilir. Karşıya yüklenen tüm varlıklar, sahneye dahil olup olmamasına bakılmaksızın varlık projesine başvuran tüm işler tarafından kullanılabilir. Sonraki işiniz tarafından başvurulan varlık projesini değiştirmek için, **Varlıklar** sekmesinin **Proje** alanındaki adı değiştirin. Karşıya yükleme işlemine dahil etmek istemediğiniz başvurulmuş dosyalar varsa, listenin yanındaki yeşil düğmeyi kullanarak bu dosyaların seçimini kaldırın.

#### <a name="submit-and-monitor-the-render-job"></a>İşleme işini gönderme ve izleme

İşleme işini eklentide yapılandırdıktan sonra, **Gönder** sekmesindeki **İşi Gönder** düğmesine tıklayarak işi Batch hesabına gönderin:

![İşleme işini gönderme](./media/batch-rendering-service/submit_job.png)

Devam etmekte olan bir işi, eklentinin **İşler** sekmesinden izleyebilirsiniz. Bir işin geçerli durumu görüntülemek için listeden işi seçin. Ayrıca bu sekmeyi kullanarak işleri iptal edip silebilir ve çıktılar ile işleme günlüklerini indirebilirsiniz. 

Çıktıları indirmek için **Çıktılar** alanını değiştirerek istediğiniz hedef dizine ayarlayın. İşi izleyen ve ilerledikçe çıktıları indiren bir arka plan işlemini başlatmak için dişli simgesine tıklayın: 

![İş durumunu görüntüleme ve çıktıları indirme](./media/batch-rendering-service/jobs.png)

İndirme işlemini kesintiye uğratmadan Maya’yı kapatabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

Batch hakkında daha fazla bilgi almak için bkz. [Batch ile doğası gereği paralel iş yüklerini çalıştırma](batch-technical-overview.md).