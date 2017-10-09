---
title: "aaaAzure hizmet uç noktaları"
description: "Merhaba Eclipse için Azure Araç Seti Hello Azure hizmet uç noktası ayarlarını açıklar."
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
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a>Azure hizmet uç noktaları
Azure hizmet uç noktaları Azure platformu, uygulamanızın hello genel Azure platformu tarafından yönetilen dağıtılan tooand olup Çin ya da özel bir 21Vianet tarafından Azure işletilen belirler. Merhaba **hizmet uç noktaları** iletişim kutusu, uç noktaları toouse istediğiniz hizmet toospecify sağlar. tooopen hello **hizmet uç noktaları** Eclipse içinde iletişim tıklatın **penceresi**, tıklatın **Tercihler**, genişletin **Azure**ve ardından **Hizmet uç noktaları**. Ayar hello **etkin olarak** alanı, hangi Azure hizmet uç noktaları hello için kullanılacak Azure geçerli çalışma alanınızda projeleri belirler.

Merhaba aşağıdaki gösterir hello **hizmet uç noktaları** iletişim.

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>tooset hello hizmet uç noktaları
Merhaba, **hizmet uç noktaları** iletişim, Eylemler aşağıdaki hello birini gerçekleştirin:

* Toouse hello genel Azure platformundan, hello isteyip istemediğinizi **etkin olarak** açılır listesinden, **windowsazure.com** tıklatıp **Tamam**.

* Azure hello gelen Çin'de, 21Vianet tarafından işletilen toouse isteyip istemediğinizi **etkin olarak** açılır listesinden, **windowsazure.cn (Çin)** tıklatıp **Tamam**.

* Toouse özel Azure platformu istiyorsanız:

  1. **Düzenle**’ye tıklayın.

  2. Bu hello bildiren bir iletişim kutusu açılır **hizmet uç noktaları** iletişim kapatılacak ve hello tercih ayarlar dosyasını açılabilir. **Tamam** düğmesine tıklayın.

  3. Merhaba preferencesets.xml dosyasında, yeni bir oluşturma `preferenceset` öğesi. Bu yeni öğe için oluşturma `name`, `blob`, `management`, `portalURL` ve `publishsettings` özniteliklerini ve değerlerini tooyour özel Azure platformu karşılık gelen bunları ekleyin. Merhaba varolan için sağlanan hello değerleri kullanabilirsiniz `preferenceset` öğeleri şablonları olarak. **Not**: Merhaba hello için kullanılan değer `blob` özniteliği hello metin "blob" Merhaba URL'de içermesi gerekir.

  4. Kaydedin ve preferencesets.xml kapatın.

  5. Merhaba yeniden **hizmet uç noktaları** iletişim.

  6. Merhaba gelen **etkin olarak** açılır listesinde, select hello etkin ayarlanmış oluşturulur ve tıklatın **Tamam**.

  7. Özel, Azure platformu oluşturduktan sonra `preferenceset` öğesi hello tıklayarak hello atanan değerlerin tooit değiştirebilirsiniz **Düzenle** hello düğmesini **Services bitiş** iletişim. Birden çok özel Azure platformu da oluşturabilirsiniz `preferenceset` , üzerinde isterse öğeleri.

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse] 

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
