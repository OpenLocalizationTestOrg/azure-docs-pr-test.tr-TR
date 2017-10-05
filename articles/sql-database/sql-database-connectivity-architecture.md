---
title: "Azure SQL veritabanı bağlantısı mimarisi | Microsoft Docs"
description: "Bu belgede Azure SQLDB bağlantı mimarisinden Azure içinde veya gelen açıklanmaktadır Azure dışında."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 8a1dd89c9e82483184ceb5d767190a5a5044265d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Azure SQL veritabanı bağlantısı mimarisi 

Bu makalede, Azure SQL veritabanı bağlantısı mimarisini açıklar ve nasıl doğrudan trafiğe örneğinizi Azure SQL veritabanı için farklı bileşenleri işlev açıklanmaktadır. İçinden Azure bağlanan istemciler ve istemcilerin Azure dışında bağlantı ile Azure veritabanı ağ trafiğini yönlendirmek için bu Azure SQL veritabanı bağlantısı bileşenleri işlevi. Bu makalede ayrıca bağlantı nasıl gerçekleştiğini değiştirmek için kod örnekleri ve varsayılan bağlantı ayarlarını değiştirmek için ilgili dikkat edilecek noktalar sağlar. Varsa herhangi bir sorunuz bu makaleyi okuduktan sonra Dhruv adresindeki temasa dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Bağlantı mimarisi

Aşağıdaki diyagramda Azure SQL veritabanı bağlantısı mimarisinin üst düzey bir genel bakış sağlar. 

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/architecture-overview.png)


Aşağıdaki adımlar, Azure SQL veritabanı yazılım yük dengeleyici (SLB) ve Azure SQL veritabanı ağ geçidi ile bir Azure SQL veritabanı için bir bağlantının nasıl kurulacağını açıklar.

- İstemcileri Azure içinde veya Azure dışında bir ortak IP adresi vardır ve 1433 bağlantı noktasını dinler SLB bağlayın.
- SLB Azure SQL veritabanı ağ trafiğini yönlendirir.
- Ağ geçidi doğru proxy Ara trafiğini yönlendirir.
- Proxy Ara trafiği uygun Azure SQL veritabanına yönlendirir.

> [!IMPORTANT]
> Bu bileşenlerin her birini koruma hizmeti (DDoS) ağ ve uygulama katmanı yerleşik reddi dağıtılmış.
>

## <a name="connectivity-from-within-azure"></a>Azure içinde bağlantısı

Azure içinde içinden bağlanan bağlantılarınızı bir bağlantı ilkesi varsa **yeniden yönlendirme** varsayılan olarak. Bir ilke **yeniden yönlendirme** TCP oturumu Azure SQL veritabanı için istemci oturum kurulduktan sonra bağlantıları sonra yönlendirildiği olduğunu proxy ara yazılımı için bir hedef sanal IP değişiklik olanlardan Azure ile anlamına gelir SQL veritabanı ağ geçidi, proxy ara yazılım. Bundan sonra tüm sonraki paketlere Azure SQL veritabanı ağ geçidi atlayarak doğrudan proxy ara yazılımı üzerinden, akış. Aşağıdaki diyagramda bu trafik akışı gösterilmektedir.

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Azure dışında bağlantısı

Dış Azure'dan bağlanıyorsanız, bir bağlantı İlkesi bağlantınız **Proxy** varsayılan olarak. Bir ilke **Proxy** Azure SQL veritabanı ağ geçidi TCP oturumun ve tüm sonraki paketlere akış yoluyla ağ geçidi anlamına gelir. Aşağıdaki diyagramda bu trafik akışı gösterilmektedir.

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Azure SQL veritabanı ağ geçidi IP adresi

Şirket içi kaynaklardan bir Azure SQL veritabanına bağlanmak için Azure SQL veritabanı ağ geçidi Azure bölgeniz için giden ağ trafiğine izin vermeniz gerekiyor. Bağlantılarınızı yoluyla ağ geçidi şirket içi kaynaklardan bağlanırken varsayılandır Proxy modunda bağlanırken yalnızca gidin.

