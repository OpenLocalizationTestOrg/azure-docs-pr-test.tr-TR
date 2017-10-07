---
title: "Günlük analizi anahtar kasası çözümde aaaAzure | Microsoft Docs"
description: "Azure anahtar kasası günlükleri günlük analizi tooreview içinde hello Azure anahtar kasası çözüm kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Günlük analizi Azure anahtar kasası Analytics çözümde

![Anahtar kasası simgesi](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

Azure anahtar kasası AuditEvent günlüklerini günlük analizi tooreview içinde hello Azure anahtar kasası çözüm kullanabilirsiniz.

toouse hello çözüm tooenable günlüğü Azure anahtar kasası tanılama ve doğrudan hello tanılama tooa günlük analizi çalışma alanı gerekir. Gerekli toowrite hello günlükleri tooAzure Blob Depolama olmadığı.

> [!NOTE]
> Ocak 2017 ' Analytics değiştirilen anahtar kasası tooLog günlükleri gönderme şekilde hello desteklenir. Merhaba anahtar kasası çözümü kullanıyorsanız gösterir *(kullanım dışı)* hello başlığında çok başvurun[hello eski anahtar kasası çözüm'den geçiş](#migrating-from-the-old-key-vault-solution) adımları toofollow gerekir.
>
>

## <a name="install-and-configure-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
Aşağıdaki yönergeler tooinstall hello kullanın ve hello Azure anahtar kasası çözüm yapılandırın:

1. Hello Azure anahtar kasası çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).
2. Merhaba anahtar kasası kaynakları toomonitor için günlüğü, her iki hello kullanarak tanılamayı etkinleştirin [portal](#enable-key-vault-diagnostics-in-the-portal) veya [PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Anahtar kasası tanılama hello portalında etkinleştir

1. Toohello anahtar kasası kaynak toomonitor Hello Azure portalına gidin
2. Seçin *tanılama günlükleri* sayfası aşağıdaki tooopen hello

   ![Azure anahtar kasası döşeme görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. Tıklatın *tanılamayı açın* sayfası aşağıdaki tooopen hello

   ![Azure anahtar kasası döşeme görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. Tanılama üzerinde tooturn tıklatın *üzerinde* altında *durumu*
5. Merhaba onay kutusunu tıklatın *tooLog Analytics Gönder*
6. Varolan bir günlük analizi çalışma alanını seçin veya bir çalışma alanı oluşturma
7. tooenable *AuditEvent* günlükleri, günlük altında hello onay kutusunu tıklatın
8. Tıklatın *kaydetmek* tooenable hello günlüğe tanılama tooLog analizi

### <a name="enable-key-vault-diagnostics-using-powershell"></a>Anahtar kasası tanılamayı PowerShell kullanarak etkinleştirme
PowerShell Betiği aşağıdaki hello nasıl bir örnek sağlar toouse `Set-AzureRmDiagnosticSetting` tooenable anahtar kasası için günlüğü Tanılama:
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Azure anahtar kasası veri toplama ayrıntılarını gözden geçirin
Azure anahtar kasası çözüm tanılama günlükleri doğrudan hello anahtar Kasası ' toplar.
Gerekli toowrite hello günlükleri tooAzure Blob Depolama değil ve aracı için veri toplama gereklidir.

Merhaba aşağıdaki tabloda veri toplama yöntemleri ve Azure anahtar kasası için verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.

| Platform | Doğrudan Aracısı | Systems Center Operations Manager Aracısı | Azure | Operations Manager gerekli? | Operations Manager Aracısı verilerinin yönetim grubu gönderilen | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  | geldiğinde |

## <a name="use-azure-key-vault"></a>Azure Key Vault kullanma
Çalıştırdıktan sonra [hello çözümü](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), hello tıklayarak hello anahtar kasası verileri görüntüleme **Azure anahtar kasası** döşeme hello **genel bakış** günlük analizi sayfası.

![Azure anahtar kasası döşeme görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

Merhaba tıklattıktan sonra **genel bakış** kutucuğu toodetails kategorileri aşağıdaki hello için günlükleri ve ardından ayrıntıya özetlerini görüntüleyebilirsiniz:

* Tüm anahtar kasası işlemleri zaman içinde hacmi
* İşlem birimleri zaman içinde başarısız oldu
* İşlem tarafından işletimsel ortalama gecikme süresi
* Birden fazla 1000 ms ele işlemlerinin hello sayısı ve birden fazla 1000 ms ele işlemleri listesini işlemleri için hizmet kalitesi

![Azure anahtar kasası Pano görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Azure anahtar kasası Pano görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>herhangi bir işlem için tooview ayrıntıları
1. Merhaba üzerinde **genel bakış** hello sayfasında, **Azure anahtar kasası** döşeme.
2. Merhaba üzerinde **Azure anahtar kasası** panoyu hello Kanatlar birinde hello özet bilgileri gözden geçirin ve ardından bir tooview hakkında ayrıntılı bilgi, hello günlük arama sayfasında.

    Merhaba günlük arama sayfaları hiçbirinde, sonuçları zaman, ayrıntılı sonuçları ve günlük arama geçmişi görüntüleyebilirsiniz. Modelleri toonarrow hello sonuçlarına göre de filtre uygulayabilirsiniz.

## <a name="log-analytics-records"></a>Log Analytics kayıtları
Hello Azure anahtar kasası çözüm çözümler türünü içeren kayıtları **KeyVaults** gelen toplanan [AuditEvent günlükleri](../key-vault/key-vault-logging.md) Azure tanılama.  Bu kayıtlar için özellikleri aşağıdaki tablonun hello şunlardır:  

| Özellik | Açıklama |
|:--- |:--- |
| Tür |*AzureDiagnostics* |
| SourceSystem |*Azure* |
| CallerIpAddress |Merhaba isteği yapan hello istemcinin IP adresi |
| Kategori | *AuditEvent* |
| CorrelationId |İstemci hello isteğe bağlı bir GUID toocorrelate istemci-tarafı günlüklerini Hizmet tarafı (anahtar kasası) günlükleriyle geçirebilirsiniz. |
| DurationMs |Milisaniye cinsinden tooservice hello REST API isteği, geçen süre. Merhaba istemci tarafında ölçmek hello süre bu süreyle eşleşmeyebilir şekilde bu kez ağ gecikmesini içermez. |
| httpStatusCode_d |HTTP durum kodu Hello istek tarafından döndürülen (örneğin, *200*) |
| id_s |Merhaba isteğin benzersiz kimliği |
| identity_claim_appid_g | Merhaba uygulama kimliği için GUID |
| OperationName |Açıklandığı gibi hello işlemi, adı [Azure anahtar kasası günlüğü](../key-vault/key-vault-logging.md) |
| OperationVersion |Merhaba istemci tarafından istenen REST API sürümü (örneğin *2015-06-01*) |
| requestUri_s |Merhaba istek URI'sini |
| Kaynak |Merhaba anahtar kasasının adı |
| ResourceGroup |Merhaba anahtar kasasının kaynak grubu |
| ResourceId |Azure Resource Manager Kaynak Kimliği. Anahtar kasası günlükleri için bu hello anahtar kasası kaynak kimliğidir. |
| ResourceProvider |*MICROSOFT. KEYVAULT* |
| ResourceType | *KASALARI* |
| ResultSignature |HTTP durumu (örneğin, *Tamam*) |
| ResultType |REST API isteğinin sonucunu (örneğin, *başarı*) |
| SubscriptionId |Merhaba anahtar kasası içeren hello aboneliğin Azure abonelik kimliği |

## <a name="migrating-from-hello-old-key-vault-solution"></a>Merhaba eski anahtar kasası çözüm'den geçiş
Ocak 2017 ' Analytics değiştirilen anahtar kasası tooLog günlükleri gönderme şekilde hello desteklenir. Bu değişiklikler hello aşağıdaki avantajları sağlar:
+ TooLog Analytics hello olmadan gereken doğrudan toouse bir depolama hesabı günlüklerine yazılır
+ Günlük analizi kullanılabilir olmasını durduracak toothem günlükleri olduğunda hello zamandan daha az gecikme oluşturulan
+ Daha az yapılandırma adımları
+ Azure tanılama tüm türleri için ortak bir biçimi

toouse hello çözüm güncelleştirildi:

1. [Anahtar Kasası'nı doğrudan tooLog Analytics gönderilen tanılama toobe yapılandırın](#enable-key-vault-diagnostics-in-the-portal)  
2. Açıklanan hello işlemi kullanarak Hello Azure anahtar kasası çözümünü etkinleştirme [hello Çözümleri Galerisi çözümlerinden günlük analizi Ekle](log-analytics-add-solutions.md)
3. Tüm kayıtlı sorgu, panolar veya uyarıları toouse hello yeni veri türü güncelleştirme
  + Değişikliği türüdür: KeyVaults tooAzureDiagnostics. Merhaba ResourceType toofilter tooKey kasası günlükleri kullanabilirsiniz.
  - Yerine: `Type=KeyVaults`, kullanın`Type=AzureDiagnostics ResourceType=VAULTS`
  + Alanlar: (alan adları büyük küçük harfe duyarlı)
  - Sonekine sahip herhangi bir alan için \_s, \_d veya \_g hello adı hello ilk karakter toolower harf durumunu değiştir
  - Sonekine sahip herhangi bir alan için \_adında, hello veri o iç içe geçmiş hello alan adlarını temel alarak tek tek alanlara bölünür. Örneğin, hello hello çağıran UPN bir alana depolanır`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - Alan değiştirilen CallerIpAddress tooCallerIPAddress
   - Alan RemoteIPCountry artık mevcut değil
4. Merhaba kaldırmak *anahtar kasası Analytics (kullanım dışı)* çözümü. PowerShell kullanıyorsanız, kullanın`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`

Merhaba değişiklik hello yeni çözümde görünür değil önce veri toplanmadı. Bu verileri kullanarak hello için eski türü ve alan adları tooquery devam edebilirsiniz.

## <a name="troubleshooting"></a>Sorun giderme
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı Azure anahtar kasası veri.
