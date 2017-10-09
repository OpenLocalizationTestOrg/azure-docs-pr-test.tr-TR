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
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="11636-103">Tooan Azure Analysis Services sunucusuna bağlan</span><span class="sxs-lookup"><span data-stu-id="11636-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="11636-104">Bu makalede, veri modellemesi ve SQL Server Management Studio (SSMS) veya SQL Server veri Araçları (SSDT) gibi yönetim uygulamaları kullanarak bağlanan tooa sunucu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="11636-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="11636-105">Veya Microsoft Excel, Power BI Desktop veya özel uygulamalar gibi uygulamalar istemcisiyle raporlama.</span><span class="sxs-lookup"><span data-stu-id="11636-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="11636-106">Bağlantıları tooAzure Analysis Services HTTPS kullanın.</span><span class="sxs-lookup"><span data-stu-id="11636-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="11636-107">İstemci kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="11636-107">Client libraries</span></span>
[<span data-ttu-id="11636-108">Merhaba son istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="11636-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="11636-109">Türü, bağımsız olarak tüm bağlantılar tooa server güncelleştirilmiş AMO, ADOMD.NET ve OLEDB istemci kitaplıkları tooconnect tooand arabirimi ile bir Analysis Services sunucusu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="11636-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="11636-110">SSMS, SSDT, Excel 2016 ve Power BI için hello son istemci kitaplıkları yüklü veya aylık sürümleriyle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="11636-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="11636-111">Ancak, bazı durumlarda, bir uygulama hello son olmayabilir mümkündür.</span><span class="sxs-lookup"><span data-stu-id="11636-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="11636-112">Örneğin, ne zaman ilkeleri gecikme güncelleştirir veya Office 365 güncelleştirmelerini ertelenmiş kanal hello üzerinde markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="11636-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="11636-113">Sunucu adı</span><span class="sxs-lookup"><span data-stu-id="11636-113">Server name</span></span>

<span data-ttu-id="11636-114">Azure'da bir Analysis Services sunucusu oluşturduğunuzda, hello sunucunun oluşturulan toobe olduğu bir benzersiz ad ve hello bölge belirtin.</span><span class="sxs-lookup"><span data-stu-id="11636-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="11636-115">Bir bağlantı Hello sunucu adı belirtme hello sunucu adlandırma şeması olur:</span><span class="sxs-lookup"><span data-stu-id="11636-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="11636-116">Dize olduğu Protokolü **asazure**, bölgedir hello hello sunucu oluşturulduğu URI (örneğin, westus.asazure.windows.net) ve servername hello bölge içinde benzersiz sunucunuzun hello adı.</span><span class="sxs-lookup"><span data-stu-id="11636-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="11636-117">Merhaba sunucu adını Al</span><span class="sxs-lookup"><span data-stu-id="11636-117">Get hello server name</span></span>
<span data-ttu-id="11636-118">İçinde **Azure portal** > server > **genel bakış** > **sunucu adı**, kopya hello tüm sunucu adı.</span><span class="sxs-lookup"><span data-stu-id="11636-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="11636-119">Kuruluşunuzda bulunan diğer kullanıcıların toothis sunucu çok bağlanıyorsanız, bu sunucu adı onlarla paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11636-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="11636-120">Bir sunucu adı belirtirken, yolun tamamını hello kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="11636-120">When specifying a server name, hello entire path must be used.</span></span>

![Azure'da sunucu adını alma](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="11636-122">Bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="11636-122">Connection string</span></span>

<span data-ttu-id="11636-123">TooAzure bağlanırken kullanarak Analysis Services tablo nesne modeli, bağlantı dizesi biçimleri aşağıdaki kullanım hello hello:</span><span class="sxs-lookup"><span data-stu-id="11636-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="11636-124">Tümleşik Azure Active Directory kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="11636-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="11636-125">Tümleşik kimlik doğrulaması hello Azure Active Directory kimlik bilgisi önbellek varsa seçer.</span><span class="sxs-lookup"><span data-stu-id="11636-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="11636-126">Aksi durumda, hello Azure oturum açma penceresi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="11636-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="11636-127">Kullanıcı adı ve parola ile Azure Active Directory kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="11636-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="11636-128">Windows kimlik doğrulaması (tümleşik güvenliği)</span><span class="sxs-lookup"><span data-stu-id="11636-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="11636-129">Merhaba geçerli işlem çalışan hello Windows hesabını kullanın.</span><span class="sxs-lookup"><span data-stu-id="11636-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="11636-130">Bir .odc dosyası kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="11636-130">Connect using an .odc file</span></span>
<span data-ttu-id="11636-131">Excel'in eski sürümleriyle, kullanıcıların bir Office veri bağlantısı (.odc) dosyası kullanarak tooan Azure Analysis Services sunucusuna bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="11636-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="11636-132">toolearn daha, fazla [bir Office veri bağlantısı (.odc) dosyası oluşturun](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="11636-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="11636-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11636-133">Next steps</span></span>
<span data-ttu-id="11636-134">[Excel ile bağlanma](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="11636-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="11636-135">[Power BI ile bağlanma](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="11636-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="11636-136">Sunucunuzu Yönetin</span><span class="sxs-lookup"><span data-stu-id="11636-136">Manage your server</span></span>](analysis-services-manage.md)   

