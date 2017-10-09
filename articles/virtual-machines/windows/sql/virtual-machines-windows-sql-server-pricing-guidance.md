---
title: "Azure virtual machines'de SQL Server için etkili bir şekilde aaaManage maliyetleri | Microsoft Docs"
description: "Merhaba doğru SQL Server sanal fiyatlandırma modeli makine seçmeden için en iyi yöntemler sağlar."
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>SQL Server Azure VM'ler için fiyatlandırma Kılavuzu

Bu konu, azure'da SQL Server sanal makineler için fiyatlandırma yönergeler sağlar. Maliyet etkileyen birkaç seçeneğiniz vardır ve iş gereksinimleri maliyetleriyle dengeleyen önemli toopick hello sağ görüntü değil.

## <a name="free-licensed-sql-server-editions"></a>Serbest lisanslı SQL Server sürümleri

Toodevelop isterseniz, test, veya bir kavram kanıtı yapı sonra serbest lisanslı hello kullan **SQL Server Geliştirici sürümü**. Bu sürüm SQL Server Enterprise Edition'da her şeyi içerir, böylece toobuild kullanabilirsiniz, istediğiniz herhangi bir uygulama. Bu toorun üretimde izin değil. Bir SQL Server Geliştirici VM yalnızca SQL Server Lisans için VM hello hello maliyetini için ücretlendirir.

Toorun basit bir iş yükü üretimde istiyorsanız (< 4 çekirdek, < 1 GB bellek, < 10 GB/veritabanı), serbest lisanslı hello kullan **SQL Server Express edition**. SQL Express VM yalnızca hello VM hello maliyeti ücretinin değil SQL lisans.

Bu geliştirme ve test veya basit üretim iş yükleri için bu iş yükleri eşleşen daha küçük bir VM boyutu seçerek para da kaydedebilirsiniz. Merhaba DS1v2 bu iş yükleri için iyi bir seçimdir olabilir.

toocreate SQL Server 2016 Azure VM bu görüntülerden birini içeren bağlantılar aşağıdaki hello bakın:

