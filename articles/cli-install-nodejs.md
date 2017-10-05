---
title: "1.0 Azure CLI'yı yükleme | Microsoft Docs"
description: "Mac, Linux ve Windows Azure hizmetlerini kullanmaya başlamak Azure CLI 1.0 yükleyin"
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
ms.openlocfilehash: 63b35ed25b809a16b61b685fd35aa67474b0a369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-cli-10"></a><span data-ttu-id="0e4b6-103">1.0 Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="0e4b6-103">Install the Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e4b6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e4b6-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="0e4b6-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0e4b6-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="0e4b6-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0e4b6-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="0e4b6-107">Bu konu, nodeJs üzerinde inşa edilmiş ve çok sayıda Resource Manager dağıtım etkinliklerini yanı sıra tüm Klasik dağıtım API çağrıları destekleyen Azure CLI 1.0 yüklemeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-107">This topic describes how to install the Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="0e4b6-108">Kullanmanız gereken [Azure CLI 2.0](/cli/azure/overview) yeni veya forward-looking CLI dağıtım ve yönetimi için.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-108">You should use the [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="0e4b6-109">Hızlı bir şekilde arabirimi oluşturmak ve Microsoft Azure kaynakları yönetmek için açık kaynak kabuk tabanlı komut kümesini kullanmak için Azure komut satırı (Azure CLI 1.0) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="0e4b6-110">Bu platformlar arası araçları bilgisayarınıza yüklemek için birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="0e4b6-110">You have several options to install these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="0e4b6-111">**npm paket** -Linux dağıtım ya da OS en son Azure CLI 1.0 paketini yüklemek için npm (JavaScript için Paket Yöneticisi) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="0e4b6-112">Node.js ve bilgisayarınızda npm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="0e4b6-113">**Yükleyici** -Mac veya Windows kolay yükleme için bir yükleyici indirin.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="0e4b6-114">**Docker kapsayıcısı** - hazır Çalıştır Docker kapsayıcısı içinde son CLI kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="0e4b6-115">Docker ana bilgisayarınızda gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="0e4b6-116">Daha fazla seçenekleri ve arka plan için proje deposu bakın [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="0e4b6-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="0e4b6-117">Azure CLI 1.0 yüklendikten sonra [Azure aboneliğinizle bağlanmak](xplat-cli-connect.md) çalıştırıp **azure** çalışmak için komut satırı arabiriminden (Bash, Terminal, komut istemi vb.) komutları, Azure kaynakları.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="0e4b6-118">Seçenek 1: bir npm paket yükleme</span><span class="sxs-lookup"><span data-stu-id="0e4b6-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="0e4b6-119">CLI bir npm paket yüklemek için indirilir ve yüklenir emin olun [en son Node.js ve npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="0e4b6-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="0e4b6-120">Daha sonra çalıştırın **npm yükleme** azure CLI paketini yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="0e4b6-120">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="0e4b6-121">Linux dağıtımları hakkında kullanmanız gerekebilir **sudo** başarıyla çalışması için **npm** komutu, şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="0e4b6-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="0e4b6-122">Yükleme veya güncelleştirme Node.js ve Linux dağıtımı veya işletim sistemi npm ihtiyacınız varsa, en son Node.js LTS sürüm (4.x) yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-122">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="0e4b6-123">Eski bir sürümünü kullanıyorsanız, yükleme hataları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="0e4b6-124">Tercih ederseniz, en son Linux karşıdan [tar dosya] [ linux-installer] yerel olarak npm paket için.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span></span> <span data-ttu-id="0e4b6-125">Daha sonra indirilen npm paket aşağıdaki gibi yükleyin (Linux dağıtımları kullanmanız gerekebilir üzerinde **sudo**):</span><span class="sxs-lookup"><span data-stu-id="0e4b6-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span></span>

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="0e4b6-126">Seçenek 2: bir yükleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="0e4b6-126">Option 2: Use an installer</span></span>
<span data-ttu-id="0e4b6-127">Mac veya Windows bilgisayarı kullanıyorsanız, aşağıdaki CLI yükleyicileri indirme için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="0e4b6-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span></span>

