---
title: aaaUsing PowerShell toomanage Azure Traffic Manager'da | Microsoft Docs
description: "Trafik Yöneticisi ile Azure kaynak yöneticisi için PowerShell kullanma"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>PowerShell toomanage trafik Yöneticisi'ni kullanma

Azure Resource Manager hello tercih edilen Yönetim Azure hizmetlerinde arabirimidir. Azure Traffic Manager profillerini, Azure Resource Manager tabanlı API'ler ve araçlar kullanılarak yönetilebilir.

## <a name="resource-model"></a>Kaynak modeli

Azure Traffic Manager trafik Yöneticisi profili denir ayarlar koleksiyonu kullanılarak yapılandırılır. Hizmet uç noktaları toowhich trafiği listesini yönlendirilir ve bu profili, DNS ayarlarını, trafik yönlendirme ayarlarını, uç nokta izleme ayarlarını içerir.

Her trafik Yöneticisi profili 'TrafficManagerProfiles' türünde bir kaynak temsil edilir. Merhaba REST API düzeyi hello URI her profili için aşağıdaki gibidir:

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Azure PowerShell ayarlama

Bu yönergeler Microsoft Azure PowerShell kullanın. Merhaba aşağıdaki makalede açıklanır nasıl tooinstall ve Azure PowerShell yapılandırın.

* [Nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview)

Bu makaledeki Hello örnekler, varolan bir kaynak grubu olduğunu varsayalım. Komutu aşağıdaki hello kullanarak bir kaynak grubu oluşturabilirsiniz:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> Azure Resource Manager, tüm kaynak gruplarının bir konum olmasını gerektirir. Bu konum hello varsayılan olarak bu kaynak grubunda oluşturduğunuz kaynaklar için kullanılır. Trafik Yöneticisi profili kaynaklar olduğundan genel, bölgesel değil, ancak kaynak grubu konumu hello seçimine Azure Traffic Manager üzerinde etkisi yoktur.

## <a name="create-a-traffic-manager-profile"></a>Trafik Yöneticisi profili oluştur

toocreate bir Traffic Manager profilini kullanmak hello `New-AzureRmTrafficManagerProfile` cmdlet:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

Aşağıdaki tablonun hello hello parametreleri açıklanır:

| Parametre | Açıklama |
| --- | --- |
| Ad |Merhaba trafik Yöneticisi profili kaynak Hello kaynak adı. Aynı Hello profilleri kaynak grubu benzersiz adlara sahip olmalıdır. Bu ad, DNS sorgularını kullanılan hello DNS adı ayrıdır. |
| resourceGroupName |Merhaba kaynak grubu içeren hello profil kaynak Hello adı. |
| TrafficRoutingMethod |Hello trafik yönlendirme yöntemini kullanılan toodetermine hangi uç noktaya bir DNS sorgusu yanıtta döndürülen belirtir. Olası değerler 'Performans', 'Weighted' veya 'Priority' tır. |
| RelativeDnsName |Bu trafik Yöneticisi profili tarafından sağlanan hello DNS adının Hello ana bilgisayar adı bölümü belirtir. Bu değer, Azure Traffic Manager tooform hello tam etki alanı adıyla hello profilinin (FQDN) kullanılan hello DNS etki alanı adı ile birleştirilir. Örneğin, 'contoso' hello değerini ayarlama 'contoso.trafficmanager.net.' olur |
| TTL |Merhaba DNS için-yaşam süresi (TTL), saniye cinsinden belirtir. Merhaba yerel DNS Çözümleyicileri ve DNS istemcilerini bu TTL bildirir Bu trafik Yöneticisi profili için ne kadar süreyle toocache DNS yanıtları. |
| MonitorProtocol |Merhaba Protokolü toouse toomonitor uç nokta durumu belirtir. Olası değerler şunlardır: 'HTTP' ve 'HTTPS'. |
| MonitorPort |Merhaba TCP bağlantı noktası toomonitor uç nokta durumu kullanılan belirtir. |
| MonitorPath |Merhaba yolu göreli toohello uç nokta etki alanı adı tooprobe uç noktası durumu için kullanılan belirtir. |