Aşağıdaki tabloda Azure SQL veritabanı ağ geçidi tüm veri bölgeleri için birincil ve ikincil IP'leri listeler. Bazı bölgelerde, iki IP adresi vardır. Bu bölgelerde, birincil IP adresi ağ geçidi geçerli IP adresini ve ikinci IP adresi bir yük devretme IP adresidir. Yük devretme adresi için size hizmet kullanılabilirliği yüksek tutmak için sunucu taşıma adresidir. Bu bölgeler için her iki IP adreslerine giden izin öneririz. İkinci IP adresi, Microsoft tarafından sahip olunan ve bağlantıları kabul etmek üzere Azure SQL veritabanı tarafından etkinleştirilene kadar hizmetlerin üzerinde dinlemez.

| Bölge Adı | Birincil IP adresi | İkincil IP adresi |
| --- | --- |--- |
| Avustralya Doğu | 191.238.66.109 | 13.75.149.87 |
| Avustralya Güneydoğu | 191.239.192.109 | 13.73.109.251 |
| Güney Brezilya | 104.41.11.5 | |    
| Orta Kanada | 40.85.224.249 | |    
| Doğu Kanada | 40.86.226.166 | |
| Orta ABD | 23.99.160.139 | 13.67.215.62 |
| Doğu Asya | 191.234.2.139 | 52.175.33.150 |
| Doğu ABD 1 | 191.238.6.43 | 40.121.158.30 |
| Doğu ABD 2 | 191.239.224.107 | 40.79.84.180 |
| Hindistan Orta | 104.211.96.159  | |   
| Hindistan Güney | 104.211.224.146  | |
| Hindistan Batı | 104.211.160.80 | |
| Japonya Doğu | 191.237.240.43 | 13.78.61.196 |
| Japonya Batı | 191.238.68.11 | 104.214.148.156 |
| Kore Orta | 52.231.32.42 | |
| Kore Güney | 52.231.200.86 |  |
| Orta Kuzey ABD | 23.98.55.75 | 23.96.178.199 |
| Kuzey Avrupa | 191.235.193.75 | 40.113.93.91 |
| Orta Güney ABD | 23.98.162.75 | 13.66.62.124 |
| Güneydoğu Asya | 23.100.117.95 | 104.43.15.0 |
| UK Kuzey | 13.87.97.210 | |
| Birleşik Krallık Güney 1 | 51.140.184.11 | |    
| UK Güney 2 | 13.87.34.7 | |
| Birleşik Krallık Batı | 51.141.8.11  | |
| Batı Orta ABD | 13.78.145.25 | |
| Batı Avrupa | 191.237.232.75 | 40.68.37.158 |
| Batı ABD 1 | 23.99.34.75 | 104.42.238.205 |
| Batı ABD 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>Azure SQL veritabanı bağlantı ilkesini değiştirme

Bir Azure SQL veritabanı sunucusu için Azure SQL veritabanı bağlantı ilkesini değiştirmek için kullanın [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Bağlantı ilkeniz ayarlanmışsa **Proxy**, tüm Azure SQL veritabanı ağ geçidi üzerinden paket akışı ağ. Bu ayar, yalnızca Azure SQL veritabanı ağ geçidi IP giden izin vermeniz gerekir. Ayarı kullanarak **Proxy** ayarı'den daha fazla gecikme sahip **yeniden yönlendirme**. 
- Bağlantı ilkeniz ayarlıyorsanız **yeniden yönlendirme**, tüm paketler akışına doğrudan ara proxy ağ. Bu ayar için birden çok IP giden izin vermeniz gerekir. 

## <a name="script-to-change-connection-settings"></a>Bağlantı ayarlarını değiştirmek için komut dosyası

> [!IMPORTANT]
> Bu komut dosyası gerektirir [Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).
>

Aşağıdaki PowerShell betiğini nasıl bir bağlantı İlkesi değiştirileceğini gösterir.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting the current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting the property to ‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Sonraki adımlar

- Bir Azure SQL veritabanı sunucusu için Azure SQL veritabanı bağlantı ilkesini değiştirme hakkında daha fazla bilgi için bkz: [oluşturma veya güncelleştirme sunucusu bağlantısı REST API kullanarak İlkesi](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- ADO.NET 4.5 veya sonraki bir sürümünü kullanan istemciler için Azure SQL veritabanı bağlantı davranışı hakkında bilgi için bkz: [ADO.NET 4.5 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).
- Genel uygulama geliştirme genel bakış bilgileri için bkz: [SQL veritabanı uygulaması geliştirmeye genel bakış](sql-database-develop-overview.md).
