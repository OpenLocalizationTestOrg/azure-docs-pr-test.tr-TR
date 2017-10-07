---
title: "Azure sanal makinelerde SQL Server kullanılabilirlik grubu dinleyicisi aaaCreate | Microsoft Docs"
description: "Always On kullanılabilirlik grubu için bir dinleyici SQL Server için Azure sanal makinelerinde oluşturmak için adım adım yönergeler"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>Always On kullanılabilirlik grubu için yük dengeleyici Azure'da yapılandırın
Bu makalede, nasıl toocreate bir yük dengeleyici bir SQL Server Always On kullanılabilirlik grubu için Azure sanal makineye açıklanmaktadır Azure Resource Manager ile çalışıyor. Merhaba SQL Server örnekleri Azure sanal makinelerde olduğunda bir kullanılabilirlik grubu yük dengeleyici gerektirir. Merhaba yük dengeleyici hello kullanılabilirlik grubu dinleyicisi hello IP adresini depolar. Bir kullanılabilirlik grubu birden çok bölgeye yayılırsa, her bölge bir yük dengeleyicinin gerekir.

toocomplete bu görev bir SQL Server kullanılabilirlik grubu dağıtılan Resource Manager ile çalışan Azure sanal makinelerde toohave gerekir. Her iki SQL Server sanal makineleri toohello ait olmalıdır aynı kullanılabilirlik kümesi. Merhaba kullanabilirsiniz [Microsoft şablonu](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Kaynak Yöneticisi'nde hello kullanılabilirlik grubu oluşturun. Bu şablon bir iç yük dengeleyici sizin için otomatik olarak oluşturur. 

İsterseniz, aşağıdakileri yapabilirsiniz [el ile bir kullanılabilirlik grubu yapılandırmak](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Bu makalede, kullanılabilirlik grupları zaten yapılandırılmış olmasını gerektirir.  

İlgili Konular şunlardır:

* [Azure VM (GUI), Always On kullanılabilirlik grupları yapılandırma](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Azure Resource Manager ve PowerShell kullanarak VNet-VNet bağlantı yapılandırma](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

Bu makalede taramasını tarafından oluşturabilir ve bir yük dengeleyici hello Azure portalında yapılandırabilirsiniz. Merhaba işlemi tamamlandıktan sonra hello küme toouse hello IP adresinden hello yük dengeleyici hello kullanılabilirlik grubu dinleyicisi için yapılandırın.

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>Oluşturma ve hello yük dengeleyici hello Azure portalını yapılandırma
Başlangıç görevinin bu bölümünde, aşağıdaki hello:

1. Hello Azure portal, hello yük dengeleyicisi oluşturun ve başlangıç IP adresi yapılandırın.
2. Merhaba arka uç havuzunu yapılandırın.
3. Merhaba araştırma oluşturun. 
4. Merhaba Yük Dengeleme kuralları ayarlayın.

> [!NOTE]
> Hello SQL Server örneklerini birden çok kaynak grupları ve bölgelerde varsa, her adım, iki kez kez her kaynak grubunda gerçekleştirin.
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>1. adım: hello yük dengeleyicisi oluşturun ve başlangıç IP adresi yapılandırın
İlk olarak hello yük dengeleyicisi oluşturun. 

1. Hello Azure portal, hello SQL Server sanal makineleri içeren hello kaynak grubu açın. 

2. Merhaba kaynak grubunda tıklatın **Ekle**.

3. Arama **yük dengeleyici** ve hello arama sonuçlarında ardından **yük dengeleyici**, tarafından yayımlanan **Microsoft**.

4. Merhaba üzerinde **yük dengeleyici** dikey penceresinde tıklatın **oluşturma**.

5. Merhaba, **oluşturma yük dengeleyici** iletişim kutusunda, hello yük dengeleyici gibi yapılandırın:

   | Ayar | Değer |
   | --- | --- |
   | **Ad** |Merhaba yük dengeleyici temsil eden bir metin adı. Örneğin, **sqlLB**. |
   | **Tür** |**İç**: çoğu uygulamalarını hello uygulamalara izin veren bir iç yük dengeleyici kullanın aynı sanal ağ tooconnect toohello kullanılabilirlik grubu.  </br> **Dış**: uygulamaları tooconnect toohello kullanılabilirlik grubu genel bir Internet bağlantısı üzerinden sağlar. |
   | **Sanal ağ** |Merhaba SQL Server intances bulunan hello sanal ağı seçin. |
   | **Alt ağ** |Merhaba SQL Server örnekleri bulunan hello alt ağ seçin. |
   | **IP adresi ataması** |**Statik** |
   | **Özel IP adresi** |Merhaba alt ağdan kullanılabilir bir IP adresi belirtin. Merhaba kümede bir dinleyici oluşturduğunuzda, bu IP adresi kullanın. Bu makalenin sonraki bölümlerinde bir PowerShell Betiği bu adresi Merhaba kullanmak `$ILBIP` değişkeni. |
   | **Abonelik** |Birden çok aboneliğiniz varsa, bu alan görünebilir. Bu kaynakla tooassociate istediğiniz hello aboneliği seçin. Bunu olduğu normalde hello aynı abonelik hello kullanılabilirlik grubu için tüm hello kaynaklar. |
   | **Kaynak grubu** |Merhaba SQL Server örnekleri bulunan hello kaynak grubu seçin. |
   | **Konum** |Merhaba hello SQL Server örnekleri bulunan Azure konumu seçin. |

6. **Oluştur**'a tıklayın. 

Azure hello yük dengeleyici oluşturur. Merhaba yük dengeleyici tooa belirli ağ, alt ağ, kaynak grubunu ve konumu aittir. Azure hello görev tamamlandıktan sonra azure'da hello yük dengeleyici ayarları doğrulayın. 

### <a name="step-2-configure-hello-back-end-pool"></a>2. adım: hello arka uç havuzunu yapılandırma
Azure çağrıları hello arka uç adres havuzu *arka uç havuzu*. Bu durumda, hello arka uç havuzu hello adresleri hello iki SQL Server örneklerinin kullanılabilirlik grubunda değil. 

1. Kaynak grubunda oluşturduğunuz hello yük dengeleyici'ı tıklatın. 

2. Üzerinde **ayarları**, tıklatın **arka uç havuzları**.

3. Üzerinde **arka uç havuzları**, tıklatın **Ekle** toocreate bir arka uç adres havuzu. 

4. Üzerinde **arka uç havuzu ekleme**altında **adı**, hello arka uç havuzu için bir ad yazın.

5. Altında **sanal makineleri**, tıklatın **bir sanal makine Ekle**. 

6. Altında **sanal makineleri seçin**, tıklatın **bir kullanılabilirlik kümesi seçin**ve ardından hello kullanılabilirlik kümesi hello SQL Server sanal makineleri ait olduğunu belirtin.

7. Merhaba kullanılabilirlik kümesi seçtikten sonra tıklatın **hello sanal makineleri seçin**, select hello hello SQL Server örnekleri hello kullanılabilirlik grubunda barındırmak ve ardından iki sanal makine **seçin**. 

8. Tıklatın **Tamam** tooclose hello kaynaklarınız için dikey pencereleri **sanal makineleri seçin**, ve **arka uç havuzu ekleme**. 

Azure hello arka uç adres havuzu hello ayarlarını güncelleştirir. Şimdi iki SQL Server örneklerinin bir havuzu kullanılabilirlik kümesi vardır.

### <a name="step-3-create-a-probe"></a>3. adım: bir araştırma oluşturma
Merhaba araştırma nasıl hello SQL Server örnekleri hangisinin hello kullanılabilirlik grubu dinleyicisi şu anda sahibi Azure doğrular tanımlar. Azure hello araştırma oluşturduğunuzda tanımlayan bir bağlantı noktası hello IP adresine göre hello hizmet araştırmaları.

1. Merhaba üzerinde yük dengeleyici **ayarları** dikey penceresinde tıklatın **sistem durumu araştırmalarının**. 

2. Merhaba üzerinde **sistem durumu araştırmalarının** dikey penceresinde tıklatın **Ekle**.

3. Merhaba üzerinde Hello araştırmasını yapılandırma **Ekle araştırma** dikey. Aşağıdaki kullanım hello tooconfigure hello araştırma değerler:

   | Ayar | Değer |
   | --- | --- |
   | **Ad** |Merhaba araştırma temsil eden bir metin adı. Örneğin, **SQLAlwaysOnEndPointProbe**. |
   | **Protokol** |**TCP** |
   | **Bağlantı Noktası** |Tüm kullanılabilir bağlantı noktası kullanabilirsiniz. Örneğin, *59999*. |
   | **Aralığı** |*5* |
   | **Sağlıksız durum eşiği.** |*2* |

4.  **Tamam** düğmesine tıklayın. 

> [!NOTE]
> Belirttiğiniz başlangıç bağlantı noktası hem de SQL Server örnekleri hello güvenlik duvarı açık olduğundan emin olun. Her iki örnek hello kullandığınız TCP bağlantı noktası için bir gelen kuralı gerektirir. Daha fazla bilgi için bkz: [Ekle veya Düzenle güvenlik duvarı kuralı](http://technet.microsoft.com/library/cc753558.aspx). 
> 
> 

Azure hello araştırması oluşturur ve hello dinleyici hello kullanılabilirlik grubu için hangi SQL Server örneğine sahip tootest kullanır.

### <a name="step-4-set-hello-load-balancing-rules"></a>4. adım: hello Yük Dengeleme kuralları ayarlama
Merhaba yük dengeleyici trafiği toohello SQL Server örneklerinin nasıl yönlendirir Hello Yük Dengeleme kuralları yapılandırın. Merhaba iki SQL Server örneği yalnızca biri aynı anda hello kullanılabilirlik grubu dinleyicisi kaynağının sahibi olduğundan bu yük dengeleyici için doğrudan sunucu dönüşü etkinleştirin.

1. Merhaba üzerinde yük dengeleyici **ayarları** dikey penceresinde tıklatın **Yük Dengeleme kuralları**. 

2. Merhaba üzerinde **Yük Dengeleme kuralları** dikey penceresinde tıklatın **Ekle**.

3. Merhaba üzerinde **Ekle Yük Dengeleme kuralları** dikey penceresinde hello Yük Dengeleme kuralını yapılandırın. Ayarları aşağıdaki hello kullan: 

   | Ayar | Değer |
   | --- | --- |
   | **Ad** |Merhaba Yük Dengeleme kuralları temsil eden bir metin adı. Örneğin, **SQLAlwaysOnEndPointListener**. |
   | **Protokol** |**TCP** |
   | **Bağlantı Noktası** |*1433* |
   | **Arka uç bağlantı noktası** |*1433*. Bu kural kullandığından bu değer yoksayılır **kayan IP (doğrudan sunucu dönüşü)**. |
   | **Araştırma** |Bu yük dengeleyici için oluşturduğunuz hello araştırma Hello adını kullanın. |
   | **Oturum kalıcılığı** |**Yok** |
   | **Boşta kalma zaman aşımı (dakika)** |*4* |
   | **Kayan IP (doğrudan sunucu dönüşü)** |**Etkin** |

   > [!NOTE]
   > Tüm hello ayarları hello dikey tooview aşağı tooscroll olabilir.
   > 

4. **Tamam** düğmesine tıklayın. 
5. Azure hello Yük Dengeleme kuralı yapılandırır. Merhaba yük dengeleyici hello kullanılabilirlik grubu için hello dinleyici barındıran yapılandırılmış tooroute trafiği toohello SQL Server örneği sunulmuştur. 

Bu noktada, tooboth SQL Server makineleri bağlayan bir yük dengeleyici hello kaynak grubunda yok. Her iki makine toorequests hello kullanılabilirlik grupları için yanıt vermesini sağlayabilirsiniz hello yük dengeleyici hello SQL Server Always On kullanılabilirlik grubu dinleyicisi, IP adresini de içerir.

> [!NOTE]
> SQL Server örnekleri iki ayrı bölgelerde bulunuyorsa, diğer bölge hello hello adımlarını yineleyin. Her bölge bir yük dengeleyici gerektirir. 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>Merhaba küme toouse hello yük dengeleyici IP adresi yapılandırın
Merhaba sonraki adıma tooconfigure hello dinleyicisi hello kümede ve hello dinleyicisi çevrimiçi duruma getirin. Aşağıdaki hello: 

1. Merhaba kullanılabilirlik grubu dinleyicisi hello yük devretme kümesinde oluşturun. 

2. Merhaba dinleyicisi çevrimiçi duruma getirin.

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>5. adım: hello yük devretme kümesinde hello kullanılabilirlik grubu dinleyicisi oluşturma
Bu adımda, yük devretme kümesi Yöneticisi'ni ve SQL Server Management Studio hello kullanılabilirlik grubu dinleyicisi el ile oluşturun.

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>Merhaba dinleyicisi Hello yapılandırmasını doğrulayın

Merhaba küme kaynakları ve bağımlılıklar doğru şekilde yapılandırılırsa, SQL Server Management Studio'da mümkün tooview hello dinleyicisi olmalıdır. tooset Merhaba dinleyicisi bağlantı noktası, aşağıdaki hello:

1. SQL Server Management Studio'yu başlatın ve sonra toohello birincil çoğaltma bağlanın.

2. Çok Git**AlwaysOn yüksek kullanılabilirlik** > **kullanılabilirlik grupları** > **kullanılabilirlik grubu dinleyicileri**.  
    Yük Devretme Kümesi Yöneticisi'nde oluşturulan hello dinleyici adı görmelisiniz. 

3. Merhaba dinleyici adına sağ tıklayın ve ardından **özellikleri**.

4. Merhaba, **bağlantı noktası** kutusunda, daha önce kullandığınız $EndpointPort hello kullanarak hello hello kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (1433 olduğu hello varsayılan) ve ardından **Tamam**.

Artık Azure sanal makinelerde Kaynak Yöneticisi modunda çalışan bir kullanılabilirlik grubuna sahip. 

## <a name="test-hello-connection-toohello-listener"></a>Test hello bağlantı toohello dinleyicisi
Merhaba aşağıdakileri yaparak hello Bağlantıyı Sına:

1. Hello olan RDP tooa SQL Server örneği aynı sanal ağ, ancak kendi hello çoğaltma. Bu sunucu olması hello hello kümedeki diğer SQL Server örneği.

2. Kullanım **sqlcmd** yardımcı programı tootest hello bağlantı. Örneğin, komut dosyası izleyen hello kurar bir **sqlcmd** bağlantı toohello birincil çoğaltma Windows kimlik doğrulaması ile Merhaba dinleyicisi aracılığıyla:
   
        sqlcmd -S <listenerName> -E

Merhaba SQLCMD bağlantı hello birincil çoğaltmayı barındıran toohello SQL Server örneği otomatik olarak bağlanır. 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>Bir ek kullanılabilirlik grubu için bir IP adresi oluştur

Her kullanılabilirlik grubu ayrı bir dinleyicisi kullanır. Her dinleyicisi kendi IP adresi vardır. Kullanım hello aynı ek dinleyicileri için yük dengeleyici toohold başlangıç IP adresi. Bir kullanılabilirlik grubu oluşturduktan sonra başlangıç IP adresi toohello yük dengeleyici eklemek ve hello dinleyicisini yapılandırın.

tooadd bir IP adresi tooa yük dengeleyici hello Azure portal ile Merhaba aşağıdaki:

1. Hello Azure portal, hello yük dengeleyici içeren hello kaynak grubunu açın ve hello yük dengeleyici'ye tıklayın. 

2. Altında **ayarları**, tıklatın **ön uç IP havuzu**ve ardından **Ekle**. 

3. Altında **ön uç IP adresi Ekle**, hello ön ucu için bir ad atayın. 

4. Bu hello doğrulayın **sanal ağ** ve hello **alt** olan, hello SQL Server örnekleri hello aynı.

5. Başlangıç IP adresi hello dinleyici için ayarlayın. 
   
   >[!TIP]
   >Başlangıç IP adresi toostatic ayarlamak ve hello alt ağda şu anda kullanılmamaktadır bir adres yazın. Alternatif olarak, başlangıç IP adresi toodynamic ayarlamak ve hello yeni ön uç IP havuzu kaydedin. Bunu yaptığınızda hello Azure portalında kullanılabilir bir IP adresi toohello havuzu otomatik olarak atar. Ardından, hello ön uç IP havuzu yeniden açın ve hello atama toostatic değiştirin. 

6. Başlangıç IP adresi hello dinleyicisinin kaydedin. 

7. Ayarları aşağıdaki hello kullanarak bir sistem durumu araştırması ekleyin:

   |Ayar |Değer
   |:-----|:----
   |**Ad** |Bir ad tooidentify hello araştırma.
   |**Protokol** |TCP
   |**Bağlantı Noktası** |Tüm sanal makinelerde kullanılabilir olması gereken bir kullanılmayan TCP bağlantı noktası. Başka bir amaçla kullanılamaz. Hiçbir iki dinleyicileri hello kullanabilirsiniz aynı araştırma bağlantı noktası. 
   |**Aralığı** |Merhaba araştırma arasındaki süre miktarı çalışır. Merhaba varsayılan (5) kullanın.
   |**Sağlıksız durum eşiği.** |bir sanal makine sağlıksız kabul edilmeden önce başarısız olması ardışık eşikleri Hello sayısı.

8. Tıklatın **Tamam** toosave hello araştırma. 

9. Bir Yük Dengeleme kuralı oluşturun. Tıklatın **Yük Dengeleme kuralları**ve ardından **Ekle**.

10. Merhaba Yeni Yük Dengeleme kuralı ayarları aşağıdaki hello kullanarak yapılandırın:

   |Ayar |Değer
   |:-----|:----
   |**Ad** |Bir ad tooidentify hello Yük Dengeleme kuralı. 
   |**Ön uç IP adresi** |Oluşturduğunuz hello IP adresi seçin. 
   |**Protokol** |TCP
   |**Bağlantı Noktası** |Merhaba SQL Server örneklerini kullanarak hello bağlantı noktasını kullanır. Bunu değiştirmediyse bağlantı noktası 1433 varsayılan bir örnek kullanır. 
   |**Arka uç bağlantı noktası** |Aynı değeri olarak kullan hello **bağlantı noktası**.
   |**Arka uç havuzu** |Merhaba sanal makinelerle hello SQL Server örneklerini içeren hello havuzu. 
   |**Sistem durumu araştırması** |Oluşturduğunuz hello araştırma seçin.
   |**Oturum kalıcılığı** |None
   |**Boşta kalma zaman aşımı (dakika)** |Varsayılan (4)
   |**Kayan IP (doğrudan sunucu dönüşü)** | Etkin

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>Merhaba kullanılabilirlik grubu toouse hello yeni IP adresini yapılandırın

Merhaba ilk kullanılabilirlik grubu yapıldığında, uyguladığınız yineleme hello adımları Hello küme yapılandırma toofinish. Diğer bir deyişle, hello yapılandırma [küme toouse hello yeni IP adresi](#configure-the-cluster-to-use-the-load-balancer-ip-address). 

Merhaba dinleyici için bir IP adresi ekledikten sonra hello ek kullanılabilirlik grubu hello aşağıdakileri yaparak yapılandırın: 

1. Merhaba sonda bağlantı noktası hello yeni IP adresi için hem SQL Server sanal makinelerde açık olduğunu doğrulayın. 

2. [Küme Yöneticisi'nde hello istemci erişim noktası Ekle](#addcap).

3. [Merhaba IP kaynağı hello kullanılabilirlik grubu için yapılandırma](#congroup).

   >[!IMPORTANT]
   >Başlangıç IP adresi oluşturduğunuzda, toohello yük dengeleyici eklenen hello IP adresi kullanın.  

4. [Merhaba SQL Server kullanılabilirlik grubu kaynağının hello istemci erişim noktasında bağımlı hale](#dependencyGroup).

5. [Merhaba istemci erişimi olun noktası hello IP adresine bağımlı kaynak](#listname).
 
6. [PowerShell'de hello küme parametreleri ayarlamak](#setparam).

Merhaba kullanılabilirlik grubu toouse hello yeni IP adresi yapılandırdıktan sonra hello bağlantı toohello dinleyicisi yapılandırın. 

## <a name="next-steps"></a>Sonraki adımlar

- [Farklı bölgelerdeki Azure sanal makinelerde bir SQL Server Always On kullanılabilirlik grubu yapılandırma](virtual-machines-windows-portal-sql-availability-group-dr.md)