Merhaba cmdlet ile Azure trafik Yöneticisi profili oluşturur ve karşılık gelen bir profil nesne tooPowerShell döndürür. Bu noktada, hello profili uç nokta içermiyor. Uç noktaları tooa trafik Yöneticisi profili ekleme hakkında daha fazla bilgi için bkz: [trafik Yöneticisi uç noktaları ekleme](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Trafik Yöneticisi profilini Al

tooretrieve var olan trafik Yöneticisi profili nesnesini kullanın hello `Get-AzureRmTrafficManagerProfle` cmdlet:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

Bu cmdlet bir trafik Yöneticisi Profil nesnesi döndürür.

## <a name="update-a-traffic-manager-profile"></a>Trafik Yöneticisi profilini güncelleştir

Traffic Manager profillerini değiştirme 3 adımlı işlem aşağıdaki gibidir:

1. Alma hello profili kullanarak `Get-AzureRmTrafficManagerProfile` veya hello profili tarafından döndürülen kullanın `New-AzureRmTrafficManagerProfile`.
2. Hello profil değiştirin. Ekleme ve uç noktaları kaldırın veya uç nokta veya profil parametrelerini değiştirin. Bu değişiklikler çevrimdışı işlemleridir. Yalnızca hello profili temsil eden bellekte hello yerel nesnesi değiştiriyorsunuz.
3. Hello kullanarak, değişiklikleri `Set-AzureRmTrafficManagerProfile` cmdlet'i.

Hello profilinin RelativeDnsName tüm profil özellikleri değiştirilebilir. toochange RelativeDnsName Merhaba, profili ve yeni bir adla yeni bir profil silmeniz gerekir.

Aşağıdaki örnek hello nasıl toochange hello profilinin TTL gösterir:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Trafik Yöneticisi uç noktaları üç tür vardır:

1. **Azure uç noktaları** Azure üzerinde barındırılan hizmeti
2. **Dış uç noktalar** Azure dışında barındırılan hizmeti
3. **İç içe uç noktaları** iç içe geçmiş kullanılan tooconstruct hiyerarşileri trafik Yöneticisi profillerine şunlardır. İç içe geçmiş uç noktaları karmaşık uygulamalar için Gelişmiş trafik yönlendirme yapılandırmaları etkinleştirin.

Her üç durumda, iki yolla uç noktalar eklenebilir:

1. Daha önce açıklanan 3 adımlı işlem kullanıyor. Bu yöntemin Hello avantajı, birkaç uç noktası değişiklikleri tek bir güncelleştirme yapılabilir ' dir.
2. Merhaba yeni AzureRmTrafficManagerEndpoint cmdlet'ini kullanarak. Bu cmdlet, tek bir işlemde bir uç nokta tooan varolan trafik Yöneticisi profili ekler.

## <a name="adding-azure-endpoints"></a>Azure uç noktaları ekleme

Azure uç noktaları Azure içinde barındırılan hizmetler başvuru. Azure uç noktaları iki tür desteklenir:

1. Azure Web Apps
2. (Olabilen ekli tooa yük dengeleyici veya bir sanal makine NIC) azure Publicıpaddress kaynaklar. Merhaba Publicıpaddress trafik Yöneticisi'nde kullanılan toobe atanmış bir DNS adı olmalıdır.

Her durumda:

* Merhaba hizmet hello 'uç noktası Targetresourceıd' parametresi kullanılarak belirtilen `Add-AzureRmTrafficManagerEndpointConfig` veya `New-AzureRmTrafficManagerEndpoint`.
* Merhaba 'Target' ve 'EndpointLocation' hello uç noktası Targetresourceıd tarafından kapsanan.
* Merhaba belirtme 'Weight' isteğe bağlıdır. Hello profil yapılandırılmış toouse hello 'Weighted' trafik yönlendirme yöntemini ise ağırlıkları yalnızca kullanılır. Aksi takdirde, bunlar yoksayılır. Belirtilen başlangıç değeri 1 ile 1000 arasında bir sayı olması gerekir. Merhaba varsayılan değer, '1' dir.
* Belirten hello 'Priority' isteğe bağlıdır. Hello profil yapılandırılmış toouse hello 'Priority' trafik yönlendirme yöntemini ise öncelikleri yalnızca kullanılır. Aksi takdirde, bunlar yoksayılır. Geçerli değerler 1 too1000 daha yüksek öncelik belirten alt ile değerlerdir. Bir uç nokta için belirtilmişse, tüm uç noktaları için belirtilmelidir. Atlanırsa, varsayılan değerleri '1'den başlayarak hello uç noktası listelenmez hello sırayla uygulanır.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Örnek 1: kullanarak Web uygulama uç noktaları ekleme`Add-AzureRmTrafficManagerEndpointConfig`

Bu örnekte, size bir trafik Yöneticisi profili oluşturun ve hello kullanarak iki Web uygulaması uç nokta ekleyin `Add-AzureRmTrafficManagerEndpointConfig` cmdlet'i.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Örnek 2: Publicıpaddress kullanarak uç nokta ekleme`New-AzureRmTrafficManagerEndpoint`

Bu örnekte, bir ortak IP adresi kaynağı toohello trafik Yöneticisi profili eklenir. Hello genel IP adresi yapılandırılmış bir DNS adına sahip olmalıdır ve her iki toohello NIC VM veya tooa yük dengeleyicinin bağlı olabilir.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Dış uç noktalar ekleme

Dış uç noktalar toodirect trafiği tooservices Azure dışında barındırılan Yöneticisi kullanır trafiği. Dış uç noktalar ya da Azure uç noktaları ile eklenen kullanarak `Add-AzureRmTrafficManagerEndpointConfig` arkasından `Set-AzureRmTrafficManagerProfile`, veya `New-AzureRMTrafficManagerEndpoint`.

Dış uç noktalar belirtirken:

* Merhaba 'Target' parametresini kullanarak Hello uç noktası etki alanı adı belirtilmelidir
* Merhaba 'EndpointLocation' Hello 'Performans' trafik yönlendirme yöntemini kullandıysanız gereklidir. Aksi takdirde isteğe bağlıdır. Merhaba değeri olmalıdır bir [geçerli Azure bölgesi adı](https://azure.microsoft.com/regions/).
* 'Ağırlık' hello ve 'Priority' isteğe bağlıdır.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Örnek 1: kullanarak dış uç noktalar ekleme `Add-AzureRmTrafficManagerEndpointConfig` ve`Set-AzureRmTrafficManagerProfile`

Bu örnekte, size bir trafik Yöneticisi profili oluşturun, iki dış uç noktalar ekleme ve hello değişiklikleri.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Örnek 2: kullanarak dış uç noktalar ekleme`New-AzureRmTrafficManagerEndpoint`

Bu örnekte, bir dış uç noktası tooan varolan profili ekleyin. Hello profil hello profili ve kaynak grubu adları kullanılarak belirtilir.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>'İç içe' uç noktaları ekleme

Her trafik Yöneticisi profili, tek bir trafik yönlendirme yöntemini belirtir. Ancak, tek bir trafik Yöneticisi profili tarafından sağlanan hello yönlendirme çok daha karmaşık trafik yönlendirme gerektiren senaryolar vardır. Trafik Yöneticisi profilleri toocombine hello birden fazla trafik yönlendirme yöntemini yararları yerleştirebilirsiniz. İç içe profil toooverride hello varsayılan trafik Yöneticisi davranışı toosupport daha büyük ve daha karmaşık uygulama dağıtımları izin verir. Daha ayrıntılı örnekler için bkz: [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md).

İç içe geçmiş uç noktalarını kullanarak belirli bir uç nokta türü, 'NestedEndpoints' hello üst profilde yapılandırılır. İç içe geçmiş uç noktaları belirtirken:

* Merhaba 'uç noktası Targetresourceıd' parametresini kullanarak Hello uç noktası belirtilmelidir
* Merhaba 'EndpointLocation' Hello 'Performans' trafik yönlendirme yöntemini kullandıysanız gereklidir. Aksi takdirde isteğe bağlıdır. Merhaba değeri olmalıdır bir [geçerli Azure bölgesi adı](http://azure.microsoft.com/regions/).
* 'Ağırlık' hello ve 'Priority' için olduğu gibi Azure uç noktaları isteğe bağlıdır.
* Merhaba 'MinChildEndpoints' parametresi isteğe bağlıdır. Merhaba varsayılan değer, '1' dir. Kullanılabilir uç nokta Hello sayısı bu eşiğin altına düşmesi durumunda hello üst profili hello alt profil 'düşürülmüş' ve diğer uç noktalardan hello üst profili trafiği toohello yönlendiren dikkate alır.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Örnek 1: kullanarak iç içe geçmiş uç noktaları ekleme `Add-AzureRmTrafficManagerEndpointConfig` ve`Set-AzureRmTrafficManagerProfile`

Bu örnekte, biz yeni trafik Yöneticisi alt ve üst profilleri oluşturma, hello alt iç içe geçmiş endpoint toohello üst öğe olarak ekleyin ve hello değişiklikleri uygulayın.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Bu örnekte okumanızdır, biz herhangi diğer uç noktaları toohello alt veya üst profilleri eklemediniz.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Örnek 2: kullanarak iç içe geçmiş uç noktaları ekleme`New-AzureRmTrafficManagerEndpoint`

Bu örnekte, biz var olan bir alt profilini bir iç içe geçmiş endpoint tooan varolan üst profili ekleyin. Hello profil hello profili ve kaynak grubu adları kullanılarak belirtilir.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Trafik Yöneticisi uç noktasını güncelleyin

Mevcut bir trafik Yöneticisi uç noktası iki yolu tooupdate vardır:

1. Merhaba trafik Yöneticisi profili kullanarak Al `Get-AzureRmTrafficManagerProfile`güncelleştirme hello profilindeki hello uç nokta özellikleri ve değişiklikleri kullanarak hello `Set-AzureRmTrafficManagerProfile`. Bu yöntem tek bir işlemde birden fazla uç mümkün tooupdate olma hello avantajına sahiptir.
2. Merhaba kullanan trafik Yöneticisi uç noktasını alın `Get-AzureRmTrafficManagerEndpoint`güncelleştirme hello uç nokta özellikleri ve değişiklikleri kullanarak hello `Set-AzureRmTrafficManagerEndpoint`. Merhaba uç noktaları hello profil dizisinde içine dizin gerektirmediğinden bu yöntem basittir.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Örnek 1: kullanarak uç noktaları güncelleştirme `Get-AzureRmTrafficManagerProfile` ve`Set-AzureRmTrafficManagerProfile`

Bu örnekte, iki uç nokta bir profil içinde hello öncelik değiştirin.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Örnek 2: bir uç nokta kullanarak güncelleştirme `Get-AzureRmTrafficManagerEndpoint` ve`Set-AzureRmTrafficManagerEndpoint`

Bu örnekte, var olan bir profili tek bir uç noktası hello ağırlığını değiştirin.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Etkinleştirme ve uç noktaları ve profilleri devre dışı bırakma

Trafik Yöneticisi etkin ve devre dışı, etkinleştirme ve tüm profillerini devre dışı bırakma izin vererek yanı sıra tekil uç noktalarını toobe sağlar.
Bu değişiklikler alma/güncelleştirme/ayarı hello uç noktası veya profili kaynaklar tarafından yapılabilir. toostreamline bu yaygın işlemler de adanmış cmdlet'leri desteklenir.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Örnek 1: Etkinleştirme ve trafik Yöneticisi profili devre dışı bırakma

tooenable bir Traffic Manager profilini kullanmak `Enable-AzureRmTrafficManagerProfile`. Hello profili, bir profil nesnesi kullanılarak belirtilebilir. Hello profil nesnesi hello ardışık düzeni aracılığıyla veya hello kullanarak geçirilebilir '-TrafficManagerProfile' parametresi. Bu örnekte, biz hello profili tarafından hello profili ve kaynak grubu adı belirtin.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

Trafik Yöneticisi profili toodisable:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

Merhaba devre dışı bırakma AzureRmTrafficManagerProfile cmdlet onaylamanızı ister. Bu istemi hello kullanılarak gizlenebilir. '-Force' parametresi.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Örnek 2: Etkinleştirme ve trafik Yöneticisi uç noktası devre dışı bırakma

tooenable bir trafik Yöneticisi uç noktası kullan `Enable-AzureRmTrafficManagerEndpoint`. İki yolu toospecify hello endpoint vardır

1. Merhaba ardışık düzeni geçirilen TrafficManagerEndpoint nesnesi veya hello kullanarak '-TrafficManagerEndpoint' parametresi
2. Merhaba uç nokta adı, uç nokta türü, profil adı ve kaynak grubu adı kullanma:

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Benzer şekilde, toodisable trafik Yöneticisi uç noktası:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

İle `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet için onay ister. Bu istemi hello kullanılarak gizlenebilir. '-Force' parametresi.

## <a name="delete-a-traffic-manager-endpoint"></a>Trafik Yöneticisi uç noktasını sil

tooremove tekil uç noktalarını kullanmak hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Bu cmdlet onaylamanızı ister. Bu istemi hello kullanılarak gizlenebilir. '-Force' parametresi.

## <a name="delete-a-traffic-manager-profile"></a>Trafik Yöneticisi profilini Sil

toodelete bir Traffic Manager profilini kullanmak hello `Remove-AzureRmTrafficManagerProfile` hello profili ve kaynak grubu adlarını belirtme cmdlet:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

Bu cmdlet onaylamanızı ister. Bu istemi hello kullanılarak gizlenebilir. '-Force' parametresi.

hello profil toobe silinmiş bir profil nesnesi kullanılarak da belirtilebilir:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

Bu sıra ayrıca yöneltilen:

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>Sonraki adımlar

[Trafik Yöneticisi izleme](traffic-manager-monitoring.md)

[Traffic Manager için performans konuları](traffic-manager-performance-considerations.md)
