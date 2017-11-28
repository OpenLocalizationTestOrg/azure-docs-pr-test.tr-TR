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
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="8d9ee-103">Azure oturum açma Eclipse için Azure Araç Seti için yönergeler</span><span class="sxs-lookup"><span data-stu-id="8d9ee-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="8d9ee-104">Eclipse için Azure Araç Seti Azure hesabınızda oturum için iki yöntem sunar:</span><span class="sxs-lookup"><span data-stu-id="8d9ee-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="8d9ee-105">**Etkileşimli** - bu yöntemi kullanırken her Azure hesabınızda oturum açışınızda Azure kimlik bilgilerinizi girer.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="8d9ee-106">**Otomatik** - bu yöntemi kullanırken geçmesi kimlik bilgileri dosyası otomatik olarak Azure hesabınızda oturum için kullanabileceğiniz, hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>

<span data-ttu-id="8d9ee-107">Aşağıdaki bölümlerdeki adımları her yönteminin nasıl kullanılacağını anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="8d9ee-108">Azure hesabınızda etkileşimli olarak imzalama</span><span class="sxs-lookup"><span data-stu-id="8d9ee-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="8d9ee-109">Aşağıdaki adımlar, Azure kimlik bilgilerinizi el ile girerek Azure'da oturum nasıl çalışılacağını.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-109">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="8d9ee-110">Projenizi Eclipse ile açın.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="8d9ee-111">Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure oturum açma için Eclipse menüsü][I01]

1. <span data-ttu-id="8d9ee-113">Zaman **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **etkileşimli**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-113">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![İletişim kutusuna oturum][I02]

1. <span data-ttu-id="8d9ee-115">Zaman **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-115">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][I03]

1. <span data-ttu-id="8d9ee-117">Zaman **seçin abonelikleri** iletişim kutusu görüntülenirse, kullanın ve ardından istediğiniz abonelikleri seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-117">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Select abonelikleri iletişim kutusu][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="8d9ee-119">Etkileşimli olarak oturum açıp Azure hesabınızda oturumu imzalama</span><span class="sxs-lookup"><span data-stu-id="8d9ee-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="8d9ee-120">Önceki bölümdeki adımları yapılandırdıktan sonra otomatik olarak her zaman Eclipse yeniden hesabınızda Azure oturumu kapattınız olur.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-120">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="8d9ee-121">Ancak, Eclipse başlatmadan dışında Azure hesabınızda oturum istiyorsanız, aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-121">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="8d9ee-122">Eclipse'te, tıklatın **Araçları**, ardından **Azure**ve ardından **oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure oturum kapatma için Eclipse menüsü][L01]

1. <span data-ttu-id="8d9ee-124">Zaman **Azure Oturumu Kapat** iletişim kutusu görüntülenirse, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-124">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![İletişim kutusunu oturum][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="8d9ee-126">Azure hesabınızda oturum otomatik olarak imzalama ve kimlik bilgileri dosyası oluşturma gelecekte kullanmak için</span><span class="sxs-lookup"><span data-stu-id="8d9ee-126">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="8d9ee-127">Aşağıdaki adımlar, hizmet asıl verilerinizi içeren bir kimlik bilgileri dosyası oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-127">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="8d9ee-128">Bu adımları tamamladıktan sonra Eclipse projenizin her açtığınızda Azure'da otomatik olarak oturum için kimlik bilgileri dosyası otomatik olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-128">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="8d9ee-129">Projenizi Eclipse ile açın.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="8d9ee-130">Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure oturum açma için Eclipse menüsü][A01]

1. <span data-ttu-id="8d9ee-132">Zaman **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **otomatik**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-132">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![İletişim kutusuna oturum][A02]

1. <span data-ttu-id="8d9ee-134">Zaman **Azure oturum açma** iletişim kutusu görüntülenirse, Azure kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-134">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A03]

1. <span data-ttu-id="8d9ee-136">Zaman **kimlik doğrulama dosyalarını oluşturmak** iletişim kutusu görüntülenirse, kullanma, hedef dizininizi seçin ve ardından istediğiniz abonelikleri seçin **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-136">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A04]

1. <span data-ttu-id="8d9ee-138">**Hizmet sorumlusu Creatation durumu** iletişim kutusu görüntülenir, tıklatıp dosyalarınızı başarıyla oluşturduktan sonra **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-138">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Hizmet sorumlusu Creatation durumu iletişim kutusu][A05]

1. <span data-ttu-id="8d9ee-140">Zaman **Azure oturum açma** iletişim kutusu görüntülenirse, tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-140">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A06]

