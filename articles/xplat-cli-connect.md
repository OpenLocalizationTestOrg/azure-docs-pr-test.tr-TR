---
title: Merhaba CLI gelen tooAzure aaaLog | Microsoft Docs
description: "Mac, Linux ve Windows için Azure komut satırı arabirimi (Azure CLI) hello tooyour Azure aboneliği bağlanmak"
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
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a><span data-ttu-id="29a2d-103">TooAzure hello Azure CLI gelen oturum</span><span class="sxs-lookup"><span data-stu-id="29a2d-103">Log in tooAzure from hello Azure CLI</span></span>
<span data-ttu-id="29a2d-104">Hello Azure CLI, Azure kaynakları ile çalışmak için açık kaynak, platformlar arası komut kümesidir.</span><span class="sxs-lookup"><span data-stu-id="29a2d-104">hello Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="29a2d-105">Bu makalede Azure hesabı kimlik bilgileri tooconnect hello Azure CLI tooyour Azure aboneliği hello farklı şekillerde tooprovide açıklanır:</span><span class="sxs-lookup"><span data-stu-id="29a2d-105">This article describes hello different ways tooprovide your Azure account credentials tooconnect hello Azure CLI tooyour Azure subscription:</span></span>

* <span data-ttu-id="29a2d-106">Merhaba çalıştırmak `azure login` CLI komutu tooauthenticate Azure Active Directory üzerinden.</span><span class="sxs-lookup"><span data-stu-id="29a2d-106">Run hello `azure login` CLI command tooauthenticate through Azure Active Directory.</span></span> <span data-ttu-id="29a2d-107">Hem de tooCLI komutları bu yöntem erişmenizi [komut modları](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="29a2d-107">This method gives you access tooCLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="29a2d-108">Merhaba komutu ek seçenekleri olmadan çalıştırdığınızda `azure login` etkileşimli bir web Portalı aracılığıyla oturum açmayı toocontinue ister.</span><span class="sxs-lookup"><span data-stu-id="29a2d-108">When you run hello command without additional options, `azure login` prompts you toocontinue logging in interactively through a web portal.</span></span> <span data-ttu-id="29a2d-109">İçin ek `azure login` komutu seçenekleri, bu makale veya türü hello senaryolar görmek `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="29a2d-109">For additional `azure login` command options, see hello scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="29a2d-110">Yalnızca toouse Azure hizmet yönetimi modu CLI komutları (en yeni dağıtımlar için önerilmez) gerekiyorsa, indirin ve yayımlama ayarları dosyası, bilgisayarınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="29a2d-110">If you only need toouse Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="29a2d-111">Merhaba CLI henüz yüklemediyseniz bkz [yükleme hello Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="29a2d-111">If you haven't already installed hello CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="29a2d-112">Bir Azure aboneliğiniz yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap](http://azure.microsoft.com/free/) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29a2d-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="29a2d-113">Farklı bir hesap kimlikleri ve Azure abonelikleri hakkında arka plan için bkz: [Azure aboneliklerinin Azure Active Directory ile ilişkili](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="29a2d-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="29a2d-114">Senaryo 1: etkileşimli oturum açma ile azure oturum açma</span><span class="sxs-lookup"><span data-stu-id="29a2d-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="29a2d-115">Belirli hesaplarıyla toorun gerektirir hello CLI `azure login` ve bir web tarayıcısı adı verilen bir işlem bir web portalı üzerinden hello oturum açma işlemine devam *etkileşimli oturum açma*.</span><span class="sxs-lookup"><span data-stu-id="29a2d-115">With certain accounts, hello CLI requires you toorun `azure login` and then continue hello login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="29a2d-116">Bir iş veya Okul hesabı varsa, ortak bir nedeni (olarak da adlandırılan bir *kuruluş hesabı*) toorequire çok faktörlü kimlik doğrulamasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="29a2d-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up toorequire multifactor authentication.</span></span> <span data-ttu-id="29a2d-117">Ayrıca toouse Resource Manager modunu komutları istediğinizde etkileşimli oturum açma Microsoft hesabınızla kullanın.</span><span class="sxs-lookup"><span data-stu-id="29a2d-117">Also use interactive login with your Microsoft account, when you want toouse Resource Manager mode commands.</span></span>

<span data-ttu-id="29a2d-118">Etkileşimli oturum açma kolaydır: türü `azure login` ----seçenekleri olmadan hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="29a2d-118">Interactive login is easy: type `azure login` -- without any options -- as shown in hello following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="29a2d-119">Merhaba çıktı hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="29a2d-119">hello output appears something like hello following:</span></span>

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
<span data-ttu-id="29a2d-120">Merhaba komut çıktısında tooyou sunulan hello kodu kopyalayın ve belirtilmişse tarayıcı toohttp://aka.ms/devicelogin veya diğer sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="29a2d-120">Copy hello code offered tooyou in hello command output, and open a browser toohttp://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="29a2d-121">(Merhaba bir tarayıcıda açın aynı bilgisayara veya başka bir bilgisayara veya aygıt.) Merhaba kodu girin ve ardından istendiğinde tooenter hello kullanıcı adı ve parola misiniz hello kimliğini toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="29a2d-121">(You can open a browser on hello same computer, or on a different computer or device.) Enter hello code, and then you are prompted tooenter hello username and password for hello identity you want toouse.</span></span> <span data-ttu-id="29a2d-122">Bu işlem tamamlandığında hello komut kabuğu hello oturum açma işlemini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="29a2d-122">When that process completes, hello command shell completes hello login.</span></span> <span data-ttu-id="29a2d-123">Şöyle görünebilir:</span><span class="sxs-lookup"><span data-stu-id="29a2d-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="29a2d-124">Etkileşimli oturum açma ile kimlik doğrulaması ve yetkilendirme Azure Active Directory'yi kullanarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="29a2d-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="29a2d-125">Bir Microsoft hesabı kimlik kullanırsanız, hello oturum açma işlemi, Azure Active Directory varsayılan etki alanınıza erişir.</span><span class="sxs-lookup"><span data-stu-id="29a2d-125">If you use a Microsoft account identity, hello login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="29a2d-126">(Ücretsiz bir Azure hesabı için kaydolduysanız, Azure Active Directory'ye otomatik olarak hesabınız için varsayılan etki alanı oluşturulur.)</span><span class="sxs-lookup"><span data-stu-id="29a2d-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="29a2d-127">2. Senaryo: bir kullanıcı adı ve parola ile azure oturum açma</span><span class="sxs-lookup"><span data-stu-id="29a2d-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="29a2d-128">Kullanım hello `azure login` hello username komutu (`-u`) istediğiniz toouse bir iş veya Okul hesabı parametresi tooauthenticate, çok faktörlü kimlik doğrulama gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="29a2d-128">Use hello `azure login` command with hello username (`-u`) parameter tooauthenticate when you want toouse a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="29a2d-129">Merhaba parolası hello komut satırında istenir (veya isteğe bağlı olarak hello parola hello ek bir parametre geçirebilir `azure login` komutu).</span><span class="sxs-lookup"><span data-stu-id="29a2d-129">You are prompted at hello command line for hello password (or you can optionally pass hello password as an additional parameter of hello `azure login` command).</span></span> <span data-ttu-id="29a2d-130">Merhaba aşağıdaki örnek hello kullanıcı bir kurumsal hesap adını geçirir:</span><span class="sxs-lookup"><span data-stu-id="29a2d-130">hello following example passes hello username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="29a2d-131">Ardından olduğunuz tooenter parolanızı istenir:</span><span class="sxs-lookup"><span data-stu-id="29a2d-131">You are then prompted tooenter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="29a2d-132">ardından Hello oturum açma işlemini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="29a2d-132">hello login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="29a2d-133">Bu kimlik bilgileri, ilk zaman oturum varsa tooverify sorulur kimlik doğrulama belirtecini toocache istiyor.</span><span class="sxs-lookup"><span data-stu-id="29a2d-133">If this is your first time logging in with these credentials, you are asked tooverify that you wish toocache an authentication token.</span></span> <span data-ttu-id="29a2d-134">Merhaba daha önce kullandıysanız bu istemi ayrıca oluşur `azure logout` (Merhaba makalenin sonraki bölümlerinde açıklanan) komutu.</span><span class="sxs-lookup"><span data-stu-id="29a2d-134">This prompt also occurs if you previously used hello `azure logout` command (described later in hello article).</span></span> <span data-ttu-id="29a2d-135">Bu istemi Otomasyon senaryoları için toobypass çalıştırma `azure login` hello ile `-q` parametresi.</span><span class="sxs-lookup"><span data-stu-id="29a2d-135">toobypass this prompt for automation scenarios, run `azure login` with hello `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="29a2d-136">Senaryo 3: bir hizmet sorumlusu ile azure oturum açma</span><span class="sxs-lookup"><span data-stu-id="29a2d-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="29a2d-137">Bir Active Directory uygulaması için bir hizmet sorumlusu oluşturmak ve hello hizmet sorumlusu, aboneliğinizde izinlere sahipse, hello kullanabilirsiniz `azure login` komutu tooauthenticate hello hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="29a2d-137">If you create a service principal for an Active Directory application, and hello service principal has permissions on your subscription, you can use hello `azure login` command tooauthenticate hello service principal.</span></span> <span data-ttu-id="29a2d-138">Senaryonuza bağlı olarak, hello açık parametre olarak hello hizmet sorumlusu hello kimlik bilgilerini sağlamanız `azure login` komutu.</span><span class="sxs-lookup"><span data-stu-id="29a2d-138">Depending on your scenario, you could provide hello credentials of hello service principal as explicit parameters of hello `azure login` command.</span></span> <span data-ttu-id="29a2d-139">Örneğin, hello aşağıdaki komutu hello hizmet asıl adı ve Active Directory Kiracı kimliği geçirir:</span><span class="sxs-lookup"><span data-stu-id="29a2d-139">For example, hello following command passes hello service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="29a2d-140">Parola istendiğinde tooprovide hello sonra size aittir.</span><span class="sxs-lookup"><span data-stu-id="29a2d-140">You are then prompted tooprovide hello password.</span></span> <span data-ttu-id="29a2d-141">Ayrıca, CLI komut dosyası veya uygulama kod aracılığıyla hello kimlik bilgilerini sağlayın veya bir sertifika tooauthenticate hello hizmet sorumlusu etkileşimsiz Otomasyon senaryoları için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29a2d-141">You can also provide hello credentials through a CLI script or application code, or use a certificate tooauthenticate hello service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="29a2d-142">Ayrıntılı bilgi ve örnekler için bkz: [bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="29a2d-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="29a2d-143">Senaryo 4: yayımlama ayarları dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="29a2d-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="29a2d-144">Yalnızca toouse hello Azure hizmet yönetimi modu CLI komutları (örneğin, toodeploy Azure VM'ler hello Klasik dağıtım modelinde) gerekiyorsa, yayımlama ayarları dosyası kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="29a2d-144">If you only need toouse hello Azure Service Management mode CLI commands (for example, toodeploy Azure VMs in hello classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="29a2d-145">Bu yöntem bir sertifika hello abonelik ve hello sertifika geçerli olduğu sürece, tooperform yönetim görevleri için sağlayan yerel bilgisayarınıza yükler.</span><span class="sxs-lookup"><span data-stu-id="29a2d-145">This method installs a certificate on your local computer that allows you tooperform management tasks for as long as hello subscription and hello certificate are valid.</span></span>

* <span data-ttu-id="29a2d-146">**toodownload hello yayımlama ayarları dosyası** hesabınız için CLI yazarak Hizmet Yönetimi modunda olduğundan bu hello olun `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="29a2d-146">**toodownload hello publish settings file** for your account, ensure that hello CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="29a2d-147">Ardından hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="29a2d-147">Then run hello following command:</span></span>

        azure account download

<span data-ttu-id="29a2d-148">Bu varsayılan tarayıcınızı açar ve toohello toosign ister [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="29a2d-148">This opens your default browser and prompts you toosign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="29a2d-149">Oturum açma, sonra bir `.publishsettings` dosya yüklemelerini.</span><span class="sxs-lookup"><span data-stu-id="29a2d-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="29a2d-150">Bu dosyanın kaydedildiği yeri not edin.</span><span class="sxs-lookup"><span data-stu-id="29a2d-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="29a2d-151">Hesabınızın birden çok Azure Active Directory Kiracı ile ilişkili ise, Active Directory yayımlama ayarlarını toodownload istediğiniz dosya için istendiğinde tooselect olabilir.</span><span class="sxs-lookup"><span data-stu-id="29a2d-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted tooselect which Active Directory you wish toodownload a publish settings file for.</span></span>
>
>

<span data-ttu-id="29a2d-152">Merhaba indirme sayfasını kullanarak seçildikten sonra veya hello Klasik Azure portalını ziyaret, hello seçili Active Directory hello Klasik portal ve indirme sayfası tarafından kullanılan hello varsayılan olur.</span><span class="sxs-lookup"><span data-stu-id="29a2d-152">Once selected using hello download page, or by visiting hello Azure classic portal, hello selected Active Directory becomes hello default used by hello classic portal and download page.</span></span> <span data-ttu-id="29a2d-153">Varsayılan kurulduktan sonra hello metni görmek '**tooreturn toohello Seçimi sayfasında burayı**' hello sayfanın üst kısmındaki hello indirme.</span><span class="sxs-lookup"><span data-stu-id="29a2d-153">Once a default has been established, you see hello text '**click here tooreturn toohello selection page**' at hello top of hello download page.</span></span> <span data-ttu-id="29a2d-154">Bağlantı tooreturn toohello Seçimi sayfasında sağlanan hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="29a2d-154">Use hello provided link tooreturn toohello selection page.</span></span>

* <span data-ttu-id="29a2d-155">**tooimport hello yayımlama ayarları dosyası**çalıştırın hello komutu aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="29a2d-155">**tooimport hello publish settings file**, run hello following command:</span></span>

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="29a2d-156">Aldıktan sonra yayımlama ayarları, hello silmelisiniz `.publishsettings` dosya.</span><span class="sxs-lookup"><span data-stu-id="29a2d-156">After importing your publish settings, you should delete hello `.publishsettings` file.</span></span> <span data-ttu-id="29a2d-157">Azure CLI hello tarafından artık gerekmiyor ve kullanılan toogain erişim tooyour abonelik olabileceğinden güvenlik riski oluşturur.</span><span class="sxs-lookup"><span data-stu-id="29a2d-157">It is no longer required by hello Azure CLI and presents a security risk as it could be used toogain access tooyour subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="29a2d-158">CLI komut modları</span><span class="sxs-lookup"><span data-stu-id="29a2d-158">CLI command modes</span></span>
<span data-ttu-id="29a2d-159">Hello Azure CLI farklı komut kümeleriyle Azure kaynakları ile çalışmak için iki komut modları sağlar:</span><span class="sxs-lookup"><span data-stu-id="29a2d-159">hello Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="29a2d-160">**Resource Manager moduna** - hello Resource Manager dağıtım modelinde Azure kaynakları ile çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="29a2d-160">**Resource Manager mode** - for working with Azure resources in hello Resource Manager deployment model.</span></span> <span data-ttu-id="29a2d-161">tooset çalıştırmak Bu mod, `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="29a2d-161">tooset this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="29a2d-162">**Hizmet Yönetimi modu** - hello Klasik dağıtım modelinde Azure kaynakları ile çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="29a2d-162">**Service Management mode** - for working with Azure resources in hello classic deployment model.</span></span> <span data-ttu-id="29a2d-163">tooset çalıştırmak Bu mod, `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="29a2d-163">tooset this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="29a2d-164">İlk yüklendiğinde, CLI Resource Manager modundayken hello sürümü geçerli hello.</span><span class="sxs-lookup"><span data-stu-id="29a2d-164">When first installed, hello current release of hello CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="29a2d-165">Merhaba Resource Manager moduna ve hizmet yönetimi modu karşılıklı olarak birbirini dışlar.</span><span class="sxs-lookup"><span data-stu-id="29a2d-165">hello Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="29a2d-166">Diğer bir deyişle, bir modunda oluşturulan kaynakları hello yönetilemez diğer modu.</span><span class="sxs-lookup"><span data-stu-id="29a2d-166">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="29a2d-167">Birden çok abonelik</span><span class="sxs-lookup"><span data-stu-id="29a2d-167">Multiple subscriptions</span></span>
<span data-ttu-id="29a2d-168">Birden çok Azure aboneliğiniz varsa, tooAzure bağlanırken kimlik bilgilerinizle ilişkili tooall abonelik erişim verir.</span><span class="sxs-lookup"><span data-stu-id="29a2d-168">If you have multiple Azure subscriptions, connecting tooAzure grants access tooall subscriptions associated with your credentials.</span></span> <span data-ttu-id="29a2d-169">Bir abonelik hello varsayılan olarak seçilen ve işlemleri gerçekleştirirken Azure CLI hello tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="29a2d-169">One subscription is selected as hello default, and used by hello Azure CLI when performing operations.</span></span> <span data-ttu-id="29a2d-170">Merhaba abonelikleri görüntüleme hello geçerli varsayılan aboneliğe dahil olmak üzere, hello kullanarak `azure account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="29a2d-170">You can view hello subscriptions, including hello current default subscription, using hello `azure account list` command.</span></span> <span data-ttu-id="29a2d-171">Bu komut, bilgi benzer toohello aşağıdaki döndürür:</span><span class="sxs-lookup"><span data-stu-id="29a2d-171">This command returns information similar toohello following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="29a2d-172">Liste önceki hello hello **geçerli** sütunu hello geçerli varsayılan abonelik Azure-alt-1 olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="29a2d-172">In hello preceding list, hello **Current** column indicates hello current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="29a2d-173">toochange hello varsayılan abonelik, kullanım hello `azure account set` komut ve toobe hello varsayılan istediğiniz hello abonelik belirtin.</span><span class="sxs-lookup"><span data-stu-id="29a2d-173">toochange hello default subscription, use hello `azure account set` command, and specify hello subscription that you wish toobe hello default.</span></span> <span data-ttu-id="29a2d-174">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="29a2d-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="29a2d-175">Bu hello varsayılan abonelik tooAzure-alt-2 değiştirir.</span><span class="sxs-lookup"><span data-stu-id="29a2d-175">This changes hello default subscription tooAzure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="29a2d-176">Merhaba varsayılan abonelik değiştirme hemen etkili olur ve genel bir değişikliktir; Yeni Azure CLI komutları, bunları çalıştırmak isteyip hello aynı komut satırı örneği veya farklı bir örnek hello yeni varsayılan abonelik kullanın.</span><span class="sxs-lookup"><span data-stu-id="29a2d-176">Changing hello default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from hello same command-line instance or a different instance, use hello new default subscription.</span></span>
>
>

<span data-ttu-id="29a2d-177">Hello Azure CLI varsayılan olmayan abonelikle toouse istiyor, ancak toochange hello geçerli varsayılan istemiyorsanız, hello kullanabilirsiniz `--subscription` seçeneği için hello komutu ve hello ad hello aboneliği hello işlemi için toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="29a2d-177">If you wish toouse a non-default subscription with hello Azure CLI, but don't want toochange hello current default, you can use hello `--subscription` option for hello command and provide hello name of hello subscription you wish toouse for hello operation.</span></span>

<span data-ttu-id="29a2d-178">Bağlı tooyour Azure aboneliğiniz olduktan sonra Azure kaynaklarıyla hello Azure CLI komutları toowork kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29a2d-178">Once you are connected tooyour Azure subscription, you can start using hello Azure CLI commands toowork with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="29a2d-179">CLI ayarlarını depolama</span><span class="sxs-lookup"><span data-stu-id="29a2d-179">Storage of CLI settings</span></span>
<span data-ttu-id="29a2d-180">Oturum hello oturumunuzu `azure login` komut veya içeri aktarma yayımlama ayarları, CLI profili ve günlükleri depolanmış bir `.azure` directory bulunan, `user` dizin.</span><span class="sxs-lookup"><span data-stu-id="29a2d-180">Whether you log in with hello `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="29a2d-181">`user` Dizin işletim sisteminiz tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="29a2d-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="29a2d-182">Ancak, ek adımlar tooencrypt almanızı öneririz, `user` dizin.</span><span class="sxs-lookup"><span data-stu-id="29a2d-182">However, we recommend that you take additional steps tooencrypt your `user` directory.</span></span> <span data-ttu-id="29a2d-183">Hello yolu izleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="29a2d-183">You can do so in hello following ways:</span></span>

* <span data-ttu-id="29a2d-184">Windows, hello dizin özelliklerini değiştirin veya BitLocker'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="29a2d-184">On Windows, modify hello directory properties or use BitLocker.</span></span>
* <span data-ttu-id="29a2d-185">Mac üzerinde FileVault üzerinde hello dizinini açın.</span><span class="sxs-lookup"><span data-stu-id="29a2d-185">On Mac, turn on FileVault for hello directory.</span></span>
* <span data-ttu-id="29a2d-186">Ubuntu üzerinde hello şifreli giriş dizini özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="29a2d-186">On Ubuntu, use hello Encrypted Home directory feature.</span></span> <span data-ttu-id="29a2d-187">Diğer Linux dağıtımları benzer özellikleri sunar.</span><span class="sxs-lookup"><span data-stu-id="29a2d-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="29a2d-188">Günlük</span><span class="sxs-lookup"><span data-stu-id="29a2d-188">Logging out</span></span>
<span data-ttu-id="29a2d-189">toolog çıkışı, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="29a2d-189">toolog out, use hello following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="29a2d-190">Merhaba abonelikleri ilişkilendirilen hello hesabı yalnızca siler hello abonelik bilgileri hello yerel profilinden günlüğü Active Directory doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="29a2d-190">If hello subscriptions associated with hello account are only authenticated with Active Directory, logging out deletes hello subscription information from hello local profile.</span></span> <span data-ttu-id="29a2d-191">Yayımlama ayarları dosyası da hello abonelikler için alındıysa, siler Active Directory ile ilgili bilgiler hello yerel profilinden yalnızca ancak oturum kapatılıyor.</span><span class="sxs-lookup"><span data-stu-id="29a2d-191">However, if a publish settings file was also imported for hello subscriptions, logging out only deletes Active Directory related information from hello local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29a2d-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="29a2d-192">Next steps</span></span>
* <span data-ttu-id="29a2d-193">bkz: toouse Azure CLI komutları [Kaynak Yöneticisi modunda Azure CLI komutları](virtual-machines/azure-cli-arm-commands.md) ve [Hizmet Yönetimi modunda Azure CLI komutları](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="29a2d-193">toouse Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="29a2d-194">toolearn hello Azure CLI hakkında daha fazla kaynak kodunu indirebilir, rapor sorunları veya toohello proje katkıda, hello ziyaret [hello Azure CLI için GitHub depo](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="29a2d-194">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="29a2d-195">Hello Azure CLI veya Azure kullanarak sorunlarla karşılaşırsanız, hello ziyaret [Azure forumları](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="29a2d-195">If you encounter problems using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
