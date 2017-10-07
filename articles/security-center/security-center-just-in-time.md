---
title: "zaman sanal makinede aaaJust erişim Azure Güvenlik Merkezi'nde | Microsoft Docs"
description: "Bu belge size nasıl yalnızca VM erişim denetimini Azure Güvenlik Merkezi yardımcı olur erişim tooyour Azure zamanında kılavuzluk sanal makineler."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>Tam zamanında kullanarak sanal makine erişimini yönetme

Yalnızca zaman sanal makine (VM) erişim gelen trafiği tooyour Azure VM'ler, gerektiğinde kolay erişim tooconnect tooVMs sağlarken Etkilenme tooattacks azaltma aşağı kullanılan toolock olabilir.

> [!NOTE]
> yalnızca zaman özellik Hello önizlemede hello Güvenlik Merkezi'nin standart katmanı üzerinde kullanılabilir.  Bkz: [fiyatlandırma](security-center-pricing.md) toolearn Güvenlik Merkezi hakkında daha fazla fiyatlandırma katmanları.
>
>

## <a name="attack-scenario"></a>Saldırı senaryosu

Deneme yanılma saldırısı, yaygın olarak anlamına gelir toogain erişim tooa VM hedef yönetim noktaları saldırıları. Başarılı olursa, bir saldırganın hello VM üzerinden denetimini ele geçirmek ve bir açısından ortamınıza oluşturun.

Tek yönlü tooreduce Etkilenme tooa yanılma saldırısı toolimit hello bir bağlantı noktasının açık olduğundan zaman miktarıdır. Yönetim bağlantı noktalarını gerek toobe açık her zaman yapın. Yalnızca ihtiyaç duydukları toobe çalışırken bağlı toohello VM, örneğin tooperform Yönetimi veya bakım görevlerinin açıktır. Tam zamanında etkinleştirilmişse, Güvenlik Merkezi kullanır [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) saldırganlar tarafından hedeflenemez erişim toomanagement bağlantı noktalarını kısıtlamanız (NSG) kuralları.

![Yalnızca zaman senaryoda][1]

## <a name="how-does-just-in-time-access-work"></a>Nasıl yalnızca süresi erişimi çalışıyor mu?

Tam zamanında etkinleştirilmişse, Güvenlik Merkezi bir NSG kuralı oluşturarak Azure VM'ler gelen trafiği tooyour kilitler. Merhaba bağlantı noktalarını seçmek aşağı gelen trafiği üzerinde hello VM toowhich kilitlenir. Bu bağlantı noktaları, yalnızca zaman çözümü hello tarafından denetlenir.

