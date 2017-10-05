---
title: "Oturum açmak için Azure CLI üzerinden | Microsoft Docs"
description: "Mac, Linux ve Windows için Azure komut satırı arabiriminden (Azure CLI) Azure aboneliğinize bağlanma"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 31efab60690b54faf7992251fcd01e307c4464f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="log-in-to-azure-from-the-azure-cli"></a><span data-ttu-id="13e1b-103">Oturum açmak için Azure Azure CLI üzerinden</span><span class="sxs-lookup"><span data-stu-id="13e1b-103">Log in to Azure from the Azure CLI</span></span>
<span data-ttu-id="13e1b-104">Azure CLI, Azure kaynakları ile çalışmak için açık kaynak, platformlar arası komut kümesidir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-104">The Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="13e1b-105">Bu makalede Azure CLI Azure aboneliğinize bağlanmak için bir Azure hesabı kimlik bilgilerinizi sağlamak için farklı yollar açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="13e1b-105">This article describes the different ways to provide your Azure account credentials to connect the Azure CLI to your Azure subscription:</span></span>

* <span data-ttu-id="13e1b-106">Çalıştırma `azure login` Azure Active Directory ile kimlik doğrulaması için CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="13e1b-106">Run the `azure login` CLI command to authenticate through Azure Active Directory.</span></span> <span data-ttu-id="13e1b-107">Bu yöntem, hem de CLI komutları erişmenizi sağlayan [komut modları](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="13e1b-107">This method gives you access to CLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="13e1b-108">Komutu ek seçenekleri olmadan çalıştırdığınızda `azure login` etkileşimli bir web Portalı aracılığıyla oturum açmayı devam etmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="13e1b-108">When you run the command without additional options, `azure login` prompts you to continue logging in interactively through a web portal.</span></span> <span data-ttu-id="13e1b-109">İçin ek `azure login` komutu seçenekleri, bu makale veya türü senaryolarda bkz `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="13e1b-109">For additional `azure login` command options, see the scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="13e1b-110">Yalnızca Azure hizmet yönetimi modu CLI komutları (en yeni dağıtımlar için önerilmez) kullanmanız gerekiyorsa, indirin ve yayımlama ayarları dosyası, bilgisayarınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="13e1b-110">If you only need to use Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="13e1b-111">CLI henüz yüklemediyseniz bkz [Azure CLI yükleme](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="13e1b-111">If you haven't already installed the CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="13e1b-112">Bir Azure aboneliğiniz yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap](http://azure.microsoft.com/free/) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13e1b-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="13e1b-113">Farklı bir hesap kimlikleri ve Azure abonelikleri hakkında arka plan için bkz: [Azure aboneliklerinin Azure Active Directory ile ilişkili](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="13e1b-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="13e1b-114">Senaryo 1: etkileşimli oturum açma ile azure oturum açma</span><span class="sxs-lookup"><span data-stu-id="13e1b-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="13e1b-115">Belirli hesaplarıyla, CLI çalıştırmanızı gerektirir `azure login` ve bir web tarayıcısı adı verilen bir işlem bir web portalı üzerinden oturum açma işlemine devam *etkileşimli oturum açma*.</span><span class="sxs-lookup"><span data-stu-id="13e1b-115">With certain accounts, the CLI requires you to run `azure login` and then continue the login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="13e1b-116">Bir iş veya Okul hesabı varsa, ortak bir nedeni (olarak da adlandırılan bir *kuruluş hesabı*), çok faktörlü kimlik doğrulaması gerektiren üzere ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="13e1b-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up to require multifactor authentication.</span></span> <span data-ttu-id="13e1b-117">Resource Manager modunu komutlarını kullanmak istediğinizde de Microsoft hesabınızla etkileşimli oturum açma kullanın.</span><span class="sxs-lookup"><span data-stu-id="13e1b-117">Also use interactive login with your Microsoft account, when you want to use Resource Manager mode commands.</span></span>

<span data-ttu-id="13e1b-118">Etkileşimli oturum açma kolaydır: türü `azure login` ----seçenekleri olmadan aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="13e1b-118">Interactive login is easy: type `azure login` -- without any options -- as shown in the following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="13e1b-119">Çıktı aşağıdakine benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="13e1b-119">The output appears something like the following:</span></span>

```         
info:    Executing command login
info:    To sign in, use a web browser to open the page http://aka.ms/devicelogin. Enter the code XXXXXXXXX to authenticate.
```
<span data-ttu-id="13e1b-120">Komut çıktısında size sunulan kodu kopyalayın ve belirtilmişse http://aka.ms/devicelogin veya diğer sayfası için bir tarayıcı açın.</span><span class="sxs-lookup"><span data-stu-id="13e1b-120">Copy the code offered to you in the command output, and open a browser to http://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="13e1b-121">(Aynı bilgisayarda ya da farklı bir bilgisayar veya aygıt bir tarayıcı açabilirsiniz.) Kodu girin ve ardından kullanmak istediğiniz kimliği için kullanıcı adı ve parola girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-121">(You can open a browser on the same computer, or on a different computer or device.) Enter the code, and then you are prompted to enter the username and password for the identity you want to use.</span></span> <span data-ttu-id="13e1b-122">Bu işlem tamamlandığında, oturum açma komut kabuğu tamamlar.</span><span class="sxs-lookup"><span data-stu-id="13e1b-122">When that process completes, the command shell completes the login.</span></span> <span data-ttu-id="13e1b-123">Şöyle görünebilir:</span><span class="sxs-lookup"><span data-stu-id="13e1b-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="13e1b-124">Etkileşimli oturum açma ile kimlik doğrulaması ve yetkilendirme Azure Active Directory'yi kullanarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="13e1b-125">Bir Microsoft hesabı kimlik kullanırsanız, oturum açma işlemi, Azure Active Directory varsayılan etki alanınıza erişir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-125">If you use a Microsoft account identity, the login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="13e1b-126">(Ücretsiz bir Azure hesabı için kaydolduysanız, Azure Active Directory'ye otomatik olarak hesabınız için varsayılan etki alanı oluşturulur.)</span><span class="sxs-lookup"><span data-stu-id="13e1b-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="13e1b-127">2. Senaryo: bir kullanıcı adı ve parola ile azure oturum açma</span><span class="sxs-lookup"><span data-stu-id="13e1b-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="13e1b-128">Kullanmak `azure login` kullanıcı komutu (`-u`) bir iş kullanmak istediğiniz ya da Okul hesabı kimlik doğrulaması için parametre çok faktörlü kimlik doğrulama gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-128">Use the `azure login` command with the username (`-u`) parameter to authenticate when you want to use a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="13e1b-129">Parola için komut satırına istenir (veya parola isteğe bağlı olarak ek bir parametre geçirebilir `azure login` komutu).</span><span class="sxs-lookup"><span data-stu-id="13e1b-129">You are prompted at the command line for the password (or you can optionally pass the password as an additional parameter of the `azure login` command).</span></span> <span data-ttu-id="13e1b-130">Aşağıdaki örnekte, kullanıcı bir kurumsal hesap adını geçirir:</span><span class="sxs-lookup"><span data-stu-id="13e1b-130">The following example passes the username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="13e1b-131">Parolanızı girmeniz istenir:</span><span class="sxs-lookup"><span data-stu-id="13e1b-131">You are then prompted to enter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="13e1b-132">Daha sonra oturum açma işlemini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="13e1b-132">The login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="13e1b-133">Bu kimlik bilgileri, ilk zaman oturum varsa, kimlik doğrulama belirtecini önbelleğe istediğiniz doğrulamak için istenir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-133">If this is your first time logging in with these credentials, you are asked to verify that you wish to cache an authentication token.</span></span> <span data-ttu-id="13e1b-134">Bu istem, ayrıca daha önce kullanılan saptanmışsa `azure logout` (makalenin sonraki bölümlerinde açıklanan) komutu.</span><span class="sxs-lookup"><span data-stu-id="13e1b-134">This prompt also occurs if you previously used the `azure logout` command (described later in the article).</span></span> <span data-ttu-id="13e1b-135">Otomasyon senaryoları için bu istemini atlamak için Çalıştır `azure login` ile `-q` parametresi.</span><span class="sxs-lookup"><span data-stu-id="13e1b-135">To bypass this prompt for automation scenarios, run `azure login` with the `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="13e1b-136">Senaryo 3: bir hizmet sorumlusu ile azure oturum açma</span><span class="sxs-lookup"><span data-stu-id="13e1b-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="13e1b-137">Bir Active Directory uygulaması için bir hizmet sorumlusu oluşturmak ve hizmet sorumlusu, aboneliğinizde izinleri varsa kullanabileceğiniz `azure login` hizmet sorumlusunun kimliğini doğrulamak için komutu.</span><span class="sxs-lookup"><span data-stu-id="13e1b-137">If you create a service principal for an Active Directory application, and the service principal has permissions on your subscription, you can use the `azure login` command to authenticate the service principal.</span></span> <span data-ttu-id="13e1b-138">Senaryonuza bağlı olarak, açık parametre olarak hizmet sorumlusu kimlik bilgilerini sağlayabilir `azure login` komutu.</span><span class="sxs-lookup"><span data-stu-id="13e1b-138">Depending on your scenario, you could provide the credentials of the service principal as explicit parameters of the `azure login` command.</span></span> <span data-ttu-id="13e1b-139">Örneğin, aşağıdaki komutu, Active Directory Kiracı kimliği ve hizmet asıl adı geçirir:</span><span class="sxs-lookup"><span data-stu-id="13e1b-139">For example, the following command passes the service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="13e1b-140">Ardından parolayı girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-140">You are then prompted to provide the password.</span></span> <span data-ttu-id="13e1b-141">CLI komut dosyası veya uygulama kod aracılığıyla kimlik bilgilerini sağlayın veya etkileşimsiz Otomasyon senaryoları için hizmet sorumlusunun kimliğini doğrulamak için bir sertifika kullanır.</span><span class="sxs-lookup"><span data-stu-id="13e1b-141">You can also provide the credentials through a CLI script or application code, or use a certificate to authenticate the service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="13e1b-142">Ayrıntılı bilgi ve örnekler için bkz: [bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="13e1b-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="13e1b-143">Senaryo 4: yayımlama ayarları dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="13e1b-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="13e1b-144">Yalnızca Azure hizmet yönetimi modu CLI komutları (örneğin, Klasik dağıtım modelinde Azure sanal makineleri dağıtmak için) kullanmanız gerekiyorsa, yayımlama ayarları dosyası kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-144">If you only need to use the Azure Service Management mode CLI commands (for example, to deploy Azure VMs in the classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="13e1b-145">Bu yöntem bir sertifika abonelik ve sertifika geçerli olduğu sürece için yönetim görevleri gerçekleştirmenizi sağlar, yerel bilgisayarınıza yükler.</span><span class="sxs-lookup"><span data-stu-id="13e1b-145">This method installs a certificate on your local computer that allows you to perform management tasks for as long as the subscription and the certificate are valid.</span></span>

* <span data-ttu-id="13e1b-146">**Yayımlama ayarları dosyasını indirmek için** hesabınız için yazarak CLI Hizmet Yönetimi modunda olduğundan emin olun `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="13e1b-146">**To download the publish settings file** for your account, ensure that the CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="13e1b-147">Ardından aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="13e1b-147">Then run the following command:</span></span>

        azure account download

<span data-ttu-id="13e1b-148">Bu, varsayılan tarayıcı açar ve oturum açmak için ister [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="13e1b-148">This opens your default browser and prompts you to sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="13e1b-149">Oturum açma, sonra bir `.publishsettings` dosya yüklemelerini.</span><span class="sxs-lookup"><span data-stu-id="13e1b-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="13e1b-150">Bu dosyanın kaydedildiği yeri not edin.</span><span class="sxs-lookup"><span data-stu-id="13e1b-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="13e1b-151">Hesabınızın birden çok Azure Active Directory Kiracı ile ilişkili ise, hangi etkin bir yayımlama ayarları dosyası indirmek istediğiniz dizini seçin istenebilir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted to select which Active Directory you wish to download a publish settings file for.</span></span>
>
>

<span data-ttu-id="13e1b-152">Yükleme sayfasını kullanarak seçildikten sonra veya Klasik Azure portalını ziyaret, seçili Active Directory Klasik portal ve indirme sayfa tarafından kullanılan varsayılan olur.</span><span class="sxs-lookup"><span data-stu-id="13e1b-152">Once selected using the download page, or by visiting the Azure classic portal, the selected Active Directory becomes the default used by the classic portal and download page.</span></span> <span data-ttu-id="13e1b-153">Varsayılan kurulduktan sonra gördüğünüz metin '**seçimi sayfaya dönmek için buraya tıklayın**' sayfanın üst kısmındaki indirme.</span><span class="sxs-lookup"><span data-stu-id="13e1b-153">Once a default has been established, you see the text '**click here to return to the selection page**' at the top of the download page.</span></span> <span data-ttu-id="13e1b-154">Seçim sayfasına geri dönmek için sağlanan bağlantıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="13e1b-154">Use the provided link to return to the selection page.</span></span>

* <span data-ttu-id="13e1b-155">**Yayımlama ayarları dosyasını içeri aktarmak için**, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="13e1b-155">**To import the publish settings file**, run the following command:</span></span>

        azure account import <path to your .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="13e1b-156">Aldıktan sonra yayımlama ayarları, silmeniz gerekir `.publishsettings` dosya.</span><span class="sxs-lookup"><span data-stu-id="13e1b-156">After importing your publish settings, you should delete the `.publishsettings` file.</span></span> <span data-ttu-id="13e1b-157">Azure CLI tarafından artık gerekli ve aboneliğinizi erişmek için kullanılabilir olarak bir güvenlik riski oluşturur.</span><span class="sxs-lookup"><span data-stu-id="13e1b-157">It is no longer required by the Azure CLI and presents a security risk as it could be used to gain access to your subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="13e1b-158">CLI komut modları</span><span class="sxs-lookup"><span data-stu-id="13e1b-158">CLI command modes</span></span>
<span data-ttu-id="13e1b-159">Azure CLI farklı komut kümeleriyle Azure kaynakları ile çalışmak için iki komut modları sağlar:</span><span class="sxs-lookup"><span data-stu-id="13e1b-159">The Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="13e1b-160">**Resource Manager moduna** - Resource Manager dağıtım modelinde Azure kaynakları ile çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="13e1b-160">**Resource Manager mode** - for working with Azure resources in the Resource Manager deployment model.</span></span> <span data-ttu-id="13e1b-161">Bu modu ayarlamak için Çalıştır `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="13e1b-161">To set this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="13e1b-162">**Hizmet Yönetimi modu** - Klasik dağıtım modelinde Azure kaynakları ile çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="13e1b-162">**Service Management mode** - for working with Azure resources in the classic deployment model.</span></span> <span data-ttu-id="13e1b-163">Bu modu ayarlamak için Çalıştır `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="13e1b-163">To set this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="13e1b-164">İlk yüklediğinizde, kaynak yöneticisi modunda CLI sürümü geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="13e1b-164">When first installed, the current release of the CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="13e1b-165">Hizmet Yönetimi ve Resource Manager moduna karşılıklı olarak birbirini dışlar.</span><span class="sxs-lookup"><span data-stu-id="13e1b-165">The Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="13e1b-166">Diğer bir deyişle, bir modunda oluşturulan kaynakları diğer modundan yönetilemez.</span><span class="sxs-lookup"><span data-stu-id="13e1b-166">That is, resources created in one mode cannot be managed from the other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="13e1b-167">Birden çok abonelik</span><span class="sxs-lookup"><span data-stu-id="13e1b-167">Multiple subscriptions</span></span>
<span data-ttu-id="13e1b-168">Birden çok Azure aboneliğiniz varsa, Azure'a bağlanılıyor kimlik bilgilerinizle ilişkili tüm Aboneliklerde erişim verir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-168">If you have multiple Azure subscriptions, connecting to Azure grants access to all subscriptions associated with your credentials.</span></span> <span data-ttu-id="13e1b-169">Bir abonelik, varsayılan olarak seçilen ve işlemleri gerçekleştirirken Azure CLI tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="13e1b-169">One subscription is selected as the default, and used by the Azure CLI when performing operations.</span></span> <span data-ttu-id="13e1b-170">Abonelikleri görüntüleme geçerli varsayılan abonelik dahil olmak üzere, kullanarak `azure account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="13e1b-170">You can view the subscriptions, including the current default subscription, using the `azure account list` command.</span></span> <span data-ttu-id="13e1b-171">Bu komut, aşağıdakine benzer bilgiler döndürür:</span><span class="sxs-lookup"><span data-stu-id="13e1b-171">This command returns information similar to the following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="13e1b-172">Yukarıdaki listede **geçerli** sütunu geçerli varsayılan abonelik Azure-alt-1 olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-172">In the preceding list, the **Current** column indicates the current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="13e1b-173">Varsayılan abonelik değiştirmek için `azure account set` komutunu ve varsayılan olmasını istediğiniz aboneliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="13e1b-173">To change the default subscription, use the `azure account set` command, and specify the subscription that you wish to be the default.</span></span> <span data-ttu-id="13e1b-174">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="13e1b-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="13e1b-175">Bu varsayılan abonelik Azure-alt-2'ye değiştirir.</span><span class="sxs-lookup"><span data-stu-id="13e1b-175">This changes the default subscription to Azure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="13e1b-176">Varsayılan abonelik değiştirme hemen etkili olur ve genel bir değişikliktir; bunları aynı komut satırı örneği veya farklı bir örnek çalıştırdığınızda yeni Azure CLI komutları, yeni varsayılan abonelik kullanın.</span><span class="sxs-lookup"><span data-stu-id="13e1b-176">Changing the default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from the same command-line instance or a different instance, use the new default subscription.</span></span>
>
>

<span data-ttu-id="13e1b-177">Varsayılan olmayan bir abonelik Azure CLI ile kullanmak istediğiniz, ancak geçerli varsayılan değiştirmek istemiyorsanız, kullanabileceğiniz `--subscription` seçeneği için komutu ve işlem için kullanmak istediğiniz abonelik adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="13e1b-177">If you wish to use a non-default subscription with the Azure CLI, but don't want to change the current default, you can use the `--subscription` option for the command and provide the name of the subscription you wish to use for the operation.</span></span>

<span data-ttu-id="13e1b-178">Azure aboneliğinize bağlandıktan sonra Azure kaynakları ile çalışmak için Azure CLI komutları kullanarak başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13e1b-178">Once you are connected to your Azure subscription, you can start using the Azure CLI commands to work with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="13e1b-179">CLI ayarlarını depolama</span><span class="sxs-lookup"><span data-stu-id="13e1b-179">Storage of CLI settings</span></span>
<span data-ttu-id="13e1b-180">İle olup olmadığını oturum `azure login` komut veya içeri aktarma yayımlama ayarları, CLI profili ve günlükleri depolanmış bir `.azure` directory bulunan, `user` dizin.</span><span class="sxs-lookup"><span data-stu-id="13e1b-180">Whether you log in with the `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="13e1b-181">`user` Dizin işletim sisteminiz tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="13e1b-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="13e1b-182">Ancak, şifrelemek için ek adımlar uygulamanız önerilir, `user` dizin.</span><span class="sxs-lookup"><span data-stu-id="13e1b-182">However, we recommend that you take additional steps to encrypt your `user` directory.</span></span> <span data-ttu-id="13e1b-183">Bunu aşağıdaki yöntemlerle yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="13e1b-183">You can do so in the following ways:</span></span>

* <span data-ttu-id="13e1b-184">Windows, dizin özelliklerini değiştirin veya BitLocker'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="13e1b-184">On Windows, modify the directory properties or use BitLocker.</span></span>
* <span data-ttu-id="13e1b-185">Mac üzerinde üzerinde FileVault dizinini açın.</span><span class="sxs-lookup"><span data-stu-id="13e1b-185">On Mac, turn on FileVault for the directory.</span></span>
* <span data-ttu-id="13e1b-186">Ubuntu’da Şifreli Giriş dizini özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="13e1b-186">On Ubuntu, use the Encrypted Home directory feature.</span></span> <span data-ttu-id="13e1b-187">Diğer Linux dağıtımları benzer özellikleri sunar.</span><span class="sxs-lookup"><span data-stu-id="13e1b-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="13e1b-188">Günlük</span><span class="sxs-lookup"><span data-stu-id="13e1b-188">Logging out</span></span>
<span data-ttu-id="13e1b-189">Oturum kapatma için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="13e1b-189">To log out, use the following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="13e1b-190">Hesapla ilişkili abonelikleri yalnızca siler abonelik bilgileri yerel profilinden günlüğü Active Directory ile doğrulanmışsa.</span><span class="sxs-lookup"><span data-stu-id="13e1b-190">If the subscriptions associated with the account are only authenticated with Active Directory, logging out deletes the subscription information from the local profile.</span></span> <span data-ttu-id="13e1b-191">Yayımlama ayarları dosyası da abonelikleri alındıysa, siler Active Directory ile ilgili bilgiler yerel profilinden yalnızca ancak oturum kapatılıyor.</span><span class="sxs-lookup"><span data-stu-id="13e1b-191">However, if a publish settings file was also imported for the subscriptions, logging out only deletes Active Directory related information from the local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e1b-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13e1b-192">Next steps</span></span>
* <span data-ttu-id="13e1b-193">Azure CLI komutları kullanmak için bkz: [Kaynak Yöneticisi modunda Azure CLI komutları](virtual-machines/azure-cli-arm-commands.md) ve [Hizmet Yönetimi modunda Azure CLI komutları](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="13e1b-193">To use Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="13e1b-194">Projeye katkıda ya da Azure CLI, yükleme kaynak kodu, rapor sorunları hakkında daha fazla bilgi için ziyaret [Azure CLI için GitHub depo](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="13e1b-194">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="13e1b-195">Azure CLI veya Azure kullanarak sorunlarla karşılaşırsanız, ziyaret [Azure forumları](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="13e1b-195">If you encounter problems using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
