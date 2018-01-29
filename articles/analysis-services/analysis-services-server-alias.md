---
title: "Azure Analysis Services diğer ad sunucusu adlarını | Microsoft Docs"
description: "Oluşturun ve sunucu adları kullanın açıklar."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: kfile
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2017
ms.author: owend
ms.openlocfilehash: a947dde1551c653faa54f088c1712c41c7657aa0
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="alias-server-names"></a>Diğer sunucu adları

Bir sunucu diğer adı kullanarak, Azure Analysis Services sunucunuzla daha kısa bir kullanıcı bağlanabilir *diğer* sunucu adı yerine. Bir istemci uygulamadan bağlanırken diğer adı kullanarak uç noktası olarak belirtilen **bağlantı: / /** Protokolü biçimi. Uç nokta ardından bağlanmak için gerçek sunucu adını döndürür.

Diğer sunucu adları için iyi şunlardır:

- Kullanıcıları etkilemeden sunucular arasında geçirme modeller. 
- Kolay sunucu adlarını unutmayın kullanıcılar için daha kolay. 
- Günün farklı zamanlarda farklı sunuculara doğrudan kullanıcılara. 
- Doğrudan kullanıcılar de farklı bölgelerdeki Azure trafik Yöneticisi kullanırken gibi coğrafi olarak yakın, örnekleri. 

Geçerli bir Azure Analysis Services server adı döndürür herhangi bir HTTP uç nokta bir diğer ad olarak hizmet verebilir.

![Bağlantı biçimi kullanarak diğer adı](media/analysis-services-alias/aas-alias-browser.png)

Bir istemciden bağlanırken, diğer sunucu adı kullanılarak girilir **bağlantı: / /** Protokolü biçimi. Örneğin, Power BI Desktop'ta:

![Power BI Desktop bağlantı](media/analysis-services-alias/aas-alias-connect-pbid.png)

## <a name="create-an-alias"></a>Diğer ad oluşturma

Bir diğer uç nokta oluşturmak için geçerli bir Azure Analysis Services server adı döndürür herhangi bir yöntemi kullanabilirsiniz. Örneğin, Azure Blob Storage'nın gerçek sunucu içeren bir dosyada başvuru adı, veya oluşturun ve ASP.NET Web Forms uygulama yayımlama.

Bu örnekte, bir ASP.NET Web Forms uygulamasını Visual Studio'da oluşturulur. Ana Sayfa başvurusu ve kullanıcı denetimini Default.aspx sayfasından kaldırılır. Default.aspx içeriğini yalnızca aşağıdaki sayfa yönergesi şunlardır:

```
<%@ Page Title="Home Page" Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="FriendlyRedirect._Default" %>
```

Default.aspx.cs Page_Load olayında Azure Analysis Services sunucu adını döndürmek için Response.Write() yöntemini kullanır.

```
protected void Page_Load(object sender, EventArgs e)
{
    this.Response.Write("asazure://<region>.asazure.windows.net/<servername>");
}
```

## <a name="see-also"></a>Ayrıca bkz.

[İstemci kitaplıkları](analysis-services-data-providers.md)   
[Power BI masaüstünden Bağlan](analysis-services-connect-pbi.md)
