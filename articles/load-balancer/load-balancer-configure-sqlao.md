---
title: "aaaConfigure yük dengeleyici her zaman açık SQL için | Microsoft Docs"
description: "Yük Dengeleyici toowork her zaman SQL ve nasıl tooleverage powershell toocreate yük dengeleyici hello SQL uygulaması için yapılandırın"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a>Yük Dengeleyici SQL için her zaman yapılandırın

SQL Server AlwaysOn Kullanılabilirlik grupları şimdi ILB ile çalıştırabilirsiniz. Kullanılabilirlik grubu SQL Server'ın flagship için yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümüdür. Merhaba kullanılabilirlik grubu dinleyicisi sağlayan istemci uygulamaları tooseamlessly hello hello yapılandırmasında hello çoğaltmaların sayısı yedeklemiş toohello birincil çoğaltma bağlanın.

Merhaba dinleyicisi (DNS) ad eşlenen tooa yük dengeli IP adresi ve Azure'nın yük dengeleyici hello gelen trafiği tooonly hello birincil sunucusu hello çoğaltma kümesinde yönlendirir.

ILB desteği SQL Server AlwaysOn (dinleyici) uç noktaları için kullanabilirsiniz. Şimdi hello dinleyicisi hello erişilebilirliğini üzerinde denetimi yoktur ve hello yük dengeli IP adresi, sanal ağ (VNet) belirli bir alt ağdan seçebilirsiniz.

Merhaba Dinleyicide ILB kullanarak, SQL sunucusu uç noktası hello (örneğin Server 1433; tcp:ListenerName, = veritabanı DatabaseName =) yalnızca tarafından erişilebilen:

* Aynı sanal ağ hizmetleri ve Vm'lerde hello
* Hizmetler ve bağlı şirket içi ağ üzerinden VM'ler
* Hizmetler ve VM'lerin birbirine bağlı sanal ağlar

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

Şekil 1 - SQL AlwaysOn Internet'e yönelik Yük Dengeleyici ile yapılandırılmış

## <a name="add-internal-load-balancer-toohello-service"></a>İç yük dengeleyici toohello Hizmet Ekle

1. Aşağıdaki örneğine hello biz 'Alt ağ-1' adlı bir alt ağ içeren bir sanal ağ yapılandırın:

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. Her bir VM üzerinde ILB için yük dengeli uç noktaları ekleme

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    Merhaba yukarıdaki örnekte, 2 VM'ın adlandırılan "sqlsvc1" ve "sqlsvc2" çalışan elinizde "Sqlsvc" Merhaba buluta hizmet. ILB ile Merhaba oluşturduktan sonra `DirectServerReturn` geçiş, eklediğiniz yük dengeli uç noktalar toohello ILB tooallow SQL tooconfigure hello dinleyicileri hello kullanılabilirlik grupları için.

SQL AlwaysOn hakkında daha fazla bilgi için bkz: [Azure'da AlwaysOn Kullanılabilirlik grubu için bir iç yük dengeleyici yapılandırma](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

## <a name="see-also"></a>Ayrıca Bkz.
[Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama](load-balancer-get-started-internet-arm-ps.md)

[Bir iç yük dengeleyici yapılandırma kullanmaya başlama](load-balancer-get-started-ilb-arm-ps.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
