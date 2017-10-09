---
title: "aaaTroubleshoot SSH bağlantı sorunlarını tooan Azure VM | Microsoft Docs"
description: "Nasıl tootroubleshoot 'SSH bağlantısı başarısız oldu' veya 'SSH bağlantı reddedildi' gibi bir Azure VM için Linux çalıştıran verir."
keywords: "SSH bağlantı reddedildi, ssh hatası, azure ssh, SSH bağlantısı başarısız oldu"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="305ea-104">SSH bağlantı tooan, hatalar, başarısız olur veya reddedilir Azure Linux VM'de sorun giderme</span><span class="sxs-lookup"><span data-stu-id="305ea-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="305ea-105">Güvenli Kabuk (SSH), SSH bağlantı hataları hatalarla veya tooconnect tooa Linux sanal makine (VM) çalıştığınızda SSH reddetti çeşitli nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="305ea-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="305ea-106">Bu makalede, bulma ve doğru hello sorunları yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="305ea-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="305ea-107">Linux tootroubleshoot için hello Azure portal, Azure CLI ya da VM erişim uzantısı kullanın ve bağlantı sorunlarını giderin.</span><span class="sxs-lookup"><span data-stu-id="305ea-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="305ea-108">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="305ea-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="305ea-109">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="305ea-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="305ea-110">Toohello Git [Azure Destek sitesi](http://azure.microsoft.com/support/options/) seçip **alma desteği**.</span><span class="sxs-lookup"><span data-stu-id="305ea-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="305ea-111">Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="305ea-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="305ea-112">Hızlı sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="305ea-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="305ea-113">Sorun giderme her adımdan sonra toohello VM yeniden bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="305ea-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="305ea-114">Merhaba SSH yapılandırmasını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="305ea-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="305ea-115">Merhaba hello kullanıcının kimlik bilgilerini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="305ea-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="305ea-116">Merhaba doğrulayın [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) kuralları SSH trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="305ea-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="305ea-117">Bir ağ güvenlik grubu kural toopermit SSH trafiği (varsayılan olarak, TCP bağlantı noktası 22) bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="305ea-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="305ea-118">Bağlantı noktası yeniden yönlendirmesine kullanamazsınız / Azure yük dengeleyici kullanmadan eşleme.</span><span class="sxs-lookup"><span data-stu-id="305ea-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="305ea-119">Merhaba denetleyin [VM kaynak durumu](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="305ea-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="305ea-120">Bu hello VM olun sağlıklı olarak rapor.</span><span class="sxs-lookup"><span data-stu-id="305ea-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="305ea-121">Önyükleme tanılaması etkin varsa, hello VM önyükleme hataları hello günlüklerine bildirmeyen doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="305ea-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="305ea-122">Merhaba VM yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="305ea-122">Restart hello VM.</span></span>
6. <span data-ttu-id="305ea-123">Merhaba VM yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="305ea-123">Redeploy hello VM.</span></span>

