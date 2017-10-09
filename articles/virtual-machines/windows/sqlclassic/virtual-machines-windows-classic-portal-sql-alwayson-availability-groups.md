---
title: "aaaConfigure Always On kullanılabilirlik grubunun Azure Virtual Machines'de (Klasik) | Microsoft Docs"
description: "Always On kullanılabilirlik grubu ile Azure sanal makine oluşturun. Bu öğretici, öncelikle hello kullanıcı arabirimi araçlarını yerine ve komut dosyası kullanır."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 8d48a3d2-79f8-4ab0-9327-2f30ee0b2ff1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: f428ad994a55378c281c959f4696fdcaf50632b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-virtual-machines-classic"></a>Always On kullanılabilirlik grubu Azure sanal makineleri (Klasik) yapılandırma
> [!div class="op_single_selector"]
> * [Klasik: kullanıcı Arabirimi](../classic/portal-sql-alwayson-availability-groups.md)
> * [Klasik: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Başlamadan önce Azure Resource Manager modelinde bu görevi tamamlamak olduğunu göz önünde bulundurun. Yeni dağıtımlar için Azure Resource Manager modeli öneririz. Bkz: [SQL Server Always On kullanılabilirlik grupları'Azure sanal makinelerinde](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT] 
> Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. İki farklı dağıtım modelleri toocreate ve iş kaynaklarla Azure sahiptir: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede nasıl toouse hello Klasik dağıtım modeli açıklanmaktadır. 

hello Azure Resource Manager modeli, bu görevle toocomplete bkz [SQL Server Always On kullanılabilirlik grupları'Azure sanal makinelerinde](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

Bu uçtan uca öğretici, SQL Server her zaman Azure sanal makinelerde çalışan kullanarak nasıl tooimplement kullanılabilirlik gruplarını gösterir.

Başlangıç Öğreticisi Hello sonunda, Azure, SQL Server Always On çözümünüz öğeleri aşağıdaki Merhaba oluşur:

* Birden çok alt kümeler içeriyor ve bir ön uç ve arka uç alt ağ içeren bir sanal ağ
* Bir Active Directory (Azure AD) etki alanı ile bir etki alanı denetleyicisi
* SQL Server çalıştıran ve dağıtılan toohello backend alt ağı ve birleştirilmiş toohello Azure AD etki alanı iki sanal makineler
* Merhaba düğüm çoğunluğu çekirdek modeli ile üç düğümlü yük devretme kümesi
* Bir kullanılabilirlik veritabanının iki synchronous-commit çoğaltmalarından sahip bir kullanılabilirlik grubu

Aşağıdaki çizimde hello hello çözüm grafik gösterimidir.

![Test laboratuvarı mimarisi Azure içindeki kullanılabilirlik grupları](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC791912.png)

Bu bir olası yapılandırma olduğuna dikkat edin. Örneğin, iki çoğaltma kullanılabilirlik grubu için sanal makine hello sayısını en aza indirebilirsiniz. İki düğümlü bir küme içinde hello çekirdek dosya paylaşım tanığı olarak hello etki alanı denetleyicisi kullanarak Azure işlem saatlerinde bu yapılandırmayı kaydeder. Bu yöntem, tek gösterilen hello yapılandırmasından hello sanal makine sayısı azaltır.

Bu öğretici hello aşağıdakileri varsayar:

* Bir Azure hesabı zaten var.
* Nasıl toouse hello GUI hello sanal makineye Galerisi tooprovision SQL Server çalıştıran bir Klasik sanal makine zaten biliyor.
* Always On kullanılabilirlik grupları düz bir anlayış zaten var. Daha fazla bilgi için bkz: [Always On kullanılabilirlik grupları (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> SharePoint ile Always On kullanılabilirlik grupları kullanarak ilgileniyorsanız, ayrıca bkz. [yapılandırmak SQL Server 2012 Always On kullanılabilirlik grupları SharePoint 2013 için](https://technet.microsoft.com/library/jj715261.aspx).
> 
> 

## <a name="create-hello-virtual-network-and-domain-controller-server"></a>Merhaba sanal ağ ve etki alanı denetleyici sunucusu oluşturun
Yeni bir Azure deneme sürümü hesabı ile başlar. Hesabınızı ayarladıktan sonra hello giriş Klasik Azure portalı Merhaba ekranında olması gerekir.

1. Merhaba tıklatın **yeni** hello sol köşesinde hello sayfasının ekran görüntüsü aşağıdaki hello gösterildiği gibi hello altındaki düğmesi.
   
    ![Merhaba Portalı'nda yeni'yi tıklatın](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665511.gif)
2. Tıklatın **Ağ Hizmetleri** > **sanal ağ** > **özel Oluştur**hello ekran aşağıdaki gösterildiği gibi.
   
    ![Sanal ağ oluşturma](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665512.gif)
3. Merhaba, **bir sanal ağ oluştur** iletişim kutusunda, hello sayfalarıyla atlama ve aşağıdaki tablonun hello hello ayarları kullanarak yeni bir sanal ağ oluşturun. 
   
   | Sayfa | Ayarlar |
   | --- | --- |
   | Sanal ağ ayrıntıları |**ADI ContosoNET =**<br/>**Bölge Batı ABD =** |
   | DNS sunucuları ve VPN bağlantısı |None |
   | Sanal ağ adres alanları |Aşağıdaki ekran görüntüsü hello ayarları gösterilmektedir: ![Sanal ağ oluşturma](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784620.png) |
4. Merhaba etki alanı denetleyicisi (DC) olarak kullanacağınız Hello sanal makine oluşturun. Tıklatın **yeni** > **işlem** > **sanal makine** > **Galeri'den**gösterildiği gibi Ekran hello.
   
    ![Sanal makine oluşturma](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784621.png)
5. Merhaba, **bir sanal makine oluşturma** iletişim kutusunda, yeni bir sanal makine hello sayfalarıyla atlama ve aşağıdaki tablonun hello hello ayarlarını kullanarak yapılandırın. 
   
   | Sayfa | Ayarlar |
   | --- | --- |
   | Merhaba sanal makine işletim sistemini seçin |Windows Server 2012 R2 Datacenter |
   | Sanal Makine Yapılandırması |**Sürüm yayın tarihi** (son) =<br/>**SANAL makine adı** ContosoDC =<br/>**KATMAN** STANDART =<br/>**BOYUTU** A2 = (2 Çekirdek)<br/>**Yeni bir kullanıcı adı** AzureAdmin =<br/>**Yeni parola** Contoso =! 000<br/>**Onayla** Contoso =! 000 |
   | Sanal Makine Yapılandırması |**Bulut hizmeti** = yeni bir bulut hizmeti oluşturun<br/>**Bulut hizmeti DNS adı** benzersiz bulut hizmeti adı =<br/>**DNS adı** benzersiz bir ad = (örn: ContosoDC123)<br/>**Bölge/BENZEŞİM grubu/sanal ağ** ContosoNET =<br/>**SANAL ağ alt ağları** Back(10.10.2.0/24) =<br/>**Depolama hesabı** otomatik olarak oluşturulan depolama hesabı kullan =<br/>**Kullanılabilirlik KÜMESİ** = (yok) |
   | Sanal makine seçenekleri |Varsayılanları kullanın |

Merhaba yeni bir sanal makine yapılandırdıktan sonra hello sanal makine toobe provsioned için bekleyin. Bu işlem biraz zaman toofinish alır. Merhaba tıklatırsanız **sanal makine** hello Azure Klasik sekmesinde ContosoDC dönüşüm durumlar görebilirsiniz portal, **başlangıç (hazırlama)** çok**durduruldu**, **Başlangıç**, **çalışan (hazırlama)**ve son olarak **çalıştıran**.

Merhaba DC sunucu şimdi başarıyla kaynak sağlandı. Ardından, bu DC sunucuda hello Active Directory etki alanı yapılandırır.

## <a name="configure-hello-domain-controller"></a>Merhaba etki alanı denetleyicisini Yapılandır
Aşağıdaki adımları hello corp.contoso.com etki alanı denetleyicisi olarak hello ContosoDC makine yapılandırın.

1. Merhaba Hello Portalı'nda seçin **ContosoDC** makine. Merhaba üzerinde **Pano** sekmesini tıklatın, **Bağlan** Uzak Masaüstü (RDP) dosyası için Uzak Masaüstü erişimi tooopen.
   
    ![TooVritual makine Bağlan](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784622.png)
2. Yapılandırılmış Yönetici hesabınızla oturum açın (**\AzureAdmin**) ve parolayı (**Contoso! 000**).
3. Varsayılan olarak, hello **Sunucu Yöneticisi'ni** Pano görüntülenmesi.
4. Merhaba tıklatın **rol ve Özellik Ekle** hello Panoda bağlantı.
   
    ![Sunucu Gezgini Rol Ekle](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784623.png)
5. Tıklatın **sonraki** toohello elde edene kadar **sunucu rolleri** bölümü.
6. Select hello **Active Directory etki alanı Hizmetleri** ve **DNS sunucusu** rolleri. İstendiğinde, bu rolleri gerektiren daha fazla özellikleri ekleyin.
   
   > [!NOTE]
   > Statik bir IP adresi olduğunu uyarı doğrulama alırsınız. Merhaba yapılandırma sınıyorsanız tıklatın **devam**. Üretim senaryoları için [PowerShell tooset hello statik IP adresi hello etki alanı denetleyicisi makinenin kullanmak](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   > 
   > 
   
    ![Rolleri iletişim ekleyin](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784624.png)
7. Tıklatın **sonraki** hello ulaşana kadar **onay** bölümü. Select hello **otomatik olarak yeniden başlatma hello hedef sunucu** onay kutusu.
8. **Yükle**'ye tıklayın.
9. Merhaba özellikleri yüklendikten sonra toohello dönmek **Sunucu Yöneticisi'ni** Pano.
10. Select hello yeni **AD DS** hello sol bölmedeki seçeneği.
11. Merhaba tıklatın **daha fazla** hello sarı uyarı çubuğundaki bağlantı.
    
     ![DNS sunucusu sanal makinesinde AD DS iletişim kutusu](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784625.png)
12. Merhaba, **eylem** hello sütunu **tüm sunucu görev ayrıntıları** iletişim kutusu, tıklatın **bu sunucu tooa etki alanı denetleyicisini yükseltmek**.
13. Merhaba, **Active Directory etki alanı Hizmetleri Yapılandırma Sihirbazı**, hello aşağıdaki değerleri kullanın:
    
    | Sayfa | Ayar |
    | --- | --- |
    | Dağıtım Yapılandırması |**Yeni orman Ekle** seçili =<br/>**Kök etki alanı adı** corp.contoso.com = |
    | Etki alanı denetleyicisi seçenekleri |**Parola** Contoso =! 000<br/>**Parolayı onaylayın** Contoso =! 000 |
14. Tıklatın **sonraki** toogo aracılığıyla hello hello Sihirbazı diğer sayfalar. Merhaba üzerinde **Önkoşul denetimi** sayfasında, iletiden hello gördüğünüzü doğrulayın: **tüm önkoşul denetimlerinden başarıyla geçti**. Tüm ilgili uyarı iletileri gözden geçirmeniz gereken ancak hello yüklemesiyle olası toocontinue olduğunu unutmayın.
15. **Yükle**'ye tıklayın. Merhaba **ContosoDC** sanal makine otomatik olarak yeniden.

## <a name="configure-domain-accounts"></a>Etki alanı hesaplarını yapılandırma
Merhaba sonraki adımlar hello Active Directory hesaplarını daha sonra kullanmak için yapılandırın.

1. İçinde toohello tekrar oturum **ContosoDC** makine.
2. İçinde **Sunucu Yöneticisi'ni**, tıklatın **Araçları** > **Active Directory Yönetim Merkezi'ni**.
   
    ![Active Directory Yönetim Merkezi](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784626.png)
3. Merhaba, **Active Directory Yönetim Merkezi'ni**seçin **corp (yerel)** hello sol bölmede.
4. Merhaba sağ üzerinde **görevleri** bölmesinde tıklatın **yeni** > **kullanıcı**. Ayarları aşağıdaki hello kullan:
   
   | Ayar | Değer |
   | --- | --- |
   | **İlk adı** |Yükleme |
   | **Kullanıcı SamAccountName** |Yükleme |
   | **Parola** |Contoso! 000 |
   | **Parolayı onayla** |Contoso! 000 |
   | **Diğer parola seçenekleri** |Seçildi |
   | **Parola her zaman geçerli olsun** |İşaretli |
5. Tıklatın **Tamam** toocreate hello **yükleme** kullanıcı. Bu hesap, kullanılan tooconfigure hello yük devretme kümesi ve hello kullanılabilirlik grubu olacaktır.
6. İki ek kullanıcılar oluşturma **CORP\SQLSvc1** ve **CORP\SQLSvc2**, hello ile aynı adımları. Bu hesapları hello SQL Server örnekleri için kullanılır. Ardından toogive gerekir **CORP\Install** gerekli izinleri tooconfigure Windows Yük Devretme Kümelemesi hello.
7. Merhaba, **Active Directory Yönetim Merkezi'ni**, tıklatın **corp (yerel)** hello sol bölmede. Merhaba, **görevleri** bölmesinde tıklatın **özellikleri**.
   
    ![CORP kullanıcı özellikleri](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784627.png)
8. Seçin **uzantıları**ve ardından hello **Gelişmiş** hello düğmesinde **güvenlik** sekmesi.
9. Merhaba, **corp için Gelişmiş güvenlik ayarları** iletişim kutusu, tıklatın **Ekle**.
10. Tıklatın **sorumlu Seç**, arama **CORP\Install**ve ardından **Tamam**.
11. Select hello **tüm özellikleri oku** ve **bilgisayar nesneleri oluşturma** izinleri.
    
     ![Corp kullanıcı izinleri](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784628.png)
12. Tıklatın **Tamam**ve ardından **Tamam** yeniden. Kapat hello corp Özellikler penceresini açın.

Active Directory ve hello kullanıcı nesneleri yapılandırılmış, üç SQL Server sanal makine oluşturacak ve bunları toothis etki alanına katılın.

## <a name="create-hello-sql-server-virtual-machines"></a>Merhaba SQL Server sanal makine oluşturma
Üç sanal makine oluşturun. Bir küme düğümü için biridir ve SQL Server için ikisidir. toocreate her hello sanal makinelerin Git geri toohello Klasik Azure Portalı'na tıklayın **yeni** > **işlem** > **sanal makine**  >  **Galerisinden**. Ardından, tablo toohelp hello sanal makineler oluşturma aşağıdaki hello hello şablonları kullanın.

| Sayfa | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Merhaba sanal makine işletim sistemini seçin |**Windows Server 2012 R2 Datacenter** |**SQL Server 2014 RTM Enterprise** |**SQL Server 2014 RTM Enterprise** |
| Sanal Makine Yapılandırması |**Sürüm yayın tarihi** (son) =<br/>**SANAL makine adı** ContosoWSFCNode =<br/>**KATMAN** STANDART =<br/>**BOYUTU** A2 = (2 Çekirdek)<br/>**Yeni bir kullanıcı adı** AzureAdmin =<br/>**Yeni parola** Contoso =! 000<br/>**Onayla** Contoso =! 000 |**Sürüm yayın tarihi** (son) =<br/>**SANAL makine adı** ContosoSQL1 =<br/>**KATMAN** STANDART =<br/>**BOYUTU** A3 = (4 çekirdek)<br/>**Yeni bir kullanıcı adı** AzureAdmin =<br/>**Yeni parola** Contoso =! 000<br/>**Onayla** Contoso =! 000 |**Sürüm yayın tarihi** (son) =<br/>**SANAL makine adı** ContosoSQL2 =<br/>**KATMAN** STANDART =<br/>**BOYUTU** A3 = (4 çekirdek)<br/>**Yeni bir kullanıcı adı** AzureAdmin =<br/>**Yeni parola** Contoso =! 000<br/>**Onayla** Contoso =! 000 |
| Sanal Makine Yapılandırması |**Bulut hizmeti** önceden oluşturulmuş benzersiz bulut hizmeti DNS adı = (örn: ContosoDC123)<br/>**Bölge/BENZEŞİM grubu/sanal ağ** ContosoNET =<br/>**SANAL ağ alt ağları** Back(10.10.2.0/24) =<br/>**Depolama hesabı** otomatik olarak oluşturulan depolama hesabı kullan =<br/>**Kullanılabilirlik KÜMESİ** = oluşturun bir kullanılabilirlik kümesi<br/>**KULLANILABİLİRLİK KÜMESİ ADI** SQLHADR = |**Bulut hizmeti** önceden oluşturulmuş benzersiz bulut hizmeti DNS adı = (örn: ContosoDC123)<br/>**Bölge/BENZEŞİM grubu/sanal ağ** ContosoNET =<br/>**SANAL ağ alt ağları** Back(10.10.2.0/24) =<br/>**Depolama hesabı** otomatik olarak oluşturulan depolama hesabı kullan =<br/>**Kullanılabilirlik KÜMESİ** = SQLHADR (de yapılandırabilirsiniz hello kullanılabilirlik hello makine oluşturulduktan sonra ayarlayın. Üç makinenin toohello SQLHADR kullanılabilirlik kümesi atanması gerekir.) |**Bulut hizmeti** önceden oluşturulmuş benzersiz bulut hizmeti DNS adı = (örn: ContosoDC123)<br/>**Bölge/BENZEŞİM grubu/sanal ağ** ContosoNET =<br/>**SANAL ağ alt ağları** Back(10.10.2.0/24) =<br/>**Depolama hesabı** otomatik olarak oluşturulan depolama hesabı kullan =<br/>**Kullanılabilirlik KÜMESİ** = SQLHADR (de yapılandırabilirsiniz hello kullanılabilirlik hello makine oluşturulduktan sonra ayarlayın. Üç makinenin toohello SQLHADR kullanılabilirlik kümesi atanması gerekir.) |
| Sanal makine seçenekleri |Varsayılanları kullanın |Varsayılanları kullanın |Varsayılanları kullanın |

<br/>

> [!NOTE]
> Temel katman makinelerde yük dengeli uç noktalar desteklemediğinden hello önceki yapılandırma standart katman sanal makinelerde önerir. Yük dengeli uç noktalar gereken sonraki toocreate bir kullanılabilirlik grubu dinleyicisi. Ayrıca, burada önerilen makine boyutlarını hello Azure sanal makinelerinde kullanılabilirlik grupları test etmek için yöneliktir. Merhaba en iyi performans için üretim iş yükleri üzerinde SQL Server makine boyutlarını ve yapılandırmada hello önerilerini görmek [Azure Virtual Machines'de SQL Server için performans en iyi uygulamaları](../sql/virtual-machines-windows-sql-performance.md).
> 
> 

Merhaba üç sanal makinelerin tam olarak sağlandıktan sonra toojoin gereksinim bunları toohello **corp.contoso.com** CORP\Install yönetici hakları toohello makineler etki alanı ve verin. toodo her hello üç sanal makineler için şu adımları Bu, kullanım hello.

1. İlk olarak, hello tercih edilen DNS sunucusu adresi değiştirin. Her sanal makinenin RDP dosyası tooyour yerel dizin hello sanal makine hello listesinde seçerek ve hello tıklatarak karşıdan **Bağlan** düğmesi. tooselect bir sanal makine tıklayın herhangi bir yere hello satırda, ilk hücrenin hello ancak hello ekran aşağıdaki gösterildiği gibi.
   
    ![Merhaba RDP dosyasını karşıdan yükleyin](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664953.jpg)
2. Açık hello RDP dosyasını karşıdan ve toohello sanal makinede yapılandırılan yönetici hesabınızı kullanarak oturum (**BUILTIN\AzureAdmin**) ve parolayı (**Contoso! 000**).
3. Oturum açtıktan sonra hello görmelisiniz **Sunucu Yöneticisi'ni** Pano. Tıklatın **yerel sunucu** hello sol bölmede.
4. Merhaba tıklatın **etkin IPv6 DHCP tarafından atanan bir IPv4 adresi** bağlantı.
5. Merhaba, **ağ bağlantıları** iletişim kutusunda, hello ağ simgesine tıklayın.
   
    ![Merhaba sanal makinenin tercih edilen DNS sunucusunu Değiştir](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784629.png)
6. Merhaba komut çubuğunda **bu bağlantının hello ayarlarını değiştir**. (Pencerenizi hello boyutuna bağlı olarak, tooclick hello çift sağ ok toosee bu komut olabilir).
7. Seçin **Internet Protokolü sürüm 4 (TCP/IPv4)**ve ardından **özellikleri**.
8. Seçin **aşağıdaki DNS sunucu adreslerini kullan hello** ve ardından belirtin **10.10.2.4** içinde **tercih edilen DNS sunucusu**.
9. Merhaba **10.10.2.4** atanan tooa sanal makine hello 10.10.2.0/24 alt ağda bir Azure sanal ağında hello adresi adresidir. Bu sanal makine **ContosoDC**. tooverify **ContosoDC**bilgisayarın IP adresi, kullanım **nslookup contosodc** hello komut istemi penceresinde hello ekran aşağıdaki gösterildiği gibi.
   
    ![Etki alanı denetleyicisi için NSLOOKUP toofind IP adresi kullanın](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664954.jpg)
10. Tıklatın **Tamam** > **Kapat** toocommit hello değişiklikleri. Merhaba sanal makine çok Şimdi Katıl**corp.contoso.com**.
11. Merhaba edilene **yerel sunucu** penceresinde hello tıklatın **çalışma grubu** bağlantı.
12. Merhaba, **bilgisayar adı** 'yi tıklatın **değişiklik**.
13. Select hello **etki alanı** onay kutusuna **corp.contoso.com** hello metin kutusuna ve ardından **Tamam**.
14. Merhaba, **Windows Güvenliği** iletişim kutusunda, hello varsayılan etki alanı yöneticisi hesabı hello kimlik bilgilerini belirtin (**CORP\AzureAdmin**) ve hello parola (**Contoso! 000**).
15. Merhaba "Hoş Geldiniz toohello corp.contoso.com etki alanında" iletisini gördüğünüzde, tıklatın **Tamam**.
16. Tıklatın **Kapat** > **şimdi yeniden Başlat** hello iletişim kutusunda.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-virtual-machine"></a>Her sanal makinede yönetici olarak Hello Corp\Install kullanıcı ekleyin
1. Merhaba sanal makine yeniden başlatılana kadar bekleyin ve ardından açık hello RDP kullanarak, dosya yeniden toosign toohello sanal makinede hello **BUILTIN\AzureAdmin** hesabı.
2. İçinde **Sunucu Yöneticisi'ni** tıklatın **Araçları** > **Bilgisayar Yönetimi**.
   
    ![Bilgisayar Yönetimi](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784630.png)
3. Merhaba, **Bilgisayar Yönetimi** iletişim kutusunda, genişletin **yerel kullanıcılar ve gruplar**ve ardından **grupları**.
4. Merhaba çift **Yöneticiler** grubu.
5. Merhaba, **Yöneticiler özellikleri** iletişim kutusunda, hello **Ekle** düğmesi.
6. Merhaba kullanıcı girin **CORP\Install**ve ardından **Tamam**. Kimlik bilgileri istendiğinde hello kullan **AzureAdmin** hello hesabıyla **Contoso! 000** parola.
7. Tıklatın **Tamam** tooclose hello **yönetici özellikleri** iletişim kutusu.

### <a name="add-hello-failover-clustering-feature-tooeach-virtual-machine"></a>Merhaba Yük Devretme Kümelemesi özelliğini tooeach sanal makine ekleyin
1. Merhaba, **Sunucu Yöneticisi'ni** panoyu tıklatın **rol ve Özellik Ekle**.
2. Merhaba, **Ekle roller ve Özellikler Sihirbazı**, tıklatın **sonraki** toohello elde edene kadar **özellikleri** sayfası.
3. Seçin **Yük Devretme Kümelemesi**. İstendiğinde, bağımlı diğer özellikleri ekleyin.
   
    ![Yük Devretme Kümelemesi özelliğini toovirtual makine ekleyin](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784631.png)
4. Tıklatın **sonraki**ve ardından **yükleme** hello üzerinde **onay** sayfası.
5. Ne zaman hello **Yük Devretme Kümelemesi** özellik yükleme tamamlandığında, tıklatın **Kapat**.
6. Merhaba sanal makineyi dışına oturum açın.
7. Merhaba üç sunucu için bu bölümdeki adımları yineleyin: **ContosoWSFCNode**, **ContosoSQL1**, ve **ContosoSQL2**.

sanal makineler artık sağlanan SQL Server ve çalışan Merhaba, ancak her SQL Server için hello varsayılan seçenekleri vardır.

## <a name="create-hello-failover-cluster"></a>Merhaba yük devretme kümesi oluşturma
Bu bölümde daha sonra oluşturacağınız hello kullanılabilirlik grubu barındıracak hello yük devretme kümesi oluşturun. Şimdi tarafından tooeach hello üç sanal makinelerin, hello yük devretme kümesinde kullanacağınız aşağıdaki hello yaptığınız:

* Azure'da tamamen sağlanan hello sanal makine
* Merhaba sanal makine toohello etki alanına katılmış
* Eklenen **CORP\Install** toohello yerel Yöneticiler grubu
* Eklenen hello Yük Devretme Kümelemesi özelliğini

Toohello yük devretme kümesi katılabilmesi için önce bu tüm sanal makinelerin her ön koşullar verilmiştir.

Ayrıca, Azure sanal ağı hello Not hello aynı şekilde davranır olmayan bir şirket içi ağ şekilde. Toocreate hello sırasının hello kümede gerekir:

1. Bir düğümde tek düğümlü bir küme oluşturun (**ContosoSQL1**).
2. Merhaba küme IP adresi tooan değiştirme kullanılmayan IP adresi (**10.10.2.101**).
3. Merhaba küme adını çevrimiçine getirin.
4. Ekleme diğer düğümlere hello (**ContosoSQL2** ve **ContosoWSFCNode**).

Tam olarak hello küme yapılandırma adımları toocomplete hello görevleri aşağıdaki hello kullanın.

1. İçin açık hello RDP dosyası **ContosoSQL1**ve hello etki alanı hesabı kullanarak oturum açma **CORP\Install**.
2. Merhaba, **Sunucu Yöneticisi'ni** panoyu tıklatın **Araçları** > **yük devretme kümesi Yöneticisi**.
3. Merhaba sol bölmesinde, **yük devretme kümesi Yöneticisi**ve ardından **bir küme oluşturmak**hello ekran aşağıdaki gösterildiği gibi.
   
    ![Küme oluşturma](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784632.png)
4. İçindeki küme oluşturma Sihirbazı'nı Merhaba, hello sayfalarıyla atlama ve aşağıdaki tablonun hello hello ayarlarını kullanarak tek düğümlü bir küme oluşturun:
   
   | Sayfa | Ayarlar |
   | --- | --- |
   | Başlamadan önce |Varsayılanları kullanın |
   | Sunucuları seçin |Tür **ContosoSQL1** içinde **sunucu adını girin** tıklatıp **Ekle** |
   | Doğrulama uyarısı |Seçin **ı bu küme için Microsoft desteğine gereksiniminiz ve bu nedenle toorun hello doğrulama istemiyorsanız Hayır sınar. Sonraki tıkladığınızda, hello küme oluşturmaya devam etmek**. |
   | Yönetme hello küme için erişim noktası |Tür **Cluster1** içinde **küme adı** |
   | Onay |Depolama alanları kullanmadığınız sürece varsayılan ayarları kullanın. Bu tablodan sonraki hello uyarı bakın. |
   
   > [!WARNING]
   > Kullanıyorsanız [depolama alanları](https://technet.microsoft.com/library/hh831739), depolama havuzu halinde birden çok disk grupları, hello temizlemeniz gerekir **tüm uygun depolama toohello küme eklemek** hello onay kutusu **onay** sayfası. Bu seçeneği temizlerseniz değil, işlem kümeleme hello sırasında hello sanal diskler ayrılacaktır. Merhaba depolama alanları hello kümeden kaldırılmış ve PowerShell kullanarak yeniden kadar sonuç olarak, bunlar ayrıca Disk Yöneticisi'nde veya Explorer görünmez.
   > 
   > 
5. Merhaba sol bölmesinde **yük devretme kümesi Yöneticisi**ve ardından **Cluster1.corp.contoso.com**.
6. Merhaba bölmeyi toohello kaydırarak **küme çekirdek kaynakları** bölümünde ve hello genişletin **ad: Clutser1** ayrıntıları. Her iki hello görmelisiniz **adı** ve hello **IP adresi** hello kaynaklarında **başarısız** durumu. Merhaba küme atandığından hello IP adresi kaynağı çevrimiçi duruma getirilemiyor hello hello makine kendisi, aynı IP adresine, yinelenen bir adrestir.
7. Başarısız sağ hello **IP adresi** kaynak ve ardından **özellikleri**.
   
    ![Küme Özellikleri](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784633.png)
8. Seçin **statik IP adresi**, belirtin **10.10.2.101** hello içinde **adresi** metin kutusuna ve ardından **Tamam**.
9. Merhaba, **küme çekirdek kaynakları** bölümünde, sağ **ad: Cluster1**ve ardından **çevrimiçine**. Her iki kaynağın çevrimiçi olana kadar bekleyin. Merhaba küme adı kaynağını çevrimiçi olduğunda hello DC sunucusuna sahip yeni bir Active Directory bilgisayar hesabı güncelleştirilir. Bu Active Directory hesabı kullanılacak toorun hello kullanılabilirlik grubu kümelenmiş hizmet daha sonra.
10. Kalan düğümleri toohello küme hello ekleyin. Merhaba tarayıcı ağacında sağ **Cluster1.corp.contoso.com**ve ardından **düğüm Ekle**hello ekran aşağıdaki gösterildiği gibi.
    
     ![Düğüm toohello kümesi Ekle](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784634.png)
11. Merhaba, **Düğüm Ekleme Sihirbazı'nı**, tıklatın **sonraki** hello üzerinde **sunucuları Seç** sayfasında, eklemek **ContosoSQL2** ve **ContosoWSFCNode**  hello sunucu adını yazarak toohello listesi **sunucu adını girin** ve ardından **Ekle**. İşiniz bittiğinde tıklatın **sonraki**.
12. Merhaba üzerinde **doğrulama uyarısı** sayfasında, **Hayır**, ancak bir üretim senaryosunda hello doğrulama testleri gerçekleştirmeniz gerekir. Ardından **İleri**'ye tıklayın.
13. Merhaba üzerinde **onay** sayfasında, **sonraki** tooadd hello düğümleri.
    
    > [!WARNING]
    > Kullanıyorsanız [depolama alanları](https://technet.microsoft.com/library/hh831739), depolama havuzu halinde birden çok disk grupları, hello temizlemeniz gerekir **tüm uygun depolama toohello küme eklemek** onay kutusu. Bu seçeneği temizlerseniz değil, işlem kümeleme hello sırasında hello sanal diskler ayrılacaktır. Sonuç olarak, hello depolama alanları kümeden kaldırılana kadar ayrıca Disk Yöneticisi'nde veya Explorer görünmez ve PowerShell kullanarak yeniden.
    > 
    > 
14. Merhaba düğümleri toohello küme eklendikten sonra tıklatın **son**. Yük Devretme Kümesi Yöneticisi şimdi Göster kümenizi üç düğüme sahip ve hello listesinde **düğümleri** kapsayıcı.
15. Merhaba dışında Uzak Masaüstü oturumu açın.

## <a name="prepare-hello-sql-server-instances-for-availability-groups"></a>Merhaba SQL Server örneklerinin kullanılabilirlik grupları için hazırlama
Bu bölümde, ne yapacağını hem aşağıdaki hello **ContosoSQL1** ve **contosoSQL2**:

* Oturum açma ekleme **NT AUTHORITY\SYSTEM** toohello varsayılan SQL Server örneği gerekli izinlere sahip ayarlayın.
* Ekleme **CORP\Install** bir sysadmin rolü toohello varsayılan SQL Server örneği olarak.
* SQL Server'ın uzaktan erişim için Hello Güvenlik Duvarı'nı açın.
* Kullanılabilirlik grupları özelliği her zaman açık Hello etkinleştirin.
* Merhaba SQL Server hizmet hesabını çok değiştirme**CORP\SQLSvc1** ve **CORP\SQLSvc2**sırasıyla.

Bunlardan herhangi bir sırada gerçekleştirilebilir. Bununla birlikte, aşağıdaki adımları hello aralarında sırayla yol gösterir. Merhaba her ikisi için adımları **ContosoSQL1** ve **ContosoSQL2**:

1. Merhaba sanal makine için Uzak Masaüstü oturumu hello dışında oturum değil, bunu şimdi yapın.
2. Açık hello RDP dosyalarını **ContosoSQL1** ve **ContosoSQL2**, olarak oturum açın ve **BUILTIN\AzureAdmin**.
3. Ekleme **NT AUTHORITY\SYSTEM** toohello SQL Server oturumları gerekli izinlere sahip. **SQL Server Management Studio**’yu açın.
4. Tıklatın **Bağlan** tooconnect toohello varsayılan SQL Server örneği.
5. İçinde **Object Explorer**, genişletin **güvenlik**, genişletin ve ardından **oturumları**.
6. Sağ hello **NT AUTHORITY\SYSTEM** oturum açma ve ardından **özellikleri**.
7. Merhaba üzerinde **güvenliği sağlanabilir öğelerle** hello yerel sunucu için select sayfa **Grant** için aşağıdaki izinleri hello ve ardından **Tamam**.
   
   * Herhangi bir kullanılabilirlik grubu Değiştir
   * SQL bağlantı
   * VIEW server state
8. Ekleme **CORP\Install** olarak bir **sysadmin** rol toohello varsayılan SQL Server örneği. İçinde **Object Explorer**, sağ **oturumları**ve ardından **yeni oturum açma**.
9. Tür **CORP\Install** içinde **oturum açma adı**.
10. Merhaba üzerinde **sunucu rolleri** sayfasında, **sysadmin**ve ardından **Tamam**. Merhaba oturum açma oluşturduktan sonra genişleterek görebileceğiniz **oturumları** içinde **Object Explorer**.
11. toocreate hello üzerinde SQL Server için bir güvenlik duvarı kuralı **Başlat** ekran, açık **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı**.
12. Merhaba sol bölmesinde seçin **gelen kuralları**. Merhaba sağ bölmede **yeni kural**.
13. Merhaba üzerinde **kural türü** sayfasında, **Program** > **sonraki**.
14. Merhaba üzerinde **Program** sayfasında, **bu programın yolu**, türü **%ProgramFiles%\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn\sqlservr.exe** hello metin kutusuna ve ardından **sonraki**. Bu yönergeleri izleyerek ancak SQL Server 2012 kullanarak hello SQL Server dizini varsa, **MSSQL11. MSSQLSERVER**.
15. Merhaba üzerinde **eylem** sayfasında, tutmak **hello bağlantıya izin verme** seçili ve ardından **sonraki**.
16. Merhaba üzerinde **profil** sayfasında, hello varsayılan ayarları kabul edin ve ardından **sonraki**.
17. Merhaba üzerinde **adı** sayfasında, bir kural adı gibi belirtin **SQL Server (Program kuralı)**, hello içinde **adı** metin kutusuna ve ardından **son**.
18. tooenable hello **Always On kullanılabilirlik grupları** özelliği, hello **Başlat** ekran, açık **SQL Server Configuration Manager**.
19. Merhaba tarayıcı ağacında tıklayın **SQL Server Hizmetleri**, sağ hello **SQL Server (MSSQLSERVER)** hizmet ve ardından **özellikleri**.
20. Merhaba tıklatın **her zaman üzerinde yüksek kullanılabilirlik** sekmesine **etkinleştirmek Always On kullanılabilirlik grupları**gösterildiği gibi hello ekran ve ardından **Uygula**. Tıklatın **Tamam** hello iletişim kutusu ve hello kapatmayın **özellikleri** henüz iletişim kutusu. Merhaba hizmet hesabı değiştirdikten sonra hello SQL Server hizmetini yeniden başlatır.
    
     ![Always On kullanılabilirlik grupları etkinleştir](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665520.gif)
21. toochange hello SQL Server hizmet hesabına tıklayın hello **oturum açma** sekmesinde, yazın **CORP\SQLSvc1** (için **ContosoSQL1**) veya **CORP\SQLSvc2** () için **ContosoSQL2**) içinde **hesap adı**doldurun ve hello parolayı onaylayın ve ardından **Tamam**.
22. Açılan hello iletişim kutusunda **Evet** toorestart hello SQL Server hizmeti. Merhaba SQL Server hizmeti yeniden başlatıldıktan sonra hello yapılan değişiklikler **özellikleri** iletişim kutusu etkin.
23. Merhaba sanal makineler dışında oturum açın.

## <a name="create-hello-availability-group"></a>Merhaba kullanılabilirlik grubu oluşturma
Hazır tooconfigure bir kullanılabilirlik grubu sunulmuştur. Ne yapacağını, ana hattı aşağıdadır:

* Yeni veritabanı oluştur (**MyDB1**) üzerinde **ContosoSQL1**.
* Tam yedekleme ve hello veritabanının işlem günlüğü yedeklemesi gerçekleştirin.
* Merhaba tam geri yükleme ve günlük yedekleri çok**ContosoSQL2** hello ile **NORECOVERY** seçeneği.
* Merhaba kullanılabilirlik grubu oluşturun (**AG1**) zaman uyumlu tamamlama, otomatik yük devretme ve okunabilir ikincil kopya.

### <a name="create-hello-mydb1-database-on-contososql1"></a>Merhaba MyDB1 veritabanı üzerinde ContosoSQL1 oluşturma
1. Zaten hello uzak masaüstü oturumları için dışında imzaladığınız değil, **ContosoSQL1** ve **ContosoSQL2**, bunu şimdi yapın.
2. İçin açık hello RDP dosyası **ContosoSQL1**, olarak oturum açın ve **CORP\Install**.
3. İçinde **dosya Gezgini**altında **C:\\**, adlı bir dizin oluşturun **yedekleme**. Bu dizin tooback kullanır ve veritabanınızı geri.
4. Merhaba yeni dizin sağ tıklayın, çok gelin**paylaşmak**ve ardından **belirli kişiler**hello ekran aşağıdaki gösterildiği gibi.
   
    ![Bir yedekleme klasörü oluşturma](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665521.gif)
5. Ekleme **CORP\SQLSvc1**ve hello verin **okuma/yazma** izni. Ekleme **CORP\SQLSvc2**ve hello verin **okuma** gösterildiği gibi izni hello ekran ve ardından **paylaşımı**. Merhaba dosya paylaşımı işlemi tamamlandıktan sonra tıklatın **Bitti**.
   
    ![Yedekleme klasörü için izin ver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665522.gif)
6. Merhaba de toocreate hello veritabanından **Başlat** menüsünde, açık **SQL Server Management Studio**ve ardından **Bağlan** tooconnect toohello varsayılan SQL Server örneği.
7. İçinde **Object Explorer**, sağ **veritabanları**ve ardından **yeni veritabanı**.
8. İçinde **veritabanı adı**, türü **MyDB1**ve ardından **Tamam**.

### <a name="make-a-full-backup-of-mydb1-and-restore-it-on-contososql2"></a>Tam MyDB1 yedeklemesini yapın ve ContosoSQL2 üzerinde geri yükleme
1. Merhaba tam yedeklemesini veritabanı toomake **Object Explorer**, genişletin **veritabanları**, sağ **MyDB1**, çok noktası**görevleri**, ve ardından **yedekleme**.
2. Merhaba, **kaynak** bölümünde, tutmak **yedekleme türü** çok ayarlamak**tam**. Merhaba, **hedef** 'yi tıklatın **kaldırmak** hello yedekleme dosyaları için tooremove hello varsayılan dosya yolu.
3. Merhaba, **hedef** 'yi tıklatın **Ekle**.
4. Merhaba, **dosya adı** metin kutusunda,  **\\ContosoSQL1\backup\MyDB1.bak**, tıklatın **Tamam**ve ardından **Tamam** yeniden Merhaba veritabanını tooback. Merhaba yedekleme işlemi bittiğinde, bilgisayarınızı **Tamam** yeniden tooclose hello iletişim kutusu.
5. toomake bir işlem oturum hello veritabanının yedeğini **Object Explorer**, genişletin **veritabanları**, sağ **MyDB1**, çok noktası**görevleri**ve ardından **yedekleme**.
6. İçinde **yedekleme türü**seçin **işlem günlüğü**. Merhaba tutmak **hedef** yol kümesi toohello biri daha önce belirtilen dosya ve ardından **Tamam**. Merhaba yedekleme işlemi bittikten sonra tıklatın **Tamam** yeniden.
7. toorestore hello tam ve işlem oturum yedeklemeleri **ContosoSQL2**açın hello RDP dosyası için **ContosoSQL2**, olarak oturum açın ve **CORP\Install**. İçin Uzak Masaüstü oturumu Hello bırakın **ContosoSQL1** açın.
8. Merhaba gelen **Başlat** menüsünde, açık **SQL Server Management Studio**ve ardından **Bağlan** tooconnect toohello varsayılan SQL Server örneği.
9. İçinde **Object Explorer**, sağ **veritabanları**ve ardından **Restore Database**.
10. Merhaba, **kaynak** bölümünde, select **aygıt**ve hello üç nokta düğmesine **...** tıklayın.
11. İçinde **yedekleme cihazları Seç**, tıklatın **Ekle**.
12. İçinde **yedekleme dosyası konumu**, türü  **\\ContosoSQL1\backup**, tıklatın **yenileme**seçin **MyDB1.bak**, tıklatın **Tamam**ve ardından **Tamam** yeniden. Merhaba tam yedekleme ve hello hello günlük yedekleme görmelisiniz **yedekleme kümelerinin toorestore** bölmesi.
13. Toohello Git **seçenekleri** sayfasında, **RESTORE WITH NORECOVERY** içinde **Kurtarma durumu**ve ardından **Tamam** toorestore hello veritabanı. Hello sonra geri yükleme işlemi tamamlandığında, tıklatın **Tamam**.

### <a name="create-hello-availability-group"></a>Merhaba kullanılabilirlik grubu oluşturma
1. Git geri toohello Uzak Masaüstü oturumu için **ContosoSQL1**. İçinde **Object Explorer** SQL Server Management Studio'da sağ **her zaman üzerinde yüksek kullanılabilirlik**ve ardından **yeni Kullanılabilirlik Grubu Sihirbazı'nı**hello gösterildiği gibi Aşağıdaki ekran görüntüsü.
   
    ![Yeni Kullanılabilirlik Grubu Sihirbazı'nı başlatın](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665523.gif)
2. Merhaba üzerinde **giriş** sayfasında, **sonraki**. Merhaba üzerinde **kullanılabilirlik grubu adı belirtin** sayfasında, **AG1** içinde **kullanılabilirlik grubu adının**, ardından **sonraki** yeniden.
   
    ![Yeni Kullanılabilirlik Grubu Sihirbazı'nı, kullanılabilirlik grubu adını belirtin](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665524.gif)
3. Merhaba üzerinde **seçin veritabanları** sayfasında **MyDB1**ve ardından **sonraki**. en az bir tam yedekleme hello hedeflenen birincil Çoğaltmada uyguladığınız için hello veritabanı bir kullanılabilirlik grubu için hello önkoşulları karşıladığını.
   
    ![Yeni Availabilty Grubu Sihirbazı'nı seçin veritabanları](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665525.gif)
4. Merhaba üzerinde **çoğaltmaları belirle** sayfasında, **eklemek çoğaltma**.
   
    ![Yeni Availabilty Grubu Sihirbazı, çoğaltmaları belirtin](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665526.gif)
5. Merhaba, **tooServer bağlanmak** iletişim kutusuna **ContosoSQL2** içinde **sunucu adı**ve ardından **Bağlan**.
   
    ![Yeni Availabilty Grubu Sihirbazı'nı Bağlan tooserver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665527.gif)
6. Merhaba üzerinde geri **çoğaltmaları belirle** sayfasında, görmelisiniz **ContosoSQL2** listelenen **kullanılabilir çoğaltmaların**. Merhaba çoğaltmaları hello ekran aşağıdaki gösterildiği gibi yapılandırın. İşiniz bittiğinde, tıklatın **sonraki**.
   
    ![Yeni Availabilty Grubu Sihirbazı'nı belirtin çoğaltmaları (tam)](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665528.gif)
7. Merhaba üzerinde **ilk veri eşitlemesi** sayfasında **yalnızca katılma**ve ardından **sonraki**. Merhaba tam ve işlem yedekleme yapıldığında, zaten veri eşitleme el ile gerçekleştirilen **ContosoSQL1** ve bunları geri **ContosoSQL2**. Yedekleme ve geri yükleme işlemleri, veritabanınızdaki değil tooperform hello seçin ve bunun yerine seçin **tam** toolet hello yeni Kullanılabilirlik Grubu Sihirbazı'nı sizin için veri eşitleme gerçekleştirin. Ancak, bazı şirketler bulunan çok büyük veritabanları için bu seçeneği önermiyoruz.
   
    ![Yeni Availabilty Grubu Sihirbazı'nı, Select ilk veri eşitlemesi](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665529.gif)
8. Merhaba üzerinde **doğrulama** sayfasında, **sonraki**. Bu sayfa aşağıdaki ekran görüntüsüne benzer toohello görünmelidir. Bir kullanılabilirlik grubu dinleyicisi yapılandırılmadığı için hello dinleyici yapılandırması için bir uyarı yok. Bu öğretici bir dinleyici yapılandırmaz çünkü bu uyarıyı yoksayabilirsiniz. Bu öğretici, bkz: tamamladıktan sonra tooconfigure hello dinleyici [Azure'da Always On kullanılabilirlik grupları için bir ILB dinleyicisi yapılandırın](../classic/ps-sql-int-listener.md).
   
    ![Yeni Availabilty Grubu Sihirbazı, doğrulama](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665530.gif)
9. Merhaba üzerinde **Özet** sayfasında, **son**ve ardından hello yeni kullanılabilirlik grubu hello Sihirbazı'nı yapılandırırken bekleyin. Merhaba üzerinde **ilerleme** tıklayabilirsiniz sayfasında, **daha fazla ayrıntı** tooview hello ayrıntılı devam ediyor. Merhaba Sihirbaz sona erdikten sonra hello incelemek **sonuçları** sayfa tooverify bu hello kullanılabilirlik grubu başarıyla hello ekran aşağıdaki gösterildiği gibi oluşturulur ve ardından **Kapat** tooexit hello Sihirbazı.
   
    ![Yeni Availabilty Grubu Sihirbazı'nı sonuçları](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665531.gif)
10. İçinde **Object Explorer**, genişletin **her zaman üzerinde yüksek kullanılabilirlik**, genişletin ve ardından **kullanılabilirlik grupları**. Bu kapsayıcıda yeni kullanılabilirlik grubu hello görmelisiniz. Sağ **AG1 (birincil)**ve ardından **Göster Pano**.
    
     ![Göster kullanılabilirlik grubu Panosu](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665532.gif)
11. **Üzerinde her zaman Pano** görünüm benzer toohello bir hello içinde aşağıdaki ekran görüntüsü. Merhaba çoğaltmaları hello yük devretme modu her çoğaltma ve hello eşitleme durumu görebilirsiniz.
    
     ![Kullanılabilirlik grubu Panosu](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665533.gif)
12. Çok dönmek**Sunucu Yöneticisi'ni**, tıklatın **Araçları**ve ardından açın **yük devretme kümesi Yöneticisi**.
13. Genişletme **Cluster1.corp.contoso.com**, genişletin ve ardından **hizmetler ve uygulamalar**. Seçin **rolleri** ve o hello Not **AG1** kullanılabilirlik grubu rolü oluşturuldu. Dinleyici yapılandırmadı çünkü AG1 hangi veritabanı tarafından toohello kullanılabilirlik grubu, istemcilerin bağlanabileceği bir IP adresi sahip olup olmadığını unutmayın. Okuma-yazma işlemleri için birincil düğüm toohello ve hello ikincil düğüm salt okunur sorgular için doğrudan bağlanabilir.
    
     ![Yük Devretme Kümesi Yöneticisi'nde AG](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665534.gif)

> [!WARNING]
> Toofail hello kullanılabilirlik grubundan hello yük devretme kümesi Yöneticisi üzerinden çalışmayın. Tüm yük devretme işlemlerini içinden gerçekleştirilmelidir **üzerinde her zaman Pano** SQL Server Management Studio'da. Daha fazla bilgi için bkz: [kullanma kısıtlamaları hello yük devretme kümesi Yöneticisi kullanılabilirlik grupları ile](https://msdn.microsoft.com/library/ff929171.aspx).
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Artık başarıyla SQL Server Always On Azure'da bir kullanılabilirlik grubu oluşturarak uyguladık. Bu kullanılabilirlik grubu için bir dinleyici tooconfigure bkz [Azure'da Always On kullanılabilirlik grupları için bir ILB dinleyicisi yapılandırın](../classic/ps-sql-int-listener.md).

Azure'da SQL Server kullanma hakkında diğer bilgi için bkz: [Azure Virtual Machines'de SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

