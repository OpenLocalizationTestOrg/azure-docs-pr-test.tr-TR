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
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a>Varsayılan TEMP klasörü boyutu bir bulut hizmeti web/çalışan rolü çok küçük.
Merhaba varsayılan bir bulut hizmeti çalışan veya web rolü geçici dizininin tam bir noktada dönüşebilir 100 MB maksimum boyuta sahip. Bu makalede nasıl tooavoid hello geçici dizin için alan azalıyor.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a>Alana neden çalıştırılsın mı?
Merhaba standart Windows ortam değişkenleri TEMP ve TMP uygulamanızda çalışan kullanılabilir toocode kullanılabilir. TEMP ve TMP 100 MB maksimum boyuta sahip tek bir dizin tooa gelin. Bu dizinde depolanan tüm verileri hello bulut hizmeti hello yaşam döngüsü kalıcı değildir; bir bulut hizmeti Hello rol örneklerinin dönüştürülünceye, hello dizin temizlendi.

## <a name="suggestion-toofix-hello-problem"></a>Öneri toofix hello sorunu
Aşağıdaki alternatifleri hello birini uygulayın:

* Yerel depolama kaynağı yapılandırın ve TEMP veya TMP kullanmak yerine doğrudan erişebilirsiniz. tooaccess uygulamanızdaki çağrısı hello çalışan kodu yerel depolama kaynağı [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) yöntemi.
* Yerel depolama kaynağı yapılandırın ve hello TEMP ve TMP dizinleri toopoint toohello yolu hello yerel depolama kaynağı gelin. Bu değişikliği hello içinde gerçekleştirilmelidir [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) yöntemi.

Merhaba aşağıdaki kod örneğinde nasıl toomodify hello hedef dizinleri TEMP ve TMP gelen hello OnStart yöntemi içinde gösterilmektedir:

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

## <a name="next-steps"></a>Sonraki adımlar
Açıklayan bir blog okuma [nasıl tooincrease hello hello Azure Web rolü ASP.NET geçici klasörü boyutunu](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).

Daha fazla bilgi görüntülemek [sorun giderme makalelerini](/?tag=top-support-issue&product=cloud-services) bulut Hizmetleri için.

Azure PaaS bilgisayar tanılama verilerini kullanarak tootroubleshoot bulut hizmet rolü sorunları nasıl toolearn görüntülemek [Kevin Williamson'ın blog dizisini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
