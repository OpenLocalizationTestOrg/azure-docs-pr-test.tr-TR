---
title: "aaaAzure günlük tümleştirme SSS | Microsoft Docs"
description: "Bu makalede Azure günlük tümleştirmesi hakkında sorular yanıtlanmaktadır."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a>Azure günlük tümleştirme hakkında SSS
Bu makalede Azure günlük tümleştirmesi hakkında sık sorulan sorular (SSS) yanıtlar. 

Azure günlük tümleştirme toointegrate ham günlükleri, şirket içi güvenlik bilgileri ve Olay yönetimi (SIEM) sistemlere Azure kaynaklarınızdan kullanabilirsiniz bir Windows işletim sistemi hizmetidir. Bu tümleştirme, tüm varlıklarınızı, şirket içi veya hello bulutta birleştirilmiş bir Pano sağlar. Ardından toplama, bağıntılı, çözümleyebilir ve uygulamalarınız ile ilişkili güvenlik olayları için uyarı.

## <a name="is-hello-azure-log-integration-software-free"></a>Hello Azure günlük tümleştirme yazılım ücretsiz mi?
Evet. Hello Azure günlük tümleştirme yazılımı için ücret ödemeden yoktur.

## <a name="where-is-azure-log-integration-available"></a>Burada Azure günlük tümleştirmesi var mı?

Azure ticari ve Azure kamu şu anda kullanılabilir değil ve Çin veya Almanya kullanılabilir değil.

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>Merhaba depolama hesaplarını Azure günlük tümleştirme Azure VM günlükleri çekme nasıl görebilirim?
Merhaba komutu çalıştırmak **azlog kaynağı listesi**.

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>Hangi abonelik hello günlükleri arasındadır Azure günlük tümleştirme nasıl anlayabilirim?

Hello yerleştirilir denetim günlüklerinin hello durumda **AzureResourcemanagerJson** dizinleri hello abonelik kimliği: hello günlük dosyası adı. Bu, aynı zamanda hello günlükleri için geçerlidir **AzureSecurityCenterJson** klasör. Örneğin:

20170407T070805_2768037.0000000023. **1111e5ee-1111-111b-a11e-1e111e1111dc**.json

Azure Active Directory denetim günlüklerini hello Kiracı kimliği hello adının bir parçası olarak içerir.

Bir olay hub'ından okuma tanılama günlüklerini hello abonelik kimliği hello adının bir parçası olarak dahil etmeyin. Bunun yerine, hello kolay ad hello kaynağı oluşturma işlemi hello olay hub'ı bir parçası olarak belirtilen içerirler. 

## <a name="how-can-i-update-hello-proxy-configuration"></a>Merhaba proxy yapılandırmasını nasıl güncelleştirebilir miyim?
Proxy ayarı Azure depolama erişime doğrudan izin vermiyorsa, hello açmak **AZLOG. EXE. CONFIG** dosyasını **c:\Program Files\Microsoft Azure günlük tümleştirme**. Güncelleştirme hello dosya tooinclude hello **defaultProxy** hello proxy adresine sahip bir bölüm, kuruluşunuzun. Merhaba güncelleştirme yapıldıktan sonra durdurmak ve hello komutlarını kullanarak hello hizmeti başlatmak **net stop azlog** ve **net Başlat azlog**.

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>Windows olayları hello abonelik bilgileri nasıl görebilirim?
Merhaba abonelik kimliği toohello kolay adı hello kaynağı eklenirken ekleyin:

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
Merhaba olay XML hello abonelik kimliği gibi meta veriler, aşağıdaki hello sahiptir:

![Olay XML][1]

## <a name="error-messages"></a>Hata iletileri
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>Merhaba komutu çalıştırdığınızda ı **azlog createazureid**, aşağıdaki hata hello neden alabilirim?
Hata:

  *Toocreate AAD uygulama - Kiracı 72f988bf-86f1-41af-91ab-2d7cd011db37 - neden başarısız = 'Yasak' - ileti 'yeterli ayrıcalığa sahip toocomplete hello işlemi' =*

