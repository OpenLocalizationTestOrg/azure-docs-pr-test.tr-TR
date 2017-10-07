---
title: aaaPass bir JSON nesnesi tooan Azure Otomasyonu runbook | Microsoft Docs
description: "Nasıl bir JSON nesnesi olarak toopass parametreleri tooa runbook"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: PowerShell runbook, json, azure Otomasyonu
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a>Bir JSON nesnesi tooan Azure Otomasyon runbook'u geçirin

Bir JSON dosyası toopass tooa runbook'ta istediğiniz yararlı toostore verileri olabilir.
Örneğin, tüm başlangıç parametreleri içeren bir JSON dosyası oluşturabilirsiniz toopass tooa runbook istiyor.
toodo bunu tooconvert hello JSON tooa dizesine sahip ve ardından, içeriği toohello runbook geçirmeden önce hello dize tooa PowerShell nesnesi dönüştürün.

Bu örnekte, çağıran bir PowerShell komut dosyası oluşturacağız [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart hello JSON toohello runbook Merhaba içeriğine geçirme bir PowerShell runbook.
Merhaba PowerShell runbook hello geçirildi JSON öğesinden Merhaba VM hello parametreler alınırken bir Azure VM başlatır.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Azure aboneliği. Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).
* [Otomasyon hesabı](automation-sec-configure-azure-runas-account.md) toohold runbook hello ve tooAzure kaynakları kimlik doğrulaması.  Bu hesap, izin toostart sahip ve hello sanal makineyi durdurun.
* Azure sanal makinesi. Bu makineyi durdurup başlatacağımız için makinenin üretime yönelik bir VM olmaması gerekir.
* Azure Powershell yerel makine üzerinde yüklü. Bkz [yükleyin ve Azure Powershell yapılandırma](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) hakkında bilgi için Azure PowerShell tooget.

## <a name="create-hello-json-file"></a>Merhaba JSON dosyası oluşturun

Türü hello aşağıdakileri bir metin dosyasına test ve olarak kaydedin `test.json` yerel bilgisayarınızdaki herhangi bir yerde.

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a>Merhaba runbook oluşturma

"Test-Json" Azure Automation adlı yeni bir PowerShell runbook oluşturun.
toocreate yeni bir PowerShell runbook nasıl görürüm toolearn [ilk PowerShell runbook'um](automation-first-runbook-textual-powershell.md).

tooaccept hello JSON verilerini hello runbook giriş parametresi olarak bir nesne almanız gerekir.

Merhaba runbook sonra hello JSON tanımlanan hello özelliklerini kullanabilirsiniz.

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 Kaydedin ve bu runbook Otomasyon hesabınızda yayımlayın.

## <a name="call-hello-runbook-from-powershell"></a>PowerShell hello runbook'tan çağrı

Artık Azure PowerShell kullanarak yerel makinenizden hello runbook çağırabilirsiniz.
Merhaba aşağıdaki PowerShell komutlarını çalıştırın:

1. İçinde tooAzure oturum:
   ```powershell
   Login-AzureRmAccount
   ```
    Azure kimlik bilgileriniz istendiğinde tooenter şunlardır.
1. Merhaba hello JSON dosyasının içeriğini alın ve tooa dize Dönüştür:
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`Merhaba JSON dosyasını kaydettiğiniz hello yolu değil.
1. Merhaba dize içeriğini Dönüştür `$json` tooa PowerShell nesnesi:
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. Merhaba parametreleri için bir karma tablosu oluşturma `Start-AzureRmAutomstionRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   Merhaba değerini ayarlama fark `Parameters` hello JSON dosyası hello değerleri içeren toohello PowerShell nesnesi. 
1. Merhaba runbook başlatın
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

Merhaba runbook hello JSON dosyasını toostart VM hello değerleri kullanır.

## <a name="next-steps"></a>Sonraki adımlar

* bir metin düzenleyicisiyle PowerShell ve PowerShell iş akışı runbook'ları düzenleme hakkında daha fazla toolearn bakın [Azure Otomasyonu'nda metinsel runbook'lar düzenleme](automation-edit-textual-runbook.md) 
* oluşturma ve runbook'ları, içeri aktarma hakkında daha fazla toolearn bakın [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md)


