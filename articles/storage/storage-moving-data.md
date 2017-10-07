---
title: "büyük miktarlarda verinin/Azure içinde bulut depolama biriminden aaaMoving | Microsoft Docs"
description: "Hello Azure depolama biriminden taşıma veri tooand için farklı yöntemler genel bakış."
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 8f7105fea7c2d28ba9954898743070d338f46a37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a>Azure depolama biriminden veri tooand taşıma
Toomove şirket içi veri tooAzure depolama isteyip istemediğinizi (veya tersi) vardır yolları toodo çeşitli bu. sizin için en iyi hello yaklaşım, senaryoya bağlıdır. Bu makalede farklı senaryolar ve her biri için uygun teklifleri hızlı bir genel bakış sağlar.

## <a name="building-applications"></a>Uygulamaları oluşturma
Bir uygulama oluşturuyorsanız hello REST API veya bizim birçok istemci kitaplıkları karşı geliştirme mükemmel şekilde toomove veri tooand Azure depolama biriminden ' dir.

Azure depolama .NET, iOS, Java, Android, Evrensel Windows Platformu (UWP), Xamarin, C++, Node.JS, PHP, Ruby ve Python için zengin istemci kitaplıkları sağlar. Merhaba istemci kitaplıkları yeniden deneme mantığı, günlüğe kaydetme ve paralel karşıya yüklemeler gibi gelişmiş özellikler sunar. Merhaba HTTP/HTTPS istekleri yapan herhangi bir dil tarafından çağrılabilen REST API karşı doğrudan geliştirebilirsiniz.

Bkz: [Azure Blob Storage ile çalışmaya başlama](storage-dotnet-how-to-use-blobs.md) toolearn daha fazla.

Merhaba de ayrıca, sunduğumuz [Azure Storage veri hareketi Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) Azure'dan veri tooand yüksek performanslı kopyalanması için tasarlanmış bir kitaplık değil. Lütfen tooour veri hareketi kitaplığı başvurun [belgelerine](https://github.com/Azure/azure-storage-net-data-movement) toolearn daha fazla. 

## <a name="quickly-viewinginteracting-with-your-data"></a>Verilerinizi hızla görüntüleme/verilerinizle etkileşim kurma
Ardından, kolay bir yolu tooview Azure Storage verilerinizin ayrıca hello özelliği tooupload yaparken ve verilerinizi indirmek istiyorsanız, bir Azure Storage Gezgini kullanmayı düşünün.

Listemiz denetleyin [Azure depolama gezginleri](storage-explorers.md) toolearn daha fazla.

## <a name="system-administration"></a>Sistem Yönetimi
Gerektiren veya bir komut satırı yardımcı programı ile (örneğin, sistem yöneticileri) daha rahat varsa, tooconsider için bazı seçenekler şunlardır:

### <a name="azcopy"></a>AzCopy
AzCopy yüksek performanslı veri tooand Azure depolama biriminden kopyalanması için tasarlanmış bir Windows komut satırı yardımcı programıdır. Ayrıca, verileri bir depolama hesabı içinde veya farklı depolama hesapları arasında kopyalayabilirsiniz.

Bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md) toolearn daha fazla.

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell, Azure hizmetlerini yönetmek için cmdlet’ler sağlayan bir modüldür. Sistem yönetimi için özel olarak tasarlanan görev tabanlı bir komut satırı kabuğu ve betik dili olarak tanımlanır.

Bkz: [Azure Storage ile Azure PowerShell'i kullanma](storage-powershell-guide-full.md) toolearn daha fazla.

### <a name="azure-cli"></a>Azure CLI
Azure CLI, Azure Hizmetleri ile çalışmak için platformlar arası komutları açık kaynak kümesi sağlar. Azure CLI, Windows, OSX ve Linux üzerinde kullanılabilir.

Bkz: [kullanma hello Azure Storage ile Azure CLI](storage-azure-cli.md) toolearn daha fazla.

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>Büyük miktarlarda verinin yavaş bir ağ ile taşıma
Büyük miktarlarda veri taşıma ile ilişkili hello en büyük zorluklardan biri hello aktarımı saattir. Ardından Azure içeri/dışarı aktarma hakkında ağları maliyetleri kaygı veya kod yazmadan tooget verileri Azure Storage/gruptan istiyorsanız, uygun bir çözümdür.

Bkz: [Azure içeri/dışarı aktarma](storage-import-export-service.md) toolearn daha fazla.

## <a name="backing-up-your-data"></a>Verilerinizi yedekleme
Toobackup, veri tooAzure depolama yeterlidir, Azure Backup hello yolu toogo olur. Bu, şirket içi veri ve Azure sanal makineleri yedeklemek için güçlü bir çözümdür.

Bkz: [Azure Backup](../backup/backup-introduction-to-azure-backup.md) toolearn daha fazla.

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a>Verileri şirket içi erişme ve hello bulut
Verileri şirket içi erişmek ve hello buluta bir çözüm gerekiyorsa, Azure'nın karma bulut depolama çözümü, StorSimple kullanmayı düşünmeniz gerekir. Bu çözüm fiziksel StorSimple cihazı akıllıca sık depoları verileri SSD üzerinde kullanılan, bazen HDD ve etkin olmayan/yedekleme/arşiv verileri Azure depolama birimindeki verileri kullanılan olduğunu oluşur.

Bkz: [StorSimple](../storsimple/storsimple-overview.md) toolearn daha fazla.

## <a name="recovering-your-data"></a>Veri Kurtarma
Şirket içi iş yüklerini ve uygulamaları varsa, bir olağanüstü durum hello olayda çalıştıran, iş toocontinue sağlayan bir çözüme ihtiyacınız vardır. Azure Site Recovery, çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma işler. Çoğaltılan veriler Azure depolama, yerinde ikincil veri merkezine tooeliminate hello gereksinimini izin vererek depolanır.

Bkz: [Azure Site Recovery](../site-recovery/site-recovery-overview.md) toolearn daha fazla.
### <a name="moving-data-faq"></a>Veri SSS taşıma:
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a>VHD bir bölge tooanother kopyalamadan geçişini sağlayabilir miyim?
Merhaba yalnızca bölge arasında yolu toocopy VHD'ler toocopy hello her bölge depolama hesapları arasında verilerdir. AZCopy için bunu kullanabilirsiniz. Merhaba AzCopy komut satırı yardımcı programı toolearn daha fazla aktarım verilerle bakın. İçin çok büyük miktarlarda verinin Azure içeri/dışarı aktarma de kullanabilirsiniz. Bkz: [Azure içeri/dışarı aktarma](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn daha fazla.
