---
title: "Azure Resource Manager VM'ler için yüksek kullanılabilirliği aaaSet | Microsoft Docs"
description: "Bu öğreticide nasıl toocreate Always On kullanılabilirlik grubu Azure Resource Manager moduna Azure sanal makinelerinde ile gösterilir."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>Always On kullanılabilirlik grupları Azure sanal makineleri otomatik olarak yapılandırın: Kaynak Yöneticisi

Bu öğretici nasıl toocreate bir SQL Server kullanılabilirlik grubu kullanan Azure Resource Manager sanal makineleri gösterir. Merhaba öğretici Azure dikey penceresi tooconfigure bir şablonu kullanır. Merhaba varsayılan ayarları gözden geçirin, gerekli ayarları yazın ve Bu öğreticide yol gibi hello Kanatlar hello portalında güncelleştirin.

Merhaba tam öğretici Azure sanal makinelerde hello aşağıdaki öğeleri içeren bir SQL Server kullanılabilirlik grubu oluşturur:

* Bir ön uç ve arka uç alt ağ dahil olmak üzere birden çok alt ağa sahip bir sanal ağ
* Bir Active Directory etki alanına sahip iki etki alanı denetleyicisi
* SQL Server çalıştıran ve dağıtılan toohello backend alt ağı ve Active Directory etki alanına katılmış toohello iki sanal makineler
* Merhaba düğüm çoğunluğu çekirdek modeli ile üç düğümlü yük devretme kümesi
* Bir kullanılabilirlik veritabanının iki synchronous-commit çoğaltmalarından sahip bir kullanılabilirlik grubu

Aşağıdaki çizimde hello hello eksiksiz bir çözüm temsil eder.