<span data-ttu-id="305ea-124">Daha ayrıntılı sorun giderme adımları ve açıklamalar için okuma devam edin.</span><span class="sxs-lookup"><span data-stu-id="305ea-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="305ea-125">Kullanılabilir yöntemleri tootroubleshoot SSH bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="305ea-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="305ea-126">Kimlik bilgileri veya yöntemler aşağıdaki hello birini kullanarak SSH yapılandırması sıfırlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="305ea-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="305ea-127">[Azure portal](#use-the-azure-portal) - tooquickly gerekiyorsa mükemmel hello SSH yapılandırması veya SSH anahtarı sıfırlama ve, yok sahip hello Azure Araçları yüklü.</span><span class="sxs-lookup"><span data-stu-id="305ea-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="305ea-128">[Azure CLI 2.0](#use-the-azure-cli-20) - zaten hello komut satırında hızla sıfırlama hello SSH yapılandırması veya kimlik bilgileri kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="305ea-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="305ea-129">Merhaba de kullanabilirsiniz [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="305ea-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="305ea-130">[Azure VMAccessForLinux uzantısını](#use-the-vmaccess-extension) - oluşturmak ve json tanım dosyalarını tooreset hello SSH yapılandırması veya kullanıcı kimlik bilgilerini yeniden kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="305ea-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="305ea-131">Sorun giderme her adımdan sonra tooyour VM yeniden bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="305ea-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="305ea-132">Hala bağlanamıyorsanız, sonraki adıma hello deneyin.</span><span class="sxs-lookup"><span data-stu-id="305ea-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="305ea-133">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="305ea-133">Use hello Azure portal</span></span>
<span data-ttu-id="305ea-134">Hello Azure portal, yerel bilgisayarınızda herhangi bir aracı yüklemeden hızlı şekilde tooreset hello SSH yapılandırması veya kullanıcı kimlik bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="305ea-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="305ea-135">VM hello Azure portal'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="305ea-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="305ea-136">Toohello aşağı **destek + sorun giderme** bölümünde ve seçin **parola sıfırlama** aşağıdaki örneğine hello olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="305ea-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![SSH yapılandırması veya hello Azure portal kimlik bilgilerini sıfırlama](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="305ea-138">Merhaba SSH yapılandırmasını sıfırlayın</span><span class="sxs-lookup"><span data-stu-id="305ea-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="305ea-139">İlk adım olarak, seçin `Reset configuration only` hello gelen **modu** açılır menü ekran, önceki hello gibi ardından hello **sıfırlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="305ea-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="305ea-140">Bu işlem tamamlandıktan sonra tooaccess VM'yi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="305ea-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="305ea-141">Bir kullanıcının SSH kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="305ea-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="305ea-142">Mevcut bir kullanıcının tooreset hello kimlik bilgilerini seçin ya da `Reset SSH public key` veya `Reset password` hello gelen **modu** ekran görüntüsü önceki hello olduğu gibi açılır menü.</span><span class="sxs-lookup"><span data-stu-id="305ea-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="305ea-143">Merhaba kullanıcı adı ve bir SSH anahtarı veya yeni bir parola belirtin ve ardından hello **sıfırlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="305ea-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="305ea-144">Bu menüden hello VM sudo ayrıcalıklarına sahip bir kullanıcı da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="305ea-145">Yeni kullanıcı adı ve ilişkili parolayı veya SSH anahtarını girin ve hello ardından **sıfırlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="305ea-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="305ea-146">Hello Azure CLI 2.0 kullanın</span><span class="sxs-lookup"><span data-stu-id="305ea-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="305ea-147">Henüz yapmadıysanız, hello son yükleme [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="305ea-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="305ea-148">Oluşturulan ve özel Linux disk görüntü karşıya emin hello olun [Microsoft Azure Linux Aracısı](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) sürüm 2.0.5 veya üstü yüklü.</span><span class="sxs-lookup"><span data-stu-id="305ea-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="305ea-149">Galeri görüntüleri kullanılarak oluşturulan VM'ler için bu erişim uzantısı zaten yüklenmiş ve sizin için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="305ea-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="305ea-150">SSH yapılandırmasını sıfırlayın</span><span class="sxs-lookup"><span data-stu-id="305ea-150">Reset SSH configuration</span></span>
<span data-ttu-id="305ea-151">Başlangıçta deneyin sıfırlama hello SSH yapılandırma toodefault değerlerini ve hello VM yeniden başlatılan hello SSH sunucuda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="305ea-152">Bu hello kullanıcı hesabı adı, parola veya SSH anahtarları değiştirmez olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="305ea-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="305ea-153">Merhaba aşağıdaki örnek kullanır [az vm kullanıcı sıfırlama-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH yapılandırması hello adlı VM üzerinde `myVM` içinde `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="305ea-154">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="305ea-155">Bir kullanıcının SSH kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="305ea-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="305ea-156">Merhaba aşağıdaki örnek kullanır [az vm kullanıcı güncelleştirme](/cli/azure/vm/user#update) tooreset hello kimlik bilgileri için `myUsername` belirtilen toohello değer `myPassword`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="305ea-157">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="305ea-158">SSH anahtar kimlik doğrulaması kullanıyorsanız, belirli bir kullanıcı için hello SSH anahtarı sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="305ea-159">Merhaba aşağıdaki örnek kullanır **az vm erişim kümesi linux kullanıcı** tooupdate hello SSH anahtarı depolanır `~/.ssh/id_rsa.pub` adlı hello kullanıcı için `myUsername`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="305ea-160">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="305ea-161">Merhaba VMAccess uzantısını kullanın</span><span class="sxs-lookup"><span data-stu-id="305ea-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="305ea-162">Merhaba Linux VM erişim uzantısını Eylemler toocarry çıkışı tanımlayan bir json dosyası olarak okur. Bu eylemler SSHD sıfırlama, bir SSH anahtarı sıfırlanıyor veya bir kullanıcı ekleme içerir.</span><span class="sxs-lookup"><span data-stu-id="305ea-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="305ea-163">Hala hello Azure CLI toocall hello VMAccess uzantısını kullanır ancak hello json dosyaları arasında birden çok VM isterseniz yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="305ea-164">Bu yaklaşım toocreate sonra için senaryoları çağrılabilir json dosyalarınızın bir havuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="305ea-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="305ea-165">SSHD Sıfırla</span><span class="sxs-lookup"><span data-stu-id="305ea-165">Reset SSHD</span></span>
<span data-ttu-id="305ea-166">Adlı bir dosya oluşturun `settings.json` içeriği aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="305ea-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="305ea-167">Hello Azure CLI kullanarak, ardından hello çağırırsınız `VMAccessForLinux` uzantısı tooreset json dosyanız belirterek SSHD bağlantınızı.</span><span class="sxs-lookup"><span data-stu-id="305ea-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="305ea-168">Merhaba aşağıdaki örnek kullanır [az vm uzantısı kümesi](/cli/azure/vm/extension#set) tooreset SSHD hello adlı VM üzerinde `myVM` içinde `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="305ea-169">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="305ea-170">Bir kullanıcının SSH kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="305ea-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="305ea-171">SSHD toofunction doğru görünüyorsa, hello kullanıcının kimlik bilgilerini bir tireyle sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="305ea-172">tooreset hello bir kullanıcının parolasını adlı bir dosya oluşturun `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="305ea-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="305ea-173">Merhaba aşağıdaki örnek sıfırlar hello kimlik bilgilerini `myUsername` belirtilen toohello değer `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="305ea-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="305ea-174">Satırlara aşağıdaki hello girin, `settings.json` dosya, kendi değerlerini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="305ea-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="305ea-175">Veya SSH anahtarı bir kullanıcı için Merhaba, ilk adlı bir dosya oluşturun tooreset `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="305ea-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="305ea-176">Merhaba aşağıdaki örnek sıfırlar hello kimlik bilgilerini `myUsername` belirtilen toohello değer `myPassword`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="305ea-177">Satırlara aşağıdaki hello girin, `settings.json` dosya, kendi değerlerini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="305ea-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="305ea-178">Json dosyanızı oluşturduktan sonra hello Azure CLI toocall hello kullan `VMAccessForLinux` SSH kullanıcı kimlik bilgileri json dosyanız belirterek uzantısı tooreset.</span><span class="sxs-lookup"><span data-stu-id="305ea-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="305ea-179">Merhaba aşağıdaki örnek sıfırlar hello adlı VM kimlik bilgisi `myVM` içinde `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="305ea-180">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="305ea-181">Hello Azure CLI 1.0 kullanın</span><span class="sxs-lookup"><span data-stu-id="305ea-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="305ea-182">Henüz yapmadıysanız [hello Azure CLI 1.0 yükleyin ve tooyour Azure aboneliğine bağlanma](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="305ea-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="305ea-183">Resource Manager moduna gibi kullandığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="305ea-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="305ea-184">Oluşturulan ve özel Linux disk görüntü karşıya emin hello olun [Microsoft Azure Linux Aracısı](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) sürüm 2.0.5 veya üstü yüklü.</span><span class="sxs-lookup"><span data-stu-id="305ea-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="305ea-185">Galeri görüntüleri kullanılarak oluşturulan VM'ler için bu erişim uzantısı zaten yüklenmiş ve sizin için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="305ea-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="305ea-186">SSH yapılandırmasını sıfırlayın</span><span class="sxs-lookup"><span data-stu-id="305ea-186">Reset SSH configuration</span></span>
<span data-ttu-id="305ea-187">Merhaba SSHD yapılandırma kendisini yanlış veya hello hizmeti bir hatayla karşılaştı.</span><span class="sxs-lookup"><span data-stu-id="305ea-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="305ea-188">SSHD toomake hello SSH yapılandırması kendisini geçerli olduğundan emin sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="305ea-189">SSHD sıfırlama hello ilk sorun giderme adımı gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="305ea-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="305ea-190">Merhaba aşağıdaki örnek sıfırlar adlı VM üzerinde SSHD `myVM` adlı hello kaynak grubunda `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="305ea-191">Kendi VM ve kaynak grubu adları şu şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="305ea-192">Bir kullanıcının SSH kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="305ea-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="305ea-193">SSHD toofunction doğru görünüyorsa, tireyle kullanıcıya hello parolayı sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="305ea-194">Merhaba aşağıdaki örnek sıfırlar hello kimlik bilgilerini `myUsername` belirtilen toohello değer `myPassword`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="305ea-195">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="305ea-196">SSH anahtar kimlik doğrulaması kullanıyorsanız, belirli bir kullanıcı için hello SSH anahtarı sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="305ea-197">Şu örnek güncelleştirmeleri hello hello depolanan SSH anahtarı `~/.ssh/id_rsa.pub` adlı hello kullanıcı için `myUsername`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="305ea-198">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="305ea-199">Bir VM’yi yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="305ea-199">Restart a VM</span></span>
<span data-ttu-id="305ea-200">Merhaba SSH yapılandırması ve kullanıcı kimlik bilgilerini sıfırlamak veya Bunun yapılması bir hatayla karşılaştı, temel alınan işlem sorunları hello VM tooaddress yeniden başlatmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="305ea-201">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="305ea-201">Azure portal</span></span>
<span data-ttu-id="305ea-202">kullanarak bir VM toorestart hello Azure portal, select tıklayın ve VM hello **yeniden** aşağıdaki örneğine hello olduğu gibi düğmesi:</span><span class="sxs-lookup"><span data-stu-id="305ea-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Bir VM hello Azure portalında yeniden başlatın](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="305ea-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="305ea-204">Azure CLI 1.0</span></span>
<span data-ttu-id="305ea-205">Aşağıdaki örnek yeniden hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="305ea-206">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="305ea-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="305ea-207">Azure CLI 2.0</span></span>
<span data-ttu-id="305ea-208">Merhaba aşağıdaki örnek kullanır [az vm yeniden başlatma](/cli/azure/vm#restart) toorestart hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="305ea-209">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="305ea-210">Bir VM’yi yeniden dağıtma</span><span class="sxs-lookup"><span data-stu-id="305ea-210">Redeploy a VM</span></span>
<span data-ttu-id="305ea-211">Temel ağ sorunları düzeltebilir Azure VM tooanother düğümde yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="305ea-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="305ea-212">Bir VM dağıtarak hakkında daha fazla bilgi için bkz: [dağıtmanız sanal makine toonew Azure düğümü](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="305ea-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="305ea-213">Bu işlem tamamlandıktan sonra kısa ömürlü disk veriler kaybolur ve hello sanal makineyle ilişkili olan dinamik IP adreslerini güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="305ea-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="305ea-214">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="305ea-214">Azure portal</span></span>
<span data-ttu-id="305ea-215">kullanarak bir VM tooredeploy hello Azure portal, select toohello aşağı kaydırın ve VM **destek + sorun giderme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="305ea-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="305ea-216">Hello tıklatın **dağıtmanız** aşağıdaki örneğine hello olduğu gibi düğmesi:</span><span class="sxs-lookup"><span data-stu-id="305ea-216">Click hello **Redeploy** button as in hello following example:</span></span>

![VM hello Azure portal ile yeniden dağıtın](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="305ea-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="305ea-218">Azure CLI 1.0</span></span>
<span data-ttu-id="305ea-219">Aşağıdaki örnek yeniden dağıtır hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="305ea-220">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="305ea-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="305ea-221">Azure CLI 2.0</span></span>
<span data-ttu-id="305ea-222">Merhaba örnek kullanım [az vm dağıtın](/cli/azure/vm#redeploy) tooredeploy hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="305ea-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="305ea-223">Kendi değerlerinizi aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="305ea-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="305ea-224">Merhaba Klasik dağıtım modeli kullanılarak oluşturulan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="305ea-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="305ea-225">Merhaba Klasik dağıtım modeli kullanılarak oluşturulmuş olan VM'ler için bu adımları tooresolve hello en sık karşılaşılan SSH bağlantı hataları deneyin.</span><span class="sxs-lookup"><span data-stu-id="305ea-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="305ea-226">Her adımdan sonra toohello VM yeniden bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="305ea-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="305ea-227">Uzaktan Erişim'hello sıfırlama [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="305ea-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="305ea-228">Üzerinde Azure portal Merhaba, VM'yi seçin ve hello tıklatın **uzaktan Sıfırla...**  düğmesi.</span><span class="sxs-lookup"><span data-stu-id="305ea-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="305ea-229">Merhaba VM yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="305ea-229">Restart hello VM.</span></span> <span data-ttu-id="305ea-230">Merhaba üzerinde [Azure portal](https://portal.azure.com), VM'yi seçin ve hello tıklatın **yeniden** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="305ea-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="305ea-231">Merhaba VM tooa yeni Azure düğümü yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="305ea-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="305ea-232">Hakkında bilgi için tooredeploy bir VM bkz [dağıtmanız sanal makine toonew Azure düğümü](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="305ea-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="305ea-233">Bu işlem tamamlandıktan sonra kısa ömürlü disk veriler kaybolur ve hello sanal makineyle ilişkili olan dinamik IP adreslerini güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="305ea-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="305ea-234">Merhaba yönergeleri izleyin [nasıl tooreset bir parola veya SSH Linux tabanlı sanal makineler için](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) için:</span><span class="sxs-lookup"><span data-stu-id="305ea-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="305ea-235">Merhaba parolayı veya SSH anahtarını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="305ea-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="305ea-236">Oluşturma bir *sudo* kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="305ea-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="305ea-237">Merhaba SSH yapılandırmasını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="305ea-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="305ea-238">Platform sorunları için Hello VM'nin kaynak sistem durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="305ea-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="305ea-239">VM seçin ve aşağı kaydırarak **ayarları** > **durum denetimi**.</span><span class="sxs-lookup"><span data-stu-id="305ea-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="305ea-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="305ea-240">Additional resources</span></span>
* <span data-ttu-id="305ea-241">Aşağıdaki adımlar hello sonra hala tooSSH tooyour VM olup olmadığını görmek [sorun giderme adımlarını ayrıntılı](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview ek adımlar tooresolve sorununuzu.</span><span class="sxs-lookup"><span data-stu-id="305ea-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="305ea-242">Uygulama erişimi sorunlarını giderme hakkında daha fazla bilgi için bkz: [bir Azure sanal makine üzerinde çalışan sorun giderme erişim tooan uygulama](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="305ea-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="305ea-243">Merhaba Klasik dağıtım modeli kullanılarak oluşturulan sanal makineler sorunlarını giderme hakkında daha fazla bilgi için bkz: [nasıl tooreset bir parola veya SSH Linux tabanlı sanal makineler için](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="305ea-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

