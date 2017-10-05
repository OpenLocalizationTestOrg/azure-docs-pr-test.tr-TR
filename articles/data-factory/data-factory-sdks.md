---
title: "Azure Data Factory Geliştirici Başvurusu"
description: "Oluştur, izlemek ve Azure data factory'leri yönetmek için farklı yollar hakkında bilgi edinin"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: dc752fa1-a6c3-4753-904e-9f32d0a940b7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2017
ms.author: spelluru
redirect_url: https://azure.microsoft.com/services/data-factory/
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: e0f6c078b60df6bb7381d066bebb3e400b3b97ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory-developer-reference"></a><span data-ttu-id="81b53-103">Azure Data Factory Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="81b53-103">Azure Data Factory Developer Reference</span></span>
<span data-ttu-id="81b53-104">Oluşturun, izlemek ve Azure portalı, Azure PowerShell, .NET sınıf kitaplığı veya REST API kullanarak oluşturucuları yönetin.</span><span class="sxs-lookup"><span data-stu-id="81b53-104">You can create, monitor, and manage the factories using either Azure portal, Azure PowerShell, .NET Class Library, or REST API.</span></span>

| <span data-ttu-id="81b53-105">Yöntem</span><span class="sxs-lookup"><span data-stu-id="81b53-105">Method</span></span> | <span data-ttu-id="81b53-106">Kaynak Konumu</span><span class="sxs-lookup"><span data-stu-id="81b53-106">Resource Location</span></span> | <span data-ttu-id="81b53-107">Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="81b53-107">Developer References</span></span> |
| --- | --- | --- |
| <span data-ttu-id="81b53-108">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="81b53-108">Azure portal</span></span> |[<span data-ttu-id="81b53-109">https://Portal.Azure.com/</span><span class="sxs-lookup"><span data-stu-id="81b53-109">https://portal.azure.com/</span></span>](https://portal.azure.com) |[<span data-ttu-id="81b53-110">Azure Data Factory (Azure portalı) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="81b53-110">Get started with Azure Data Factory (Azure portal)</span></span>](data-factory-build-your-first-pipeline-using-editor.md) |
| <span data-ttu-id="81b53-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="81b53-111">Azure PowerShell</span></span> |<span data-ttu-id="81b53-112">En son karşıdan [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="81b53-112">Download the latest [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span></span> |[<span data-ttu-id="81b53-113">Cmdlet başvurusu</span><span class="sxs-lookup"><span data-stu-id="81b53-113">Cmdlet reference</span></span>](https://msdn.microsoft.com/library/dn820234.aspx) |
| <span data-ttu-id="81b53-114">.NET sınıf kitaplığı</span><span class="sxs-lookup"><span data-stu-id="81b53-114">.NET Class Library</span></span> |<span data-ttu-id="81b53-115">Azure Data Factory .NET SDK'yı oluşturmak, izlemek ve Azure data factory'leri yönetmek ve Data Factory kullanarak .NET etkinliğini genişletmek etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="81b53-115">The Azure Data Factory .NET SDK enables you to create, monitor, and manage Azure data factories and extend Data Factory using a .NET activity.</span></span> <span data-ttu-id="81b53-116">Bkz: [bir Azure Data Factory ardışık düzeninde özel etkinlikleri kullanmak](data-factory-use-custom-activities.md) ve [oluşturun, izleme ve veri fabrikası .NET SDK kullanarak Azure data factory'leri yönetme](data-factory-create-data-factories-programmatically.md) yardımcı olması için makaleleri Başlarken.</span><span class="sxs-lookup"><span data-stu-id="81b53-116">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) and [Create, monitor, and manage Azure data factories using Data Factory .NET SDK](data-factory-create-data-factories-programmatically.md) articles to help you get started.</span></span><br/><br/><span data-ttu-id="81b53-117"><b>En son Nuget indirme</b></span><span class="sxs-lookup"><span data-stu-id="81b53-117"><b>Downloading the latest Nuget</b></span></span><br/><span data-ttu-id="81b53-118">En son Azure Data Factory Yönetimi Kitaplığı Nuget paketi yükleyebilirsiniz: [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span><span class="sxs-lookup"><span data-stu-id="81b53-118">You can download the latest Azure Data Factory Management Library Nuget package from: [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span></span><br/><br/><span data-ttu-id="81b53-119">**Visual Studio'da Paket Yöneticisi konsolu kullanılarak**</span><span class="sxs-lookup"><span data-stu-id="81b53-119">**Using Package Manager Console in Visual Studio**</span></span><br/><span data-ttu-id="81b53-120">En son Azure veri fabrikası Yönetimi Kitaplığı almak için Visual Studio'nun Paket Yöneticisi konsolunda aşağıdaki komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="81b53-120">You can run the following command in Visual Studio’s Package Manager Console to get the latest Azure Data Factory Management Library</span></span><br/><br/><span data-ttu-id="81b53-121">Install-Package Microsoft.Azure.Management.DataFactories</span><span class="sxs-lookup"><span data-stu-id="81b53-121">Install-Package Microsoft.Azure.Management.DataFactories</span></span> |[<span data-ttu-id="81b53-122">.NET SDK'sı başvurusu</span><span class="sxs-lookup"><span data-stu-id="81b53-122">.NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt415893.aspx) |
| <span data-ttu-id="81b53-123">REST API</span><span class="sxs-lookup"><span data-stu-id="81b53-123">REST API</span></span> |<span data-ttu-id="81b53-124">Veri Fabrikası REST API oluşturmak, izlemek ve Azure data factory'leri yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81b53-124">You can use the Data Factory REST API to create, monitor, and manage Azure data factories.</span></span> |[<span data-ttu-id="81b53-125">REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="81b53-125">REST API Reference</span></span>](https://msdn.microsoft.com/library/dn906738.aspx) |

