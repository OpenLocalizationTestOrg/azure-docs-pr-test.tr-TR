---
title: "Merhaba Eclipse için Azure Araç Seti için yönergeler de aaaSign | Microsoft Docs"
description: "Eclipse için Azure Araç Seti kullanarak Microsoft Azure içine toosign hello nasıl öğrenin."
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Merhaba Eclipse için Azure araç seti, Azure oturum yönergeleri

Hello Azure araç setini Eclipse için Azure hesabınızda oturum için iki yöntem sunar:

  * **Etkileşimli** - bu yöntemi kullanırken her Azure hesabınızda oturum açışınızda Azure kimlik bilgilerinizi girer.
  * **Otomatik** - bu yöntemi kullandığınızda daha sonra kullanabileceğiniz hello kimlik bilgileri dosyası tooautomatically oturum Azure hesabınızda, hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturur.

Merhaba hello bölümleri aşağıdaki adımlarda anlatmaktadır nasıl toouse her yöntemi.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Azure hesabınızda etkileşimli olarak imzalama

Merhaba aşağıdaki adımları gösterecektir nasıl Azure kimlik bilgilerinizi el ile girerek toosign Azure içine.

1. Projenizi Eclipse ile açın.

1. Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.

   ![Azure oturum açma için Eclipse menüsü][I01]

1. Ne zaman hello **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **etkileşimli**ve ardından **oturum**.

   ![İletişim kutusuna oturum][I02]

1. Ne zaman hello **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][I03]

1. Ne zaman hello **seçin abonelikleri** iletişim kutusu görüntülenirse, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.

   ![Select abonelikleri iletişim kutusu][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Etkileşimli olarak oturum açıp Azure hesabınızda oturumu imzalama

Merhaba önceki bölümde hello adımları yapılandırdıktan sonra otomatik olarak her zaman Eclipse yeniden hesabınızda Azure oturumu kapattınız olur. Ancak, toosign, Eclipse başlatmadan Azure hesabınızda oturumu istiyorsanız hello aşağıdaki adımları kullanın.

1. Eclipse'te, tıklatın **Araçları**, ardından **Azure**ve ardından **oturum kapatma**.

   ![Azure oturum kapatma için Eclipse menüsü][L01]

1. Ne zaman hello **Azure Oturumu Kapat** iletişim kutusu görüntülenirse, tıklatın **Evet**.

   ![İletişim kutusunu oturum][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>Azure hesabınızda oturum otomatik olarak imzalama ve bir kimlik bilgileri oluşturma toouse hello gelecekteki dosya

Merhaba aşağıdaki adımlar, hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturmada size yol gösterir. Otomatik olarak bu adımları, Eclipse tamamladıktan sonra size içine Azure her zaman kullanım hello kimlik bilgileri dosyası tooautomatically oturum projenizi açın.

1. Projenizi Eclipse ile açın.

1. Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.

   ![Azure oturum açma için Eclipse menüsü][A01]

1. Ne zaman hello **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **otomatik**ve ardından **yeni**.

   ![İletişim kutusuna oturum][A02]

1. Ne zaman hello **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][A03]

1. Ne zaman hello **kimlik doğrulama dosyalarını oluşturmak** iletişim kutusu görüntülenirse, toouse istediğiniz hedef dizininizi seçin ve ardından select hello abonelikleri **Başlat**.

   ![Azure Oturum Açma İletişim Kutusu][A04]

1. Merhaba **hizmet sorumlusu Creatation durumu** iletişim kutusu görüntülenir, tıklatıp dosyalarınızı başarıyla oluşturduktan sonra **Tamam**.

   ![Hizmet sorumlusu Creatation durumu iletişim kutusu][A05]

1. Ne zaman hello **Azure oturum açma** iletişim kutusu görüntülenirse, tıklatın **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][A06]

1. Ne zaman hello **seçin abonelikleri** iletişim kutusu görüntülenirse, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.

   ![Select abonelikleri iletişim kutusu][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Azure hesabınızda oturumu otomatik olarak imzalanmış imzalarken

Merhaba önceki bölümde hello adımları yapılandırdıktan sonra hello Azure Araç Seti otomatik olarak, her zaman Eclipse yeniden Azure hesabınızda oturum açın. Ancak, toosign Azure hesabınızda out ve otomatik olarak, aşağıdaki adımları kullanın hello kaydınızı hello Azure Araç Seti engelleyebilirsiniz.

1. Eclipse'te, tıklatın **Araçları**, ardından **Azure**ve ardından **oturum kapatma**.

   ![Azure oturum kapatma için Eclipse menüsü][L01]

1. Ne zaman hello **Azure Oturumu Kapat** iletişim kutusu görüntülenirse, tıklatın **Evet**.

   ![İletişim kutusunu oturum][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Önceden oluşturduğunuz bir kimlik bilgileri dosyası kullanılarak otomatik olarak Azure hesabınızda imzalama

Eclipse kullanırken Azure oturumunu oturum açarsanız, Eclipse toouse otomatik olarak Azure hesabınız oturum önce oluşturmuş olduğunuz bir kimlik bilgileri dosyası tooreconfigure hello Azure Araç Seti gerekir. Merhaba aşağıdaki adımları hello Azure Araç Seti toouse nasıl yapılandıracağınız varolan kimlik bilgileri dosyasını anlatılmaktadır.

1. Projenizi Eclipse ile açın.

1. Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.

   ![Azure oturum açma için Eclipse menüsü][A01]

1. Ne zaman hello **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **otomatik**ve ardından **Gözat**.

   ![İletişim kutusuna oturum][A02]

1. Ne zaman hello **kimliği doğrulanmış Dosya Seç** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz bir kimlik bilgileri dosyasını seçin ve ardından **seçin**.

   ![İletişim kutusuna oturum][A08]

1. Ne zaman hello **Azure oturum açma** iletişim kutusu görüntülenirse, tıklatın **oturum**.

   ![Azure Oturum Açma İletişim Kutusu][A06]

1. Ne zaman hello **seçin abonelikleri** iletişim kutusu görüntülenirse, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.

   ![Select abonelikleri iletişim kutusu][A07]

## <a name="see-also"></a>Ayrıca Bkz.
Java IDE hello Azure araç takımları hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:

* [Eclipse için Azure Araç Seti]
  * [Yeni hello Eclipse için Azure Araç Seti nedir]
  * [Yükleme hello Eclipse için Azure Araç Seti]
  * *Hello Azure araç setini Eclipse (Bu makalede) için oturum yönergeleri*
  * [Eclipse Azure'da Hello World Web uygulaması oluşturun]
* [IntelliJ için Azure Araç Seti]
  * [Yeni hello Intellij için Azure Araç Seti nedir]
  * [Yükleme hello Intellij için Azure Araç Seti]
  * [Merhaba Intellij için Azure Araç Seti içinde oturum yönergeleri]
  * [Intellij Azure'da Hello World Web uygulaması oluşturun]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Merhaba Intellij için Azure Araç Seti içinde oturum yönergeleri]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Yeni hello Eclipse için Azure Araç Seti nedir]: ./azure-toolkit-for-eclipse-whats-new.md
[Yeni hello Intellij için Azure Araç Seti nedir]: ./azure-toolkit-for-intellij-whats-new.md

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
