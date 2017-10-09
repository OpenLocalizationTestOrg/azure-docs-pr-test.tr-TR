---
title: aaaPublish WebApplicationVM | Microsoft Docs
description: "Bilgi nasıl toodeploy bir web uygulaması tooa sanal makine. Bu komut dosyası yoksa hello gerekli kaynakları Azure aboneliğinizde oluşturur."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Yayımlama WebApplicationVM (Windows PowerShell komut dosyası)
Bir web uygulaması tooa sanal makine dağıtır. yoksa hello komut dosyası Azure aboneliğinizde hello gerekli kaynakları oluşturur.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Yapılandırma
Merhaba dağıtımın hello ayrıntılarını açıklayan hello yolu toohello JSON yapılandırma dosyası.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konumu |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

### <a name="subscriptionname"></a>varlığıyla subscriptionName
Merhaba adını hello toocreate hello sanal makine istediğiniz Azure aboneliği.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |Merhaba ilk abonelik hello abonelik dosyasındaki kullanır |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

### <a name="webdeploypackage"></a>WebDeployPackage
Merhaba yolu toohello web dağıtım paketi toopublish toohello sanal makine. Visual Studio'da hello Web Yayımlama Sihirbazı'nı kullanarak bu paketi oluşturabilirsiniz. Bkz: [nasıl yapılır: Visual Studio'da bir Web dağıtım paketi oluşturma](https://msdn.microsoft.com/library/dd465323.aspx).

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

### <a name="allowuntrusted"></a>AllowUntrusted
TRUE ise, bir güvenilen kök yetkilisi tarafından imzalanmadığını sertifikaları hello kullanılmasına izin verin.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |False |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

### <a name="vmpassword"></a>VMPassword
Hello hello sanal makine hesabı için kimlik bilgileri. Örnek: - VMPassword @{Name = "Yönetici"; Parola = "parola"}

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
Azure SQL veritabanı hello Hello kimlik bilgileri. Örnek: - DatabaseServerPassword @{Name = "Yönetici"; Parola = "parola"}

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
TRUE ise, yazdırma iletilerden hello betik toohello akış çıkışı.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |False |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

## <a name="remarks"></a>Açıklamalar
Nasıl toouse hello betik toocreate geliştirme ve Test ortamları için bkz. bir tam açıklama için [Windows PowerShell komut dosyalarını kullanarak tooPublish tooDev ve Test ortamları](vs-azure-tools-publishing-using-powershell-scripts.md).

Merhaba JSON yapılandırma dosyası dağıtılan toobe nedir hello ayrıntılarını belirtir. Merhaba adı, benzeşim grubu, VHD görüntüsü ve hello sanal makinesinin boyutu gibi hello proje oluşturduğunuzda, belirttiğiniz hello bilgiler içerir. Ayrıca hello sanal makinedeki hello veritabanları tooprovision hello uç noktaları varsa ve dağıtım parametreleri web. koddan hello örnek bir JSON yapılandırma dosyası gösterir:

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Merhaba JSON yapılandırma dosyası toochange ne sağlandığında düzenleyebilirsiniz. Bir sanal makine ve bulut hizmeti gerekiyor, ancak hello veritabanı bölümü isteğe bağlıdır.

