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
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="13a21-103">Merhaba Eclipse için Azure araç seti, Azure oturum yönergeleri</span><span class="sxs-lookup"><span data-stu-id="13a21-103">Azure Sign In Instructions for hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="13a21-104">Hello Azure araç setini Eclipse için Azure hesabınızda oturum için iki yöntem sunar:</span><span class="sxs-lookup"><span data-stu-id="13a21-104">hello Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="13a21-105">**Etkileşimli** - bu yöntemi kullanırken her Azure hesabınızda oturum açışınızda Azure kimlik bilgilerinizi girer.</span><span class="sxs-lookup"><span data-stu-id="13a21-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="13a21-106">**Otomatik** - bu yöntemi kullandığınızda daha sonra kullanabileceğiniz hello kimlik bilgileri dosyası tooautomatically oturum Azure hesabınızda, hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="13a21-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use hello credentials file tooautomatically sign into your Azure account.</span></span>

<span data-ttu-id="13a21-107">Merhaba hello bölümleri aşağıdaki adımlarda anlatmaktadır nasıl toouse her yöntemi.</span><span class="sxs-lookup"><span data-stu-id="13a21-107">hello steps in hello following sections will describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="13a21-108">Azure hesabınızda etkileşimli olarak imzalama</span><span class="sxs-lookup"><span data-stu-id="13a21-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="13a21-109">Merhaba aşağıdaki adımları gösterecektir nasıl Azure kimlik bilgilerinizi el ile girerek toosign Azure içine.</span><span class="sxs-lookup"><span data-stu-id="13a21-109">hello following steps will illustrate how toosign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="13a21-110">Projenizi Eclipse ile açın.</span><span class="sxs-lookup"><span data-stu-id="13a21-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="13a21-111">Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="13a21-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure oturum açma için Eclipse menüsü][I01]

1. <span data-ttu-id="13a21-113">Ne zaman hello **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **etkileşimli**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="13a21-113">When hello **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![İletişim kutusuna oturum][I02]

1. <span data-ttu-id="13a21-115">Ne zaman hello **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="13a21-115">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][I03]

1. <span data-ttu-id="13a21-117">Ne zaman hello **seçin abonelikleri** iletişim kutusu görüntülenirse, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="13a21-117">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Select abonelikleri iletişim kutusu][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="13a21-119">Etkileşimli olarak oturum açıp Azure hesabınızda oturumu imzalama</span><span class="sxs-lookup"><span data-stu-id="13a21-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="13a21-120">Merhaba önceki bölümde hello adımları yapılandırdıktan sonra otomatik olarak her zaman Eclipse yeniden hesabınızda Azure oturumu kapattınız olur.</span><span class="sxs-lookup"><span data-stu-id="13a21-120">After you have configured hello steps in hello previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="13a21-121">Ancak, toosign, Eclipse başlatmadan Azure hesabınızda oturumu istiyorsanız hello aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="13a21-121">However, if you want toosign out of your Azure account without restarting Eclipse, use hello following steps.</span></span>

1. <span data-ttu-id="13a21-122">Eclipse'te, tıklatın **Araçları**, ardından **Azure**ve ardından **oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="13a21-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure oturum kapatma için Eclipse menüsü][L01]

1. <span data-ttu-id="13a21-124">Ne zaman hello **Azure Oturumu Kapat** iletişim kutusu görüntülenirse, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="13a21-124">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![İletişim kutusunu oturum][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a><span data-ttu-id="13a21-126">Azure hesabınızda oturum otomatik olarak imzalama ve bir kimlik bilgileri oluşturma toouse hello gelecekteki dosya</span><span class="sxs-lookup"><span data-stu-id="13a21-126">Signing into your Azure account automatically and creating a credentials file toouse in hello future</span></span>

<span data-ttu-id="13a21-127">Merhaba aşağıdaki adımlar, hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="13a21-127">hello following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="13a21-128">Otomatik olarak bu adımları, Eclipse tamamladıktan sonra size içine Azure her zaman kullanım hello kimlik bilgileri dosyası tooautomatically oturum projenizi açın.</span><span class="sxs-lookup"><span data-stu-id="13a21-128">Once you have completed these steps, Eclipse will automatically use hello credentials file tooautomatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="13a21-129">Projenizi Eclipse ile açın.</span><span class="sxs-lookup"><span data-stu-id="13a21-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="13a21-130">Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="13a21-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure oturum açma için Eclipse menüsü][A01]

1. <span data-ttu-id="13a21-132">Ne zaman hello **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **otomatik**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="13a21-132">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![İletişim kutusuna oturum][A02]

1. <span data-ttu-id="13a21-134">Ne zaman hello **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="13a21-134">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A03]

1. <span data-ttu-id="13a21-136">Ne zaman hello **kimlik doğrulama dosyalarını oluşturmak** iletişim kutusu görüntülenirse, toouse istediğiniz hedef dizininizi seçin ve ardından select hello abonelikleri **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="13a21-136">When hello **Create authentication files** dialog box appears, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A04]

