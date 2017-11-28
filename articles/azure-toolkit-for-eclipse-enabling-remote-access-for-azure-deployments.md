---
title: "aaaEnabling eclipse'te Azure dağıtımları için uzaktan erişim"
description: "Nasıl tooenable uzaktan erişim için Eclipse hello Azure Araç Seti kullanarak Azure dağıtımları için öğrenin."
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
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="c4776-103">Eclipse'te Azure dağıtımları için uzaktan erişimi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c4776-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="c4776-104">toohelp dağıtımlarınızı sorun giderme, etkinleştirmek ve Uzaktan erişim tooconnect toohello sanal makine dağıtımınızı barındırma kullanmak.</span><span class="sxs-lookup"><span data-stu-id="c4776-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="c4776-105">Uzak Masaüstü Protokolü (RDP) hello üzerinde Hello uzak erişim işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c4776-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="c4776-106">TooAzure yayımladığınız veya bir Windows işletim sistemiyle Eclipse kullanıyorsanız, tooAzure yayımlamadan önce uzaktan erişim yapılandırabilirsiniz, uzaktan erişim dağıtımı için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4776-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="c4776-107">Azure'da sipariş tooconnect tooyour dağıtımın sanal makine işletim sisteminizdeki ile uyumlu bir Uzak Masaüstü İstemcisi gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c4776-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="c4776-108">Önce uzaktan erişim tooenable tooAzure nasıl dağıtma</span><span class="sxs-lookup"><span data-stu-id="c4776-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="c4776-109">tooenable uygulama tooAzure dağıtmadan önce uzaktan erişim, Eclipse Windows üzerinde çalışan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4776-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="c4776-110">Merhaba aşağıdaki resimde gösterilmiştir hello **uzaktan erişim** tooenable uzaktan erişim özellikleri iletişim kutusu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4776-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="c4776-111">İki yolu toodisplay hello vardır **uzaktan erişim** Özellikleri iletişim kutusu:</span><span class="sxs-lookup"><span data-stu-id="c4776-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="c4776-112">Merhaba tıklatın **Gelişmiş** hello bağlantıyı **uzaktan erişim** hello bölümünü **tooAzure yayımlama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c4776-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="c4776-113">Açık hello **özellikleri** Azure projenizin iletişim.</span><span class="sxs-lookup"><span data-stu-id="c4776-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="c4776-114">Yeni bir Azure dağıtım projesi oluşturduğunuzda, hello proje uzak varsayılan olarak etkin erişemeyecektir.</span><span class="sxs-lookup"><span data-stu-id="c4776-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="c4776-115">Ancak, kolayca uzaktan erişim hello hello kullanıcı adı ve parola belirterek etkinleştirebilirsiniz **tooAzure yayımlama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c4776-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="c4776-116">Merhaba uzaktan erişim parolası X.509 sertifikaları kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="c4776-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="c4776-117">Kullanmıyorsanız, kendi sertifikanızı sağlamak hello şifreleme hello Eclipse için Azure eklentisi ile birlikte otomatik olarak imzalanan bir sertifika kullanır.</span><span class="sxs-lookup"><span data-stu-id="c4776-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="c4776-118">Bu otomatik olarak imzalanan sertifika hello olan **cert** Azure projenizin klasörü hem bir ortak sertifika dosyası (SampleRemoteAccessPublic.cer) olarak depolanır ve bir kişisel bilgi değişimi (PFX) olarak sertifika dosyası ( SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="c4776-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="c4776-119">Merhaba ikinci hello hello sertifikanın özel anahtarı içerir ve bir varsayılan parolaya sahip **Parola1**.</span><span class="sxs-lookup"><span data-stu-id="c4776-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="c4776-120">Bu parola ortak bilgi olduğundan, ancak hello varsayılan sertifika yalnızca Üretim dağıtımı için değil, amaçları için öğrenme için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4776-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="c4776-121">Tooenabled Uzak Oturumlar, dağıtımları için istediğiniz zaman bu nedenle dışındaki amacıyla öğrenme için hello tıklamanız **Gelişmiş** hello bağlantıyı **tooAzure yayımlama** iletişim toospecify kendi Sertifika.</span><span class="sxs-lookup"><span data-stu-id="c4776-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="c4776-122">Bu Azure hello kullanıcı parolasının şifresini çözebilir şekilde tooupload hello PFX hello sertifika tooyour barındırılan hizmet hello Azure Yönetim Portalı içinde sürümü gerekeceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c4776-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="c4776-123">Merhaba kalan hello öğreticinin nasıl tooenable uzaktan erişim uzak erişim devre dışı başlangıçta oluşturulmuş bir Azure dağıtım projesi için gösterir.</span><span class="sxs-lookup"><span data-stu-id="c4776-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="c4776-124">Bu öğreticinin amacı, yeni bir otomatik olarak imzalanan sertifika oluşturacağız ve kendi .pfx dosyasını tercih ettiğiniz bir parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4776-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="c4776-125">Bir sertifika yetkilisi tarafından verilen bir sertifikayı kullanarak hello seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="c4776-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="c4776-126">Sonra uzaktan erişim tooenable tooAzure dağıtılan nasıl</span><span class="sxs-lookup"><span data-stu-id="c4776-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="c4776-127">tooAzure, aşağıdaki adımları kullanın hello dağıttıktan sonra tooenable uzaktan erişim:</span><span class="sxs-lookup"><span data-stu-id="c4776-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="c4776-128">Hello Azure yönetim portalında, Azure hesabınızı kullanarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="c4776-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="c4776-129">Listenizde **bulut Hizmetleri**, dağıtılan bulut hizmetinizi seçin</span><span class="sxs-lookup"><span data-stu-id="c4776-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="c4776-130">Merhaba Hello bulut hizmeti web sayfasında, tıklatın **yapılandırma** bağlantı</span><span class="sxs-lookup"><span data-stu-id="c4776-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="c4776-131">Merhaba Hello alta hello yapılandırma sayfasında, tıklatın **uzak** bağlantı</span><span class="sxs-lookup"><span data-stu-id="c4776-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="c4776-132">Merhaba açılan iletişim kutusu görüntülendiğinde:</span><span class="sxs-lookup"><span data-stu-id="c4776-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="c4776-133">Merhaba rol belirtin, istediğiniz tooenable uzaktan erişim</span><span class="sxs-lookup"><span data-stu-id="c4776-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="c4776-134">Tooselect hello tıklatın **Uzak Masaüstü'nü etkinleştirme** onay kutusu</span><span class="sxs-lookup"><span data-stu-id="c4776-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="c4776-135">Bir kullanıcı adı ve Uzaktan erişim için toouse istediğiniz parolayı belirtin</span><span class="sxs-lookup"><span data-stu-id="c4776-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="c4776-136">Merhaba sertifika toouse seçin</span><span class="sxs-lookup"><span data-stu-id="c4776-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="c4776-137">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4776-137">Click **OK**</span></span> 

<span data-ttu-id="c4776-138">Yapılandırma değişikliği birkaç dakika toocomplete sürebilir sürmekte olduğunu bildiren bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c4776-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="c4776-139">Hello yapılandırma değişikliği tamamlandıktan sonra hello hello adımları **toolog içinde uzaktan** bu makalenin sonraki bölümlerinde bölümü.</span><span class="sxs-lookup"><span data-stu-id="c4776-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="c4776-140">Tooenable uzaktan erişim nasıl paketinize</span><span class="sxs-lookup"><span data-stu-id="c4776-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="c4776-141">Eclipse'nın Proje Gezgini bölmesinde içinde Azure projenize sağ tıklatın ve **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="c4776-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="c4776-142">Merhaba, **özellikleri** iletişim kutusunda, genişletin **Azure** hello sol bölmedeki ve tıklatın **uzaktan erişim**.</span><span class="sxs-lookup"><span data-stu-id="c4776-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="c4776-143">Merhaba, **uzaktan erişim** iletişim kutusunda, olun **tüm rolleri tooaccept Uzak Masaüstü bağlantıları bu oturum açma kimlik bilgileri ile etkinleştirmek** denetlenir.</span><span class="sxs-lookup"><span data-stu-id="c4776-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="c4776-144">Merhaba Uzak Masaüstü bağlantısı için bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="c4776-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="c4776-145">Belirtin ve hello hello kullanıcının parolasını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c4776-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="c4776-146">Uzak Masaüstü Bağlantısı yaptığınızda bu iletişim kutusunda ayarladığınız hello kullanıcı adı ve parola değerlerini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4776-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="c4776-147">(Bu PFX parolanızı ayrı bir paroladan olduğunu unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="c4776-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="c4776-148">Merhaba kullanıcı hesabı için Hello sona erme tarihi belirtin.</span><span class="sxs-lookup"><span data-stu-id="c4776-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="c4776-149">Tıklatın **yeni** toocreate yeni bir otomatik olarak imzalanan sertifika.</span><span class="sxs-lookup"><span data-stu-id="c4776-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="c4776-150">(Alternatif olarak, çalışma alanı veya dosya sistemi hello aracılığıyla bir sertifika seçin **çalışma** veya **FileSystem** sırasıyla ancak biz oluşturacaksınız yeni bir Bu öğreticinin amaçları için düğmeler Sertifika.)</span><span class="sxs-lookup"><span data-stu-id="c4776-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="c4776-151">Merhaba, **yeni sertifika** iletişim kutusunda, belirtin ve onaylayın hello parola PFX dosyanız için kullanmanız.</span><span class="sxs-lookup"><span data-stu-id="c4776-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="c4776-152">İçin sağlanan hello değeri kabul **ad (CN)**, veya özel bir ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4776-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="c4776-153">.Cer formunda, yeni sertifika hello kaydedileceği hello yolu ve dosya adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c4776-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="c4776-154">Bu adım ve hello sonraki adım için hello kullanabilirsiniz **cert** Azure projeniz, ancak klasör boş toochoose olduğunuz başka bir konum.</span><span class="sxs-lookup"><span data-stu-id="c4776-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="c4776-155">Bu öğreticinin amaçları doğrultusunda kullanacağız **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="c4776-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="c4776-156">(Merhaba oluşturma **c:\mycert** klasörü önceki tooproceeding ya da kullanmak isterseniz varolan bir klasöre.)</span><span class="sxs-lookup"><span data-stu-id="c4776-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="c4776-157">Merhaba yeni bir sertifika ve özel anahtarını, .pfx formunda kaydedileceği hello yolu ve dosya adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c4776-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="c4776-158">Bu öğreticinin amaçları doğrultusunda kullanacağız **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="c4776-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="c4776-159">**Yeni sertifika** iletişim benzer toohello aşağıdaki görünmelidir (kullanmadıysanız, hello klasör yollarını Güncelleştir **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="c4776-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="c4776-160">Tıklatın **Tamam** tooclose hello **yeni sertifika** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c4776-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="c4776-161">**Uzaktan erişim** iletişim toohello aşağıdaki benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c4776-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="c4776-162">Tıklatın **Tamam** tooclose hello **uzaktan erişim** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c4776-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="c4776-163">Uygulamanızı yeniden, hello ile dağıtım toocloud için kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4776-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="c4776-164">içinde toolog uzaktan</span><span class="sxs-lookup"><span data-stu-id="c4776-164">toolog in remotely</span></span>
<span data-ttu-id="c4776-165">Rol örneği hazır olduktan sonra toohello sanal makineyi uygulamanızı barındıran uzaktan oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="c4776-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="c4776-166">Windows ve, seçili hello Eclipse kullanıyorsanız **başlangıç Uzak Masaüstü'nü dağıtma** seçeneği dağıtımınızı başladığında, dağıtım tooAzure sırasında ile bir Uzak Masaüstü Bağlantısı oturum açma ekranı sunulur.</span><span class="sxs-lookup"><span data-stu-id="c4776-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="c4776-167">Merhaba kullanıcı adı ve parola istendiğinde, hello uzak kullanıcı için belirtilen başlangıç değerleri girin ve de mümkün toolog olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4776-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="c4776-168">İçinde başka bir şekilde toolog hello uzaktan olan <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Yönetim Portalı</a>:</span><span class="sxs-lookup"><span data-stu-id="c4776-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="c4776-169">Merhaba içinde **bulut Hizmetleri** hello Azure Yönetim Portalı görünümünü bulut hizmetiniz tıklatın, **örnekleri**, belirli bir örneğe tıklayın ve hello ardından **Bağlan**düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c4776-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="c4776-170">Merhaba **Bağlan** düğmesi görünür hello aşağıdaki hello komut çubuğunda olarak:</span><span class="sxs-lookup"><span data-stu-id="c4776-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="c4776-171">Başlangıç'ı tıklattıktan sonra **Bağlan** düğmesi, istendiğinde tooopen bir RDP dosyası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4776-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="c4776-172">Merhaba dosyasını açın ve hello istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c4776-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="c4776-173">(Ayrıca bu dosya tooyour yerel bilgisayara kaydedin ve ardından hello dosyasını çift tıklatarak tooremote günlük tooyour içinde çalıştırmak toofirst gerek olmadan sanal makine hello yönetim portalına gidin.)</span><span class="sxs-lookup"><span data-stu-id="c4776-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="c4776-174">Merhaba kullanıcı adı ve parola istendiğinde, hello uzak kullanıcı için belirtilen başlangıç değerleri girin ve de mümkün toolog olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4776-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="c4776-175">Bir Windows olmayan işletim sisteminde varsa, toouse işletim sistemiyle uyumlu olan bir Uzak Masaüstü istemci gerekir ve istemci indirdiğiniz hello RDP dosyasındaki hello ayarları ile Merhaba adımları tooconfigure izleyin.</span><span class="sxs-lookup"><span data-stu-id="c4776-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="c4776-176">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="c4776-176">See Also</span></span>
<span data-ttu-id="c4776-177">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c4776-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="c4776-178">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c4776-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="c4776-179">[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c4776-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="c4776-180">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="c4776-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
