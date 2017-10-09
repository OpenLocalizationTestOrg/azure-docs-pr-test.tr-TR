---
title: "Windows sanal makine DotNet çekirdek Öğreticisi 1 aaaAzure | Microsoft Docs"
description: "Azure sanal makinesi DotNet çekirdek Öğreticisi"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 14d5f250-1f76-49d4-898f-07b58fd39e7c
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8df69c496f44acb02d8afc45695349ec1f558f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toowindows-virtual-machines"></a>Uygulama dağıtımlarını tooWindows sanal makineleri otomatikleştirme

Bu dört bölümlü seri dağıtma ve Azure kaynak ve uygulamaları Azure Resource Manager şablonları kullanarak yapılandırma ayrıntılarını verir. Bu serideki örnek şablonu dağıtılır ve dağıtım şablonu incelenmesi hello. Bu serinin Hello hedef hello ilişkideki Azure kaynakları arasında tooeducate ve tam olarak tümleşik Azure Resource Manager şablonları dağıtımı deneyimi tooprovide aktarır. Bu belge temel düzeyde bir bilgi Azure Resource Manager ile varsayar, bu öğreticiye başlamadan önce temel Azure Resource Manager kavramları öğrenmeniz.

## <a name="music-store-application"></a>Müzik deposu uygulama
Merhaba bu dizide kullanılan örnek olan bir .net Core uygulama deneyimi alışveriş müzik deposu benzetimini yapma. Bu uygulama, dağıtılan tooeither bir Linux veya Windows sanal sistem, örnek dağıtımları her ikisi için oluşturulmuş olabilir. Merhaba uygulama bir web uygulaması ve SQL veritabanı içerir. Bu serideki Hello makaleleri okumadan önce bu sayfada bulunan hello dağıtım düğmesini kullanarak hello uygulamayı dağıtın. Tam olarak dağıtıldığında, hello uygulama / Azure Mimarisi diyagramı aşağıdaki hello gibi görünüyor. 

Merhaba müzik deposu Resource Manager şablonu burada bulunabilir [müzik deposu Windows şablonu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)

![Müzik deposu uygulama](./media/dotnet-core-1-landing/music-store.png)

Merhaba dahil olmak üzere, bu bileşenlerin her birini JSON dört makaleler hello incelenir şablon ilişkilendirin.

* [**Uygulama Mimarisi** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – uygulama bileşenleri gibi web siteleri ve veritabanları sanal makineler ve Azure SQL veritabanları gibi Azure bilgisayar kaynaklarına barındırılan toobe gerekir. Bu belge eşleme işlem gereksinimi, tooAzure kaynakları ve Azure Resource Manager şablonu ile bu kaynakları dağıtma anlatılmaktadır. 
* [**Erişim ve güvenliği** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – Azure uygulamalarda barındırma gerekli tooconsider Merhaba uygulaması erişilen nasıl ve farklı uygulama bileşenleri birbirine erişim nasıl olur. Bu belge, sağlama ve Internet erişimi tooan uygulama ve uygulama bileşenleri arasında erişimi güvenli hale getirme ayrıntıları.
* [**Kullanılabilirlik ve ölçek** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – kullanılabilirliğini ve ölçeğini altyapı kapalı kalma süresi sırasında çalışan toohello uygulamaları özelliği toostay bakın ve hello özelliği tooscale işlem kaynakları toomeet uygulama isteğe bağlı. Bu belge ayrıntıları hello bileşenlerini bir yük dengeli toodeploy ve yüksek oranda kullanılabilir uygulama gerekli.
* [**Uygulama dağıtımı** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) - uygulamaları üzerine Azure sanal makineler, hangi hello tarafından uygulama ikili dosyaları yüklü hello sanal makine üzerinde hello yöntemi dağıtma dikkate alınmalıdır. Bu belge, Azure sanal makine özel komut dosyası uzantılarını kullanarak otomatik otomatikleştirme uygulama yükleme ayrıntıları.

Azure Resource Manager şablonları geliştirirken hello tooautomate hello dağıtım Azure altyapısı ve hello yükleme ve yapılandırma bu Azure altyapı üzerinde barındırılan tüm uygulamaların hedeftir. Bu makaleler aracılığıyla çalışma bu deneyim ilişkin bir örnek sağlar.

## <a name="deploy-hello-music-store-application"></a>Merhaba müzik deposu uygulaması dağıtma
Bu düğme kullanarak Hello müzik deposu uygulama dağıtılabilir.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-windows%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

Hello Azure Resource Manager şablonu parametre değerlerini aşağıdaki hello gerektirir.

| Parametre Adı | Açıklama |
| --- | --- |
| ADMINUSERNAME |Merhaba sanal makine ve hello Azure SQL veritabanı üzerinde kullanılan yönetici kullanıcı adı. |
| ADMINPASSWORD |Hello Azure sanal makinesi ve SQL veritabanı üzerinde kullanılan parola. |
| NUMBEROFINSTANCES |oluşturulan sanal makineler toobe Hello sayısı. Her bu sanal makineleri ana bilgisayar Merhaba müzik deposu web uygulaması ve tüm trafiği bunları dengelendiği ' dir. |
| PUBLICIPADDRESSDNSNAME |Merhaba genel IP adresi ile ilişkili genel benzersiz DNS adı. |

Merhaba şablon dağıtımı tamamlandığında, ortak IP adresi herhangi bir internet tarayıcı kullanarak toohello göz atın. Merhaba .net Core müzik site sunulabilir.

## <a name="next-steps"></a>Sonraki adımlar
<hr>

[1. adım - Azure Resource Manager şablonları ile uygulama mimarisi](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[2. adım - Azure Resource Manager şablonları güvenlik ve erişim](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[3. adım - kullanılabilirliğini ve ölçeğini Azure Resource Manager şablonlarındaki](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[4. adım - Azure Resource Manager şablonları ile uygulama dağıtımı](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

