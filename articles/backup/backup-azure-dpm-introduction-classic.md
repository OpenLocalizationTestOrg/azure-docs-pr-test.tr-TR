---
title: "DPM iş yüklerini tooAzure Klasik portal yukarı aaaBack | Microsoft Docs"
description: "Bir giriş toobacking hello Azure Yedekleme hizmetini kullanarak DPM sunucularını ayarlama"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: "System Center Data Protection Manager, veri koruma Yöneticisi, dpm yedekleme"
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>DPM ile iş yüklerini tooAzure yukarı tooback hazırlama
> [!div class="op_single_selector"]
> * [Azure Backup Sunucusu](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup sunucusu (Klasik)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (Klasik)](backup-azure-dpm-introduction-classic.md)
>
>

Bu makalede, System Center Data Protection Manager (DPM) sunucuları ve iş yükleri bir giriş toousing Microsoft Azure yedekleme tooprotect sağlar. Bunu okuyarak, anlamanız:

* Azure DPM sunucusu yedek nasıl çalışır
* Merhaba Önkoşullar tooachieve kesintisiz bir yedekleme deneyimi
* Merhaba tipik hatalarla karşılaşıldı ve nasıl onlarla toodeal
* Desteklenen senaryolar

System Center DPM dosya ve uygulama verileri yedekler. TooDPM yedeklenen verileri diskte, bantta depolanan veya Microsoft Azure yedekleme ile tooAzure yedeklendi. DPM Azure Backup ile aşağıdaki gibi etkileşim kurar:

* **Fiziksel sunucu veya şirket içi sanal makine olarak dağıtılan DPM** — DPM fiziksel sunucu olarak veya geri bir şirket içi Hyper-V sanal makinesi olarak dağıtılırsa toodisk ayrıca veri tooan Azure yedekleme kasası ve bant yedekleme.
* **Azure sanal makinesi olarak dağıtılan DPM** — güncelleştirme 3 ile System Center 2012 R2'den DPM Azure sanal makinesi olarak dağıtılabilir. DPM veri tooAzure diskleri de yedekleyebilirsiniz bir Azure sanal makinesi olarak dağıtılırsa toohello DPM Azure sanal makinesine bağlı veya tooan Azure Backup kasasını yedekleyerek hello veri depolama boşaltabilir.

## <a name="why-backup-your-dpm-servers"></a>Neden DPM sunucularını yedekleme?
DPM sunucularını yedekleme için Azure Yedekleme'yi kullanarak hello iş avantajları şunlardır:

* Şirket içi DPM dağıtımı için bir alternatif toolong terim dağıtım tootape Azure Yedekleme'yi kullanabilirsiniz.
* Azure'da DPM dağıtımları için Azure yedekleme toooffload depolama biriminden hello Azure disk tooscale yukarı eski verileri Azure yedekleme ve disk üzerindeki yeni verileri depolayarak olanak sağlar.

## <a name="how-does-dpm-server-backup-work"></a>DPM sunucusu yedek nasıl çalışır?
bir sanal makineyi zaman içinde nokta verilerin bir anlık görüntüsünü hello gereken ilk tooback. Hello Azure yedekleme hizmeti başlatır hello yedekleme işi hello zamanlanan saati ve yedekleme uzantısını tootake bir anlık görüntü Tetikleyicileri hello. Merhaba yedekleme uzantısını hello Konuk VSS koordinatlarıyla tooachieve tutarlılık hizmet ve tutarlılık ulaşıldığında hello blob anlık görüntü API'hello Azure depolama hizmeti, çağırır. Bu tooshut gerek kalmadan hello disklerin hello sanal makinenin, tutarlı bir anlık görüntü tooget Bitti, aşağı.

Başlangıç anlık görüntü alındıktan sonra hello veri hello Azure yedekleme hizmeti toohello yedekleme kasası tarafından aktarılır. Merhaba hizmet tanımlama ve hello yedeklemelerin depolama ve ağ verimli hale hello son yedeklemeden değişen hello blokları aktarma ilgilenir. Merhaba veri aktarımı tamamlandığında hello anlık görüntü kaldırılır ve bir kurtarma noktası oluşturulur. Bu kurtarma noktasını hello Klasik Azure portalı görülebilir.

> [!NOTE]
> Linux sanal makineleri için yalnızca dosyayla tutarlı yedekleme mümkündür.
>
>

