---
title: "aaaMonitor uygulama ağ geçidi için erişim günlükleri, performans günlükleri, arka uç sistem durumu ve ölçümleri | Microsoft Docs"
description: "Bilgi nasıl tooenable ve uygulama ağ geçidi için erişim günlüklerini ve performans günlüklerini yönetme"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Arka uç sistem durumu, tanılama günlüklerini ve uygulama ağ geçidi ölçümleri

Azure uygulama ağ geçidi kullanarak yolları aşağıdaki hello kaynaklarında izleyebilirsiniz:

* [Arka uç sistem durumu](#back-end-health): uygulama ağ geçidi arka uç havuzları ve PowerShell hello Azure portal aracılığıyla hello yetenek toomonitor hello hello hello sunucuları durumunu sağlar. Merhaba arka uç havuzları hello performans tanılama günlükleri aracılığıyla hello durumunu da bulabilirsiniz.

* [Günlükleri](#diagnostic-logs): günlükleri izin performans için erişim ve diğer veri toobe kaydedildi veya izleme amacıyla bir kaynaktan tüketilen.

* [Ölçümleri](#metrics): uygulama ağ geçidi şu anda bir ölçüm yok. Bu ölçüm, saniye başına baytların hello uygulama ağ geçidi hello verimini ölçer.

## <a name="back-end-health"></a>Arka uç sistem durumu

Uygulama ağ geçidi hello yetenek toomonitor hello hello arka uç havuzları hello portal, PowerShell ve hello komut satırı arabirimi (CLI) aracılığıyla tek tek üyeleri durumunu sağlar. Birleşik bir sistem durumu da bulabilirsiniz hello performans tanılama günlükleri aracılığıyla arka uç havuzları özeti. 

Merhaba arka uç sistem durumu raporu hello çıktı hello uygulama ağ geçidi durumu araştırma toohello arka uç örneklerinin yansıtır. Yoklama başarılı olduğunda ve geri hello son trafik alabilir, sağlıklı kabul edilir. Aksi takdirde, kötü olarak değerlendirilir.

> [!IMPORTANT]
> Bir uygulama ağ geçidi alt ağı üzerinde bir ağ güvenlik grubu (NSG) varsa, bağlantı noktası aralıkları 65503 65534 hello uygulama ağ geçidi alt gelen trafik için açın. Bu bağlantı noktaları hello arka uç sistem API toowork için gereklidir.


### <a name="view-back-end-health-through-hello-portal"></a>Merhaba Portalı aracılığıyla arka uç durumunu görüntüle

Merhaba Portalı'nda, arka uç sistem durumu otomatik olarak sağlanır. Mevcut bir uygulama ağ geçidi içinde seçin **izleme** > **arka uç sistem durumu**. 

(Bu bir NIC, IP veya FQDN olup olmadığı) hello arka uç havuzu içindeki her üyenin bu sayfada listelenir. Arka uç havuzu adını, bağlantı noktası, arka uç HTTP ayarları adı ve sistem durumu gösterilir. Sistem durumu için geçerli değerler **sağlıklı**, **sağlıksız**, ve **bilinmeyen**.

> [!NOTE]
> Arka uç sistem durumunu görüyorsanız, **bilinmeyen**, bu erişim toohello arka uç engellenmez bir NSG kuralı, bir kullanıcı tanımlı yönlendirme (UDR) veya özel DNS hello sanal ağındaki emin olun.

![Arka uç sistem durumu][10]

### <a name="view-back-end-health-through-powershell"></a>PowerShell aracılığıyla arka uç durumunu görüntüle

PowerShell koddan hello gösterir kullanarak tooview arka uç sistem durumu nasıl hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Azure CLI 2.0 aracılığıyla arka uç durumunu görüntüle

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>Sonuçlar

Aşağıdaki kod parçacığında hello hello yanıt örneği gösterilmektedir:

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Tanılama günlükleri

Günlükleri farklı türlerde içinde Azure toomanage kullanın ve uygulama ağ geçitleri giderebilirsiniz. Bu günlükler bazıları hello portalı üzerinden erişebilirsiniz. Tüm günlükler Azure Blob depolama alanından ayıklanan ve farklı Araçlar'da gibi görüntülenebilir [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md), Excel ve Power BI. Merhaba farklı türlerinden günlükleri listesi aşağıdaki hello hakkında daha fazla bilgi edinebilirsiniz:

* **Etkinlik günlüğü**: kullanabileceğiniz [Azure etkinlik günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md) (önceki adıyla işletimsel ve Denetim günlükleri olarak bilinir) tooview olmayan tüm işlemleri tooyour Azure aboneliği ve durumlarını gönderildi. Etkinlik günlüğü girişleri varsayılan olarak toplanır ve hello Azure portal görüntüleyebilirsiniz.
* **Erişim günlüğüne**: Bu günlük tooview uygulama ağ geçidi erişim desenlerini kullanın ve önemli bilgiler, dahil olmak üzere hello arayanın IP, istenen URL, yanıt gecikme, dönüş kodu ve bayt giriş ve çıkış analiz edin. Bir erişim günlüğü, her 300 saniyede toplanır. Bu günlük, uygulama ağ geçidi örneği başına bir kayıt içerir. Merhaba uygulama ağ geçidi örneği hello InstanceId özelliği tarafından belirlenebilir.
* **Performans günlüğü**: uygulama ağ geçidi örneklerinin nasıl gerçekleştirmekte bu günlük tooview kullanabilirsiniz. Bu günlük sunulan, toplam istekleri dahil olmak üzere her bir örnek, üretilen iş bayt performans bilgilerini yakalar, toplam istek sayısı sunulan, başarısız istek sayısını ve sağlıklı ve sağlıksız arka uç örnek sayısı. Bir performans günlüğü, her 60 saniyede toplanır.
* **Güvenlik Duvarı günlük**: hello web uygulaması güvenlik duvarı ile yapılandırılmış bir uygulama Ağ Geçidi algılama veya önleme modu üzerinden oturum bu günlük tooview hello isteklerini kullanabilirsiniz.

> [!NOTE]
> Günlükleri, yalnızca hello Azure Resource Manager dağıtım modelinde dağıtılan kaynaklar için kullanılabilir. Merhaba Klasik dağıtım modelinde kaynakların günlükleri kullanamazsınız. Merhaba daha iyi hello iki modellerinin anlamak için bkz: [anlama Resource Manager dağıtımını ve klasik dağıtımı](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.

Günlüklerinizi depolamak için üç seçeneğiniz vardır:

* **Depolama hesabı**: günlükleri uzun bir süre depolandığında ve gerektiğinde gözden depolama hesapları günlükleri için en iyi kullanımı.
* **Olay hub'ları**: olay hub'ları olan diğer güvenlik bilgilerini ile tümleştirmek için harika bir seçenek ve Olay yönetimi (SEIM) araçları kaynaklarınızı tooget uyarılar.
* **Günlük analizi**: günlük analizi uygulamanızın veya genel gerçek zamanlı izleme veya eğilimleri bakarak için en iyi şekilde kullanılır.

### <a name="enable-logging-through-powershell"></a>PowerShell aracılığıyla günlük kaydını etkinleştir

Etkinlik günlüğü her Resource Manager kaynak için otomatik olarak etkinleştirilir. Erişim ve bu günlükleri kullanılabilir hello veri toplama performans günlüğü toostart etkinleştirmeniz gerekir. Günlük, aşağıdaki adımları kullanın hello tooenable:

1. Merhaba günlük verilerinin depolandığı, depolama hesabınızın kaynak kimliği unutmayın. Bu değer hello şekildedir: /subscriptions/\<Subscriptionıd\>/resourceGroups/\<kaynak grubu adı\>/providers/Microsoft.Storage/storageAccounts/\<depolama hesabı adı\>. Aboneliğinizdeki herhangi bir depolama hesabı kullanabilirsiniz. Hello Azure portal toofind bu bilgileri kullanabilirsiniz.

    ![Portal: depolama hesabı kaynak kimliği](./media/application-gateway-diagnostics/diagnostics1.png)

2. Günlük kaydı etkin uygulama ağ geçidinizin kaynak kimliği unutmayın. Bu değer hello şekildedir: /subscriptions/\<Subscriptionıd\>/resourceGroups/\<kaynak grubu adı\>/providers/Microsoft.Network/applicationGateways/\<uygulama ağ geçidi ad\>. Merhaba portal toofind bu bilgileri kullanabilirsiniz.

    ![Portal: uygulama ağ geçidi kaynak kimliği](./media/application-gateway-diagnostics/diagnostics2.png)

3. Merhaba aşağıdaki PowerShell cmdlet'ini kullanarak tanılama günlük kaydını etkinleştir:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>Etkinlik günlükleri ayrı bir depolama hesabı gerektirmez. Depolama Hello kullanılması erişimi ve performans günlüğünü servis ücretleri oluşturur.

### <a name="enable-logging-through-hello-azure-portal"></a>Azure portal Hello günlüğü etkinleştirme

1. İçinde Azure portal Merhaba, kaynağınızı bulun ve tıklatın **tanılama günlükleri**.

   Uygulama ağ geçidi için üç günlük vardır:

   * Erişim günlüğü
   * Performans günlüğü
   * Güvenlik Duvarı günlüğü

2. veri toplama toostart, tıklatın **tanılamayı açın**.

   ![Tanılama açma][1]

3. Merhaba **tanılama ayarları** dikey penceresinde hello ayarları hello için tanılama günlükleri sağlar. Bu örnekte, günlük analizi hello günlükleri depolar. Tıklatın **yapılandırma** altında **günlük analizi** tooconfigure çalışma alanınızı. Olay hub'ları ve bir depolama hesabı toosave hello tanılama günlüklerini de kullanabilirsiniz.

   ![Merhaba yapılandırma işlemini başlatma][2]

4. Varolan bir Operations Management Suite (OMS) çalışma alanını seçin veya yeni bir tane oluşturun. Bu örnek, mevcut bir kullanır.

   ![OMS çalışma alanları için seçenekleri][3]

5. Hello ayarları onaylayın ve tıklatın **kaydetmek**.

   ![Tanılama ayarları dikey seçimleri][4]

### <a name="activity-log"></a>Etkinlik günlüğü

Azure hello etkinlik günlüğü varsayılan olarak oluşturur. Merhaba günlükleri 90 gün boyunca hello Azure olay günlüklerini deposunda korunur. Merhaba okuyarak Bu günlükler hakkında daha fazla bilgi [olayları ve etkinlik günlüğü görüntüle](../monitoring-and-diagnostics/insights-debugging-with-events.md) makalesi.

### <a name="access-log"></a>Erişim günlüğü

Ayrıntılı adımları önceki hello biçimde açıklandığı gibi her bir uygulama ağ geçidi örnek üzerinde yalnızca etkinleştirdikten ise hello erişim günlüğü oluşturulur. Merhaba veri hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır. Uygulama ağ geçidi'nin her erişim JSON biçiminde hello aşağıdaki örnekte gösterildiği gibi kaydedilir:


|Değer  |Açıklama  |
|---------|---------|
|örnek kimliği     | Uygulama ağ geçidi örneği, sunulacak hello isteği.        |
|ClientIP     | Kaynak IP hello istek için.        |
|clientPort     | Merhaba istek için kaynak bağlantı noktası.       |
|HttpMethod     | Merhaba isteği tarafından kullanılan HTTP yöntemi.       |
|requestUri     | Merhaba URI'sini isteği aldı.        |
|RequestQuery     | **Sunucu yönlendirilen**: hello isteğin gönderildiği arka uç havuzu örnek. </br> **X-AzureApplicationGateway-günlük-ID**: bağıntı hello istek için kullanılan kimliği. Merhaba arka uç sunucularda kullanılan tootroubleshoot trafiği sorunları olabilir. </br>**Sunucu durumu**: uygulama ağ geçidi hello arka uçtan alınan HTTP yanıt kodu.       |
|UserAgent     | Kullanıcı Aracısı'ndan hello HTTP istek üstbilgisi.        |
|httpStatus     | HTTP durum kodu toohello istemci uygulama ağ geçidi'nden döndürdü.       |
|httpVersion     | Merhaba İstek HTTP sürümü.        |
|ReceivedBytes     | Paket, alınan bayt cinsinden boyutu.        |
|SentBytes| Paket, gönderilen bayt cinsinden boyutu.|
|TimeTaken| Uzunluk, işlenen istek toobe ve gönderilen kendi yanıt toobe için geçen süre (milisaniye cinsinden). Bu uygulama ağ geçidi hello ilk bayta kalan süreyi hello yanıt işlemi tamamlanmadan gönderdiğinizde bir HTTP isteği toohello zaman alır hello zamandan hello aralığı olarak hesaplanır. Karşılama istek ve yanıt paketleri hello ağ üzerinden yolculuk hello süresi geçen süre alan genellikle hello toonote içerir önemlidir. |
|sslEnabled| SSL iletişimi toohello arka uç havuzları kullanılıp. Açma ve kapatma değerler geçerlidir.|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>Performans günlüğü

Ayrıntılı adımları önceki hello biçimde açıklandığı gibi her bir uygulama ağ geçidi örnek üzerinde yalnızca etkinleştirdiyseniz, hello performans günlüğü oluşturulur. Merhaba veri hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır. Merhaba performans günlüğü verilerini 1 dakikalık aralıklarla oluşturulur. Veri aşağıdaki hello kaydedilir:


|Değer  |Açıklama  |
|---------|---------|
|örnek kimliği     |  Uygulama ağ geçidi örneği performans verileri oluşturuluyor. Birden çok örnekli uygulama ağ geçidi için örneği başına bir satır yok.        |
|healthyHostCount     | Merhaba arka uç havuzundaki sağlıklı ana bilgisayar sayısı.        |
|unHealthyHostCount     | Merhaba arka uç havuzundaki sağlıksız ana bilgisayar sayısı.        |
|RequestCount     | Hizmet isteği sayısı.        |
|Gecikme süresi | Gecikme süresi (milisaniye cinsinden) hello örneği toohello gelen istekleri hello istekleri hizmet uç yedekleyin. |
|failedRequestCount| Başarısız istek sayısı.|
|Üretilen iş| Saniyedeki bayt cinsinden hello son günlük itibaren ortalama performansıdır.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Gecikme hello HTTP isteğin ilk baytını hello hello HTTP yanıtı son baytını hello gönderildiğinde alınan toohello zaman olduğunda hello zamandan hesaplanır. Buna ait hello toplamını hello uygulama ağ geçidi işleme artı hello maliyet ağ toohello end, arka uç alır tooprocess hello isteği hello hello saati.

### <a name="firewall-log"></a>Güvenlik Duvarı günlüğü

önceki adımları hello içinde ayrıntılı olarak her uygulama ağ geçidi için yalnızca etkinleştirdiyseniz, hello Güvenlik Duvarı günlük oluşturulur. Bu günlük, aynı zamanda bu hello web uygulaması güvenlik duvarı bir uygulama ağ geçidi üzerinde yapılandırılmış gerektirir. Merhaba veri hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır. Veri aşağıdaki hello kaydedilir:


|Değer  |Açıklama  |
|---------|---------|
|örnek kimliği     | Uygulama ağ geçidi örneği için hangi güvenlik duvarı veri oluşturuluyor. Birden çok örnekli uygulama ağ geçidi için örneği başına bir satır yok.         |
|clientIp     |   Kaynak IP hello istek için.      |
|clientPort     |  Merhaba istek için kaynak bağlantı noktası.       |
|requestUri     | Merhaba, bir URL isteği aldı.       |
|ruleSetType     | Kural türünü ayarlayın. Merhaba kullanılabilir OWASP değerdir.        |
|ruleSetVersion     | Kural kullanılan sürümünü ayarlayın. Değerleri 2.2.9 ve 3.0 kullanılabilir.     |
|RuleId     | Olay tetikleme hello kuralı kimliği.        |
|İleti     | Olay tetikleme hello için kullanıcı dostu iletisi. Daha fazla ayrıntı hello Ayrıntılar bölümünde verilmiştir.        |
|Eylem     |  Merhaba istek üzerinde gerçekleştirilecek eylem. Engellenen ve izin verilen değerleri kullanılabilir.      |
|Site     | Site için hangi hello günlük oluşturuldu. Şu anda, yalnızca genel kurallar genel olduğundan listelenir.|
|Ayrıntıları     | Olay tetikleme hello ayrıntıları.        |
|details.Message     | Merhaba kuralı açıklaması.        |
|details.Data     | Belirli veri, eşleşen hello kural isteğinde bulundu.         |
|details.File     | Merhaba kuralı bulunan yapılandırma dosyası.        |
|details.Line     | Merhaba olayı tetikleyen hello yapılandırma dosyasındaki satır numarası.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>Görüntüleme ve çözümleme hello etkinlik günlüğü

Görüntüleme ve yöntemleri aşağıdaki hello birini kullanarak Etkinlik günlüğü verilerini çözümleme:

* **Azure Araçları**: bilgi almanızı hello etkinlik günlüğü Azure PowerShell, hello Azure CLI, hello Azure REST API'si aracılığıyla ya da Azure portal hello. Her yöntem için adım adım yönergeler hello ayrıntılı [etkinlik işlemleri Resource Manager ile](../azure-resource-manager/resource-group-audit.md) makalesi.
* **Power BI**: henüz yoksa bir [Power BI](https://powerbi.microsoft.com/pricing) hesabı deneyebilirsiniz, ücretsiz. Hello kullanarak [Azure etkinlik günlükleri paketi Power BI için içerik](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), verilerinizi olduğu veya özelleştirin olarak kullanabileceğiniz, önceden yapılandırılmış panolarla çözümleyebilirsiniz.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>Görüntüleme ve hello erişim, performans ve güvenlik duvarı günlüklerini çözümleme

Azure [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md) Blob storage hesabınızdan hello sayacı ve olay günlük dosyaları toplayabilirsiniz. Görselleştirme ve güçlü arama özellikleri tooanalyze günlüklerinizi içerir.

Ayrıca, tooyour depolama hesabı bağlanmak ve erişim ve performans günlüklerini hello JSON günlük girişlerini almak. Hello JSON dosyaları indirdikten sonra bunları tooCSV dönüştürmek ve bunları Excel, Power BI veya diğer herhangi bir veri görselleştirmesi aracı görüntüleyin.

> [!TIP]
> Visual Studio ve sabitleri ve değişkenleri C# değerlerini değiştirmenin temel kavramları biliyorsanız hello kullanabilirsiniz [Dönüştürücü Araçları oturum](https://github.com/Azure-Samples/networking-dotnet-log-converter) github'dan kullanılabilir.
> 
> 

## <a name="metrics"></a>Ölçümler

Ölçümleri hello Portalı'nda performans sayaçları görüntüleyebileceğiniz belirli Azure kaynakları için bir özelliğidir. Uygulama ağ geçidi için bir ölçüm kullanıma sunulmuştur. Bu ölçümüdür üretilen iş ve hello Portalı'nda bkz. Tooan uygulama ağ geçidi bulun ve tıklatın **ölçümleri**. tooview hello değerleri, hello select performansı **kullanılabilir ölçümler** bölümü. Görüntü aşağıdaki hello farklı zaman aralıkları toodisplay hello veri kullanabileceğiniz bir örnek hello filtrelerle görebilirsiniz.

![Filtrelerle ölçüm görünümü][5]

toosee ölçümleri, geçerli bir listesini görmek [desteklenen Azure İzleyicisi ile ölçümleri](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

### <a name="alert-rules"></a>Uyarı kuralları

Bir kaynak için ölçümleri temel uyarı kuralları başlatabilirsiniz. Örneğin, bir uyarı bir Web kancası çağrısı veya hello uygulama ağ geçidi hello verimini belirli bir süre boyunca yukarıda, aşağıda veya bir eşik ise yönetici e-posta.

Aşağıdaki örneğine hello size bir e-posta tooan yönetici eşik bir işleme ihlallerini sonra gönderir bir uyarı kuralı oluşturmada size yardımcı olur:

1. Tıklatın **ölçüm uyarı Ekle** tooopen hello **Ekle kuralı** dikey. Bu dikey hello ölçümleri dikey penceresinden de ulaşabilir.

   !["Ölçüm uyarı Ekle" düğmesi][6]

2. Merhaba üzerinde **Ekle kuralı** dikey penceresinde hello adı, koşul, dolgu bölümleri bildir tıklatın ve **Tamam**.

   * Merhaba, **koşulu** Seçici, hello dört değerleri birini seçin: **büyük**, **büyük veya ona eşit**, **değerinden**, veya  **Küçük veya eşit**.

   * Merhaba, **süresi** bir süre 5 dakika too6 Saat Seçici, seçin.

   * Seçerseniz **sahipleri, Katkıda Bulunanlar ve okuyucular e-posta**, hello e-posta olabilir dinamik erişim toothat kaynağa sahip hello kullanıcıları temel alan. Aksi takdirde hello kullanıcıların virgülle ayrılmış bir listesini sağlayabilirsiniz **ek yönetici email(s)** kutusu.

   ![Kural dikey ekleme][7]

Merhaba eşik ihlal varsa, benzer toohello bir görüntü aşağıdaki hello içinde bir e-postalar ulaşır:

![E-posta ihlal edilen eşiği][8]

Ölçüm uyarı oluşturduktan sonra uyarıların bir listesi görüntülenir. Tüm hello uyarı kuralları genel bir bakış sağlar.

![Uyarılar ve kuralları listesi][9]

Uyarı bildirimleri hakkında daha fazla toolearn bkz [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Web kancası ve nasıl uyarıları ile kullanabilmek için hakkında daha fazla toounderstand ziyaret [bir Web kancası Azure ölçüm uyarıyı yapılandırmak](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="next-steps"></a>Sonraki adımlar

* Sayaç ve olay günlüklerini kullanarak Görselleştir [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md).
* [Azure etkinlik günlüğü Power BI ile görselleştirme](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog postası.
* [Görüntüleme ve Azure etkinlik günlükleri Power BI ve daha fazla çözümleme](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog postası.

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
