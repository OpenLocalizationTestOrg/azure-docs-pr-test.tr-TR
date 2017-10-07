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
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="12b23-103">Oturum açma hello Azure Araç Seti için Intellij için yönergeler</span><span class="sxs-lookup"><span data-stu-id="12b23-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="12b23-104">Merhaba Intellij için Azure Araç Seti tooyour Azure hesabı imzalama için iki yöntem sunar:</span><span class="sxs-lookup"><span data-stu-id="12b23-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="12b23-105">**Etkileşimli**: her oturum açışınızda tooyour Azure hesabı Azure kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="12b23-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="12b23-106">**Otomatik**: tooyour Azure hesabı tooautomatically oturum kullanabileceğiniz bir kimlik bilgileri dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="12b23-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="12b23-107">Merhaba aşağıdaki bölümlerde nasıl toouse her yöntemi.</span><span class="sxs-lookup"><span data-stu-id="12b23-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="12b23-108">Tooyour Azure hesabı etkileşimli olarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="12b23-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="12b23-109">Azure kimlik bilgilerinizi, el ile girerek tooAzure toosign hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="12b23-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="12b23-110">Projenizi Intellij Idea ile açın.</span><span class="sxs-lookup"><span data-stu-id="12b23-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="12b23-111">Tıklatın **Araçları**, çok noktası**Azure**ve ardından **Azure oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="12b23-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Merhaba Intellij Azure Oturum Aç komutu][I01]

3. <span data-ttu-id="12b23-113">Merhaba, **Azure oturum açma** penceresinde, seçin **etkileşimli**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="12b23-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Hello Azure oturum penceresinde seçili etkileşimli ile][I02]

4. <span data-ttu-id="12b23-115">Merhaba, **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="12b23-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Hello Azure oturum açma iletişim penceresi][I03]

5. <span data-ttu-id="12b23-117">Merhaba, **seçin abonelikleri** iletişim kutusu, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="12b23-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Merhaba abonelikleri seçin iletişim kutusu][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="12b23-119">Etkileşimli olarak oturum açtıktan sonra dışında Azure hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="12b23-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="12b23-120">Önceki adımları hello kullanarak hesabınızı yapılandırdıktan sonra otomatik olarak her zaman Intellij Idea yeniden Azure hesabınıza oturumunuz kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="12b23-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="12b23-121">Ancak, Azure hesabınızı dışında toosign istiyorsanız *olmadan* Intellij Idea yeniden hello aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="12b23-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="12b23-122">Merhaba üzerinde Intellij Idea içinde **Araçları** menüsünde çok noktası**Azure**ve ardından **Azure oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="12b23-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Merhaba Intellij Azure Sign Out komutu][L01]

2. <span data-ttu-id="12b23-124">Merhaba, **Azure Oturumu Kapat** onay penceresi tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="12b23-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Hello Azure oturumu kapat onay penceresi][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="12b23-126">Tooyour Azure hesabı otomatik olarak oturum aç</span><span class="sxs-lookup"><span data-stu-id="12b23-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="12b23-127">Bu bölüm hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="12b23-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="12b23-128">Bu işlemi tamamladıktan sonra Eclipse kullanır hello kimlik bilgileri dosyası tooautomatically oturum size tooAzure her zaman projenizi açın.</span><span class="sxs-lookup"><span data-stu-id="12b23-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="12b23-129">Projenizi Intellij Idea ile açın.</span><span class="sxs-lookup"><span data-stu-id="12b23-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="12b23-130">Merhaba üzerinde **Araçları** menüsünde çok noktası**Azure**ve ardından **Azure oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="12b23-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Merhaba Intellij Azure Oturum Aç komutu][A01]

3. <span data-ttu-id="12b23-132">Merhaba, **Azure oturum açma** penceresinde, seçin **otomatik**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="12b23-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Hello Azure oturum penceresinde seçili otomatik ile][A02]

4. <span data-ttu-id="12b23-134">Merhaba, **Azure oturum açma iletişim** penceresinde Azure kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="12b23-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Hello Azure oturum açma iletişim penceresi][A03]

5. <span data-ttu-id="12b23-136">Merhaba, **kimlik doğrulama dosyalarını oluşturmak** penceresinde, toouse istediğiniz hedef dizininizi seçin ve ardından select hello abonelikleri **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="12b23-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Merhaba kimlik doğrulama dosyalarını Oluştur penceresi][A04]

