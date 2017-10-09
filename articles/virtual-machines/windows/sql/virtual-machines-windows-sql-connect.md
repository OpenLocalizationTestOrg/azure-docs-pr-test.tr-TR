---
title: aaaConnect tooa SQL Server sanal makinesine (Resource Manager) | Microsoft Docs
description: "Bilgi nasıl tooconnect tooSQL Server azure'da sanal makine üzerinde çalışan. Bu konuda hello Klasik dağıtım modeli kullanır. Hello senaryoları hello ağ yapılandırmasını ve hello istemci hello konumunu bağlı olarak farklılık gösterir."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>Tooa Azure (Kaynak Yöneticisi) SQL Server sanal makineye bağlanma
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-connect.md)
> * [Klasik](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Genel Bakış

Bu konuda nasıl tooconnect tooyour SQL Server örneği bir Azure sanal makine üzerinde çalışan açıklanmaktadır. Bazı kapsayan [genel bağlantı senaryoları](#connection-scenarios) ve ardından sağlar [ayrıntılı bir Azure VM'de SQL Server bağlantısı yapılandırma adımları](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Hem sağlama hem de bağlantı tam bir gözden geçirme olurdu olup [Azure üzerinde bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="connection-scenarios"></a>Bağlantı senaryoları

Merhaba yolu bir istemci bir sanal makinede çalışan sunucu hello hello istemci ve konumunu hello ağ yapılandırmasına bağlı olarak farklı tooSQL bağlanır.

SQL Server VM hello Azure portal ile sağlarsanız, hello türünü belirleyen hello seçeneğiniz **SQL Bağlantısı**.

![Sağlama sırasında ortak SQL bağlantı seçeneği](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

Bağlantı için seçenekleriniz şunlardır:

| Seçenek | Açıklama |
|---|---|
| **Ortak** | TooSQL sunucu hello üzerinden bağlanma Internet |
| **Özel** | Merhaba içinde sunucu tooSQL bağlanmak aynı sanal ağ |
| **Yerel** | TooSQL sunucu hello yerel olarak bağlanmak aynı sanal makine | 

Merhaba aşağıdaki bölümlerde açıklanmıştır hello **ortak** ve **özel** daha ayrıntılı seçenekleri.

## <a name="connect-toosql-server-over-hello-internet"></a>TooSQL sunucu hello Internet üzerinden Bağlan

Tooconnect tooyour SQL Server veritabanı altyapısı, hello Internet istiyorsanız seçin **ortak** hello için **SQL Bağlantısı** sağlama sırasında hello portalında türü. Merhaba portal otomatik olarak adımları hello:

* Merhaba TCP/IP Protokolü SQL Server için etkinleştirir.
* Bir güvenlik duvarı kuralı tooopen hello SQL Server TCP bağlantı noktası (varsayılan 1433) yapılandırır.
* SQL Server ortak erişim için gerekli kimlik doğrulamasını etkinleştirir.
* Merhaba ağ güvenlik grubu hello hello SQL Server bağlantı noktasında VM tooall TCP trafiğine yapılandırır.

> [!IMPORTANT]
> otomatik olarak hello SQL Server Geliştirici Hello sanal makine görüntülerinin ve Express sürümleri hello TCP/IP Protokolü etkinleştirmeyin. Geliştirici ve Express sürümleri için SQL Server Configuration Manager çok kullanmalısınız[el ile Merhaba TCP/IP protokolünü etkinleştirin](#manualtcp) VM hello oluşturduktan sonra.

İnternet erişimi olan herhangi bir istemci toohello SQL Server örneği hello genel IP adresi hello sanal makinenin veya toothat IP adresi atanmış herhangi bir DNS etiketi belirterek bağlanabilir. Merhaba SQL Server bağlantı noktası 1433 ise, toospecify gerekmez hello bağlantı dizesi içinde. bağlantı dizesi aşağıdaki hello tooa SQL VM ile bir DNS etiketi bağlanır, `sqlvmlabel.eastus.cloudapp.azure.com` SQL kimlik doğrulaması (Ayrıca kullanabileceğiniz hello genel IP adresi) kullanarak.

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

Bu bağlantı için istemciler üzerinde sağlar, ancak internet Merhaba, bu herkes tooyour SQL Server bağlanabilir anlamına gelmez. Dış istemcileri toohello doğru kullanıcı adı ve parolaya sahip. Ancak, ek güvenlik için hello iyi bilinen bağlantı noktası 1433 önleyebilirsiniz. Örneğin, SQL Server toolisten 1500 bağlantı noktasında ve kurulan uygun güvenlik duvarı ve ağ güvenlik grubu kural yapılandırdıysanız, başlangıç bağlantı noktası numarası toohello sunucu adı eklenerek bağlanamadı. Merhaba aşağıdaki örnek hello önceki bir özel bağlantı noktası numarası ekleyerek değiştirir **1500**, toohello sunucu adı:

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> Üzerinden bir VM'de SQL Server sorguladığınızda Internet, tüm giden veri hello hello Azure ' veri merkezi konu toonormal olan [giden veri aktarımları fiyatlandırma](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="connect-toosql-server-within-a-virtual-network"></a>Bir sanal ağ içinde sunucu tooSQL Bağlan

Seçtiğinizde **özel** hello için **SQL Bağlantısı** hello portalındaki Azure türünü yapılandırır aynı hello ayarlarının çoğu çok**ortak**. Merhaba tek fark hiçbir ağ güvenlik grubu kural tooallow hello SQL Server bağlantı noktası (varsayılan 1433) trafiğine dışında olmasıdır.

> [!IMPORTANT]
> otomatik olarak hello SQL Server Geliştirici Hello sanal makine görüntülerinin ve Express sürümleri hello TCP/IP Protokolü etkinleştirmeyin. Geliştirici ve Express sürümleri için SQL Server Configuration Manager çok kullanmalısınız[el ile Merhaba TCP/IP protokolünü etkinleştirin](#manualtcp) VM hello oluşturduktan sonra.

Özel bağlantı ile birlikte kullanılan genellikle [sanal ağ](../../../virtual-network/virtual-networks-overview.md), birkaç senaryo sağlar. Sanal makineleri aynı sanal ağ, bu durumunda bile sanal makineleri farklı kaynak gruplarında mevcut hello olarak bağlanabilir. İle bir [siteden siteye VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), şirket içi ağlar ve makineler VM'ler bağlayan bir karma mimarisi oluşturabilirsiniz.

Sanal ağlar, toojoin de Azure Vm'lerde tooa etki alanınızın etkinleştirin. Merhaba tek yolu toouse Windows kimlik doğrulaması tooSQL sunucu budur. Merhaba bağlantı gerektiren diğer senaryolar SQL kimlik doğrulaması kullanıcı adları ve parolalar.

Sanal ağınıza DNS yapılandırmış olduğunuz varsayılarak hello bağlantı dizesinde hello SQL Server VM bilgisayar adını belirterek tooyour SQL Server örneği bağlanabilir. Ayrıca aşağıdaki örneğine hello Windows kimlik doğrulaması da yapılandırılmış ve bu hello kullanıcı erişimi toohello SQL Server örneği verildi varsayar.

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a>SQL bağlantı ayarlarını değiştirme

Hello Azure portal, SQL Server sanal makine için başlangıç bağlantı ayarlarını değiştirebilirsiniz.

1. Hello Azure portal, seçin **sanal makineleri**.

2. SQL Server VM'yi seçin.

3. Altında **ayarları**, tıklatın **SQL Server yapılandırma**.

4. Değişiklik hello **SQL bağlantı düzeyi** gerekli tooyour ayarlama. İsteğe bağlı olarak, bu alanı toochange hello SQL Server bağlantı noktası veya hello SQL kimlik doğrulaması ayarlarını da kullanabilirsiniz.

   ![SQL Bağlantısı değiştirme](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. Merhaba güncelleştirme toocomplete birkaç dakika bekleyin.

   ![SQL VM güncelleştirme bildirimi](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a>Geliştirici ve Express sürümleri için TCP/IP'yi etkinleştirin

SQL Server bağlantı ayarları değiştirirken, Azure otomatik olarak hello TCP/IP Protokolü SQL Server Developer ve Express sürümleri için izin vermez. nasıl toomanually etkinleştirmek TCP/IP'yi IP adresi ile uzaktan bağlanabilmesi Hello adımları açıklanmaktadır.

İlk olarak, Uzak Masaüstü'nü toohello SQL Server makinesinde bağlayın.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Ardından, hello TCP/IP protokolü ile etkinleştirmek **SQL Server Configuration Manager**.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>SSMS ile bağlanma

Merhaba aşağıdaki adımları nasıl toocreate isteğe bağlı bir DNS etiketi Azure VM için Göster ve SQL Server Management Studio (SSMS) bağlayın.

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Sonraki Adımlar

Bu bağlantı adımlarını toosee sağlama yönergelere bakın [Azure üzerinde bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).

Azure vm'lerinde SQL Server toorunning ilgili diğer konular için bkz: [Azure Virtual Machines'de SQL Server](virtual-machines-windows-sql-server-iaas-overview.md).
