---
title: "Büyük dağıtımlar dağıtma"
description: "Eclipse için Azure Araç Seti kullanarak büyük dağıtımlar dağıtmayı öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: e12e379e2b6727653e2377b1760c3745596a1e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploying-large-deployments"></a>Büyük dağıtımlar dağıtma
Dağıtımınız varsayılan approot klasöründe bulunması için çok büyük ise, JDK için yerel depolama kaynağı dağıtım kök klasör olarak kullanabilirsiniz ve uygulama sunucusu.

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a>Yerel depolama kaynağı büyük dağıtımlar için dağıtım kök klasör olarak kullanmak için
1. Yeni bir yerel depolama kaynağı oluşturun. Kaynağın adını belirttiğinizin önemi yoktur. Depolama kaynaklarını rol düzeyinde tanımlanır. İçinden oluşturduğunuz yeni bir yerel depolama kaynağı yerel depolama yapılandırma iletişim erişmek için en hızlı aşağıdaki adımları kullanarak yoludur: rolünde sağ **Proje Gezgini** Görünüm (Azure projenizi genişletin düğüm) rolü görmüyorsanız, tıklatın **Azure**ve ardından **yerel depolama**. İçinde **yerel depolama** iletişim kutusunda, tıklatın **Ekle** yeni bir yerel depolama kaynağı oluşturmak için.

2. İstenen boyuta (karşılaşabileceğinizi herhangi bir şey daha az aynı dosyanın boyutu sorunları approot neden olabilir) en az 2048 MB ayarlayın.

3. Emin **rol örneği geri dönüştürüldüğünde içeriği temiz** denetlenir; bu dağıtımın başlangıç mantığı rol örneği olduğunda çakışmaları kaynak önceden var olan dosyalarla engellenmesine yardımcı olur geri dönüştürüldü.

4. Emin **kaynağın dizin yolu dağıtımdan sonra Depolama ortam değişkeni** değeri dizeye ayarlayın **DEPLOYROOT**. Yerel depolama kaynak iletişim aşağıdakine benzer görünecektir.

   ![][ic667943]

Alternatif olarak, kullanırsanız **DEPLOYROOT** olarak *adı* yerel kaynağınız ve, otomatik olarak oluşturulan ortam değişkeni adı değiştirmeyin (hangi şekilde ayarlanacak **DEPLOYROOT_ YOL** bu durumda), uygulamanız için çalışması.

Yerel depolama kaynağı oluşturma hakkında daha fazla bilgi bulunabilir [yerel depolama özellikleri][Local storage properties].

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse] 

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
