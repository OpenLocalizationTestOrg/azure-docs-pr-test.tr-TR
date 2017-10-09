---
title: "Visual Studio ile özel Azure Bulutları aaaAccessing | Microsoft Docs"
description: "Nasıl tooaccess özel bulut kaynaklarına Visual Studio kullanarak öğrenin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Özel Azure bulut Visual Studio ile erişme
Varsayılan olarak, Visual Studio genel Azure bulut REST uç noktalarını destekler. Bu konuda, nasıl toouse, özel bulut bilgi sertifika tooaccess - kullanıcının ve etkileşim - hello Visual Studio'dan özel bulut.

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a>Visual Studio'da tooaccess özel bir Azure bulut
1. Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885) hello özel bulut için yayımlama ayarları dosyanız indirin veya yayımlama ayarları dosyası için yöneticinize başvurun. Merhaba ortak sürümünde Azure, bu bağlantı toodownload hello [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/). (Merhaba indirilen dosya uzantısına sahip olmalıdır `.publishsettings`)

1. Açık Visual Studio

1. İçinde **Sunucu Gezgini**, sağ hello **Azure** düğümü ve hello bağlam menüsünden seçin **yönetin ve filtre abonelikleri**.
   
    ![Abonelikleri komutu yönetme](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. Merhaba, **Microsoft Azure Aboneliklerini Yönet** iletişim, select hello **sertifikaları** sekmesini tıklatın ve ardından **alma**.
   
    ![Azure sertifikaları alma](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. Merhaba, **alma Microsoft Azure abonelikleri** iletişim kutusunda **Gözat**.

    ![Gözat düğmesi hello alma Microsoft Azure abonelikleri iletişim](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. Merhaba, **açık** iletişim kutusunda, Gözat toohello, kaydedilen hello yayımlama ayarları dosyası, select hello burada dosya dizin ve ardından **açık**.

    ![Merhaba yayımlama ayarları dosyasını seçin](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Zaman toohello döndürülen **alma Microsoft Azure abonelikleri** iletişim kutusunda **alma**.

    ![Merhaba yayımlama ayarları dosyasını içeri aktarma](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    Merhaba sertifikaları hello yayımlama ayarları dosyası Visual Studio'ya aktarılır ve şimdi, özel bulut kaynakları ile etkileşim kurabilirsiniz.
   
## <a name="next-steps"></a>Sonraki adımlar
- [Yayımlama tooan Visual Studio'dan Azure bulut hizmeti](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [Nasıl yapılır: indirme ve içeri aktarma yayımlama ayarları ve abonelik bilgileri](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)
