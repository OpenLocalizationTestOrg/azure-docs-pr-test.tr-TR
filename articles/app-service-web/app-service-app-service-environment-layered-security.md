---
title: "aaaLayered App Service ortamları ile güvenlik mimarisi"
description: "Uygulama hizmeti ortamları katmanlı güvenlik mimarisiyle uygulama."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>Uygulama hizmeti ortamları katmanlı güvenlik mimarisiyle uygulama
## <a name="overview"></a>Genel Bakış
Uygulama hizmeti ortamları sanal ağınıza dağıtılmış bir yalıtılmış çalışma zamanı ortamı sağlamak için geliştiriciler için her fiziksel uygulama katmanı düzeyleri farklı ağ erişim sağlayan bir katmanlı güvenlik mimarisi oluşturabilir.

Ortak desire toohide API'si arka uçları genel Internet erişimine karşı olduğu ve yalnızca Yukarı Akış web uygulamaları tarafından adlı API'leri toobe sağlar.  [Ağ güvenlik grupları (Nsg'ler)] [ NetworkSecurityGroups] App Service ortamları toorestrict genel erişim tooAPI uygulamaları içeren alt ağlarda kullanılabilir.

Hello diyagrama bir uygulama hizmeti ortamı dağıtılan Webapı tabanlı uygulama ile bir örnek mimari gösterilir.  Üç ayrı uygulama hizmeti ortamları üzerinde dağıtılan üç ayrı web app örnekleri olun arka uç çağrıları toohello aynı Webapı uygulama.

![Kavramsal mimarisi][ConceptualArchitecture] 

Merhaba yeşil artı işaretini gösteren bu hello "apiase" içeren hello alt ağındaki ağ güvenlik grubu kendisinden iyi çağrıları Yukarı Akış web uygulamaları hello gelen gelen çağrıları sağlar.  Aynı ağ güvenlik grubu açıkça reddeder hello erişim ancak toogeneral gelen hello Internet trafiği. 

Bu konunun geri kalanı Hello "apiase" içeren hello alt ağda hello adımları gerekli tooconfigure hello ağ güvenlik grubu anlatılmaktadır.

## <a name="determining-hello-network-behavior"></a>Merhaba ağ davranışı belirleme
Sipariş tooknow kuralları gereklidir, hangi ağ güvenliği hangi ağ istemcileri tooreach hello uygulama hizmeti ortamı içeren hello API uygulaması ve hangi istemcilerin engellenecek izin verilecek toodetermine gerekir.

Bu yana [güvenlik gruplarını (Nsg'ler) ağ] [ NetworkSecurityGroups] uygulanan toosubnets olan ve uygulama hizmeti ortamları dağıtılır, alt hello kuralları bir NSG içinde yer alan çok geçerli**tüm** bir uygulama hizmeti ortamı üzerinde çalıştırılan uygulamalar.  Bir ağ güvenlik grubu "apiase", "Merhaba apiase uygulama hizmeti ortamı hello tarafından korunur" üzerinde çalışan tüm uygulamaları içeren uygulanan toohello alt olduğunda bu makale için hello örnek mimarisi kullanarak, aynı güvenlik kuralları ayarlayın. 

* **Yukarı Akış arayanlar Hello giden IP adresini belirlemek:** hello IP adresini veya adreslerini hello Yukarı Akış arayanlar nedir?  Bu adresler erişim hello NSG açıkça izin verilen toobe gerekir.  Uygulama hizmeti ortamları arasında çağrıları "Internet" çağrıları kabul edilen olduğundan, bu hello giden IP adresi atanmış tooeach erişim hello NSG hello "apiase" alt ağı için izin verilen hello üç Yukarı Akış App Service ortamları gereksinimlerini toobe, anlamına gelir.   Uygulama hizmeti ortamı'nda çalışan uygulamalar hello görmek için hello giden IP adresi belirleme hakkında daha fazla bilgi [ağ mimarisi] [ NetworkArchitecture] genel bakış makalesi.
* **Merhaba arka uç API uygulaması toocall kendisini gerekecek mi?**  Bazen gözden kaçan önemli ve zarif noktası nerede toocall kendisini Merhaba arka uç uygulaması gereken hello senaryodur.  Bir uygulama hizmeti ortamı üzerinde bir arka uç API uygulamasının toocall kendisini gerekiyorsa, bu da değerlendirilir "Internet" çağrısı olarak.  Merhaba örnek mimarisinde bu hello "apiase" uygulama hizmeti ortamı de hello giden IP adresinden gelen erişimine gerektirir.

## <a name="setting-up-hello-network-security-group"></a>Ağ güvenlik grubu hello ayarlama
Merhaba, ayarladıktan sonra giden IP adreslerini bilinen, hello sonraki adıma tooconstruct bir ağ güvenlik grubu.  Sanal ağlar olarak Klasik sanal ağlar hem Resource Manager tabanlı için ağ güvenlik grupları oluşturulabilir.  Aşağıdaki Hello örnekleri oluşturma ve Powershell kullanarak bir Klasik sanal ağda bir NSG yapılandırma gösterir.

Boş bir NSG bu bölgede oluşturulan şekilde hello örnek mimarisi için Orta Güney ABD içinde hello ortamları bulunur:

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

İlk açık bir izin üzerinde hello makalesinde belirtildiği gibi hello Azure Yönetimi altyapısı için eklenen kural [gelen trafiği] [ InboundTraffic] App Service ortamları için.

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

Ardından, iki kural tooallow HTTP eklenir ve HTTPS çağrılarından hello ilk Yukarı Akış uygulama hizmeti ortamı ("fe1ase").

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Parlatıcı ve yineleme için ikinci ve üçüncü Yukarı Akış App Service ortamları ("fe2ase" ve "fe3ase") hello.

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Son olarak, böylece kendi içine geri çağırabilirsiniz hello arka uç API'nin uygulama hizmeti ortamı erişim toohello giden IP adresi verin.

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Başka bir ağ güvenlik kuralları her NSG hello Internet'ten gelen erişim engelle varsayılan kuralları kümesi olduğundan, varsayılan olarak yapılandırılan toobe gerekir.

Merhaba hello ağ güvenlik grubu kuralları tam listesini aşağıda gösterilmektedir.  Vurgulanır, hello son kural hangi açık olarak erişim izni olanlar dışındaki tüm arayanlar'ten gelen erişim nasıl engellediği unutmayın.

![NSG yapılandırma][NSGConfiguration] 

Merhaba son hello "apiase" uygulama hizmeti ortamı içeren tooapply hello NSG toohello alt adımdır.  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

Merhaba NSG uygulanır toohello olan bir alt ağ, yalnızca hello üç Yukarı Akış App Service ortamları ve hello uygulama hizmeti ortamı içeren hello API uç toocall hello "apiase" ortamına izin verilir.

## <a name="additional-links-and-information"></a>Ek bağlantıları ve bilgileri
Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

Hakkında bilgi [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md). 

Anlama [giden IP adreslerini] [ NetworkArchitecture] ve uygulama hizmeti ortamları.

[Ağ bağlantı noktalarını] [ InboundTraffic] App Service ortamları tarafından kullanılır.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
