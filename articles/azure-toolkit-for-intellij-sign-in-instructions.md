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
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="122c7-103">Oturum açma Azure Araç Seti için Intellij için yönergeler</span><span class="sxs-lookup"><span data-stu-id="122c7-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="122c7-104">Intellij için Azure Araç Seti Azure hesabınızda oturum açmak için iki yöntem sunar:</span><span class="sxs-lookup"><span data-stu-id="122c7-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="122c7-105">**Etkileşimli**: Azure hesabınıza her oturum açışınızda Azure kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="122c7-105">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>
  * <span data-ttu-id="122c7-106">**Otomatik**: otomatik olarak Azure hesabınızda oturum açmak için kullanabileceğiniz bir kimlik bilgileri dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="122c7-106">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>

<span data-ttu-id="122c7-107">Aşağıdaki bölümlerde her yöntemin nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="122c7-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="122c7-108">Azure hesabınızda etkileşimli olarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="122c7-108">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="122c7-109">Azure için Azure kimlik bilgilerinizi el ile girerek oturum açmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="122c7-109">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="122c7-110">Projenizi Intellij Idea ile açın.</span><span class="sxs-lookup"><span data-stu-id="122c7-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="122c7-111">Tıklatın **Araçları**, işaret **Azure**ve ardından **Azure oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="122c7-111">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Intellij Azure Oturum Aç komutu][I01]

3. <span data-ttu-id="122c7-113">İçinde **Azure oturum açma** penceresinde, seçin **etkileşimli**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="122c7-113">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Azure oturum penceresinde seçili etkileşimli ile][I02]

4. <span data-ttu-id="122c7-115">İçinde **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="122c7-115">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Azure oturum açma iletişim penceresi][I03]

5. <span data-ttu-id="122c7-117">İçinde **seçin abonelikleri** iletişim kutusunda, kullanmak istediğiniz abonelikleri seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="122c7-117">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Abonelik Seç iletişim kutusu][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="122c7-119">Etkileşimli olarak oturum açtıktan sonra dışında Azure hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="122c7-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="122c7-120">Yukarıdaki adımları kullanarak hesabınızı yapılandırdıktan sonra otomatik olarak her zaman Intellij Idea yeniden Azure hesabınıza oturumunuz kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="122c7-120">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="122c7-121">Ancak, dışında Azure hesabınızda oturum isteyip istemediğinizi *olmadan* Intellij Idea, yeniden başlatma, aşağıdakileri yapın.</span><span class="sxs-lookup"><span data-stu-id="122c7-121">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="122c7-122">Intellij Idea içinde üzerinde **Araçları** menüsündeki **Azure**ve ardından **Azure oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="122c7-122">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Intellij Azure Oturumu Kapat komutu][L01]

2. <span data-ttu-id="122c7-124">İçinde **Azure Oturumu Kapat** onay penceresi tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="122c7-124">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Azure oturum kapatma onay penceresi][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="122c7-126">Otomatik olarak Azure hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="122c7-126">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="122c7-127">Bu bölüm hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="122c7-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="122c7-128">Bu işlemi tamamladıktan sonra Eclipse için Azure projenizi her açtığınızda otomatik olarak oturum için kimlik bilgileri dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="122c7-128">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="122c7-129">Projenizi Intellij Idea ile açın.</span><span class="sxs-lookup"><span data-stu-id="122c7-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="122c7-130">Üzerinde **Araçları** menüsündeki **Azure**ve ardından **Azure oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="122c7-130">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Intellij Azure Oturum Aç komutu][A01]

3. <span data-ttu-id="122c7-132">İçinde **Azure oturum açma** penceresinde, seçin **otomatik**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="122c7-132">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Azure oturum penceresinde seçili otomatik ile][A02]

4. <span data-ttu-id="122c7-134">İçinde **Azure oturum açma iletişim** penceresinde Azure kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="122c7-134">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Azure oturum açma iletişim penceresi][A03]

5. <span data-ttu-id="122c7-136">İçinde **kimlik doğrulama dosyalarını oluşturmak** penceresinde kullanın, hedef dizininizi seçin ve ardından istediğiniz abonelikleri seçin **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="122c7-136">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Kimlik doğrulama dosyalarını Oluştur penceresi][A04]

6. <span data-ttu-id="122c7-138">İçinde **hizmet sorumlusu oluşturma durumu** iletişim kutusu, dosyalarınızı başarıyla oluşturduktan sonra tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="122c7-138">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Hizmet sorumlusu oluşturma durumu iletişim kutusu][A05]

