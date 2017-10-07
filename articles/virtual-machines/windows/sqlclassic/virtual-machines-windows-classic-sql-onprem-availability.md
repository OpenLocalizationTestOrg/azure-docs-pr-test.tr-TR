---
title: "aaaExtend şirket içi Always On kullanılabilirlik grupları tooAzure | Microsoft Docs"
description: "Bu öğretici hello Klasik dağıtım modeli kullanılarak oluşturulmuş kaynaklarını kullanır ve nasıl toouse hello çoğaltma Ekleme Sihirbazı'nda SQL Server Management Studio (SSMS) tooadd her zaman üzerindeki kullanılabilirlik grubu çoğaltması Azure açıklar."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 7ca7c423-8342-4175-a70b-d5101dfb7f23
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 51fe117b40d69706b35f30101538a7a36116e128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-on-premises-always-on-availability-groups-tooazure"></a>Şirket içi Always On kullanılabilirlik grupları tooAzure genişletme
Always On kullanılabilirlik grupları ikincil çoğaltmaları ekleyerek veritabanının grupları için yüksek kullanılabilirlik sağlar. Bu çoğaltmalar izin arıza durumunda veritabanlarını yük devrediliyor. Ayrıca, iş yükleri veya yedekleme görevlerini okuma kullanılan toooffload olabilir.

Bir veya daha fazla Azure Vm'lerde SQL Server ile sağlama ve çoğaltmaları tooyour kullanılabilirlik grupları şirket içi olarak bunları eklendiğinde, şirket içi kullanılabilirlik grupları tooMicrosoft Azure genişletebilirsiniz.

Bu öğretici hello aşağıdaki olduğu varsayılır:

