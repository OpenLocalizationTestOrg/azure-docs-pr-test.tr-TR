---
title: "VMware VM çoğaltma tooAzure (CSP programı) aaaMulti Kiracı desteği | Microsoft Docs"
description: "Nasıl toodeploy Azure Site Recovery çok kiracılı ortamı tooorchestrate çoğaltma, yük devretme ve kurtarma işlemi VMware sanal makineleri (VM'ler) tooAzure hello CSP program aracılığıyla hello Azure portal kullanarak şirket içi açıklar"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 9be555c9a438f66e6d3dfcdc9f507a84763846d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-tooazure-through-csp"></a>VMware sanal makineleri tooAzure CSP üzerinden çoğaltmak için Azure Site Recovery çok kiracılı desteği

Azure Site Recovery Kiracı abonelikler için çok kiracılı ortamlarda destekler. Oluşturulan ve hello Microsoft bulut çözümü sağlayıcısı (CSP) programı aracılığıyla yönetilen Kiracı abonelikler için çoklu kiracı de destekler. Bu makalede, uygulamayı ve yönetmeyi çok kiracılı VMware Azure senaryoları için Başlangıç Kılavuzu ayrıntıları verilmektedir. Ayrıca, oluşturma ve CSP Kiracı aboneliği yönetme de kapsar.

Bu kılavuz, VMware sanal makineleri tooAzure çoğaltılması hello varolan belgelerindeki yoğun olarak çizer. Daha fazla bilgi için bkz: [çoğaltmak VMware sanal makineleri tooAzure Site Recovery ile](site-recovery-vmware-to-azure.md).

## <a name="multi-tenant-environments"></a>Çok kiracılı ortamlarda
Üç ana çok kiracılı modeli vardır:

* **Barındırma hizmetleri sağlayıcısı (HSP) paylaşılan**: hello ortağı hello fiziksel altyapı sahip olan ve paylaşılan kaynakları (vCenter, veri merkezleri, fiziksel depolama alanı ve benzeri) kullanan toohost birden çok kiracıya Vm'lerinde hello aynı altyapı. Merhaba Kiracı Self Servis bir çözüm olarak olağanüstü durum kurtarma sahip olabilir veya Hello ortağı olağanüstü durum kurtarma yönetim yönetilen bir hizmet olarak sağlayabilir.

* **Barındırma hizmeti sağlayıcısı ayrılmış**: hello ortak sahibi hello fiziksel altyapı ancak özel kaynakları (birden çok Vcenter, fiziksel datastores vb.) kullanan toohost her bir kiracının sanal makineleri ayrı bir altyapı. Merhaba Kiracı Self Servis bir çözüm olarak sahip olabilir veya Hello ortağı olağanüstü durum kurtarma yönetim yönetilen bir hizmet olarak sağlayabilir.

* **Hizmetler Sağlayıcısı (MSP) yönetilen**: hello müşteri hello sanal makineleri barındıran fiziksel altyapı hello sahip olan ve hello ortağı olağanüstü durum kurtarma etkinleştirme ve yönetimi sağlar.

## <a name="shared-hosting-multi-tenant-guidance"></a>Paylaşılan barındırma çok kiracılı Kılavuzu
Bu bölümde ayrıntılı hello paylaşılan barındırma senaryo kapsar. Merhaba diğer iki senaryo hello paylaşılan barındırma senaryo kümeleridir ve hello kullandıkları aynı ilkeleri. Merhaba hello paylaşılan barındırma Kılavuzu sonunda Hello farklar açıklanmaktadır.

Merhaba temel bir çok kiracılı senaryosunda tooisolate gereksinimdir çeşitli kiracılar hello. Bir kiracı mümkün tooobserve başka bir kiracı barındırılan olmamalıdır. İş ortağı tarafından yönetilen bir ortamda, bu gereksinim Burada, kritik olabilir bir Self Servis ortamında, olduğu gibi önemli değil. Bu kılavuz, Kiracı yalıtımı gerekli olduğunu varsayar.

