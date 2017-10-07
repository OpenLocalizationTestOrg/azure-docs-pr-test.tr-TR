---
title: "Eclipse için Azure Araç Seti hello aaaEnable oturum benzeşimi kullanma"
description: "Nasıl tooenable oturum benzeşimi kullanılarak izin ver hello Eclipse için Azure Araç Seti öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>Oturum benzeşimi etkinleştirme
Eclipse için Azure Araç Seti Hello içinde HTTP oturum benzeşimi ya da "Yapışkan oturumlarına", rollerinizi etkinleştirebilirsiniz. Merhaba aşağıdaki resimde gösterilmiştir hello **Yük Dengeleme** özellikler kullanılan iletişim tooenable hello oturum benzeşimi özelliğini:

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>tooenable oturum benzeşimi rolünüz için
1. Merhaba rol Eclipse'nın Proje Gezgini'nde sağ tıklayın, **Azure**ve ardından **Yük Dengeleme**.

2. Merhaba, **WorkerRole1 Yük Dengeleme özelliklerini** iletişim:

   a. Denetleme **bu rol için HTTP etkinleştirme oturum benzeşimi (Yapışkan oturumları).**

   b. İçin **giriş uç noktası toouse**, örneğin, bir giriş uç noktası toouse seçin **http (ortak: 80, özel: 8080)**. Uygulamanız bu uç noktası, HTTP uç noktası olarak kullanmanız gerekir. Birden çok uç nokta rolünüz için etkinleştirebilirsiniz, ancak yalnızca bunlardan birinin toosupport seçebilirsiniz Yapışkan oturumları.

   c. Uygulamanızı yeniden oluşturun.

Birden fazla rol örneği varsa, etkinleştirildikten sonra belirli bir istemciden gelen HTTP istekleri aynı hello tarafından işlenen devam edecek rol örneği.

Merhaba Eclipse Araç Seti Bu uygulama isteği yönlendirme (ARR) her rolü örneklerinizi adlı özel bir IIS Modülü yükleyerek sağlar. ARR, HTTP isteklerini toohello uygun rol örneği yeniden yönlendirmeler. Böylece Hello gelen HTTP trafiği ilk yönlendirilmiş toohello ARR yazılım hello Araç Seti seçili hello uç noktası otomatik olarak yeniden yapılandırır. Merhaba Araç Seti ayrıca Java sunucunuz için yapılandırılmış toolisten olan yeni bir iç uç noktası oluşturur. ARR tooreroute hello HTTP trafiği toohello uygun rol örneği tarafından kullanılan hello endpoint olmasıdır. Tümü için ters proxy hello gibi diğer örnekleri Yapışkan oturumları etkinleştirme bu şekilde, her rol örneği çok örnekli dağıtımınızdaki işlevi görür.

## <a name="notes-about-session-affinity"></a>Oturum benzeşimi ile ilgili notlar
* Oturum benzeşimi hello işlem öykünücüsü çalışmaz. Hello ayarları hello işlem öykünücüsü yapı işleminizin engellemeden uygulanabilir veya öykünücü yürütme işlem, ancak hello özelliğe hello işlem öykünücüsü içinde çalışmaz.

* Oturum benzeşimi etkinleştirme hello Azure, dağıtımınızdaki tarafından ek yazılım indirilir ve hello Azure bulut hizmetinize başlatıldığında rolü örneklerinizi yüklü olarak kapladığı disk alanı miktarını artış neden olur.

* Başlangıç saati tooinitialize her rol daha uzun sürer.

* İç uç nokta, toofunction, yukarıda belirtildiği gibi bir trafik rerouter olarak eklenir.


## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse] 

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
