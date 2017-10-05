---
title: Azure DevTest Labs laboratuarda bir Git deposu ekleme | Microsoft Docs
description: "Azure DevTest Labs'de özel yapılar kaynağınız için bir GitHub ya da Visual Studio Team Services Git deposu ekleme"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 053f92a65f9ae29154d471fd22ee842620b4f273
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-git-repository-to-store-custom-artifacts-and-azure-resource-manager-templates"></a><span data-ttu-id="d8b2c-103">Özel yapılar ve Azure Resource Manager şablonları depolamak için bir Git deposu ekleme</span><span class="sxs-lookup"><span data-stu-id="d8b2c-103">Add a Git repository to store custom artifacts and Azure Resource Manager templates</span></span>

<span data-ttu-id="d8b2c-104">İsterseniz [özel yapılar oluşturma](devtest-lab-artifact-author.md) laboratuvarınızda, VM'ler veya [bir özel test ortamı oluşturmak için Azure Resource Manager şablonlarını kullanma](devtest-lab-create-environment-from-arm.md), dahil etmek için özel bir Git deposuna eklemeniz gerekir yapıları veya ekibinizin oluşturduğu Azure Resource Manager şablonları.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-104">If you want to [create custom artifacts](devtest-lab-artifact-author.md) for the VMs in your lab, or [use Azure Resource Manager templates to create a custom test environment](devtest-lab-create-environment-from-arm.md), you must also add a private Git repository to include the artifacts or Azure Resource Manager templates that your team creates.</span></span> <span data-ttu-id="d8b2c-105">Depo üzerinde barındırılan [GitHub](https://github.com) veya [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="d8b2c-105">The repository can be hosted on [GitHub](https://github.com) or on [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span></span>

<span data-ttu-id="d8b2c-106">Sağladık bir [Github deposunu yapılarının](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) olarak dağıtabileceğiniz-olduğu veya Laboratuvarları için özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-106">We have provided a [Github repository of artifacts](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) that you can deploy as-is or customize for your labs.</span></span> <span data-ttu-id="d8b2c-107">Özelleştirme veya bir yapıya oluşturduğunuzda, genel havuzda depolanamıyor – kendi özel depo oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-107">When you customize or create an artifact, you cannot store them in the public repository – you must create your own private repo.</span></span> 

<span data-ttu-id="d8b2c-108">Bir VM oluşturduğunuzda, Azure Resource Manager şablonu kaydetmek, istiyorsanız ve ardından daha sonra kolayca daha fazla sanal makineleri oluşturmak için kullanmak istiyorsanız özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-108">When you create a VM, you can save the Azure Resource Manager template, customize it if you want, and then use it later to easily create more VMs.</span></span> <span data-ttu-id="d8b2c-109">Özel Azure Resource Manager şablonlarınızı depolamak için kendi özel depo oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-109">You must create your own private repository to store your custom Azure Resource Manager templates.</span></span>  

