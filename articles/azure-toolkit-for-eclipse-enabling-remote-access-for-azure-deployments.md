---
title: "Eclipse'te Azure dağıtımları için uzaktan erişimi etkinleştirme"
description: "Eclipse için Azure Araç Seti kullanarak Azure dağıtımları için uzaktan erişimi etkinleştirmek öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="03e55-103">Eclipse'te Azure dağıtımları için uzaktan erişimi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="03e55-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="03e55-104">Dağıtımlarınızı gidermenize yardımcı olması için etkinleştirmek ve Uzaktan erişim, dağıtımınızı barındıran sanal makineye bağlanmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="03e55-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="03e55-105">Uzak Masaüstü Protokolü (RDP) üzerinde uzak erişim işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="03e55-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="03e55-106">Azure'da yayımladınız veya bir Windows işletim sistemiyle Eclipse kullanıyorsanız, Azure'da yayımlamadan önce uzaktan erişim yapılandırabilirsiniz, uzaktan erişim dağıtımı için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03e55-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="03e55-107">Azure'daki dağıtımınızın sanal makineye bağlanmak için işletim sistemiyle uyumlu olan bir Uzak Masaüstü istemci gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="03e55-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="03e55-108">Azure'a dağıtmadan önce uzaktan erişim etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="03e55-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="03e55-109">Uygulamanızı Azure'a dağıtmadan önce uzaktan erişimi etkinleştirmek için Eclipse Windows üzerinde çalışıyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="03e55-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="03e55-110">Aşağıdaki resimde gösterildiği **uzaktan erişim** uzaktan erişimi etkinleştirmek için kullanılan özellikleri iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="03e55-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="03e55-111">Görüntülenecek iki yolla **uzaktan erişim** Özellikleri iletişim kutusu:</span><span class="sxs-lookup"><span data-stu-id="03e55-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="03e55-112">Tıklatın **Gelişmiş** bağlamak **uzaktan erişim** bölümünü **Azure Yayımla** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03e55-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="03e55-113">Açık **özellikleri** Azure projenizin iletişim.</span><span class="sxs-lookup"><span data-stu-id="03e55-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="03e55-114">Yeni bir Azure dağıtım projesi oluşturduğunuzda, projeyi uzak varsayılan olarak etkin erişemeyecektir.</span><span class="sxs-lookup"><span data-stu-id="03e55-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="03e55-115">Ancak, kolayca uzaktan erişim kullanıcı adı ve parola belirterek etkinleştirebilirsiniz **Azure Yayımla** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03e55-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="03e55-116">Uzaktan erişim parolası X.509 sertifikaları kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="03e55-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="03e55-117">Kullanmıyorsanız, kendi sertifikanızı sağlamak Eclipse için Azure eklentisi ile birlikte otomatik olarak imzalanan bir sertifika şifreleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="03e55-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="03e55-118">Bu otomatik olarak imzalanan sertifika bulunduğu **cert** hem bir ortak sertifika dosyası (SampleRemoteAccessPublic.cer) ve bir kişisel bilgi değişimi (PFX) sertifika dosyası (SampleRemoteAccessPrivate.pfx) olarak depolanan projenizin Azure klasör.</span><span class="sxs-lookup"><span data-stu-id="03e55-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="03e55-119">İkinci sertifikanın özel anahtarı içerir ve bir varsayılan parolaya sahip **Parola1**.</span><span class="sxs-lookup"><span data-stu-id="03e55-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="03e55-120">Bu parola ortak bilgi olduğundan, ancak varsayılan sertifikayı amacıyla, Üretim dağıtımı için değil yalnızca öğrenme için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="03e55-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="03e55-121">Böylece dışındaki amacıyla öğrenme için etkin uzaktan oturumlar, dağıtımları için istediğinizde tıklamanız **Gelişmiş** bağlamak **Azure Yayımla** iletişim kutusunu kullanarak kendi sertifikanızı belirtin.</span><span class="sxs-lookup"><span data-stu-id="03e55-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="03e55-122">Bu Azure kullanıcı parolasının şifresini çözebilir şekilde Azure Yönetim Portalı içinde barındırılan hizmetinize Sertifika PFX sürümünü yüklemek gerekeceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="03e55-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="03e55-123">Öğretici geri kalanı ile uzaktan erişim devre dışı başlangıçta oluşturulmuş bir Azure dağıtım projesi için uzaktan erişimi etkinleştirmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="03e55-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="03e55-124">Bu öğreticinin amacı, yeni bir otomatik olarak imzalanan sertifika oluşturacağız ve kendi .pfx dosyasını tercih ettiğiniz bir parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="03e55-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="03e55-125">Ayrıca bir sertifika yetkilisi tarafından verilen bir sertifika kullanma seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="03e55-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="03e55-126">Azure'a dağıttıktan sonra uzaktan erişim etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="03e55-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="03e55-127">Azure'a dağıttıktan sonra uzaktan erişimi etkinleştirmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="03e55-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="03e55-128">Azure hesabınızı kullanarak Azure yönetim portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="03e55-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="03e55-129">Listenizde **bulut Hizmetleri**, dağıtılan bulut hizmetinizi seçin</span><span class="sxs-lookup"><span data-stu-id="03e55-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="03e55-130">Bulut hizmeti web sayfasını tıklatın **yapılandırma** bağlantı</span><span class="sxs-lookup"><span data-stu-id="03e55-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="03e55-131">Yapılandırma sayfasında altta tıklatın **uzak** bağlantı</span><span class="sxs-lookup"><span data-stu-id="03e55-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="03e55-132">Açılan iletişim kutusu görüntülendiğinde:</span><span class="sxs-lookup"><span data-stu-id="03e55-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="03e55-133">Uzaktan erişimi etkinleştirmek, için istediğiniz rolü belirtin</span><span class="sxs-lookup"><span data-stu-id="03e55-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="03e55-134">Seçmek için tıklatın **Uzak Masaüstü'nü etkinleştirme** onay kutusu</span><span class="sxs-lookup"><span data-stu-id="03e55-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="03e55-135">Bir kullanıcı adı ve Uzaktan erişim için kullanmak istediğiniz parolayı belirtin</span><span class="sxs-lookup"><span data-stu-id="03e55-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="03e55-136">Kullanılacak sertifikayı seçin</span><span class="sxs-lookup"><span data-stu-id="03e55-136">Select the certificate to use</span></span>

