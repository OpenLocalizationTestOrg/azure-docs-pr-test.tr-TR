---
title: "Azure Analysis Services'a bağlanın | Microsoft Docs"
description: "Bağlanmak ve Azure Analysis Services sunucusundan veri alma hakkında bilgi edinin."
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
ms.openlocfilehash: deb3ef28d20decef01826450bd6091f87dd069de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-an-azure-analysis-services-server"></a><span data-ttu-id="589b9-103">Bir Azure Analysis Services sunucusuna bağlan</span><span class="sxs-lookup"><span data-stu-id="589b9-103">Connect to an Azure Analysis Services server</span></span>

<span data-ttu-id="589b9-104">Bu makalede, veri modellemesi ve SQL Server Management Studio (SSMS) veya SQL Server veri Araçları (SSDT) gibi yönetim uygulamaları kullanarak bir sunucuya bağlanma açıklanır.</span><span class="sxs-lookup"><span data-stu-id="589b9-104">This article describes connecting to a server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="589b9-105">Veya Microsoft Excel, Power BI Desktop veya özel uygulamalar gibi uygulamalar istemcisiyle raporlama.</span><span class="sxs-lookup"><span data-stu-id="589b9-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="589b9-106">Azure Analysis Services bağlantı HTTPS kullanın.</span><span class="sxs-lookup"><span data-stu-id="589b9-106">Connections to Azure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="589b9-107">İstemci kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="589b9-107">Client libraries</span></span>
[<span data-ttu-id="589b9-108">Son istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="589b9-108">Get the latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="589b9-109">Tüm bağlantılar türü, bağımsız olarak bir sunucuya bağlanmak ve Analysis Services sunucusu ile arabirim için güncelleştirilmiş AMO, ADOMD.NET ve OLEDB istemci kitaplıkları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="589b9-109">All connections to a server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries to connect to and interface with an Analysis Services server.</span></span> <span data-ttu-id="589b9-110">SSMS, SSDT, Excel 2016 ve Power BI için en son istemci kitaplıkları yüklü veya aylık sürümleriyle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="589b9-110">For SSMS, SSDT, Excel 2016, and Power BI, the latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="589b9-111">Ancak, bazı durumlarda, bir uygulamanın en son olmayabilir mümkündür.</span><span class="sxs-lookup"><span data-stu-id="589b9-111">However, in some cases, it's possible an application may not have the latest.</span></span> <span data-ttu-id="589b9-112">Örneğin, ne zaman ilkeleri gecikme güncelleştirir veya Office 365 güncelleştirmelerini ertelenmiş kanalı markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="589b9-112">For example, when policies delay updates, or Office 365 updates are on the Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="589b9-113">Sunucu adı</span><span class="sxs-lookup"><span data-stu-id="589b9-113">Server name</span></span>

<span data-ttu-id="589b9-114">Azure'da bir Analysis Services sunucusu oluşturduğunuzda, benzersiz bir ad ve sunucunun oluşturulması olduğu bölge belirtin.</span><span class="sxs-lookup"><span data-stu-id="589b9-114">When you create an Analysis Services server in Azure, you specify a unique name and the region where the server is to be created.</span></span> <span data-ttu-id="589b9-115">Bir bağlantı sunucu adı belirtme sunucu adlandırma şeması olur:</span><span class="sxs-lookup"><span data-stu-id="589b9-115">When specifying the server name in a connection, the server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="589b9-116">Dize olduğu Protokolü **asazure**, bölgedir sunucu oluşturulduğu URI (örneğin, westus.asazure.windows.net) ve servername bölge içinde benzersiz sunucunuzun adıdır.</span><span class="sxs-lookup"><span data-stu-id="589b9-116">Where protocol is string **asazure**, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.</span></span>

### <a name="get-the-server-name"></a><span data-ttu-id="589b9-117">Sunucu adını Al</span><span class="sxs-lookup"><span data-stu-id="589b9-117">Get the server name</span></span>
<span data-ttu-id="589b9-118">İçinde **Azure portal** > server > **genel bakış** > **sunucu adı**, tüm sunucu adını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="589b9-118">In **Azure portal** > server > **Overview** > **Server name**, copy the entire server name.</span></span> <span data-ttu-id="589b9-119">Kuruluşunuzda bulunan diğer kullanıcıların bu sunucuya çok bağlanıyorsanız, bu sunucu adı onlarla paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="589b9-119">If other users in your organization are connecting to this server too, you can share this server name with them.</span></span> <span data-ttu-id="589b9-120">Bir sunucu adı belirtirken, tüm yol kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="589b9-120">When specifying a server name, the entire path must be used.</span></span>

![Azure'da sunucu adını alma](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="589b9-122">Bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="589b9-122">Connection string</span></span>

<span data-ttu-id="589b9-123">Tablo nesne modelini kullanarak Azure Analysis Services için bağlanırken aşağıdaki bağlantı dize biçimleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="589b9-123">When connecting to Azure Analysis Services using the Tabular Object Model, use the following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="589b9-124">Tümleşik Azure Active Directory kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="589b9-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="589b9-125">Tümleşik kimlik doğrulaması Azure Active Directory kimlik bilgisi önbelleği varsa seçer.</span><span class="sxs-lookup"><span data-stu-id="589b9-125">Integrated authentication picks up the Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="589b9-126">Aksi durumda, Azure oturum açma penceresi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="589b9-126">If not, the Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="589b9-127">Kullanıcı adı ve parola ile Azure Active Directory kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="589b9-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="589b9-128">Windows kimlik doğrulaması (tümleşik güvenliği)</span><span class="sxs-lookup"><span data-stu-id="589b9-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="589b9-129">Geçerli işlem çalıştıran Windows hesabını kullanın.</span><span class="sxs-lookup"><span data-stu-id="589b9-129">Use the Windows account running the current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="589b9-130">Bir .odc dosyası kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="589b9-130">Connect using an .odc file</span></span>
<span data-ttu-id="589b9-131">Excel'in eski sürümleriyle, kullanıcıların bir Office veri bağlantısı (.odc) dosyası kullanarak bir Azure Analysis Services sunucusuna bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="589b9-131">With older versions of Excel, users can connect to an Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="589b9-132">Daha fazla bilgi için bkz: [bir Office veri bağlantısı (.odc) dosyası oluşturun](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="589b9-132">To learn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="589b9-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="589b9-133">Next steps</span></span>
<span data-ttu-id="589b9-134">[Excel ile bağlanma](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="589b9-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="589b9-135">[Power BI ile bağlanma](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="589b9-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="589b9-136">Sunucunuzu Yönetin</span><span class="sxs-lookup"><span data-stu-id="589b9-136">Manage your server</span></span>](analysis-services-manage.md)   

