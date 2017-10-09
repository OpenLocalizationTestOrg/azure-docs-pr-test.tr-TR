---
title: Azure depolama kullanan aaaSecuring PaaS uygulamalar | Microsoft Docs
description: " Azure Storage güvenliği hakkında bilgi edinme PaaS web ve mobil uygulamaların güvenliğini sağlamaya yönelik en iyi uygulamalar. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: TomShinder
ms.openlocfilehash: 3fed75cb121e7f32eb8b948ee12ca35fb25eca7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-storage"></a>PaaS web ve mobil uygulamaları Azure Storage kullanarak güvenli hale getirme
Bu makalede, PaaS web ve mobil uygulamaların güvenliğini sağlamak için Azure Storage en iyi güvenlik yöntemleri topluluğu tartışın. Bu en iyi uygulamaları Azure ile deneyimi bizim türetilmiş ve müşterilerin hello deneyimleri bulunun.

Merhaba [Azure Storage Güvenlik Kılavuzu'nu](../storage/common/storage-security-guide.md) Azure Storage ve güvenlik hakkında ayrıntılı bilgi için mükemmel bir kaynaktır.  Bu makalede yüksek düzeyde hello kavramların hello Güvenlik Kılavuzu ve bağlantıları toohello Güvenlik Kılavuzu'nu yanı sıra, daha fazla bilgi için diğer kaynakları bulunan bazıları giderir.

## <a name="azure-storage"></a>Azure Storage
Azure yapar olası toodeploy ve kullanımı depolama yollarla içi kolayca ulaşılabilir. Azure storage ile ölçeklenebilirlik ve kullanılabilirlik nispeten az çaba ile yüksek düzeyde ulaşabilirsiniz. Yalnızca Azure depolama hello foundation, Windows ve Linux Azure sanal makineler için de büyük dağıtılmış uygulamaları destekleyebilir.

Azure depolama dört Hizmetleri aşağıdaki hello sunar: Blob Depolama, Table storage, kuyruk depolama ve dosya depolama. toolearn daha, fazla [giriş tooMicrosoft Azure Storage](../storage/storage-introduction.md).

## <a name="best-practices"></a>En iyi uygulamalar
Bu makalede en iyi uygulamaları izleyerek hello ele alır:

- Erişim Koruması:
   - Paylaşılan Erişim İmzaları (SAS)
   - Yönetilen disk
   - Rol Tabanlı Erişim Denetimi (RBAC)

- Depolama şifrelemesi:
   - Yüksek değerli veri için istemci tarafı şifrelemesi
   - Sanal makineler (VM'ler) için Azure Disk şifrelemesi
   - Depolama Hizmeti Şifrelemesi

## <a name="access-protection"></a>Erişimi Koruması
### <a name="use-shared-access-signature-instead-of-a-storage-account-key"></a>Bir depolama hesabı anahtarı yerine paylaşılan erişim imzası kullanın

Genellikle Windows Server veya Linux sanal makineleri çalıştıran bir Iaas çözümündeki dosyaları açığa çıkması ve erişim denetimi düzenekleri kullanarak değiştirme tehditlerinden korunur. Windows üzerinde kullanacağınız [erişim denetimi listeleri (ACL)](../virtual-network/virtual-networks-acl.md) ve büyük olasılıkla kullandığınız Linux üzerinde [chmod](https://en.wikipedia.org/wiki/Chmod). Esas olarak, tam olarak kendi veri merkezinizde bir sunucudaki dosyalarının bugün koruma varsa yapmayı tercih budur.

PaaS farklıdır. Merhaba en yaygın şekilde toostore dosyalarında Microsoft Azure biri toouse [Azure Blob Depolama](../storage/storage-dotnet-how-to-use-blobs.md). Bir Blob Depolama ve diğer dosya depolama arasında hello dosya g/ç ve dosya g/ç ile gelen hello koruma yöntemleri farktır.

Erişim denetimi önemlidir. erişim tooAzure depolama kontrol toohelp hello sistem oluşturacağını iki 512 bit depolama hesabı anahtarları (SAKs) olduğunda, [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md). anahtar artıklık Hello düzeyi, rutin anahtar döndürme sırasında tooavoid hizmet kesme için mümkün kılar.

Depolama erişim tuşlarını yüksek öncelikli gizli olan ve erişilebilen toothose depolama erişim denetimi için sorumlu yalnızca olmalıdır. Hello yanlış kişilerin toothese anahtarları erişmek depolama tam denetime sahiptir ve değiştirmek, silmek veya dosyaları toostorage ekleyin. Bu, kötü amaçlı yazılım ve diğer kuruluşunuzun veya müşterilerinize tehlikeye atabilir içerik türlerini içerir.

Yine bir şekilde tooprovide erişim tooobjects depolama gerekir. tooprovide daha ayrıntılı erişim yararlanabilir [paylaşılan erişim imzası](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). Merhaba SAS, depolama tooshare belirli nesneler için özel izinler ve ön tanımlı bir zaman aralığı için mümkün kılar. Paylaşılan erişim imzası toodefine sağlar:

- hello aralığı hangi hello SAS hello başlangıç saati ve hello sona erme saati dahil olmak üzere, geçerli değil.
- SAS Hello tarafından hello izinler. Örneğin, bir blob SAS kullanıcı okuma izni ve izinleri toothat blob yazma, ancak izinleri silmemeniz.
- İsteğe bağlı bir IP adresi veya IP adresi aralığı, Azure Storage kabul SAS hello. Örneğin, tooyour kuruluş ait bir IP adresi aralığı belirtebilirsiniz. Bu, SA'ları için başka bir ölçüye güvenlik sağlar.
- Merhaba protokolü üzerinden Azure Storage hello SAS kabul eder. HTTPS kullanarak bu isteğe bağlı bir parametre toorestrict erişim tooclients kullanabilirsiniz.

SAS tooshare istediğiniz tooshare içerik hello biçimde verir uzakta depolama hesabı anahtarlarını vermiş olmadan. Her zaman, uygulamanızda SAS kullanarak depolama hesabı anahtarlarını tehlikeye olmadan depolama kaynaklarınıza güvenli şekilde tooshare değil.

toolearn daha, fazla [paylaşılan erişim imzaları kullanma](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). Bu riskleri toolearn olası riskleri ve öneriler toomitigate hakkında daha fazla bilgi görmek [en iyi yöntemler SAS kullanırken](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="use-managed-disks-for-vms"></a>VM'ler için yönetilen diskleri kullanın

Seçtiğinizde [Azure yönetilen diskleri](../storage/storage-managed-disks-overview.md), Azure VM diskleriniz için kullandığınız hello depolama hesapları yönetir. Toodo gereken tek şey hello disk (Premium ya da standart) ve hello disk boyutu seçin; Azure depolama yeterlidir hello rest. Aksi takdirde tooyou toomultiple depolama hesapları gerekli sahip ölçeklenebilirlik sınırları hakkında tooworry yok.

toolearn daha, fazla [yönetilen ve yönetilmeyen premium diskler hakkında sık sorulan sorular](../storage/storage-faq-for-disks.md).

### <a name="use-role-based-access-control"></a>Rol tabanlı erişim denetimi kullanma

Daha önce hesabı depolama hesabı anahtarınızı sokmadan depolama hesabı tooother istemcilerinize, paylaşılan erişim imzası (SAS) toogrant sınırlı erişim tooobjects kullanma açıklanmaktadır. Bazen, depolama hesabınız karşı belirli bir işlemle ilişkili hello riskleri SAS hello avantajlarından daha ağır basar. Bazen diğer yollarla daha basit toomanage erişimi olur.

Başka bir şekilde toomanage erişim toouse, [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) (RBAC). RBAC, çalışanlar gereksinim duydukları hello tam izinleri veriyorsanız, odaklanmasına ile hello gerek tooknow ve en az ayrıcalık güvenlik ilkelerine göre. Çok fazla izinleri bir hesap tooattackers getirebilir. Çok az izinleri anlamına gelir çalışanlar verimli bir şekilde işlerini alınamıyor. RBAC, Azure için ayrıntılı erişim yönetimi sunarak bu sorunu gidermeye yardımcı olur. Bu, veri erişimi için tooenforce güvenlik ilkeleri istediğiniz kuruluşlar için zorunludur.

Azure tooassign ayrıcalıkları toousers yerleşik RBAC rollerinde yararlanabilirsiniz. Depolama hesabı katkıda bulunan toomanage depolama hesapları ve klasik depolama hesabı katkıda bulunan rolü toomanage Klasik depolama hesaplarını gereken bulut işleçlerini kullanmayı düşünün. Toomanage VM'ler ancak hello sanal ağ veya depolama hesabı toowhich bağlı olan gereksinim bulut operatörleri için bunları toohello sanal makine katkıda bulunan rolü eklemeyi düşünün.

Veri erişim denetimi RBAC gibi özellikler yararlanarak zorlamaz kuruluşlar kendi kullanıcıları için gerekenden daha fazla ayrıcalık vermiş. Merhaba ilk yerinde olmamalıdır bazı kullanıcılara erişim toodata izin vererek bu toodata güvenliğinin aşılmasına neden olabilir.

toolearn RBAC hakkında daha fazla bakın:

- [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md)
- [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md)
- [Azure depolama Güvenlik Kılavuzu](../storage/common/storage-security-guide.md) nasıl toosecure depolama hesabı ile RBAC hakkında ayrıntılı bilgi için

## <a name="storage-encryption"></a>Depolama şifrelemesi
### <a name="use-client-side-encryption-for-high-value-data"></a>İstemci tarafı şifreleme yüksek değerli verileri için kullanın

Tooprogrammatically tooAzure depolama karşıya yüklemeden önce Aktarımdaki verileri şifrelemek ve program aracılığıyla depolama biriminden alınırken verilerin şifresini istemci tarafı şifreleme sağlar.  Bu Aktarımdaki verileri şifreleme sağlar ancak aynı zamanda kalan verileri şifrelemesini sağlar.  İstemci tarafı şifreleme, verileri şifrelemek hello en güvenli yöntemdir, ancak toomake programsal değişiklikler tooyour uygulama gerektirir ve anahtar yönetimi işlemleri yerleştirdiniz.

İstemci tarafı şifreleme, şifreleme anahtarlarınızı üzerinde tek denetim toohave da sağlar.  Oluştur ve kendi şifreleme anahtarlarınızı yönetin.  İstemci tarafı şifreleme yere hello Azure storage istemci kitaplığı (Merhaba anahtar şifreleme anahtarı (KEK) kullanılarak şifrelenir) sonra kaydırılan bir içerik şifreleme anahtarı (CEK) oluşturur bir zarf teknik kullanır. Merhaba KEK anahtar bir tanımlayıcıyla tanımlanır ve asimetrik anahtar çifti ya da bir simetrik anahtar olması ve yerel olarak yönetilebilir veya depolanan [Azure anahtar kasası](../key-vault/key-vault-whatis.md).

İstemci tarafı şifreleme hello Java ve hello .NET depolama istemcisi kitaplıklarını içinde yerleşik olarak bulunur.  Bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](../storage/storage-client-side-encryption.md) istemci uygulamalar içinde verilerin şifrelenmesi ve oluşturma ve kendi şifreleme anahtarlarınızı yönetme hakkında bilgi için.

### <a name="azure-disk-encryption-for-vms"></a>VM'ler için Azure Disk şifrelemesi
Azure Disk şifrelemesi, Windows ve Linux Iaas sanal makine disklerinizi şifrelemek yardımcı olan bir özelliktir. Azure Disk şifrelemesi hello endüstri standart BitLocker özelliği, Windows ve Linux tooprovide birim şifreleme hello işletim sistemi için hello DM-Crypt özelliği ve hello veri diskleri yararlanır. Merhaba çözüm denetlemek ve hello disk şifreleme anahtarları ve gizli anahtar kasası aboneliğinizi yönetmek Azure anahtar kasası toohelp tümleşiktir. Merhaba çözüm ayrıca hello sanal makine disklerdeki tüm veriler Azure depolama alanınızı bekleyen şifrelenmesini sağlar.

Bkz: [Windows ve Linux Iaas VM'ler için Azure Disk şifrelemesi](azure-security-disk-encryption.md).

### <a name="storage-service-encryption"></a>Depolama Hizmeti Şifrelemesi
Zaman [depolama hizmeti şifrelemesi](../storage/storage-service-encryption.md) dosya depolama etkin hello verileri otomatik olarak AES 256 şifreleme kullanılarak şifrelenir. Microsoft, tüm hello şifreleme, şifre çözme ve anahtar yönetimi işler. Bu özellik LRS ve GRS artıklık türleri için kullanılabilir.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede PaaS web ve mobil uygulamaların güvenliğini sağlamak için Azure Storage en iyi güvenlik uygulamaları tooa koleksiyonu kullanıma sunuldu. PaaS dağıtımlarınızın güvenliğini sağlama hakkında daha fazla toolearn bakın:

- [PaaS dağıtımlarının güvenliğini sağlama](security-paas-deployments.md)
- [PaaS web ve mobil uygulamaları Azure App Services kullanarak güvenli hale getirme](security-paas-applications-using-app-services.md)
- [Azure PaaS veritabanlarında güvenliğini sağlama](security-paas-applications-using-sql.md)
