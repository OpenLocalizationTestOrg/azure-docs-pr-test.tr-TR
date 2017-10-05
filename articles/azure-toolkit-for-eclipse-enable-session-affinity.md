---
title: "Eclipse için Azure Araç Seti kullanarak oturum benzeşimi etkinleştir"
description: "Eclipse için Azure Araç Seti kullanarak oturum benzeşimi etkinleştirme hakkında bilgi edinin."
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
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a>Oturum benzeşimi etkinleştirme
Eclipse için Azure araç içinde HTTP oturum benzeşimi ya da "Yapışkan oturumlarına", rollerinizi etkinleştirebilirsiniz. Aşağıdaki resimde gösterildiği **Yük Dengeleme** oturum benzeşimi özelliğini etkinleştirmek için kullanılan özellikleri iletişim kutusu:

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a>Rolünüz için oturum benzeşimi etkinleştirmek için
1. Eclipse'nın Proje Gezgini rolüne sağ tıklayın, **Azure**ve ardından **Yük Dengeleme**.

2. İçinde **WorkerRole1 Yük Dengeleme özelliklerini** iletişim:

   a. Denetleme **bu rol için HTTP etkinleştirme oturum benzeşimi (Yapışkan oturumları).**

   b. İçin **giriş kullanmak için uç nokta**, örneğin kullanmak için bir giriş uç noktası seçin **http (ortak: 80, özel: 8080)**. Uygulamanız bu uç noktası, HTTP uç noktası olarak kullanmanız gerekir. Birden çok uç nokta rolünüz için etkinleştirebilirsiniz, ancak Yapışkan oturumları desteklemek için bunlardan yalnızca birini seçebilirsiniz.

   c. Uygulamanızı yeniden oluşturun.

Birden fazla rol örneği varsa, etkinleştirildikten sonra belirli bir istemciden gelen HTTP istekleri aynı rol örneği tarafından işlenen devam eder.

Eclipse Araç Seti Bu uygulama isteği yönlendirme (ARR) her rolü örneklerinizi adlı özel bir IIS Modülü yükleyerek sağlar. ARR, HTTP isteklerini uygun rol örneği yeniden yönlendirmeler. Gelen HTTP trafiği için ARR yazılım ilk yönlendirilmesi Araç Seti seçili uç noktası otomatik olarak yeniden yapılandırır. Araç Seti ayrıca yeni bir iç uç noktası oluşturan Java sunucunuz dinlemek üzere yapılandırılmış. Uygun rol örneği HTTP trafiği yeniden yönlendirebilir için ARR tarafından kullanılan uç noktayla olmasıdır. Bu şekilde, her rol örneği çok örnekli dağıtımınızdaki Yapışkan oturumları etkinleştirme için ters proxy tüm diğer örnekleri, işlevi görür.

## <a name="notes-about-session-affinity"></a>Oturum benzeşimi ile ilgili notlar
* Oturum benzeşimi işlem öykünücüsü çalışmaz. Ayarları ile derleme işleminin engellemeden işlem öykünücüsü uygulanabilir veya öykünücüsü yürütme işlem, ancak özellik işlem öykünücüsü içinde çalışmaz.

* Oturum benzeşimi etkinleştirme Azure, dağıtımınızdaki tarafından ek yazılım indirilir ve hizmetinizi Azure bulutunda başlatıldığında rolü örneklerinizi yüklü olarak kapladığı disk alanı miktarında artış neden olur.

* Her rol başlatmak için daha uzun sürer.

* Yukarıda belirtildiği gibi trafik rerouter çalışması için dahili uç noktayı, eklenir.


## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse] 

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
