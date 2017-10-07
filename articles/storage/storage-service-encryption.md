---
title: "Rest verileri için depolama hizmeti şifrelemesi aaaAzure | Microsoft Docs"
description: "Merhaba veri alınırken şifresini çözmek ve Azure Blob Depolama alanınızın hello hizmet tarafında hello veri depolarken Hello Azure depolama hizmeti şifrelemesi özelliği tooencrypt kullanın."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 304f1c21200f86f2084ce98788b2fc7ca893d1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a>Bekleyen Veri için Azure Storage Hizmeti Şifreleme
Azure Storage hizmeti şifreleme (SSE) bekleyen veri için korumak ve Kuruluş güvenliği ve uyumluluk taahhüt veri toomeet korumaya yardımcı olur. Bu özellik ile Azure depolama otomatik olarak veri önceki toopersisting toostorage şifreler ve önceki tooretrieval şifresini çözer. Merhaba şifreleme, şifre çözme ve anahtar yönetimi tamamen saydam toousers verilebilir.

Merhaba aşağıdaki bölümlerde ayrıntılı kılavuz nasıl hello yanı sıra toouse hello depolama hizmeti şifrelemesi özellikleri senaryoları ve kullanıcı deneyimleri desteklenmiyor sağlar.

## <a name="overview"></a>Genel Bakış
Azure depolama toobuild güvenli uygulamalar birlikte, geliştiricilerin güvenlik özellikleri kapsamlı bir kümesini sağlar. Veri güvenli bir uygulama ile Azure arasında aktarımda kullanarak [istemci tarafı şifreleme](storage-client-side-encryption.md), HTTPs veya SMB 3.0. Depolama hizmeti şifrelemesi, bekleyen şifreleme, işleme şifreleme, şifre çözme ve tamamen saydam bir şekilde anahtar yönetimi sağlar. Tüm veriler, 256 bit kullanılarak şifrelenir [AES şifreleme](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), hello güçlü blok birini şifrelemeleri kullanılabilir.

SSE tooAzure depolama yazılır ve Azure Blob Depolama ve File Storage için kullanılabilir olduğunda hello verileri şifreleyerek çalışır. Merhaba şunlar için geçerlidir:

* Standart Depolama: Genel amaçlı depolama hesapları BLOB ve dosya depolama ve Blob storage hesapları
* Premium depolama 
* Tüm artıklık düzeyleri (LRS, ZRS, GRS, RA-GRS)
* Azure Resource Manager depolama hesapları (ancak klasik değil) 
* Tüm bölgeler.

toolearn daha, lütfen bakın toohello SSS.

