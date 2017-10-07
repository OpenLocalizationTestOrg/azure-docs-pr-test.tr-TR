---
title: "aaaDeploying büyük dağıtımlar"
description: "Eclipse için Azure Araç Seti kullanarak toodeploy büyük dağıtımları nasıl hello öğrenin."
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
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a>Büyük dağıtımlar dağıtma
Dağıtımınızı hello varsayılan approot klasöründe yer alan çok büyük toobe ise, JDK için yerel depolama kaynağı hello dağıtım kök klasör olarak kullanabilirsiniz ve uygulama sunucusu.

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>toouse büyük dağıtımlar için hello dağıtım kök klasör olarak yerel depolama kaynağı
1. Yeni bir yerel depolama kaynağı oluşturun. Merhaba hello kaynağın adını belirttiğinizin önemi yoktur. Depolama kaynaklarını hello rol düzeyinde tanımlanır. Merhaba içinden oluşturduğunuz yeni bir yerel depolama kaynağı hızlı şekilde tooaccess hello yerel depolama yapılandırması iletişim kutusunda, aşağıdaki adımları hello kullanmaktır: hello sağ hello rolünde **Proje Gezgini** Görünüm (genişletin, Azure projesi düğümü) hello rolü görmüyorsanız, tıklatın **Azure**ve ardından **yerel depolama**. Merhaba içinde **yerel depolama** iletişim kutusunda, tıklatın **Ekle** toocreate yeni bir yerel depolama kaynağı.

2. Set hello istenen boyutu tooat (hiçbir şey daha az hello aynı dosya boyutu sorunlara neden karşılaşabileceğinizi hello approot) en az 2048 MB.

3. Emin **hello rol örneği geri dönüştürüldüğünde hello içeriği temiz** denetlenir; bu hello dağıtımın başlangıç mantığı çakışmaları hello kaynak önceden var olan dosyaları ile engellenmesine yardımcı olur rolü'ne zaman hello geri dönüştürüldüğünde örneğidir.

4. Bu hello olun **dağıtımdan sonra hello kaynağın dizin yolu ortam değişkeni depolamak** değeri toohello dize ayarlanır **DEPLOYROOT**. Yerel depolama kaynak iletişim benzer toohello aşağıdaki arar.

   ![][ic667943]

Alternatif olarak, kullanırsanız **DEPLOYROOT** hello olarak *adı* yerel kaynağınız ve, hello otomatik olarak oluşturulan ortam değişkeni adı değiştirmeyin (hangi ayarlanacak çok **DEPLOYROOT_PATH** bu durumda), uygulamanız için çalışması.

Yerel depolama kaynağı oluşturma hakkında daha fazla bilgi bulunabilir [yerel depolama özellikleri][Local storage properties].

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse] 

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