Merhaba mimarisi diyagramı aşağıdaki hello sunulur:

![Bir vCenter ile paylaşılan HSP](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)  
**Bir vCenter paylaşılan barındırma senaryoyla**

Hello önceki diyagramda görüldüğü gibi her bir müşteri bir ayrı yönetim sunucusu vardır. Bu yapılandırma sınırları Kiracı tootenant özgü VM'ler erişmek ve Kiracı yalıtımı sağlar. Bir VMware sanal makinesi çoğaltma senaryo hello yapılandırma sunucusu toomanage hesapları toodiscover VM'ler kullanır ve aracıları yükleyin. Biz hello izleyin aynı ilkeler vCenter ile VM bulma kısıtlama hello eklenerek çok kiracılı ortamlar için erişim denetimi.

tüm duyarlı altyapı bilgileri (örneğin, erişim kimlik bilgileri) kalması gerektiğini belirlenmemiş tootenants hello veri yalıtımı gereksinim gerekir. Bu nedenle, hello management server'ın tüm bileşenleri hello özel hello ortağı denetiminde kalmasını öneririz. Merhaba yönetim sunucusu bileşenleri şunlardır:
* Yapılandırma sunucusu (CS)
* İşlem Sunucusu (PS)
* Ana hedef sunucusu (MT) 

Bir genişleme PS ayrıca hello ortağın altında denetimdir.

### <a name="every-cs-in-hello-multi-tenant-scenario-uses-two-accounts"></a>İki hesap hello çok kiracılı senaryoda her CS kullanır

- **vCenter erişim hesabı**: Bu hesap toodiscover Kiracı VM'ler kullanın. (Merhaba sonraki bölümde açıklandığı gibi) tooit atanan vCenter erişim izinleri vardır. toohelp yanlışlıkla erişim sızıntıları kaçınmak için iş ortakları hello Yapılandırma aracında bu kimlik bilgileri kendilerini girin öneririz.

- **Sanal makine erişim hesabı**: Bu hesap tooinstall hello mobility aracısının hello Kiracı sanal makineleri otomatik bir anında iletme kullanın. Genellikle, bir etki alanı hesabı bir kiracı tooa iş ortağı sağlayabilir veya alternatif olarak, hello ortağı doğrudan yönetebilir, olabilir. Bir kiracı tooshare hello ayrıntıları hello ortağıyla doğrudan değil isterseniz, isterse sınırlı süreli üzerinden tooenter hello kimlik bilgileri toohello CS erişmek veya, hello ortağın Yardımı ile mobility aracıları el ile yükleyin izin verilebilir.

### <a name="requirements-for-a-vcenter-access-account"></a>Bir vCenter erişim hesabı gereksinimleri

Hello önceki bölümünde belirtildiği gibi bir özel rolü atanmış tooit sahip bir hesap ile Merhaba CS yapılandırmanız gerekir. Merhaba rol ataması olmalıdır uygulanan toohello vCenter erişim hesabını her vCenter nesne ve toohello alt nesneleri yayılan değil. Erişim yayma yanlışlıkla erişim tooother nesneleri sağladığından bu yapılandırmayı Kiracı yalıtımı sağlar.