1. <span data-ttu-id="8d9ee-142">Zaman **seçin abonelikleri** iletişim kutusu görüntülenirse, kullanın ve ardından istediğiniz abonelikleri seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-142">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Select abonelikleri iletişim kutusu][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="8d9ee-144">Azure hesabınızda oturumu otomatik olarak imzalanmış imzalarken</span><span class="sxs-lookup"><span data-stu-id="8d9ee-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="8d9ee-145">Önceki bölümdeki adımları yapılandırdıktan sonra Azure Araç Seti otomatik olarak, her zaman Eclipse yeniden Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-145">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="8d9ee-146">Ancak, dışında Azure hesabınızda oturum açın ve Azure Araç Seti otomatik olarak oturum açma engellemek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="8d9ee-147">Eclipse'te, tıklatın **Araçları**, ardından **Azure**ve ardından **oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure oturum kapatma için Eclipse menüsü][L01]

1. <span data-ttu-id="8d9ee-149">Zaman **Azure Oturumu Kapat** iletişim kutusu görüntülenirse, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-149">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![İletişim kutusunu oturum][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="8d9ee-151">Önceden oluşturduğunuz bir kimlik bilgileri dosyası kullanılarak otomatik olarak Azure hesabınızda imzalama</span><span class="sxs-lookup"><span data-stu-id="8d9ee-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="8d9ee-152">Eclipse kullanırken Azure oturumunu oturum açarsanız, otomatik olarak Azure hesabınız oturum önce oluşturmuş olduğunuz bir kimlik bilgileri dosyası kullanmak Eclipse için Azure Araç Seti yeniden yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-152">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="8d9ee-153">Aşağıdaki adımlar varolan kimlik bilgileri dosyasını kullanmak için Azure Araç Seti yapılandırırken size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-153">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="8d9ee-154">Projenizi Eclipse ile açın.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="8d9ee-155">Tıklatın **Araçları**, ardından **Azure**ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure oturum açma için Eclipse menüsü][A01]

1. <span data-ttu-id="8d9ee-157">Zaman **Azure oturum açma** seçin iletişim kutusu görüntülenirse, **otomatik**ve ardından **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-157">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![İletişim kutusuna oturum][A02]

1. <span data-ttu-id="8d9ee-159">Zaman **kimliği doğrulanmış Dosya Seç** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz bir kimlik bilgileri dosyasını seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-159">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![İletişim kutusuna oturum][A08]

1. <span data-ttu-id="8d9ee-161">Zaman **Azure oturum açma** iletişim kutusu görüntülenirse, tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-161">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure Oturum Açma İletişim Kutusu][A06]

1. <span data-ttu-id="8d9ee-163">Zaman **seçin abonelikleri** iletişim kutusu görüntülenirse, kullanın ve ardından istediğiniz abonelikleri seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-163">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Select abonelikleri iletişim kutusu][A07]

## <a name="see-also"></a><span data-ttu-id="8d9ee-165">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8d9ee-165">See Also</span></span>
<span data-ttu-id="8d9ee-166">Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:</span><span class="sxs-lookup"><span data-stu-id="8d9ee-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="8d9ee-167">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="8d9ee-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8d9ee-168">[Eclipse için Azure Araç Seti Yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="8d9ee-168">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8d9ee-169">[Eclipse için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="8d9ee-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8d9ee-170">*Yönergeler için Azure araç setini Eclipse (Bu makalede) Kaydol*</span><span class="sxs-lookup"><span data-stu-id="8d9ee-170">*Sign In Instructions for the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="8d9ee-171">[Eclipse Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="8d9ee-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="8d9ee-172">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="8d9ee-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8d9ee-173">[IntelliJ için Azure Araç Seti Yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="8d9ee-173">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8d9ee-174">[IntelliJ için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="8d9ee-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8d9ee-175">[IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]</span><span class="sxs-lookup"><span data-stu-id="8d9ee-175">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8d9ee-176">[Intellij Azure'da Hello World Web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="8d9ee-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="8d9ee-177">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="8d9ee-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="8d9ee-178">[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="8d9ee-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="8d9ee-179">[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="8d9ee-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="8d9ee-180">[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="8d9ee-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="8d9ee-181">[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="8d9ee-181">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="8d9ee-182">[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="8d9ee-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="8d9ee-183">[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="8d9ee-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
<span data-ttu-id="8d9ee-184">[IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="8d9ee-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="8d9ee-185">[Eclipse için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="8d9ee-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="8d9ee-186">[IntelliJ için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="8d9ee-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="8d9ee-187">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="8d9ee-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="8d9ee-188">[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="8d9ee-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

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
