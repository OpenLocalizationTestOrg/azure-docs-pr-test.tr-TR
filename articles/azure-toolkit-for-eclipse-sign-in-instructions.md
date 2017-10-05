---
title: "Yönergeler için Azure araç setini Eclipse oturum | Microsoft Docs"
description: "Eclipse için Azure Araç Seti kullanarak Microsoft Azure'da oturum öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Azure oturum açma Eclipse için Azure Araç Seti için yönergeler

Eclipse için Azure Araç Seti Azure hesabınızda oturum için iki yöntem sunar:

  * **Etkileşimli** - bu yöntemi kullanırken her Azure hesabınızda oturum açışınızda Azure kimlik bilgilerinizi girer.
  * **Otomatik** - bu yöntemi kullanırken geçmesi kimlik bilgileri dosyası otomatik olarak Azure hesabınızda oturum için kullanabileceğiniz, hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturur.

Aşağıdaki bölümlerdeki adımları her yönteminin nasıl kullanılacağını anlatmaktadır.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Azure hesabınızda etkileşimli olarak imzalama

Aşağıdaki adımlar, Azure kimlik bilgilerinizi el ile girerek Azure'da oturum nasıl çalışılacağını.

1. Projenizi Eclipse ile açın.

1. Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.

   ![Azure oturum açma için Eclipse menüsü][I01]

1. Zaman **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **etkileşimli**ve ardından **oturum**.

   ![İletişim kutusuna oturum][I02]

1. Zaman **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][I03]

1. Zaman **seçin abonelikleri** iletişim kutusu görüntülenirse, kullanın ve ardından istediğiniz abonelikleri seçin **Tamam**.

   ![Select abonelikleri iletişim kutusu][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Etkileşimli olarak oturum açıp Azure hesabınızda oturumu imzalama

Önceki bölümdeki adımları yapılandırdıktan sonra otomatik olarak her zaman Eclipse yeniden hesabınızda Azure oturumu kapattınız olur. Ancak, Eclipse başlatmadan dışında Azure hesabınızda oturum istiyorsanız, aşağıdaki adımları kullanın.

1. Eclipse'te, tıklatın **Araçları**, ardından **Azure**ve ardından **oturum kapatma**.

   ![Azure oturum kapatma için Eclipse menüsü][L01]

1. Zaman **Azure Oturumu Kapat** iletişim kutusu görüntülenirse, tıklatın **Evet**.

   ![İletişim kutusunu oturum][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a>Azure hesabınızda oturum otomatik olarak imzalama ve kimlik bilgileri dosyası oluşturma gelecekte kullanmak için

Aşağıdaki adımlar, hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturmada size yol gösterir. Bu adımları tamamladıktan sonra Eclipse projenizin her açtığınızda Azure'da otomatik olarak oturum için kimlik bilgileri dosyası otomatik olarak kullanır.

1. Projenizi Eclipse ile açın.

1. Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.

   ![Azure oturum açma için Eclipse menüsü][A01]

1. Zaman **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **otomatik**ve ardından **yeni**.

   ![İletişim kutusuna oturum][A02]

1. Zaman **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][A03]

1. Zaman **kimlik doğrulama dosyalarını oluşturmak** iletişim kutusu görüntülenirse, kullanma, hedef dizininizi seçin ve ardından istediğiniz abonelikleri seçin **Başlat**.

   ![Azure Oturum Açma İletişim Kutusu][A04]

1. **Hizmet sorumlusu Creatation durumu** iletişim kutusu görüntülenir, tıklatıp dosyalarınızı başarıyla oluşturduktan sonra **Tamam**.

   ![Hizmet sorumlusu Creatation durumu iletişim kutusu][A05]

1. Zaman **Azure oturum açma** iletişim kutusu görüntülenirse, tıklatın **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][A06]

1. Zaman **seçin abonelikleri** iletişim kutusu görüntülenirse, kullanın ve ardından istediğiniz abonelikleri seçin **Tamam**.

   ![Select abonelikleri iletişim kutusu][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Azure hesabınızda oturumu otomatik olarak imzalanmış imzalarken

Önceki bölümdeki adımları yapılandırdıktan sonra Azure Araç Seti otomatik olarak, her zaman Eclipse yeniden Azure hesabınızda oturum açın. Ancak, dışında Azure hesabınızda oturum açın ve Azure Araç Seti otomatik olarak oturum açma engellemek için aşağıdaki adımları kullanın.

1. Eclipse'te, tıklatın **Araçları**, ardından **Azure**ve ardından **oturum kapatma**.

   ![Azure oturum kapatma için Eclipse menüsü][L01]

1. Zaman **Azure Oturumu Kapat** iletişim kutusu görüntülenirse, tıklatın **Evet**.

   ![İletişim kutusunu oturum][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Önceden oluşturduğunuz bir kimlik bilgileri dosyası kullanılarak otomatik olarak Azure hesabınızda imzalama

Eclipse kullanırken Azure oturumunu oturum açarsanız, otomatik olarak Azure hesabınız oturum önce oluşturmuş olduğunuz bir kimlik bilgileri dosyası kullanmak Eclipse için Azure Araç Seti yeniden yapılandırmanız gerekir. Aşağıdaki adımlar varolan kimlik bilgileri dosyasını kullanmak için Azure Araç Seti yapılandırırken size yol gösterir.

1. Projenizi Eclipse ile açın.

1. Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.

   ![Azure oturum açma için Eclipse menüsü][A01]

1. Zaman **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **otomatik**ve ardından **Gözat**.

   ![İletişim kutusuna oturum][A02]

1. Zaman **kimliği doğrulanmış Dosya Seç** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz bir kimlik bilgileri dosyasını seçin ve ardından **seçin**.

   ![İletişim kutusuna oturum][A08]

1. Zaman **Azure oturum açma** iletişim kutusu görüntülenirse, tıklatın **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][A06]

1. Zaman **seçin abonelikleri** iletişim kutusu görüntülenirse, kullanın ve ardından istediğiniz abonelikleri seçin **Tamam**.

   ![Select abonelikleri iletişim kutusu][A07]

## <a name="see-also"></a>Ayrıca Bkz.
Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:

* [Eclipse için Azure Araç Seti]
  * [Eclipse için Azure Araç Seti Yenilikleri]
  * [Eclipse için Azure Araç Setini Yükleme]
  * *Yönergeler için Azure araç setini Eclipse (Bu makalede) Kaydol*
  * [Eclipse Azure'da Hello World Web uygulaması oluşturun]
* [IntelliJ için Azure Araç Seti]
  * [IntelliJ için Azure Araç Seti Yenilikleri]
  * [IntelliJ için Azure Araç Setini Yükleme]
  * [IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]
  * [Intellij Azure'da Hello World Web uygulaması oluşturun]

Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Eclipse için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[IntelliJ için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