bir depolama hesabı için depolama hizmeti şifrelemesi tooenable veya devre dışı bırakma hello oturum [Azure portal](https://portal.azure.com) ve bir depolama hesabı seçin. Hello ayarları dikey penceresinde, bu ekran görüntüsünde gösterildiği gibi hello Blob hizmeti bölümüne bakın ve şifreleme'yi tıklatın.

![Portal gösteren ekran görüntüsü şifreleme seçeneği](./media/storage-service-encryption/image1.png)
<br/>*Şekil 1: (1. adım) Blob hizmeti için SSE etkinleştir*

![Portal gösteren ekran görüntüsü şifreleme seçeneği](./media/storage-service-encryption/image3.png)
<br/>*Şekil 2: Dosya hizmeti (1. adım) SSE etkinleştir*

Hello şifreleme ayarı tıkladıktan sonra etkinleştirme veya depolama hizmeti şifrelemesi devre dışı bırakabilirsiniz.

![Portal gösteren ekran görüntüsü şifreleme özellikleri](./media/storage-service-encryption/image2.png)
<br/>*Şekil 3: SSE için Blob etkinleştirin ve dosya hizmeti (Adım2)*

## <a name="encryption-scenarios"></a>Şifreleme senaryosu
Depolama hizmeti şifrelemesi, bir depolama hesabı düzeyde etkinleştirilebilir. Etkinleştirildikten sonra müşterilerin hangi Hizmetleri tooencrypt seçin. Müşteri senaryoları aşağıdaki hello destekler:

* Resource Manager hesaplarındaki şifreleme Blob Depolama ve dosya depolama.
* Şifreleme Blob ve dosya hizmeti klasik depolama hesaplarındaki kez tooResource Manager depolama hesaplarıyla geçirildi.

SSE hello aşağıdaki sınırlamalar vardır:

* Klasik depolama hesaplarını şifrelenmesi desteklenmiyor.
* Merhaba şifreleme etkinleştirildikten sonra varolan verilerin - SSE yalnızca yeni oluşturulan verileri şifreler. Örneğin yeni bir Resource Manager depolama hesabı oluşturun ancak şifreleme kapatmayın ve ardından BLOB veya arşivlenmiş VHD'ler toothat depolama hesabı karşıya yükleyin ve sonra SSE açın, yeniden yazılmıştır veya kopyaladığınız sürece bu BLOB'lar şifrelenmez.
* Market desteği - VMs şifrelenmesi oluşturulan etkinleştir hello hello kullanarak Market [Azure portal](https://portal.azure.com), PowerShell ve Azure CLI. Merhaba VHD temel görüntü şifrelenmemiş kalacak; Ancak, hello VM çalışmaya başlar sonra yapılan tüm yazma şifrelenir.
* Tablo ve kuyruklarını veriler şifrelenmez.

## <a name="getting-started"></a>Başlarken
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>1. adım: [yeni depolama hesabı oluşturma](storage-create-storage-account.md).
### <a name="step-2-enable-encryption"></a>2. adım: şifrelemeyi etkinleştirin.
Hello kullanarak şifrelemeyi etkinleştirebilirsiniz [Azure portal](https://portal.azure.com).

> [!NOTE]
> Tooprogrammatically etkinleştirmek istediğiniz veya bir depolama hesabında depolama hizmeti şifrelemesi hello devre dışı bırakırsanız hello kullanabilirsiniz [Azure depolama kaynak sağlayıcısı REST API](https://msdn.microsoft.com/library/azure/mt163683.aspx), hello [depolama kaynak sağlayıcısı istemci kitaplığı .NET için](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), veya hello [Azure CLI](storage-azure-cli.md).
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a>3. adım: veri toostorage hesabı kopyalama
Merhaba Blob hizmeti SSE etkinleştirirseniz, toothat depolama hesabına yazılan BLOB şifrelenir. Bunlar yazılır kadar bu depolama hesabında zaten bulunan tüm BLOB'ları şifrelenmez. Hello veri şifrelenmiş SSE ile bir depolama hesabı tooone kopyalayın veya bile SSE etkinleştirmek ve bir kapsayıcı tooanother toosure önceki veri şifrelenir hello BLOB'lar kopyalayın. Araçlar tooaccomplish aşağıdaki hello hiçbirini bunu kullanabilirsiniz. Bu olduğu hello aynı davranışı dosya depolama için de.

#### <a name="using-azcopy"></a>AzCopy kullanma
AzCopy en uygun performans ile basit komutları kullanarak Microsoft Azure Blob, dosya ve tablo depolama biriminden veri tooand kopyalanması için tasarlanmış bir Windows komut satırı yardımcı programıdır. Bu toocopy BLOB veya bir depolama hesabı tooanother etkin SSE içeren dosyaları kullanabilirsiniz. 

toolearn daha, lütfen şu adresi ziyaret [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).

#### <a name="using-smb"></a>SMB kullanma
Azure File storage hello bulutta hello standart SMB protokolünü kullanan dosya paylaşımları sağlar. Şirket içinde veya Azure bir istemciden bir dosya paylaşımı bağlayabilir. Takılı sonra Robocopy gibi araçlar dosya paylaşımları tooAzure kullanılan toocopy dosyaları olabilir. Daha fazla bilgi için bkz: [nasıl toomount Azure dosya paylaşımı Windows](storage-file-how-to-use-files-windows.md) ve [nasıl toomount Azure dosya paylaşımı Linux'ta](storage-how-to-use-files-linux.md).


#### <a name="using-hello-storage-client-libraries"></a>Merhaba depolama istemcisi kitaplıklarını kullanma
Blob depolama biriminden veya depolama istemci kitaplığı .NET, C++, Java, Android, Node.js, PHP, Python ve Ruby gibi zengin bizim kümesini kullanarak depolama hesapları arasında blob veya dosya veri tooand kopyalayabilirsiniz.

toolearn daha, lütfen şu adresi ziyaret bizim [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md).

#### <a name="using-a-storage-explorer"></a>Depolama Gezgini'ni kullanma
Bir Depolama Gezgini toocreate depolama hesaplarını kullanmak, karşıya yükleme ve veri indirin, BLOB'lar içeriğini görüntülemek ve dizinleri gidin. Şifreleme etkin bu tooupload BLOB'lar tooyour depolama hesabı birini kullanabilirsiniz. Bazı depolama gezginleri ile mevcut blob depolama tooa farklı kapsayıcısı hello depolama hesabındaki verilerden veya etkin SSE sahip yeni bir depolama hesabı da kopyalayabilirsiniz.

toolearn daha, lütfen şu adresi ziyaret [Azure depolama gezginleri](storage-explorers.md).

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a>4. adım: Sorgu hello hello durumunu veri şifrelenir.
Merhaba depolama istemci Kitaplığı'nın güncelleştirilmiş bir sürümünü veya şifrelenmişse sağlayan bir nesne toodetermine tooquery hello durumu dağıtıldı. Bu şu anda yalnızca Blob Depolama için kullanılabilir. Merhaba yol haritası üzerinde dosya depolama desteğidir. 

Hello bu arada, çağırıp [hesap özellikleri Al](https://msdn.microsoft.com/library/azure/mt163553.aspx) depolama hesabı hello tooverify şifreleme etkin ya da Görünüm hello Azure Portalı'nda depolama hesap özelliklerini hello içeriyor.

## <a name="encryption-and-decryption-workflow"></a>Şifreleme ve şifre çözme iş akışı
Aşağıda, hello şifreleme/şifre çözme iş akışı kısa bir açıklaması verilmiştir:

* Merhaba müşteri hello depolama hesabı üzerinde şifrelemeyi etkinleştirir.
* Merhaba müşteri yeni verileri (PUT Blob, PUT bloğu, PUT sayfası, PUT dosya vb.) tooBlob veya dosya depolama yazdığında; Her yazma 256 bit kullanılarak şifrelenir [AES şifreleme](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), hello güçlü blok birini şifrelemeleri kullanılabilir.
* Merhaba müşteri tooaccess verileri (Blob alma, vb.) gerektiğinde veri toohello kullanıcı döndürmeden önce otomatik olarak çözülür.
* Şifreleme devre dışı bırakılırsa, yeni yazma artık şifrelenir ve mevcut şifrelenmiş verileri hello kullanıcı tarafından yeniden yazılmıştır kadar şifrelenmiş kalır. Şifreleme etkinken tooBlob veya dosya depolama şifrelenir yazar. etkinleştirme/hello depolama hesabı için şifrelemeyi devre dışı bırakma arasında geçiş hello kullanıcıyla veri Hello durumunu değiştirmez.
* Tüm şifreleme anahtarlarını şifreli, saklanır ve Microsoft tarafından yönetilir.

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Sık sorulan bekleyen veri için depolama hizmeti şifrelemesi hakkında sorular
**S: Klasik depolama hesabınız sahibim. SSE üzerinde etkinleştirebilirim?**

A: Hayır SSE yalnızca Resource Manager depolama hesaplarında desteklenir.

**S: nasıl ı veri Klasik depolama Hesabımı şifreleyebilir mi?**

Y: yeni bir Resource Manager depolama hesabı oluşturabilir ve kullanarak verilerinizi kopyalamak [AzCopy](storage-use-azcopy.md) varolan Klasik depolama hesabınızdan tooyour yeni Resource Manager depolama hesabı oluşturuldu. 

Klasik depolama hesabı tooa Resource Manager depolama hesabı geçirirseniz, bu işlem anlık, hesabınızı hello türünü değiştirir ancak mevcut verilerinizi etkilemez. Yalnızca şifreleme etkinleştirildikten sonra herhangi bir yeni yazılmış veri şifrelenir. Daha fazla bilgi için bkz: [Platform desteklenen geçiş, Iaas kaynaklardan Klasik tooResource Yöneticisi](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/). Bu yalnızca Blob ve Dosya Hizmetleri için desteklendiğini unutmayın.

**S: mevcut bir Resource Manager depolama hesabını sahibim. SSE üzerinde etkinleştirebilirim?**

Evet, ancak yalnızca yeni veri yazıldığı A: şifrelenir. Geri dönün yok ve önceden mevcut verileri şifrelemek. Bu dosya depolama Önizleme hello için henüz desteklenmiyor.

**S: tooencrypt hello geçerli verileri var olan bir Resource Manager depolama hesabı ister misiniz?**

A: Resource Manager depolama hesabı herhangi bir zamanda, SSE etkinleştirebilirsiniz. Ancak, zaten mevcut veri şifrelenmez. tooencrypt mevcut verileri tooanother adı veya başka bir kapsayıcı kopyalayın ve şifrelenmemiş hello sürümlerini kaldırın.

**S: Premium depolama kullanıyorum; SSE kullanabilir miyim?**

A: Evet SSE hem standart depolama hem de Premium depolama desteklenir.  Premium depolama dosya hizmeti hello için desteklenmiyor.

**S: ı yeni bir depolama hesabı oluşturup SSE etkinleştirmek, ardından bu depolama hesabı kullanarak yeni bir VM oluşturmak varsa, VM'im şifrelenmiş anlama geliyor?**

Y: Evet. SSE etkinleştirildikten sonra oluşturulan sürece hello yeni depolama hesabı kullanmak oluşturulmuş diskler şifrelenir. VM Azure markette, hello VHD temel görüntü kullanılarak oluşturulmuş hello şifrelenmemiş kalacaksa; Ancak, hello VM çalışmaya başlar sonra yapılan tüm yazma şifrelenir.

**S: yeni depolama hesapları ile Azure PowerShell ve Azure CLI kullanarak etkin SSE oluşturabilir miyim?**

Y: Evet.

**S: SSE etkinse, daha fazlasını nasıl Azure depolama maliyeti?**

Y: yoktur ek ücret ödemeden.

**S: hello şifreleme anahtarları yöneten?**

Y: hello anahtarları Microsoft tarafından yönetilir.

**S: kendi şifreleme anahtarları kullanmak?**

Y: özelliklerinin müşteriler toobring için kendi şifreleme anahtarlarını sağlanması çalışıyoruz.

**S: erişim toohello şifreleme anahtarlarını iptal?**

Şu anda A:; Merhaba anahtarları tam olarak Microsoft tarafından yönetilir.

**S: yeni bir depolama hesabı oluşturduğunuzda, varsayılan olarak etkin SSE mi?**

Y: SSE varsayılan olarak etkin değildir; hello Azure portal tooenable kullanabilirsiniz. Program aracılığıyla da hello depolama kaynak sağlayıcısı REST API kullanarak bu özelliği etkinleştirebilirsiniz.

**S: nasıl bu Azure Disk Şifrelemesi ' farklı mı?**

Y: Bu özellik, Azure Blob depolamada kullanılan tooencrypt verilerdir. Hello Azure Disk şifrelemesi Iaas Vm'leri kullanılan tooencrypt işletim sistemi ve veri diskleri ' dir. Daha fazla ayrıntı için lütfen ziyaret bizim [depolama Güvenlik Kılavuzu](storage-security-guide.md).

**S: Peki SSE, etkinleştirilir ve ardından Git ve Azure Disk şifrelemesi hello disklerde etkinleştirmek?**

Y: Bu sorunsuz bir şekilde çalışır. Her iki yöntemle veri şifrelenir.

**S: depolama Hesabımı coğrafi nedenle çoğaltılan toobe ayarlanır. SSE etkinleştirirseniz, my yedek kopya de şifrelenir mi?**

A: Evet hello depolama hesabı tüm kopyalarını şifrelenir ve tüm artıklık seçenekleri – yerel olarak yedekli depolama (LRS), bölge olarak yedekli depolama (ZRS), coğrafi olarak yedekli depolama (GRS) ve okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) – desteklenir.

**Depolama Hesabımı s: şifreleme etkinleştirilemiyor.**

Y: Resource Manager depolama hesabı mı? Klasik depolama hesapları desteklenmez. 

**S: SSE yalnızca belirli bölgelerine izin?**

Y: hello SSE Blob storage için tüm bölgelerde kullanılabilir. Dosya depolama için hello kullanılabilirlik bölümünü gözden geçirin. 

**S: herhangi bir sorununuz veya tooprovide geri bildirim istediğiniz nasıl ı biriyle iletişim?**

A: Lütfen başvurun [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) tooStorage hizmeti şifreleme herhangi bir sorunla ilgili.

## <a name="next-steps"></a>Sonraki Adımlar
Azure depolama toobuild güvenli uygulamalar birlikte, geliştiricilerin güvenlik özellikleri kapsamlı bir kümesini sağlar. Daha fazla ayrıntı için hello ziyaret [depolama Güvenlik Kılavuzu](storage-security-guide.md).

