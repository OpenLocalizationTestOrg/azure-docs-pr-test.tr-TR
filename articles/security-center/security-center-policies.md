---
title: "Azure Güvenlik Merkezi'nde güvenlik ilkelerini aaaSet | Microsoft Docs"
description: "Bu belge, Azure Güvenlik Merkezi'nde güvenlik ilkelerini tooconfigure yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama
Bu belge, Güvenlik Merkezi'nde güvenlik ilkelerini tooconfigure bu görevi hello gerekli adımları tooperform arasında göstererek yardımcı olur.

>[!NOTE] 
>Güvenlik Merkezi erken Haziran 2017'den itibaren hello Microsoft İzleme Aracısı toocollect ve depolama verileri kullanır. Bkz: [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md) toolearn daha fazla. Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.
>

## <a name="what-are-security-policies"></a>Güvenlik ilkeleri nedir?
Bir güvenlik ilkesi belirtilen hello içindeki kaynaklar için önerilen denetimleri hello kümesini tanımlayan abonelik. Güvenlik Merkezi'nde, Azure aboneliklerinize tooyour şirketinizin güvenlik gereksinimlerine veya uygulamaların hello türü veya hello her Abonelikteki verilerin duyarlılığına göre ilkeleri tanımlar.

Örneğin, geliştirme veya test için kullanılan kaynaklar, üretim uygulamaları için kullanılan kaynaklardan farklı güvenlik gereksinimlerine sahip olabilir. Benzer şekilde, kişisel bilgiler gibi düzenlenen veriler kullanan uygulamalar daha yüksek bir güvenlik düzeyi gerektirebilir. Azure Güvenlik Merkezi sürücü güvenlik önerileri ve olası güvenlik açıklarını tanımlamanıza ve tehdit risklerini azaltmanıza izleme toohelp etkin güvenlik ilkeleri. Okuma [Azure Güvenlik Merkezi planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md) nasıl toodetermine hello seçeneği, hakkında daha fazla bilgi için uygun için.

## <a name="set-security-policies"></a>Güvenlik ilkeleri ayarlama
Her bir abonelik için güvenlik ilkeleri yapılandırabilirsiniz. bir güvenlik ilkesi toomodify sahibi veya katkıda bu aboneliğin olması gerekir. Toohello Azure portalında oturum açın ve Güvenlik Merkezi'nde tooconfigure güvenlik ilkelerinin adımları başarılı hello izleyin:

