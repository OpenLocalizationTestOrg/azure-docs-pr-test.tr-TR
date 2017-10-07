---
title: "aaaAzure SQL veritabanı bağlantısı mimarisi | Microsoft Docs"
description: "Bu belge hello Azure SQLDB bağlantı mimarisinden Azure içinde veya gelen açıklar Azure dışında."
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
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Azure SQL veritabanı bağlantısı mimarisi 

Bu makalede hello Azure SQL veritabanı bağlantısı mimarisini açıklar ve nasıl hello farklı bileşenleri toodirect trafiği tooyour Azure SQL veritabanı örneğini işlev açıklanmaktadır. Bu Azure SQL veritabanı bağlantısı bileşenlerinin toodirect ağ trafiği toohello Azure veritabanı içinden Azure bağlanan istemciler ve Azure dışında bağlantı istemcileri ile işlev. Bu makalede ayrıca bağlantı nasıl gerçekleştiğini kod örnekleri toochange sağlar ve hello konuları ilgili toochanging hello varsayılan bağlantı ayarları. Varsa herhangi bir sorunuz bu makaleyi okuduktan sonra Dhruv adresindeki temasa dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Bağlantı mimarisi

Aşağıdaki diyagramda hello hello Azure SQL veritabanı bağlantısı mimarisinin üst düzey bir genel bakış sağlar. 

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/architecture-overview.png)


Merhaba aşağıdakileri nasıl bir bağlantı hello Azure SQL veritabanı yazılım yük dengeleyici (SLB) ve hello Azure SQL veritabanı ağ geçidi ile kurulan tooan Azure SQL veritabanı olduğunu açıklayın.

- İstemcileri Azure içinde veya Azure dışında toohello bir ortak IP adresi vardır ve 1433 bağlantı noktasını dinler SLB bağlayın.
- Merhaba SLB trafiği toohello Azure SQL veritabanı ağ geçidi yönlendirir.
- Merhaba ağ geçidi hello trafiği toohello doğru proxy Ara yönlendirir.
- Merhaba proxy Ara hello trafiği toohello uygun Azure SQL veritabanı yönlendirir.

> [!IMPORTANT]
> Bu bileşenlerin her birini engelleme (DDoS) hizmeti koruma hello ağ ve hello uygulama katmanı yerleşik dağıtılmış.
>

## <a name="connectivity-from-within-azure"></a>Azure içinde bağlantısı

Azure içinde içinden bağlanan bağlantılarınızı bir bağlantı ilkesi varsa **yeniden yönlendirme** varsayılan olarak. Bir ilke **yeniden yönlendirme** kurulan toohello Azure SQL veritabanı hello TCP oturumu tamamlandıktan sonra bağlantılar, hello istemci oturumu anlamına gelir sonra toohello proxy Ara yazılımla bir değişiklik toohello hedef sanal IP yeniden yönlendirildi hello Azure SQL veritabanı ağ geçidi toothat hello proxy ara yazılım,. Bundan sonra tüm sonraki paketlere hello Azure SQL veritabanı ağ geçidi atlayarak doğrudan hello proxy ara yazılımı üzerinden, akış. Aşağıdaki diyagramda hello Bu trafik akışı gösterilmektedir.

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Azure dışında bağlantısı

Dış Azure'dan bağlanıyorsanız, bir bağlantı İlkesi bağlantınız **Proxy** varsayılan olarak. Bir ilke **Proxy** hello TCP oturumu yoluyla hello Azure SQL veritabanı ağ geçidi kuruldu ve tüm sonraki paketlere aracılığıyla akış anlamına gelir. ağ geçidi hello. Aşağıdaki diyagramda hello Bu trafik akışı gösterilmektedir.

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Azure SQL veritabanı ağ geçidi IP adresi

Şirket içi kaynaklardan tooconnect tooan Azure SQL database, Azure bölgeniz için tooallow giden ağ trafiğini toohello Azure SQL veritabanı ağ geçidi gerekir. Bağlantılarınızı hello ağ geçidi şirket kaynaklarına bağlanırken hello varsayılandır Proxy modunda bağlanırken yalnızca gidin.

Aşağıdaki tabloda hello hello Azure SQL veritabanı ağ geçidinin tüm veri bölgeleri için birincil ve ikincil IP'leri hello. Bazı bölgelerde, iki IP adresi vardır. Bu bölgelerde hello birincil IP adresi hello ağ geçidinin hello geçerli IP adresini ve hello ikinci IP adresi bir yük devretme IP adresidir. Başlangıç adresi toowhich, sunucu tookeep hello hizmet kullanılabilirliği yüksek taşıma Hello yük devretme adresidir. Bu bölgeler için giden tooboth hello IP adreslerinin izin öneririz. Merhaba ikinci IP adresi, Microsoft tarafından sahip olunan ve Azure SQL veritabanı tooaccept bağlantılar tarafından etkinleştirilene kadar hizmetlerin üzerinde dinlemez.

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

toochange hello kullan hello bir Azure SQL veritabanı sunucusu için Azure SQL veritabanı bağlantı İlkesi [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Bağlantı ilkeniz çok ayarlarsanız**Proxy**, tüm paketlerin akışı hello Azure SQL veritabanı ağ geçidi aracılığıyla ağ. Bu ayar için tooallow giden tooonly hello Azure SQL veritabanı ağ geçidi IP gerekir. Ayarı kullanarak **Proxy** ayarı'den daha fazla gecikme sahip **yeniden yönlendirme**. 
- Bağlantı ilkeniz ayarlıyorsanız **yeniden yönlendirme**, tüm ağ paketlerinin doğrudan toohello ara proxy akış. Bu ayar için tooallow giden toomultiple IP'leri gerekir. 

## <a name="script-toochange-connection-settings"></a>Komut dosyası toochange bağlantı ayarları

> [!IMPORTANT]
> Bu komut dosyası hello gerektirir [Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).
>

PowerShell Betiği aşağıdaki hello nasıl toochange hello bağlantı İlkesi gösterir.

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

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Sonraki adımlar

- Nasıl toochange hello Azure SQL veritabanı bağlantı ilkesi için bir Azure SQL veritabanı sunucusu hakkında daha fazla bilgi için bkz: [hello REST API'si oluşturma veya güncelleştirme sunucusu bağlantısı İlkesi kullanarak](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- ADO.NET 4.5 veya sonraki bir sürümünü kullanan istemciler için Azure SQL veritabanı bağlantı davranışı hakkında bilgi için bkz: [ADO.NET 4.5 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).
- Genel uygulama geliştirme genel bakış bilgileri için bkz: [SQL veritabanı uygulaması geliştirmeye genel bakış](sql-database-develop-overview.md).