1. <span data-ttu-id="13a21-138">Merhaba **hizmet sorumlusu Creatation durumu** iletişim kutusu görüntülenir, tıklatıp dosyalarınızı başarıyla oluşturduktan sonra **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="13a21-138">hello **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Hizmet sorumlusu Creatation durumu iletişim kutusu][A05]

1. <span data-ttu-id="13a21-140">Ne zaman hello **Azure oturum açma** iletişim kutusu görüntülenirse, tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="13a21-140">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A06]

1. <span data-ttu-id="13a21-142">Ne zaman hello **seçin abonelikleri** iletişim kutusu görüntülenirse, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="13a21-142">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Select abonelikleri iletişim kutusu][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="13a21-144">Azure hesabınızda oturumu otomatik olarak imzalanmış imzalarken</span><span class="sxs-lookup"><span data-stu-id="13a21-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="13a21-145">Merhaba önceki bölümde hello adımları yapılandırdıktan sonra hello Azure Araç Seti otomatik olarak, her zaman Eclipse yeniden Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="13a21-145">After you have configured hello steps in hello previous section, hello Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="13a21-146">Ancak, toosign Azure hesabınızda out ve otomatik olarak, aşağıdaki adımları kullanın hello kaydınızı hello Azure Araç Seti engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13a21-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, use hello following steps.</span></span>

1. <span data-ttu-id="13a21-147">Eclipse'te, tıklatın **Araçları**, ardından **Azure**ve ardından **oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="13a21-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure oturum kapatma için Eclipse menüsü][L01]

1. <span data-ttu-id="13a21-149">Ne zaman hello **Azure Oturumu Kapat** iletişim kutusu görüntülenirse, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="13a21-149">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![İletişim kutusunu oturum][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="13a21-151">Önceden oluşturduğunuz bir kimlik bilgileri dosyası kullanılarak otomatik olarak Azure hesabınızda imzalama</span><span class="sxs-lookup"><span data-stu-id="13a21-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="13a21-152">Eclipse kullanırken Azure oturumunu oturum açarsanız, Eclipse toouse otomatik olarak Azure hesabınız oturum önce oluşturmuş olduğunuz bir kimlik bilgileri dosyası tooreconfigure hello Azure Araç Seti gerekir.</span><span class="sxs-lookup"><span data-stu-id="13a21-152">If you sign out of Azure when you are using Eclipse, you will need tooreconfigure hello Azure Toolkit for Eclipse toouse a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="13a21-153">Merhaba aşağıdaki adımları hello Azure Araç Seti toouse nasıl yapılandıracağınız varolan kimlik bilgileri dosyasını anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="13a21-153">hello following steps will walk you through configuring hello Azure Toolkit toouse an existing credentials file.</span></span>

1. <span data-ttu-id="13a21-154">Projenizi Eclipse ile açın.</span><span class="sxs-lookup"><span data-stu-id="13a21-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="13a21-155">Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="13a21-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure oturum açma için Eclipse menüsü][A01]

1. <span data-ttu-id="13a21-157">Ne zaman hello **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **otomatik**ve ardından **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="13a21-157">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![İletişim kutusuna oturum][A02]

1. <span data-ttu-id="13a21-159">Ne zaman hello **kimliği doğrulanmış Dosya Seç** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz bir kimlik bilgileri dosyasını seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="13a21-159">When hello **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![İletişim kutusuna oturum][A08]

1. <span data-ttu-id="13a21-161">Ne zaman hello **Azure oturum açma** iletişim kutusu görüntülenirse, tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="13a21-161">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A06]

1. <span data-ttu-id="13a21-163">Ne zaman hello **seçin abonelikleri** iletişim kutusu görüntülenirse, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="13a21-163">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Select abonelikleri iletişim kutusu][A07]

## <a name="see-also"></a><span data-ttu-id="13a21-165">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="13a21-165">See Also</span></span>
<span data-ttu-id="13a21-166">Java IDE hello Azure araç takımları hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="13a21-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="13a21-167">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="13a21-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="13a21-168">[Yeni hello Eclipse için Azure Araç Seti nedir]</span><span class="sxs-lookup"><span data-stu-id="13a21-168">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="13a21-169">[Yükleme hello Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="13a21-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="13a21-170">*Hello Azure araç setini Eclipse (Bu makalede) için oturum yönergeleri*</span><span class="sxs-lookup"><span data-stu-id="13a21-170">*Sign In Instructions for hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="13a21-171">[Eclipse Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="13a21-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="13a21-172">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="13a21-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="13a21-173">[Yeni hello Intellij için Azure Araç Seti nedir]</span><span class="sxs-lookup"><span data-stu-id="13a21-173">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="13a21-174">[Yükleme hello Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="13a21-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="13a21-175">[Merhaba Intellij için Azure Araç Seti içinde oturum yönergeleri]</span><span class="sxs-lookup"><span data-stu-id="13a21-175">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="13a21-176">[Intellij Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="13a21-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="13a21-177">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="13a21-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

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