Kullanıcı erişim tooa VM istediğinde, Güvenlik Merkezi hello kullanıcının sahip denetler [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) hello Azure kaynak yazma erişimi sağlayan izinler. Yazma izinlerine sahip oldukları, hello isteğini onayladı ve Güvenlik Merkezi hello ağ güvenlik grupları (Nsg'ler) otomatik olarak yapılandırır tooallow hello süreyi belirttiğiniz için trafiği toohello yönetim bağlantı noktalarını gelen. Merhaba süresi dolduktan sonra Güvenlik Merkezi hello Nsg'ler tootheir önceki durumlarına geri yükler.

> [!NOTE]
> Güvenlik Merkezi'nde yalnızca zaman VM erişim şu anda yalnızca Azure Resource Manager aracılığıyla dağıtılan VM'ler destekler. Merhaba Klasik ve Resource Manager dağıtım modelleri hakkında daha fazla toolearn [Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md).
>
>

## <a name="using-just-in-time-access"></a>Yalnızca süresi erişimi kullanma

Merhaba **saat VM erişimi hemen** döşeme hello üzerinde **Güvenlik Merkezi** dikey penceresinde hello yalnızca zaman erişim ve hello sayısında hello geçen hafta yapılan onaylanan erişim istekleri için yapılandırılan VM sayısını gösterir.

Select hello **saat VM erişimi hemen** döşeme ve hello **saat VM erişimi hemen** dikey pencere açılır.

![Tam zamanında VM erişim döşeme][2]

Merhaba **saat VM erişimi hemen** dikey Vm'leriniz hello durumunu bilgileri sağlar:

- **Yapılandırılmış** -zaman VM Access'te yalnızca yapılandırılan toosupport silinmiş VM'ler. sunulan hello veri Merhaba geçen hafta ve her VM hello sayısı onaylanan istekleri, son erişim tarihi ve saati ve son kullanıcı için içerir.
- **Önerilen** -Vm'lerini yalnızca süresi VM erişimi destekler ancak için yapılandırılmamış. Yalnızca zaman VM erişim denetimi bu VM'ler için etkinleştirmenizi öneririz. Bkz: [yalnızca süresi VM erişimi etkinleştirmek](#enable-just-in-time-vm-access).
- **Öneri yok** -VM önerilen toobe neden olabilir nedenleri şunlardır:
  - NSG - yalnızca zaman çözümü hello eksik bir NSG toobe yerinde gerektirir.
  - Klasik VM - Güvenlik Merkezi'nde yalnızca zaman VM erişim şu anda yalnızca Azure Resource Manager aracılığıyla dağıtılan VM'ler destekler. Klasik dağıtım hello yalnızca zaman çözümü tarafından desteklenmiyor.
  - Çözüm hello güvenlik ilkesinde hello abonelik veya kaynak grubu hello devre dışı zamanında Hello ya da bu hello VM genel IP eksik ve bir NSG yerinde yoksa diğer - bir VM bu kategorisindedir.

## <a name="configuring-a-just-in-time-access-policy"></a>Yalnızca bir yapılandırma saat erişim ilkesinde

tooselect hello tooenable istediğiniz sanal makineleri:

1. Merhaba üzerinde **saat VM erişimi hemen** dikey penceresinde, select hello **önerilen** sekmesi.

  ![Yalnızca süresi erişimi etkinleştir][3]

2. Altında **VM'ler**, hello VM'ler tooenable istediğinizi seçin. Bir onay işareti sonraki tooa VM koyar.
3. Seçin **etkinleştirmek JIT vm'lerde**.
4. **Kaydet**’i seçin.

### <a name="default-ports"></a>Varsayılan bağlantı noktaları

Güvenlik Merkezi tam zamanında etkinleştirme önerir hello varsayılan bağlantı noktalarını görebilirsiniz.

1. Merhaba üzerinde **saat VM erişimi hemen** dikey penceresinde, select hello **önerilen** sekmesi.

  ![Varsayılan bağlantı noktalarını görüntüle][6]

2. Altında **VM'ler**, bir VM seçin. Bu bir onay işareti sonraki toohello VM ve açılır hello koyar **JIT VM erişim yapılandırması** dikey. Bu dikey penceresinde hello varsayılan bağlantı noktalarını görüntüler.

### <a name="add-ports"></a>Bağlantı noktaları ekleme

Merhaba gelen **JIT VM erişim yapılandırması** dikey penceresinde de ekleyebilir ve tooenable hello yalnızca zaman çözümü istediğiniz yeni bir bağlantı noktası yapılandırın.

1. Merhaba üzerinde **JIT VM erişim yapılandırması** dikey penceresinde, select **Ekle**. Merhaba açılır **Ekle bağlantı noktası yapılandırmasını** dikey.

  ![Bağlantı noktası yapılandırması][7]

2. Üzerinde **Ekle bağlantı noktası yapılandırmasını** dikey penceresinde hello kaynak IP'leri ve en fazla istek süresi izin verilen bağlantı noktası, protokol türü belirleyin.

  Kaynak IP izin onaylanmış bir istek üzerine hello IP aralıkları izin verilen tooget erişimi verilir.

  En fazla istek süresi belirli bir bağlantı noktasını açılabilir hello en uzun süre penceredir.

3. **Tamam**’ı seçin.

## <a name="requesting-access-tooa-vm"></a>İstekte bulunan erişim tooa VM

toorequest erişim tooa VM:

1. Merhaba üzerinde **saat VM erişimi hemen** dikey penceresinde, select hello **yapılandırıldı** sekmesi.
2. Altında **VM'ler**, hello VM'ler tooenable erişim istediğinizi seçin. Bir onay işareti sonraki tooa VM koyar.
3. Seçin **erişim isteği**. Merhaba açılır **erişim isteği** dikey.

  ![İstek erişim tooa VM][4]

4. Merhaba üzerinde **erişim isteği** dikey penceresinde, yapılandırmanız için her VM hello bağlantı noktaları tooopen hello bağlantı noktası hello kaynak IP yanı sıra hangi hello için bağlantı noktası açıldığında tooand hello zaman penceresi açılır. Yalnızca zaman İlkesi'nde hello yapılandırılmış olan erişim yalnızca toohello bağlantı noktaları isteyebilir. Her bağlantı noktası yalnızca zaman İlkesi'nde hello türetilmiş bir maksimum izin verilen süre içeriyor.
5. Seçin **bağlantı noktalarını açmak**.

## <a name="editing-a-just-in-time-access-policy"></a>Yalnızca bir düzenleme zaman erişim ilkesinde

VM'in ekleyerek ve o VM için yeni bir bağlantı noktası tooopen yapılandırma yalnızca zaman ilkesinde varolan değiştirebilir veya başka bir parametre değiştirerek ilgili tooan zaten bağlantı noktası korumalı.

İçinde yalnızca bir VM zaman İlkesi'nde hello varolan tooedit sipariş **yapılandırıldı** sekmesi kullanılır:

1. Altında **VM'ler**, VM tooadd hello üç nokta hello satır içinde o VM için tıklayarak bir bağlantı noktası tooby seçin. Bir menüdeki açılır.
2. Seçin **Düzenle** hello menüsünde. Merhaba açılır **JIT VM erişim yapılandırması** dikey.

  ![İlkeyi Düzenle][8]

3. Merhaba üzerinde **JIT VM erişim yapılandırması** dikey penceresinde, bağlantı noktası üzerinde tıklayarak ya da zaten korumalı bir bağlantı noktasının hello mevcut ayarları düzenleyebilirsiniz veya seçebilirsiniz **Ekle**. Merhaba açılır **Ekle bağlantı noktası yapılandırmasını** dikey.

  ![Bir bağlantı noktası ekleme][7]

4. Üzerinde **Ekle bağlantı noktası yapılandırmasını** dikey penceresinde hello bağlantı noktası, protokol türü, izin verilen kaynak IP'leri ve en fazla istek süresi tanımlayın.
5. **Tamam**’ı seçin.
6. **Kaydet**’i seçin.

## <a name="auditing-just-in-time-access-activity"></a>Yalnızca zaman erişim etkinliğinde denetleme

Günlük arama kullanarak VM etkinlikleri Öngörüler elde edebilirsiniz. tooview günlükleri:

1. Merhaba üzerinde **saat VM erişimi hemen** dikey penceresinde, select hello **yapılandırıldı** sekmesi.
2. Altında **VM'ler**, o VM için hello üç nokta hello satır içinde tıklayarak hakkında VM tooview bilgileri seçin. Bir menüdeki açılır.
3. Seçin **etkinlik günlüğü** hello menüsünde. Merhaba açılır **etkinlik günlüğü** dikey.

![Etkinlik günlüğü seçin][9]

Merhaba **etkinlik günlüğü** dikey önceki işlem saati, tarih ve abonelik ile birlikte bu VM için filtre uygulanmış bir görünümünü sağlar.

![Etkinlik Günlüğü Görüntüle][5]

Seçerek hello günlük bilgilerini indirebilirsiniz **toodownload CSV olarak tüm hello öğeleri burayı**.

Merhaba filtreleri değiştirmek ve seçin **Uygula** toocreate arama ve günlük.

## <a name="using-just-in-time-vm-access-via-powershell"></a>Tam zamanında PowerShell aracılığıyla VM erişim kullanma

PowerShell aracılığıyla zaman çözümde hemen sipariş toouse hello içinde hello olduğundan emin olun [son](/powershell/azure/install-azurerm-ps) Azure PowerShell sürümü.
Bunu yaptığınızda tooinstall hello gereksinim [son](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Güvenlik Merkezi'nden hello PowerShell Galerisi.

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>Yalnızca bir yapılandırma bir VM için zaman İlkesi

tooconfigure bir yalnızca belirli bir VM'de zaman ilkesinde toorun bu komut PowerShell oturumunuzda ihtiyacınız: Set-ASCJITAccessPolicy.
Merhaba cmdlet belgeleri toolearn daha fazla izleyin.

### <a name="requesting-access-tooa-vm"></a>İstekte bulunan erişim tooa VM

tooaccess ile korunan belirli bir VM'yi Merhaba yalnızca zaman çözümde, PowerShell oturumunuzda bu komut toorun gerekir: çağırma ASCJITAccess.
Merhaba cmdlet belgeleri toolearn daha fazla izleyin.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl tam zamanında VM erişim Güvenlik Merkezi yardımcı olur erişim tooyour Azure denetim öğrenilen sanal makineler.

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

- [Güvenlik ilkelerini ayarlama](security-center-policies.md) — öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
- [Güvenlik önerilerini yönetme](security-center-recommendations.md) — nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
- [Güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
- [Yönetme ve toosecurity uyarıları yanıt](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
- [İş ortağı çözümlerini izleme](security-center-partner-solutions.md) — nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
- [Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
- [Azure Güvenlik blogu](https://blogs.msdn.microsoft.com/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
