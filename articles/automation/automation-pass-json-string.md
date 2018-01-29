---
title: "Bir Azure Otomasyonu runbook'u bir JSON nesnesi geçirmek | Microsoft Docs"
description: "Nasıl bir JSON nesnesi olarak runbook parametreleri geçirme"
services: automation
documentationcenter: dev-center-name
author: georgewallace
manager: carmonm
keywords: PowerShell runbook, json, azure Otomasyonu
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: gwallace
ms.openlocfilehash: 5390ba34a25713aed84d6e778335e30f27c2b1f8
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a>Bir Azure Otomasyonu runbook'u bir JSON nesnesi geçirin

Bir runbook'ta bir JSON dosyası geçirmek istediğiniz verileri depolamak yararlı olabilir.
Örneğin, tüm bir runbook'a geçirmek için istediğiniz parametreleri içeren bir JSON dosyası oluşturabilirsiniz.
Bunu yapmak için JSON bir dizeye dönüştürmek ve içeriğini runbook'a geçirmeden önce bu dize bir PowerShell nesnesine dönüştürmek sahip.

Bu örnekte, çağıran bir PowerShell komut dosyası oluşturacağız [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) runbook'a JSON içeriği geçirme bir PowerShell runbook'u başlatın.
PowerShell runbook geçirildi JSON öğesinden VM için parametreler alınırken bir Azure VM başlatır.

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:

* Azure aboneliği. Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).
* Runbook’u tutacak ve Azure kaynaklarında kimlik doğrulamasını yapacak bir [Automation hesabı](automation-sec-configure-azure-runas-account.md).  Bu hesabın sanal makineyi başlatma ve durdurma izni olmalıdır.
* Azure sanal makinesi. Bu makineyi durdurup başlatacağımız için makinenin üretime yönelik bir VM olmaması gerekir.
* Azure Powershell yerel makine üzerinde yüklü. Bkz: [yükleyin ve Azure Powershell yapılandırma](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) Azure PowerShell alma hakkında bilgi için.

## <a name="create-the-json-file"></a>JSON dosyası oluşturun

Bir metin dosyasına aşağıdaki sınama yazın ve kaydedileceği `test.json` yerel bilgisayarınızdaki herhangi bir yerde.

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a>Runbook oluşturma

"Test-Json" Azure Automation adlı yeni bir PowerShell runbook oluşturun.
Yeni bir PowerShell runbook oluşturulacağını öğrenmek için bkz: [ilk PowerShell runbook'um](automation-first-runbook-textual-powershell.md).

JSON verileri kabul etmek için runbook giriş parametresi olarak bir nesne almanız gerekir.

Runbook ardından JSON içinde tanımlanan özellikleri kullanabilirsiniz.

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 Kaydedin ve bu runbook Otomasyon hesabınızda yayımlayın.

## <a name="call-the-runbook-from-powershell"></a>Runbook Powershell'den çağırın

Artık Azure PowerShell kullanarak yerel makineden runbook çağırabilirsiniz.
Aşağıdaki PowerShell komutlarını çalıştırın:

1. Azure'da oturum açın:
   ```powershell
   Login-AzureRmAccount
   ```
    Azure kimlik bilgilerinizi girmeniz istenir.
1. JSON dosyasının içeriğini almak ve bir dizeye dönüştürün:
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`JSON dosyasının kaydedildiği yoludur.
1. Dize içeriği Dönüştür `$json` bir PowerShell nesnesi için:
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. Parametre için bir karma tablosu oluşturma `Start-AzureRmAutomationRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   Değerini ayarlama fark `Parameters` JSON dosyası değerleri içeren PowerShell nesnesi için. 
1. Runbook'u Başlat
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

Runbook VM başlatmak için JSON dosyasından değerleri kullanır.

## <a name="next-steps"></a>Sonraki adımlar

* Bir metin düzenleyicisiyle PowerShell ve PowerShell iş akışı runbook'ları düzenleme hakkında daha fazla bilgi için bkz: [Azure Otomasyonu'nda metinsel runbook'lar düzenleme](automation-edit-textual-runbook.md) 
* Daha fazla hakkında oluşturma ve runbook'ları içeri aktarma bilgi edinmek için [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md)


