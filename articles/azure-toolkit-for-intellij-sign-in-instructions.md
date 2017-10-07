---
title: "aaaSign bileşenini ilişkin yönergeler için hello Azure Araç Seti Intellij | Microsoft Docs"
description: "Nasıl kullanarak Azure tooMicrosoft toosign hello Azure Araç Seti için Intellij öğrenin."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>Oturum açma hello Azure Araç Seti için Intellij için yönergeler

Merhaba Intellij için Azure Araç Seti tooyour Azure hesabı imzalama için iki yöntem sunar:

  * **Etkileşimli**: her oturum açışınızda tooyour Azure hesabı Azure kimlik bilgilerinizi girin.
  * **Otomatik**: tooyour Azure hesabı tooautomatically oturum kullanabileceğiniz bir kimlik bilgileri dosyası oluşturun.

Merhaba aşağıdaki bölümlerde nasıl toouse her yöntemi.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>Tooyour Azure hesabı etkileşimli olarak oturum açın

Azure kimlik bilgilerinizi, el ile girerek tooAzure toosign hello aşağıdaki:

1. Projenizi Intellij Idea ile açın.

2. Tıklatın **Araçları**, çok noktası**Azure**ve ardından **Azure oturum açma**.

   ![Merhaba Intellij Azure Oturum Aç komutu][I01]

3. Merhaba, **Azure oturum açma** penceresinde, seçin **etkileşimli**ve ardından **oturum**.

   ![Hello Azure oturum penceresinde seçili etkileşimli ile][I02]

4. Merhaba, **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.

   ![Hello Azure oturum açma iletişim penceresi][I03]

5. Merhaba, **seçin abonelikleri** iletişim kutusu, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.

   ![Merhaba abonelikleri seçin iletişim kutusu][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Etkileşimli olarak oturum açtıktan sonra dışında Azure hesabınızda oturum açın

Önceki adımları hello kullanarak hesabınızı yapılandırdıktan sonra otomatik olarak her zaman Intellij Idea yeniden Azure hesabınıza oturumunuz kapatılacak. Ancak, Azure hesabınızı dışında toosign istiyorsanız *olmadan* Intellij Idea yeniden hello aşağıdaki.

1. Merhaba üzerinde Intellij Idea içinde **Araçları** menüsünde çok noktası**Azure**ve ardından **Azure oturum kapatma**.

   ![Merhaba Intellij Azure Sign Out komutu][L01]

2. Merhaba, **Azure Oturumu Kapat** onay penceresi tıklatın **Evet**.

   ![Hello Azure oturumu kapat onay penceresi][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Tooyour Azure hesabı otomatik olarak oturum aç

Bu bölüm hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturmada size yol gösterir. Bu işlemi tamamladıktan sonra Eclipse kullanır hello kimlik bilgileri dosyası tooautomatically oturum size tooAzure her zaman projenizi açın.

1. Projenizi Intellij Idea ile açın.

2. Merhaba üzerinde **Araçları** menüsünde çok noktası**Azure**ve ardından **Azure oturum açma**.

   ![Merhaba Intellij Azure Oturum Aç komutu][A01]

3. Merhaba, **Azure oturum açma** penceresinde, seçin **otomatik**ve ardından **yeni**.

   ![Hello Azure oturum penceresinde seçili otomatik ile][A02]

4. Merhaba, **Azure oturum açma iletişim** penceresinde Azure kimlik bilgilerinizi girin ve ardından **oturum**.

   ![Hello Azure oturum açma iletişim penceresi][A03]

5. Merhaba, **kimlik doğrulama dosyalarını oluşturmak** penceresinde, toouse istediğiniz hedef dizininizi seçin ve ardından select hello abonelikleri **Başlat**.

   ![Merhaba kimlik doğrulama dosyalarını Oluştur penceresi][A04]

6. Merhaba, **hizmet sorumlusu oluşturma durumu** iletişim kutusu, dosyalarınızı başarıyla oluşturduktan sonra tıklatın **Tamam**.

   ![Merhaba hizmet sorumlusu oluşturma durumu iletişim kutusu][A05]

7. Merhaba, **Azure oturum açma** penceresinde, tıklatın **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][A06]

8. Merhaba, **seçin abonelikleri** iletişim kutusu, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.

   ![Merhaba abonelikleri seçin iletişim kutusu][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Otomatik olarak oturum açtıktan sonra dışında Azure hesabınızda oturum açın

Önceki adımları hello kullanarak hesabınızı yapılandırdıktan sonra hello Azure araç seti, otomatik olarak tooyour Azure hesabı her zaman Intellij Idea yeniden imzalar. Ancak, toosign out Azure hesabınızı ve hello Azure Araç Seti engellemek, otomatik olarak oturum açmaya, izleyen hello:

1. Merhaba üzerinde Intellij Idea içinde **Araçları** menüsünde çok noktası**Azure**ve ardından **Azure oturum kapatma**.

   ![Merhaba Intellij Azure Sign Out komutu][L01]

2. Merhaba, **Azure Oturumu Kapat** onay penceresi tıklatın **Evet**.

   ![Hello Azure oturumu kapat onay penceresi][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>Tooyour içinde varolan kimlik bilgileri dosyasını kullanarak Azure hesabı otomatik olarak oturum.

Intellij Idea kullanırken dışında Azure hesabınızda oturum açarsanız, geri toohello hesabında bir var olan kimlik bilgileri dosyası tooautomatically oturum kullanmanız gerekir. tooconfigure Merhaba Azure araç setini Eclipse toouse varolan bir kimlik bilgileri dosyasını hello aşağıdaki:

1. Projenizi Intellij Idea ile açın.

2. Merhaba üzerinde **Araçları** menüsünde çok noktası**Azure**ve ardından **Azure oturum açma**.

   ![Merhaba Intellij Azure Oturum Aç komutu][A01]

3. Merhaba, **Azure oturum açma** penceresinde, seçin **otomatik**ve ardından **Gözat**.

   ![Hello Azure oturum penceresinde seçili otomatik ile][A02]

4. Merhaba, **kimlik doğrulaması Dosya Seç** iletişim kutusunda, önceden oluşturulmuş kimlik bilgileri dosyasını seçin ve ardından **seçin**.

   ![Merhaba kimlik doğrulaması Dosya Seç iletişim kutusu][A08]

5. Merhaba, **Azure oturum açma** penceresinde, tıklatın **oturum**.

   ![Hello Azure oturum penceresinde seçili otomatik ile][A06]

6. Merhaba, **seçin abonelikleri** iletişim kutusu, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.

   ![Merhaba abonelikleri seçin iletişim kutusu][A07]

## <a name="next-steps"></a>Sonraki adımlar
Java IDE hello Azure araç takımları hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:

* [Eclipse için Azure Araç Seti]
  * [Merhaba Eclipse için Azure Araç Seti yenilikleri]
  * [Yükleme hello Eclipse için Azure Araç Seti]
  * [Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]
  * [Eclipse'te Azure Hello World web uygulaması oluşturma]
* [IntelliJ için Azure Araç Seti]
  * [Merhaba Intellij için Azure Araç Seti yenilikleri]
  * [Yükleme hello Intellij için Azure Araç Seti]
  * *Oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij* (Bu makalede)
  * [Intellij Azure'da Hello World web uygulaması oluşturun]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ./azure-toolkit-for-intellij-installation.md
[Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Merhaba Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Merhaba Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
