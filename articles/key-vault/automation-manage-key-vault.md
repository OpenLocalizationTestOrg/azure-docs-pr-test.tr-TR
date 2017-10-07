---
title: "Azure otomasyonu kullanarak Azure anahtar kasası aaaManage | Microsoft Docs"
description: "Kullanılan toomanage Azure anahtar Kasası'hello Azure Otomasyon hizmetine nasıl olabilir hakkında bilgi edinin."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>Azure anahtar Kasası'nın Azure otomasyonu kullanarak yönetme
Bu kılavuz toohello Azure Otomasyon hizmetine ve anahtarları ve gizli anahtarları Azure anahtar Kasası'nda kullanılan toosimplify yönetimini nasıl çalıştırılabilir tanıtılacaktır.

## <a name="what-is-azure-automation"></a>Azure Otomasyonu Nedir?
[Azure Otomasyonu](../automation/automation-intro.md) işlem Otomasyonu ve istenen durum yapılandırması aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir. Azure otomasyonu kullanarak, el ile yinelenen, uzun süre çalışan ve hataya yatkın görevleri otomatik tooincrease güvenilirlik, verimliliği ve kuruluşunuz için zaman toovalue olabilir.

Azure Otomasyon gereksinimlerinizi toomeet ölçeklendirir bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar. Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.

İşlem yükünü azaltmak ve boş BT ve DevOps personel toofocus iş değeri, bulut yönetim görevleri toobe taşıyarak ekler iş Azure Automation'ın otomatik olarak çalıştırın.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>Azure Otomasyonu Azure anahtar kasası yönetmenize nasıl yardımcı olabilir?
Anahtar kasası yönetilebilir Azure Otomasyonu'nda hello kullanarak [AzureRM anahtar kasası cmdlet'leri](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) ve [Azure Klasik anahtar kasası cmdlet'leri](https://msdn.microsoft.com/library/azure/dn868052.aspx). otomatik olarak Azure Otomasyonu'nda Klasik anahtar kasası yönetme kullanılabilir için Azure modülü hello ve hello içeri aktarabilirsiniz [AzureRM KeyVault Modülü](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) içine Azure Otomasyonu, böylece anahtar kasası yönetimini çoğunu gerçekleştirebilirsiniz Görevler hello hizmet içinde. Azure Automation bu cmdlet'leri diğer Azure Hizmetleri, tooautomate karmaşık görevleri için hello cmdlet'leri ile Azure hizmeti ve 3. taraf sistemi arasında eşleştirin.

Hello Azure anahtar kasası cmdlet'leri ile diğerlerinin yanı sıra bu görevleri gerçekleştirebilirsiniz: 

* Oluşturma ve bir anahtar kasası yapılandırma
* Oluşturun veya bir anahtarı içeri aktarın
* Bir parolayı güncelle
* Bir anahtarı güncelleştirme öznitelikleri
* Bir anahtar veya gizli Al
* Bir anahtar veya gizli Sil

PowerShell toomanage anahtar kasası kullanmanın bazı örnekler şunlardır:  

* [Azure anahtar kasası - adım adım](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Ayarlama ve Azure anahtar kasası yapılandırma](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>Sonraki adımlar
Artık Azure Automation ve nasıl kullanılan toomanage Azure anahtar kasası olabilir hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn Azure Otomasyonu hakkında daha fazla izleyin.

* Hello Azure Otomasyonu bkz [başlangıç Öğreticisi](../automation/automation-first-runbook-graphical.md).
* Merhaba bkz [Azure anahtar kasası PowerShell komut dosyalarını](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).

