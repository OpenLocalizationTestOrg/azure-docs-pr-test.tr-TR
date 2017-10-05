---
title: "Java için Azure kitaplıkları paketine Eclipse'te Javadoc içerik görüntüleme"
description: "Eclipse'te Azure kitaplıkları Javadoc içeriği görüntülemek nasıl."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b44deb773b2159cba1d5d957455409f10fc49334
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a>Java için Azure kitaplıkları paketine Eclipse'te Javadoc içerik görüntüleme
Javadoc içerik Java için Azure kitaplıkları için Java için Azure kitaplıkları Javadoc içeriği ilişkilendirerek Eclipse ortamınızda görüntülenebilir. Aşağıdaki adımlar bu işlevselliğinin Eclipse içinde nasıl kullanılacağını gösterir.

Bu yordam, Java için Azure kitaplığı yapı yolunuzu eklemiş varsayar.

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a>Java için Azure kitaplıkları için Eclipse'te Javadoc içeriği görüntülemek için
* Eclipse'nın Proje Gezgini içinde içinde **başvurulan kitaplıkları** bölüm projenizi bağlam menüsü için Azure kitaplığı Java JAR için açın. Örneğin, **microsoft-windowsazure-API-0.1.0.jar** (sürüm numarası olabilir farklı, yüklediğiniz hangi sürümünün bağımlı).

* **Özellikler**'e tıklayın.

* İçinde **özellikleri** iletişim kutusunda, sol bölmedeki tıklatın **Javadoc konumu**. **Javadoc konumu** iletişim kutusu gösterilir.

* Belirleyebileceğiniz bir **Javadoc URL**, veya bir **Javadoc arşivde**.

   * Belirtmeyi seçerseniz bir **Javadoc URL**, URL'ler gibi kullandığınız **http://dl.windowsazure.com/javadoc** veya **http://dl.windowsazure.com/storage/javadoc**.

   * Kullanmayı seçerseniz **Javadoc arşivde**, dış bir dosya veya bir çalışma dosyası belirtebilirsiniz.

   Seçiminizi yapın ve Gözat/gerektiğinde doğrulayın. Aşağıdaki örnek Java için Azure kitaplıkları karşılık gelen Javadoc adlı bir klasöre yerel olarak indirdiği JAR ilişkilendirir **c:\MyAzureJARs**.

   ![][ic553487]

* *İsteğe bağlı adım*: tıklatın **doğrulamak**. Javadoc JAR olası sorunlar burada gösterilemedi.

* **Tamam** düğmesine tıklayın.

Kitaplıkla ilişkilendirilmiş sonra Eclipse IDE içinde Javadoc içeriği görüntülemelidir. Örneğin, varsa `blob` türü tanımlı `CloudBlockBlob` kodunuzu içinde yazarken görüntülenen Javadoc içeriğine bir örnek verilmiştir `blob.acquireLease` kod:

![][ic553488]

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

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
