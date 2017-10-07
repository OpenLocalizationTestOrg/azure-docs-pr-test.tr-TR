---
title: "aaaPublish WebApplicationWebSite (Windows PowerShell komut dosyası) | Microsoft Docs"
description: "Nasıl toopublish bir web projesi tooan Azure Web sitesi öğrenin. Bu komut dosyası yoksa hello gerekli kaynakları Azure aboneliğinizde oluşturur."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Yayımlama WebApplicationWebSite (Windows PowerShell komut dosyası)
## <a name="syntax"></a>Sözdizimi
Bir web projesi tooan Azure Web sitesi yayımlar. yoksa hello komut dosyası Azure aboneliğinizde hello gerekli kaynakları oluşturur.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Yapılandırma
Merhaba dağıtımın hello ayrıntılarını açıklayan hello yolu toohello JSON yapılandırma dosyası.

| Parametre | Varsayılan değer |
| --- | --- |
| Diğer adlar |Yok |
| Gerekli mi? |TRUE |
| Konumu |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

## <a name="subscriptionname"></a>varlığıyla subscriptionName
Merhaba toocreate hello Web sitesi istediğiniz Azure aboneliği Hello adı.

| Parametre | Varsayılan değer |
| --- | --- |
| Diğer adlar |Yok |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

## <a name="webdeploypackage"></a>WebDeployPackage
Merhaba yolu toohello web dağıtım paketi toopublish toohello Web sitesi. Visual Studio'da hello Web Yayımlama Sihirbazı'nı kullanarak bu paketi oluşturabilirsiniz. Daha fazla bilgi için bkz: [Azure Cloud Services ve ASP.NET kullanmaya başlama](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Parametre | Varsayılan değer |
| --- | --- |
| Diğer adlar |Yok |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
Merhaba kullanıcı adı ve parola hello Azure SQL veritabanı için.

| Parametre | Varsayılan değer |
| --- | --- |
| Diğer adlar |Yok |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
TRUE ise, yazdırma iletilerden hello betik toohello akış çıkışı.

| Parametre | Varsayılan değer |
| --- | --- |
| Diğer adlar |Yok |
| Gerekli mi? |False |
| Konumu |Adlı |
| Varsayılan değer |False |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

## <a name="remarks"></a>Açıklamalar
Nasıl toouse hello betik toocreate geliştirme ve Test ortamları için bkz. bir tam açıklama için [Windows PowerShell komut dosyalarını kullanarak tooPublish tooDev ve Test ortamları](vs-azure-tools-publishing-using-powershell-scripts.md).

Merhaba JSON yapılandırma dosyası dağıtılan toobe nedir hello ayrıntılarını belirtir. Merhaba adı ve hello Web sitesi için kullanıcı adı gibi hello proje oluşturduğunuzda, belirttiğiniz hello bilgiler içerir. Ayrıca hello veritabanı tooprovision varsa içerir. koddan hello örnek bir JSON yapılandırma dosyası gösterir:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

Ne dağıtılan hello JSON yapılandırma dosyası toochange düzenleyebilirsiniz. Bir Web Bölümü gereklidir, ancak hello veritabanı bölümü isteğe bağlıdır.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: [Yayımla-WebApplicationVM (Windows PowerShell komut dosyası)](vs-azure-tools-publish-webapplicationvm.md)