6. <span data-ttu-id="12b23-138">Merhaba, **hizmet sorumlusu oluşturma durumu** iletişim kutusu, dosyalarınızı başarıyla oluşturduktan sonra tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="12b23-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Merhaba hizmet sorumlusu oluşturma durumu iletişim kutusu][A05]

7. <span data-ttu-id="12b23-140">Merhaba, **Azure oturum açma** penceresinde, tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="12b23-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A06]

8. <span data-ttu-id="12b23-142">Merhaba, **seçin abonelikleri** iletişim kutusu, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="12b23-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Merhaba abonelikleri seçin iletişim kutusu][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="12b23-144">Otomatik olarak oturum açtıktan sonra dışında Azure hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="12b23-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="12b23-145">Önceki adımları hello kullanarak hesabınızı yapılandırdıktan sonra hello Azure araç seti, otomatik olarak tooyour Azure hesabı her zaman Intellij Idea yeniden imzalar.</span><span class="sxs-lookup"><span data-stu-id="12b23-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="12b23-146">Ancak, toosign out Azure hesabınızı ve hello Azure Araç Seti engellemek, otomatik olarak oturum açmaya, izleyen hello:</span><span class="sxs-lookup"><span data-stu-id="12b23-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="12b23-147">Merhaba üzerinde Intellij Idea içinde **Araçları** menüsünde çok noktası**Azure**ve ardından **Azure oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="12b23-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Merhaba Intellij Azure Sign Out komutu][L01]

2. <span data-ttu-id="12b23-149">Merhaba, **Azure Oturumu Kapat** onay penceresi tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="12b23-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Hello Azure oturumu kapat onay penceresi][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="12b23-151">Tooyour içinde varolan kimlik bilgileri dosyasını kullanarak Azure hesabı otomatik olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="12b23-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="12b23-152">Intellij Idea kullanırken dışında Azure hesabınızda oturum açarsanız, geri toohello hesabında bir var olan kimlik bilgileri dosyası tooautomatically oturum kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="12b23-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="12b23-153">tooconfigure Merhaba Azure araç setini Eclipse toouse varolan bir kimlik bilgileri dosyasını hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="12b23-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="12b23-154">Projenizi Intellij Idea ile açın.</span><span class="sxs-lookup"><span data-stu-id="12b23-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="12b23-155">Merhaba üzerinde **Araçları** menüsünde çok noktası**Azure**ve ardından **Azure oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="12b23-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Merhaba Intellij Azure Oturum Aç komutu][A01]

3. <span data-ttu-id="12b23-157">Merhaba, **Azure oturum açma** penceresinde, seçin **otomatik**ve ardından **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="12b23-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Hello Azure oturum penceresinde seçili otomatik ile][A02]

4. <span data-ttu-id="12b23-159">Merhaba, **kimlik doğrulaması Dosya Seç** iletişim kutusunda, önceden oluşturulmuş kimlik bilgileri dosyasını seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="12b23-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Merhaba kimlik doğrulaması Dosya Seç iletişim kutusu][A08]

5. <span data-ttu-id="12b23-161">Merhaba, **Azure oturum açma** penceresinde, tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="12b23-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Hello Azure oturum penceresinde seçili otomatik ile][A06]

6. <span data-ttu-id="12b23-163">Merhaba, **seçin abonelikleri** iletişim kutusu, toouse istediğiniz ve ardından select hello abonelikleri **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="12b23-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Merhaba abonelikleri seçin iletişim kutusu][A07]

## <a name="next-steps"></a><span data-ttu-id="12b23-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="12b23-165">Next steps</span></span>
<span data-ttu-id="12b23-166">Java IDE hello Azure araç takımları hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="12b23-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="12b23-167">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="12b23-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="12b23-168">[Merhaba Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="12b23-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="12b23-169">[Yükleme hello Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="12b23-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="12b23-170">[Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="12b23-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="12b23-171">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="12b23-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="12b23-172">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="12b23-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="12b23-173">[Merhaba Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="12b23-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="12b23-174">[Yükleme hello Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="12b23-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="12b23-175">*Oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij* (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="12b23-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="12b23-176">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="12b23-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="12b23-177">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="12b23-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

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
