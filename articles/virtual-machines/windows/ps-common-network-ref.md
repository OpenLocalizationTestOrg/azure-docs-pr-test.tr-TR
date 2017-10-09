---
title: "aaaCommon PowerShell komutları için Azure sanal ağlar | Microsoft Docs"
description: "Ortak PowerShell komutları tooget VM'ler için sanal ağ ve onun ilişkili kaynakları oluşturma başladı."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Azure Sanal Ağları için ortak PowerShell komutları

Bir sanal makine toocreate istiyorsanız, toocreate gerekir bir [sanal ağ](../../virtual-network/virtual-networks-overview.md) veya varolan bir sanal ağı hakkında biliyorsanız hangi hello VM eklenebilir. Genellikle, bir VM oluştururken de bu makalede açıklanan hello kaynakları oluşturma tooconsider gerekir.

Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooyour hesabında imzalama hakkında bilgi.

Bazı değişkenler birden fazla hello komutları bu makalede çalıştırılıyorsa sizin için yararlı olabilir:

- $location - hello ağ kaynaklarının başlangıç konumu. Kullanabileceğiniz [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind bir [coğrafi bölge](https://azure.microsoft.com/regions/) için çalışır.
- $myResourceGroup - hello hello ağ kaynaklarına bulunduğu hello kaynak grubunun adını.

## <a name="create-network-resources"></a>Ağ kaynakları oluşturun

| Görev | Komut |
| ---- | ------- |
| Alt ağ yapılandırmaları oluşturma |$subnet1 = [AzureRmVirtualNetworkSubnetConfig yeni](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -"mySubnet1" - AddressPrefix XX adı. X.X.X/XX<BR>$Altağ2 AzureRmVirtualNetworkSubnetConfig yeni =-"mySubnet2" - AddressPrefix XX adı. X.X.X/XX<BR><BR>Tipik bir ağ için bir alt ağ olabilir bir [internet'e yönelik Yük Dengeleyici](../../load-balancer/load-balancer-internet-overview.md) ve ayrı bir alt ağ için bir [iç yük dengeleyici](../../load-balancer/load-balancer-internal-overview.md). |
| Sanal ağ oluşturma |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -adı "myVNet" - ResourceGroupName $myResourceGroup-konum $location - AddressPrefix XX. X.X.X/XX-alt $subnet1, $Altağ2 |
| Test için benzersiz etki alanı adı |[Test-AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) - DomainNameLabel "myDNS"-Konum $location<BR><BR>Bir DNS etki alanı adı için belirttiğiniz bir [genel IP kaynağı](../../virtual-network/virtual-network-ip-addresses-overview-arm.md), oluşturan domainname.location.cloudapp.azure.com toohello genel IP adresi için bir eşleme hello Azure tarafından yönetilen DNS sunucuları. Merhaba adı yalnızca harf, rakam ve kısa çizgi içerebilir. Merhaba ilk ve son karakter bir harf veya sayı olması gerekir ve hello etki alanı adını Azure konumuna içinde benzersiz olmalıdır. Varsa **True** döndürülür, önerilen adınız genel benzersiz. |
| Genel IP adresi oluşturma |$pip = [yeni AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -- ResourceGroupName $myResourceGroup - DomainNameLabel "myDNS" "myPublicIp" ad-konum $location - AllocationMethod dinamik<BR><BR>Merhaba genel IP adresi daha önce test ve hello ön uç yapılandırma hello yük dengeleyici tarafından kullanılan hello etki alanı adını kullanır. |
| Bir ön uç IP yapılandırması oluştur |$frontendIP = [yeni AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -adı "myFrontendIP" - Publicıpaddress $pip<BR><BR>Merhaba ön uç yapılandırma için gelen ağ trafiğini daha önce oluşturduğunuz hello ortak IP adresini içerir. |
| Arka uç adres havuzu oluşturma |$beAddressPool = [yeni AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -adı "myBackendAddressPool"<BR><BR>Merhaba, hello arka uç için iç adresleri bir ağ arabirimi üzerinden erişilen yük sağlar. |
| Bir araştırma oluşturma |$healthProbe = [yeni AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -adı "myProbe" - RequestPath 'HealthProbe.aspx'-protokolü http-bağlantı noktası 80 - Intervalınseconds 15 - ProbeCount 2<BR><BR>Sistem durumu kullanılan araştırmalar toocheck kullanılabilirliği hello arka uç adres havuzundaki sanal makineler örnekleri içerir. |
| Bir Yük Dengeleme kuralı oluştur |$lbRule = [yeni AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) -adı HTTP - Frontendıpconfiguration $frontendIP - BackendAddressPool $beAddressPool-araştırma $healthProbe-protokol Tcp - FrontendPort 80 - BackendPort 80<BR><BR>Genel bir bağlantı noktası hello yük dengeleyicide hello arka uç adres havuzu tooa bağlantı noktası atama kurallarını içerir. |
| Gelen NAT kuralı oluştur |$inboundNATRule = [yeni AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -$frontendIP "myInboundRule1" - Frontendıpconfiguration ad-protokol TCP - FrontendPort 3441 - BackendPort 3389<BR><BR>Bağlantı noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir. |
| Yük dengeleyici oluşturma |$loadBalancer = [yeni AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) - ResourceGroupName $myResourceGroup-adı "myLoadBalancer"-Konum $location - Frontendıpconfiguration $frontendIP - Inboundnatrule $inboundNATRule - LoadBalancingRule $lbRule - BackendAddressPool $beAddressPool-araştırma $healthProbe |
| Bir ağ arabirimi oluştur |$nıc1 = [yeni AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) - ResourceGroupName $myResourceGroup-adı "myNIC" - Konum $location - PrivateIpAddress XX. X.X.X-alt $Altağ2 - LoadBalancerBackendAddressPool $loadBalancer.BackendAddressPools[0] - Ipconfiguration'a $loadBalancer.InboundNatRules[0]<BR><BR>Merhaba genel IP adresi ve daha önce oluşturduğunuz sanal ağ alt ağını kullanarak bir ağ arabirimi oluşturur. |

## <a name="get-information-about-network-resources"></a>Ağ kaynakları hakkında bilgi edinin

| Görev | Komut |
| ---- | ------- |
| Sanal ağlar |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) - ResourceGroupName $myResourceGroup<BR><BR>Merhaba kaynak grubundaki tüm hello sanal ağları listeler. |
| Bir sanal ağ hakkında bilgi edinin |Get-AzureRmVirtualNetwork-adı "myVNet" - ResourceGroupName $myResourceGroup |
| Bir sanal ağ alt ağların listesi |Get-AzureRmVirtualNetwork-adı "myVNet" - ResourceGroupName $myResourceGroup &#124; Alt ağları seçin |
| Bir alt ağ hakkında bilgi edinin |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -$vnet "mySubnet1" - VirtualNetwork adı<BR><BR>Merhaba alt ağ bilgilerini hello belirtilen sanal ağda alır. Merhaba $vnet değerini Get-AzureRmVirtualNetwork tarafından döndürülen hello nesnesini temsil eder. |
| IP adresleri listesi |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) - ResourceGroupName $myResourceGroup<BR><BR>Merhaba kaynak grubunda Hello ortak IP adresleri listelenir. |
| Liste yük Dengeleyiciler |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) - ResourceGroupName $myResourceGroup<BR><BR>Merhaba kaynak grubundaki tüm hello yük dengeleyicileri listeler. |
| Liste ağ arabirimleri |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) - ResourceGroupName $myResourceGroup<BR><BR>Merhaba kaynak grubundaki tüm hello ağ arabirimlerini listeler. |
| Bir ağ arabirimi hakkında bilgi edinin |Get-AzureRmNetworkInterface-$myResourceGroup "myNIC" - ResourceGroupName adı<BR><BR>Belirli bir ağ arabiriminde hakkındaki bilgileri alır. |
| Bir ağ arabiriminin Hello IP yapılandırmasını al |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -adı "myNICIP" - Networkınterface $nic<BR><BR>Merhaba hello belirtilen ağ arabiriminin IP yapılandırması hakkındaki bilgileri alır. Merhaba $nic değerini Get-AzureRmNetworkInterface tarafından döndürülen hello nesnesini temsil eder. |

## <a name="manage-network-resources"></a>Ağ kaynaklarını yönetme

| Görev | Komut |
| ---- | ------- |
| Alt ağ tooa sanal ağ ekleme |[Ekleme AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) - AddressPrefix XX. X.X.X/XX-$vnet "mySubnet1" - VirtualNetwork adı<BR><BR>Bir alt tooan varolan sanal ağ ekler. Merhaba $vnet değerini Get-AzureRmVirtualNetwork tarafından döndürülen hello nesnesini temsil eder. |
| Bir sanal ağı silme |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -adı "myVNet" - ResourceGroupName $myResourceGroup<BR><BR>Belirtilen sanal ağ Hello hello kaynak grubundan kaldırır. |
| Bir ağ arabirimi Sil |[Remove-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -$myResourceGroup "myNIC" - ResourceGroupName adı<BR><BR>Merhaba belirtilen ağ arabirimi hello kaynak grubundan kaldırır. |
| Yük dengeleyici silme |[Remove-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -adı "myLoadBalancer" - ResourceGroupName $myResourceGroup<BR><BR>Yük Dengeleyici hello kaynak grubundan kaldırır hello belirtilmiş. |
| Bir ortak IP adresini Sil |[Remove-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-adı "myIpAddress" - ResourceGroupName $myResourceGroup<BR><BR>Kaldırır hello hello kaynak grubundan genel IP adresi belirtildi. |

## <a name="next-steps"></a>Sonraki Adımlar
* Oluşturulan yeni kullanım hello ağ arabirimi, [bir VM oluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Hakkında öğrenin [birden çok ağ arabirimi ile bir VM oluşturma](../../virtual-network/virtual-networks-multiple-nics.md).

