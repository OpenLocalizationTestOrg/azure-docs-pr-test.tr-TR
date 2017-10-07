---
title: "Merhaba Java için Azure kitaplıkları paketi için Eclipse Javadoc içeriği aaaDisplaying"
description: "Nasıl toodisplay hello Javadoc içerik eclipse'te hello Azure kitaplıkları."
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
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a>Merhaba Java için Azure kitaplıkları paketi için Eclipse'te Javadoc içerik görüntüleme
Merhaba Javadoc içerik hello Java için Azure kitaplıkları için Eclipse ortamınızda hello Javadoc içerik toohello Java için Azure kitaplıkları ilişkilendirerek görüntülenebilir. Merhaba aşağıdaki adımlarda size yol gösterecektir toouse Eclipse içinde bu işlev.

Bu yordam, Java tooyour derleme yolu için hello Azure kitaplığı eklemiş varsayar.

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a>toodisplay eclipse'te Javadoc içerik hello Java için Azure kitaplıkları için
* Merhaba de Eclipse'nın Proje Gezgini'nde içinde **başvurulan kitaplıkları** projenizin bölümü, açık hello bağlam menüsü hello JAR Java için Azure kitaplığı. Örneğin, **microsoft-windowsazure-API-0.1.0.jar** (Merhaba sürüm numarası farklı, yüklediğiniz hangi sürümünün bağımlı olabilir).

* **Özellikler**'e tıklayın.

* Merhaba içinde **özellikleri** hello sol bölmesinde, iletişim tıklatın **Javadoc konumu**. Merhaba **Javadoc konumu** iletişim kutusu gösterilir.

* Belirleyebileceğiniz bir **Javadoc URL**, veya bir **Javadoc arşivde**.

   * Toospecify seçerseniz bir **Javadoc URL**, hello URL'ler gibi kullandığınız **http://dl.windowsazure.com/javadoc** veya **http://dl.windowsazure.com/storage/javadoc**.

   * Toouse seçerseniz **Javadoc arşivde**, dış bir dosya veya bir çalışma dosyası belirtebilirsiniz.

   Seçiminizi yapın ve Gözat/gerektiğinde doğrulayın. Merhaba aşağıdaki örnek hello Java için Azure kitaplıkları karşılık gelen Javadoc boyunca JAR indirilen yerel olarak adlı tooa klasör hello ile ilişkilendirir **c:\MyAzureJARs**.

   ![][ic553487]

* *İsteğe bağlı adım*: tıklatın **doğrulamak**. Olası sorunlar hello Javadoc JAR burada gösterilemedi.

* **Tamam** düğmesine tıklayın.

Merhaba Kitaplıkla ilişkilendirilmiş sonra hello Javadoc içerik Eclipse IDE içinde görüntülemelidir. Örneğin, varsa `blob` türü tanımlı `CloudBlockBlob` yazarken görüntülenen Javadoc içeriğine bir örnek kodunuzu içinde hello aşağıdadır `blob.acquireLease` kod:

![][ic553488]

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

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
