---
title: "bir bulut hizmeti için aaaMutiple VIP'ler"
description: "MultiVIP genel bakış ve nasıl tooset bir bulut hizmeti üzerinde birden çok Vip"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a>Birden çok Vip bir bulut hizmeti için yapılandırma

Hello Azure tarafından sağlanan bir IP adresi kullanarak genel Internet üzerinden Azure bulut hizmetlerine erişebilir. Bu genel IP adresi başvurulan tooas VIP (sanal IP) olan bağlı olduğu bu yana toohello Azure yük dengeleyici ve hello bulut hizmeti içindeki sanal makine (VM) örnekleri hello değil. Bir bulut hizmeti içinde herhangi bir VM örneğine tek bir VIP kullanarak erişebilirsiniz.

Ancak, hangi ihtiyacınız olabilecek birden çok VIP senaryolar vardır bir giriş noktası toohello aynı bulut hizmeti. Örneğin, bulut hizmetinizin her site için farklı bir müşteri barındırılan olarak hello varsayılan bağlantı noktası 443'ü kullanarak SSL bağlantısı gerektiren veya Kiracı birden çok Web sitesi barındırabilir. Bu senaryoda, her Web sitesi için toohave farklı genel kullanıma yönelik bir IP adresi gerekir. Merhaba diyagramda hello üzerinde aynı birden çok SSL sertifikaları için bir tipik çok kiracılı web ile gerek duyduğu barındırma gösterilmiştir genel bağlantı noktası.

![Çoklu VIP SSL senaryosu](./media/load-balancer-multivip/Figure1.png)

Yukarıdaki tüm VIP'ler kullanım hello hello örnekte aynı genel bağlantı noktası (443) ve trafiği yeniden yönlendirilen tooone ya da daha fazla yük dengeli sanal makinelerin hello iç IP adresi hello bulut hizmetinin tüm hello Web siteleri barındırmak için bir benzersiz özel bağlantı noktası.

> [!NOTE]
> Başka bir durum gerektiren hello kullan hello birden çok Vip barındırma hello aynı sanal makinelerin kümesi üzerinde birden çok SQL AlwaysOn Kullanılabilirlik grubu dinleyicileri.

VIP'ler dinamik varsayılan toohello bulut hizmeti atanan hello gerçek IP adresi zaman içinde değişebilir anlamına gelir. oluşmasını, bir VIP hizmetiniz için ayırabilirsiniz olduğunu tooprevent. toolearn ayrılmış VIP'ler hakkında daha fazla bilgi görmek [ayrılmış genel IP](../virtual-network/virtual-networks-reserved-public-ip.md).

> [!NOTE]
> Lütfen bakın [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses/) üzerinde VIP'ler fiyatlandırma ve ayrılmış IP hakkında bilgi.

PowerShell tooverify Merhaba, bulut Hizmetleri tarafından kullanılan VIP'ler kullanın yanı sıra ekleyin ve VIP'ler kaldırmak, bir VIP tooan uç noktası ilişkilendirmek ve Yük Dengeleme özgü bir VIP yapılandırın.

## <a name="limitations"></a>Sınırlamalar

Şu anda çoklu VIP senaryoları aşağıdaki sınırlı toohello işlevdir:

* **Iaas yalnızca**. Bu gibi durumlarda, çoklu VIP yalnızca VM içermesi için bulut hizmetlerini etkinleştirebilirsiniz. Çoklu VIP PaaS rol örnekleri senaryolarla kullanamazsınız.
* **Yalnızca PowerShell**. PowerShell kullanarak yalnızca çoklu VIP yönetebilirsiniz.

Bu sınırlamaların geçicidir ve herhangi bir zamanda değişebilir. Emin toorevisit bu sayfa tooverify gelecekteki değişiklikler yapın.

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>Nasıl tooadd bir VIP tooa bulut hizmeti
tooadd bir VIP tooyour hizmeti, hello aşağıdaki PowerShell komutunu çalıştırın:

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

Bu komut, aşağıdaki örnek bir sonuç benzer toohello görüntüler:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>Nasıl bir bulut hizmetinden bir VIP tooremove
tooremove hello VIP tooyour hizmeti üzerinde aşağıdaki PowerShell komutunu çalıştırma hello hello örnekte ekledi:

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> Hiçbir ilişkili uç noktaları tooit varsa, yalnızca bir VIP kaldırabilirsiniz.


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>Nasıl bir bulut hizmeti tooretrieve VIP bilgileri
tooretrieve hello VIP'ler PowerShell Betiği aşağıdaki hello çalıştırmak bir bulut hizmetiyle ilişkili:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

Aşağıdaki örnek bir sonuç benzer toohello Hello betik görüntüler:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

Bu örnekte, 3 hello bulut hizmeti olan VIP'ler:

* **Vıp1** olan varsayılan VIP Merhaba, IsDnsProgrammedName hello değeri tootrue ayarlandığından, biliyor.
* **Vıp2** ve **Vip3** herhangi bir IP adresi yok olarak kullanılmaz. Bir uç nokta toohello VIP ilişkilendirirseniz yalnızca kullanılır.

> [!NOTE]
> Bir uç nokta ile ilişkili olduğunda, aboneliğiniz için ek VIP'ler yalnızca ücretlendirilir. Fiyatlandırma hakkında daha fazla bilgi için bkz: [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>Nasıl tooassociate bir VIP tooan uç noktası

PowerShell komutunu aşağıdaki hello çalıştırmak bir bulut hizmeti tooan uç noktasında bir VIP tooassociate:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

Merhaba komut oluşturur bağlantılı toohello VIP adlı bir uç nokta *vıp2* bağlantı noktasında *80*ve toohello adlı VM bağlantılar *myVM1* bir bulut hizmetinde adlı  *myService* kullanarak *TCP* bağlantı noktasında *8080*.

tooverify hello yapılandırması, hello aşağıdaki PowerShell komutunu çalıştırın:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

Hello çıkış benzer toohello örnek aşağıdaki gibidir:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>Tooenable nasıl Yük Dengeleme özgü bir VIP

Yük Dengeleyici amaçları için birden çok sanal makine tek bir VIP ilişkilendirebilirsiniz. Örneğin, adlandırılmış bir bulut hizmetine sahip *myService*ve adlı iki sanal makine *myVM1* ve *myVM2*. Ve bunların adlı birden çok Vip bulut hizmetiniz sahip *vıp2*. Tüm tooport trafiği tooensure istiyorsanız *81* üzerinde *vıp2* arasında dengeli *myVM1* ve *myVM2* bağlantı noktasında *8181* çalıştırın hello aşağıdaki PowerShell komut dosyası:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

Ayrıca, yük dengeleyici toouse farklı bir VIP güncelleştirebilirsiniz. Örneğin, hello aşağıdaki PowerShell komutu çalıştırırsanız, hello Yük Dengeleme kümesi toouse vıp1 adlı bir VIP değişir:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>Sonraki Adımlar

[Azure Yük Dengeleme için günlük analizi](load-balancer-monitor-log.md)

[Internet kullanıma yönelik Yük Dengeleyici genel bakış](load-balancer-internet-overview.md)

[Yük Dengeleyici Internet'e üzerinde çalışmaya başlama](load-balancer-get-started-internet-arm-ps.md)

[Sanal ağ genel bakış](../virtual-network/virtual-networks-overview.md)

[Ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx)
