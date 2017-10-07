---
title: bir SQL Server sanal makine aaaProvision | Microsoft Docs
description: "Oluşturabilir ve hello Portal kullanarak azure'da tooa SQL Server sanal makine bağlayabilirsiniz. Bu öğretici hello Resource Manager modunu kullanır."
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: 
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
experimental_id: a641df96-f27d-40
ms.openlocfilehash: aaad422d6ed47f5ca00b1ef484ac270a58e24f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Hello Azure Portal'ın SQL Server sanal makine sağlama
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

Bu uçtan uca öğretici nasıl toouse hello Azure Portal tooprovision SQL Server çalıştıran bir sanal makine gösterir.

Hello Azure sanal makine (VM) Galerisi, Microsoft SQL Server içeren birkaç görüntüyü içerir. Birkaç tıklama ile Merhaba galerideki SQL VM görüntüleri hello birini seçin ve Azure ortamınızda sağlayın.

Bu öğreticide şunları yapacaksınız:

* [Merhaba Galeriden bir SQL VM görüntüsü seçin](#select-a-sql-vm-image-from-the-gallery)
* [Yapılandırma ve hello VM oluşturma](#configure-the-vm)
* [Merhaba VM Uzak Masaüstü ile açma](#open-the-vm-with-remote-desktop)
* [TooSQL sunucu uzaktan bağlanma](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Merhaba Galeriden bir SQL VM görüntüsü seçin
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hesabınızı kullanarak.

   > [!NOTE]
   > Bir Azure hesabınız yoksa, [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)yi ziyaret edin.

2. Hello Azure portal, tıklatın **yeni**. Merhaba portal açar hello **yeni** dikey. Merhaba SQL Server VM kaynakları olan hello **işlem** hello Market grubunu.
3. Merhaba, **yeni** dikey penceresinde tıklatın **işlem** ve ardından **tümünü görmek**.
4. Merhaba, **filtre** metin kutusunda türü SQL Server ve hello ENTER tuşuna basın.

   ![Azure Virtual Machines Dikey Penceresi](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Merhaba kullanılabilir SQL Server görüntülerinin gözden geçirin. Her görüntü bir SQL Server sürümü ve işletim sistemi tanımlar. 
6. SQL Server 2016 SP1 Geliştirici Windows Server 2016 için Hello görüntüsünü seçin.

   > [!TIP]
   > Test amacıyla geliştirme için ücretsiz bir SQL Server tam özellikli bir sürümü olduğundan hello Geliştirici sürümü Bu öğreticide kullanılır. Merhaba VM çalıştıran yalnızca hello maliyetini ücret ödersiniz.

   > [!NOTE]
   > SQL VM görüntülerini hello lisanslama maliyetleri, SQL Server için dakika başına hello fiyatlandırma hello VM (Merhaba Geliştirici ve Express sürümleri hariç) oluşturmak, içine içerir. SQL Server Developer, geliştirme/test için (üretim için değil); SQL Express ise hafif iş yükleri (1 GB'tan küçük bellek, 10 GB'tan küçük depolama alanı) için ücretsizdir.
   > Başka bir seçenek toobring bilgisayarınızı-kendi-lisans (KLG) ve yalnızca hello VM için ödeme yoktur. Bu görüntü adlarının başına {BYOL} ön eki getirilir. Bu seçeneklerle ilgili daha fazla bilgi için bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).

7. **Dağıtım modeli seçin** altında, **Resource Manager**’ın seçili olduğunu doğrulayın. Resource Manager dağıtım modeli yeni sanal makineler için önerilen hello ' dir. **Oluştur**'a tıklayın.

    ![Resource Manager ile SQL VM oluşturma](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Merhaba VM yapılandırma
Bir SQL Server sanal makineyi yapılandırmak için beş dikey pencere vardır.

| Adım | Açıklama |
| --- | --- |
| **Temel Bilgiler** |[Temel ayarları yapılandırma](#1-configure-basic-settings) |
| **Boyut** |[Sanal makine boyutunu seçme](#2-choose-virtual-machine-size) |
| **Ayarlar** |[İsteğe bağlı özellikleri yapılandırma](#3-configure-optional-features) |
| **SQL Server ayarları** |[SQL Server ayarlarını yapılandırma](#4-configure-sql-server-settings) |
| **Özet** |[Gözden geçirme hello özeti](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Temel ayarları yapılandırma
Merhaba üzerinde **Temelleri** dikey penceresinde, aşağıdaki bilgilerle hello sağlayın:

* Benzersiz bir sanal makine **adı** girin.
* Belirtin bir **kullanıcı adı** hello VM hello yerel yönetici hesabı için. Bu hesap aynı zamanda toohello SQL Server eklenen **sysadmin** sabit sunucu rolü.
* Güçlü bir **parola** girin.
* Merhaba abonelik için doğru olduğundan emin olun, birden çok aboneliğiniz varsa, yeni VM hello.
* Merhaba, **kaynak grubu** kutusuna, yeni bir kaynak grubu için bir ad yazın. Alternatif olarak, var olan bir kaynak grubunu toouse tıklatın **var olanı kullan**. Bir kaynak grubu, Azure’daki ilgili kaynakların bir koleksiyonudur (sanal makineler, depolama hesapları, sanal ağlar, vb.).
  
  > [!NOTE]
  > Yalnızca Azure’daki SQL Server dağıtımlarını test ediyor veya öğreniyorsanız, yeni bir kaynak grubu kullanmak faydalıdır. Test işleminizi tamamladıktan sonra hello kaynak grubu tooautomatically delete hello VM ve bu kaynak grubu ile ilişkili tüm kaynakları silin. Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a Genel Bakış](../../../azure-resource-manager/resource-group-overview.md).
  > 
  > 
* Bu dağıtım için bir **Konum** seçin.
* Tıklatın **Tamam** toosave hello ayarları.
  
    ![SQL Temel Bilgileri Dikey Penceresi](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. Sanal makine boyutunu seçme
Merhaba üzerinde **boyutu** adım, bir sanal makine boyutu hello seçin **bir boyutu seçin** dikey. Merhaba dikey ilk başta seçtiğiniz hello görüntüde göre önerilen makine boyutlarını görüntüler.

> [!IMPORTANT]
> Merhaba tahmini aylık maliyeti hello üzerinde görüntülenen **bir boyutu seçin** dikey penceresinde, SQL Server Lisans maliyetleri içermez. Bu tahmini aylık maliyeti hello VM başına hello maliyetidir. Merhaba Express ve geliştirici SQL Server sürümleri için bu hello toplam tahmini maliyet olur. Merhaba diğer sürümleri için bkz: [Windows sanal makineler fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) ve hedef sürümünüz SQL Server'ın seçin. Ayrıca bkz. hello [Kılavuzu SQL Server Azure VM'ler için fiyatlandırma](virtual-machines-windows-sql-server-pricing-guidance.md).

![SQL VM Boyut Seçenekleri](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Üretim iş yükleri için, [Premium Storage](../../../storage/storage-premium-storage.md)’ı destekleyen bir sanal makine boyutu seçilmesini öneriyoruz. Bu düzeyde performans gerekli değil, hello kullanın. **tüm görüntüle** tüm makine boyutu seçeneklerini gösteren düğmesi. Örneğin, geliştirme veya test ortamı için daha küçük bir makine boyutu kullanabilirsiniz.

> [!NOTE]
> Sanal makine boyutları hakkında daha fazla bilgi için bkz. [Sanal makineler için boyutlar](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). SQL Server VM boyutları hakkında dikkat edilecek noktalar için bkz. [Azure Virtual Machines’de SQL Server için performans en iyi uygulamaları](virtual-machines-windows-sql-performance.md).

Makine boyutunuzu seçin ve ardından **Seç**’e tıklayın.

## <a name="3-configure-optional-features"></a>3. İsteğe bağlı özellikleri yapılandırma
Merhaba üzerinde **ayarları** dikey penceresinde, Azure depolama, ağ ve hello sanal makine için izlemeyi yapılandırın.

* **Depolama** altında, Standart veya Premium (SSD) olarak **Disk türü**nü belirtin. Premium Storage üretim iş yükleri için önerilir.

> [!NOTE]
> Premium Storage’ı desteklemeyen bir makine boyutu için Premium (SSD) seçerseniz, makine boyutunuz otomatik olarak değişir.  
> 
> 

* Altında **depolama hesabı**, hello otomatik olarak sağlanan depolama hesabı adını kabul edebilirsiniz. Ayrıca tıklatabilirsiniz **depolama hesabı** toochoose var olan bir hesap ve hello hesap türünü yapılandırabilirsiniz. Varsayılan olarak, Azure yerel olarak yedekli depolama ile yeni bir depolama hesabı oluşturur. Depolama seçenekleri hakkında daha fazla bilgi için bkz. [Azure Storage çoğaltma](../../../storage/storage-redundancy.md).
* Altında **ağ**, otomatik olarak doldurulur hello değerlerini kabul edebilir. Her bir özelliğe de tıklatabilirsiniz toomanually yapılandırma hello **sanal ağ**, **alt**, **genel IP adresi**, ve **ağ güvenlik grubu**. Bu öğreticinin Hello amaçları hello varsayılan değerleri koruyun.
* Azure etkinleştirir **izleme** aynı depolama hesabındaki hello VM için belirlenen hello ile varsayılan ayar. Burada bu ayarları değiştirebilirsiniz.
* **Kullanılabilirlik kümesi** altında, bir kullanılabilirlik kümesi belirtin. Bu öğreticinin Hello amaçları doğrultusunda, seçtiğiniz **hiçbiri**. SQL AlwaysOn Kullanılabilirlik gruplarını tooset planlıyorsanız, hello kullanılabilirlik tooavoid yeniden oluşturma hello sanal makineyi yapılandırın.  Daha fazla bilgi için bkz: [Yönet hello sanal makinelerin kullanılabilirliğini](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Yapılandırma ayarlarını tamamladığınızda, **Tamam**’a tıklayın.

## <a name="4-configure-sql-server-settings"></a>4. SQL server ayarlarını yapılandırma
Merhaba üzerinde **SQL Server ayarları** dikey penceresinde, belirli ayarları ve SQL Server iyileştirmelerini yapılandırın. SQL Server için yapılandırabileceğiniz hello ayarları hello ayarları aşağıdaki içerir.

| Ayar |
| --- |
| [Bağlantı](#connectivity) |
| [Kimlik doğrulaması](#authentication) |
| [Depolama yapılandırması](#storage-configuration) |
| [Otomatik Düzeltme Eki Uygulama](#automated-patching) |
| [Otomatik Yedekleme](#automated-backup) |
| [Azure Anahtar Kasası Tümleştirmesi](#azure-key-vault-integration) |
| [R Hizmetleri](#r-services) |

### <a name="connectivity"></a>Bağlantı
Altında **SQL Bağlantısı**, hello türünü belirtin erişimi toohello SQL Server örneği bu VM'de istiyor. Bu öğreticinin Hello amaçları seçin **genel (internet)** makineler veya hizmetler tooallow bağlantıları tooSQL sunucu hello Internet. Bu seçenek ile Azure otomatik olarak hello güvenlik duvarı ve hello ağ güvenlik grubu tooallow trafiği 1433 bağlantı noktasını yapılandırır.  

![SQL Bağlantı Seçenekleri](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

Merhaba aracılığıyla tooconnect tooSQL sunucu Internet da etkinleştirmeniz gerekir hello sonraki bölümde açıklanan SQL Server kimlik.

> [!NOTE]
> Bu olası tooadd hello ağ iletişimleri tooyour SQL Server VM için daha fazla kısıtlama değil. Merhaba VM oluşturulduktan sonra düzenleme hello ağ güvenlik grubu tarafından daha fazla kısıtlama ekleyebilirsiniz. Daha fazla bilgi için bkz. [Ağ Güvenlik Grubu (NSG) nedir?](../../../virtual-network/virtual-networks-nsg.md)
> 
> 

Toonot etkinleştirmek bağlantıları toohello veritabanı altyapısı tercih ederseniz aracılığıyla Internet Merhaba, aşağıdaki seçenekleri şu hello birini seçin:

* **Yerel (yalnızca VM)** tooallow bağlantıları tooSQL sunucusundan yalnızca hello VM içinde.
* **Özel (sanal ağ dahilinde)** tooallow bağlantıları tooSQL sunucu makineler ve hizmetlerden Merhaba, aynı sanal ağ.

> [!NOTE]
> SQL Server Express edition için Hello sanal makine görüntüsü hello TCP/IP Protokolü otomatik olarak etkinleştirmez. Böyle bile hello ortak ve özel bağlantı seçenekleri. Express edition için SQL Server Configuration Manager çok kullanmalısınız[el ile Merhaba TCP/IP protokolünü etkinleştirin](#configure-sql-server-to-listen-on-the-tcp-protocol) VM hello oluşturduktan sonra.
> 
> 

Genel olarak, senaryonuzun izin verdiği hello en kısıtlayıcı bağlantıyı seçerek güvenliği geliştirin. Ancak tüm hello seçenekler ağ güvenlik grubu kuralları ve SQL/Windows kimlik doğrulaması ile güvenliği sağlanabilir.

**Bağlantı noktası** too1433 Varsayılanları. Farklı bir bağlantı noktası belirtebilirsiniz.
Daha fazla bilgi için bkz: [tooa SQL Server sanal makinesine (Resource Manager) bağlanma | Microsoft Azure](virtual-machines-windows-sql-connect.md).

### <a name="authentication"></a>Kimlik Doğrulaması
SQL Server Kimlik Doğrulaması gerekiyorsa, **SQL kimlik doğrulaması** altında **Etkinleştir**’e tıklayın.

![SQL Server Kimlik Doğrulaması](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Üzerinden tooaccess SQL Server planlıyorsanız Internet (diğer bir deyişle, hello genel bağlantı seçeneği), burada SQL kimlik doğrulamasını etkinleştirmelisiniz hello. Genel erişim toohello SQL Server, SQL kimlik doğrulaması hello kullanılmasını gerektirir.
> 
> 

SQL Server Kimlik Doğrulamasını etkinleştirirseniz, bir **Oturum açma adı** ve **parola** belirtin. Bu kullanıcı adı bir SQL Server kimlik doğrulaması oturum açma ve hello üyesi olarak yapılandırılmış **sysadmin** sabit sunucu rolü. Kimlik Doğrulama Modları hakkında daha fazla bilgi için bkz. [Kimlik Doğrulama Modu Seçme](http://msdn.microsoft.com/library/ms144284.aspx).

SQL Server kimlik doğrulamasını etkinleştirmezseniz hello VM tooconnect toohello SQL Server örneğinde hello yerel yönetici hesabını kullanabilirsiniz.

### <a name="storage-configuration"></a>Depolama yapılandırması
Tıklatın **depolama yapılandırması** toospecify hello depolama gereksinimleri.

![SQL Storage Yapılandırması](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Standart depolamayı seçerseniz, bu seçenek kullanılamaz. Otomatik depolama iyileştirmesi yalnızca Premium Storage için kullanılabilir.
> 
> 

Gereksinimleri, saniye başına girdi/çıktı işlemleri (IOP), MB/saniyedeki iş ve toplam depolama boyutu olarak belirleyebilirsiniz. Merhaba hareketli ölçekleri kullanarak bu değerleri yapılandırın. Merhaba portal hello Bu gereksinimler temelinde, disk sayısını otomatik olarak hesaplar.

Varsayılan olarak, Azure hello depolama 5000 IOP 200 MB ve 1 TB depolama alanı için en iyi duruma getirir. İş yüküne göre bu depolama ayarlarını değiştirebilirsiniz. Altında **depolama en iyi duruma getirilmiş**, aşağıdaki seçenekleri şu hello birini seçin:

* **Genel** hello varsayılan ayardır ve çoğu iş yükünü destekler.
* **İşlem** işleme hello depolama geleneksel veritabanı OLTP iş yükleri için iyileştirir.
* **Veri ambarı** hello depolama çözümleme ve raporlama iş yükleri için en iyi duruma getirir.

> [!NOTE]
> Merhaba kaydırıcılar Hello üst sınırları seçilen sanal makine boyutu bağlı olarak değişir.
> 
> 

### <a name="automated-patching"></a>Otomatik düzeltme eki uygulama
**Otomatik düzeltme eki uygulama** varsayılan olarak etkindir. Otomatik düzeltme eki uygulama Azure tooautomatically düzeltme eki SQL Server ve hello işletim sistemi sağlar. Merhaba haftanın günü, saati ve bir bakım penceresi süresi bir gün belirtin. Azure düzeltme eki uygulamayı bu bakım penceresinde gerçekleştirir. Merhaba bakım penceresi zamanlaması hello VM yerel saati kullanır. Azure tooautomatically düzeltme eki SQL Server ve hello işletim sistemi istemiyorsanız tıklayın **devre dışı**.  

![SQL Otomatik Düzeltme Eki Uygulama](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Daha fazla bilgi için bkz. [Azure Virtual Machines’de SQL Server için Otomatik Düzeltme Eki Uygulama](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Otomatik yedekleme
**Otomatik yedekleme** altında, tüm veritabanları için otomatik veritabanı yedeklemeyi etkinleştirin. Otomatik yedekleme varsayılan olarak devre dışıdır.

SQL otomatik yedeklemeyi etkinleştirdiğinizde, hello aşağıdaki ayarları yapılandırabilirsiniz:

* Yedeklemeler için elde tutma süresi (gün)
* Yedeklemeler için depolama hesabı toouse
* Yedeklemeler için şifreleme seçeneği ve parola
* Backup sistem veritabanları
* Yedekleme zamanlamasını yapılandırma

tooencrypt hello yedekleme, tıklatın **etkinleştirmek**. Merhaba belirtin **parola**. Azure tooencrypt hello yedeklemeleri bir sertifika oluşturur ve kullanır hello parola tooprotect bu sertifikayı belirtilen.

![SQL Otomatik Yedekleme](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 Daha fazla bilgi için bkz. [Azure Virtual Machines’de SQL Server için Otomatik Yedekleme](virtual-machines-windows-sql-automated-backup.md).

### <a name="azure-key-vault-integration"></a>Azure Anahtar Kasası tümleştirme
azure'daki toostore güvenlik gizli şifreleme için tıklatın **Azure anahtar kasası tümleştirme** tıklatıp **etkinleştirmek**.

![SQL Azure Anahtar Kasası Tümleştirme](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

Merhaba aşağıdaki tabloda hello parametreleri gerekli tooconfigure Azure anahtar kasası tümleştirmeyi listeler.

| PARAMETRE | AÇIKLAMA | ÖRNEK |
| --- | --- | --- |
| **Anahtar Kasası URL'si** |Merhaba anahtar kasası başlangıç konumu. |https://contosokeyvault.vault.azure.net/ |
| **Asıl ad** |Azure Active Directory hizmet asıl adı. Bu ad ayrıca başvurulan tooas hello istemci kimliği belirtin |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **Asıl parola** |Azure Active Directory hizmet asıl gizli anahtarı. Bu gizli de başvurulan tooas hello gizli olabilir. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **Kimlik bilgisi adı** |**Kimlik bilgisi adı**: AKV tümleştirme, SQL Server, hello VM toohave erişim toohello anahtar kasası sağlayan bir kimlik bilgisi oluşturur. Bu kimlik bilgisi için bir ad seçin. |mycred1 |

Daha fazla bilgi için bkz. [Azure VM’lerde SQL Server için Azure Anahtar Kasası Tümleştirmeyi Yapılandırma](virtual-machines-windows-ps-sql-keyvault.md).

SQL Server ayarlarını yapılandırmayı bitirdiğinizde, **Tamam**’a tıklayın.

### <a name="r-services"></a>R hizmetleri
[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)'i etkinleştirebilirsiniz. SQL Server R Hizmetleri Gelişmiş toouse analytics SQL Server 2016 ile sağlar. Tıklatın **etkinleştirmek** hello üzerinde **SQL Server ayarları** dikey.

![SQL Server R Hizmetlerini Etkinleştirme](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-hello-summary"></a>5. Gözden geçirme hello özeti
Merhaba üzerinde **Özet** dikey penceresinde, gözden geçirme Özet hello ve tıklatın **Tamam** bu VM için belirtilen toocreate SQL Server, kaynak grubu ve kaynakları.

Merhaba dağıtım hello azure portalından izleyebilirsiniz. Merhaba **bildirimleri** düğmesi Merhaba ekranında hello üstündeki hello dağıtımın temel durumunu gösterir.

> [!NOTE]
> tooprovide dağıtım hakkında bir fikir ile defa, ı varsayılan ayarlarla bir SQL VM toohello Doğu ABD bölgesinde dağıtılır. Bu test dağıtımını toplam 26 dakika toocomplete sürdü. Ancak bölgeniz ve seçili ayarlarınıza göre, daha hızlı veya daha yavaş dağıtım süresiyle karşılaşabilirsiniz.
> 
> 

## <a name="open-hello-vm-with-remote-desktop"></a>Merhaba VM Uzak Masaüstü ile açma
Uzak Masaüstü ile adımları tooconnect toohello sanal makine aşağıdaki hello kullan:

1. Azure VM oluşturulduktan, hello hello hello simgesini sonra Azure Panonuzda VM görünür. Bu, varolan sanal makinelerinize göz atarak da bulabilirsiniz. Yeni SQL sanal makinenize tıklayın. Bir **Sanal makine** dikey penceresi sanal makine ayrıntılarını görüntüler.
2. Merhaba hello üstündeki **sanal makine** dikey penceresinde tıklatın **Bağlan**.
3. Merhaba tarayıcı hello VM için RDP dosyasını indirir. Açık hello RDP dosyası.
    ![Uzak Masaüstü tooSQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)
4. Merhaba Uzak Masaüstü Bağlantısı, o hello bu uzak bağlantının yayımcısının tanımlanamıyor bildirir. Tıklatın **Bağlan** toocontinue.
5. Merhaba, **Windows Güvenliği** iletişim kutusunda, tıklatın **başka bir hesap kullan**.
6. İçin **kullanıcı adı** türü  **\<kullanıcı adı >**, burada <user name> hello VM yapılandırdığınızda belirtilen hello kullanıcı adıdır. Bir başlangıç eğik çizgisi hello adından önce tooadd var.
7. Türü hello **parola** bu VM için daha önce yapılandırdığınız ve ardından **Tamam** tooconnect.
8. Başka bir **Uzak Masaüstü Bağlantısı** iletişim sizden olup tooconnect, tıklatın **Evet**.

Toohello SQL Server sanal makineye bağlandıktan sonra SQL Server Management Studio'yu başlatın ve Windows, yerel yönetici kimlik bilgilerinizi kullanarak kimlik doğrulamasına bağlanabilirsiniz. SQL Server kimlik doğrulaması etkinleştirilirse, SQL hello SQL oturum açma ve sağlama işlemi sırasında yapılandırdığınız parola kullanarak kimlik doğrulaması ile bağlanabilir.

Erişim toohello makine toodirectly değişiklik makinesi ve SQL Server ayarlarını gereksinimlerinize göre sağlar. Örneğin, hello güvenlik duvarı ayarlarını yapılandırmak veya SQL Server yapılandırma ayarlarını değiştirebilirsiniz.

## <a name="connect-toosql-server-remotely"></a>TooSQL sunucu uzaktan bağlanma
Bu öğreticide, seçtik **ortak** hello sanal makine için erişim ve **SQL Server kimlik doğrulaması**. Bu ayarlar otomatik olarak yapılandırılan hello sanal makine tooallow SQL Server bağlantıları herhangi bir istemciden (Merhaba doğru SQL oturum açma sahip oldukları varsayılarak) Internet hello.

> [!NOTE]
> SQL Server örneğinizi üzerinden ek adımlar gerekli tooaccess sonra ortak sağlama sırasında seçmediyseniz Internet hello. Daha fazla bilgi için bkz: [tooa SQL Server sanal makinesine bağlanmak](virtual-machines-windows-sql-connect.md).
> 
> 

Aşağıdaki bölümlerde hello nasıl tooconnect tooyour SQL Server Örneğinize başka bir bilgisayardan hello Internet gösterir.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
Azure'da SQL Server kullanma hakkında diğer bilgi için bkz: [Azure Virtual Machines'de SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) ve hello [ilgili sık sorulan sorular](virtual-machines-windows-sql-server-iaas-faq.md).

Azure Virtual Machines'de SQL Server video bir genel bakış için izleme [Azure VM, SQL Server 2016 için en iyi platformdur hello](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).

[Merhaba öğrenme yolunu keşfedin](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) Azure virtual machines'de SQL Server için.