![Merhaba Propagate tooChild nesneleri seçeneği](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

Merhaba alternatif tooassign hello kullanıcı hesabı ve rol hello datacenter nesnede ve bunları toohello alt nesneleri yayar. Merhaba hesabı verin bir *erişim yok* rol erişilemez tooa belirli Kiracı olması gereken her nesnenin (örneğin, diğer kiracılar VM). Bu yapılandırma sıkıcı ve her yeni alt nesne da otomatik olarak hello üst öğeden devralındı erişim izni olduğundan yanlışlıkla erişim denetimleri gösterir. Bu nedenle, hello ilk yaklaşımı kullanmanızı öneririz.

Merhaba vCenter hesap erişim yordam aşağıdaki gibidir:

1. Önceden tanımlanmış hello kopyalayarak yeni bir rol oluşturmak *salt okunur* rolü ve bir kolay ad (örneğin, Azure_Site_Recovery, bu örnekte gösterildiği gibi) verin.

2. İzinleri toothis rol aşağıdaki hello ata:

    * **Veri deposu**: tahsis alanı, Gözat veri deposu, alt düzey dosya işlemleri, Kaldır dosyası, sanal makine dosyaları güncelleştirmesi

    * **Ağ**: ağ atama

    * **Kaynak**: Ata VM tooresource havuzu, geçiş VM gücü, VM gücü geçirme

    * **Görevleri**: görev, güncelleştirme görevi oluşturma

    * **Sanal makine**: 
        * Yapılandırma > tüm
        * Etkileşim > yanıt soru, cihaz bağlantısı, yapılandırma CD medyasından, yapılandırma disket ortamı, kapatma, açma, VMware araçları yükleme
        * Stok > oluşturma varolandan, yeni oluştur, kaydetme, kaydı
        * Sağlama > izin sanal makine indirme, izin sanal makine dosyaları karşıya yükleme
        * Anlık Görüntü Yönetimi > anlık görüntüleri kaldırma

    ![Merhaba rol Düzenle iletişim kutusu](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. Aşağıdaki gibi çeşitli nesneler için erişim düzeylerini toohello vCenter hesabı (Merhaba Kiracı CS kullanılır) atayın:

>| Nesne | Rol | Açıklamalar |
>| --- | --- | --- |
>| vCenter | Salt okunur | Yalnızca tooallow vCenter farklı nesneleri yönetmek için gereken erişim. Merhaba hesabı hiçbir zaman toobe tooa Kiracı sağlanan veya hello vcenter yönetim işlemleri için kullanılan olacaksa, bu izni kaldırabilirsiniz. |
>| Datacenter | Azure_Site_Recovery |  |
>| Konak ve konak kümesi | Azure_Site_Recovery | Böylece Kiracı sanal makineleri yük devretme öncesinde ve sonrasında yeniden çalışma yalnızca erişilebilir konağınız erişim hello nesne düzeyinde yeniden sağlar. |
>| Veri deposu ve veri deposu küme | Azure_Site_Recovery | Önceki aynıdır. |
>| Ağ | Azure_Site_Recovery |  |
>| Yönetim sunucusu | Azure_Site_Recovery | Merhaba CS makine dışında olduğunda erişim tooall bileşenleri (CS, PS ve MT) içerir. |
>| Kiracı VM'ler | Azure_Site_Recovery | Tüm yeni Kiracı VM'ler belirli bir kiracı aynı zamanda bu erişim alın veya bunlar hello Azure portal bulunabilirlik olmaz sağlar. |

Merhaba vCenter hesap erişim tamamlanmıştır. Bu adım hello minimum izinleri gereksinim toocomplete yeniden çalışma işlemlerini yerine getirir. Varolan ilkeleri ile bu erişim izinleri de kullanabilirsiniz. Yalnızca, varolan izinleri tooinclude rol izinleri ayarlama, 2. adımda daha önce ayrıntılı değiştirin.

toorestrict olağanüstü durum kurtarma işlemleri hello yük devretme durumu tamamlanana kadar (diğer bir deyişle, yeniden çalışma özellikleri olmayan), bir özel durum ile yordamdan önceki hello izleyin: hello atama yerine *Azure_Site_Recovery* rolü toohello vCenter erişim hesabı, Ata yalnızca bir *salt okunur* rol toothat hesabı. Bu izin kümesi VM çoğaltma ve yük devretme sağlar ve geri dönme izin vermez. İşlem önceki hello bir şey olduğu gibi kalır. tooensure Kiracı yalıtımını ve VM bulma kısıtlamak, her izni hello nesne düzeyinde yalnızca ve değil yayılan toochild nesneler hala atanır.

## <a name="other-multi-tenant-environments"></a>Diğer çok kiracılı ortamlarda

önceki bölümde açıklanan nasıl hello tooset paylaşılan bir barındırma çözümü için çok kiracılı ortamı kurma. Merhaba diğer iki ana ayrılmış barındırma ve yönetilen hizmet çözümdür. Bu çözümler için Hello mimarisi hello aşağıdaki bölümlerde açıklanmıştır.

### <a name="dedicated-hosting-solution"></a>Barındırma çözümü ayrılmış

Hello Aşağıdaki diyagramda gösterildiği gibi hello mimari adanmış bir barındırma çözümüne yalnızca Kiracı için her bir kiracının altyapı ayarlandığını farktır. Kiracılar ayrı Vcenter yalıtılmış olduğundan, hello barındırma sağlayıcısına hala paylaşılan barındırma için sağlanan hello CSP adımları izlemeniz gerekir, ancak tooworry Kiracı yalıtımı hakkında gerekli değildir. CSP Kurulum değişmeden kalır.

![Mimari paylaşılan hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)  
**Birden çok Vcenter ile ayrılmış barındırma senaryosu**

### <a name="managed-service-solution"></a>Yönetilen hizmet çözümü

Gösterildiği hello Aşağıdaki diyagramda, bir yönetilen hizmet çözümde hello mimari fark her bir kiracının altyapı ayrıca diğer kiracılar altyapısından ayrı fiziksel olmasıdır. Merhaba Kiracı hello altyapı sahip ve bir çözüm sağlayıcısı toomanage olağanüstü durum kurtarma istediğinde bu senaryo genellikle bulunmaktadır. Yeniden, kiracılar farklı altyapılar aracılığıyla fiziksel olarak yalıtılmış olduğundan, hello ortak paylaşılan barındırma için sağlanan toofollow hello CSP adımları gerekiyor ancak tooworry Kiracı yalıtımı hakkında gerekli değildir. CSP sağlama değişmeden kalır.

![Mimari paylaşılan hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)  
**Birden çok Vcenter hizmet senaryoyla yönetilen**

## <a name="csp-program-overview"></a>CSP program genel bakış
Merhaba [CSP program](https://partner.microsoft.com/en-US/cloud-solution-provider) Office 365, Enterprise Mobility Suite ve Microsoft Azure dahil olmak üzere tüm Microsoft bulut hizmetlerine iş ortaklarının sunduğu daha iyi birlikte hikayeleri destekler. CSP ile ortaklarımızın hello uçtan uca ilişki sahip müşteriler kendi ve hello birincil ilişki için bağlantı noktası olur. İş ortakları, müşteriler için Azure abonelikleri dağıtmak ve kendi katma değer, özelleştirilmiş teklifleri hello aboneliklerle birleştirin.

Azure Site Recovery ile iş ortakları, müşteriler CSP aracılığıyla doğrudan hello tam olağanüstü durum kurtarma çözümü yönetebilirsiniz. Ya da CSP tooset Site Recovery ortamları ayarlama kullanın ve müşterilerin kendi olağanüstü durum kurtarma gereksinimlerini Self Servis bir şekilde yönetmenize olanak tanır. Her iki durumda da, Site Recovery ve müşterileri arasında hello ilişkiler ortaklarıdır. İş ortakları ve müşteriler Site Recovery kullanımı için fatura hello müşteri ilişkileri hizmeti.

## <a name="create-and-manage-tenant-accounts"></a>Kiracı hesapları oluşturma ve yönetme

### <a name="step-0-prerequisite-check"></a>0. adım: Önkoşul denetimi

Merhaba VM Önkoşullar olan hello aynı hello açıklandığı gibi [Azure Site Recovery belgelerine](site-recovery-vmware-to-azure.md). Toplama toothose Önkoşullar, sahip hello yukarıda açıklanan erişim denetimlerin CSP aracılığıyla Kiracı Yönetimi ile devam etmeden önce. Her bir kiracı için hello Kiracı sanal makineleri ve iş ortağının vCenter ile iletişim kurabilen bir ayrı yönetim sunucusu oluşturun. İş ortağı hello erişim hakları toothis sunucusu vardır.

### <a name="step-1-create-a-tenant-account"></a>1. adım: bir kiracı hesabı oluşturma

1. Aracılığıyla [Microsoft Partner Center](https://partnercenter.microsoft.com/), tooyour CSP hesabında oturum açın. 
 
2. Merhaba üzerinde **Pano** menüsünde, select **müşteriler**.

    ![Merhaba Microsoft iş ortağı merkezi müşterileri bağlantı](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. Merhaba açar hello sayfasında, tıklatın **Ekle müşteri** düğmesi.

    ![Merhaba müşteri Ekle düğmesi](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. Merhaba üzerinde **yeni müşteri** sayfasında, hello Kiracı için hello hesap bilgileri ayrıntıları doldurun ve ardından **sonraki: abonelikleri**.

    ![Merhaba hesap bilgileri sayfası](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. Merhaba Hello abonelikleri Seçimi sayfasında, seçin **Microsoft Azure** onay kutusu. Diğer abonelikler şimdi veya herhangi bir anda ekleyebilirsiniz.

    ![Merhaba Microsoft Azure aboneliği onay kutusu](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. Merhaba üzerinde **gözden geçirme** sayfasında, hello Kiracı ayrıntıları onaylayın ve ardından **gönderme**.

    ![Merhaba İnceleme sayfası](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    Merhaba Kiracı hesabınızı oluşturduktan sonra bir onay sayfasına görünür, varsayılan hesap ve parola Bu abonelik için hello hello hello ayrıntılarını görüntüleme. 

7. Merhaba bilgileri kaydedin ve daha sonra gerektiği gibi hello Azure portalı oturum açma sayfası aracılığıyla hello parolayı değiştirin.  
 
    Bu bilgileri olduğu gibi hello Kiracı ile paylaşabilir veya oluşturabilir ve gerekirse ayrı bir hesap paylaşın.

### <a name="step-2-access-hello-tenant-account"></a>2. adım: Erişim hello Kiracı hesabı

Merhaba kiracının abonelik açıklandığı gibi Microsoft iş ortağı merkezi Panosu'nda hello erişebilirsiniz "1. adım: bir kiracı hesabı oluşturun." 

1. Toohello Git **müşteriler** sayfasında ve hello hello Kiracı hesabının adını tıklatın.

2. Merhaba üzerinde **abonelikleri** sayfa hello Kiracı hesabını, izleme hello mevcut hesabı abonelikleri ve daha fazla abonelik gerektiği gibi ekleyin. toomanage hello kiracının olağanüstü durum kurtarma işlemleri seçin **tüm kaynaklar (Azure portalı)**.

    ![Hello tüm kaynak bağlantı](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    Tıklatarak **tüm kaynakları** toohello kiracının Azure abonelikleri erişim sağlar. Merhaba hello Azure Active Directory bağlantısını tıklatarak erişim doğrulayabilirsiniz top hello Azure portal sağındaki.

    ![Azure Active Directory bağlantısı](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

Şimdi hello Kiracı hello Azure portal aracılığıyla ilişkin tüm site kurtarma işlemlerini gerçekleştirme ve hello olağanüstü durum kurtarma işlemlerini yönetebilirsiniz. tooaccess hello Kiracı aboneliği CSP ile yönetilen olağanüstü durum kurtarma için izleme hello önceden işlemi açıklanmıştır.

### <a name="step-3-deploy-resources-toohello-tenant-subscription"></a>3. adım: kaynakları toohello Kiracı aboneliği dağıtma
1. Hello Azure portal, bir kaynak grubu oluşturun ve sonra bir kurtarma Hizmetleri kasası hello normal işlem başına dağıtın. 
 
2. Merhaba kasa kayıt anahtarını indirin.

3. Merhaba Kiracı Hello CS hello kasa kayıt anahtarını kullanarak kaydedin.

4. Merhaba iki erişim hesapları'Hello kimlik bilgilerini girin: vCenter erişim hesabı ve VM erişim hesabı.

    ![Yönetici yapılandırması sunucu hesapları](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-toohello-recovery-services-vault"></a>4. adım: Kayıt Site Recovery altyapısı toohello kurtarma Hizmetleri kasası
1. İçinde Azure Portal'da, daha önce oluşturduğunuz hello kasası Merhaba, içinde kayıtlı hello vCenter server toohello CS kaydetme "3. adım: kaynakları toohello Kiracı aboneliği dağıtın." Merhaba vCenter erişim hesabı bu amaçla kullanın.
2. Merhaba "Altyapıyı Hazırlama" işlem hello normal işlem başına Site Recovery için Son'u tıklatın.
3. Merhaba VM'ler çoğaltılan hazır toobe sunulmuştur. Yalnızca hello kiracının sanal makineleri üzerinde hello görüntülendiğini doğrulayın **sanal makine Seç** dikey penceresinde hello altında **çoğaltmak** seçeneği.

    ![Kiracı VM'ler listede hello Select virtual machines dikey penceresi](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-toohello-subscription"></a>5. adım: Kiracı erişim toohello abonelik atayın.

Self Servis olağanüstü durum kurtarma için hello 6. adımında açıklandığı gibi hello hesap ayrıntıları toohello Kiracı yapılandırmayı sağlar. "1. adım: bir kiracı hesap oluşturmak" bölümü. Merhaba olağanüstü durum kurtarma altyapıyı Hello ortak ayarlar sonra bu eylemi gerçekleştirin. Yönetilen veya Self Servis Hello olağanüstü durum kurtarma türü olup olmadığını belirtir, iş ortakları hello CSP Portalı aracılığıyla Kiracı aboneliklerine erişmeniz gerekir. Bunlar, iş ortağı şirkete ait hello kasasını oluşturup ve altyapı toohello Kiracı aboneliklerine kaydedin.

İş ortakları, hello aşağıdakileri yaparak hello CSP Portalı aracılığıyla yeni bir kullanıcı toohello Kiracı aboneliği de ekleyebilirsiniz:

1. Toohello kiracının CSP aboneliği sayfasına gidin ve ardından hello seçin **kullanıcılar ve lisansları** seçeneği.

    ![Kiracı'nın CSP aboneliği sayfasına hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    Artık hello ilgili ayrıntıları girerek ve izinleri seçerek veya bir CSV dosyasındaki kullanıcı hello listesi yükleyerek yeni bir kullanıcı oluşturabilirsiniz.

2. Yeni bir kullanıcı oluşturduktan sonra toohello Azure portal ve ardından hello dön **abonelik** dikey penceresinde, select hello ilgili abonelik.

3. Açılan hello dikey penceresinde, seçin **erişim denetimi (IAM)**ve ardından **Ekle** tooadd hello ilgili erişim düzeyine sahip bir kullanıcı.      
    Merhaba CSP Portalı aracılığıyla oluşturulan hello kullanıcılar otomatik olarak bir erişim düzeyi tıklattığınızda, açılan hello dikey penceresinde görüntülenir.

    ![Kullanıcı ekleme](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    Yönetim işlemlerinin çoğu için hello *katkıda bulunan* rolüdür yeterli. Bu erişim düzeyi kullanıcılarla bir abonelikte erişim düzeylerini değiştirme dışında her şeyi yapabilir (kendisi için *sahibi*-düzeyinde erişim gereklidir). Merhaba erişim düzeyleri gerektiği gibi ince ayar yapabilirsiniz.
