---
title: "işlem düğümleri aaaManage HPC Pack kümesi | Microsoft Docs"
description: "PowerShell komut dosyası araçları tooadd, Kaldır, başlangıç hakkında bilgi edinin ve HPC Pack 2012 R2 küme işlem düğümlerine Azure Durdur"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Merhaba numarası ve Azure HPC Pack kümede işlem düğümlerine kullanılabilirliğini yönetme
Azure Vm'lerinde bir HPC Pack 2012 R2 kümesi oluşturduysanız, küme düğümü Vm'lerde tooeasily ekleyin, kaldırın, (sağlayamaz) Başlat veya (deprovision) bazı Durdur yolları işlem isteyebilirsiniz. Bu görevleri toodo hello baş düğümünde VM yüklü olan Azure PowerShell komut dosyalarını çalıştır. Bu maliyetleri denetimi hello numarası ve HPC paketi küme kaynaklarınızın kullanılabilirliğini denetlemenize yardımcı olur komutlar.

> [!IMPORTANT] 
> Bu makale yalnızca tooHPC Pack 2012 R2 kümeleri hello Klasik dağıtım modeli kullanılarak oluşturulmuş Azure içinde geçerlidir. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.
> Ayrıca, bu makalede açıklanan hello PowerShell betikleri HPC Pack 2016'da kullanılabilir değildir.

## <a name="prerequisites"></a>Ön koşullar
* **Azure VM'de HPC Pack 2012 R2 küme**: hello Klasik dağıtım modelinde bir HPC Pack 2012 R2 kümesi oluşturun. Örneğin, hello dağıtım hello Azure Marketi hello HPC Pack 2012 R2 VM görüntüsünde ve bir Azure PowerShell komut dosyası kullanarak otomatikleştirebilirsiniz. Bilgi ve Önkoşullar için bkz: [hello HPC Pack Iaas dağıtım betiği ile bir HPC kümesi oluşturma](hpcpack-cluster-powershell-script.md).
  
    Dağıtımdan sonra hello düğümü yönetim komut dosyaları hello % CCP bulur\_giriş % bin klasörü hello baş düğüm üzerinde. Her hello komut dosyalarının, yönetici olarak çalıştırın.
* **Azure yayımlama ayarları dosyası veya yönetim sertifikası**: toodo hello aşağıdakilerden birini hello baş düğümünde gerekir:
  
  * **İçeri aktarma hello Azure yayımlama ayarları dosyası**. toodo hello baş düğümünde Azure PowerShell cmdlet'lerini aşağıdaki Bu, çalışma hello:
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **Merhaba baş düğümünde Hello Azure yönetim sertifikası yapılandırma**. Merhaba .cer dosyanız varsa, hello CurrentUser\My sertifika deposuna içeri aktarın ve ardından Azure ortamınıza (AzureCloud veya AzureChinaCloud) için Azure PowerShell cmdlet'i aşağıdaki hello çalıştırın:
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>İşlem düğümü sanal makineleri ekleyin
İşlem düğümleri hello ile ekleme **Ekle HpcIaaSNode.ps1** komut dosyası.

### <a name="syntax"></a>Sözdizimi
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>Parametreler
* **ServiceName**: yeni düğümü VM'ler işlem hello bulut hizmeti adını eklenir.
* **Görüntü adı**: hello Azure Klasik portalında veya Azure PowerShell cmdlet'i aracılığıyla alınabilir Azure VM görüntü adı **Get-AzureVMImage**. Hello görüntü hello aşağıdaki gereksinimleri karşılamalıdır:
  
  1. Bir Windows işletim sistemi yüklenmelidir.
  2. HPC Pack Merhaba bilgi işlem düğümü rolü yüklü olmalıdır.
  3. Merhaba görüntü hello kullanıcı kategorisi, ortak bir Azure VM görüntüsü değil, özel bir görüntü olması gerekir.