1. Merhaba tıklatın **İlkesi** döşeme hello Güvenlik Merkezi panosunda.
2. Açılan hello güvenlik ilkesi dikey penceresinde, tooenable hello güvenlik ilkesi istediğiniz hello aboneliği seçin.

    ![İlke tanımlama](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. Merhaba **Güvenlik İlkesi** dikey penceresinde seçili hello abonelik için bir seçenek kümesini açar. Bu dikey penceresinde Hello kullanılabilir seçenekler şunlardır:

   * **Önleme İlkesi**: Bu seçenek tooconfigure ilkeleri abonelik başına kullanın.  
   * **E-posta bildirimi**: hello ilk günlük oluşması bir uyarı ve yüksek öneme sahip uyarılar için bu seçeneği tooconfigure gönderilen bir e-posta bildirimi kullanın. E-posta tercihleri yalnızca abonelik ilkeleri için yapılandırılabilir. Okuma [Azure Güvenlik Merkezi'nde güvenlik iletişim ayrıntılarını sağlamak](security-center-provide-security-contact-details.md) hakkında daha fazla bilgi için tooconfigure bir e-posta bildirimi.
   * **Fiyatlandırma katmanı**: Bu seçenek tooupgrade hello fiyatlandırma katmanı seçimi kullanın. Bkz: [Güvenlik Merkezi fiyatlandırma](security-center-pricing.md) toolearn seçenekleri fiyatlandırma hakkında daha fazla bilgi.
4. **Sanal makinelerden veri toplama** seçeneğinin **Açık** olduğundan emin olun. Bu seçenek hello Microsoft Monitoring Agent'ı kullanarak mevcut ve yeni kaynaklar için otomatik günlük koleksiyonunu etkinleştirir – aynı aracı hello Operations Management Suite ve günlük analizi hizmeti tarafından kullanılan hello budur. Bu Aracıdan toplanan verileri Azure aboneliğinizle ilişkili var olan bir günlük analizi çalışma alanları veya yeni bir çalışma alanları hello VM, hesap hello Coğrafya alma depolanır.

5. Merhaba, **Güvenlik İlkesi** dikey penceresinde tıklatın **önleme İlkesi** toosee hello kullanılabilir seçenekler. Tıklatın **üzerinde** Bu abonelik için uygun olan tooenable hello güvenlik önerileri.

    ![Merhaba güvenlik ilkelerini seçme](./media/security-center-policies/security-center-policies-fig7.png)

Aşağıdaki tablonun başvuru toounderstand olarak hello her seçeneğini kullanın:

| İlke | Durum açık olduğunda |
| --- | --- |
| Sistem güncelleştirmeleri |Windows Update veya Windows Server Update Services kaynağından kullanılabilir güvenlik güncelleştirmelerinin ve kritik güncelleştirmelerin günlük listesini alır. Merhaba alınan listesi, sanal makine için yapılandırılmış ve hello eksik güncelleştirmelerin uygulanmasını önerir hello hizmete bağlı. Linux sistemleri için kullanılabilir güncelleştirmeleri hello distro tarafından sağlanan bir paket yönetim sistemi toodetermine paketleri hello İlkesi kullanır. Ayrıca, [Azure Cloud Services](../cloud-services/cloud-services-how-to-configure.md) sanal makinelerinden güvenlik güncelleştirmelerini ve kritik güncelleştirmeleri denetler. |
| İşletim sistemi güvenlik açıkları |Merhaba sanal makine savunmasız tooattack yapabilir işletim sistemi yapılandırmalarını günlük toodetermine sorunları analiz eder. Hello ilkesi yapılandırma değişiklikleri tooaddress açıklarından de önerir. Merhaba bkz [önerilen temel kurallar listesi](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) izlenmekte olan hello belirli yapılandırmalar hakkında daha fazla bilgi. (Şu an için Windows Server 2016 tam olarak desteklenmemektedir.) |
| Uç nokta koruması |Tüm Windows sanal toohelp tanımlamak ve virüsler, casus yazılım ve diğer kötü amaçlı yazılım kaldırma makineler için sağlanan uç nokta koruma toobe önerir. |
| Disk şifrelemesi |Tüm sanal makineleri tooenhance bekleyen verilerin korunması konusunda disk şifrelemesi etkinleştirme önerir. |
| Ağ güvenlik grupları |Önerir [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) yapılandırılmış toocontrol gelen ve giden trafiği ortak uç noktaları sahip tooVMs. Aksi belirtilmediği sürece bir alt ağ için yapılandırılan ağ güvenlik grupları tüm sanal makine ağ arabirimleri tarafından devralınır. Ayrıca bir ağ güvenlik grubu yapılandırıldığını toochecking, bu ilkeyi gelen trafiğe izin veren gelen güvenlik kuralları tooidentify kuralları değerlendirir. |
| Web uygulaması güvenlik duvarı |Merhaba aşağıdaki doğru olduğunda bir web uygulaması güvenlik duvarı sanal makinelerde sağlanmasını önerir: </br></br>[Örnek düzeyinde ortak IP](../virtual-network/virtual-networks-instance-level-public-ip.md) (ILPIP) kullanıldığında ve hello hello ilişkilendirilmiş ağ güvenlik grubu için gelen güvenlik kuralları olan yapılandırılmış tooallow erişim tooport 80/443'tür.</br></br>Yük dengeli IP kullanılır ve Yük Dengeleme hello ilişkili ve gelen ağ adresi çevirisi (NAT) kuralları yapılandırılmış tooallow erişim tooport 80/443'tür. (Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](../load-balancer/load-balancer-arm.md). |
| Yeni nesil güvenlik duvarı |Ağ korumalarını Azure’da yerleşik olan ağ güvenlik gruplarının ötesine genişletir. Güvenlik Merkezi, yeni nesil güvenlik duvarı önerilir ve sanal gereç tooprovision etkinleştirmek dağıtımları bulur. |
| SQL denetimi ve Tehdit algılama |Veritabanı erişimi tooAzure denetim için Uyumluluk etkinleştirilmeli ve tehdit algılama, araştırma amacıyla da Gelişmiş olduğunu önerir. |
| SQL Şifrelemesi |Azure SQL Veritabanınız, ilişkili yedeklemeler ve işlem günlük dosyaları için bekleyen şifrelemenin etkinleştirilmesini önerir. Verilerinizi ihlal edilse bile okunabilir olmayacaktır. |
| Güvenlik açığı değerlendirmesi |Sanal makinenize bir güvenlik açığı değerlendirme çözümü yüklemenizi önerir. |
| Depolama Şifrelemesi |Şu anda bu özellik Azure Blob'ları ve Dosyaları için kullanılabilir. Depolama Hizmeti Şifrelemesi’ni etkinleştirdikten sonra yalnızca yeni veriler şifrelenir ve bu depolama hesabında var olan dosyalar şifrelenmemiş olarak kalır. |
| JIT Ağ Erişimi |Tam zamanında etkinleştirilmişse, Güvenlik Merkezi bir NSG kuralı oluşturarak Azure VM'ler gelen trafiği tooyour kilitler. Merhaba bağlantı noktalarını seçin hello VM toowhich üzerinde gelen trafiği kilitli. Daha fazla bilgi için bkz. [Tam zamanında özelliğini kullanarak sanal makine erişimini yönetme](https://docs.microsoft.com/azure/security-center/security-center-just-in-time). |

Tüm seçenekleri yapılandırdıktan sonra tıklatın **Tamam** hello içinde **Güvenlik İlkesi** hello öneriler içerir ve ardından dikey **kaydetmek** hello içinde **güvenlik İlke** hello ilk ayarları içeren dikey.

> [!NOTE]
> Fiyatlandırma katmanı hello hello kaynak grubu düzeyinde için hala geçerlidir. Merhaba ziyaret eden daha fazla bilgi için [fiyatlandırma](https://azure.microsoft.com/pricing/details/security-center/) sayfası.
>
>

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, nasıl öğrenilen Azure Güvenlik Merkezi'nde güvenlik ilkelerini tooconfigure. Azure Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi planlama ve işlemler kılavuzu](security-center-planning-and-operations-guide.md). Bilgi nasıl tooplan ve hello tasarım konuları tooadopt Azure Güvenlik Merkezi anladığınızdan emin olun.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md). Nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md). Bilgi nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md). Nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi SSS](security-center-faq.md). Merhaba Hizmeti'ni kullanma hakkında sık sorulan soruları bulabilirsiniz.
* [Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/). Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulun.
