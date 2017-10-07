---
title: "aaaEnable PowerShell kullanarak Azure Cloud Services rolünde için Uzak Masaüstü Bağlantısı"
description: "Nasıl tooconfigure azure bulut hizmeti uygulaması PowerShell tooallow Uzak Masaüstü bağlantıları kullanma"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>PowerShell kullanarak Azure Cloud Services rolünde için Uzak Masaüstü Bağlantısı etkinleştir
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Klasik Azure Portalı](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Uzak Masaüstü tooaccess hello Masaüstü Azure'da çalışan bir rolün sağlar. Çalışırken uygulamanız ile sorunları tanılamak ve Uzak Masaüstü Bağlantısı tootroubleshoot kullanın.

Bu makalede nasıl tooenable Uzak Masaüstü'nü PowerShell kullanarak, bulut hizmeti rollerinizi. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) için bu makalede gerekli hello Önkoşullar için. Merhaba uygulama dağıtıldıktan sonra Uzak Masaüstü'nü etkinleştirmek için PowerShell hello Uzak Masaüstü uzantısı kullanır.

## <a name="configure-remote-desktop-from-powershell"></a>Uzak Masaüstü PowerShell üzerinden yapılandırmak
Merhaba [kümesi AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet'i belirtilen roller veya Bulut hizmeti dağıtımınızın tüm roller üzerinde Uzak Masaüstü tooenable sağlar. Merhaba cmdlet hello Uzak Masaüstü kullanıcı hello aracılığıyla hello kullanıcı adı ve parola belirtmenize olanak sağlar *kimlik bilgisi* bir PSCredential nesnesi kabul parametresi.

PowerShell etkileşimli olarak kullanıyorsanız, hello PSCredential nesnesinin arama hello tarafından kolayca ayarlayabilirsiniz [Get-kimlik bilgilerinin](https://technet.microsoft.com/library/hh849815.aspx) cmdlet'i.

```
$remoteusercredentials = Get-Credential
```

Bu komut, tooenter hello kullanıcı adı ve parola hello uzak kullanıcı için güvenli bir şekilde sağlayan bir iletişim kutusu görüntüler.

PowerShell Otomasyon senaryolarda yardımcı olduğundan, hello de ayarlayabilirsiniz **PSCredential** , kullanıcı etkileşimi gerektirmeyen şekilde nesnesi. İlk olarak, tooset güvenli bir parola gerekir. Düz metinli bir parola tooa güvenli dize dönüştürür belirterek başlamadan kullanarak [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx). Sonraki tooconvert güvenli Bu dize bir şifrelenmiş standart dize kullanarak gereksinim duyduğunuz [ConvertFrom SecureString](https://technet.microsoft.com/library/hh849814.aspx). Bu şifreli standart dize tooa dosyasını kullanarak kaydedebilirsiniz [kümesi içeriği](https://technet.microsoft.com/library/ee176959.aspx).

Böylece her zaman hello Parolada tootype yok güvenli parola dosyası da oluşturabilirsiniz. Ayrıca, güvenli parola dosyasına düz metin dosyasından daha iyidir. PowerShell toocreate güvenli parola dosyasına aşağıdaki hello kullan:

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> Merhaba parolayı ayarlarken hello karşıladığından emin olun [karmaşıklık gereksinimlerini](https://technet.microsoft.com/library/cc786468.aspx).
>
>

toocreate hello kimlik bilgisi nesnesinin hello güvenli parola dosyasından gerekir hello dosya içeriklerini okuma ve bunları dönüştürmeniz geri tooa güvenli bir dize kullanarak [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).

Merhaba [kümesi AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet'ini de kabul eder bir *sona erme* belirten parametresi bir **DateTime** hello kullanıcı hesabının süresi dolar. Örneğin, birkaç gün hello hesap tooexpire geçerli tarih ve saat hello ayarlayabilirsiniz.

Bu PowerShell örnek nasıl tooset hello Uzak Masaüstü uzantısı'nda bir bulut hizmeti gösterir:

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
Merhaba dağıtım yuvası ve tooenable Uzak Masaüstü'nü istediğiniz rolleri Ayrıca isteğe bağlı olarak belirtebilirsiniz. Bu parametre belirtilmezse, Uzak Masaüstü'nü hello tüm rollerde hello cmdlet sağlar **üretim** dağıtım yuvası.

Uzak Masaüstü uzantısı Hello dağıtımı ile ilişkilidir. Merhaba hizmeti için yeni bir dağıtım oluşturursanız, bu dağıtım üzerinde tooenable Uzak Masaüstü sahip. Ardından, her zaman etkin toohave Uzak Masaüstü istiyorsanız, dağıtım iş akışınıza hello PowerShell betikleri tümleştirme düşünmelisiniz.

## <a name="remote-desktop-into-a-role-instance"></a>Rol örneği içine Uzak Masaüstü
Merhaba [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet'tir kullanılan tooremote Desktop'a bulut hizmetinizin belirli rol örneği. Merhaba kullanabilirsiniz *LocalPath* parametresi toodownload hello RDP dosyasını yerel olarak. Veya hello kullanabilirsiniz *başlatma* parametresi toodirectly başlatma hello Uzak Masaüstü Bağlantısı iletişim tooaccess hello bulut hizmet rolü örneği.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>Uzak Masaüstü uzantısı'nda bir hizmeti etkin olup olmadığını denetleyin
Merhaba [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet görüntüler Uzak Masaüstü etkin veya bir hizmet dağıtımı için devre dışı. Merhaba cmdlet hello Uzak Masaüstü kullanıcı ve hello Uzak Masaüstü uzantısı için etkin hello rolleri için hello kullanıcı adını döndürür. Varsayılan olarak, bu hello dağıtım yuvasına gerçekleşir ve bunun yerine hazırlık yuvasındaki toouse hello seçebilirsiniz.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>Uzak Masaüstü uzantısı bir hizmetten kaldırın
Merhaba Uzak Masaüstü uzantısı bir dağıtımda zaten etkinleştirdiyseniz ve uzak masaüstü ayarlarını tooupdate hello, ilk hello uzantısını kaldırın. Ve hello yeni ayarlarla yeniden etkinleştirin. Örneğin, tooset istiyorsanız hello uzak kullanıcı hesabı veya hello hesabı için yeni bir parola süresi. Bunun yapılması hello Uzak Masaüstü uzantısı etkin olan mevcut dağıtımlarında gereklidir. Yeni dağıtımlar için yalnızca hello uzantısı doğrudan uygulayabilirsiniz.

tooremove hello Uzak Masaüstü uzantısı hello dağıtımından, kullanabileceğiniz hello [Kaldır AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet'i. Ayrıca isteğe bağlı olarak, hello dağıtım yuvası ve tooremove hello Uzak Masaüstü uzantısı istediğiniz rolü de belirtebilirsiniz.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> toocompletely Kaldır hello uzantı yapılandırması hello çağrı *kaldırmak* hello cmdlet'iyle **UninstallConfiguration** parametresi.
>
> Merhaba **UninstallConfiguration** parametresi kaldırır herhangi bir uzantı yapılandırma diğer bir deyişle uygulanan toohello hizmet. Merhaba hizmet yapılandırmasıyla ilişkili her uzantı yapılandırmadır. Arama hello *kaldırmak* cmdlet olmadan **UninstallConfiguration** hello keser <mark>dağıtım</mark> hello uzantısı yapılandırmasından nedenle etkili bir şekilde kaldırılıyor Merhaba uzantısı. Ancak, hello uzantı yapılandırması hello hizmeti ile ilişkili olarak kalır.
>
>

## <a name="additional-resources"></a>Ek kaynaklar

[Nasıl tooConfigure bulut Hizmetleri](cloud-services-how-to-configure.md)
[bulut SSS - Uzak Masaüstü Hizmetleri](cloud-services-faq.md)
