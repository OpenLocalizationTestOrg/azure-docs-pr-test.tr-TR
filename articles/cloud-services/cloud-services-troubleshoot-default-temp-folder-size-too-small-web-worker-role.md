---
title: "aaaDefault TEMP klasörü boyutunu bir rol için çok küçük | Microsoft Docs"
description: "Sınırlı miktarda alan hello TEMP klasörü için bir bulut hizmet rolü vardır. Bu makalede hakkında bazı öneriler sağlar tooavoid alana sahip."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="28d1b-104">Varsayılan TEMP klasörü boyutu bir bulut hizmeti web/çalışan rolü çok küçük.</span><span class="sxs-lookup"><span data-stu-id="28d1b-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="28d1b-105">Merhaba varsayılan bir bulut hizmeti çalışan veya web rolü geçici dizininin tam bir noktada dönüşebilir 100 MB maksimum boyuta sahip.</span><span class="sxs-lookup"><span data-stu-id="28d1b-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="28d1b-106">Bu makalede nasıl tooavoid hello geçici dizin için alan azalıyor.</span><span class="sxs-lookup"><span data-stu-id="28d1b-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="28d1b-107">Alana neden çalıştırılsın mı?</span><span class="sxs-lookup"><span data-stu-id="28d1b-107">Why do I run out of space?</span></span>
<span data-ttu-id="28d1b-108">Merhaba standart Windows ortam değişkenleri TEMP ve TMP uygulamanızda çalışan kullanılabilir toocode kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="28d1b-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="28d1b-109">TEMP ve TMP 100 MB maksimum boyuta sahip tek bir dizin tooa gelin.</span><span class="sxs-lookup"><span data-stu-id="28d1b-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="28d1b-110">Bu dizinde depolanan tüm verileri hello bulut hizmeti hello yaşam döngüsü kalıcı değildir; bir bulut hizmeti Hello rol örneklerinin dönüştürülünceye, hello dizin temizlendi.</span><span class="sxs-lookup"><span data-stu-id="28d1b-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="28d1b-111">Öneri toofix hello sorunu</span><span class="sxs-lookup"><span data-stu-id="28d1b-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="28d1b-112">Aşağıdaki alternatifleri hello birini uygulayın:</span><span class="sxs-lookup"><span data-stu-id="28d1b-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="28d1b-113">Yerel depolama kaynağı yapılandırın ve TEMP veya TMP kullanmak yerine doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28d1b-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="28d1b-114">tooaccess uygulamanızdaki çağrısı hello çalışan kodu yerel depolama kaynağı [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="28d1b-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="28d1b-115">Yerel depolama kaynağı yapılandırın ve hello TEMP ve TMP dizinleri toopoint toohello yolu hello yerel depolama kaynağı gelin.</span><span class="sxs-lookup"><span data-stu-id="28d1b-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="28d1b-116">Bu değişikliği hello içinde gerçekleştirilmelidir [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="28d1b-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="28d1b-117">Merhaba aşağıdaki kod örneğinde nasıl toomodify hello hedef dizinleri TEMP ve TMP gelen hello OnStart yöntemi içinde gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="28d1b-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="28d1b-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="28d1b-118">Next steps</span></span>
<span data-ttu-id="28d1b-119">Açıklayan bir blog okuma [nasıl tooincrease hello hello Azure Web rolü ASP.NET geçici klasörü boyutunu](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="28d1b-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="28d1b-120">Daha fazla bilgi görüntülemek [sorun giderme makalelerini](/?tag=top-support-issue&product=cloud-services) bulut Hizmetleri için.</span><span class="sxs-lookup"><span data-stu-id="28d1b-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="28d1b-121">Azure PaaS bilgisayar tanılama verilerini kullanarak tootroubleshoot bulut hizmet rolü sorunları nasıl toolearn görüntülemek [Kevin Williamson'ın blog dizisini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="28d1b-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
