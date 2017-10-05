---
title: "Oturum açma ilişkin yönergeler için Azure Araç Seti Intellij | Microsoft Docs"
description: "Intellij için Azure Araç Seti kullanarak Microsoft Azure oturumu açın öğrenin."
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
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a>Oturum açma Azure Araç Seti için Intellij için yönergeler

Intellij için Azure Araç Seti Azure hesabınızda oturum açmak için iki yöntem sunar:

  * **Etkileşimli**: Azure hesabınıza her oturum açışınızda Azure kimlik bilgilerinizi girin.
  * **Otomatik**: otomatik olarak Azure hesabınızda oturum açmak için kullanabileceğiniz bir kimlik bilgileri dosyası oluşturun.

Aşağıdaki bölümlerde her yöntemin nasıl kullanılacağı açıklanmaktadır.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a>Azure hesabınızda etkileşimli olarak oturum açın

Azure için Azure kimlik bilgilerinizi el ile girerek oturum açmak için aşağıdakileri yapın:

1. Projenizi Intellij Idea ile açın.

2. Tıklatın **Araçları**, işaret **Azure**ve ardından **Azure oturum açma**.

   ![Intellij Azure Oturum Aç komutu][I01]

3. İçinde **Azure oturum açma** penceresinde, seçin **etkileşimli**ve ardından **oturum**.

   ![Azure oturum penceresinde seçili etkileşimli ile][I02]

4. İçinde **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.

   ![Azure oturum açma iletişim penceresi][I03]

5. İçinde **seçin abonelikleri** iletişim kutusunda, kullanmak istediğiniz abonelikleri seçin ve ardından **Tamam**.

   ![Abonelik Seç iletişim kutusu][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Etkileşimli olarak oturum açtıktan sonra dışında Azure hesabınızda oturum açın

Yukarıdaki adımları kullanarak hesabınızı yapılandırdıktan sonra otomatik olarak her zaman Intellij Idea yeniden Azure hesabınıza oturumunuz kapatılacak. Ancak, dışında Azure hesabınızda oturum isteyip istemediğinizi *olmadan* Intellij Idea, yeniden başlatma, aşağıdakileri yapın.

1. Intellij Idea içinde üzerinde **Araçları** menüsündeki **Azure**ve ardından **Azure oturum kapatma**.

   ![Intellij Azure Oturumu Kapat komutu][L01]

2. İçinde **Azure Oturumu Kapat** onay penceresi tıklatın **Evet**.

   ![Azure oturum kapatma onay penceresi][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a>Otomatik olarak Azure hesabınızda oturum açın

Bu bölüm hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturmada size yol gösterir. Bu işlemi tamamladıktan sonra Eclipse için Azure projenizi her açtığınızda otomatik olarak oturum için kimlik bilgileri dosyasını kullanır.

1. Projenizi Intellij Idea ile açın.

2. Üzerinde **Araçları** menüsündeki **Azure**ve ardından **Azure oturum açma**.

   ![Intellij Azure Oturum Aç komutu][A01]

3. İçinde **Azure oturum açma** penceresinde, seçin **otomatik**ve ardından **yeni**.

   ![Azure oturum penceresinde seçili otomatik ile][A02]

4. İçinde **Azure oturum açma iletişim** penceresinde Azure kimlik bilgilerinizi girin ve ardından **oturum**.

   ![Azure oturum açma iletişim penceresi][A03]

5. İçinde **kimlik doğrulama dosyalarını oluşturmak** penceresinde kullanın, hedef dizininizi seçin ve ardından istediğiniz abonelikleri seçin **Başlat**.

   ![Kimlik doğrulama dosyalarını Oluştur penceresi][A04]

6. İçinde **hizmet sorumlusu oluşturma durumu** iletişim kutusu, dosyalarınızı başarıyla oluşturduktan sonra tıklatın **Tamam**.

   ![Hizmet sorumlusu oluşturma durumu iletişim kutusu][A05]

7. İçinde **Azure oturum açma** penceresinde tıklatın **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][A06]

8. İçinde **seçin abonelikleri** iletişim kutusunda, kullanmak istediğiniz abonelikleri seçin ve ardından **Tamam**.

   ![Abonelik Seç iletişim kutusu][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Otomatik olarak oturum açtıktan sonra dışında Azure hesabınızda oturum açın

Yukarıdaki adımları kullanarak hesabınızı yapılandırdıktan sonra Azure Araç Seti otomatik olarak, her zaman Intellij Idea yeniden Azure hesabınızda oturum açtığında. Ancak, dışında Azure hesabınızda oturum açın ve Azure Araç Seti otomatik olarak oturum açma engellemek için aşağıdakileri yapın:

1. Intellij Idea içinde üzerinde **Araçları** menüsündeki **Azure**ve ardından **Azure oturum kapatma**.

   ![Intellij Azure Oturumu Kapat komutu][L01]

2. İçinde **Azure Oturumu Kapat** onay penceresi tıklatın **Evet**.

   ![Azure oturum kapatma onay penceresi][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a>Azure hesabınızda otomatik olarak var olan bir kimlik bilgileri dosyasını kullanarak oturum açın

Intellij Idea kullanırken dışında Azure hesabınızda oturum açarsanız, otomatik olarak hesabına yeniden oturum açmanız varolan kimlik bilgileri dosyasını kullanmanız gerekir. Varolan kimlik bilgileri dosyasını kullanmak Eclipse için Azure Araç Seti yapılandırmak için aşağıdakileri yapın:

1. Projenizi Intellij Idea ile açın.

2. Üzerinde **Araçları** menüsündeki **Azure**ve ardından **Azure oturum açma**.

   ![Intellij Azure Oturum Aç komutu][A01]

3. İçinde **Azure oturum açma** penceresinde, seçin **otomatik**ve ardından **Gözat**.

   ![Azure oturum penceresinde seçili otomatik ile][A02]

4. İçinde **kimlik doğrulaması Dosya Seç** iletişim kutusunda, önceden oluşturulmuş kimlik bilgileri dosyasını seçin ve ardından **seçin**.

   ![Kimlik doğrulama Dosya Seç iletişim kutusu][A08]

5. İçinde **Azure oturum açma** penceresinde tıklatın **oturum**.

   ![Azure oturum penceresinde seçili otomatik ile][A06]

6. İçinde **seçin abonelikleri** iletişim kutusunda, kullanmak istediğiniz abonelikleri seçin ve ardından **Tamam**.

   ![Abonelik Seç iletişim kutusu][A07]

## <a name="next-steps"></a>Sonraki adımlar
Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:

* [Eclipse için Azure Araç Seti]
  * [Eclipse için Azure Araç Seti yenilikleri]
  * [Eclipse için Azure Araç Setini Yükleme]
  * [Eclipse için Azure Araç Seti için oturum açma yönergeleri]
  * [Eclipse'te Azure Hello World web uygulaması oluşturma]
* [IntelliJ için Azure Araç Seti]
  * [Intellij için Azure Araç Seti yenilikleri]
  * [IntelliJ için Azure Araç Setini Yükleme]
  * *Oturum açma ilişkin yönergeler için Azure Araç Seti Intellij* (Bu makalede)
  * [Intellij Azure'da Hello World web uygulaması oluşturun]

Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md
[Eclipse için Azure Araç Seti için oturum açma yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

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
