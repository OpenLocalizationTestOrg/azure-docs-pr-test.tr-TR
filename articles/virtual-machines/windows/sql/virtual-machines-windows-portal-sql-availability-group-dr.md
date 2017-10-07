---
title: "aaaSQL Server kullanılabilirlik gruplarını - Azure sanal makineleri - olağanüstü durum kurtarma | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure bir SQL Server kullanılabilirlik grubu Azure sanal makinelerinde farklı bir bölgede çoğaltmasıyla açıklanmaktadır."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>Azure sanal makinelerinde farklı bölgelerdeki Always On kullanılabilirlik grubu yapılandırma

Bu makalede, Azure sanal makinelerinde uzak bir Azure konumda çoğaltma tooconfigure bir SQL Server Always On kullanılabilirlik Grup nasıl açıklanmaktadır. Bu yapılandırma toosupport olağanüstü durum kurtarma kullanın.

Bu makale, Resource Manager moduna tooAzure sanal makineleri geçerlidir.

Merhaba aşağıdaki resimde bir kullanılabilirlik grubu ortak dağıtımı Azure sanal makinelerde gösterilmektedir:

   ![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

Bu dağıtımda, tüm sanal makineleri bir Azure bölgesinde ' dir. Merhaba kullanılabilirlik grubu çoğaltmalarının zaman uyumlu işleme SQL-1 ve 2 SQL otomatik yük devretme ile olabilir. toobuild Bu mimarinin bkz [kullanılabilirlik grubu şablon veya öğretici](virtual-machines-windows-portal-sql-availability-group-overview.md).

Bu mimari Hello Azure bölgesi erişilemez duruma karşı savunmasız toodowntime olur. tooovercome bu güvenlik açığından farklı bir Azure bölgesinde bir çoğaltma ekleyin. Merhaba Aşağıdaki diyagramda hello yeni mimarisi nasıl görüneceği gösterilmektedir:

   ![Kullanılabilirlik grubu DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

Merhaba önceki diyagramda SQL 3 adlı yeni bir sanal makine gösterir. SQL-3 farklı bir Azure bölgesinde kullanılır. SQL 3 toohello Windows Server Yük devretme eklenir. SQL 3 bir kullanılabilirlik grubu çoğaltması barındırabilir. Son olarak, bu hello Azure bölgesi SQL 3 için yeni bir Azure yük dengeleyici sahip dikkat edin.

>[!NOTE]
> Bir Azure kullanılabilirlik kümesi, sanal makine birden fazla aynı bölgede hello durumlarda gereklidir. Bir sanal makine hello bölgede yalnızca, hello kullanılabilirlik kümesi gerekli değildir. Yalnızca bir sanal makine kullanılabilirlik kümesi oluşturma zamanında yerleştirebilirsiniz. Merhaba sanal makine zaten bir kullanılabilirlik kümesine ise, daha sonra ek bir çoğaltma için bir sanal makine ekleyebilirsiniz.

Bu mimaride hello çoğaltma hello uzak bölgede normalde zaman uyumsuz tamamlama kullanılabilirlik modu ve el ile yük devretme modu ile yapılandırılır.

Kullanılabilirlik grubu çoğaltmalarının Azure sanal makinelerinde farklı Azure bölgelerinde olduğunda, her bölge gerektirir:

* Bir sanal ağ geçidi
* Sanal ağ geçidi bağlantısı

Merhaba Aşağıdaki diyagramda hello ağları veri merkezleri arasında nasıl iletişim kurduğunu gösterir.

   ![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>Bu mimarinin Azure bölgeler arasında çoğaltılan veriler için giden veri ücret doğurur. Bkz: [bant genişliği fiyatlandırma](http://azure.microsoft.com/pricing/details/bandwidth/).  

## <a name="create-remote-replica"></a>Uzak bir çoğaltma oluşturma

bir uzak veri merkezindeki bir çoğaltma toocreate adımları izleyerek hello:

1. [Merhaba yeni bölgede bir sanal ağ oluşturma](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

1. [Hello Azure portalını kullanarak VNet-VNet bağlantı yapılandırma](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).

   >[!NOTE]
   >Bazı durumlarda, toouse PowerShell toocreate hello VNet-VNet bağlantı olabilir. Örneğin, farklı Azure hesapları kullanıyorsanız hello bağlantı hello Portalı'nda yapılandıramazsınız. Bu durumda bakın, [hello Azure portal yapılandırma bir VNet-VNet bağlantısı kullanarak](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

1. [Bir etki alanı denetleyicisi hello yeni bölge Oluştur](../../../active-directory/active-directory-new-forest-virtual-machine.md).

   Merhaba birincil sitedeki Hello etki alanı denetleyicisinin kullanılabilir değilse, bu etki alanı denetleyicisi kimlik doğrulaması sağlar.

1. [Bir SQL Server sanal makine hello yeni bölge Oluştur](virtual-machines-windows-portal-sql-server-provision.md).

1. [Bir Azure yük dengeleyici hello ağ hello yeni bölge oluşturma](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

   Bu yük dengeleyici gerekir:

   - Olması yeni bir sanal makine hello gibi aynı ağ ve alt ağ hello.
   - Merhaba kullanılabilirlik grubu dinleyicisi için statik bir IP adresi vardır.
   - Yük Dengeleyici hello gibi Hello sanal makinelerin aynı bölgede hello yalnızca oluşan bir arka uç havuzu ekleyin.
   - Bir TCP bağlantı noktası araştırma belirli toohello IP adresi kullanın.
   - Bir Yük Dengeleme kuralı belirli toohello SQL Server hello içinde sahip aynı bölgede.  

1. [Yük Devretme Kümelemesi özelliğini toohello ekleme yeni SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

1. [Merhaba yeni SQL Server toohello etki alanına](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

1. [Bir etki alanı hesabı Hello yeni SQL Server hizmet hesabı toouse ayarlamanız](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).

1. [Merhaba yeni SQL Server toohello Windows Server Yük devretme eklemek](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).

1. Bir IP adresi kaynağı hello kümede oluşturun.

   Yük Devretme Kümesi Yöneticisi'nde hello IP adresi kaynağı oluşturabilirsiniz. Merhaba kullanılabilirlik grubu role sağ tıklayın, **kaynak ekleme**, **daha kaynakları**, tıklatıp **IP adresi**.

   ![IP adresi oluşturun](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   Bu IP adresi gibi yapılandırın:

   - Merhaba ağ hello uzak veri merkezinden kullanın.
   - Başlangıç IP adresi hello yeni Azure yük dengeleyiciden atayın. 

1. Üzerinde yeni SQL Server SQL Server Yapılandırma Yöneticisi ' nde hello [Always On kullanılabilirlik grupları etkinleştirmek](http://msdn.microsoft.com/library/ff878259.aspx).

1. [Açık güvenlik duvarı bağlantı noktaları hello yeni SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

   başlangıç bağlantı noktası numaralarını tooopen ihtiyacınız ortamınıza bağlıdır. Yansıtma uç noktası ve Azure hello açık bağlantı noktalarını dengeleyici durum araştırması yükleyin.

1. [Bir çoğaltma toohello kullanılabilirlik grubu üzerinde hello ekleyin yeni SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).

   Uzak bir Azure bölgesindeki bir çoğaltma için el ile yük devretme ile zaman uyumsuz çoğaltma için ayarlayın.  

1. Başlangıç IP adresi kaynağı hello dinleyicisi istemci erişim noktası (ağ adı) küme için bağımlılık olarak ekleyin.

   Merhaba aşağıdaki ekran görüntüsü düzgün şekilde yapılandırılmış bir IP adresi küme kaynağı gösterir:

   ![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >Merhaba küme kaynak grubu iki IP adresi içerir. Bağımlılıklar hello dinleyicisi istemci erişim noktası için her iki IP adresleridir. Kullanım hello **veya** hello küme bağımlılık yapılandırmasında işleci.

1. [PowerShell'de hello küme parametreleri ayarlamak](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).

Merhaba küme ağ adı, IP adresi ve hello yeni bölgede hello yük dengeleyici üzerinde yapılandırılmış yoklama bağlantı noktası ile Merhaba PowerShell betiğini çalıştırın.

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>Birden çok alt ağlar için kümesi bağlantı

Merhaba çoğaltma hello uzak veri merkezinde hello kullanılabilirlik grubunun parçası olan ancak farklı bir alt ağda değil. Bu çoğaltma hello birincil çoğaltma olursa, uygulama bağlantı zaman aşımları ortaya çıkabilir. Bu davranış olduğu hello bir şirket içi kullanılabilirlik grubunda birden çok alt ağ dağıtımı ile aynı. istemci uygulamaları tooallow bağlantılarından hello istemci bağlantısını güncelleştirin veya hello küme ağ adı kaynağına bağlı önbelleğe alma ad çözümlemesi yapılandırabilirsiniz.

Tercihen Merhaba istemci bağlantı dizeleri tooset güncelleştirme `MultiSubnetFailover=Yes`. Bkz: [MultiSubnetFailover ile bağlanma](http://msdn.microsoft.com/library/gg471494#Anchor_0).

Merhaba bağlantı dizeleri değiştirilemiyor, ad çözümlemesi önbelleğe alma yapılandırabilirsiniz. Bkz: [birden çok alt ağ kullanılabilirlik grubundaki zaman aşımları](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).

## <a name="fail-over-tooremote-region"></a>Tooremote bölge başarısız

tootest dinleyici bağlantı toohello uzak bölge, hello çoğaltma toohello uzak bölge başarısız olabilir. Merhaba çoğaltma zaman uyumsuz olsa da, yük devretme savunmasız toopotential veri kaybı olmuş. veri kaybı olmadan üzerinden toofail hello kullanılabilirlik modu toosynchronous değiştirmek ve hello yük devretme modu tooautomatic ayarlayın. Merhaba aşağıdaki adımları kullanın:

1. İçinde **Nesne Gezgini**, toohello hello birincil çoğaltmayı barındıran SQL Server örneğine bağlanın.
1. Altında **AlwaysOn Kullanılabilirlik grupları**, **kullanılabilirlik grupları**, kullanılabilirlik grubunuzun sağ tıklatın ve **özellikleri**.
1. Merhaba üzerinde **genel** sayfasında **kullanılabilirlik çoğaltmalarının**, kümesi hello ikincil çoğaltmasında hello DR sitesi toouse **zaman uyumlu yürütme** kullanılabilirlik modu ve **Otomatik** yük devretme modu.
1. Yüksek kullanılabilirlik için birincil, çoğaltma olarak aynı sitedeki bir ikincil çoğaltma varsa, bu kopya çok kümesi**zaman uyumsuz tamamlama** ve **el ile**.
1. Tamam'a tıklayın.
1. İçinde **Object Explorer**, hello kullanılabilirlik grubuna sağ tıklayın ve **Göster Pano**.
1. Bu hello Hello Panoda doğrulayın hello DR sitesi üzerinde çoğaltma eşitlenir.
1. İçinde **Object Explorer**, hello kullanılabilirlik grubuna sağ tıklayın ve **yük devretme...** . SQL Server Management stüdyoları Sihirbazı toofail üzerinden SQL Server açar.  
1. Tıklatın **sonraki**ve select hello SQL Server örneğinde hello DR sitesi. Tıklatın **sonraki** yeniden.
1. Merhaba DR sitesi toohello SQL Server örneğinde bağlanmak ve tıklatın **sonraki**.
1. Merhaba üzerinde **Özet** sayfasında hello ayarlarını doğrulayın ve tıklayın **son**.

Bağlantı test ediliyor sonra hello birincil çoğaltma geri tooyour birincil veri merkezi ve hello kullanılabilirlik modu geri tootheir normal işletim ayarlar taşıyın. Merhaba aşağıdaki tabloda bu belgede açıklanan hello mimarisi için normal işletimsel ayarları hello gösterilmektedir:

| Konum | Sunucu örneği | Rol | Kullanılabilirlik modu | Yük devretme modu
| ----- | ----- | ----- | ----- | -----
| Birincil veri merkezi | SQL-1 | Birincil | Zaman uyumlu | Otomatik
| Birincil veri merkezi | SQL-2 | İkincil | Zaman uyumlu | Otomatik
| İkincil ya da uzak veri merkezi | SQL-3 | İkincil | Zaman uyumsuz | El ile


### <a name="more-information-about-planned-and-forced-manual-failover"></a>Planlanan ve zorunlu el ile yük devretme hakkında daha fazla bilgi

Daha fazla bilgi için aşağıdaki konularda hello bakın:

- [Bir kullanılabilirlik grubu (SQL Server) planlanmış bir el ile yük gerçekleştirin](http://msdn.microsoft.com/library/hh231018.aspx)
- [Bir kullanılabilirlik grubu (SQL Server) zorla el ile yük devretme gerçekleştirme](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>Ek bağlantılar

* [Always On kullanılabilirlik grupları](http://msdn.microsoft.com/library/hh510230.aspx)
* [Azure sanal makineler](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Azure yük dengeleyicileri](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Azure kullanılabilirlik kümeleri](../manage-availability.md)
