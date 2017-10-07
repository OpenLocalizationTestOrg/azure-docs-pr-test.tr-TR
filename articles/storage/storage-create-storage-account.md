---
title: "aaaHow toocreate, yönetme veya hello Azure portalında bir depolama hesabını silme | Microsoft Docs"
description: "Yeni bir depolama hesabı oluşturun, hesap erişim tuşlarınızı yönetin veya hello Azure portalında bir depolama hesabını silin. Standart ve premium depolama hesapları hakkında bilgi edinin."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: c11c6509e192170db4812f47c389fc1009b94daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Azure Storage hesapları hakkında
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>Genel Bakış
Bir Azure depolama hesabı bir benzersiz ad alanı toostore sağlar ve Azure Storage veri nesnelerinizi erişebilirsiniz. Depolama hesabındaki tüm nesneler bir grup halinde faturalandırılır. Varsayılan olarak, hesabınızdaki hello veriler kullanılabilir yalnızca tooyou, hello hesap sahibi ' dir.

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>Depolama hesabı faturalama
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

> [!NOTE]
> Bir Azure sanal makine oluşturduğunuzda, bir depolama hesabı söz konusu konumda zaten yoksa bir depolama hesabı sizin için otomatik olarak hello dağıtım konumda oluşturulur. Bu nedenle gerekli toofollow hello adımları toocreate, sanal makine diskleriniz için depolama hesabı şu değil. Merhaba depolama hesabı adı hello sanal makine adına dayalı olarak belirlenir. Merhaba bkz [Azure Virtual Machines belgeleri](https://azure.microsoft.com/documentation/services/virtual-machines/) daha fazla ayrıntı için.
> 
> 

## <a name="storage-account-endpoints"></a>Depolama hesabı uç noktaları
Azure Storage’da depoladığınız her nesnenin benzersiz bir URL adresi vardır. Merhaba depolama hesabı adı forms o adresin alt etki alanı hello. Merhaba belirli tooeach hizmeti olan alt etki alanı ve etki alanı adı birleşimi forms bir *endpoint* depolama hesabınız için.

Örneğin, depolama hesabınızın adı *mystorageaccount*, depolama hesabınız için hello varsayılan uç nokta sonra:

* Blob hizmeti: http://*mystorageaccount*.blob.core.windows.net
* Tablo hizmeti: http://*mystorageaccount*.table.core.windows.net
* Kuyruk hizmeti: http://*mystorageaccount*.queue.core.windows.net
* Dosya hizmeti: http://*mystorageaccount*.file.core.windows.net

> [!NOTE]
> Blob storage hesabı yalnızca hello Blob Hizmeti uç noktası kullanıma sunar.
> 
> 

Depolama hesabındaki bir nesneye erişilirken URL'si hello hello depolama hesabınızın toohello uç hello nesnenin konumda eklenerek oluşturulur. Örneğin bir blob adresi şu biçimde olabilir: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

Bu gibi durumlarda, özel etki alanı adı toouse ayrıca depolama hesabınız ile yapılandırabilirsiniz. Klasik depolama hesapları için ayrıntıları öğrenmek üzere [Blob Depolama Uç Noktanız için özel bir etki alanı Adı yapılandırma](storage-custom-domain-name.md) sayfasına bakın. Resource Manager depolama hesapları için bu özelliği toohello eklenmemiş [Azure portal](https://portal.azure.com) henüz, ancak PowerShell ile yapılandırabilirsiniz. Daha fazla bilgi için bkz: Merhaba [Set-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607146.aspx) cmdlet'i.  

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde seçin **yeni** -> **depolama** -> **depolama hesabı**.
3. Depolama hesabınız için bir ad girin. Bkz: [depolama hesabı uç noktaları](#storage-account-endpoints) ayrıntıları hello depolama hesabı adı kullanılan tooaddress nasıl olacaktır hakkında Azure storage'da nesnelerinizin.
   
   > [!NOTE]
   > Depolama hesabı adları 3 ile 24 karakter arasında olmalı ve yalnızca sayıyla küçük harf içermelidir.
   > 
   > Depolama hesabınızın adının Azure içinde benzersiz olması gerekir. Hello Azure portal seçtiğiniz hello depolama hesabı adı zaten kullanımda olup olmadığını belirtir.
   > 
   > 
4. Kullanılan hello dağıtım modeli toobe belirtin: **Resource Manager** veya **Klasik**. **Resource Manager** hello dağıtım modeli önerilir. Daha fazla bilgi için bkz. [Resource Manager dağıtımını ve klasik dağıtımı anlama](../azure-resource-manager/resource-manager-deployment-model.md).
   
   > [!NOTE]
   > BLOB storage hesapları yalnızca hello Resource Manager dağıtım modeli kullanılarak oluşturulabilir.
   > 
   > 
5. Merhaba depolama hesabı türünü seçin: **genel amaçlı** veya **Blob storage**. **Genel amaçlı** hello varsayılandır.
   
    Varsa **genel amaçlı** seçilmedi sonra hello performans katmanını belirtin: **standart** veya **Premium**. Merhaba varsayılandır **standart**. Standart ve premium depolama hesapları hakkında daha fazla bilgi için bkz: [giriş tooMicrosoft Azure Storage](storage-introduction.md) ve [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](storage-premium-storage.md).
   
    Varsa **Blob Storage** seçilmedi sonra hello erişim katmanını belirtin: **etkin** veya **Cool**. Merhaba varsayılandır **etkin**. Daha fazla ayrıntı için bkz. [Azure Blob Storage: Seyrek erişimli ve Sık erişimli katmanlar](storage-blob-storage-tiers.md).
6. Merhaba hello depolama hesabı için çoğaltma seçeneğini seçin: **LRS**, **GRS**, **RA-GRS**, veya **ZRS**. Merhaba varsayılandır **RA-GRS**. Azure Storage çoğaltma seçenekleri ile ilgili ayrıntılar için bkz. [Azure Storage çoğaltma](storage-redundancy.md).
7. Toocreate hello yeni depolama hesabı istediğiniz hello aboneliği seçin.
8. Yeni bir kaynak grubu belirtin veya varolan bir kaynak grubunu seçin. Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md).
9. Depolama hesabınız için Hello coğrafi konumu seçin. Hangi bölgede hangi hizmetin sağlandığına dair daha fazla bilgi için bkz.[Azure Bölgeleri](https://azure.microsoft.com/regions/#services).
10. Tıklatın **oluşturma** toocreate hello depolama hesabı.

## <a name="manage-your-storage-account"></a>Depolama hesabınızı yönetme
### <a name="change-your-account-configuration"></a>Hesap yapılandırmanızı değiştirme
Depolama hesabınızı oluşturduktan sonra hello hesabı veya bir Blob Depolama hesabı için değişen hello erişim katmanı için kullanılan hello çoğaltma seçeneğinin değiştirilmesi gibi kendi yapılandırmasını değiştirebilirsiniz. Merhaba, [Azure portal](https://portal.azure.com), tooyour depolama hesabını bulun ve tıklatın gidin **yapılandırma** altında **ayarları** tooview ve/veya değişiklik hello hesabı yapılandırması.

> [!NOTE]
> Merhaba depolama hesabı oluştururken seçtiğiniz hello performans katmanına bağlı olarak bazı çoğaltma seçenekleri kullanılamayabilir.
> 
> 

Merhaba çoğaltma seçeneğinin değiştirilmesi, fiyatlandırmanızı da değiştirir. Daha fazla ayrıntı için [Azure Storage Fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/) sayfasına bakın.

İçin Blob Depolama hesapları, Hello erişim katmanını değiştirme maruz kalabilirsiniz ücretleri hello için ayrıca toochanging fiyatlandırma değiştirin. Lütfen hello bakın [Blob storage hesapları - fiyatlandırma ve faturalama](storage-blob-storage-tiers.md#pricing-and-billing) daha fazla ayrıntı için.

### <a name="manage-your-storage-access-keys"></a>Depolama erişim tuşlarınızı yönetme
Bir depolama hesabı oluşturduğunuzda Azure hello depolama hesabına erişim sağlandığında kimlik doğrulaması için kullanılan iki 512 bit depolama erişim tuşu oluşturur. İki depolama erişim tuşu sağlayarak Azure tooregenerate hello anahtarlarla herhangi kesinti tooyour depolama hizmeti veya erişim toothat hizmeti sağlar.

> [!NOTE]
> Depolama erişim tuşlarınızı başkalarıyla paylaşmaktan kaçınmanızı öneririz. erişim tuşlarınızı vermeden olmadan toopermit toostorage erişimine, kullanabileceğiniz bir *paylaşılan erişim imzası*. Paylaşılan erişim imzası erişim tooa kaynak hesabınızda tanımladığınız bir zaman aralığı için ve belirttiğiniz hello izinleri sağlar. Daha fazla bilgi edinmek için bkz. [Paylaşılan Erişim İmzaları (SAS) kullanma](storage-dotnet-shared-access-signature-part-1.md).
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>Depolama erişim tuşlarını görüntüleme ve kopyalama
Merhaba, [Azure portal](https://portal.azure.com), tooyour depolama hesabına gidin,'ı tıklatın **tüm ayarları** ve ardından **erişim anahtarları** tooview, kopyalamak ve hesap erişim tuşlarınızı yeniden. Merhaba **erişim tuşları** dikey penceresinde de uygulamalarınızda toouse kopyalayabilirsiniz, birincil ve ikincil anahtarları kullanan önceden yapılandırılmış bağlantı dizeleri içerir.

#### <a name="regenerate-storage-access-keys"></a>Depolama erişim tuşlarını yeniden oluşturma
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
2. Merhaba depolama hesabınız için birincil erişim tuşunu yeniden oluşturun. Hello üzerinde **erişim tuşları** dikey penceresinde tıklatın **anahtarı yeniden oluştur1**ve ardından **Evet** tooconfirm toogenerate yeni bir anahtar istiyor.
3. Kod tooreference hello yeni birincil erişim anahtarınızı Hello bağlantı dizelerini güncelleştirin.
4. Regenerate hello ikincil erişim anahtarını hello aynı şekilde.

## <a name="delete-a-storage-account"></a>Bir depolama hesabını silme
tooremove artık kullanıyorsanız, bir depolama hesabı gidin hello toohello depolama hesabında [Azure portal](https://portal.azure.com), tıklatıp **silmek**. Bir depolama hesabını silme hello hesaptaki tüm veriler dahil olmak üzere hello tüm hesap silinir.

> [!WARNING]
> Olası toorestore silinen depolama hesabıdır veya herhangi bir silme işleminden önce yer alan hello içeriği almak. Merhaba hesabı silmeden önce emin tooback herhangi bir şey olması toosave istiyor. Bu ayrıca hello hesaptaki tüm kaynaklar için geçerlidir; blob, tablo, kuyruk veya dosya sildiğinizde, kalıcı olarak silinir.
> 
> 

toodelete bir Azure sanal makineyle ilişkili bir depolama hesabı, önce tüm sanal makine disklerinin silindiğinden emin olmalısınız. İlk sanal makine disklerini silmezseniz, depolama hesabınız toodelete çalıştığınızda benzer bir hata iletisi görürsünüz:

    Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.

Merhaba depolama hesabı hello Klasik dağıtım modeli kullanıyorsa, hello'nda aşağıdaki adımları izleyerek hello sanal makine diski kaldırabilirsiniz [Azure portal](https://manage.windowsazure.com):

1. Toohello gidin [Klasik Azure portalı](https://manage.windowsazure.com).
2. Toohello Virtual Machines sekmesine gidin.
3. Merhaba diskler sekmesine tıklayın.
4. Veri diskinizi seçin ve Diski Sil’e tıklayın.
5. toodelete disk görüntülerini toohello görüntüler sekmesine gidin ve hello hesapta yer alan tüm görüntüleri silin.

Daha fazla bilgi için bkz: Merhaba [Azure Virtual Machines belgeleri](http://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="next-steps"></a>Sonraki adımlar
* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.
* [Azure Blob Depolama: Seyrek Erişimli ve Sık Erişimli katmanlar](storage-blob-storage-tiers.md)
* [Azure Depolama çoğaltması](storage-redundancy.md)
* [Azure Depolama Bağlantı Dizelerini yapılandırma](storage-configure-connection-string.md)
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](storage-use-azcopy.md)
* Merhaba ziyaret [Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/).

