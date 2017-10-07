---
title: aaaInstall hello Azure CLI 1.0 | Microsoft Docs
description: "Azure hizmetlerini kullanarak Mac, Linux ve Windows toostart için Azure CLI 1.0 Hello yükleyin"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="11277-103">Hello Azure CLI 1.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="11277-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11277-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11277-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="11277-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="11277-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="11277-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="11277-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="11277-107">Bu konuda, çok sayıda Resource Manager dağıtım etkinliklerini yanı sıra nasıl tooinstall hello nodeJs inşa edilmiş ve tüm Klasik dağıtım API destekleyen Azure CLI 1.0 çağırır açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="11277-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="11277-108">Merhaba kullanması gereken [Azure CLI 2.0](/cli/azure/overview) yeni veya forward-looking CLI dağıtım ve yönetimi için.</span><span class="sxs-lookup"><span data-stu-id="11277-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="11277-109">Hızlı bir şekilde hello Azure komut satırı arabirimi (Azure CLI 1.0) toouse oluşturmak ve Microsoft Azure kaynakları yönetmek için açık kaynaklı, komut kabuğu tabanlı kümesini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="11277-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="11277-110">Bu platformlar arası araçları çeşitli seçenekler tooinstall bilgisayarınızda var:</span><span class="sxs-lookup"><span data-stu-id="11277-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="11277-111">**npm paket** - çalışma npm (JavaScript için Paket Yöneticisi hello) tooinstall hello en son Azure CLI 1.0 paket Linux dağıtımı veya işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="11277-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="11277-112">Node.js ve bilgisayarınızda npm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="11277-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="11277-113">**Yükleyici** -Mac veya Windows kolay yükleme için bir yükleyici indirin.</span><span class="sxs-lookup"><span data-stu-id="11277-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="11277-114">**Docker kapsayıcısı** - başlangıç hello kullanarak en son CLI hazır Çalıştır Docker kapsayıcısı içinde.</span><span class="sxs-lookup"><span data-stu-id="11277-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="11277-115">Docker ana bilgisayarınızda gerektirir.</span><span class="sxs-lookup"><span data-stu-id="11277-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="11277-116">Daha fazla seçenekleri ve arka plan için hello proje deposu bakın [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="11277-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="11277-117">Hello Azure CLI 1.0 yüklendikten sonra [Azure aboneliğinizle bağlanmak](xplat-cli-connect.md) ve çalışma hello **azure** komutları, komut satırı arabiriminden (Bash, Terminal, komut istemi vb.) ile toowork Azure kaynaklarınızı.</span><span class="sxs-lookup"><span data-stu-id="11277-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="11277-118">Seçenek 1: bir npm paket yükleme</span><span class="sxs-lookup"><span data-stu-id="11277-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="11277-119">bir npm paketinden tooinstall hello CLI indirilir ve hello yüklü olduğundan emin olun [en son Node.js ve npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="11277-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="11277-120">Daha sonra çalıştırın **npm yükleme** tooinstall hello azure CLI paketi:</span><span class="sxs-lookup"><span data-stu-id="11277-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="11277-121">Linux dağıtımları hakkında toouse gerekebilecek **sudo** çalıştırmak toosuccessfully hello **npm** komutu, şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="11277-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="11277-122">Node.js ve npm Linux dağıtımı veya işletim sistemi güncelleştirme veya tooinstall ihtiyacınız varsa, hello en son Node.js LTS sürüm (4.x) yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="11277-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="11277-123">Eski bir sürümünü kullanıyorsanız, yükleme hataları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11277-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="11277-124">İsterseniz, indirme son Linux hello [tar dosya] [ linux-installer] hello npm paket yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="11277-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="11277-125">Ardından, hello indirilen npm paket aşağıdaki gibi yükleyin (Linux dağıtımları toouse gerekebilecek **sudo**):</span><span class="sxs-lookup"><span data-stu-id="11277-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="11277-126">Seçenek 2: bir yükleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="11277-126">Option 2: Use an installer</span></span>
<span data-ttu-id="11277-127">Mac veya Windows bilgisayarı kullanıyorsanız, CLI yükleyicileri aşağıdaki hello indirme için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="11277-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="11277-128">[Mac OS X yükleyici][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="11277-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="11277-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="11277-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="11277-130">Windows hello de indirebilirsiniz [Web Platformu yükleyicisi](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span><span class="sxs-lookup"><span data-stu-id="11277-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="11277-131">Seçenek tooinstall hello yükleyici kazandırır yükledikten sonra komut satırı araçları ve ek Azure SDK'sını hello CLI.</span><span class="sxs-lookup"><span data-stu-id="11277-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="11277-132">Seçenek 3: bir Docker kapsayıcısı kullanın</span><span class="sxs-lookup"><span data-stu-id="11277-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="11277-133">Bilgisayarınızda olarak ayarladıysanız, bir [Docker](https://docs.docker.com/engine/understanding-docker/) ana çalıştırabileceğiniz bir Docker kapsayıcısı en son Azure CLI 1.0 hello.</span><span class="sxs-lookup"><span data-stu-id="11277-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="11277-134">Çalışma hello komutu aşağıdaki (Linux dağıtımları toouse gerekebilecek **sudo**):</span><span class="sxs-lookup"><span data-stu-id="11277-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="11277-135">Azure CLI 1.0 komutlarını çalıştırın</span><span class="sxs-lookup"><span data-stu-id="11277-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="11277-136">Hello Azure CLI 1.0 yüklendikten sonra hello çalıştıracak **azure** komutu, komut satırı kullanıcı arabiriminden (Bash, Terminal, komut istemi vb.).</span><span class="sxs-lookup"><span data-stu-id="11277-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="11277-137">Örneğin, toorun hello Yardım komutu hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="11277-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="11277-138">Bazı Linux dağıtımları üzerinde benzer bir hata çok alabileceğiniz`/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="11277-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="11277-139">Bu hata /usr/bin/nodejs sırasında yüklenen Node.js son yüklemeleri gelir.</span><span class="sxs-lookup"><span data-stu-id="11277-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="11277-140">toofix, şu komutu çalıştırarak sembolik bağlantıyı çok/usr/bin/düğüm oluşturun:</span><span class="sxs-lookup"><span data-stu-id="11277-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="11277-141">hello Azure CLI yüklediğiniz, 1.0 aşağıdaki türü hello toosee hello sürümü:</span><span class="sxs-lookup"><span data-stu-id="11277-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="11277-142">Artık hazırsınız!</span><span class="sxs-lookup"><span data-stu-id="11277-142">Now you are ready!</span></span> <span data-ttu-id="11277-143">Tüm tooaccess hello CLI komutları toowork kendi kaynaklarla [tooyour Azure aboneliği hello Azure CLI ' bağlanma](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="11277-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11277-144">Azure CLI ilk kullandığınızda tooallow Microsoft toocollect kullanım bilgileri isteyip istemediğinizi soran bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="11277-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="11277-145">Katılım gönüllüdür.</span><span class="sxs-lookup"><span data-stu-id="11277-145">Participation is voluntary.</span></span> <span data-ttu-id="11277-146">Tooparticipate seçerseniz, çalıştırarak herhangi bir zamanda durdurabilirsiniz `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="11277-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="11277-147">herhangi bir zamanda tooenable katılım çalıştırmak `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="11277-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="11277-148">Merhaba CLI güncelleştir</span><span class="sxs-lookup"><span data-stu-id="11277-148">Update hello CLI</span></span>
<span data-ttu-id="11277-149">Microsoft, sık hello Azure CLI güncelleştirilmiş sürümlerini serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="11277-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="11277-150">Yeniden işletim sisteminizi hello Yükleyicisi'ni kullanarak CLI hello veya hello son Docker kapsayıcısı'nı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="11277-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="11277-151">Veya sahip Merhaba, en son Node.js ve yüklü npm hello aşağıdakileri yazarak güncelleştirmeniz (Linux dağıtımları toouse gerekebilecek **sudo**).</span><span class="sxs-lookup"><span data-stu-id="11277-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="11277-152">Sekme tamamlama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="11277-152">Enable tab completion</span></span>
<span data-ttu-id="11277-153">Sekme tamamlama CLI komutlarının Mac ve Linux için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="11277-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="11277-154">tooenable zsh, içinde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="11277-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="11277-155">tooenable bash, içinde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="11277-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="11277-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11277-156">Next steps</span></span>
* <span data-ttu-id="11277-157">[Hello CLI tooyour Azure aboneliği ' bağlanma](xplat-cli-connect.md) toocreate ve Azure kaynaklarınızı yönetmek.</span><span class="sxs-lookup"><span data-stu-id="11277-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="11277-158">toolearn hello Azure CLI hakkında daha fazla kaynak kodunu indirebilir, rapor sorunları veya toohello proje katkıda, hello ziyaret [hello Azure CLI için GitHub depo](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="11277-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="11277-159">Hello Azure CLI veya Azure kullanma hakkında sorularınız varsa, hello ziyaret [Azure forumları](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="11277-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
