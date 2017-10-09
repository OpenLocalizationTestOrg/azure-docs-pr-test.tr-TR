---
title: aaaConnect tooAzure Analysis Services | Microsoft Docs
description: "Nasıl tooconnect tooand veri alma Azure Analysis Services sunucusundan öğrenin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a>Tooan Azure Analysis Services sunucusuna bağlan

Bu makalede, veri modellemesi ve SQL Server Management Studio (SSMS) veya SQL Server veri Araçları (SSDT) gibi yönetim uygulamaları kullanarak bağlanan tooa sunucu açıklanmaktadır. Veya Microsoft Excel, Power BI Desktop veya özel uygulamalar gibi uygulamalar istemcisiyle raporlama. Bağlantıları tooAzure Analysis Services HTTPS kullanın.

## <a name="client-libraries"></a>İstemci kitaplıkları
[Merhaba son istemci kitaplıkları Al](analysis-services-data-providers.md)

Türü, bağımsız olarak tüm bağlantılar tooa server güncelleştirilmiş AMO, ADOMD.NET ve OLEDB istemci kitaplıkları tooconnect tooand arabirimi ile bir Analysis Services sunucusu gerektirir. SSMS, SSDT, Excel 2016 ve Power BI için hello son istemci kitaplıkları yüklü veya aylık sürümleriyle güncelleştirilir. Ancak, bazı durumlarda, bir uygulama hello son olmayabilir mümkündür. Örneğin, ne zaman ilkeleri gecikme güncelleştirir veya Office 365 güncelleştirmelerini ertelenmiş kanal hello üzerinde markalarıdır.

## <a name="server-name"></a>Sunucu adı

Azure'da bir Analysis Services sunucusu oluşturduğunuzda, hello sunucunun oluşturulan toobe olduğu bir benzersiz ad ve hello bölge belirtin. Bir bağlantı Hello sunucu adı belirtme hello sunucu adlandırma şeması olur:

```
<protocol>://<region>/<servername>
```
 Dize olduğu Protokolü **asazure**, bölgedir hello hello sunucu oluşturulduğu URI (örneğin, westus.asazure.windows.net) ve servername hello bölge içinde benzersiz sunucunuzun hello adı.

### <a name="get-hello-server-name"></a>Merhaba sunucu adını Al
İçinde **Azure portal** > server > **genel bakış** > **sunucu adı**, kopya hello tüm sunucu adı. Kuruluşunuzda bulunan diğer kullanıcıların toothis sunucu çok bağlanıyorsanız, bu sunucu adı onlarla paylaşabilirsiniz. Bir sunucu adı belirtirken, yolun tamamını hello kullanılması gerekir.

![Azure'da sunucu adını alma](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Bağlantı dizesi

TooAzure bağlanırken kullanarak Analysis Services tablo nesne modeli, bağlantı dizesi biçimleri aşağıdaki kullanım hello hello:

###### <a name="integrated-azure-active-directory-authentication"></a>Tümleşik Azure Active Directory kimlik doğrulaması
Tümleşik kimlik doğrulaması hello Azure Active Directory kimlik bilgisi önbellek varsa seçer. Aksi durumda, hello Azure oturum açma penceresi gösterilir.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Kullanıcı adı ve parola ile Azure Active Directory kimlik doğrulaması

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Windows kimlik doğrulaması (tümleşik güvenliği)
Merhaba geçerli işlem çalışan hello Windows hesabını kullanın.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Bir .odc dosyası kullanarak bağlan
Excel'in eski sürümleriyle, kullanıcıların bir Office veri bağlantısı (.odc) dosyası kullanarak tooan Azure Analysis Services sunucusuna bağlanabilir. toolearn daha, fazla [bir Office veri bağlantısı (.odc) dosyası oluşturun](analysis-services-odc.md).


## <a name="next-steps"></a>Sonraki adımlar
[Excel ile bağlanma](analysis-services-connect-excel.md)    
[Power BI ile bağlanma](analysis-services-connect-pbi.md)   
[Sunucunuzu Yönetin](analysis-services-manage.md)   