![Test laboratuvarı mimarisi Azure içindeki kullanılabilirlik grupları](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

Bu çözümdeki tüm kaynakları tooa tek bir kaynak grubuna ait.

Bu öğretici başlamadan önce hello aşağıdakileri doğrulayın:

* Bir Azure hesabı zaten var. Biri, yoksa [bir deneme hesabı için kaydolun](http://azure.microsoft.com/pricing/free-trial/).
* Nasıl toouse hello GUI tooprovision hello sanal makine Galerisi SQL Server sanal makine zaten biliyor. Daha fazla bilgi için bkz: [Azure üzerinde bir SQL Server sanal makinenin sağlanması](virtual-machines-windows-portal-sql-server-provision.md).
* Kullanılabilirlik grupları düz bir anlayış zaten var. Daha fazla bilgi için bkz: [Always On kullanılabilirlik grupları (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Kullanılabilirlik grupları ile SharePoint kullanarak ilgileniyorsanız, ayrıca bkz. [yapılandırmak SQL Server 2012 Always On kullanılabilirlik grupları SharePoint 2013 için](http://technet.microsoft.com/library/jj715261.aspx).
>
>

Bu öğreticide Azure hello kullanmak için portal:

* Her zaman açık Hello şablon hello portalından seçin.
* Merhaba şablon ayarlarını gözden geçirin ve ortamınız için birkaç yapılandırma ayarlarını güncelleştirin.
* İzleyici Azure şekilde hello tüm ortamı oluşturur.
* Tooa etki alanı denetleyicisi ve SQL Server çalıştıran tooa sunucuya bağlanın.

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>Sağlama hello küme hello Galeriden
Azure galeri görüntüsü hello tüm çözümü sağlar. toolocate hello şablonu:

1. İçinde toohello, hesabınızı kullanarak Azure portalında oturum açın.
2. Hello Azure portal'ı tıklatın **+ yeni** tooopen hello **yeni** dikey.
3. Merhaba üzerinde **yeni** dikey penceresinde, arama **AlwaysOn**.
   ![AlwaysOn şablonunu bulun](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. Merhaba arama sonuçlarında bulun **SQL Server AlwaysOn kümesi**.
   ![AlwaysOn şablonu](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. Üzerinde **dağıtım modeli seçin**, seçin **Resource Manager**.

### <a name="basics"></a>Temel Bilgiler
Tıklatın **Temelleri** ve hello aşağıdaki ayarları yapılandırın:

* **Yönetici kullanıcı adı** etki alanı yönetici izinlerine sahip bir kullanıcı hesabı ve her iki SQL Server örnekleri üzerinde hello SQL Server sysadmin sabit sunucu rolünün bir üyesidir. Bu öğretici için kullanmak **DomainAdmin**.
* **Parola** hello etki alanı yönetici hesabı için hello paroladır. Karmaşık bir parola kullanın. Merhaba parolayı onaylayın.
* **Abonelik** Azure hello kullanılabilirlik grubu için Dağıtılmış toorun tüm kaynaklar bills hello abonelik. Hesabınızın birden çok aboneliğiniz varsa, farklı bir abonelik belirtebilirsiniz.
* **Kaynak grubu** bu şablonla oluşturulan tüm Azure kaynaklarına ait hello Grup toowhich hello adıdır. Bu öğretici için kullanmak **SQL-HA-RG**. Daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../../../azure-resource-manager/resource-group-overview.md#resource-groups).
* **Konum** olan hello hello öğretici oluşturur hello kaynakları Azure bölgesi. Bir Azure bölgesi seçin.

Merhaba aşağıdaki ekran görüntüsünde bir tamamlanmış olan **Temelleri** dikey penceresinde:

![Temel Bilgiler](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

**Tamam** düğmesine tıklayın.

### <a name="domain-and-network-settings"></a>Etki alanı ve ağ ayarları
Bir etki alanı ve etki alanı denetleyicileri bu Azure galerisinde şablon oluşturur. Ayrıca, bir ağ ve iki alt ağı oluşturur. Merhaba şablon sunucuları bir var olan etki alanı ya da sanal ağ oluşturulamıyor. Merhaba sonraki adıma hello etki alanı ve ağ ayarlarını yapılandırır.

Merhaba üzerinde **etki alanı ve ağ ayarlarını** dikey penceresinde, gözden geçirme hello önceden hello etki alanı ve ağ ayarları için değerleri:

* **Orman kök etki alanı adı** hello hello Active Directory etki alanı için etki alanı adı, ana hello kümedir. Merhaba öğretici için kullanmak **contoso.com**.
* **Sanal ağ adı** hello Azure sanal ağı için hello ağ adıdır. Merhaba öğretici için kullanmak **autohaVNET**.
* **Etki alanı denetleyicisi alt ağ adı** hello hello sanal ağ bir kısmı konakları hello etki alanı denetleyicisi adıdır. Kullanım **alt ağ 1**. Bu alt ağ adresi öneki kullanan **10.0.0.0/24**.
* **SQL Server alt ağ adı** SQL Server ve hello dosya çalıştıran konaklar hello sunucular Tanık paylaşır hello sanal ağ bir kısmı hello adıdır. Kullanım **alt ağ-2**. Bu alt ağ adresi öneki kullanan **10.0.1.0/26**.

toolearn, azure'da sanal ağlar hakkında daha fazla bilgi görmek [sanal ağa genel bakış](../../../virtual-network/virtual-networks-overview.md).  

Merhaba **etki alanı ve ağ ayarlarını** hello görünümlü aşağıdaki ekran görüntüsü:

![Etki alanı ve ağ ayarları](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

Gerekirse, bu değerleri değiştirebilirsiniz. Bu öğretici için kullanmak hello önceden değerleri.

Hello ayarları gözden geçirin ve ardından **Tamam**.

### <a name="availability-group-settings"></a>Kullanılabilirlik grubu ayarları
Üzerinde **kullanılabilirlik grubu ayarlarını**, gözden geçirme hello önceden hello kullanılabilirlik grubu için değerler ve hello dinleyicisi.

* **Kullanılabilirlik grubu adının** hello kümelenmiş bir kaynak hello kullanılabilirlik grubunun adıdır. Bu öğretici için kullanmak **Contoso ag**.
* **Kullanılabilirlik grubu dinleyici adı** hello küme ve hello iç yük dengeleyici tarafından kullanılır. TooSQL sunucusuna bağlanan istemciler bu adı tooconnect toohello uygun hello veritabanının kopyasını kullanabilirsiniz. Bu öğretici için kullanmak **Contoso dinleyici**.
* **Kullanılabilirlik grubu dinleyicisinin bağlantı noktası** hello SQL Server dinleyicisi hello TCP bağlantı noktasını belirtir. Merhaba varsayılan bağlantı noktası, Bu öğretici için kullanmak **1433**.

Gerekirse, bu değerleri değiştirebilirsiniz. Bu öğretici için kullanmak hello önceden değerleri.  

![Kullanılabilirlik grubu ayarları](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

**Tamam** düğmesine tıklayın.

### <a name="virtual-machine-size-storage-settings"></a>Sanal makine boyutu, depolama ayarları
Üzerinde **VM boyutu, depolama ayarlarını**, bir SQL Server sanal makine boyutu seçin ve hello diğer ayarları gözden geçirin.

* **SQL Server sanal makine boyutu** SQL Server çalıştıran her iki sanal makine için başlangıç boyutu. İş yükü için uygun sanal makine boyutu seçin. Bu ortam hello öğretici için oluşturuluyorsa, kullanın **DS2**. Üretim iş yükleri için hello iş yükü destekleyebilir bir sanal makine boyutu seçin. Birçok üretim iş yükleri gerektiren **DS4** veya daha büyük. Merhaba şablon bu boyuttaki iki sanal makine oluşturur ve her biri üzerinde SQL Server'ı yükler. Daha fazla bilgi için bkz: [sanal makineler için Boyutlar](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> SQL Server, Enterprise Edition hello Azure yükler. Merhaba maliyet hello edition ve hello sanal makine boyutuna bağlıdır. Geçerli maliyetler hakkında ayrıntılı bilgi için bkz: [sanal makineler fiyatlandırma](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql).
>
>

* **Etki alanı denetleyicisi sanal makine boyutu** hello sanal makine hello için etki alanı denetleyicileri boyutudur. Bu öğretici kullanmak için **D2**.
* **Dosya paylaşımı tanığı sanal makine boyutu** hello dosya paylaşım tanığı için hello sanal makine boyutu. Bu öğretici için kullanmak **A1**.
* **SQL depolama hesabı** hello SQL Server veri ve işletim sistemi disklerinde tutan hello depolama hesabı hello adıdır. Bu öğretici için kullanmak **alwaysonsql01**.
* **DC depolama hesabı** hello hello depolama hesabı hello için etki alanı denetleyicileri adıdır. Bu öğretici için kullanmak **alwaysondc01**.
* **SQL Server verilerini disk boyutu** TB hello hello SQL Server veri diski TB boyutudur. 1 ile 4 arasında bir sayı belirtin. Bu öğretici için kullanmak **1**.
* **Depolama İyileştirme** hello iş yükü türüne göre hello SQL Server sanal makineler için belirli bir depolama yapılandırma ayarlarını belirler. Bu senaryoda tüm SQL Server sanal makineleri yalnızca tooread ayarlamak Azure disk konak önbelleği premium depolama kullanın. Ayrıca, bu üç ayarlarından birini seçerek hello iş yükü için SQL Server ayarları iyileştirebilirsiniz:

  * **Genel iş yükü** belirli yapılandırma ayarları yok ayarlar.
  * **İşlem işleme** kümeleri izleme bayrağı 1117 ve 1118.
  * **Veri ambarı** kümeleri izleme bayrağı 1117 ve 610.

Bu öğretici için kullanmak **genel iş yükü**.

![VM boyutu depolama ayarları](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

Hello ayarları gözden geçirin ve ardından **Tamam**.

#### <a name="a-note-about-storage"></a>Depolama hakkında bir Not
Ek iyileştirmeler hello SQL Server veri diskleri hello boyutuna göre değişir. Her veri diski terabayt için Azure ek 1 TB premium depolama alanı ekler. Bir sunucu 2 TB veya daha fazla gerektirdiğinde hello şablon her SQL Server sanal makinede bir depolama havuzu oluşturur. Bir depolama havuzu depolama sanallaştırma birden çok diske yapılandırılmış tooprovide daha yüksek kapasite, esneklik ve performans nerede biçimidir.  Merhaba şablon hello depolama havuzunda bir depolama alanı oluşturur ve bir tek veri diski toohello işletim sistemine gösterir. Merhaba şablonu bu disk için SQL Server hello veri diski olarak belirler. Merhaba şablon hello depolama havuzu ayarlarını aşağıdaki hello kullanarak SQL Server için ayarladığını:

* Şerit boyutudur hello hello sanal disk için ayar Interleave. İşlem iş yükleri 64 KB kullanır. Veri ambarı iş yükleri 256 KB kullanın.
* Dayanıklılık basit (esnekliği yok).

> [!NOTE]
> Azure premium storage yerel olarak yedekli ve hello depolama havuzu en fazla esneklik gerekli olmamasını sağlayacak şekilde tek bir bölge içinde hello veri üç kopyasını tutar.
>
>

* Sütun sayısı hello hello depolama havuzundaki disklerin sayısına eşittir.

Depolama alanı ve depolama havuzları hakkında ek bilgi için bkz:

* [Depolama alanlarına genel bakış](http://technet.microsoft.com/library/hh831739.aspx)
* [Windows Server Yedekleme ve depolama havuzları](http://technet.microsoft.com/library/dn390929.aspx)

SQL Server yapılandırma en iyi uygulamalar hakkında daha fazla bilgi için bkz: [performans Azure sanal makinelerde SQL Server için en iyi uygulamaları](virtual-machines-windows-sql-performance.md).

### <a name="sql-server-settings"></a>SQL Server ayarları
Üzerinde **SQL Server ayarları**gözden geçirin ve hello SQL Server sanal makine adı ön eki, SQL Server sürümü, SQL Server hizmet hesabı ve parola değiştirme ve hello SQL otomatik düzeltme eki uygulama bakım zamanlaması.

* **SQL Server adı öneki** kullanılan toocreate her SQL Server sanal makine için bir addır. Bu öğretici için kullanmak **sqlserver**. Merhaba şablon hello SQL Server sanal makineleri adları *sqlserver-0* ve *sqlserver-1*.
* **SQL Server sürümü** SQL Server'ın hello sürümüdür. Bu öğretici kullanmak için **SQL Server 2014**. Ayrıca seçebilirsiniz **SQL Server 2012** veya **SQL Server 2016**.
* **SQL Server hizmet hesabının kullanıcı adı** hello SQL Server hizmeti için hello etki alanı hesap adı. Bu öğretici için kullanmak **SQL hizmet**.
* **Parola** hello SQL Server hizmet hesabı için hello paroladır.  Karmaşık bir parola kullanın. Merhaba parolayı onaylayın.
* **SQL otomatik düzeltme eki uygulama bakım zamanlaması** Azure hello SQL sunucuları otomatik olarak düzeltme ekleri hello haftanın başlangıç günü tanımlar. Bu öğretici için yazın **Pazar**.
* **SQL otomatik düzeltme eki uygulama bakım başlangıç saati** otomatik düzeltme eki uygulama başladığında hello hello Azure bölgesi için günün saattir.

> [!NOTE]
> pencere her bir sanal makine için düzeltme eki uygulama hello bir saate göre aşamalı. Yalnızca bir sanal makine Hizmetleri zaman tooprevent çalışmasının düzeltme.
>
>

![SQL Server ayarları](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

Hello ayarları gözden geçirin ve ardından **Tamam**.

### <a name="summary"></a>Özet
Merhaba Özet sayfasında, Azure hello ayarlarını doğrular. Merhaba şablon de indirebilirsiniz. Gözden geçirme hello Özet. **Tamam** düğmesine tıklayın.

### <a name="buy"></a>Satın Al
Bu son dikey içeren **kullanım koşulları**, ve **gizlilik ilkesi**. Bu bilgileri gözden geçirin. Azure toostart toocreate hello sanal makineler için hazır olduğunda ve tüm hello kullanılabilirlik grubu için gerekli diğer kaynaklar hello olduğunda tıklatın **oluşturma**.

Hello Azure portal hello kaynak grubu ve tüm hello kaynaklar oluşturur.

## <a name="monitor-deployment"></a>İzleyici dağıtım
Hello Azure Portalı'ndan Hello dağıtımının ilerleme durumunu izleyin. Merhaba dağıtım temsil eden bir otomatik olarak sabitlenmiş toohello Azure portalı panosunun simgedir.

![Azure Panosu](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>TooSQL sunucusuna bağlan
Merhaba yeni SQL Server örneği internet'e bağlı IP adresine sahip sanal makinelerde çalışmıyor. Uzak Masaüstü (RDP) doğrudan tooeach SQL Server sanal makine olabilir.

tooRDP tooa SQL Server, aşağıdaki adımları izleyin:

1. Azure portalı panosunun Hello hello dağıtım başarılı olduğunu doğrulayın.
2. Tıklatın **kaynakları**.
3. Merhaba, **kaynakları** dikey penceresinde tıklatın **sqlserver-0**, hello hello sanal makinelerin, SQL Server çalıştıran bir bilgisayar adı olduğu.
4. Merhaba dikey **sqlserver-0**, tıklatın **Bağlan**. Tarayıcınız tooopen istediğiniz veya hello uzak bağlantı nesnesi kaydetmek ister. Tıklatın **açık**.
5. **Uzak Masaüstü Bağlantısı** , o hello bu uzak bağlantının yayımcısının belirlenemedi sizi uyarabilir. **Bağlan**'a tıklayın.
6. Windows güvenlik kimlik bilgileri tooconnect toohello IP adresiniz hello birincil etki alanı denetleyicisinin, tooenter ister. Tıklatın **başka bir hesap kullan**. İçin **kullanıcı adı**, türü **contoso\DomainAdmin**. Merhaba yönetici kullanıcı adı hello şablonunda ayarladığınızda, bu hesabı yapılandırılmış. Merhaba şablonunu yapılandırdığınızda seçtiğiniz hello karmaşık parola kullanın.
7. **Uzak Masaüstü** hello uzak bilgisayarında doğrulanmamış son uyarabilir tooproblems güvenlik sertifikası ile. Size gösterir hello güvenlik sertifika adı. Başlangıç Öğreticisi izlediyseniz hello adıdır **sqlserver 0.contoso.com**. Tıklatın **Evet**.

Şimdi RDP toohello SQL Server sanal makine ile bağlanır. SQL Server Management Studio'yu açın, toohello varsayılan SQL Server örneğine bağlanmak ve o hello kullanılabilirlik grubu yapılandırıldığını doğrulayın.