6. <span data-ttu-id="03e55-137">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="03e55-137">Click **OK**</span></span> 

<span data-ttu-id="03e55-138">Yapılandırma değişikliği tamamlanması birkaç dakika sürebilir sürmekte olduğunu bildiren bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="03e55-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="03e55-139">Yapılandırma değişikliği tamamlandıktan sonra adımları **uzaktan oturum açmak için** bu makalenin sonraki bölümlerinde bölümü.</span><span class="sxs-lookup"><span data-stu-id="03e55-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="03e55-140">Uzaktan erişim paketinize etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="03e55-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="03e55-141">Eclipse'nın Proje Gezgini bölmesinde içinde Azure projenize sağ tıklatın ve **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="03e55-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="03e55-142">İçinde **özellikleri** iletişim kutusunda, genişletin **Azure** tıklatın ve sol bölmesinde **uzaktan erişim**.</span><span class="sxs-lookup"><span data-stu-id="03e55-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="03e55-143">İçinde **uzaktan erişim** iletişim kutusunda, olun **bu oturum açma kimlik bilgileri ile Uzak Masaüstü bağlantıları kabul etmek üzere tüm rolleri etkinleştir** denetlenir.</span><span class="sxs-lookup"><span data-stu-id="03e55-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="03e55-144">Uzak Masaüstü bağlantısı için bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="03e55-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="03e55-145">Belirtin ve kullanıcının parolasını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="03e55-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="03e55-146">Uzak Masaüstü Bağlantısı yaptığınızda bu iletişim kutusunda ayarladığınız kullanıcı adı ve parola değerlerini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="03e55-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="03e55-147">(Bu PFX parolanızı ayrı bir paroladan olduğunu unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="03e55-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="03e55-148">Kullanıcı hesabı için sona erme tarihi belirtin.</span><span class="sxs-lookup"><span data-stu-id="03e55-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="03e55-149">Tıklatın **yeni** yeni bir otomatik olarak imzalanan sertifika oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="03e55-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="03e55-150">(Alternatif olarak, çalışma alanı veya dosya sistemi bir sertifika seçin **çalışma** veya **FileSystem** düğmeleri, sırasıyla ancak amacıyla Bu öğretici yeni bir sertifika oluşturacağız.)</span><span class="sxs-lookup"><span data-stu-id="03e55-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="03e55-151">İçinde **yeni sertifika** iletişim kutusunda, belirtin ve PFX dosyası için kullandığınız parolayı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="03e55-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="03e55-152">İçin sağlanan değer kabul **ad (CN)**, veya özel bir ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="03e55-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="03e55-153">.Cer formunda, yeni sertifikanın kaydedileceği yolu ve dosya adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="03e55-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="03e55-154">Bu adımı ve sonraki adım için kullanabileceğinizi **cert** klasörü Azure projeniz, ancak başka bir konum seçmek boş.</span><span class="sxs-lookup"><span data-stu-id="03e55-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="03e55-155">Bu öğreticinin amaçları doğrultusunda kullanacağız **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="03e55-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="03e55-156">(Oluşturma **c:\mycert** devam etmeden veya kullanmak isterseniz var olan bir klasörü önce klasör.)</span><span class="sxs-lookup"><span data-stu-id="03e55-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="03e55-157">Yeni sertifikayı ve özel anahtarını, .pfx formunda kaydedileceği yolu ve dosya adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="03e55-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="03e55-158">Bu öğreticinin amaçları doğrultusunda kullanacağız **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="03e55-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="03e55-159">**Yeni sertifika** iletişim aşağıdakine benzer görünmelidir (kullanmadıysanız, klasör yollarını güncelleştirme **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="03e55-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="03e55-160">Tıklatın **Tamam** kapatmak için **yeni sertifika** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03e55-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="03e55-161">**Uzaktan erişim** iletişim aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="03e55-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="03e55-162">Tıklatın **Tamam** kapatmak için **uzaktan erişim** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03e55-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="03e55-163">Uygulamanızın, bulut dağıtımı için ayarlanmış yapı ile yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03e55-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="03e55-164">Uzaktan oturum açmak için</span><span class="sxs-lookup"><span data-stu-id="03e55-164">To log in remotely</span></span>
<span data-ttu-id="03e55-165">Rol örneği hazır olduğunda, uzaktan uygulamanızı barındıran sanal makineye oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="03e55-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="03e55-166">Windows ve seçtiğiniz Eclipse kullanıyorsanız **başlangıç Uzak Masaüstü'nü dağıtma** seçeneği dağıtımınızı başladığında Azure, dağıtım sırasında ile bir Uzak Masaüstü Bağlantısı oturum açma ekranı sunulur.</span><span class="sxs-lookup"><span data-stu-id="03e55-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="03e55-167">Kullanıcı adı ve parola istendiğinde, uzak kullanıcı için belirtilen değerleri girin ve oturum açamaz.</span><span class="sxs-lookup"><span data-stu-id="03e55-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="03e55-168">Uzaktan oturum açmak için başka bir yolunu <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Yönetim Portalı</a>:</span><span class="sxs-lookup"><span data-stu-id="03e55-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="03e55-169">İçinde **bulut Hizmetleri** görüntüleme Azure Yönetim Portalı'nın, bulut hizmeti,'ı tıklatın **örnekleri**, belirli bir örneğe tıklayın ve ardından **Bağlan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="03e55-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="03e55-170">**Bağlan** düğmesi, komut çubuğunda aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="03e55-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="03e55-171">' I tıklattıktan sonra **Bağlan** istenir bir RDP dosyasını açmak için düğmesi,.</span><span class="sxs-lookup"><span data-stu-id="03e55-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="03e55-172">Dosyasını açın ve yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="03e55-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="03e55-173">(, De bu dosyayı yerel bilgisayarınıza kaydedin ve ardından, sanal makinenize uzaktan oturum açmak önce Yönetim Portalı'na gitmesini gerek kalmadan çift tıklayarak dosyayı çalıştırın.)</span><span class="sxs-lookup"><span data-stu-id="03e55-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="03e55-174">Kullanıcı adı ve parola istendiğinde, uzak kullanıcı için belirtilen değerleri girin ve oturum açamaz.</span><span class="sxs-lookup"><span data-stu-id="03e55-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="03e55-175">Bir Windows olmayan işletim sisteminde varsa, işletim sistemiyle uyumlu bir Uzak Masaüstü İstemcisi'ni kullanın ve indirdiğiniz RDP dosyasındaki ayarları ile istemci yapılandırma adımlarını izleyin gerekir.</span><span class="sxs-lookup"><span data-stu-id="03e55-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="03e55-176">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="03e55-176">See Also</span></span>
<span data-ttu-id="03e55-177">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="03e55-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="03e55-178">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="03e55-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="03e55-179">[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="03e55-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="03e55-180">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="03e55-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
