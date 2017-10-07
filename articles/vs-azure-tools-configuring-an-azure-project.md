---
title: bir Azure bulut hizmeti projesini Visual Studio ile aaaConfigure | Microsoft Docs
description: "Nasıl tooconfigure bir Azure bulut hizmeti projesini Visual Studio'da o projesi, gereksinimlerinize bağlı olarak öğrenin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Bir Azure bulut hizmeti projesi ile Visual Studio'yu yapılandırma
Bu proje için gereksinimlerinize bağlı olarak, bir Azure bulut hizmeti projesi yapılandırabilirsiniz. Kategoriler aşağıdaki hello hello proje özelliklerini ayarlayabilirsiniz:

- **Bir bulut hizmeti tooAzure yayımlama** -var olan bir bulut dağıtılan hizmet tooAzure yanlışlıkla silinmez emin bir özellik toomake ayarlayabilirsiniz.
- **Çalıştırmak veya hello yerel bilgisayardaki bir bulut hizmetinde hata ayıklama** -hizmet yapılandırma toouse seçin ve toostart hello Azure storage öykünücüsü isteyip istemediğinizi belirtin.
- **Bir bulut hizmet paketi oluşturulduğunda doğrulama** -tüm uyarıları hata olarak o hello bulut hizmet paketi sağlayabilirsiniz böylece herhangi bir sorun oluşmadan dağıtır tootreat karar verebilirsiniz. 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>Adımları tooconfigure bir Azure bulut hizmeti projesi
1. Visual Studio'da bir bulut hizmeti projesi oluşturun veya açın

1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve, hello bağlam menüsünden seçin **özellikleri**.
   
1. Merhaba Hello projenin Özellikler sayfasında, seçin **geliştirme** sekmesi.

    ![Proje Özellikleri menüsü](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Ayarlama **var olan bir dağıtıma silmeden önce sor** çok**doğru**. Bu ayar Azure var olan bir dağıtıma yanlışlıkla silmeyin tooensure yardımcı olur.

1. İstenen select hello **hizmet yapılandırmasını** tooindicate hangi hizmet yapılandırmasını toouse çalıştırdığınızda veya Bulut hizmeti yerel olarak hata ayıklama istiyor. Hakkında daha fazla bilgi için bir rol için bir hizmet yapılandırması toomodify bkz [nasıl tooconfigure hello rolleri bir Azure için bulut hizmeti Visual Studio ile](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Ayarlama **Başlat Azure storage öykünücüsü** çok**True** çalıştırdığınızda veya Bulut hizmeti yerel olarak hata ayıklama toostart hello Azure storage öykünücüsü.

1. Ayarlama **uyarıları hata ele** çok**True** toomake paketi doğrulama hatası varsa yayımlayamıyor emin.

1. Ayarlama **web projesi bağlantı noktalarını kullanacak** çok**True** toomake web rolünüz aynı bağlantı noktası her hello kullandığından emin zaman onu yerel IIS Express olarak başlatır.

1. Merhaba Visual Studio araç çubuğundan seçin **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
- [Birden çok hizmet yapılandırmalarını kullanarak bir Azure projesi yapılandırın](vs-azure-tools-multiple-services-project-configurations.md)