Merhaba **azlog createazureid** komut çalışır toocreate Azure oturum açma hello hello abonelikler için tüm hello Azure AD kiracılar bir hizmet sorumlusu erişimi vardır. Azure oturum açma bilgilerinizi yalnızca Konuk kullanıcı olarak Azure AD Kiracı ise, "yeterli ayrıcalığa sahip toocomplete hello işlemiyle." Merhaba komutu başarısız Merhaba Kiracı yönetici tooadd isteyin hesabınız hello kiracısındaki bir kullanıcı olarak.

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>Merhaba komutu çalıştırdığınızda ı **azlog yetkilendirmek**, aşağıdaki hata hello neden alabilirim?
Hata:

  *Uyarı rol ataması - AuthorizationFailed oluşturma: hello istemci janedo@microsoft.com' olan nesne kimliği 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' yetkilendirme tooperform eylemi 'Microsoft.Authorization/roleAssignments/write' kapsamı üzerinde yok ' / Abonelikleri / 70d 95299 d689 4c 97-b971-0d8ff0000000'.*

Merhaba **azlog yetkilendirmek** atar hello okuyucu toohello Azure AD hizmet sorumlusu rolü komutu (ile oluşturulan **azlog createazureid**) sağlanan toohello abonelikleri. Hello Azure oturum açma bir ortak yönetici veya hello abonelik sahibi değilse, bir "Yetkilendirme başarısız oldu" hata iletisiyle başarısız olur. Azure rol tabanlı erişim denetimi (RBAC) ortak yönetici veya sahibi gerekli toocomplete bu eylemdir.

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>Merhaba Denetim günlüğüne hello özellikleri hello tanımını nereden bulabilirim?
Bkz.:

* [Azure Resource Manager ile işlemlerini denetleme](../azure-resource-manager/resource-group-audit.md)
* [Bir abonelikte hello Azure İzleyici REST API listesi hello yönetim olayları](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>Azure Güvenlik Merkezi uyarılarını ayrıntıları nereden bulabilirim?
Bkz: [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları](../security-center/security-center-managing-and-responding-alerts.md).

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>Nasıl VM Tanılama ile toplanan değişiklik yapabilirsiniz?
Nasıl tooget, değiştirmek ve hello Azure tanılama yapılandırma hakkında ayrıntılar için bkz: [Windows çalıştıran bir sanal makinede kullan PowerShell tooenable Azure tanılama](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Aşağıdaki örnek hello hello Azure Tanılama yapılandırmasını alır:

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

Aşağıdaki örnek hello hello Azure Tanılama yapılandırmasını değiştirir. Bu yapılandırmada, yalnızca olay kimliği 4624 ve olay kimliği 4625 hello güvenlik olay günlüğü'nden toplanır. Azure olayları için Microsoft Antimalware hello sistem olay günlüğü'nden toplanır. XPath ifadeleri hello kullanımı hakkında daha fazla bilgi için bkz: [tüketen olayları](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

Merhaba aşağıdaki örnek hello Azure tanılama yapılandırması ayarlar:

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

Değişiklikleri yaptıktan sonra o hello olayları toplanan doğru hello depolama hesabı tooensure denetleyin.

Merhaba yükleme ve yapılandırma sırasında herhangi bir sorun varsa, lütfen açık bir [destek isteği](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request). Seçin **günlük tümleştirme** destek isteyen hello hizmet olarak.

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>My SIEM Azure günlük tümleştirme toointegrate Ağ İzleyicisi günlüklerini kullanabilir miyim?

Azure Ağ İzleyicisi günlük bilgileri büyük miktarlarda oluşturur. Bu günlükler gönderilen yüksetlmesi toobe tooa SIEM olup olmadığı. yalnızca desteklenen hello hedef Ağ İzleyicisi günlükleri için bir depolama hesabıdır. Bu günlükler okuma ve kullanılabilir tooa SIEM yaparak Azure günlük tümleştirme desteklemez.

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
