---
title: "Azure hata ayıklama için aaaOptions bulut hizmetlerini | Microsoft Docs"
description: "Hata ayıklama Azure bulut Hizmetleri"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>Merhaba çeşitli şekillerde öğrenin toodebug Azure bulut hizmeti
Bu makalede bağlantılar toohello çeşitli sağlayan yolları toodebug bir Azure bulut hizmeti. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Bir Azure bulut hizmeti Visual Studio'da hata ayıklama
Zaman ve para hello Azure işlem öykünücüsü toodebug kullanarak bulut hizmetinizi yerel makinede kaydedebilirsiniz. Dağıtmadan önce bir hizmet yerel olarak hata ayıklama tarafından, güvenilirlik ve performans işlem zaman için ödeme olmadan artırabilir. Ancak, yalnızca bir bulut hizmeti Azure'da çalıştırdığınızda bazı hatalar oluşabilir. Yalnızca bir bulut hizmeti Azure'da çalıştırdığınızda oluşan hataları hizmetinizi yayımladığınızda, uzaktan hata ayıklama ve hello hata ayıklayıcı tooa rol örneği ekleme etkinleştirerek hata ayıklaması yapılabilir. Daha fazla bilgi için bkz: [, bulut hizmeti, yerel bilgisayarınızda hata ayıklama](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).

## <a name="using-azure-diagnostics"></a>Azure Tanılama'yı kullanarak 
Azure tanılama kullanabilirsiniz toolog ayrıntılı bilgileri rolleri, kod çalıştırılmasını hello rolleri hello geliştirme ortamında veya Azure çalıştırıp çalıştırmadığınızı. Daha fazla bilgi için bkz: [Azure tanılamada etkinleştirme Azure Cloud Services](http://go.microsoft.com/fwlink/p/?LinkId=400450).

## <a name="using-intellitrace"></a>IntelliTrace'i kullanma 
Kullanıyorsanız, .NET Framework 4.5 Visual Studio Enterprise toowrite rolleri hedeflenen, Visual Studio'dan Azure bulut hizmeti dağıtmak hello zamanında IntelliTrace etkinleştirebilirsiniz. IntelliTrace günlüğünü sağlar Azure'da çalışıyormuş gibi Visual Studio toodebug ile uygulamanızı kullanabilirsiniz. Daha fazla bilgi için bkz: [yayımlanan bulut hizmeti IntelliTrace ve Visual Studio ile hata ayıklama](http://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Uzaktan hata ayıklama 
Uzaktan bulut hizmetlerinizi hello bulut hizmeti Visual Studio'dan dağıttığınızda hello zamanında hata ayıklamayı etkinleştirebilirsiniz. Bir dağıtım için hata ayıklama uzak tooenable seçerseniz, uzaktan hata ayıklama Hizmetleri hello sanal makinelere her rol örneğini çalıştıran yüklenir. Gibi bu hizmetleri - `msvsmon.exe` - performansını etkilemez ya da neden ek maliyetleri de. Daha fazla bilgi için bkz: [Azure bulut hizmetinde hata ayıklama](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).

## <a name="next-steps"></a>Sonraki adımlar
- [Bir Azure bulut hizmeti ya da VM Visual Studio'da hata ayıklama](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -hello ayrıntılarını nasıl toodebug Azure cloud services öğrenin.