## <a name="prerequisites"></a>Ön koşullar
Azure Backup tooback DPM verilerini aşağıdaki gibi hazırlayın:

1. **Bir yedekleme kasası oluşturma**. Hello Azure aboneliğinizde bir yedekleme kasası oluşturmadıysanız, bkz: Bu makalenin - portal sürümü [tooback DPM ile iş yüklerini tooAzure yukarı hazırlama](backup-azure-dpm-introduction.md).

  > [!IMPORTANT]
  > Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz.
  > Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> 15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız. **1 Kasım 2017’ye kadar**:
  >- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
  >- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
  >

2. **Kasa kimlik bilgilerini indirme** — içinde Azure Backup, toohello kasası oluşturduğunuz karşıya yükleme hello yönetim sertifikası.
3. **Hello Azure Yedekleme aracısı yükleyin ve hello sunucuyu kaydetmek** — gelen Azure yedekleme, her DPM sunucusunda hello aracıyı yükleyin ve hello yedekleme kasasında hello DPM sunucusunu kaydettirin.

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>Gereksinimleri (ve sınırlamaları)
* Bir fiziksel sunucuda veya System Center 2012 SP1 veya System Center 2012 R2'de yüklü bir Hyper-V sanal makinesi olarak DPM çalıştırıyor olabilir. System Center 2012 R2 ile en az çalışan Azure sanal makinesi olarak da çalışabilir DPM 2012 R2 güncelleştirme paketi 3 veya System Center 2012 R2 ile en az çalışan vmware'deki Windows sanal makine Güncelleştirme Paketi 5.
* System Center 2012 SP1 ile DPM çalıştırıyorsanız, System Center Data Protection Manager SP1 için Güncelleştirme Paketi 2 yüklemeniz gerekir. Hello Azure Backup aracısını yüklemeden önce bu gereklidir.
* Merhaba DPM sunucusu sahip Windows PowerShell ve .net Framework 4.5 yüklü.
* DPM, yedekleme çoğu iş yükleri tooAzure yedekleyebilirsiniz. Bkz: desteklenen sahip bir tam listesi için Azure Backup hello aşağıdaki öğeleri destekler.
* Azure Yedekleme'de depolanan verileri hello "tootape Kopyala" seçeneğiyle kurtarılamıyor.
* Hello Azure Backup özelliği etkinleştirilmiş bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Hakkında bilgi edinin [Azure yedekleme fiyatlandırması](https://azure.microsoft.com/pricing/details/backup/).
* Azure Backup kullanılarak tooback yedeklemek istediğiniz hello sunucularda yüklü hello Azure Yedekleme aracısı toobe gerektirir. Her sunucusunun yerel boş depolama olarak kullanılabilir yedeklendiğinden hello verilerin hello boyutu en az % 10 olması gerekir. Örneğin, 100 GB veri yedekleme 10 GB boş alan hello karalama konumda en az gerektirir. Merhaba en az % 10 olsa da, hello önbellek konumu için kullanılan boş yerel depolama alanı toobe % 15 önerilir.
* Veri hello Azure kasası depolama depolanır. Hiçbir sınır toohello miktarda veri tooan Azure Backup kasasını yedekleyebilirsiniz yoktur ancak (örneğin sanal makine ya da veritabanı) veri kaynağının hello boyutunu 54,400 GB aşan döndürmemelidir.

Bu dosya türlerini tooAzure yedeklemek için desteklenir:

* Şifrelenmiş (yalnızca tam yedeklemeler)
* Sıkıştırılmış (artımlı yedeklemeler desteklenir)
* Aralıklı (artımlı yedeklemeler desteklenir)
* Sıkıştırılmış ve aralıklı (aralıklı olarak kabul edilir)

Ve bu desteklenmez:

* Büyük küçük harfe duyarlı dosya sistemlerindeki sunucular desteklenmez.
* Sabit bağlantılar (atlanır)
* Yeniden ayrıştırma noktaları (atlanır)
* Şifrelenmiş ve sıkıştırılmış (atlanır)
* Şifrelenmiş ve aralıklı (atlanır)
* Sıkıştırılmış akış
* Aralıklı akış

> [!NOTE]
> Gelen System Center 2012 DPM SP1 ile başlayarak, içinde Microsoft Azure Yedekleme'yi kullanarak DPM tooAzure tarafından korunan iş yüklerini yedekleme yapabilir.
>
>
