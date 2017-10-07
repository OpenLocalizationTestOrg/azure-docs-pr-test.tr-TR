---
title: "aaaUpgrade bir yedekleme kasası tooa kurtarma Hizmetleri Kasası'nı (Önizleme) | Microsoft Docs"
description: "Yönergeler ve destek bilgileri tooupgrade Azure yedekleme kasası kurtarma Hizmetleri kasası tooa."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>Bir yedekleme kasası tooa kurtarma Hizmetleri kasası yükseltme

Bu makalede nasıl tooupgrade bir yedekleme kasası tooa kurtarma Hizmetleri kasası açıklanmaktadır. Merhaba yükseltme işlemi herhangi bir çalışan yedekleme işi etkilemez ve hiçbir yedekleme verileri kaybolur. Merhaba birincil tooupgrade kurtarma Hizmetleri kasası bir yedekleme kasası tooa nedenleri:
- Tüm özellikleri bir Backup kasasının kurtarma Hizmetleri kasasına korunur.
- Kurtarma Hizmetleri kasaları dahil olmak üzere, yedekleme kasaları daha fazla özelliğe sahip: izleme, tümleşik daha iyi güvenlik, daha hızlı geri yükler ve öğe düzeyinde geri yüklemeler.
- Yedekleme öğeleri geliştirilmiş, Basitleştirilmiş portalından yönetin.
- Yeni özellikler yalnızca tooRecovery Hizmetleri kasalarının geçerlidir.

## <a name="impact-toooperations-during-upgrade"></a>Yükseltme sırasında etkisi toooperations

Bir yedekleme kasası tooa kurtarma Hizmetleri kasası yükseltirken tooyour veri düzlemi işlemleri üzerinde etkisi yoktur. Tüm yedekleme işleri normal olarak devam etmek ve kesinti olmadan herhangi bir etkin geri yükleme işi devam. Merhaba yükseltme sırasında kısa bir kapalı kalma süresi yönetim işlemlerini uygulanır ve yeni öğelerinizi koruyun veya geçici yedekleme işleri oluşturun. Iaas VM'ler için geri yükleme işleri hello yükseltme sırasında çalıştırmayın. Merhaba kasası yükseltme altında bir saat toocomplete alır. İşlemi tamamladıktan sonra bir kurtarma Hizmetleri kasası hello yedekleme kasası yerini alır.

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>Değişiklikleri tooyour otomasyon ve yükselttikten sonra aracı

Hello kasası yükseltme için altyapınızı hazırlanırken, mevcut automation'ınızı güncelleştirmeniz gerekir veya tooensure tooling olan, hello yükseltmeden sonra toowork devam eder.
Merhaba Hello PowerShell cmdlet'leri başvuruları başvurun [Service Manager dağıtım modeli](backup-client-automation-classic.md) ve hello [Resource Manager dağıtım modeli](backup-client-automation.md).


## <a name="before-you-upgrade"></a>Yükseltmeden önce

Merhaba aşağıdaki yükseltme, önce yedekleme kasaları tooRecovery hizmet kasalarını sorunları kontrol edin.

- **En düşük aracı sürümü**: tooupgrade yapma emin hello Microsoft Azure kurtarma Hizmetleri (MARS) aracısı kasanızı olan en az sürüm 2.0.9070.0. Merhaba MARS Aracısı 2.0.9070.0 eski ise hello yükseltme işlemini başlatmadan önce hello aracısını güncelleştirin.
- **Örnek tabanlı faturalama modeli**: kurtarma hizmeti kasalarını yalnızca hello örnek tabanlı faturalama modelini destekler. Merhaba eski depolama tabanlı faturalama modeli kullanarak bir yedekleme kasası varsa, yükseltme sırasında hello faturalama modelini dönüştürün.
- **Yedekleme yapılandırması devam eden işlem yok**: yükseltme sırasında erişim toohello Yönetim düzeyi sınırlandırılır. Tüm yönetim düzlemi eylemleri tamamlayın ve ardından hello yükseltme başlatın.

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>PowerShell komut dosyaları tooupgrade, kasa kullanma

PowerShell komut dosyaları tooupgrade kullanabileceğiniz tooRecovery Hizmetleri kasalarının yedekleme kasaları. Sahip hello onay PowerShell bileşenleri tootrigger hello kasası yükseltme gerekli. Yedekleme kasaları için PowerShell komut dosyaları için kurtarma Hizmetleri kasalarını çalışmaz. Ortamınızı tooupgrade hello kasaları hazırlayın:

