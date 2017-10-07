---
title: "Klasik tooAzure Resource Manager Iaas kaynaklardan geçişinde aaaPlanning | Microsoft Docs"
description: "Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini planlama"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 7574122d951119db4991187945739b190ef14995
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini planlama
Azure Resource Manager birçok harika özellikler sunar, ancak emin şeyler sorunsuz, geçiş gezisine toomake çıkışı kritik tooplan var. Planlama zaman harcama geçiş etkinliklerini yürütülürken sorunlarla değil olduğunu güvence altına alır.

> [!NOTE]
> yönergeleri izleyerek hello yoğun revizyonlarınız tooby hello Azure Müşteri danışma ekibi ve müşterilerle geçirme büyük ortamlarda üzerinde çalışan bulut çözümü mimarları oluştu. Bu nedenle bu belgeyi başarı yeni desenler ortaya çıkan gibi bunu denetimden geri zaman tootime toosee herhangi bir yeni önerimiz varsa güncelleştirilmiş tooget devam eder.

Merhaba geçiş gezisine dört genel aşamaları şunlardır:<br>

![Yükseltme aşamaları](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>Planlama

### <a name="technical-considerations-and-tradeoffs"></a>Teknik konuları ve bileşim

Teknik gereksinimleri boyutu, coğrafyalara ve işletimsel yöntemler bağlı olarak, tooconsider isteyebilirsiniz:

1. Neden Azure Resource Manager, kuruluşunuz için istendiğini?  Bir geçiş için hello iş nedenleri nelerdir?
2. Merhaba teknik nedenlerle Azure Resource Manager nelerdir?  Hangi (varsa) ek Azure Hizmetleri gibi tooleverage istiyorsunuz?
3. Hangi uygulama (veya sanal makineler kümesi) hello geçişte dahil edildi?
4. Hangi senaryoları ile Merhaba geçiş API destekleniyor mu?  Gözden geçirme hello [desteklenmeyen özellikler ve yapılandırmalar](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#unsupported-features-and-configurations).
5. İşletimsel ekipleriniz artık hem Klasik hem de Azure Resource Manager uygulamalar/VMs destekleyecek mi?
6. Nasıl (varsa) Azure Resource Manager VM Dağıtım, yönetim, izleme ve raporlama işlemleri değişiyor mu?  Dağıtım betikleri güncelleştirilmiş toobe gerekiyor mu?
7. Merhaba iletişimleri nedir tooalert Paydaşlar (son kullanıcılar, uygulama sahipleri ve altyapı sahipleri) planlıyor?
8. Merhaba ortamı Hello karmaşıklığına bağlı olarak, Merhaba uygulaması kullanılamıyor tooend kullanıcılar ve tooapplication sahipleri olduğu bir bakım süresine var olması gerekiyor mu?  Öyleyse, ne kadar süreyle?
9. Bilgili ve Azure Kaynak Yöneticisi'nde yeterli hello eğitim planı tooensure Paydaşlar nedir?
10. Merhaba program yönetimi veya hello geçiş için proje yönetim planı nedir?
11. Ne hello zaman çizelgelerini hello Azure Resource Manager geçiş ve diğer teknoloji yol haritalarına ilişkilidir?  Bunlar en iyi şekilde hizalanmış mı?

### <a name="patterns-of-success"></a>Başarı desenleri

Başarılı müşteriler burada hello önceki soruları ele alınan, belgelenen kapsamındadır ve plan ayrıntılı.  Geniş çapta iletildiğinden toosponsors ve Paydaşlar Hello geçiş planlarını olduğundan emin olun.  Geçiş seçenekleri hakkında bilgi Donatı; Bu geçiş belge aşağıda kümesi aracılığıyla okuma kullanmamanız önerilir.

* [Klasik tooAzure Resource Manager Iaas kaynaklardan platform desteklenen geçişini genel bakış](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini planlama](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Klasik tooAzure Resource Manager PowerShell toomigrate Iaas kaynakları kullanın](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI toomigrate Iaas kaynaklarına Klasik tooAzure Kaynak Yöneticisi'ni kullanın](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini ile Yardım için topluluk araçları](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [En sık karşılaşılan geçiş hatalarını gözden geçirme](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Gözden geçirme hello en sık Klasik tooAzure Kaynak Yöneticisi geçirme Iaas kaynaklardan hakkında sorular](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>Tuzaklar tooavoid

- Hata tooplan.  Bu geçiş teknolojisi adımlardan Hello kanıtlanmış ve hello sonucu tahmin edilebilir.
- Desteklenen platform geçiş API hello varsayım tüm senaryoları için hesap. Okuma hello [desteklenmeyen özellikler ve yapılandırmalar](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#unsupported-features-and-configurations) toounderstand hangi senaryoları desteklenir.
- Olası uygulama kesinti son kullanıcılar için planlama değil.  Yeterli arabellek planlama tooadequately son kullanıcılar olası kullanılamaz uygulama zaman uyar.


## <a name="lab-test"></a>Laboratuvar Test

**Ortamınızı çoğaltabilir ve bir test geçişi yapın**
  > [!NOTE]
  > Resmi Microsoft Support tarafından desteklenmeyen bir topluluk katkıda bulunan aracı kullanarak mevcut ortamınızın tam çoğaltma yürütülür. Bu nedenle, bir **isteğe bağlı** adım ancak olduğu hello en iyi şekilde toofind üretim ortamınızı temas olmadan sorunları çıkışı. Topluluğa katkıda bulunan bir araç kullanarak bir seçenek değilse, hazırlama/doğrula/durdurma kuru Çalıştır öneri aşağıda hello hakkında okuyun.
  >

  Tam senaryonuz (işlem, ağ ve depolama) bir laboratuvar testi gerçekleştirme hello en iyi şekilde tooensure sorunsuz bir geçiş değil. Bu, olmanıza yardımcı olur:

  - Tamamen ayrı bir laboratuvar veya varolan bir üretim ortamı dışındaki tootest. Sürekli olarak geçirilebilir ve kalıcı olmayacak şekilde değiştirilebilir tamamen ayrı bir laboratuvar öneririz.  Merhaba gerçek abonelikleri betikleri toocollect/hydrate meta verileri aşağıda listelenmektedir.
  - Ayrı bir abonelik iyi bir fikir toocreate hello laboratuvarda olur. Merhaba hello Laboratuvar art arda bozulur ve ayrı bir sahip, yalıtılmış abonelik bir şey gerçek yanlışlıkla silinecek olduğunu hello olasılığını azaltır nedenidir.

  Bu, hello AsmMetadataParser aracı kullanılarak gerçekleştirilebilir. [Burada bu araç hakkında daha fazla bilgi](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

### <a name="patterns-of-success"></a>Başarı desenleri

Merhaba aşağıdaki hello büyük geçişler çoğunu bulunan sorunları oluştu. Bu kapsamlı bir liste değildir ve toohello başvurmalıdır [desteklenmeyen özellikler ve yapılandırmalar](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#unsupported-features-and-configurations) daha fazla ayrıntı için.  Bu teknik sorunlar yaşayabilirsiniz değil veya olabilir ancak bunu yaparsanız, geçiş işlemini denemeden önce bunları çözme daha sorunsuz bir deneyim garanti eder.

- **Prepare/doğrula/durdurma kuru Çalıştır yapmak** -hello en önemli adım tooensure Klasik tooAzure Resource Manager geçiş başarılı belki de budur. Merhaba geçiş API üç ana adım vardır: doğrulamak için hazırlama ve tamamlama. Doğrulamak Klasik ortamınızın hello durumu okuyamadı ve tüm sorunların bir sonuç döndürür. Ancak, bazı sorunlar hello Azure Kaynak Yöneticisi yığınında olabileceğinden doğrula her şeyi yakalamaz. Merhaba sonraki adımda geçiş işlemi, bu sorunları kullanıma hazırlama yardımcı olur. Hazırlama Klasik tooAzure Resource Manager meta verilerini hello ancak değil yürütme hello taşıma ve kaldırmaz veya hiçbir şey hello Klasik tarafı değiştirme taşıyın. Hello kuru Çalıştır hello geçişi hazırlama sonra durduruluyor içerir (**değil yürüten**) hello geçiş hazırlayın. Merhaba doğrula/hazırlama/durdurma kuru Çalıştır hedefidir toosee tüm hello meta verileri hello Azure Kaynak Yöneticisi yığınında inceleyerek, (*program aracılığıyla veya Portal*), her şeyin doğru şekilde geçirir olduğunu doğrulayın ve ile çalışma teknik sorunlar.  Kapalı kalma süresi için uygun planı yapabilmesi için Ayrıca, geçiş süresi bir fikir verir.  Bir doğrula/hazırlama/durdurma kullanıcı kapalı kalma süresi neden olmaz; Bu nedenle benzer tooapplication kullanım olur.
  - Merhaba öğelerden hello kuru çalıştırmadan önce Çözüldü toobe gerekir, ancak bunlar eksik, test kuru çalıştırma hazırlık adımları da güvenli bir şekilde temizler. Kurumsal geçiş sırasında biz güvenli ve çok değerli bir kaynak yolu tooensure geçiş hazırlığı hello kuru Çalıştır toobe buldunuz.
  - Ne zaman hazırlama çalışıyor, hello denetim düzlemi (Azure yönetim işlemlerini) herhangi bir değişiklik tooVM meta verileri doğrula/hazırlama/durdurma sırasında böylece hello tüm sanal ağ için kilitlenir.  Ancak Aksi durumda herhangi bir uygulama işlevini (RD, VM kullanımı, vb.) etkilenmeyecek.  Merhaba VM'ler kullanıcılarının hello kuru çalıştıran yürütülen bilmez.

- **Rota devreler ve VPN express**. Şu anda Express rota ağ geçitleri yetkilendirme bağlantılarla kapalı kalma süresi olmadan geçirilemez. Merhaba geçici çözüm için bkz: [geçirmek ExpressRoute bağlantı hattına ve hello Klasik toohello Resource Manager dağıtım modeli sanal ağlardan ilişkili](../../expressroute/expressroute-migration-classic-resource-manager.md).

- **VM uzantıları** -sanal makine uzantıları olası VM'ler çalıştıran hello büyük roadblocks toomigrating biri. Düzeltme VM uzantıları, çalınıyor 1-2 gün sürebilir, bu nedenle uygun şekilde planlamanız.  Çalışan bir Azure Aracısı çalışan Vm'lerinin gerekli tooreport geri VM uzantısı durumudur. Merhaba durumu kötü olarak çalışan VM için geliyorsa, bu geçiş durdurulur. Merhaba aracının kendisi değil toobe çalışma sırasını tooenable geçiş gerekir, ancak uzantıları üzerinde varsa VM, hem bir çalışma aracısı ve giden internet bağlantısı (DNS ile) İleri geçiş toomove gerekli olacağını sonra hello.
  - Bağlantı tooa DNS sunucusu geçiş sırasında Bgınfo sürüm 1 dışındaki tüm VM uzantıları kaybolursa. \* toofirst her geçiş hazırlamadan önce VM ve daha sonra yeniden eklenen geri toohello VM Azure Resource Manager geçişten sonra kaldırılması.  **Çalıştırmakta olan VM'ler için budur.**  Merhaba VM'ler deallocated durdurulmuşsa VM uzantıları kaldırılan toobe gerekmez.

  > [!NOTE]
  > İzleme edecek Azure tanılama ve Güvenlik Merkezi gibi birçok uzantıları kendilerini yeniden geçişten sonra bu nedenle bunları kaldırma bir sorun değildir.

  - Ayrıca, ağ güvenlik grupları olmadığından emin olun giden internet erişimi kısıtlama. Bu, bazı ağ güvenlik grupları yapılandırmalarla meydana gelebilir. Giden internet erişimi (ve DNS) VM uzantıları için gereken toobe geçirilen tooAzure Resource Manager.
  - Merhaba Bgınfo uzantısını iki sürümü vardır ve 1 ve 2 sürümlerinde denir.  

      - Merhaba VM hello Bgınfo sürüm 1 uzantısını kullanıyorsanız, bu uzantı olduğu gibi bırakabilirsiniz. Bu uzantı Hello geçiş API atlar. Merhaba Bgınfo uzantısını geçişten sonra eklenebilir.
      - Merhaba VM hello JSON tabanlı Bgınfo sürüm 2 uzantısını kullanıyorsanız, hello VM hello Azure portalı kullanılarak oluşturuldu. Merhaba geçişi API bu uzantı Kaynak Yöneticisi, hello Aracısı sağlanan çalıştığından ve giden internet erişimi (ve DNS) sahip hello geçiş tooAzure içerir.

  - **Düzeltme seçeneği 1**. Vm'leriniz erişim, çalışma DNS hizmeti ve Azure aracıları hello Vm'lerinde çalışan, tüm VM uzantıları hazırlama önce hello geçiş işleminin parçası olarak kaldırın giden internet olmaz biliyorsanız, hello VM uzantıları geçişten sonra yeniden yükleyin.
  - **Düzeltme seçeneği 2**. VM uzantıları hurdle çok büyük ise, başka bir seçenek tooshutdown ve ayırması olan geçişten önce tüm VM'ler. VM serbest hello geçirmek sonra bunları Azure Resource Manager yan hello üzerinde yeniden başlatın. Burada Hello avantaj VM uzantıları geçiş yapacağınız olmalıdır. Merhaba dezavantajı tüm genel sanal IP'ye kullanıma yönelik kaybolacak olduğundan (Bu, başlangıç olmayan olabilir), ve çok daha büyük etkisi üzerinde çalışan uygulamalar neden aşağı hello VM'ler açıkça kapanır.

    > [!NOTE]
    > Azure Güvenlik Merkezi ilke Geçirilmekte olan sanal makineleri çalıştıran hello karşı yapılandırdıysanız, hello Güvenlik İlkesi uzantıları kaldırmadan önce durduruldu toobe gerekir, aksi takdirde hello güvenlik izleme uzantısı otomatik olarak üzerinde yeniden yüklenecek hello sonra VM kaldırma.

- **Kullanılabilirlik kümeleri** - sanal ağ (vNet) toobe tooAzure Resource Manager geçişi, hello Klasik dağıtım (yani, bulut hizmeti) yer alan VM'ler tüm olmalıdır bir kullanılabilirlik kümesinde veya hello VM'ler herhangi bir kullanılabilirlik kümesi tümü olması gerekir. Merhaba bulut hizmetinde birden fazla kullanılabilirlik sahip Azure Resource Manager ile uyumlu değildir ve geçiş durdurulur.  Ayrıca, olamaz bazı sanal makineleri bir kullanılabilirlik kümesinde ve bazı sanal makineleri bir kullanılabilirlik kümesinde değil. tooresolve bunu tooremediate gerekir veya Bulut hizmetiniz sırasını yeniden ayarlaması.  Plan uygun şekilde gibi bu zaman alıcı olabilir.

- **Web/çalışan rolü dağıtımları** -web ve çalışan rolleri içeren Cloud Services tooAzure Resource Manager geçirilemiyor. geçiş başlamadan önce hello web/çalışan rolleri hello sanal ağdan kaldırılmalıdır.  Ayrıca bağlantılı tooan expressroute bağlantı hattı veya toomigrate hello kod toonewer PaaS uygulama (Bu tartışma hello bu belgenin kapsamında değildir) Hizmetleri toojust taşıma web/çalışan rolü örnekleri tooa ayrı Klasik sanal ağ buna tipik bir çözümdür. Merhaba eski durum dağıtmanız, yeni bir Klasik sanal ağ oluşturma, taşıma/hello web/çalışan rolleri toothat yeni sanal ağı yeniden dağıtın ve ardından taşınan hello sanal ağdan hello dağıtımları silin. Kod değişiklikleri gerekli. Merhaba yeni [sanal ağ eşlemesi](../../virtual-network/virtual-network-peering-overview.md) yetenek hello web/çalışan rolleri içeren kullanılan toopeer birlikte hello Klasik sanal ağı olabilir ve diğer sanal ağlarda hello hello olan sanal ağ gibi aynı Azure bölgesi geçirilen (**eşlenmiş sanal ağlar geçirilemez gibi sanal ağ geçişi tamamlandıktan sonra**), bu nedenle hello performans kaybı ve gecikme/bant genişliği cezaları ile aynı özelliklerinin sağlanması. Merhaba eklenmesi verilen [sanal ağ eşlemesi](../../virtual-network/virtual-network-peering-overview.md), web/çalışan rolü dağıtımları şimdi kolayca azaltılabilir ve hello geçiş tooAzure Resource Manager engelleme değil.

- **Azure Kaynak Yöneticisi kotaları** -Azure bölgeleri hem Klasik hem de Azure Resource Manager için ayrı kota sınırları vardır. Bir geçiş senaryosunda yeni donanım tüketilen değil olsa bile *(biz Klasik tooAzure Resource Manager mevcut VM'lerin takas etme)*, Azure Kaynak Yöneticisi kotaları yine de toobe önce yeterli kapasiteye sahip yerinde gerekir geçiş başlatabilirsiniz. Aşağıda, hello ana sınırları gördük sorunlara neden yer alır.  Açık bir kota destek bileti tooraise hello sınırlar.

    > [!NOTE]
    > Bu sınırlar içinde gerçekleştirilen toobe gerekir, geçerli ortamı toobe geçişi gibi aynı bölgede hello.
    >

    - Ağ Arabirimleri
    - Yük Dengeleyici
    - Genel IP'ler
    - Statik genel IP'ler
    - Çekirdek
    - Ağ Güvenlik Grupları
    - Yönlendirme Tabloları

    Azure PowerShell'in en son sürümünü hello komutlarıyla aşağıdaki hello kullanarak, geçerli Azure Kaynak Yöneticisi kotaları kontrol edebilirsiniz.

    **İşlem** *(çekirdek, kullanılabilirlik kümeleri)*

    ```powershell
    Get-AzureRmVMUsage -Location <azure-region>
    ```

    **Ağ** *(sanal ağlar, statik genel IP'ler, genel IP'ler, ağ güvenlik grupları, ağ arabirimleri, yük Dengeleyiciler, yol tablolarını)*

    ```powershell
    Get-AzureRmUsage /subscriptions/<subscription-id>/providers/Microsoft.Network/locations/<azure-region> -ApiVersion 2016-03-30 | Format-Table
    ```

    **Depolama** *(depolama hesabı)*

    ```powershell
    Get-AzureRmStorageUsage
    ```

- **Azure Resource Manager azaltma sınırları API** - (ör. yeterli büyüklükte bir ortamınız varsa > Merhaba varsayılan API azaltma sınırları yazmalar için isabet 400 bir VNET içindeki Vm'leri), (şu anda `1200 writes/hour`) Azure Kaynak Yöneticisi'nde. Geçiş işlemini başlatmadan önce aboneliğiniz için bu sınırı bir destek bileti tooincrease tetiklemelidir.


- **Sağlama zaman aşımına uğradı VM durumu** - VM hello durumunu `provisioning timed out`, bu ihtiyaçları toobe geçiş öncesi çözümlendi. Merhaba tek yolu toodo kapalı kalma süresi ile sağlamayı/hello VM, hello disk tutmak ve hello VM oluşturun (silme) sağlama işleminin tarafından budur.

- **RoleStateUnknown VM durumu** - son geçiş işlemindeki tooa `role state unknown` hata iletisi, inceleme hello portal kullanarak VM hello ve çalıştığından emin olun. Bu hata genellikle kaybolur, birkaç dakika sonra (düzeltme gerekli) sahibi ve geçici bir türü sırasında sanal makine genellikle sık görülen `start`, `stop`, `restart` işlemleri. **Önerilen yöntem:** birkaç dakika sonra tekrar geçiş işlemini yeniden deneyin.

- **Fabric kümesi yok** - bazı durumlarda, bazı sanal makineleri tek çeşitli nedenlerle geçirilemez. Bu bilinen durumların hello VM (Merhaba geçen hafta ya da bunu içinde) yakın zamanda oluşturulduğu ve tooland Azure Resource Manager iş yükleri için henüz donatılmış olmayan bir Azure küme oldu biridir.  Bildiren bir hata iletisiyle karşılaşırsınız `fabric cluster does not exist` ve hello VM geçirilemez. Merhaba küme yakında Azure Kaynak Yöneticisi etkin alırsınız gibi birkaç gün bekleyen genellikle belirli bu sorunu giderir. Ancak, hemen çözüm çok uzun`stop-deallocate` VM Merhaba, İleri geçirme işlemine devam etmek ve taşıdıktan sonra Azure Kaynak Yöneticisi'nde hello VM Başlat yedekleyin.

### <a name="pitfalls-tooavoid"></a>Tuzaklar tooavoid

- Kısayollar ele değil ve hello doğrula/hazırlama/durdurma kuru Çalıştır geçişler atlayabilirsiniz.
- En değilse, olası sorunları, hello doğrula/hazırlama/durdurma adımları sırasında belirir.

## <a name="migration"></a>Geçiş

### <a name="technical-considerations-and-tradeoffs"></a>Teknik konuları ve bileşim

Ortamınız ile ilgili bilinen sorunlar hello aracılığıyla çalışılan çünkü artık hazırsınız.

Merhaba gerçek geçişler için tooconsider isteyebilirsiniz:

1. Planlama ve öncelik artan hello sanal ağ (geçiş en küçük birim) zamanlayabilirsiniz.  Basit sanal ağlar ilk hello ve sanal ağlar hello daha fazla ile ilerlemeyi karmaşık.
2. Müşterilerin çoğu, üretim dışı ve üretim ortamlarını sahip olur.  Üretim son zamanlayın.
3. **(İSTEĞE BAĞLI)**  Beklenmeyen sorunlar çıkması durumunda bir bakım kapalı kalma arabellek bolca zamanlayın.
4. İle iletişim kurmasını ve sorunlar çıkması durumunda destek ekipleriniz hizalayın.

### <a name="patterns-of-success"></a>Başarı desenleri

Merhaba hello teknik Kılavuzu _Laboratuvar Test_ bölümü düşünülmesi gereken ve önceki tooa gerçek geçiş azaltıldığından.  Uygun testleri ile Merhaba geçiş gerçekten dışı bir olay değil.  Üretim ortamları için güvenilen bir Microsoft iş ortağı veya Microsoft Premier Hizmetleri gibi yararlı toohave ek destek olması olabilir.

### <a name="pitfalls-tooavoid"></a>Tuzaklar tooavoid

Tam olarak test sorunlara neden ve hello geçişte gecikme olabilir.  

## <a name="beyond-migration"></a>Geçiş dışında

### <a name="technical-considerations-and-tradeoffs"></a>Teknik konuları ve bileşim

Azure Kaynak Yöneticisi'nde artık olduğuna göre hello platform ekranı kaplamasını sağlayın.  Okuma hello [genel bakış Azure Kaynak Yöneticisi'nin](../../azure-resource-manager/resource-group-overview.md) çıkışı toofind başka avantajları hakkında.

Şeyler tooconsider:

- Diğer etkinlikleri ile Merhaba geçiş paketleme.  Müşterilerin çoğu, bir uygulama bakım penceresi için kabul et.  Bu nedenle, bu kapalı kalma süresi tooenable toouse isteyebilirsiniz, şifreleme ve geçiş diğer Azure Resource Manager yetenekleri gibi tooManaged diskler.
- Merhaba teknik ve iş nedenleri Azure kaynak yöneticisi için yeniden ziyaret; tooyour ortamı geçerli hello ek hizmetler yalnızca Azure Kaynak Yöneticisi kullanılabilir etkinleştirin.
- Ortamınızı PaaS hizmetleriyle modernize.

### <a name="patterns-of-success"></a>Başarı desenleri

Şimdi istediğiniz tooenable Azure Kaynak Yöneticisi'nde Hizmetleri amaca olabilir.  Birçok müşteri hello Azure ortamlarını çekici aşağıda bulabilirsiniz:

- [Rol tabanlı erişim denetimi](../../azure-resource-manager/resource-group-overview.md#access-control).
- [Daha kolay ve daha denetimli dağıtımı için Azure Resource Manager şablonları](../../azure-resource-manager/resource-group-overview.md#template-deployment).
- [Etiketleri](../../azure-resource-manager/resource-group-using-tags.md).
- [Etkinlik denetimi](../../azure-resource-manager/resource-group-audit.md)
- [Kaynak ilkeleri](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>Tuzaklar tooavoid

Bu Klasik tooAzure Resource Manager geçiş gezisine neden başlattığınız unutmayın.  Ne hello özgün iş nedenleri muydunuz? Merhaba iş neden elde?


## <a name="next-steps"></a>Sonraki adımlar

* [Klasik tooAzure Resource Manager Iaas kaynaklardan platform desteklenen geçişini genel bakış](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Klasik tooAzure Resource Manager PowerShell toomigrate Iaas kaynakları kullanın](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI toomigrate Iaas kaynaklarına Klasik tooAzure Kaynak Yöneticisi'ni kullanın](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini ile Yardım için topluluk araçları](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [En sık karşılaşılan geçiş hatalarını gözden geçirme](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Gözden geçirme hello en sık Klasik tooAzure Kaynak Yöneticisi geçirme Iaas kaynaklardan hakkında sorular](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