* <span data-ttu-id="d8b2c-110">GitHub depo oluşturmayı öğrenmek için bkz: [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span><span class="sxs-lookup"><span data-stu-id="d8b2c-110">To learn how to create a GitHub repository, see [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span></span>
* <span data-ttu-id="d8b2c-111">Git deposunu bir Team Services projesi oluşturmayı öğrenmek için bkz: [Visual Studio Team Services Bağlan](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span><span class="sxs-lookup"><span data-stu-id="d8b2c-111">To learn how to create a Team Services project with a Git Repository, see [Connect to Visual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span></span>

<span data-ttu-id="d8b2c-112">Aşağıdaki ekran görüntüsünde yapıları içeren bir havuz Github'da nasıl görünebileceği örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d8b2c-112">The following screen shot shows an example of how a repository containing artifacts might look in GitHub:</span></span>  
![Örnek GitHub yapıları depo](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-the-repository-information-and-credentials"></a><span data-ttu-id="d8b2c-114">Depo bilgileri ve kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="d8b2c-114">Get the repository information and credentials</span></span>
<span data-ttu-id="d8b2c-115">Laboratuvarınızı için bir depo eklemek için belirli bilgileri, depodan almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-115">To add a repository to your lab, you must first get certain information from your repository.</span></span> <span data-ttu-id="d8b2c-116">Aşağıdaki bölümlerde, GitHub ve Visual Studio Team Services üzerinde barındırılan depoları için bu bilgileri getirmenizde size rehberlik.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-116">The following sections guide you through getting this information for repositories hosted on GitHub and Visual Studio Team Services.</span></span>

### <a name="get-the-github-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="d8b2c-117">GitHub depo kopya URL'si ve kişisel erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="d8b2c-117">Get the GitHub repository clone URL and personal access token</span></span>
<span data-ttu-id="d8b2c-118">GitHub depo kopya URL'si ve kişisel erişim belirteci almak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d8b2c-118">To get the GitHub repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="d8b2c-119">Yapıyı veya Azure Resource Manager şablonu tanımlarını içeren GitHub deposunu giriş sayfasına göz atın.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-119">Browse to the home page of the GitHub repository that contains the artifact or Azure Resource Manager template definitions.</span></span>
2. <span data-ttu-id="d8b2c-120">Seçin **Kopyala veya indir**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-120">Select **Clone or download**.</span></span>
3. <span data-ttu-id="d8b2c-121">Kopyalamak için düğmesini seçin **HTTPS kopyalayın url** panoya ve daha sonra kullanmak için URL kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-121">Select the button to copy the **HTTPS clone url** to the clipboard, and save the URL for later use.</span></span>
4. <span data-ttu-id="d8b2c-122">GitHub sağ üst köşesinde profilinin resmi seçin ve Seç **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-122">Select the profile image in the upper-right corner of GitHub, and select **Settings**.</span></span>
5. <span data-ttu-id="d8b2c-123">İçinde **kişisel ayarları** menüsünü seçin sol taraftaki **kişisel erişim belirteçleri**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-123">In the **Personal settings** menu on the left, select **Personal access tokens**.</span></span>
6. <span data-ttu-id="d8b2c-124">Seçin **yeni belirteç Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-124">Select **Generate new token**.</span></span>
7. <span data-ttu-id="d8b2c-125">Üzerinde **yeni kişisel erişim belirteci** want bir **belirteci açıklama**, varsayılan öğelerde kabul **kapsamı Seç**ve ardından **belirteç oluştur** .</span><span class="sxs-lookup"><span data-stu-id="d8b2c-125">On the **New personal access token** page, enter a **Token description**, accept the default items in the **Select scopes**, and then choose **Generate Token**.</span></span>
8. <span data-ttu-id="d8b2c-126">Daha sonra ihtiyacınız olarak oluşturulan belirteç kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-126">Save the generated token as you need it later.</span></span>
9. <span data-ttu-id="d8b2c-127">GitHub artık kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-127">You can close GitHub now.</span></span>   
10. <span data-ttu-id="d8b2c-128">Devam [Laboratuvarınızı deposuna Bağlan](#connect-your-lab-to-the-repository) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-128">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span></span>

### <a name="get-the-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="d8b2c-129">Visual Studio Team Services depo kopya URL'si ve kişisel erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="d8b2c-129">Get the Visual Studio Team Services repository clone URL and personal access token</span></span>
<span data-ttu-id="d8b2c-130">Visual Studio Team Services depo kopya URL'si ve kişisel erişim belirteci almak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d8b2c-130">To get the Visual Studio Team Services repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="d8b2c-131">Takım koleksiyonunuz giriş sayfasını açın (örneğin, `https://contoso-web-team.visualstudio.com`) ve projenizi seçin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-131">Open the home page of your team collection (for example, `https://contoso-web-team.visualstudio.com`), and then select your project.</span></span>
2. <span data-ttu-id="d8b2c-132">Proje giriş sayfasında seçin **kod**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-132">On the project home page, select **Code**.</span></span>
3. <span data-ttu-id="d8b2c-133">Projede kopya URL görüntülemek için **kod** sayfasında, **kopya**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-133">To view the clone URL, on the project **Code** page, select **Clone**.</span></span>
4. <span data-ttu-id="d8b2c-134">Daha sonra Bu öğreticide gerektiği URL kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-134">Save the URL as you need it later in this tutorial.</span></span>
5. <span data-ttu-id="d8b2c-135">Kişisel erişim belirteci oluşturmak için seçin **Profilim** kullanıcı hesabı açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-135">To create a Personal Access Token, select **My profile** from the user account drop-down menu.</span></span>
6. <span data-ttu-id="d8b2c-136">Profil bilgileri sayfasında seçin **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-136">On the profile information page, select **Security**.</span></span>
7. <span data-ttu-id="d8b2c-137">Üzerinde **güvenlik** sekmesine **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-137">On the **Security** tab, select **Add**.</span></span>
8. <span data-ttu-id="d8b2c-138">İçinde **kişisel erişim belirteci oluşturma** sayfa:</span><span class="sxs-lookup"><span data-stu-id="d8b2c-138">In the **Create a personal access token** page:</span></span>

   * <span data-ttu-id="d8b2c-139">Girin bir **açıklama** belirteci.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-139">Enter a **Description** for the token.</span></span>
   * <span data-ttu-id="d8b2c-140">Seçin **180 gün** gelen **süresi içinde** listesi.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-140">Select **180 days** from the **Expires In** list.</span></span>
   * <span data-ttu-id="d8b2c-141">Seçin **tüm erişilebilir hesapları** gelen **hesapları** listesi.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-141">Choose **All accessible accounts** from the **Accounts** list.</span></span>
   * <span data-ttu-id="d8b2c-142">Seçin **tüm kapsamlar** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-142">Choose the **All scopes** option.</span></span>
   * <span data-ttu-id="d8b2c-143">Seçin **belirteç Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-143">Choose **Create Token**.</span></span>
9. <span data-ttu-id="d8b2c-144">Tamamlandığında, yeni bir belirteç görünür **kişisel erişim belirteçleri** listesi.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-144">When finished, the new token appears in the **Personal Access Tokens** list.</span></span> <span data-ttu-id="d8b2c-145">Seçin **kopyalama belirteci**ve daha sonra kullanmak için belirteç değeri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-145">Select **Copy Token**, and then save the token value for later use.</span></span>
10. <span data-ttu-id="d8b2c-146">Devam [Laboratuvarınızı deposuna Bağlan](#connect-your-lab-to-the-repository) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-146">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span></span>

## <a name="connect-your-lab-to-the-repository"></a><span data-ttu-id="d8b2c-147">Laboratuvarınızı deposuna Bağlan</span><span class="sxs-lookup"><span data-stu-id="d8b2c-147">Connect your lab to the repository</span></span>
1. <span data-ttu-id="d8b2c-148">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-148">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d8b2c-149">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** listeden.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-149">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="d8b2c-150">İstenen Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-150">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="d8b2c-151">Sol panelde seçin **yapılandırma ve ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-151">On the left panel, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="d8b2c-152">Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** alanında **depoları**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-152">On the lab's **Configuration and policies** area, select **Repositories**.</span></span>
6. <span data-ttu-id="d8b2c-153">Üzerinde **depoları** alanında **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-153">On the **Repositories** area, select **+ Add**.</span></span>

    ![Depo düğme ekleme](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. <span data-ttu-id="d8b2c-155">İkinci **depoları** sayfasında, aşağıdaki bilgileri belirtin:</span><span class="sxs-lookup"><span data-stu-id="d8b2c-155">On the second **Repositories** page, specify the following information:</span></span>

   * <span data-ttu-id="d8b2c-156">**Ad** -deposu için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-156">**Name** - Enter a name for the repository.</span></span>
   * <span data-ttu-id="d8b2c-157">**Git kopyalama URL'si** -GitHub veya Visual Studio Team Services daha önce kopyaladığınız Git HTTPS kopya URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-157">**Git Clone Url** - Enter the Git HTTPS clone URL that you copied earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="d8b2c-158">**Şube** -tanımlarınızı almak için dal girin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-158">**Branch** - Enter the branch to get your definitions.</span></span>
   * <span data-ttu-id="d8b2c-159">**Kişisel erişim belirteci** -daha önce aldığınız GitHub veya Visual Studio Team Services kişisel erişim belirteci girin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-159">**Personal Access Token** - Enter the personal access token you obtained earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="d8b2c-160">**Klasör yolları** -, yapı veya Azure Resource Manager şablonu tanımlarını içeren kopya URL göreli en az bir klasör yolu girin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-160">**Folder Paths** - Enter at least one folder path relative to the clone URL that contains your artifact or Azure Resource Manager template definitions.</span></span> <span data-ttu-id="d8b2c-161">Bir alt belirtirken, klasörün yolunu eğik eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-161">When specifying a subdirectory, make sure to include the forward slash in the folder path.</span></span>

     ![Depoları alanı](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. <span data-ttu-id="d8b2c-163">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-163">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8b2c-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8b2c-164">Next steps</span></span>
<span data-ttu-id="d8b2c-165">Özel Git deponuzu oluşturduktan sonra gereksinimlerinize bağlı olarak biri veya her ikisi, aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d8b2c-165">After you have created your private Git repository, you can do one or both of the following, depending on your needs:</span></span>
* <span data-ttu-id="d8b2c-166">Mağaza, [özel yapılar](devtest-lab-artifact-author.md), hangi daha sonra yeni sanal makineleri oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-166">Store your [custom artifacts](devtest-lab-artifact-author.md), which you can use later to create new VMs.</span></span>
* <span data-ttu-id="d8b2c-167">[Azure Resource Manager şablonları ile çoklu VM ortamları ve PaaS kaynaklarına oluşturmak](devtest-lab-create-environment-from-arm.md) ve ardından özel bağlantıların bulunması şablonları saklayın.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-167">[Create multi-VM environments and PaaS resources with Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md) and then store the templates in your private repo.</span></span>

<span data-ttu-id="d8b2c-168">Bir VM oluştururken yapıları veya şablonları Git deponuzu eklenen doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-168">When you create a VM, you can verify that the artifacts or templates are added to your Git repository.</span></span> <span data-ttu-id="d8b2c-169">Bunlar, özel depo kaynağını belirtir sütununda gösterilen adını yapıları veya şablonları listesinde hemen kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d8b2c-169">They are available immediately in the list of artifacts or templates, with the name of your private repo shown in the column that specifies the source.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a><span data-ttu-id="d8b2c-170">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="d8b2c-170">Related blog posts</span></span>
* [<span data-ttu-id="d8b2c-171">Azure DevTest Labs yapıları başarısız olan ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="d8b2c-171">How to troubleshoot failing Artifacts in Azure DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="d8b2c-172">Bir VM Azure DevTest Labs'de resource manager şablonu kullanarak mevcut AD etki alanına</span><span class="sxs-lookup"><span data-stu-id="d8b2c-172">Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
