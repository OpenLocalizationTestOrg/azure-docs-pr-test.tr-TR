---
title: "Anahtar kasası (Klasik) azure'da Windows vm'lerinde SQL Server ile aaaIntegrate | Microsoft Docs"
description: "Nasıl tooautomate hello Azure anahtar kasası ile kullanmak için SQL Server şifreleme yapılandırma hakkında bilgi edinin. Bu konu, SQL Server sanal makinelerle toouse Azure anahtar kasası tümleştirmeyi hello Klasik dağıtım modelinde nasıl oluşturacağınızı açıklar."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>SQL Server için Azure anahtar kasası tümleştirme Azure sanal makinelerde (Klasik) yapılandırma
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Klasik](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Birden çok SQL Server şifreleme özellikleri vardır, gibi [saydam veri şifreleme (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [sütun düzeyinde şifreleme (Temizle)](https://msdn.microsoft.com/library/ms173744.aspx), ve [yedek şifreleme](https://msdn.microsoft.com/library/dn449489.aspx). Bu formlar şifreleme ve şifreleme için kullandığınız hello şifreleme anahtarlarını saklamak toomanage gerektirir. Hello Azure anahtar kasası (AKV) hizmeti tasarlanmış tooimprove hello güvenliği ve yönetimi için güvenli ve yüksek oranda kullanılabilir bir konumda Bu anahtarları ' dir. Merhaba [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) SQL Server toouse Bu anahtarları Azure anahtar Kasası'ndan sağlar.

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Şirket içi makineler ile SQL Server çalışıyorsa, vardır [şirket içi SQL Server makinenizden tooaccess Azure anahtar kasası izlemeniz adımları](https://msdn.microsoft.com/library/dn198405.aspx). Ancak Azure vm'lerinde SQL Server için hello kullanarak zaman kazanabilirsiniz *Azure anahtar kasası tümleştirmeyi* özelliği. Bu özellik ile birkaç Azure PowerShell cmdlet'leri tooenable otomatikleştirebilirsiniz yapılandırması için bir SQL VM tooaccess gerekli anahtar kasanızı hello.

Bu özellik etkinleştirildiğinde, otomatik olarak yükler hello SQL Server Bağlayıcısı, hello EKM sağlayıcısı tooaccess Azure anahtar kasası yapılandırır ve hello kimlik bilgisi tooallow oluşturur, tooaccess kasanızı. Konumundaki görünüyorsa hello hello adımlarda şirket içi belgelerine daha önce bahsedilen, bu özellik adım 2 ve 3 otomatikleştirir görebilirsiniz. toodo el ile gerekir hello yalnızca toocreate hello anahtar kasasını ve anahtarları şeydir. Buradan, hello tüm Kurulum, SQL VM otomatik hale getirilmiştir. Bu özellik, bu kurulum tamamlandıktan sonra veritabanları veya yedeklemeler normal olarak şifreleme T-SQL deyimleri toobegin yürütebilir.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>AKV tümleştirme yapılandırın
PowerShell tooconfigure Azure anahtar kasası tümleştirmeyi kullanın. Aşağıdaki bölümlerde hello hello gerekli parametreleri genel bir bakış ve örnek bir PowerShell komut dosyası sağlar.

### <a name="install-hello-sql-server-iaas-extension"></a>SQL Server Iaas uzantısı Hello yükleyin
İlk olarak, [hello SQL Server Iaas uzantısı yüklemek](../classic/sql-server-agent-extension.md).

### <a name="understand-hello-input-parameters"></a>Merhaba giriş parametreleri anlamak
Merhaba aşağıdaki tabloda listeleri hello parametreleri toorun hello PowerShell Betiği hello sonraki bölümde gereklidir.

| Parametre | Açıklama | Örnek |
| --- | --- | --- |
| **$akvURL** |**Merhaba anahtar kasası URL'si** |"https://contosokeyvault.vault.azure.net/" |
| **$spName** |**Hizmet asıl adı** |"fde2b411 - 33d 5-4e11-af04eb07b669ccf2" |
| **$spSecret** |**Hizmet asıl gizli anahtarı** |"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM =" |
| **$credName** |**Kimlik bilgisi adı**: AKV tümleştirme, SQL Server, hello VM toohave erişim toohello anahtar kasası sağlayan bir kimlik bilgisi oluşturur. Bu kimlik bilgisi için bir ad seçin. |"mycred1" |
| **$vmName** |**Sanal makine adı**: önceden oluşturulmuş bir SQL VM hello adı. |"myvmname" |
| **$serviceName** |**Hizmet adı**: hello SQL VM ile ilişkili hello bulut hizmeti adını. |"mycloudservicename" |

### <a name="enable-akv-integration-with-powershell"></a>PowerShell ile AKV tümleştirmeyi etkinleştir
Merhaba **yeni AzureVMSqlServerKeyVaultCredentialConfig** cmdlet'i hello Azure anahtar kasası tümleştirme özelliği için bir yapılandırma nesnesi oluşturur. Merhaba **kümesi AzureVMSqlServerExtension** Bu tümleştirme ile Merhaba yapılandırır **KeyVaultCredentialSettings** parametresi. adımları Göster nasıl aşağıdaki hello toouse bu komutları.

1. Azure PowerShell'de ilk hello giriş parametreleri belirli değerlerinizle, bu konunun hello önceki bölümlerde açıklandığı gibi yapılandırın. komut dosyası izleyen hello bir örnektir.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. Ardından kullanım hello aşağıdaki tooconfigure komut dosyası ve AKV tümleştirme etkinleştirin.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Merhaba SQL Iaas Aracısı uzantısı hello SQL VM yeni bu yapılandırmasıyla güncelleştirir.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

