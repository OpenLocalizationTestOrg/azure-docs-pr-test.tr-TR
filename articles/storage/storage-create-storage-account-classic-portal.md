---
title: "aaaHow toocreate, yönetme veya hello Klasik Azure portalında bir depolama hesabını silme | Microsoft Docs"
description: "Yeni bir depolama hesabı oluşturun, hesap erişim tuşlarınızı yönetin veya hello Azure portalında bir depolama hesabını silin. Standart ve premium depolama hesapları hakkında bilgi edinin."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 5e4f4360-3f81-4d63-a0b1-e7771b67af11
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 6ee2359e02c7c9e9c111e1fc87a6160bb8b785b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Azure Storage hesapları hakkında
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-try-azure-tools](../../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Genel Bakış
Azure storage'da toohello Azure Blob, kuyruk, tablo ve dosya hizmetlere erişmek bir Azure depolama hesabı sağlar. Depolama hesabınız Azure Storage veri nesneleriniz için hello benzersiz ad alanı sağlar. Varsayılan olarak, hesabınızdaki hello veriler kullanılabilir yalnızca tooyou, hello hesap sahibi ' dir.

İki tür depolama hesabı vardır:

* Standart depolama hesabı Blob, Tablo, Kuyruk ve File Storage içerir.
* Bir premium depolama hesabı şu anda yalnızca Azure Virtual Machine disklerini destekler. Premium Storage için ayrıntılı genel bakış için bkz. [Premium Storage: Azure Virtual Machines İş Yükleri için Yüksek Performanslı Depolama](storage-premium-storage.md).

## <a name="storage-account-billing"></a>Depolama hesabı faturalama
Depolama hesabınıza bağlı olarak Azure Storage kullanımınıza göre faturalandırılırsınız. Depolama maliyetleri dört etkene bağlıdır: depolama kapasitesi, çoğaltma düzeni, depolama işlemleri ve veri çıkışı.

* Depolama kapasitesi toohow çok başvuruyor, depolama hesabı ayrılan toostore veri kullanıyor. yalnızca, veri depolama maliyetini hello verinizi, depoladığınız ve çoğaltılma belirlenir.
* Çoğaltma, verilerinizin aynı anda tutulan kopya sayısına ve tutulduğu konumu belirtir.
* İşlemler tooall okuma bakın ve işlemleri tooAzure depolama yazma.
* Veri çıkışı bir Azure bölgesinin dışına aktarılan toodata başvuruyor. Depolama hesabınızdaki Hello veri tarafından erişildiğinde içinde çalışmıyor uygulamanın hello aynı bölgede olup, uygulama bir bulut hizmeti veya diğer tür bir uygulama ve veri çıkışı için ücretlendirilirsiniz. (Azure Hizmetleri için adımları toogroup veri ve hizmetlerinizi sürebilir hello aynı veri merkezleri tooreduce veya veri çıkış ücretlerini ortadan kaldırmak.)  

Merhaba [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage) sayfası depolama kapasitesi, çoğaltma ve işlemler için ayrıntılı fiyatlandırma bilgileri sağlar. Merhaba [veri aktarımları fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/data-transfers/) sayfası veri çıkışı için ayrıntılı fiyatlandırma bilgileri sağlar.

Depolama hesabının kapasite ve performans hedefleri hakkında ayrıntılar için bkz. [Azure Storage Ölçeklenebilirlik ve Performans Hedefleri](storage-scalability-targets.md).

> [!NOTE]
> Bir Azure sanal makine oluşturduğunuzda, bir depolama hesabı söz konusu konumda zaten yoksa bir depolama hesabı sizin için otomatik olarak hello dağıtım konumda oluşturulur. Bu nedenle gerekli toofollow hello adımları toocreate, sanal makine diskleriniz için depolama hesabı şu değil. Merhaba depolama hesabı adı hello sanal makine adına dayalı olarak belirlenir. Merhaba bkz [Azure Virtual Machines belgeleri](https://azure.microsoft.com/documentation/services/virtual-machines/) daha fazla ayrıntı için.
> 
> 

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Tıklatın **yeni** hello sayfanın hello sonundaki hello çubuğunda. **Veri Hizmetleri** | **Depolama**, ve ardından **Hızlı Oluştur**’u seçin.
   
    ![NewStorageAccount](./media/storage-create-storage-account-classic-portal/storage_NewStorageAccount.png)
3. **URL**’ye depolama hesabınız için bir ad girin.
   
   > [!NOTE]
   > Depolama hesabı adları 3 ile 24 karakter arasında olmalı ve yalnızca sayıyla küçük harf içermelidir.
   > 
   > Depolama hesabınızın adının Azure içinde benzersiz olması gerekir. Seçtiğiniz hello depolama hesabı adı alınmışsa Hello Klasik Azure portalı bildirecektir.
   > 
   > 
   
    Bkz: [depolama hesabı uç noktaları](#storage-account-endpoints) aşağıda ayrıntıları hello depolama hesabı adı kullanılan tooaddress nasıl olacaktır hakkında Azure storage'da nesnelerinizin.
4. İçinde **konum/benzeşim grubu**, Kapat tooyou veya tooyour müşterileri içindir depolama hesabınız için bir konum seçin. Depolama hesabınızdaki verilere Azure sanal makine veya Bulut hizmeti gibi başka bir Azure hizmeti erişecek olursa tooselect hello listesi toogroup bir benzeşim grubu depolama hesabınızdaki hello isteyebilirsiniz diğer Azure hizmetleriyle aynı veri merkezinde tooimprove performans ve maliyetleri kullandığınız.
   
    Depolama hesabınız oluşturulduğunda bir benzeşim grubu seçmeniz gerektiğini unutmayın. Var olan bir hesap tooan benzeşim grubunu taşınamıyor. Benzeşim grupları hakkında daha fazla bilgi için bkz. [Benzeşim grubu ile hizmeti aynı konuma yerleştirme](#service-co-location-with-an-affinity-group).
   
   > [!IMPORTANT]
   > aboneliğiniz için hangi konumların kullanılabilir toodetermine hello çağırabilir [tüm kaynak sağlayıcıları Listele](https://msdn.microsoft.com/library/azure/dn790524.aspx) işlemi. toolist sağlayıcıları PowerShell üzerinden çağrısı [Get-AzureLocation](https://msdn.microsoft.com/library/azure/dn757693.aspx). .NET üzerinden hello kullan [listesi](https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.provideroperationsextensions.list.aspx) hello ProviderOperationsExtensions sınıfının yöntemi.
   > 
   > Ayrıca hangi bölgede hangi hizmetin sağlandığına dair daha fazla bilgi için bkz.[Azure Bölgeleri](https://azure.microsoft.com/regions/#services).
   > 
   > 
5. Birden fazla Azure aboneliğiniz varsa, ardından hello **abonelik** alanı görüntülenir. İçinde **abonelik**, hello toouse hello depolama hesabıyla istediğiniz Azure aboneliğini girin.
6. İçinde **çoğaltma**, hello çoğaltma depolama hesabınız için istenen düzeyini seçin. Merhaba çoğaltma seçeneği, verileriniz için en üst düzeyde dayanıklılık sağlayan coğrafi olarak yedekli çoğaltma önerilir. Azure Storage çoğaltma seçenekleri ile ilgili ayrıntılar için bkz. [Azure Storage çoğaltma](storage-redundancy.md).
7. **Depolama Hesabı Oluştur**’a tıklayın.
   
    Bu işlem birkaç dakika toocreate depolama hesabınız sürebilir. toocheck hello durumunu hello Klasik Azure portalı hello sonundaki hello bildirimleri izleyebilirsiniz. Merhaba depolama hesabı oluşturulduktan sonra yeni depolama hesabınızın sahip **çevrimiçi** durumu ve kullanıma hazırdır.

![StoragePage](./media/storage-create-storage-account-classic-portal/Storage_StoragePage.png)

### <a name="storage-account-endpoints"></a>Depolama hesabı uç noktaları
Azure Storage’da depoladığınız her nesnenin benzersiz bir URL adresi vardır. Merhaba depolama hesabı adı forms o adresin alt etki alanı hello. Merhaba belirli tooeach hizmeti olan alt etki alanı ve etki alanı adı birleşimi forms bir *endpoint* depolama hesabınız için.

Örneğin, depolama hesabınızın adı *mystorageaccount*, depolama hesabınız için hello varsayılan uç nokta sonra:

* Blob hizmeti: http://*mystorageaccount*.blob.core.windows.net
* Tablo hizmeti: http://*mystorageaccount*.table.core.windows.net
* Kuyruk hizmeti: http://*mystorageaccount*.queue.core.windows.net
* Dosya hizmeti: http://*mystorageaccount*.file.core.windows.net

Merhaba hello depolama panosunda depolama hesabınıza hello uç noktalarını görebilirsiniz [Klasik Azure portalı](https://manage.windowsazure.com) hello hesabı oluşturulduktan sonra.

Depolama hesabındaki bir nesneye erişilirken URL'si hello hello depolama hesabınızın toohello uç hello nesnenin konumda eklenerek oluşturulur. Örneğin bir blob adresi şu biçimde olabilir: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

Bu gibi durumlarda, özel etki alanı adı toouse ayrıca depolama hesabınız ile yapılandırabilirsiniz. Ayrıntılar için bkz. [Blob Storage uç noktanız için özel bir etki alanı adı yapılandırma](storage-custom-domain-name.md).

### <a name="service-co-location-with-an-affinity-group"></a>Hizmeti benzeşim grubu ile birlikte bulundurma
*Benzeşim grubu*, Azure hizmetlerinizi ve VM’lerinizi Azure Storage hesabınızla coğrafi olarak gruplamaktır. Bir benzeşim grubu bilgisayar iş yüklerini aynı veri merkezi veya hello hedef kullanıcının hedef kitle yakınında hello yerleştirerek hizmet performansını iyileştirebilir. Veri depolama hesabındaki hello parçası olan başka bir hizmet eriştiğinde Ayrıca, fatura harcamanız çıkışı için alınan aynı benzeşim grubu.

> [!NOTE]
> toocreate bir benzeşim grubu açık hello <b>ayarları</b> hello alanı [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın <b>benzeşim grupları</b>ve ardından ya da <b>Ekle bir benzeşim grubu</b> veya hello <b>Ekle</b> düğmesi. Ayrıca, oluşturabilir ve hello Azure Hizmet Yönetimi API'sini kullanarak benzeşim gruplarını yönetin. Daha fazla bilgi için bkz. <a href="http://msdn.microsoft.com/library/azure/ee460798.aspx">Benzeşim gruplarında işlemler</a>.
> 
> 

## <a name="view-copy-and-regenerate-storage-access-keys"></a>Depolama erişim tuşlarını görüntüleme, kopyalama ve yeniden oluşturma
Bir depolama hesabı oluşturduğunuzda Azure hello depolama hesabına erişim sağlandığında kimlik doğrulaması için kullanılan iki 512 bit depolama erişim tuşu oluşturur. İki depolama erişim tuşu sağlayarak Azure tooregenerate hello anahtarlarla herhangi kesinti tooyour depolama hizmeti veya erişim toothat hizmeti sağlar.

> [!NOTE]
> Depolama erişim tuşlarınızı başkalarıyla paylaşmaktan kaçınmanızı öneririz. erişim tuşlarınızı vermeden olmadan toopermit toostorage erişimine, kullanabileceğiniz bir *paylaşılan erişim imzası*. Paylaşılan erişim imzası erişim tooa kaynak hesabınızda tanımladığınız bir zaman aralığı için ve belirttiğiniz hello izinleri sağlar. Daha fazla bilgi edinmek için bkz. [Paylaşılan Erişim İmzaları (SAS) kullanma](storage-dotnet-shared-access-signature-part-1.md).
> 
> 

Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), kullanın **anahtarları Yönet** hello Pano veya hello **depolama** sayfa tooview, kopyalama ve kullanılan depolama erişim tuşlarını yeniden oluşturma hello tooaccess hello Blob, tablo ve kuyruk Hizmetleri.

### <a name="copy-a-storage-access-key"></a>Depolama erişim tuşu kopyalama
Kullanabileceğiniz **anahtarları Yönet** toocopy depolama erişim anahtarı toouse bir bağlantı dizesi içinde. Merhaba depolama hesabı adı ve kimlik doğrulaması'ndaki anahtar toouse Hello bağlantı dizesi gerektirir. Bağlantı yapılandırma hakkında bilgi tooaccess Azure storage Hizmetleri dizeleri için bkz: [Azure Storage bağlantı dizelerini yapılandırma](storage-configure-connection-string.md).

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **depolama**ve ardından hello depolama hesabı tooopen hello Panosu hello adına tıklayın.
2. **Anahtarları Yönet**’i tıklayın.
   
     **Erişim Tuşlarını Yönet** açılır.
   
    ![Managekeys](./media/storage-create-storage-account-classic-portal/Storage_ManageKeys.png)
3. toocopy bir depolama erişim tuşu select hello anahtar metin. Ardından sağ tıklayarak **Kopyala**’ya tıklayın.

### <a name="regenerate-storage-access-keys"></a>Depolama erişim tuşlarını yeniden oluşturma
Merhaba erişim tuşları tooyour depolama hesabı düzenli aralıklarla depolama bağlantılarınızı güvenli toohelp Koru değiştirmenizi öneririz. Böylece bağlantıları toohello depolama hesabı hello yeniden oluşturmak, bir erişim tuşunu kullanarak diğer erişim tuşu bulundurabilirsiniz iki erişim tuşu atanır.

> [!WARNING]
> Erişim anahtarlarını yeniden Hizmetleri Azure yanı sıra hello depolama hesabına bağlı kendi uygulamalarınızı etkileyebilir. Hello erişim anahtar tooaccess hello depolama hesabını kullanan tüm istemciler güncelleştirilmiş toouse hello yeni anahtarı olması gerekir.
> 
> 

**Medya Hizmetleri** -depolama hesabınıza bağlı medya Hizmetleri varsa hello anahtarları yeniden oluşturduktan sonra hello erişim tuşlarını medya hizmetlerinizle yeniden eşitlemeniz gerekir.

**Uygulamaları** - web uygulamanız veya Bulut Hizmetleri, kullanım hello depolama hesabı, anahtarları, yeniden yüklerseniz, anahtarları toplamazsanız hello bağlantıları kaybedeceksiniz. 

**Depolama gezginleri** - herhangi bir kullanıyorsanız [depolama Gezgin uygulaması](storage-explorers.md), büyük olasılıkla bu uygulamaları tarafından kullanılan tooupdate hello depolama anahtarı gerekir.

Depolama erişim tuşlarınızı döndürme hello işlemi şöyledir:

1. Uygulama kodu tooreference hello ikincil erişim anahtarınızı hello depolama hesabının Hello bağlantı dizelerini güncelleştirin.
2. Merhaba depolama hesabınız için birincil erişim tuşunu yeniden oluşturun. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), hello Pano veya hello **yapılandırma** sayfasında, **anahtarları Yönet**. Tıklatın **yeniden** altında hello birincil erişim anahtarını ve ardından **Evet** tooconfirm toogenerate yeni bir anahtar istiyor.
3. Kod tooreference hello yeni birincil erişim anahtarınızı Hello bağlantı dizelerini güncelleştirin.
4. Merhaba ikincil erişim tuşunu yeniden oluşturun.

## <a name="delete-a-storage-account"></a>Bir depolama hesabını silme
tooremove artık kullanıyorsanız, bir depolama hesabı kullan **silmek** hello Pano veya hello **yapılandırma** sayfası. **Silme** hello tüm hello BLOB'lar, tablolar ve Kuyruklar hello hesaptaki dahil olmak üzere tüm depolama hesabının tamamını siler.

> [!WARNING]
> Olası toorestore silinen depolama hesabıdır veya herhangi bir silme işleminden önce yer alan hello içeriği almak. Merhaba hesabı silmeden önce emin tooback herhangi bir şey olması toosave istiyor. Bu ayrıca hello hesaptaki tüm kaynaklar için geçerlidir; blob, tablo, kuyruk veya dosya sildiğinizde, kalıcı olarak silinir.
> 
> Ardından, depolama hesabınız VHD dosyaları veya bir Azure virtual machine içeriyorsa, tüm görüntü ve hello depolama hesabını silmeden önce bu VHD dosyalarını kullanan diskler silmeniz gerekir. İlk olarak, çalıştırıyorsa ve silin hello sanal makineyi durdurun. toodelete diskleri gidin toohello **diskleri** sekmesinde ve var. tüm diskleri silin. toodelete görüntülerinde gezinebilir toohello **görüntüleri** sekmesinde ve hello hesapta yer alan tüm görüntüleri silin.
> 
> 

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **depolama**.
2. Merhaba depolama hesabı girişinde hello adı dışında herhangi bir yere tıklayın ve ardından **silmek**.
   
     -Veya-
   
    Merhaba depolama hesabı tooopen hello Panosu Hello adına tıklayın ve ardından **silmek**.
3. Tıklatın **Evet** tooconfirm toodelete hello depolama hesabı istiyor.

## <a name="next-steps"></a>Sonraki adımlar
* Azure Storage hakkında daha fazla toolearn bkz hello [Azure Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/).
* Merhaba ziyaret [Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/).
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](storage-use-azcopy.md)

