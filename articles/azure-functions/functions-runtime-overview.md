---
title: "aaaAzure işlevleri çalışma zamanına genel bakış | Microsoft Docs"
description: "Hello Azure işlevleri çalışma zamanı önizlemesi genel bakış"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Azure işlevleri çalışma zamanına genel bakış

Hello Azure işlevleri çalışma zamanı programlama modeli şirket içi, tootake avantajlarından hello kolaylık ve esneklik hello Azure işlevlerinin için yeni bir yolunu sunar. Azure işlevleri, Azure işlevleri çalışma zamanı olduğu gibi neredeyse aynı geliştirme deneyimi hello bulut hizmeti olarak şirket içinde dağıtılabilir tooprovide hello üzerinde oluşturulmuş aynı kaynak kökleri açın.

![Azure işlevleri çalışma zamanı Önizleme portalı][1]

Hello Azure işlevleri çalışma zamanı toohello bulut kaydetmeden önce bir yol, tooexperience Azure işlevleri sağlar. Geçirdiğinizde bu şekilde, oluşturacağınız hello kod varlıklarına sonra toohello bulutla alınabilir.  Örneğin, şirket içi bilgisayarları toorun toplu işlemler hello yedek işlem gücünü günde kullanarak yeni seçeneklerini, Hello çalışma zamanı da açılır. Cihazlar, kuruluş tooconditionally gönderme veri tooother sistemlerinizi, hem şirket içinde ve hello bulutta de kullanabilirsiniz.

Hello Azure işlevleri çalışma zamanı iki parça oluşur:
* Azure işlevleri çalışma zamanı Yönetimi rolü
* Azure işlevleri çalışma zamanı çalışan rolü

## <a name="azure-functions-management-role"></a>Azure işlevleri Yönetimi rolü

Hello Azure işlevleri yönetim rolü işlevleri şirket içi hello yönetimi için bir konak sağlar. Bu rolü hello aşağıdaki görevleri gerçekleştirir:

* Merhaba hello olan Azure işlevleri Yönetim Portalı barındırma, hello hello gördüğünüz aynı [Azure portal](https://portal.azure.com). Şekilde hello Azure portalı gibi bu sağlar, işlevlerde geliştirmek aynı hello.
* İşlevler arasında birden çok işlevleri Worker dağıtma.
* Microsoft Visual Studio, işlevleri doğrudan yayımlaması yayımlama bir uç noktası sağlama.

## <a name="azure-functions-worker-role"></a>Azure işlevleri çalışan rolü

Hello Azure işlevleri çalışan rolleri Windows kapsayıcılarında dağıtılır ve bu işlev kodunuzu nereye yürütür.  Birden çok çalışan rolleri kuruluşunuz genelinde dağıtabilirsiniz ve müşteriler hale getirebilir anahtar şekilde yedek işlem gücünü kullanın.

## <a name="minimum-requirements"></a>En düşük gereksinimler

hello Azure işlevleri sahip bir makine olmalıdır çalışma zamanı ile çalışmaya tooget **Windows Server 2016 veya Windows 10 oluşturucuları Update** erişim tooa ile **SQL Server** örneği.

## <a name="next-steps"></a>Sonraki Adımlar

Merhaba yüklemek [Azure işlevleri çalışma zamanı Önizleme](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