* Etkin bir Azure aboneliği. Yapabilecekleriniz [ücretsiz deneme için kaydolun](https://azure.microsoft.com/pricing/free-trial/).
* Varolan her zaman üzerinde kullanılabilirlik grubunu şirket içi. Kullanılabilirlik grupları hakkında daha fazla bilgi için bkz: [Always On kullanılabilirlik grupları](https://msdn.microsoft.com/library/hh510230.aspx).
* Merhaba arasındaki bağlantıyı Ağ ve Azure sanal ağınıza şirket içi. Bu sanal ağ oluşturma hakkında daha fazla bilgi için bkz: [oluşturma bir Site siteye bağlantıyı kullanarak Azure portalında (Klasik) hello](../../../vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal.md).

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

## <a name="add-azure-replica-wizard"></a>Azure Yineleme Sihirbazı Ekle
Bu bölümde, nasıl gösterilir toouse hello **Azure çoğaltma Ekleme Sihirbazı'nı** tooextend her zaman üzerindeki kullanılabilirlik grubu çözüm tooinclude Azure çoğaltmaları.

> [!IMPORTANT]
> Merhaba **Azure çoğaltma Ekleme Sihirbazı'nı** yalnızca hello Klasik dağıtım modeliyle oluşturulan sanal makineleri destekler. Yeni VM dağıtımlarının hello yeni Resource Manager modeli kullanmanız gerekir. Resource Manager ile VM kullanıyorsanız hello ikincil Azure çoğaltma Transact-SQL commmands (burada gösterilmiyor) kullanarak el ile eklemelisiniz. Bu sihirbaz hello Resource Manager senaryoda çalışmaz.

1. Gelen SQL Server Management Studio içinde genişletin **her zaman üzerinde yüksek kullanılabilirlik** > **kullanılabilirlik grupları** > **[kullanılabilirlik grubu adı]**.
2. Sağ **kullanılabilirlik çoğaltmalarının**, ardından **eklemek çoğaltma**.
3. Varsayılan olarak, hello **eklemek çoğaltma tooAvailability Grubu Sihirbazı'nı** görüntülenir. **İleri**’ye tıklayın.  Merhaba seçtiyseniz **bu sayfayı bir daha gösterme** tasarrufunda hello sayfanın hello önceki başlatma sırasında bu sihirbaz, bu ekranda görüntülenmez.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742861.png)
4. Gerekli tooconnect tooall mevcut ikincil çoğaltmaları olacaktır. Tıklatabilirsiniz **Bağlan...** her yineleme veya tıklatabilirsiniz **bağlanmak tüm...** Merhaba ekranın hello altında. Sonra kimlik doğrulaması **sonraki** tooadvance toohello sonraki ekranda.
5. Merhaba üzerinde **çoğaltmaları belirle** sayfasında, birden fazla sekme hello üstte listelenir: **çoğaltmaları**, **uç noktaları**, **yedekleme tercihlerine**, ve **Dinleyici**. Merhaba gelen **çoğaltmaları** sekmesini tıklatın, **Azure çoğaltma Ekle...** toolaunch hello Azure çoğaltma Ekleme Sihirbazı.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742863.png)
6. Önce bir yüklediyseniz hello yerel Windows sertifika depolama alanından olan bir Azure yönetim sertifikasını seçin. Önce bir kullandıysanız, Azure aboneliği hello kimliğini girin veya seçin. İndirme toodownload'ı tıklatın ve bir Azure yönetim sertifikasını yükleyin ve bir Azure hesabı kullanarak abonelikleri hello listesini indirir.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742864.png)
7. Her bir alan hello sayfasında kullanılan toocreate hello Azure sanal makine (Merhaba çoğaltmasını barındıracak VM) olacak değerleriyle dolduracaktır.
   
   | Ayar | Açıklama |
   | --- | --- |
   | **Görüntü** |İşletim sistemi ve SQL Server'ın istenen hello birleşimi seçin |
   | **VM boyutu** |Merhaba, iş gereksinimlerinize en uygun VM boyutunu seçin |
   | **VM adı** |Hello için benzersiz bir ad belirtin yeni VM. Merhaba adı gerekir 3 ile 15 karakter arasında içeren, yalnızca harf, rakam ve tire içerebilir ve gerekir bir harfle başlamalı ve harf veya sayı ile bitmelidir. |
   | **VM kullanıcı adı** |Merhaba VM hello yönetici hesabı olacaktır bir kullanıcı adı belirtin |
   | **VM yönetici parolası** |Merhaba yeni hesap için bir parola belirtin |
   | **Parolayı onaylayın** |Merhaba yeni hesabın Hello parolayı onaylayın |
   | **Sanal Ağ** |Azure sanal ağ yeni VM kullanması gereken bu hello hello belirtin. Sanal ağlar hakkında daha fazla bilgi için bkz: [Virtual Network'e genel bakış](../../../virtual-network/virtual-networks-overview.md). |
   | **Sanal ağ alt ağı** |Yeni VM kullanması gereken bu hello Hello sanal ağ alt ağını belirtin |
   | **Etki alanı** |Merhaba önceden doldurulmuş haldedir değeri hello etki alanı için doğru olduğunu onaylayın |
   | **Etki alanı kullanıcı adı** |Merhaba yerel küme düğümlerinde hello yerel Yöneticiler grubunda olan bir hesabı belirtin |
   | **Parola** |Merhaba hello etki alanı kullanıcı adı parolasını belirtin |
8. Tıklatın **Tamam** toovalidate hello dağıtım ayarları.
9. Yasal koşullar sonraki görüntülenir. Okuma ve tıklatın **Tamam** toothese onaylıyorsanız koşulları.
10. Merhaba **çoğaltmaları belirle** sayfası yeniden görüntülenir. Yeni Azure Çoğaltmada hello hello Hello ayarları doğrulama **çoğaltmaları**, **uç noktaları**, ve **yedekleme tercihlerine** sekmeleri. Ayarları toomeet iş gereksinimlerinizi değiştirin.  Bu sekmelerde bulunan hello parametreleri hakkında daha fazla bilgi için bkz: [çoğaltmaları sayfası belirtin (yeni Kullanılabilirlik Grubu Sihirbazı'nı / Add çoğaltma Sihirbazı)](https://msdn.microsoft.com/library/hh213088.aspx). Dinleyicileri kullanılabilirlik grupları için Azure çoğaltmaları içeren hello dinleyicisi sekmesini kullanarak oluşturulamıyor unutmayın. Ayrıca, bir dinleyici önceki toolaunching hello Sihirbazı oluşturduysanız, Azure'da desteklenmiyor belirten bir ileti alırsınız. Nasıl tümleştirildiği incelenmektedir toocreate dinleyicileri hello içinde **bir kullanılabilirlik grubu dinleyicisi oluşturma** bölümü.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742865.png)
11. **İleri**’ye tıklayın.
12. Merhaba üzerinde toouse istediğiniz hello veri eşitleme yöntemini seçin **ilk veri eşitlemesi** sayfasında ve tıklayın **sonraki**. Çoğu senaryoda, seçin **tam veri eşitlemesi**. Veri Eşitleme yöntemleri hakkında daha fazla bilgi için bkz: [seçin ilk veri eşitlemesi sayfası (her zaman üzerinde kullanılabilirlik grubu sihirbazlar)](https://msdn.microsoft.com/library/hh231021.aspx).
13. Merhaba hello sonuçları gözden **doğrulama** sayfası. Bekleyen sorunları düzeltin ve gerekirse hello doğrulamayı yeniden çalıştırın. **İleri**’ye tıklayın.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742866.png)
14. Merhaba hello ayarlarını gözden **Özet** sayfasında ve ardından **son**.
15. Merhaba sağlama işlemi başlar. Başlangıç Sihirbazı'nı başarıyla tamamlandığında, tıklayın **Kapat** tooexit hello Sihirbazı dışında.

> [!NOTE]
> Hello Azure çoğaltma Ekleme Sihirbazı'nı bir günlük dosyası Users\User Name\AppData\Local\SQL Server\AddReplicaWizard oluşturur. Bu günlük dosyası başarısız kullanılan tootroubleshoot Azure çoğaltma dağıtımları olabilir. Herhangi bir eylem yürütme Hello Sihirbazı başarısız olursa, tüm önceki işlemleri geri, VM hello silme de dahil olmak üzere sağlanan.
> 
> 

## <a name="create-an-availability-group-listener"></a>Bir kullanılabilirlik grubu dinleyicisi oluşturma
Merhaba kullanılabilirlik grubu oluşturulduktan sonra istemcileri tooconnect için bir dinleyici toohello çoğaltmaları oluşturmanız gerekir. Dinleyicileri gelen bağlantıları tooeither hello birincil veya salt okunur bir ikincil çoğaltmaya yönlendirir. Dinleyicileri hakkında daha fazla bilgi için bkz: [Azure'da Always On kullanılabilirlik grupları için bir ILB dinleyicisi yapılandırın](../classic/ps-sql-int-listener.md).

## <a name="next-steps"></a>Sonraki adımlar
Toplama toousing hello içinde **Azure çoğaltma Ekleme Sihirbazı'nı** tooextend, her zaman üzerindeki kullanılabilirlik grubu tooAzure bazı SQL Server iş yüklerini taşıma tamamen tooAzure. başlatıldı, tooget bkz [Azure üzerinde bir SQL Server sanal makine sağlama](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Azure vm'lerinde SQL Server toorunning ilgili diğer konular için bkz: [Azure Virtual Machines'de SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