* <span data-ttu-id="0e4b6-128">[Mac OS X yükleyici][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="0e4b6-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="0e4b6-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="0e4b6-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="0e4b6-130">Windows üzerinde de indirebilirsiniz [Web Platformu yükleyicisi](https://go.microsoft.com/?linkid=9828653) CLI yükleme.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-130">On Windows, you can also download the [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) to install the CLI.</span></span> <span data-ttu-id="0e4b6-131">Bu yükleyici CLI yükledikten sonra ek Azure SDK ve komut satırı araçlarını yüklemek için seçeneği sunar.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-131">This installer gives you the option to install additional Azure SDK and command-line tools after installing the CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="0e4b6-132">Seçenek 3: bir Docker kapsayıcısı kullanın</span><span class="sxs-lookup"><span data-stu-id="0e4b6-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="0e4b6-133">Bilgisayarınızda olarak ayarladıysanız, bir [Docker](https://docs.docker.com/engine/understanding-docker/) konak, en son Azure CLI 1.0 Docker kapsayıcısı içinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="0e4b6-134">Aşağıdaki komutu çalıştırın (Linux dağıtımları kullanmanız gerekebilir üzerinde **sudo**):</span><span class="sxs-lookup"><span data-stu-id="0e4b6-134">Run the following command (on Linux distributions you might need to use **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="0e4b6-135">Azure CLI 1.0 komutlarını çalıştırın</span><span class="sxs-lookup"><span data-stu-id="0e4b6-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="0e4b6-136">Azure CLI 1.0 yüklendikten sonra çalıştıracak **azure** komutu, komut satırı kullanıcı arabiriminden (Bash, Terminal, komut istemi vb.).</span><span class="sxs-lookup"><span data-stu-id="0e4b6-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="0e4b6-137">Örneğin, Yardım komutu çalıştırmak için aşağıdakini yazın:</span><span class="sxs-lookup"><span data-stu-id="0e4b6-137">For example, to run the help command, type the following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="0e4b6-138">Bazı Linux dağıtımları üzerinde benzer bir hata iletisi alabilirsiniz `/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-138">On some Linux distributions, you may receive an error similar to `/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="0e4b6-139">Bu hata /usr/bin/nodejs sırasında yüklenen Node.js son yüklemeleri gelir.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="0e4b6-140">Sorunu gidermek için şu komutu çalıştırarak /usr/bin/node sembolik bağlantı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0e4b6-140">To fix it, create a symbolic link to /usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="0e4b6-141">Azure CLI 1.0, yüklü sürümünü görmek için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="0e4b6-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="0e4b6-142">Artık hazırsınız!</span><span class="sxs-lookup"><span data-stu-id="0e4b6-142">Now you are ready!</span></span> <span data-ttu-id="0e4b6-143">Kendi kaynakları ile çalışmak için tüm CLI komutlara erişmek için [Azure CLI üzerinden Azure aboneliğinize bağlanmak](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0e4b6-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0e4b6-144">Azure CLI ilk kullandığınızda Microsoft kullanım bilgilerini toplamasına izin vermek isteyip istemediğinizi soran bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-144">When you first use Azure CLI, you see a message asking if you want to allow Microsoft to collect usage information.</span></span> <span data-ttu-id="0e4b6-145">Katılım gönüllüdür.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-145">Participation is voluntary.</span></span> <span data-ttu-id="0e4b6-146">Katılmayı seçerseniz, çalıştırarak herhangi bir zamanda durdurabilirsiniz `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-146">If you choose to participate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="0e4b6-147">Katılım herhangi bir zamanda etkinleştirmek için çalıştırın `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-147">To enable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-the-cli"></a><span data-ttu-id="0e4b6-148">CLI’yı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0e4b6-148">Update the CLI</span></span>
<span data-ttu-id="0e4b6-149">Microsoft Azure CLI güncelleştirilmiş sürümlerini sık serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-149">Microsoft frequently releases updated versions of the Azure CLI.</span></span> <span data-ttu-id="0e4b6-150">İşletim sisteminizi Yükleyicisi'ni kullanarak CLI yeniden yükleyin veya son Docker kapsayıcısı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span></span> <span data-ttu-id="0e4b6-151">Veya, en son Node.js ve yüklü npm varsa, aşağıdakini yazarak güncelleştirmeniz (kullanmanız gerekebilir Linux dağıtımları hakkında **sudo**).</span><span class="sxs-lookup"><span data-stu-id="0e4b6-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="0e4b6-152">Sekme tamamlama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0e4b6-152">Enable tab completion</span></span>
<span data-ttu-id="0e4b6-153">Sekme tamamlama CLI komutlarının Mac ve Linux için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="0e4b6-154">İçinde zsh etkinleştirmek için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0e4b6-154">To enable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="0e4b6-155">Bash'te etkinleştirmek için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0e4b6-155">To enable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="0e4b6-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e4b6-156">Next steps</span></span>
* <span data-ttu-id="0e4b6-157">[CLI üzerinden Azure aboneliğinize bağlanmak](xplat-cli-connect.md) oluşturmak ve Azure kaynaklarınızı yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="0e4b6-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span></span>
* <span data-ttu-id="0e4b6-158">Projeye katkıda ya da Azure CLI, yükleme kaynak kodu, rapor sorunları hakkında daha fazla bilgi için ziyaret [Azure CLI için GitHub depo](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="0e4b6-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="0e4b6-159">Azure CLI veya Azure kullanma hakkında sorularınız varsa, ziyaret [Azure forumları](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="0e4b6-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