* **Miktar**: işlem düğümü VM'ler toobe eklenen sayısı.
* **InstanceSize**: hello boyutunu işlem düğümü VM'ler.
* **DomainUserName**: kullanılan toojoin hello yeni VM'ler toohello etki alanında etki alanı kullanıcı adı.
* **DomainUserPassword**: hello etki alanı kullanıcı parolası.
* **NodeNameSeries** (isteğe bağlı): deseni Merhaba işlem düğümleri adlandırma. Merhaba biçiminde olmalıdır &lt; *kök\_adı*&gt;&lt;*Başlat\_numarası*&gt;%. Örneğin, MyCN11 başlangıç düğümü adlarını MyCN % %10 anlamına gelir hello bir dizi işlem. Belirtilmezse, hello komut dosyası kullanan hello düğümü adlandırma serisi hello HPC kümede yapılandırılmış.

### <a name="example"></a>Örnek
Merhaba aşağıdaki örnek 20 boyutu büyük işlem düğümü VM'ler hello bulut hizmetinde, *hpcservice1*bağlı hello VM görüntüsü olarak *hpccnimage1*.

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>İşlem düğümü VM'ler Kaldır
İşlem düğümleri hello ile Kaldır **Kaldır HpcIaaSNode.ps1** komut dosyası.

### <a name="syntax"></a>Sözdizimi
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>Parametreler
* **Ad**: küme düğümleri toobe adlarını kaldırıldı. Joker karakterleri desteklenir. Merhaba parametre kümesi adı adıdır. Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.
* **Düğüm**: hello HPC PowerShell cmdlet'i alınabilir hello HpcNode nesne kaldırılmış hello düğümleri toobe için [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). Merhaba parametre kümesi adı düğümdür. Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.
* **DeleteVHD** (isteğe bağlı): toodelete ilişkili hello diskler hello kaldırılır VM'ler için ayarlama.
* **Zorla** (isteğe bağlı): kaldırmadan önce çevrimdışı HPC düğümleri tooforce ayarlama.
* **Onayla** (isteğe bağlı): hello komutu çalıştırmadan önce onaylamanız için komut istemi.
* **WhatIf**: toodescribe ne ayarı durum hello komutu çalıştırmadan hello komut yürütülürse.

### <a name="example"></a>Örnek
Merhaba aşağıdaki örnek çevrimdışı hello düğümleri başlayan adlarla zorlar *HPCNode-CN -* hello düğümler ve bunların ilişkili diskler kaldırır.

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>İşlem düğümü sanal makineleri Başlat
Başlangıç işlem düğümlerini hello ile **başlangıç HpcIaaSNode.ps1** komut dosyası.

### <a name="syntax"></a>Sözdizimi
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>Parametreler
* **Ad**: hello küme düğümleri toobe adlarını başlatıldı. Joker karakterleri desteklenir. Merhaba parametre kümesi adı adıdır. Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.
* **Düğüm**-hello HPC PowerShell cmdlet'i alınabilir hello HpcNode nesne hello düğümleri toobe başlamak için [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). Merhaba parametre kümesi adı düğümdür. Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.

### <a name="example"></a>Örnek
Merhaba aşağıdaki örnek düğümleri başlayan adlarla başlatır *HPCNode-CN -*.

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>İşlem düğümü VM'ler Durdur
İşlem düğümleri hello ile Durdur **Stop-HpcIaaSNode.ps1** komut dosyası.

### <a name="syntax"></a>Sözdizimi
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>Parametreler
* **Ad**-hello küme düğümleri toobe adlarını durduruldu. Joker karakterleri desteklenir. Merhaba parametre kümesi adı adıdır. Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.
* **Düğüm**: hello HPC PowerShell cmdlet'i alınabilir hello HpcNode nesne durduruldu, hello düğümleri toobe için [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). Merhaba parametre kümesi adı düğümdür. Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.
* **Zorla** (isteğe bağlı): durdurmadan önce çevrimdışı HPC düğümleri tooforce ayarlama.

### <a name="example"></a>Örnek
Merhaba aşağıdaki örnek çevrimdışı düğümleri başlayan adlarla zorlar *HPCNode-CN -* ve ardından düğümler durakları hello.

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>Sonraki adımlar
* tooautomatically arttıkça ya da küçültmek hello küme düğümleri, işler ve görevleri hello kümede hello geçerli iş yükü göre bkz: [otomatik olarak Büyüt ve Küçült Azure according toohello küme iş yükühelloHPCpaketikümekaynaklarında](hpcpack-cluster-node-autogrowshrink.md).

