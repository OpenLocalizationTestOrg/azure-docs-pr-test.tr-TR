---
title: "Azure hizmet uç noktaları"
description: "Azure araç setini Eclipse için Azure hizmet uç noktası ayarlarında açıklar."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a>Azure hizmet uç noktaları
Azure hizmet uç noktaları Azure platformu uygulamanız için dağıtılan ve genel Azure platformu tarafından yönetilen olup olmadığını, Çin ya da özel bir 21Vianet tarafından Azure işletilen belirler. **Hizmet uç noktaları** iletişim kutusu, kullanmak istediğiniz hangi hizmet uç noktaları belirtmenize olanak sağlar. Açmak için **hizmet uç noktaları** Eclipse içinde iletişim tıklatın **penceresi**, tıklatın **Tercihler**, genişletin **Azure**ve ardından **hizmet uç noktaları**. Ayarı **etkin olarak** alanı, hangi Azure hizmet uç noktaları geçerli çalışma alanınızı Azure projelerinde kullanılıp kullanılmayacağını belirler.

Aşağıdaki gösterildiği **hizmet uç noktaları** iletişim.

![][ic719493]

## <a name="to-set-the-service-endpoints"></a>Hizmet uç noktalarına ayarlamak için
İçinde **hizmet uç noktaları** iletişim, aşağıdaki eylemlerden birini gerçekleştirin:

* Genel Azure platformu kullanmak isteyip istemediğinizi **etkin olarak** açılır listesinden, **windowsazure.com** tıklatıp **Tamam**.

* Gelen Çin'de 21Vianet tarafından işletilen Azure kullanmak isteyip istemediğinizi **etkin olarak** açılır listesinden, **windowsazure.cn (Çin)** tıklatıp **Tamam**.

* Özel bir Azure platformu kullanmak istiyorsanız:

  1. **Düzenle**’ye tıklayın.

  2. Size bildiren bir iletişim kutusunu açar, **hizmet uç noktaları** iletişim kapatılacak ve tercih ayarlar dosyasını açılacak. **Tamam** düğmesine tıklayın.

  3. Preferencesets.xml dosyasında, yeni bir oluşturma `preferenceset` öğesi. Bu yeni öğe için oluşturma `name`, `blob`, `management`, `portalURL` ve `publishsettings` özniteliklerini ve değerlerini karşılık gelen kendileri için özel Azure platformunuz için ekleyin. Varolan için sağlanan değerler kullanabilirsiniz `preferenceset` öğeleri şablonları olarak. **Not**: için kullanılan değer `blob` özniteliği URL'deki "blob" metin içermesi gerekir.

  4. Kaydedin ve preferencesets.xml kapatın.

  5. Yeniden **hizmet uç noktaları** iletişim.

  6. Gelen **etkin olarak** etkin ayarlanmış oluşturulur ve tıklatın açılır listesinden, **Tamam**.

  7. Özel, Azure platformu oluşturduktan sonra `preferenceset` öğesini tıklatarak atanmış değerleri değiştirebilir **Düzenle** düğmesini **Services bitiş** iletişim. Birden çok özel Azure platformu da oluşturabilirsiniz `preferenceset` , üzerinde isterse öğeleri.

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse] 

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
