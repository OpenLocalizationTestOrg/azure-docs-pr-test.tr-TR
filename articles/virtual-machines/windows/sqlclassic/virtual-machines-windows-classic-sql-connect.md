---
title: SQL Server sanal makinesi (Klasik) azure'da aaaConnect tooa | Microsoft Docs
description: "Bilgi nasıl tooconnect tooSQL Server azure'da sanal makine üzerinde çalışan. Bu konuda hello Klasik dağıtım modeli kullanır. Hello senaryoları hello ağ yapılandırmasını ve hello istemci hello konumunu bağlı olarak farklılık gösterir."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Tooa Azure (Klasik dağıtım) SQL Server sanal makineye bağlanma
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-connect.md)
> * [Klasik](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Bu konuda nasıl tooconnect tooyour SQL Server örneği bir Azure sanal makine üzerinde çalışan açıklanmaktadır. Bazı kapsayan [genel bağlantı senaryoları](#connection-scenarios) ve ardından sağlar [ayrıntılı bir Azure VM'de SQL Server bağlantısı yapılandırma adımları](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Resource Manager VM kullanıyorsanız, bkz: [tooa Azure Kaynak Yöneticisi'ni kullanarak SQL Server sanal makineye bağlanma](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a>Bağlantı senaryoları
Merhaba yolu bir istemci bir sanal makinede çalışan sunucu hello hello istemci ve konumunu hello makine/ağ yapılandırması bağlı olarak farklı tooSQL bağlanır. Bu senaryolar şunlardır:

* [TooSQL sunucu bağlanmak hello aynı bulut hizmeti](#connect-to-sql-server-in-the-same-cloud-service)
* [TooSQL sunucu hello üzerinden bağlanma Internet](#connect-to-sql-server-over-the-internet)
* [Merhaba içinde sunucu tooSQL bağlanmak aynı sanal ağ](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Bu yöntemlerin herhangi biriyle ile bağlanmadan önce hello izlemelisiniz [Bu makale tooconfigure Bağlantısı'ndaki adımları](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>TooSQL sunucu bağlanmak hello aynı bulut hizmeti
Hello aynı birden çok sanal makine oluşturulan bulut hizmeti. toounderstand bu sanal makineleri senaryosu, bkz: [nasıl tooconnect sanal makineleri bir sanal ağ veya Bulut hizmeti ile](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service). Bir sanal makine bir istemcide tooconnect tooSQL Server çalışan çalıştığında bu senaryodur aynı bulut hizmeti hello başka bir sanal makinede.

Bu senaryoda, hello VM kullanarak bağlanabilir **adı** (Ayrıca gösterilen **bilgisayar adı** veya **ana bilgisayar adı** hello Portalı'nda). Bu Merhaba VM oluşturma sırasında sağlanan hello adıdır. Örneğin, SQL VM'nizi adlı **mysqlvm**, bir ' % s'istemcinin VM hello aynı bulut hizmetine kullanır, bağlantı dizesi tooconnect aşağıdaki hello:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>TooSQL sunucu hello Internet üzerinden Bağlan
Tooconnect tooyour SQL Server veritabanı altyapısı, hello Internet istiyorsanız, bir sanal makine uç noktası gelen TCP iletişimi için oluşturmanız gerekir. Bu Azure yapılandırma adımı erişilebilir toohello sanal makine gelen TCP bağlantı noktası trafik tooa TCP bağlantı noktasına yönlendirir.

Internet üzerinden tooconnect Merhaba, (Bu makalenin sonraki bölümlerinde yapılandırılmış) hello sanal makinenin DNS adı ve hello VM uç nokta bağlantı noktası numarası kullanmanız gerekir. toofind hello DNS adı gidin toohello Azure portal ve select **sanal makineleri (Klasik)**. Ardından, sanal makineyi seçin. Merhaba **DNS adı** hello gösterilen **genel bakış** bölümü.

Örneğin, klasik bir sanal makine adlı göz önünde bulundurun **mysqlvm** bir DNS adı ile **mysqlvm7777.cloudapp.net** VM bitiş noktası **57500**. Düzgün şekilde yapılandırılmış bağlantı varsayıldığında, bağlantı dizesi aşağıdaki hello kullanılan tooaccess hello sanal makine yerden olabilir Internet hello:

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

Bu bağlantı için istemciler üzerinde sağlar, ancak internet Merhaba, bu herkes tooyour SQL Server bağlanabilir anlamına gelmez. Dış istemcileri toohello doğru kullanıcı adı ve parolaya sahip. Ek güvenlik için hello iyi bilinen bağlantı noktası 1433 hello genel sanal makine uç noktası için kullanmayın. Ve mümkünse, bir ACL izin uç nokta toorestrict trafiği yalnızca toohello istemcilerinize eklemeyi düşünün. ACL'ler uç ile kullanma ile ilgili yönergeler için bkz: [uç noktada Yönet hello ACL](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

> [!NOTE]
> Bu teknik toocommunicate SQL Server ile kullandığınızda, tüm giden verileri Azure veri merkezi hello toonote olan konu toonormal önemlidir [giden veri aktarımları fiyatlandırma](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>Merhaba içinde sunucu tooSQL bağlanmak aynı sanal ağ
[Sanal ağ](../../../virtual-network/virtual-networks-overview.md) ek senaryolara olanak sağlar. Sanal makineleri aynı sanal ağ, bu durumunda bile sanal makineleri farklı bir bulut Hizmetleri'nde mevcut hello olarak bağlanabilir. İle bir [siteden siteye VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), şirket içi ağlar ve makineler VM'ler bağlayan bir karma mimarisi oluşturabilirsiniz.

Sanal ağlar Azure VM'ler tooa etki alanınızın Ayrıca, toojoin sağlar. Merhaba tek yolu toouse Windows kimlik doğrulaması tooSQL sunucu budur. Merhaba bağlantı gerektiren diğer senaryolar SQL kimlik doğrulaması kullanıcı adları ve parolalar.

Tooconfigure bir etki alanı ortamı ve Windows kimlik doğrulaması kullanacaksanız, bu makale tooconfigure hello ortak uç nokta veya hello SQL kimlik doğrulaması ve oturum açma bilgileri toouse hello adımları uygulamanız gerekmez. Bu senaryoda, hello bağlantı dizesinde hello SQL Server VM adı belirterek tooyour SQL Server örneği bağlanabilir. Aşağıdaki örneğine hello Windows kimlik doğrulaması da yapılandırılmış ve hello kullanıcı erişimi toohello SQL Server örneği verilmiş olduğunu varsayar.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Bir Azure VM'de SQL Server bağlantısı yapılandırma adımları
Aşağıdaki adımları hello nasıl tooconnect toohello SQL Server örneği üzerinde hello SQL Server Management Studio (SSMS) kullanarak Internet göstermektedir. Ancak, hello aynı adımlar toomaking SQL Server sanal makinenizi çalıştıran her iki şirket içi uygulamalarınızı ve Azure erişilebilir geçerlidir.

Toohello SQL Server'ın başka bir sanal makineden bağlanın ya da Internet hello önce izleyin hello bölümlerinde açıklandığı gibi görevleri aşağıdaki hello tamamlamanız gerekir:

* [Merhaba sanal makine için bir TCP uç noktası oluşturma](#create-a-tcp-endpoint-for-the-virtual-machine)
* [TCP bağlantı noktaları hello Windows Güvenlik Duvarı'nı açın](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [SQL Server toolisten TCP protokolü hello üzerinde yapılandırma](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [SQL Server için karma mod kimlik doğrulamasını yapılandırma](#configure-sql-server-for-mixed-mode-authentication)
* [SQL Server kimlik doğrulama oturumları oluşturma](#create-sql-server-authentication-logins)
* [Merhaba DNS hello sanal makinenin adını belirleme](#determine-the-dns-name-of-the-virtual-machine)
* [Başka bir bilgisayardan toohello veritabanına bağlan](#connect-to-the-database-engine-from-another-computer)

Merhaba bağlantı yolu diyagramı aşağıdaki hello tarafından özetlenmiştir:

![Tooa SQL Server sanal makineye bağlanma](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>Sonraki Adımlar
Yüksek kullanılabilirlik ve olağanüstü durum kurtarma toouse AlwaysOn Kullanılabilirlik grupları da planlıyorsanız, bir dinleyici uygulama düşünmelisiniz. Veritabanı istemcileri toohello dinleyicisi yerine doğrudan hello SQL Server örneklerinin tooone bağlanır. Merhaba dinleyicisi yollar istemcileri toohello birincil çoğaltma hello kullanılabilirlik grubunda. Daha fazla bilgi için bkz: [Azure'da AlwaysOn Kullanılabilirlik grupları için bir ILB dinleyicisi yapılandırın](../classic/ps-sql-int-listener.md).

Merhaba güvenlik tümünün bir Azure sanal makinede çalışan SQL Server için en iyi uygulamalar önemli tooreview olur. Daha fazla bilgi için bkz. [Azure Sanal Makineler'de SQL Server için Güvenlikle İlgili Dikkat Edilmesi Gerekenler](../sql/virtual-machines-windows-sql-security.md).

[Merhaba öğrenme yolunu keşfedin](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) Azure virtual machines'de SQL Server için. 

Azure vm'lerinde SQL Server toorunning ilgili diğer konular için bkz: [Azure Virtual Machines'de SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