1. Yükleme veya yükseltme [Windows Management Framework (WMF) tooversion 5](https://www.microsoft.com/download/details.aspx?id=50395) veya üstü.
2. [Azure PowerShell MSI yükleme](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi).
3. Merhaba karşıdan [PowerShell Betiği](https://aka.ms/vaultupgradescript2) tooupgrade, kasa.

### <a name="run-hello-powershell-script"></a>Merhaba PowerShell betiğini çalıştırın

Komut dosyası tooupgrade aşağıdaki Merhaba, kasa kullanın. Aşağıdaki örnek betik hello hello parametre açıklamalarını sahiptir.

RecoveryServicesVaultUpgrade 1.0.2.ps1 **- Subscriptionıd** `<subscriptionID>` **- VaultName** `<vaultname>` **-konum** `<location>` **- ResourceType** `BackupVault` **- TargetResourceGroupName**`<rgname>`

**Subscriptionıd** -hello yükseltiliyor hello kasa abonelik kimliği sayısı.<br/>
**VaultName** - hello yükseltiliyor hello yedekleme kasasının adı.<br/>
**Konum** -yükseltilen hello kasasının konumu.<br/>
**ResourceType** -BackupVault kullanın.<br/>
**TargetResourceGroupName** - bir kaynak grubu belirtin Resource Manager tabanlı hello kasa tooa dağıtımı yükseltiyorsanız bu yana. Varolan bir kaynak grubunu kullanın veya yeni bir ad sağlayarak oluşturabilirsiniz. Bir kaynak grubu adını hello yazıyorsanız, yeni bir kaynak grubu oluşturabilir. Kaynak grupları hakkında daha fazla toolearn okuma bu [kaynak grupları hakkında genel bakış](../azure-resource-manager/resource-group-overview.md#resource-groups).

>[!NOTE]
> Kaynak grubu adları kısıtlamaları vardır. Toofollow hello Kılavuzu emin olun; hata toodo şekilde kasası yükseltmeler toofail neden olabilir.
>
>

Merhaba aşağıdaki kod parçacığını hangi PowerShell komutu gibi görünmelidir, bir örnek verilmiştir:

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

Merhaba komut dosyası hiçbir parametre olmadan da çalıştırabilirsiniz ve tüm gerekli parametreleri için tooprovide girişleri sorulur.

Merhaba PowerShell komut dosyası, tooenter kimlik bilgilerinizi ister. Kimlik bilgilerinizi iki kez girin: hello Service Manager hesabı ve ikinci kez hello Resource Manager hesabı için bir kez.

### <a name="pre-requisites-checking"></a>Ön koşul denetimi
Azure kimlik bilgilerinizi girdikten sonra Azure ortamınıza hello aşağıdaki önkoşulları karşıladığını denetler:

- **En düşük aracı sürümü** -yükseltme yedekleme kasalarını tooRecovery Hizmetleri kasaları hello MARS Aracısı toobe en azından sürüm 2.0.9070. Varsa bir aracı ile tooa yedekleme kasası öğeleri 2.0.9070'den önceki kayıtlı, hello Önkoşul denetimi başarısız olur. Merhaba Önkoşul denetimi başarısız olursa hello aracısını güncelleştirmek ve tooupgrade hello kasası yeniden deneyin. Merhaba hello Aracısı'ndan en son sürümünü indirebilirsiniz [http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe).
- **Devam eden yapılandırma işleri**: bir yedekleme kasası yükseltilmiş toobe veya öğeyi kayıt kümesi için birisi iş yapılandırıyor, hello Önkoşul denetimi başarısız olur. Başlangıç yapılandırmasını tamamlayın veya hello öğesi kaydolma işlemini tamamlamak ve hello kasası yükseltme işlemi başlatın.
- **Depolama tabanlı faturalama modeli**: Kurtarma Hizmetleri kasaları destek hello örnek tabanlı faturalama modeli. Bir yedekleme kasası hello kasası yükseltme çalıştırırsanız, depolama tabanlı faturalama modelini kullanan Merhaba, istendiğinde tooupgrade olduğunuz hello yanı sıra faturalama modelinizi Kasa. Faturalama modelinizi ilk olarak, aksi takdirde, güncelleştirebilir ve ardından hello kasası yükseltme çalıştırın.
- Merhaba kurtarma Hizmetleri kasası için bir kaynak grubu tanımlayın. tootake avantajlarından Merhaba Resource Manager dağıtım özellikleri, bir kaynak grubu bir kurtarma Hizmetleri kasası konulmalıdır. Bir ad ve hello yükseltme işlemine sağlayın, hangi kaynak grubu toouse bilmiyorsanız hello kaynak grubu oluşturur. Merhaba yükseltme işlemi de ilişkilendirir hello kasası ile yeni kaynak grubu hello.

Merhaba ön koşul denetimi Hello yükseltme işlemi tamamlandıktan sonra toostart hello kasası yükseltme hello işlem ister. Siz onayladıktan sonra hello yükseltme işlemi genellikle kasanızı hello boyutuna bağlı olarak 15-20 dakika toocomplete geçici sürer. Büyük bir kasa varsa, yükseltme too90 dakika sürebilir.

## <a name="managing-your-recovery-services-vaults"></a>Kurtarma Hizmetleri kasalarını yönetme

ekranlar aşağıdaki hello yedekleme Kasası'hello Azure Portalı'ndan yükseltme yeni bir kurtarma Hizmetleri kasası gösterir. Merhaba ilk ekranda hello kasa için anahtar varlıklar görüntüler hello kasa Panosu gösterilir.

![Kurtarma Hizmetleri kasasına yedekleme Kasası'nı yükseltme örneği](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

Merhaba ikinci ekranı hello kurtarma hizmetleri kullanmaya başlama kullanılabilir toohelp kasa hello Yardım bağlantıları gösterir.

![Yardım bağlantıları hello hızlı başlangıç dikey](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>Yükseltme sonrası adımlar
Kurtarma Hizmetleri kasasına yedekleme ilkesine belirten saat dilimi bilgilerini destekler. Kasa başarıyla yükseltildikten sonra kasa ayarları menüsünden tooBackup ilkeleri gidin ve her hello kasasında yapılandırılan hello İlkesi hello saat dilimi bilgilerini güncelleştirin. Bu ekran zaten kullanıldığında yerel saat dilimi ilke oluşturuldu olarak belirtilen hello yedekleme zamanlaması saati gösterir. 

## <a name="enhanced-security"></a>Geliştirilmiş güvenlik

Bir yedekleme kasası yükseltildiğinde tooa kurtarma Hizmetleri kasası, o kasası hello güvenlik ayarlarını otomatik olarak etkinleştirilir. Ne zaman hello güvenlik ayarları olan, yedeklemeler silme gibi bazı işlemler veya bir parola değiştirilmesini gerektiren bir [Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md) PIN. Merhaba makale hello Artırılmış güvenliği hakkında daha fazla bilgi için bkz [güvenlik özellikleri tooprotect karma yedeklemeleri](backup-azure-security-feature.md). 

Merhaba Gelişmiş Güvenlik etkinleştirildiğinde, veri hello kurtarma noktası bilgilerini hello kasadan silindikten sonra too14 günlerini korunur. Müşteriler bu güvenlik veri depolama için faturalandırılır. Güvenlik veri saklama hello Azure Yedekleme aracısı, Azure yedekleme sunucusu ve System Center Data Protection Manager için alınan toorecovery puan geçerlidir. 

## <a name="gather-data-on-your-vault"></a>Kasanızda verileri toplayın

Tooa kurtarma Hizmetleri kasası yükseltme yaptıktan sonra (Iaas Vm'leri ve Microsoft Azure kurtarma Hizmetleri (MARS)) raporları için Azure yedeklemeyi yapılandırma ve Power BI tooaccess hello raporları kullanın. Veri toplama hakkında ek bilgi için hello makalesine bakın [Azure Yedekleme'yi yapılandırma raporları](backup-azure-configure-reports.md).

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

**Merhaba yükseltme planı devam eden yedeklerim etkiliyor mu?**</br>
Hayır. Devam eden Yedeklemelerinizin kesintisiz sırasında ve yükseltmeden sonra devam eder.

**En kısa sürede yükseltmeyi düşünüyorsanız yok, toomy kasalarını ne olur?**</br>
Tüm yeni özellikler yalnızca tooRecovery Hizmetleri kasa uygulamak olduğundan, biz, tooupgrade, kasa bağlantısını okumanızı tavsiye. Microsoft, sonunda hello Klasik portal Kaldır. 1 Eylül 2017 başlangıç Microsoft Otomatik yükseltme başlayacak yedekleme kasaları tooRecovery Hizmetleri kasalarının. 1 Kasım 2017 tarafından Microsoft hello yükseltme işlemini tamamlanır. Kasanızı Eylül veya Ekim sırasında her zaman otomatik olarak yükseltilebilir. Microsoft, mümkün olan en kısa sürede kasanızı yükseltme önerir.

**Bu yükseltme ortalaması my varolan araçları için nedir?**</br>
Araç toohello Resource Manager dağıtım modeli güncelleştirin. Kurtarma Hizmetleri kasaları için oluşturulan hello Resource Manager dağıtım modelinde kullanın. Merhaba Resource Manager dağıtım modeli için planlama ve hello fark, kasa için Hesap önemlidir. 

**Merhaba yükseltme sırasında kadar kapalı kalma süresi var mı?**</br>
Yükseltilen kaynakları hello sayısına bağlıdır. (Korumalı örnekler birkaç onlarca) daha küçük dağıtımlar için hello tüm yükseltme 20 dakikadan kısa sürer. Büyük ölçekli dağıtımlarda, en çok bir saat sürer.

**I yükselttikten sonra geri alabilirsiniz?**</br>
Hayır. Merhaba kaynakları başarılı bir şekilde yükselttikten sonra geri alma desteklenmiyor.

**My abonelik veya kaynak toosee, yükseltme kapasitesi olmadığını doğrulamak için?**</br>
Evet. Yükseltme ilk adımda Hello hello kaynakları yükseltme kapasitesi olduğunu doğrular. Ön koşullar Hello doğrulanması başarısız olursa, hello yükseltme tamamlanamıyor tüm hello nedenlerle iletilerini alır.

**Hangi izinlerin sahibim tootrigger kasası yükseltme?**</br>
tooperform hello kasa yükseltme, hello Klasik Azure portalı hello abonelikte için ortak yönetici olarak eklenmelidir. Zaten hello Azure portal sahibi olarak listelenen olsa bile, bu gereklidir. Hello aboneliğin ortak Yöneticisi iseniz tooadd hello abonelikte Klasik Azure portalı toofind için bir ortak yönetici deneyin. Mümkün tooadd bir ortak yönetici değilse, bir ortak yönetici ekleyebilir hello abonelik için bir Hizmet Yöneticisi veya ortak yönetici başvurun.

**My CSP tabanlı bir yedekleme kasası yükseltebilir miyim?**</br>
Hayır. Şu anda, CSP tabanlı Yedekleme kasalarını yükseltemezsiniz. CSP tabanlı Yedekleme kasaları hello sonraki sürümlerde yükseltmek için destek ekleyeceğiz.

**Yükseltme sonrası my Klasik kasası görüntüleyebilir miyim?**</br>
Hayır. Görüntüleyemez veya Klasik kasanızı yükseltme sonrası yönetin. Yalnızca mümkün toouse hello yeni Azure portalına hello kasası tüm yönetim eylemlerini için olacaktır.

**My yükseltmesi başarısız oldu, ancak gerektiren hello Aracısı tutulan hello makine güncelleştiriliyor, artık mevcut değil. Böyle bir durumda ne yapmalıyım?**</br>
Toouse hello deposu ihtiyacınız varsa, bu makine için uzun vadeli bekletme, ardından hello yedeklerini mümkün tooupgrade hello kasası olmaz. Bu tür bir kasa yükseltmek için destek gelecek sürümlerde ekleyeceğiz.
Bu makinenin toostore hello yedeklemelerinin gerekmiyorsa artık sonra lütfen bu makine hello kasasından kaydını ve hello yükseltmeyi yeniden deneyin.

**Neden hello işleri bilgi şirket içi Kaynaklarım yükseltmeden sonra göremiyorum**</br>
İzleme yedeklemeleri (MARS Aracısı, DPM ve Azure Backup sunucusu), yedekleme kasası tooRecovery Hizmetleri kasası yükselttiğinizde aldığınız yeni bir özelliktir şirket içi. İzleme bilgilerini hello too12 saatleri toosync hello hizmetiyle kaplar.

**Bir sorunu nasıl bildirebilirim?**</br>
Herhangi bir kısmının hello kasası yükseltme başarısız olur, Operationıd hello hata listelenen Not hello. Microsoft Support tooresolve hello sorunu proaktif olarak çalışır. Out tooSupport ulaşmak ya da adresinden bize e-posta rsvaultupgrade@service.microsoft.com abonelik kimliği, kasa adı ve Operationıd. Mümkün olan en kısa sürede tooresolve hello sorunu deneriz. Merhaba açıkça toodo belirtilmedikçe denemeyi değil Microsoft tarafından bunu.


## <a name="next-steps"></a>Sonraki adımlar
Makale için aşağıdaki hello kullan:</br>
[Bir Iaas VM'yi yedeklemek](backup-azure-arm-vms-prepare.md)</br>
[Bir Azure yedekleme sunucuyu yedekleme](backup-azure-microsoft-azure-backup.md)</br>
[Windows Server Yedekleme](backup-configure-vault.md).