7. <span data-ttu-id="122c7-140">İçinde **Azure oturum açma** penceresinde tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="122c7-140">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A06]

8. <span data-ttu-id="122c7-142">İçinde **seçin abonelikleri** iletişim kutusunda, kullanmak istediğiniz abonelikleri seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="122c7-142">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Abonelik Seç iletişim kutusu][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="122c7-144">Otomatik olarak oturum açtıktan sonra dışında Azure hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="122c7-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="122c7-145">Yukarıdaki adımları kullanarak hesabınızı yapılandırdıktan sonra Azure Araç Seti otomatik olarak, her zaman Intellij Idea yeniden Azure hesabınızda oturum açtığında.</span><span class="sxs-lookup"><span data-stu-id="122c7-145">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="122c7-146">Ancak, dışında Azure hesabınızda oturum açın ve Azure Araç Seti otomatik olarak oturum açma engellemek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="122c7-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="122c7-147">Intellij Idea içinde üzerinde **Araçları** menüsündeki **Azure**ve ardından **Azure oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="122c7-147">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Intellij Azure Oturumu Kapat komutu][L01]

2. <span data-ttu-id="122c7-149">İçinde **Azure Oturumu Kapat** onay penceresi tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="122c7-149">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Azure oturum kapatma onay penceresi][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="122c7-151">Azure hesabınızda otomatik olarak var olan bir kimlik bilgileri dosyasını kullanarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="122c7-151">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="122c7-152">Intellij Idea kullanırken dışında Azure hesabınızda oturum açarsanız, otomatik olarak hesabına yeniden oturum açmanız varolan kimlik bilgileri dosyasını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="122c7-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="122c7-153">Varolan kimlik bilgileri dosyasını kullanmak Eclipse için Azure Araç Seti yapılandırmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="122c7-153">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="122c7-154">Projenizi Intellij Idea ile açın.</span><span class="sxs-lookup"><span data-stu-id="122c7-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="122c7-155">Üzerinde **Araçları** menüsündeki **Azure**ve ardından **Azure oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="122c7-155">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Intellij Azure Oturum Aç komutu][A01]

3. <span data-ttu-id="122c7-157">İçinde **Azure oturum açma** penceresinde, seçin **otomatik**ve ardından **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="122c7-157">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Azure oturum penceresinde seçili otomatik ile][A02]

4. <span data-ttu-id="122c7-159">İçinde **kimlik doğrulaması Dosya Seç** iletişim kutusunda, önceden oluşturulmuş kimlik bilgileri dosyasını seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="122c7-159">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Kimlik doğrulama Dosya Seç iletişim kutusu][A08]

5. <span data-ttu-id="122c7-161">İçinde **Azure oturum açma** penceresinde tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="122c7-161">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Azure oturum penceresinde seçili otomatik ile][A06]

6. <span data-ttu-id="122c7-163">İçinde **seçin abonelikleri** iletişim kutusunda, kullanmak istediğiniz abonelikleri seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="122c7-163">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Abonelik Seç iletişim kutusu][A07]

## <a name="next-steps"></a><span data-ttu-id="122c7-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="122c7-165">Next steps</span></span>
<span data-ttu-id="122c7-166">Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:</span><span class="sxs-lookup"><span data-stu-id="122c7-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="122c7-167">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="122c7-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="122c7-168">[Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="122c7-168">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="122c7-169">[Eclipse için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="122c7-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="122c7-170">[Eclipse için Azure Araç Seti için oturum açma yönergeleri]</span><span class="sxs-lookup"><span data-stu-id="122c7-170">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="122c7-171">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="122c7-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="122c7-172">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="122c7-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="122c7-173">[Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="122c7-173">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="122c7-174">[IntelliJ için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="122c7-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="122c7-175">*Oturum açma ilişkin yönergeler için Azure Araç Seti Intellij* (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="122c7-175">*Sign-in instructions for the Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="122c7-176">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="122c7-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="122c7-177">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="122c7-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="122c7-178">[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="122c7-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="122c7-179">[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="122c7-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="122c7-180">[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="122c7-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="122c7-181">[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="122c7-181">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="122c7-182">[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="122c7-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="122c7-183">[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="122c7-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="122c7-184">[Eclipse için Azure Araç Seti için oturum açma yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="122c7-184">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="122c7-185">[Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="122c7-185">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="122c7-186">[Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="122c7-186">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="122c7-187">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="122c7-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="122c7-188">[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="122c7-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

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
