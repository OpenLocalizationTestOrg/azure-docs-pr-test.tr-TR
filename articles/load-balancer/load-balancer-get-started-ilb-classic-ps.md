---
title: "aaaCreate Azure iç yük dengeleyici - Klasik PowerShell | Microsoft Docs"
description: "Toocreate bir iç yük dengeleyici hello Klasik dağıtım modelinde PowerShell kullanarak nasıl öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>PowerShell kullanarak iç yük dengeleyici (klasik) oluşturmaya başlama

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Bulut hizmetleri](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](load-balancer-get-started-ilb-arm-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>Sanal makineler için iç yük dengeleyici oluşturma

bir iç yük dengeleyicisi ayarlayın ve bunların trafiğini tooit göndereceğiniz sunucuları hello toocreate toodo hello aşağıdaki vardır:

1. İç yük iş yükünün bir yük dengeli kümesi hello sunucular arasında dengeli gelen trafik toobe hello uç nokta olacak Dengeleme örneği oluşturun.
2. Merhaba gelen trafiği almak toohello sanal makineleri karşılık gelen uç noktalarını ekleyin.
3. Kendi trafiği toohello sanal IP (VIP) adresi iç Yük Dengeleme hello örneğinin toosend hello trafiği toobe yük dengeli gönderme hello sunucularını yapılandırın.

### <a name="step-1-create-an-internal-load-balancing-instance"></a>1. Adım: İç Yük Dengeleme örneği oluşturun

Var olan bir bulut hizmetini veya bölgesel bir sanal ağ altında dağıtılan bir bulut hizmeti için bir iç Yük Dengeleme örneği ile Windows PowerShell komutlarını aşağıdaki hello oluşturabilirsiniz:

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

Unutmayın hello bu kullanımını [Ekle AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet hello DefaultProbe parametre kümesi kullanır. Ek parametre kümeleri hakkında daha fazla bilgi için bkz. [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>2. adım: uç noktaları toohello iç Yük Dengeleme örneği ekleme

Örnek aşağıda verilmiştir:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>3. adım: sunucuları toosend kendi trafiği toohello yeni iç Yük Dengeleme uç noktasını yapılandırma

Sahip çok yapılandırdığınız hello sunucuları, trafiğine giderek toobe yükü dengelenmiş toouse hello yeni IP adresi (Merhaba VIP) hello iç Yük Dengeleme örnek olacak. Bu örnek hangi hello üzerinde iç Yük Dengeleme dinleme hello adresidir. Çoğu durumda, toojust gereksinim ekleyin veya hello VIP hello örneğinin iç Yük Dengeleme için bir DNS kaydı değiştirin.

Başlangıç IP adresi hello iç Yük Dengeleme örnek hello oluşturma sırasında belirtilen zaten hello VIP varsa. Aksi takdirde, komutları aşağıdaki hello gelen hello VIP görebilirsiniz:

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse bu komutları doldurun hello değerleri ve Kaldır merhaba < ve >. Örnek aşağıda verilmiştir:

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

Merhaba Get-AzureInternalLoadBalancer komutu görüntüsünü Merhaba, hello IP adresini not edin ve hello gerekli değişiklikleri tooyour sunucuları veya trafiği toohello VIP gönderilir DNS kayıtları tooensure olun.

> [!NOTE]
> Merhaba Microsoft Azure platformu statik, genel olarak yönlendirilebilir bir IPv4 adresi çeşitli yönetim senaryoları için kullanır. Başlangıç IP adresi 168.63.129.16 değil. Bu IP adresinin güvenlik duvarları tarafından engellenmesi beklenmeyen davranışlara neden olabilir.
> Saygı tooAzure ile iç Yük Dengeleme, bu IP adresi, yük dengelenmiş bir küme içinde sanal makineler için hello yük dengeleyici toodetermine hello sistem durumu araştırmalarının izleme tarafından kullanılır. Bir ağ güvenlik grubu kullanılan toorestrict trafiği tooAzure sanal makineleri bir dahili yük dengeli kümesindeki ya uygulanan tooa sanal ağ alt ağı ise, bir ağ güvenlik kuralı tooallow trafiği 168.63.129.16 eklendiğinden emin olun.

## <a name="example-of-internal-load-balancing"></a>İç yük dengeleme örneği

iki örnek yapılandırmalar için yük dengeli kümesi oluşturma hello son tooend işlemiyle toostep gördüğünüz hello bölümler.

### <a name="an-internet-facing-multi-tier-application"></a>İnternet'e yönelik, çok katmanlı uygulama

Tooprovide İnternete dönük web sunucuları kümesi için bir yük dengeli veritabanı hizmeti istiyorsunuz. İki sunucu kümesi de tek bir Azure bulut hizmetinde. Web sunucusu trafiği tooTCP bağlantı noktası 1433 hello veritabanı katmanı iki sanal makine arasında dağıtılmalıdır. Şekil 1'hello yapılandırmasını gösterir.

![Merhaba veritabanı katmanı için iç yük dengeli kümesi](./media/load-balancer-internal-getstarted/IC736321.png)

Merhaba yapılandırması hello aşağıdakilerden oluşur:

* Merhaba sanal makineleri barındıran hello mevcut bulut hizmeti mytestcloud adlandırılır.
* Merhaba iki varolan veritabanı sunucuları DB1, DB2 adlandırılır.
* Merhaba web katmanı Web sunucularının hello veritabanı katmanı toohello veritabanı sunucuları hello özel IP adresini kullanarak bağlanın. Başka bir seçenek hello sanal ağ için kendi DNS toouse olan ve hello iç yük dengeleyici kümesi için bir A kaydı el ile kaydedin.

Merhaba aşağıdaki komutları yapılandırma adlı yeni bir iç Yük Dengeleme örnek **ILBset** ve toohello iki veritabanı sunucularına karşılık gelen uç noktaları toohello sanal makineleri ekleyin:

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a>İç Yük Dengeleme yapılandırmasını kaldırma

sanal makine örneğinden bir iç yük dengeleyici, aşağıdaki komutları kullanın hello bir uç nokta olarak tooremove:

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

toouse bu komutları doldurun hello kaldırma hello değerlerde < ve >.

Örnek aşağıda verilmiştir:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

tooremove aşağıdaki komutları kullanın hello bir bulut hizmeti bir iç yük dengeleyici örneği:

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

Bu komutlar, toouse hello değer girin ve hello Kaldır < ve >.

Örnek aşağıda verilmiştir:

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>İç yük dengeleyici cmdlet'leri hakkında ek bilgi

tooobtain komutlar Windows PowerShell isteminde aşağıdaki hello çalıştırmak, iç Yük Dengeleme cmdlet'leri hakkında ek bilgi:

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>Sonraki adımlar

[Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)