- [SQL Server 2016 Geliştirici Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [SQL Server 2016 Express Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>Ücretli SQL Server sürümleri

Basit olmayan üretim iş yükü varsa, SQL Server sürümleri aşağıdaki hello birini kullanın:

| SQL Server sürümü | İş yükü |
|-----|-----|
| Web | Küçük web siteleri |
| Standart | Küçük toomedium iş yükleri |
| Enterprise | Büyük veya kritik iş yükleri|

Bu sürümleri için SQL Server Lisans için iki seçenek toopay sahip: *kullanım başına ödeme* veya *kendi lisansını Getir*.

### <a name="pay-per-usage"></a>Kullanım Öde

**Ödeyen hello SQL Server Lisansı kullanım başına** hello Azure VM çalıştıran hello dakika başına maliyetini hello SQL Server Lisans hello maliyetini içerdiği anlamına gelir. Hello hello hello farklı SQL Server sürümleri için (Web, Standard, Enterprise) fiyatlandırma görebilirsiniz [Azure VM fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Merhaba maliyet olduğu hello aynı SQL Server'ın tüm sürümleri için (2008 R2 too2016). SQL Server ile lisans genel olarak, hello gibi dakika başına lisanslama ücreti hello VM çekirdek sayısına bağlıdır.

SQL Server Hello ödeme kullanım lisansı için önerilir:

- Geçici veya düzenli aralıklarla iş yükleri. Örneğin, bir olay toosupport birkaç ay sayısı her yıl veya İş analizi Pazartesi günleri gereken bir uygulaması.
- İş yükleri bilinmeyen yaşam süresi veya ölçeğe sahip. Örneğin, birkaç ay içinde gerekli olabilecek değil ya da daha fazla veya daha az işlem gücü, isteğe bağlı olarak gerektirebilecek uygulama.

toocreate SQL Server 2016 Azure VM bu kullanım başına ödeme görüntülerden birini içeren bağlantılar aşağıdaki hello bakın:

- [SQL Server 2016 Web Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [SQL Server 2016 standart Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> Hello Azure portalında bir SQL Server sanal makine oluşturduğunuzda, hello hello üzerinde görüntülenen aylık maliyeti tahmini **bir boyutu seçin** dikey penceresinde, SQL Server Lisans maliyetleri içermez. Merhaba VM başına başlangıç maliyeti budur.
>
> ![VM boyutu dikey seçin](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Merhaba serbest lisanslı Express ve geliştirici SQL Server sürümleri için bu hello toplam tahmini maliyet olur. Ancak Web, Standard ve Enterprise hello ek SQL lisanslama maliyetleri üzerinde hello bulur. [Windows sanal makineler fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Fiyatlandırma sayfası hello üzerinde SQL Server'ın, hedef sürümünü seçin.

### <a name="bring-your-own-license-byol"></a>Kendi lisansınızı getirin (BYOL)

**SQL Server Lisansı ile lisans taşınabilirliği getiren**, tooas ya da **KLG**, Azure VM'deki Yazılım Güvencesi ile varolan bir SQL Server toplu lisans kullanarak anlamına gelir. Toplu Lisanslama programı aracılığıyla lisans ve Yazılım Güvencesi zaten edindiğiniz o KLG kullanarak bir SQL Server VM yalnızca SQL Server Lisans değil, VM, hello çalıştırmaya hello maliyeti için ücretlendirir.

Kendi SQL getirme ile lisans taşınabilirliği lisans için önerilir:

- Sürekli iş yükleri. Örneğin, toosupport işletmenize 7 x 24 gerektiren bir uygulama.
- İş yükleri bilinen yaşam süresi ve ölçeğe sahip. Örneğin, hello tüm yıl ve hangi talebin tahmini için gerekli olacak bir uygulama.

toouse KLG bir SQL Server VM ile olmalıdır bir lisans için SQL Server Standard veya Enterprise ve [Yazılım Güvencesi](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), gerekli bir seçenek bazı aracılığıyla olduğu [Toplu Lisanslama](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programlar ve isteğe bağlı başkalarıyla satın alın.  Toplu Lisanslama programları üzerinden sağlanan düzeyleri fiyatlandırma Merhaba, hello sözleşme ve hello miktarı ve/veya taahhüt tooSQL sunucu türüne göre değişir. Ancak altın kural, sürekli üretim iş yükleri için kendi lisansını getiren hello aşağıdaki avantajları vardır:

| KLG avantajı | Açıklama |
|-----|-----|
| **Maliyet tasarrufları** | Kendi SQL Server lisansınızı getiren daha düşük bir iş yükü sürekli olarak SQL Server Standard veya Enterprise çalıştırırsanız, kullanım ödeme daha maliyetli *10 aydan daha uzun*. |
| **Uzun vadeli tasarrufları** | Ortalama olarak olan *% 30 yıllık ucuz* toobuy veya ilk 3 yıl hello için bir SQL Server Lisans yenileme. Ayrıca, 3 yıl sonra toorenew hello lisans artık, Yazılım Güvencesi için yalnızca ödeme gerekmez. Bu noktada, olan *% 200 ucuz*. |
| **Ücretsiz pasif ikincil çoğaltma** | Kendi lisansını getiren başka bir yararı hello olan [Pasif bir ikincil çoğaltma için lisans serbest](https://azure.microsoft.com/pricing/licensing-faq/) başına SQL Server yüksek kullanılabilirlik sağlamak için. Yarı hello (örn. Always On kullanılabilirlik grupları kullanarak) yüksek oranda kullanılabilir bir SQL Server dağıtımı maliyetini lisans keser. Merhaba hakları toorun hello pasif ikincil yük devretme sunucuları Yazılım Güvencesi avantajı hello sağlanır. |

toocreate bir SQL Server 2016 Azure VM ile bu Getir bilgisayarınızı-kendi-lisans görüntülerden birini "{KLG}" ile önek hello VM'ler bakın:

- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [SQL Server 2016 standart Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Lütfen bize 10 gün içinde Azure'da kullanacağınız kaç SQL Server lisansları bildirin. Merhaba bağlantılar toohello önceki görüntüleri yönergeleri hakkında sahip toodo bu.

## <a name="avoid-unecessary-costs"></a>Unecessary maliyetleri kaçının

Sürekli olarak çalıştırmayın herhangi bir iş yükünü kullanıyorsanız, hello etkin olmayan dönemlerde hello sanal makinesi kapatılıyor göz önünde bulundurun. Sadece kullandığınız kadar ödersiniz.

Yalnızca Azure VM'de SQL Server çıkışı çalışıyorsanız, örneğin, size tooincur ücretleri yanlışlıkla hafta boyunca çalışır durumda bırakarak istemezsiniz. Bir çözümdür toouse hello [otomatik kapatma özelliği](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![SQL VM autoshutdown](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

Otomatik kapatma benzer özellikleri tarafından sağlanan daha büyük bir parçası olan [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).

Diğer iş akışları için otomatik olarak kapatma ve gibi bir komut dosyası çözümüyle Azure sanal makineleri yeniden başlatmayı düşünün [Azure Otomasyonu](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> Kapatılıyor ve VM serbest bırakma hello tek yolu tooavoid ücret olur. Sadece durdurma veya güç seçenekleri tooshut hello VM tuşunu kullanarak hala kullanım ücretleri doğurur.

## <a name="next-steps"></a>Sonraki adımlar

Kılavuzlar, fiyatlandırma için genel Azure bkz [Azure faturalama ve maliyet yönetimi ile beklenmeyen maliyetleri önlemek](../../../billing/billing-getting-started.md).

Merhaba fiyatlandırma, sanal makinelere en son SQL Server dahil olmak üzere bkz hello [Azure VM fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Diğer SQL Server sanal makine konuları gözden [Azure sanal makineleri genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).
