---
title: "aaaSQL Server kullanılabilirlik gruplarını - Azure sanal makineleri - Öğreticisi | Microsoft Docs"
description: "Bu öğreticide gösterilmiştir nasıl toocreate bir SQL Server her zaman üzerinde kullanılabilirlik grubu Azure sanal makineler üzerinde."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>Yapılandırma her zaman üzerindeki kullanılabilirlik grubu Azure VM'de el ile

Bu öğreticide gösterilmiştir nasıl toocreate bir SQL Server her zaman üzerinde kullanılabilirlik grubu Azure sanal makineler üzerinde. Merhaba tam öğretici iki SQL sunucusu üzerindeki veritabanı çoğaltmasıyla bir kullanılabilirlik grubu oluşturur.

**Zaman tahmin**: hello Önkoşullar sağlandığında yaklaşık 30 dakika toocomplete alır.

Merhaba diyagram hello öğreticide yapı gösterir.

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>Ön koşullar

SQL Server Always On kullanılabilirlik grupları temel bir anlayış Hello öğretici varsayar. Daha fazla bilgi için bkz: [genel bakış, Always On kullanılabilirlik grupları (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Merhaba aşağıdaki tabloda bu öğreticiye başlamadan önce toocomplete gereken hello önkoşulları listeler:

|  |Gereksinim |Açıklama |
|----- |----- |----- |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | İki SQL sunucuları | -Bir Azure kullanılabilirlik kümesine <br/> -Tek bir etki alanı <br/> -Yük Devretme Kümelemesi özelliği yüklü olan |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | Küme Tanık dosya paylaşımı |  
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|SQL Server hizmet hesabı | Etki alanı hesabı |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|SQL Server Aracısı hizmet hesabı | Etki alanı hesabı |  
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Güvenlik Duvarı bağlantı noktalarını açın | -SQL Server: **1433** varsayılan örnek için <br/> -Veritabanı yansıtma uç noktası: **5022** veya tüm kullanılabilir bağlantı noktası <br/> -Azure yük dengeleyici araştırmasını: **59999** veya tüm kullanılabilir bağlantı noktası |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Yük Devretme Kümelemesi özelliği Ekle | Bu özellik, her iki SQL sunucuları gerektirir |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Yükleme etki alanı hesabı | -Her bir SQL Server yerel yönetici <br/> -Her SQL Server örneği için SQL Server sysadmin sabit sunucu rolünün üyesi  |


Merhaba öğreticiye başlamadan önce çok ihtiyacınız[tamamlamak Azure sanal makinelerinde Always On kullanılabilirlik grupları oluşturmak için Önkoşullar](virtual-machines-windows-portal-sql-availability-group-prereq.md). Bu Önkoşullar zaten tamamladıysanız, sizin çok atlayabilirsiniz[küme oluşturma](#CreateCluster).


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Merhaba kümesi oluşturma

Hello Önkoşullar tamamlandıktan sonra hello ilk toocreate iki SQL Server'lar içeren Windows Server Yük devretme kümesi ve bir Tanık adımdır.  

1. RDP toohello SQL sunucuları ve hello Tanık sunucu üzerindeki bir yönetici olan bir etki alanı hesabı kullanarak ilk SQL Server.

   >[!TIP]
   >Merhaba izlediyseniz [önkoşul belgesi](virtual-machines-windows-portal-sql-availability-group-prereq.md), adlı bir hesap oluşturulan **CORP\Install**. Bu hesabı kullanın.

2. Merhaba, **Sunucu Yöneticisi'ni** Pano, select **Araçları**ve ardından **yük devretme kümesi Yöneticisi**.
3. Merhaba sol bölmesinde, **yük devretme kümesi Yöneticisi**ve ardından **bir küme oluşturmak**.
   ![Küme oluşturma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. Buna küme oluşturma Sihirbazı'nı Merhaba, aşağıdaki tablonun hello hello ayarlarla hello sayfalarıyla adımla tek düğümlü bir küme oluşturun:

   | Sayfa | Ayarlar |
   | --- | --- |
   | Başlamadan önce |Varsayılanları kullanın |
   | Sunucuları seçin |İlk SQL Server adı türü hello **sunucu adını girin** tıklatıp **Ekle**. |
   | Doğrulama uyarısı |Seçin **ı bu küme için Microsoft desteğine gereksiniminiz ve bu nedenle toorun hello doğrulama istemiyorsanız Hayır sınar. Sonraki tıkladığınızda, hello küme oluşturmaya devam etmek**. |
   | Yönetme hello küme için erişim noktası |Bir küme adı yazın, örneğin **SQLAGCluster1** içinde **küme adı**.|
   | Onay |Depolama alanları kullanmadığınız sürece varsayılan ayarları kullanın. Bu tablodan sonraki hello nota bakın. |

### <a name="set-hello-cluster-ip-address"></a>Merhaba küme IP adresi ayarlayın

1. İçinde **yük devretme kümesi Yöneticisi**, çok ilerleyin**küme çekirdek kaynakları** ve hello küme Ayrıntıları'nı genişletin. Her iki hello görmelisiniz **adı** ve hello **IP adresi** hello kaynaklarında **başarısız** durumu. Merhaba küme hello atandığından hello IP adresi kaynağı çevrimiçi duruma getirilemiyor aynı IP adresi hello makine olarak kendisi, bu nedenle, bir yinelenen adresidir.

2. Başarısız sağ hello **IP adresi** kaynak ve ardından **özellikleri**.

   ![Küme Özellikleri](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. Seçin **statik IP adresi** ve kullanılabilir bir hello SQL Server hello adresi metin kutusuna olduğu alt ağ adresi belirtin. Ardından **Tamam**.
4. Merhaba, **küme çekirdek kaynakları** bölümünde, küme adını sağ tıklatın ve **çevrimiçine**. Daha sonra her iki kaynağın çevrimiçi olana kadar bekleyin. Merhaba küme adı kaynağını çevrimiçi olduğunda hello DC sunucusuna yeni bir AD bilgisayar hesabı ile güncelleştirir. Bu AD hesabı toorun hello daha sonra kullanılabilirlik grubu kümelenmiş hizmet kullanın.

### <a name="addNode"></a>Ekleme diğer SQL Server toocluster hello

Ekleme diğer SQL Server toohello küme hello.

1. Merhaba tarayıcı ağacında hello kümeye sağ tıklayın ve **düğüm Ekle**.

    ![Küme düğümü toohello Ekle](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. Merhaba, **Düğüm Ekleme Sihirbazı'nı**, tıklatın **sonraki**. Merhaba, **sunucuları Seç** sayfasında, eklemek ikinci SQL Server hello. Tür hello sunucu adı **sunucu adını girin** ve ardından **Ekle**. İşiniz bittiğinde tıklatın **sonraki**.

1. Merhaba, **doğrulama uyarısı** sayfasında, **Hayır** (bir üretim senaryosunda, hello doğrulama testleri gerçekleştirmeniz gerekir). Ardından **İleri**'ye tıklayın.

8. Merhaba, **onay** depolama alanları, etiketli Temizle hello onay kutusunu kullanıyorsanız, sayfa **tüm uygun depolama toohello küme ekleyin.**

   ![Düğüm onay Ekle](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >Depolama alanları kullanma ve değil işaretini **tüm uygun depolama toohello küme eklemek**, Windows hello kümeleme işlemi sırasında hello sanal diskler ayırır. Sonuç olarak, hello depolama alanları hello kümeden kaldırılana kadar Disk Yöneticisi'nde veya Explorer görünmez ve PowerShell kullanarak yeniden. Depolama alanları, birden çok disk toostorage havuzlarında gruplandırır. Daha fazla bilgi için bkz: [depolama alanları](https://technet.microsoft.com/library/hh831739).

1. **İleri**’ye tıklayın.

1. **Son**'a tıklayın.

   Yük Devretme Kümesi Yöneticisi'ni gösterir kümenizi yeni bir düğüm ve hello listeler **düğümleri** kapsayıcı.

10. Merhaba Uzak Masaüstü oturumunu kapatmak.

### <a name="add-a-cluster-quorum-file-share"></a>Bir küme çekirdek dosya paylaşımı Ekle

Bu örnekte, bir dosya paylaşımı toocreate Küme çekirdeğini hello Windows kümesi kullanır. Bu öğretici, bir düğüm ve dosya paylaşımı çoğunluğu çekirdek kullanır. Daha fazla bilgi için bkz: [yük devretme kümesindeki çekirdek yapılandırmalarını anlama](http://technet.microsoft.com/library/cc731739.aspx).

1. Toohello dosya paylaşımı tanığı üye sunucusu ile Uzak Masaüstü oturumu bağlayın.

1. Üzerinde **Sunucu Yöneticisi'ni**, tıklatın **Araçları**. Açık **Bilgisayar Yönetimi**.

1. Tıklatın **paylaşılan klasörleri**.

1. Sağ **paylaşımları**, tıklatıp **yeni paylaşım...** .

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Kullanım **bir paylaşılan klasör oluşturma Sihirbazı** toocreate bir paylaşımı.

1. Üzerinde **klasör yolu**, tıklatın **Gözat** ve bulun veya hello paylaşılan klasör için bir yol oluşturun. **İleri**’ye tıklayın.

1. İçinde **adı, açıklama ve ayarları** hello paylaşım adını ve yolunu doğrulayın. **İleri**’ye tıklayın.

1. Üzerinde **paylaşılan klasör izinlerini** ayarlamak **izinleri Özelleştir**. Tıklatın **özel...** .

1. Üzerinde **izinleri Özelleştir**, tıklatın **Ekle...** .

1. Tam Denetim bu hello kullanılan hesap toocreate hello küme olduğundan emin olun.

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. **Tamam** düğmesine tıklayın.

1. İçinde **paylaşılan klasör izinlerini**, tıklatın **son**. Tıklatın **son** yeniden.  

1. Merhaba sunucu dışında oturum

### <a name="configure-cluster-quorum"></a>Küme çekirdeğini yapılandırın

Ardından, hello Küme çekirdeğini ayarlayın.

1. Toohello ilk küme düğümüne Uzak Masaüstü'nü bağlayın.

1. İçinde **yük devretme kümesi Yöneticisi**, hello kümeye sağ tıklayın, çok noktası**diğer eylemler**, tıklatıp **küme çekirdek ayarlarını yapılandır...** .

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. İçinde **küme çekirdeği Yapılandırma Sihirbazı**, tıklatın **sonraki**.

1. İçinde **çekirdek yapılandırma seçeneğini**, seçin **hello çekirdek tanığı Seç**, tıklatıp **sonraki**.

1. Üzerinde **çekirdek tanığı Seç**, tıklatın **bir dosya paylaşımı tanığı Yapılandır**.

   >[!TIP]
   >Windows Server 2016 bulut Tanık destekler. Bu tür bir Tanık seçerseniz, bir dosya gerekmez paylaşımı tanığını. Daha fazla bilgi için bkz: [bir yük devretme kümesi için bir bulut tanığı dağıtmak](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness). Bu öğretici, önceki işletim sistemleri tarafından desteklenen bir dosya paylaşımı tanığı kullanır.

1. Üzerinde **dosya paylaşımı Tanığını Yapılandır**, oluşturduğunuz hello paylaşımı için hello yolunu yazın. **İleri**’ye tıklayın.

1. Hello ayarlarını doğrulayın **onay**. **İleri**’ye tıklayın.

1. **Son**'a tıklayın.

Merhaba küme çekirdek kaynakları dosya paylaşım tanığı ile yapılandırılır.

## <a name="enable-availability-groups"></a>Kullanılabilirlik gruplarını etkinleştir

Ardından, hello etkinleştirmek **AlwaysOn Kullanılabilirlik grupları** özelliği. Her iki SQL sunucularında bu adımları uygulayın.

1. Merhaba gelen **Başlat** ekranında, başlatma **SQL Server Configuration Manager**.
2. Merhaba tarayıcı ağacında tıklayın **SQL Server Hizmetleri**, hello sağ tıklatın **SQL Server (MSSQLSERVER)** 'ı tıklatın ve hizmeti **özellikleri**.
3. Merhaba tıklatın **AlwaysOn yüksek kullanılabilirlik** sekmesini ve ardından **etkinleştirmek AlwaysOn Kullanılabilirlik grupları**aşağıdaki gibi:

    ![AlwaysOn Kullanılabilirlik gruplarını etkinleştir](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. **Uygula**'ya tıklayın. Tıklatın **Tamam** hello açılan iletişim kutusunda.

5. Merhaba SQL Server hizmetini yeniden başlatın.

Diğer SQL Server hello bu adımları yineleyin.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Bir veritabanı üzerinde hello oluşturmak ilk SQL Server

1. Başlatma hello RDP dosyası toohello ilk SQL Server ile bir etki alanı hesabı başka bir deyişle bir üyesi sysadmin sabit sunucu rolü.
1. SQL Server Management Studio'yu açın ve toohello bağlanın ilk SQL Server.
7. İçinde **Object Explorer**, sağ **veritabanları** tıklatıp **yeni veritabanı**.
8. İçinde **veritabanı adı**, türü **MyDB1**, ardından **Tamam**.

### <a name="backupshare"></a>Bir yedekleme paylaşımı oluşturun

1. Üzerinde ilk SQL Server'da hello **Sunucu Yöneticisi'ni**, tıklatın **Araçları**. Açık **Bilgisayar Yönetimi**.

1. Tıklatın **paylaşılan klasörleri**.

1. Sağ **paylaşımları**, tıklatıp **yeni paylaşım...** .

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Kullanım **bir paylaşılan klasör oluşturma Sihirbazı** toocreate bir paylaşımı.

1. Üzerinde **klasör yolu**, tıklatın **Gözat** ve bulun veya hello veritabanı yedekleme paylaşılan klasörü için bir yol oluşturun. **İleri**’ye tıklayın.

1. İçinde **adı, açıklama ve ayarları** hello paylaşım adını ve yolunu doğrulayın. **İleri**’ye tıklayın.

1. Üzerinde **paylaşılan klasör izinlerini** ayarlamak **izinleri Özelleştir**. Tıklatın **özel...** .

1. Üzerinde **izinleri Özelleştir**, tıklatın **Ekle...** .

1. Her iki sunucuyu Hello SQL Server ve SQL Server Aracısı hizmet hesaplarını tam denetime sahip olduğunuzdan emin olun.

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. **Tamam** düğmesine tıklayın.

1. İçinde **paylaşılan klasör izinlerini**, tıklatın **son**. Tıklatın **son** yeniden.  

### <a name="take-a-full-backup-of-hello-database"></a>Tam hello veritabanı yedek alın

Merhaba yeni veritabanı tooinitialize hello günlük zinciri yukarı tooback gerekir. Merhaba yeni veritabanının bir yedeğini almazsanız, bir kullanılabilirlik grubuna eklenemez.

1. İçinde **Object Explorer**, hello veritabanını sağ tıklatın, çok noktası**görevleri...** , tıklatın **yedekleme**.

1. Tıklatın **Tamam** tootake tam yedekleme toohello varsayılan yedekleme konumu.

## <a name="create-hello-availability-group"></a>Merhaba kullanılabilirlik grubu oluşturma
Aşağıdaki hello kullanarak bir kullanılabilirlik grubu adımları hazır tooconfigure sunulmuştur:

* Bir veritabanı üzerinde hello oluşturmak ilk SQL Server.
* Tam yedekleme ve hello veritabanının işlem günlüğü yedeklemesi gerçekleştirin
* Tam geri yükleme hello ve SQL Server ile Merhaba ikinci günlük yedekleri toohello **NORECOVERY** seçeneği
* Merhaba kullanılabilirlik grubu oluşturun (**AG1**) zaman uyumlu tamamlama, otomatik yük devretme ve okunabilir ikincil çoğaltmalarda

### <a name="create-hello-availability-group"></a>Merhaba kullanılabilirlik grubu oluşturun:

1. Uzak Masaüstü oturumu toohello üzerinde ilk SQL Server. İçinde **Object Explorer** SSMS, sağ **AlwaysOn yüksek kullanılabilirlik** tıklatıp **yeni Kullanılabilirlik Grubu Sihirbazı'nı**.

    ![Yeni kullanılabilirlik grubu sihirbazını başlat](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. Merhaba, **giriş** sayfasında, **sonraki**. Merhaba, **kullanılabilirlik grubu adı belirtin** sayfasında, hello kullanılabilirlik grubu için bir ad yazın, örneğin **AG1**, **kullanılabilirlik grubu adının**. **İleri**’ye tıklayın.

    ![Yeni AG Sihirbazı, AG adını belirtin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. Merhaba, **veritabanlarını seçin** sayfasında Veritabanınızı seçin ve tıklayın **sonraki**.

   >[!NOTE]
   >en az bir tam yedekleme hello hedeflenen birincil Çoğaltmada uyguladığınız için hello veritabanı bir kullanılabilirlik grubu için hello önkoşulları karşıladığını.

   ![Yeni AG Sihirbazı, veritabanlarını seçin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. Merhaba, **çoğaltmaları belirle** sayfasında, **eklemek çoğaltma**.

   ![Yeni AG Sihirbazı, çoğaltmaları belirtin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. Merhaba **tooServer bağlanmak** iletişim kutusu açılır. Merhaba ikinci sunucusunun türü hello adı **sunucu adı**. **Bağlan**'a tıklayın.

   Merhaba edilene **çoğaltmaları belirle** sayfasında, listelenen hello ikinci sunucu artık görmelisiniz **kullanılabilirlik çoğaltmalarının**. Merhaba çoğaltmaları şu şekilde yapılandırın.

   ![Yeni AG Sihirbazı, çoğaltmaları belirtin (tam)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. Tıklatın **uç noktaları** toosee hello veritabanı yansıtma uç noktası bu kullanılabilirlik grubu için. Aynı bağlantı noktası hello ayarlarken kullandığınız kullanım hello [veritabanı yansıtma uç noktaları için güvenlik duvarı kuralı](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

    ![Yeni AG Sihirbazı, ilk veri eşitlemeyi seçin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. Merhaba, **ilk veri eşitlemesi** sayfasında **tam** ve paylaşılan bir ağ konumu belirtin. Merhaba Hello konumu için kullanmanız [oluşturduğunuz yedekleme paylaşımı](#backupshare). Merhaba örnekte olduğu, **\\\\\<ilk SQL Server\>\Backup\**. **İleri**’ye tıklayın.

   >[!NOTE]
   >Tam eşitleme hello veritabanı hello ilk SQL Server örneği üzerinde tam yedeğini alır ve toohello ikinci örneği geri yükler. Büyük veritabanları için tam eşitleme önerilmez uzun bir süre devam edebilir. El ile Merhaba veritabanının bir yedeğini almak ve onunla geri yükleme bu kez azaltabilir `NO RECOVERY`. Merhaba veritabanı zaten ile geri yüklenirse `NO RECOVERY` hello ikinci SQL Server kullanılabilirlik grubu hello yapılandırmadan önce seçin **yalnızca katmak**. Merhaba kullanılabilirlik grubu yapılandırdıktan sonra tootake hello yedekleme istiyorsanız, tercih **ilk veri eşitlemeyi atla**.

    ![Yeni AG Sihirbazı, ilk veri eşitlemeyi seçin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. Merhaba, **doğrulama** sayfasında, **sonraki**. Bu sayfayı benzer toohello görüntü aşağıdaki gibi görünmelidir:

    ![Yeni AG Sihirbazı, doğrulama](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >Bir kullanılabilirlik grubu dinleyicisi yapılandırılmadığı için hello dinleyici yapılandırması için bir uyarı yok. Azure sanal makinelerde, hello dinleyicisi hello Azure yük dengeleyici oluşturduktan sonra oluşturduğundan bu uyarıyı yoksayabilirsiniz.

10. Merhaba, **Özet** sayfasında, **son**, Başlangıç Sihirbazı'nı yapılandırırken bekleyin hello sonra yeni kullanılabilirlik grubu. Merhaba, **ilerleme** tıklayabilirsiniz sayfasında, **daha fazla ayrıntı** tooview hello ayrıntılı devam ediyor. Merhaba Sihirbaz tamamlandıktan sonra hello incelemek **sonuçları** kullanılabilirlik grubu hello sayfa tooverify başarıyla oluşturuldu.

     ![Yeni AG Sihirbazı, sonuçlar](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. Tıklatın **Kapat** tooexit hello Sihirbazı.

### <a name="check-hello-availability-group"></a>Onay hello kullanılabilirlik grubu

1. İçinde **Object Explorer**, genişletin **AlwaysOn yüksek kullanılabilirlik**, ardından **kullanılabilirlik grupları**. Artık görmelisiniz bu kapsayıcıda yeni kullanılabilirlik grubu hello. Merhaba kullanılabilirlik grubunu sağ tıklatın ve **Göster Pano**.

   ![AG panosunu Göster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   **AlwaysOn panosunu** benzer toothis görünmelidir.

   ![AG Panosu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   Merhaba çoğaltmalar, her çoğaltma ve hello eşitleme durumunun hello yük devretme modu görebilirsiniz.

2. İçinde **yük devretme kümesi Yöneticisi**, kümenizi'ı tıklatın. Seçin **rolleri**. kullandığınız hello kullanılabilirlik grubu adını hello kümede bir roldür. Bu kullanılabilirlik grubu dinleyici yapılandırmadı olduğundan istemci bağlantıları için bir IP adresi yok. Bir Azure yük dengeleyici oluşturduktan sonra hello dinleyicisi yapılandırır.

   ![Yük Devretme Kümesi Yöneticisi'nde AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > Toofail hello yük devretme kümesi Yöneticisi'nden hello kullanılabilirlik grubu üzerinden çalışmayın. Tüm yük devretme işlemlerini içinden gerçekleştirilmelidir **AlwaysOn panosunu** SSMS içinde. Daha fazla bilgi için bkz: [kullanma kısıtlamaları hello yük devretme kümesi Yöneticisi kullanılabilirlik grupları ile](https://msdn.microsoft.com/library/ff929171.aspx).
    >

Bu noktada, çoğaltmalar SQL Server'ın iki örneği üzerinde kullanılabilirlik grubuyla sahip. Merhaba kullanılabilirlik grubu örnekleri arasında taşıyabilirsiniz. Dinleyici olmadığından toohello kullanılabilirlik grubu henüz bağlanamıyor. Azure sanal makinelerinde hello dinleyicisi bir yük dengeleyici gerektirir. Merhaba sonraki toocreate hello yük dengeleyici Azure adımdır.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Bir Azure yük dengeleyici oluşturma

Azure sanal makinelerde SQL Server kullanılabilirlik grubu yük dengeleyici gerektirir. Merhaba yük dengeleyici hello kullanılabilirlik grubu dinleyicisi için başlangıç IP adresi tutar. Bu bölümde, nasıl toocreate hello yük dengeleyici hello Azure portal'ın özetlenmektedir.

1. Burada, SQL sunucuları ve tıklatın toohello kaynak grubu Hello Azure portal, Git **+ Ekle**.
2. Arama **yük dengeleyici**. Microsoft tarafından yayımlanan hello yük dengeleyici seçin.

   ![Yük Devretme Kümesi Yöneticisi'nde AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  **Oluştur**'a tıklayın.
3. Şu parametreler hello yük dengeleyici için hello yapılandırın.

   | Ayar | Alan |
   | --- | --- |
   | **Ad** |Hello yük dengeleyici için bir metin adı kullanın örneğin **sqlLB**. |
   | **Tür** |İç |
   | **Sanal ağ** |Hello Azure sanal ağı Hello adını kullanın. |
   | **Alt ağ** |Sanal makine hello hello alt ağın kullanım hello adı kullanılıyor.  |
   | **IP adresi ataması** |Statik |
   | **IP adresi** |Kullanılabilir bir alt ağ adresi kullanın. |
   | **Abonelik** |Kullanım hello aynı abonelik hello sanal makine olarak. |
   | **Konum** |Kullanım hello aynı konumu hello sanal makine olarak. |

   Azure portal dikey penceresinde Hello aşağıdaki gibi görünmelidir:

   ![Yük Dengeleyici oluşturma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. Tıklatın **oluşturma**, toocreate hello yük dengeleyici.

tooconfigure hello yük dengeleyici, toocreate bir arka uç havuzu, araştırma ve kümesi hello Yük Dengeleme kuralları gerekir. Bu hello Azure portal yapın.

### <a name="add-backend-pool"></a>Arka uç havuzu ekleme

1. Hello Azure portal, tooyour kullanılabilirlik grubu gidin. Toorefresh hello görünüm toosee hello yeni oluşturulan yük dengeleyici gerekebilir.

   ![Yük Dengeleyici kaynak grubunda bulunamadı](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Merhaba yük dengeleyici tıklatın, **arka uç havuzları**, tıklatıp **+ Ekle**. Merhaba arka uç havuzu aşağıdaki gibi ayarlayın:

   | Ayar | Açıklama | Örnek
   | --- | --- |---
   | **Ad** | Bir metin yazın | SQLLBBE
   | **İle ilişkili** | Listeden seçin | Kullanılabilirlik kümesi
   | **Kullanılabilirlik kümesi** | SQL Server Vm'lerinin bulunan hello kullanılabilirlik kümesi adını kullanın | sqlAvailabilitySet |
   | **Sanal makineler** |Merhaba iki Azure SQL Server VM adları | SQLServer-0, sqlserver-1

1. Merhaba hello arka uç havuzu için bir ad yazın.

1. Tıklatın **+ bir sanal makine Ekle**.

1. Merhaba kullanılabilirlik kümesi için SQL sunucusu olduğundan bu hello hello kullanılabilirlik kümesi'ni seçin.

1. Sanal makineler için ikisi de hello SQL sunucuları içerir. Merhaba dosya paylaşımı tanığı sunucusu içermez.

1. Tıklatın **Tamam** toocreate hello arka uç havuzu.

### <a name="set-hello-probe"></a>Kümesi hello araştırması

1. Merhaba yük dengeleyici tıklatın, **sistem durumu araştırmalarının**, tıklatıp **+ Ekle**.

1. Merhaba durumu araştırması aşağıdaki gibi ayarlayın:

   | Ayar | Açıklama | Örnek
   | --- | --- |---
   | **Ad** | Metin | SQLAlwaysOnEndPointProbe |
   | **Protokol** | TCP seçin | TCP |
   | **Bağlantı Noktası** | Kullanılmayan bir bağlantı noktası | 59999 |
   | **Aralığı**  | saniye cinsinden araştırma arasındaki süre miktarı Hello çalışır |5 |
   | **Sağlıksız durum eşiği.** | Merhaba sağlıksız kabul bir sanal makine toobe için oluşması gereken arka arkaya araştırma hatası sayısı  | 2 |

1. Tıklatın **Tamam** tooset hello durumu araştırması.

### <a name="set-hello-load-balancing-rules"></a>Merhaba Yük Dengeleme kuralları ayarlama

1. Merhaba yük dengeleyici tıklatın, **Yük Dengeleme kuralları**, tıklatıp **+ Ekle**.

1. Merhaba Yük Dengeleme kuralları aşağıdaki gibi ayarlayın.
   | Ayar | Açıklama | Örnek
   | --- | --- |---
   | **Ad** | Metin | SQLAlwaysOnEndPointListener |
   | **Ön uç IP adresi** | Adres seçin |Merhaba yük dengeleyici oluşturduğunuz sırada oluşturduğunuz hello adresi kullanın. |
   | **Protokol** | TCP seçin |TCP |
   | **Bağlantı Noktası** | Merhaba SQL Server örneği için başlangıç bağlantı noktası kullanma | 1433 |
   | **Arka uç bağlantı noktası** | Kayan IP için doğrudan sunucu dönüş ayarladığınızda, bu alan kullanılmıyor | 1433 |
   | **Araştırma** |Merhaba araştırması için belirtilen hello adı | SQLAlwaysOnEndPointProbe |
   | **Oturum kalıcılığı** | Açılan liste | **Yok** |
   | **Boşta kalma zaman aşımı** | Bir TCP bağlantı açmak dakika tookeep | 4 |
   | **Kayan IP (doğrudan sunucu dönüşü)** | |Etkin |

   > [!WARNING]
   > Doğrudan sunucu dönüşü oluşturma sırasında ayarlanır. Değiştirilemez.

1. Tıklatın **Tamam** tooset hello Yük Dengeleme kuralları.

## <a name="configure-listener"></a>Merhaba dinleyicisini yapılandırın

Merhaba sonraki şey toodo tooconfigure hello yük devretme kümesindeki bir kullanılabilirlik grubu dinleyicisi ' dir.

> [!NOTE]
> Bu öğretici nasıl toocreate tek bir dinleyici - bir ILB'nin IP adresini gösterir. bir veya daha fazla IP adresi kullanarak bir veya daha fazla dinleyicileri toocreate bakın [oluşturma kullanılabilirlik grubu dinleyici ve yük dengeleyici | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>Set dinleyicisi bağlantı noktası

SQL Server Management Studio'da hello dinleyicisi bağlantı noktası ayarlayın.

1. SQL Server Management Studio'yu başlatın ve toohello birincil çoğaltma bağlanın.

1. Çok gidin**AlwaysOn yüksek kullanılabilirlik** | **kullanılabilirlik grupları** | **kullanılabilirlik grubu dinleyicileri**.

1. Yük Devretme Kümesi Yöneticisi'nde oluşturulan hello dinleyici adı görmelisiniz. Merhaba dinleyicisi adını sağ tıklatıp **özellikleri**.

1. Merhaba, **bağlantı noktası** kutusunda, daha önce kullandığınız $EndpointPort hello kullanarak hello hello kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (1433 olduğu hello varsayılan), ardından **Tamam**.

Artık Azure sanal makinelerde Kaynak Yöneticisi modunda çalışan bir SQL Server kullanılabilirlik grubu vardır.

## <a name="test-connection-toolistener"></a>Test bağlantısı toolistener

tootest hello bağlantısı:

1. RDP tooa hello SQL Server aynı sanal ağ, ancak kendi hello çoğaltma. Kullanabileceğiniz diğer SQL Server hello kümedeki hello.

1. Kullanım **sqlcmd** yardımcı programı tootest hello bağlantı. Örneğin, komut dosyası izleyen hello kurar bir **sqlcmd** bağlantı toohello birincil çoğaltma Windows kimlik doğrulaması ile Merhaba dinleyicisi aracılığıyla:

    ```
    sqlcmd -S <listenerName> -E
    ```

    Merhaba dinleyicisi dışında bir bağlantı noktası kullanıyorsa, varsayılan hello (1433) bağlantı noktası, başlangıç bağlantı noktası başlangıç bağlantı dizesinde belirtin. Örneğin, hello aşağıdaki sqlcmd komut tooa dinleyicisi bağlantı noktası 1435 bağlanır:

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Merhaba SQLCMD bağlantı toowhichever örneğini SQL Server konakları hello birincil çoğaltma otomatik olarak bağlanır.

> [!TIP]
> Belirttiğiniz başlangıç bağlantı noktası hem SQL sunucuları hello güvenlik duvarı açık olduğundan emin olun. Her iki sunucuyu hello kullandığınız TCP bağlantı noktası için bir gelen kuralı gerektirir. Daha fazla bilgi için bkz: [Ekle veya Düzenle güvenlik duvarı kuralı](http://technet.microsoft.com/library/cc753558.aspx).
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>Sonraki adımlar

- [İkinci bir kullanılabilirlik grubu için bir IP adresi tooa yük dengeleyici eklemek](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).
