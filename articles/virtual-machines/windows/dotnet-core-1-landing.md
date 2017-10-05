---
title: "Azure Windows sanal makine DotNet çekirdek Öğreticisi 1 | Microsoft Docs"
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
ms.openlocfilehash: bfb3a27d20e8cdcff8dff75e4dfb2685e2781d45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automating-application-deployments-to-windows-virtual-machines"></a>Uygulama dağıtımları için Windows sanal makineleri otomatikleştirme

Bu dört bölümlü seri dağıtma ve Azure kaynak ve uygulamaları Azure Resource Manager şablonları kullanarak yapılandırma ayrıntılarını verir. Bu serideki örnek şablonu dağıtılır ve dağıtım şablonu inceledi. Azure kaynakları arasındaki ilişkiyi bilgilendirin ve ellere tam olarak tümleşik Azure Resource Manager şablonları dağıtımı deneyimi sağlamak için bu dizinin hedefidir. Bu belge temel düzeyde bir bilgi Azure Resource Manager ile varsayar, bu öğreticiye başlamadan önce temel Azure Resource Manager kavramları öğrenmeniz.

## <a name="music-store-application"></a>Müzik deposu uygulama
Bu serideki kullanılan örnek bir .net olan çekirdek uygulama deneyimi alışveriş müzik deposu benzetimini yapma. Bu uygulama için bir Linux veya Windows sanal makine dağıtılabilir, örnek dağıtımları her ikisi için oluşturulmuş. Uygulama bir web uygulaması ve SQL veritabanı içerir. Bu serideki makaleleri okumadan önce bu sayfada bulunan dağıtım düğmesini kullanarak uygulamayı dağıtın. Tam olarak dağıtıldığında, uygulama / Azure Mimarisi Aşağıdaki diyagramda gibi görünüyor. 

Müzik deposu Resource Manager şablonu burada bulunabilir [müzik deposu Windows şablonu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)

![Müzik deposu uygulama](./media/dotnet-core-1-landing/music-store.png)

İlişkilendirme şablon JSON dahil olmak üzere, bu bileşenlerin her birini aşağıdaki dört makalelerinde incelenir.

* [**Uygulama Mimarisi** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – uygulama bileşenleri gibi web siteleri ve veritabanları sanal makineler ve Azure SQL veritabanları gibi Azure bilgisayar kaynakları üzerinde barındırılması gerekir. Bu belge eşleme işlem gerek Azure kaynakları ve Azure Resource Manager şablonu ile bu kaynakları dağıtma anlatılmaktadır. 
* [**Erişim ve güvenliği** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – Azure uygulamalarda barındırma uygulamayı nasıl erişilir ve nasıl farklı uygulama bileşenleri erişim birbirine göz önünde bulundurmanız gereken olur. Bu belge, sağlama ve uygulamaya internet erişimi ve uygulama bileşenleri arasında erişimi güvenli hale getirme ayrıntıları.
* [**Kullanılabilirlik ve ölçek** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – kullanılabilirliğini ve ölçeğini uygulamaları özelliği altyapı kapalı kalma süresi sırasında çalışan kalır ve uygulama talebi karşılamak üzere işlem kaynaklarını ölçeklendirme olanağı bakın. Bu belge ayrıntıları bir yük dengeli dağıtmak için gereken bileşenler ve yüksek oranda kullanılabilir uygulama.
* [**Uygulama dağıtımı** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) - uygulamaları üzerine Azure sanal makineler tarafından uygulama ikili dosyaları sanal makineye yüklenir yöntemi dağıtma dikkate alınmalıdır. Bu belge, Azure sanal makine özel komut dosyası uzantılarını kullanarak otomatik otomatikleştirme uygulama yükleme ayrıntıları.

Azure Resource Manager şablonları geliştirirken Azure altyapısı ve yüklenmesini ve yapılandırılmasını bu Azure altyapı üzerinde barındırılan herhangi bir uygulama dağıtımını otomatik hale getirmek için belirtilir. Bu makaleler aracılığıyla çalışma bu deneyim ilişkin bir örnek sağlar.

## <a name="deploy-the-music-store-application"></a>Müzik deposu uygulama dağıtma
Müzik deposu uygulama bu düğmesi kullanılarak dağıtılabilir.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-windows%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

Azure Resource Manager şablonu aşağıdaki parametre değerleri gerektirir.

| Parametre Adı | Açıklama |
| --- | --- |
| ADMINUSERNAME |Sanal makine ve Azure SQL veritabanı üzerinde kullanılan yönetici kullanıcı adı. |
| ADMINPASSWORD |SQL Database ve Azure sanal makine üzerinde kullanılan parola. |
| NUMBEROFINSTANCES |Oluşturulacak sanal makine sayısı. Bu sanal makinelerin her konak müzik deposu web uygulaması ve bunları dengelendiği tüm trafiğidir. |
| PUBLICIPADDRESSDNSNAME |Genel IP adresi ile ilişkili genel benzersiz DNS adı. |

Şablon dağıtımı tamamlandığında, herhangi bir internet tarayıcı kullanarak genel IP adresine göz atın. .Net Core müzik site sunulabilir.

## <a name="next-steps"></a>Sonraki adımlar
<hr>

[1. adım - Azure Resource Manager şablonları ile uygulama mimarisi](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[2. adım - Azure Resource Manager şablonları güvenlik ve erişim](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[3. adım - kullanılabilirliğini ve ölçeğini Azure Resource Manager şablonlarındaki](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[4. adım - Azure Resource Manager şablonları ile uygulama dağıtımı](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

