---
title: "aaaUse Hadoop - Azure Hdınsight ile SSH | Microsoft Docs"
description: "Secure Shell (SSH) kullanarak HDInsight'a erişebilirsiniz. Bu belge, tooHDInsight kullanarak hello ssh ve scp komutları Windows, Linux, Unix ya da macOS istemcilerden bağlanma hakkında bilgi sağlar."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "linux’taki hadoop komutları,hadoop linux komutları,hadoop macos,ssh hadoop,ssh hadoop kümesi"
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a><span data-ttu-id="fcbfb-105">SSH kullanarak tooHDInsight (Hadoop) bağlanma</span><span class="sxs-lookup"><span data-stu-id="fcbfb-105">Connect tooHDInsight (Hadoop) using SSH</span></span>

<span data-ttu-id="fcbfb-106">Bilgi nasıl toouse [güvenli Kabuk (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely tooHadoop Azure hdınsight'ta bağlanın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-106">Learn how toouse [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely connect tooHadoop on Azure HDInsight.</span></span> 

<span data-ttu-id="fcbfb-107">Hdınsight Linux (Ubuntu) hello Hadoop küme içindeki düğümler hello işletim sistemi olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-107">HDInsight can use Linux (Ubuntu) as hello operating system for nodes within hello Hadoop cluster.</span></span> <span data-ttu-id="fcbfb-108">Merhaba aşağıdaki tabloda bir SSH istemcisi kullanarak tooLinux tabanlı Hdınsight bağlanırken gereken hello adresi ve bağlantı noktası bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-108">hello following table contains hello address and port information needed when connecting tooLinux-based HDInsight using an SSH client:</span></span>

| <span data-ttu-id="fcbfb-109">Adres</span><span class="sxs-lookup"><span data-stu-id="fcbfb-109">Address</span></span> | <span data-ttu-id="fcbfb-110">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="fcbfb-110">Port</span></span> | <span data-ttu-id="fcbfb-111">Bağlandığı yer...</span><span class="sxs-lookup"><span data-stu-id="fcbfb-111">Connects to...</span></span> |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | <span data-ttu-id="fcbfb-112">22</span><span class="sxs-lookup"><span data-stu-id="fcbfb-112">22</span></span> | <span data-ttu-id="fcbfb-113">Kenar düğümü (HDInsight üzerinde R Sunucusu)</span><span class="sxs-lookup"><span data-stu-id="fcbfb-113">Edge node (R Server on HDInsight)</span></span> |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="fcbfb-114">22</span><span class="sxs-lookup"><span data-stu-id="fcbfb-114">22</span></span> | <span data-ttu-id="fcbfb-115">Kenar düğümü (bir kenar düğümü varsa diğer küme türleri)</span><span class="sxs-lookup"><span data-stu-id="fcbfb-115">Edge node (any other cluster type, if an edge node exists)</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="fcbfb-116">22</span><span class="sxs-lookup"><span data-stu-id="fcbfb-116">22</span></span> | <span data-ttu-id="fcbfb-117">Birincil baş düğüm</span><span class="sxs-lookup"><span data-stu-id="fcbfb-117">Primary headnode</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="fcbfb-118">23</span><span class="sxs-lookup"><span data-stu-id="fcbfb-118">23</span></span> | <span data-ttu-id="fcbfb-119">İkincil baş düğüm</span><span class="sxs-lookup"><span data-stu-id="fcbfb-119">Secondary headnode</span></span> |

> [!NOTE]
> <span data-ttu-id="fcbfb-120">Değiştir `<edgenodename>` hello kenar düğümüne hello adı.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-120">Replace `<edgenodename>` with hello name of hello edge node.</span></span>
>
> <span data-ttu-id="fcbfb-121">Değiştir `<clustername>` kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-121">Replace `<clustername>` with hello name of your cluster.</span></span>
>
> <span data-ttu-id="fcbfb-122">Kümeniz bir kenar düğümüne içeriyorsa öneririz, __zaman toohello kenar düğümüne bağlanabilirsiniz__ SSH kullanarak.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-122">If your cluster contains an edge node, we recommend that you __always connect toohello edge node__ using SSH.</span></span> <span data-ttu-id="fcbfb-123">Merhaba baş düğümler Hadoop kritik toohello durumunu hizmetlerini barındırır.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-123">hello head nodes host services that are critical toohello health of Hadoop.</span></span> <span data-ttu-id="fcbfb-124">Merhaba kenar düğümüne yalnızca ne üzerinde yerleştirdiğiniz çalışır.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-124">hello edge node runs only what you put on it.</span></span>
>
> <span data-ttu-id="fcbfb-125">Kenar düğümlerini kullanma hakkında daha fazla bilgi için bkz. [HDInsight’ta kenar düğümlerini kullanma](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span><span class="sxs-lookup"><span data-stu-id="fcbfb-125">For more information on using edge nodes, see [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span></span>

## <a name="ssh-clients"></a><span data-ttu-id="fcbfb-126">SSH istemcileri</span><span class="sxs-lookup"><span data-stu-id="fcbfb-126">SSH clients</span></span>

<span data-ttu-id="fcbfb-127">Linux ve UNIX macOS sistemleri sağlar hello `ssh` ve `scp` komutları.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-127">Linux, Unix, and macOS systems provide hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="fcbfb-128">Merhaba `ssh` yaygın olarak kullanılan toocreate bir Linux veya UNIX tabanlı bir sistemi uzaktan komut satırı oturumla bir istemcidir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-128">hello `ssh` client is commonly used toocreate a remote command-line session with a Linux or Unix-based system.</span></span> <span data-ttu-id="fcbfb-129">Merhaba `scp` istemcidir kullanılan toosecurely kopya dosyalarını, istemci ve hello uzak sistem arasında.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-129">hello `scp` client is used toosecurely copy files between your client and hello remote system.</span></span>

<span data-ttu-id="fcbfb-130">Microsoft Windows, varsayılan olarak SSH istemcisi sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-130">Microsoft Windows does not provide any SSH clients by default.</span></span> <span data-ttu-id="fcbfb-131">Merhaba `ssh` ve `scp` istemcileridir paketleri aşağıdaki hello ile Windows için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-131">hello `ssh` and `scp` clients are available for Windows through hello following packages:</span></span>

* <span data-ttu-id="fcbfb-132">[Azure bulut Kabuk](../cloud-shell/quickstart.md): hello bulut Kabuk tarayıcınızda Bash ortamı sağlar ve hello sağlar `ssh`, `scp`ve diğer ortak Linux komutlarını.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): hello Cloud Shell provides a Bash environment in your browser, and provides hello `ssh`, `scp`, and other common Linux commands.</span></span>

* <span data-ttu-id="fcbfb-133">[Windows 10 Ubuntu bash](https://msdn.microsoft.com/commandline/wsl/about): Merhaba `ssh` ve `scp` komutları Windows komut satırında hello Bash üzerinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-133">[Bash on Ubuntu on Windows 10](https://msdn.microsoft.com/commandline/wsl/about): hello `ssh` and `scp` commands are available through hello Bash on Windows command line.</span></span>

* <span data-ttu-id="fcbfb-134">[Git (https://git-scm.com/)](https://git-scm.com/): Merhaba `ssh` ve `scp` komutları hello Gitbash'i komut satırı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-134">[Git (https://git-scm.com/)](https://git-scm.com/): hello `ssh` and `scp` commands are available through hello GitBash command line.</span></span>

* <span data-ttu-id="fcbfb-135">[GitHub Masaüstü (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` ve `scp` komutları hello GitHub Kabuk komut satırı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-135">[GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` and `scp` commands are available through hello GitHub Shell command line.</span></span> <span data-ttu-id="fcbfb-136">GitHub Masaüstü hello Git Kabuk komut satırı hello olarak yapılandırılmış toouse Bash, hello Windows komut istemi veya PowerShell olabilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-136">GitHub Desktop can be configured toouse Bash, hello Windows Command Prompt, or PowerShell as hello command line for hello Git Shell.</span></span>

* <span data-ttu-id="fcbfb-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell takım OpenSSH tooWindows taşıma ve test sürümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell team is porting OpenSSH tooWindows, and provides test releases.</span></span>

    > [!WARNING]
    > <span data-ttu-id="fcbfb-138">Merhaba OpenSSH paketi içerir hello SSH sunucu bileşeni, `sshd`.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-138">hello OpenSSH package includes hello SSH server component, `sshd`.</span></span> <span data-ttu-id="fcbfb-139">Bu bileşen SSH sunucusu diğerlerine izin veren sisteminizde başlatır tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-139">This component starts an SSH server on your system, allowing others tooconnect tooit.</span></span> <span data-ttu-id="fcbfb-140">Bu bileşen yapılandırmazsanız veya sisteminizde toohost SSH sunucusu istemediğiniz sürece bağlantı noktası 22'ni açın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-140">Do not configure this component or open port 22 unless you want toohost an SSH server on your system.</span></span> <span data-ttu-id="fcbfb-141">Hdınsight ile gerekli toocommunicate değil.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-141">It is not required toocommunicate with HDInsight.</span></span>

<span data-ttu-id="fcbfb-142">Ayrıca [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) ve [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/) gibi çeşitli grafiksel SSH istemcisi mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-142">There are also several graphical SSH clients, such as [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) and [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/).</span></span> <span data-ttu-id="fcbfb-143">Bu istemciler kullanılan tooconnect tooHDInsight olabilirler, ancak bağlanma hello hello kullanmaktan farklı işlemidir `ssh` yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-143">While these clients can be used tooconnect tooHDInsight, hello process of connecting is different than using hello `ssh` utility.</span></span> <span data-ttu-id="fcbfb-144">Daha fazla bilgi için kullanmakta olduğunuz hello grafik istemcisinin hello belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-144">For more information, see hello documentation of hello graphical client you are using.</span></span>

## <span data-ttu-id="fcbfb-145"><a id="sshkey"></a>Kimlik doğrulaması: SSH Anahtarları</span><span class="sxs-lookup"><span data-stu-id="fcbfb-145"><a id="sshkey"></a>Authentication: SSH Keys</span></span>

<span data-ttu-id="fcbfb-146">SSH anahtarları kullanmak [ortak anahtar şifrelemesini](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH oturumları.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-146">SSH keys use [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH sessions.</span></span> <span data-ttu-id="fcbfb-147">SSH anahtarları parolalara göre daha güvenli ve bir kolay bir yolu toosecure erişim tooyour Hadoop kümesi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-147">SSH keys are more secure than passwords, and provide an easy way toosecure access tooyour Hadoop cluster.</span></span>

<span data-ttu-id="fcbfb-148">Bir anahtar kullanarak SSH hesabınızı güvenli, hello istemci bağlandığınızda özel anahtarı eşleşen hello sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-148">If your SSH account is secured using a key, hello client must provide hello matching private key when you connect:</span></span>

* <span data-ttu-id="fcbfb-149">Çoğu istemciler yapılandırılmış toouse olabilir bir __varsayılan anahtar__.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-149">Most clients can be configured toouse a __default key__.</span></span> <span data-ttu-id="fcbfb-150">Örneğin, hello `ssh` bir özel anahtar, istemci arar `~/.ssh/id_rsa` Linux ve UNIX ortamlarla.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-150">For example, hello `ssh` client looks for a private key at `~/.ssh/id_rsa` on Linux and Unix environments.</span></span>

* <span data-ttu-id="fcbfb-151">Merhaba belirtebilirsiniz __yolu tooa özel anahtarı__.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-151">You can specify hello __path tooa private key__.</span></span> <span data-ttu-id="fcbfb-152">Merhaba ile `ssh` istemcisi, hello `-i` kullanılan toospecify hello yol tooprivate anahtarını bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-152">With hello `ssh` client, hello `-i` parameter is used toospecify hello path tooprivate key.</span></span> <span data-ttu-id="fcbfb-153">Örneğin, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-153">For example, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span></span>

* <span data-ttu-id="fcbfb-154">Farklı sunucularla kullanılacak __birden fazla özel anahtarınız__ varsa [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent) gibi bir yardımcı program kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-154">If you have __multiple private keys__ for use with different servers, consider using a utility such as [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent).</span></span> <span data-ttu-id="fcbfb-155">Merhaba `ssh-agent` yardımcı programı bir SSH oturumu oluşturulurken kullanılan tooautomatically select hello anahtar toouse olabilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-155">hello `ssh-agent` utility can be used tooautomatically select hello key toouse when establishing an SSH session.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="fcbfb-156">Özel anahtarınızı bir parola ile güvenli, başlangıç anahtarı kullanırken hello parola girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-156">If you secure your private key with a passphrase, you must enter hello passphrase when using hello key.</span></span> <span data-ttu-id="fcbfb-157">Yardımcı programlar gibi `ssh-agent` hello parola size kolaylık sağlamak için önbelleğe alabilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-157">Utilities such as `ssh-agent` can cache hello password for your convenience.</span></span>

### <a name="create-an-ssh-key-pair"></a><span data-ttu-id="fcbfb-158">SSH anahtar çifti oluşturma</span><span class="sxs-lookup"><span data-stu-id="fcbfb-158">Create an SSH key pair</span></span>

<span data-ttu-id="fcbfb-159">Kullanım hello `ssh-keygen` toocreate ortak ve özel anahtar dosyaları komutu.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-159">Use hello `ssh-keygen` command toocreate public and private key files.</span></span> <span data-ttu-id="fcbfb-160">Merhaba aşağıdaki komutu Hdınsight ile kullanılabilir 2048 bit RSA anahtar çifti oluşturur:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-160">hello following command generates a 2048-bit RSA key pair that can be used with HDInsight:</span></span>

    ssh-keygen -t rsa -b 2048

<span data-ttu-id="fcbfb-161">Merhaba anahtar oluşturma işlemi sırasında bilgileri istenir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-161">You are prompted for information during hello key creation process.</span></span> <span data-ttu-id="fcbfb-162">Örneğin, hello anahtarları depolandığı veya toouse bir parola.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-162">For example, where hello keys are stored or whether toouse a passphrase.</span></span> <span data-ttu-id="fcbfb-163">Merhaba işlemi tamamlandıktan sonra iki dosya oluşturulur; Ortak anahtar ve özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-163">After hello process completes, two files are created; a public key and a private key.</span></span>

* <span data-ttu-id="fcbfb-164">Merhaba __ortak anahtar__ kullanılan toocreate Hdınsight kümesi değil.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-164">hello __public key__ is used toocreate an HDInsight cluster.</span></span> <span data-ttu-id="fcbfb-165">Merhaba ortak anahtara sahip bir uzantısı olarak `.pub`.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-165">hello public key has an extension of `.pub`.</span></span>

* <span data-ttu-id="fcbfb-166">Merhaba __özel anahtarı__ istemci toohello Hdınsight kümenize kullanılan tooauthenticate değil.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-166">hello __private key__ is used tooauthenticate your client toohello HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcbfb-167">Anahtarlarınızın güvenliğini şifre ile sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-167">You can secure your keys using a passphrase.</span></span> <span data-ttu-id="fcbfb-168">Parola, aslında özel anahtarınız üzerindeki bir şifredir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-168">A passphrase is effectively a password on your private key.</span></span> <span data-ttu-id="fcbfb-169">Birisi özel anahtarınızı edinir olsa bile, bunlar hello parola toouse hello anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-169">Even if someone obtains your private key, they must have hello passphrase toouse hello key.</span></span>

### <a name="create-hdinsight-using-hello-public-key"></a><span data-ttu-id="fcbfb-170">Merhaba ortak anahtarı kullanılarak Hdınsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="fcbfb-170">Create HDInsight using hello public key</span></span>

| <span data-ttu-id="fcbfb-171">Oluşturma yöntemi</span><span class="sxs-lookup"><span data-stu-id="fcbfb-171">Creation method</span></span> | <span data-ttu-id="fcbfb-172">Nasıl toouse hello ortak anahtar</span><span class="sxs-lookup"><span data-stu-id="fcbfb-172">How toouse hello public key</span></span> |
| ------- | ------- |
| <span data-ttu-id="fcbfb-173">**Azure portal**</span><span class="sxs-lookup"><span data-stu-id="fcbfb-173">**Azure portal**</span></span> | <span data-ttu-id="fcbfb-174">İşaretini __küme oturum açma aynı parolayı kullanın__ve ardından __ortak anahtar__ SSH kimlik doğrulama türü hello gibi.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-174">Uncheck __Use same password as cluster login__, and then select __Public Key__ as hello SSH authentication type.</span></span> <span data-ttu-id="fcbfb-175">Son olarak, hello ortak anahtar dosyası seçin veya hello hello metin hello dosyasının içeriğini yapıştırın __SSH ortak anahtarını__ alan.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-175">Finally, select hello public key file or paste hello text contents of hello file in hello __SSH public key__ field.</span></span></br><span data-ttu-id="fcbfb-176">![HDInsight küme oluşturma işleminde SSH ortak anahtarı iletişim kutusu](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span><span class="sxs-lookup"><span data-stu-id="fcbfb-176">![SSH public key dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span></span> |
| <span data-ttu-id="fcbfb-177">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="fcbfb-177">**Azure PowerShell**</span></span> | <span data-ttu-id="fcbfb-178">Kullanım hello `-SshPublicKey` hello parametresinin `New-AzureRmHdinsightCluster` hello ortak anahtarı bir dize olarak cmdlet'i ve geçişi hello içeriğini.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-178">Use hello `-SshPublicKey` parameter of hello `New-AzureRmHdinsightCluster` cmdlet and pass hello contents of hello public key as a string.</span></span>|
| <span data-ttu-id="fcbfb-179">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="fcbfb-179">**Azure CLI 1.0**</span></span> | <span data-ttu-id="fcbfb-180">Kullanım hello `--sshPublicKey` hello parametresinin `azure hdinsight cluster create` komut ve hello ortak anahtar Merhaba içeriğine bir dize olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-180">Use hello `--sshPublicKey` parameter of hello `azure hdinsight cluster create` command and pass hello contents of hello public key as a string.</span></span> |
| <span data-ttu-id="fcbfb-181">**Resource Manager Şablonu**</span><span class="sxs-lookup"><span data-stu-id="fcbfb-181">**Resource Manager Template**</span></span> | <span data-ttu-id="fcbfb-182">SSH anahtarlarını şablonla kullanma örneği için bkz. [HDInsight’ı SSH anahtarı ile Linux’a dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span><span class="sxs-lookup"><span data-stu-id="fcbfb-182">For an example of using SSH keys with a template, see [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span></span> <span data-ttu-id="fcbfb-183">Merhaba `publicKeys` hello öğesinde [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) dosyasıdır kullanılan toopass hello anahtarları tooAzure hello kümesi oluştururken.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-183">hello `publicKeys` element in hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) file is used toopass hello keys tooAzure when creating hello cluster.</span></span> |

## <span data-ttu-id="fcbfb-184"><a id="sshpassword"></a>Kimlik doğrulaması: Parola</span><span class="sxs-lookup"><span data-stu-id="fcbfb-184"><a id="sshpassword"></a>Authentication: Password</span></span>

<span data-ttu-id="fcbfb-185">SSH hesaplarının güvenliği bir parola kullanılarak sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-185">SSH accounts can be secured using a password.</span></span> <span data-ttu-id="fcbfb-186">SSH kullanarak tooHDInsight bağlandığınızda, istendiğinde tooenter hello parola olur.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-186">When you connect tooHDInsight using SSH, you are prompted tooenter hello password.</span></span>

> [!WARNING]
> <span data-ttu-id="fcbfb-187">SSH için parola kimlik doğrulamasının kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-187">We do not recommend using password authentication for SSH.</span></span> <span data-ttu-id="fcbfb-188">Parolalar, tahmin edilebilir ve güvenlik açığı toobrute zorla saldırılar.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-188">Passwords can be guessed and are vulnerable toobrute force attacks.</span></span> <span data-ttu-id="fcbfb-189">Bunun yerine, [kimlik doğrulaması için SSH anahtarları](#sshkey) kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-189">Instead, we recommend that you use [SSH keys for authentication](#sshkey).</span></span>

### <a name="create-hdinsight-using-a-password"></a><span data-ttu-id="fcbfb-190">Parola kullanarak HDInsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="fcbfb-190">Create HDInsight using a password</span></span>

| <span data-ttu-id="fcbfb-191">Oluşturma yöntemi</span><span class="sxs-lookup"><span data-stu-id="fcbfb-191">Creation method</span></span> | <span data-ttu-id="fcbfb-192">Nasıl toospecify hello parola</span><span class="sxs-lookup"><span data-stu-id="fcbfb-192">How toospecify hello password</span></span> |
| --------------- | ---------------- |
| <span data-ttu-id="fcbfb-193">**Azure portal**</span><span class="sxs-lookup"><span data-stu-id="fcbfb-193">**Azure portal**</span></span> | <span data-ttu-id="fcbfb-194">Varsayılan olarak, hello hello SSH kullanıcı hesabı sahip hello küme oturum açma hesabı olarak aynı parola.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-194">By default, hello SSH user account has hello same password as hello cluster login account.</span></span> <span data-ttu-id="fcbfb-195">toouse farklı bir parola işaretini __küme oturum açma aynı parolayı kullanın__ve hello parola hello enter __SSH parolası__ alan.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-195">toouse a different password, uncheck __Use same password as cluster login__, and then enter hello password in hello __SSH password__ field.</span></span></br><span data-ttu-id="fcbfb-196">![HDInsight küme oluşturma işleminde SSH parolası iletişim kutusu](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span><span class="sxs-lookup"><span data-stu-id="fcbfb-196">![SSH password dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span></span>|
| <span data-ttu-id="fcbfb-197">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="fcbfb-197">**Azure PowerShell**</span></span> | <span data-ttu-id="fcbfb-198">Kullanım hello `--SshCredential` hello parametresinin `New-AzureRmHdinsightCluster` cmdlet'i ve geçirin bir `PSCredential` hello SSH kullanıcı hesabı adını ve parolayı içeren nesne.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-198">Use hello `--SshCredential` parameter of hello `New-AzureRmHdinsightCluster` cmdlet and pass a `PSCredential` object that contains hello SSH user account name and password.</span></span> |
| <span data-ttu-id="fcbfb-199">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="fcbfb-199">**Azure CLI 1.0**</span></span> | <span data-ttu-id="fcbfb-200">Kullanım hello `--sshPassword` hello parametresinin `azure hdinsight cluster create` komut ve hello parola değeri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-200">Use hello `--sshPassword` parameter of hello `azure hdinsight cluster create` command and provide hello password value.</span></span> |
| <span data-ttu-id="fcbfb-201">**Resource Manager Şablonu**</span><span class="sxs-lookup"><span data-stu-id="fcbfb-201">**Resource Manager Template**</span></span> | <span data-ttu-id="fcbfb-202">Parolayı şablonla kullanma örneği için bkz. [HDInsight’ı SSH parolası ile Linux’a dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span><span class="sxs-lookup"><span data-stu-id="fcbfb-202">For an example of using a password with a template, see [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span></span> <span data-ttu-id="fcbfb-203">Merhaba `linuxOperatingSystemProfile` hello öğesinde [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) dosyasıdır adı ve parola kullanılan toopass hello SSH hesabı tooAzure hello kümesi oluştururken.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-203">hello `linuxOperatingSystemProfile` element in hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) file is used toopass hello SSH account name and password tooAzure when creating hello cluster.</span></span>|

### <a name="change-hello-ssh-password"></a><span data-ttu-id="fcbfb-204">Merhaba SSH Parolayı Değiştir</span><span class="sxs-lookup"><span data-stu-id="fcbfb-204">Change hello SSH password</span></span>

<span data-ttu-id="fcbfb-205">Merhaba hello SSH kullanıcı hesabının parolasını değiştirme hakkında daha fazla bilgi için bkz __parolaları değiştirme__ hello bölümünü [yönetmek Hdınsight](hdinsight-administer-use-portal-linux.md#change-passwords) belge.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-205">For information on changing hello SSH user account password, see hello __Change passwords__ section of hello [Manage HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) document.</span></span>

## <span data-ttu-id="fcbfb-206"><a id="domainjoined"></a>Kimlik doğrulama: Etki alanına katılmış HDInsight</span><span class="sxs-lookup"><span data-stu-id="fcbfb-206"><a id="domainjoined"></a>Authentication: Domain-joined HDInsight</span></span>

<span data-ttu-id="fcbfb-207">Kullanıyorsanız bir __etki alanına katılmış Hdınsight kümesi__, hello kullanmalısınız `kinit` SSH ile bağlandıktan sonra komutu.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-207">If you are using a __domain-joined HDInsight cluster__, you must use hello `kinit` command after connecting with SSH.</span></span> <span data-ttu-id="fcbfb-208">Bu komutu bir etki alanı kullanıcısı ve parola isteyen ve hello kümesi ile ilişkili hello Azure Active Directory etki alanı ile oturumunuz doğrular.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-208">This command prompts you for a domain user and password, and authenticates your session with hello Azure Active Directory domain associated with hello cluster.</span></span>

<span data-ttu-id="fcbfb-209">Daha fazla bilgi için bkz. [Etki alanına katılmış HDInsight yapılandırma](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="fcbfb-209">For more information, see [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md).</span></span>

## <a name="connect-toonodes"></a><span data-ttu-id="fcbfb-210">Toonodes Bağlan</span><span class="sxs-lookup"><span data-stu-id="fcbfb-210">Connect toonodes</span></span>

<span data-ttu-id="fcbfb-211">(varsa) baş düğümler ve kenar düğümüne hello hello erişilebilmesi için bağlantı noktası 22 ve 23 Internet'te.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-211">hello head nodes and edge node (if there is one) can be accessed over hello internet on ports 22 and 23.</span></span>

* <span data-ttu-id="fcbfb-212">Toohello bağlanırken __baş düğümler__, bağlantı noktasını kullanacak __22__ tooconnect toohello birincil baş düğüm ve bağlantı noktası __23__ tooconnect toohello ikincil baş düğüm.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-212">When connecting toohello __head nodes__, use port __22__ tooconnect toohello primary head node and port __23__ tooconnect toohello secondary head node.</span></span> <span data-ttu-id="fcbfb-213">Merhaba tam etki alanı adı toouse olan `clustername-ssh.azurehdinsight.net`, burada `clustername` hello kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-213">hello fully qualified domain name toouse is `clustername-ssh.azurehdinsight.net`, where `clustername` is hello name of your cluster.</span></span>

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* <span data-ttu-id="fcbfb-214">Zaman connectiung toohello __kenar düğümüne__, bağlantı noktası 22 kullanın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-214">When connectiung toohello __edge node__, use port 22.</span></span> <span data-ttu-id="fcbfb-215">Merhaba tam etki alanı adıdır `edgenodename.clustername-ssh.azurehdinsight.net`, burada `edgenodename` ne zaman sağladığınız adı hello kenar düğümüne oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-215">hello fully qualified domain name is `edgenodename.clustername-ssh.azurehdinsight.net`, where `edgenodename` is a name you provided when creating hello edge node.</span></span> <span data-ttu-id="fcbfb-216">`clustername`Merhaba hello küme adıdır.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-216">`clustername` is hello name of hello cluster.</span></span>

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> <span data-ttu-id="fcbfb-217">Merhaba önceki örneklerde, parola kimlik doğrulaması kullanıyorsanız veya bu sertifika kimlik doğrulaması otomatik olarak ortaya çıkma varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-217">hello previous examples assume that you are using password authentication, or that certificate authentication is occuring automatically.</span></span> <span data-ttu-id="fcbfb-218">Kimlik doğrulaması için bir SSH anahtar çiftini kullanırsanız ve hello sertifika otomatik olarak kullanılmaz, hello kullan `-i` parametre toospecify hello özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-218">If you use an SSH key-pair for authentication, and hello certificate is not used automatically, use hello `-i` parameter toospecify hello private key.</span></span> <span data-ttu-id="fcbfb-219">Örneğin, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-219">For example, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span></span>

<span data-ttu-id="fcbfb-220">Bağlantı kurulduktan sonra hello istemi bağlı tooindicate hello SSH kullanıcı adı ve hello düğümü değiştirir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-220">Once connected, hello prompt changes tooindicate hello SSH user name and hello node you are connected to.</span></span> <span data-ttu-id="fcbfb-221">Örneğin, bağlıyken toohello birincil baş düğümü olarak `sshuser`, hello komut istemi `sshuser@hn0-clustername:~$`.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-221">For example, when connected toohello primary head node as `sshuser`, hello prompt is `sshuser@hn0-clustername:~$`.</span></span>

### <a name="connect-tooworker-and-zookeeper-nodes"></a><span data-ttu-id="fcbfb-222">Tooworker ve Zookeeper düğümleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="fcbfb-222">Connect tooworker and Zookeeper nodes</span></span>

<span data-ttu-id="fcbfb-223">çalışan düğümü hello ve Zookeeper düğümleri doğrudan erişilebilir olmayan hello Internet.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-223">hello worker nodes and Zookeeper nodes are not directly accessible from hello internet.</span></span> <span data-ttu-id="fcbfb-224">Bunlar hello küme baş düğüm veya kenar düğümleri erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-224">They can be accessed from hello cluster head nodes or edge nodes.</span></span> <span data-ttu-id="fcbfb-225">Merhaba, hello genel adımlar tooconnect tooother düğümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-225">hello following are hello general steps tooconnect tooother nodes:</span></span>

1. <span data-ttu-id="fcbfb-226">SSH, tooconnect tooa head veya edge düğümünü kullanın:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-226">Use SSH tooconnect tooa head or edge node:</span></span>

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. <span data-ttu-id="fcbfb-227">Merhaba SSH bağlantı toohello head veya kenar düğümünü, hello kullan `ssh` komutu tooconnect tooa çalışan hello küme düğümünde:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-227">From hello SSH connection toohello head or edge node, use hello `ssh` command tooconnect tooa worker node in hello cluster:</span></span>

        ssh sshuser@wn0-myhdi

    <span data-ttu-id="fcbfb-228">tooretrieve hello kümedeki hello düğümlerinin hello etki alanı adlarının bir listesini görmek hello [Ambari REST API kullanarak Hdınsight yönetmek hello](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) belge.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-228">tooretrieve a list of hello domain names of hello nodes in hello cluster, see hello [Manage HDInsight by using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.</span></span>

<span data-ttu-id="fcbfb-229">Merhaba SSH hesabı kullanarak güvenli bir __parola__, bağlanırken hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-229">If hello SSH account is secured using a __password__, enter hello password when connecting.</span></span>

<span data-ttu-id="fcbfb-230">Merhaba SSH hesabı kullanarak sağlanmışsa __SSH anahtarları__, SSH iletme hello istemcide etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-230">If hello SSH account is secured using __SSH keys__, make sure that SSH forwarding is enabled on hello client.</span></span>

> [!NOTE]
> <span data-ttu-id="fcbfb-231">Toodirectly erişim hello kümedeki tüm düğümlerin başka bir Azure sanal ağı Hdınsight'a tooinstall yoludur.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-231">Another way toodirectly access all nodes in hello cluster is tooinstall HDInsight into an Azure Virtual Network.</span></span> <span data-ttu-id="fcbfb-232">Ardından, uzak makine toohello katılabilirsiniz aynı sanal ağ ve hello kümedeki tüm düğümlere doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-232">Then, you can join your remote machine toohello same virtual network and directly access all nodes in hello cluster.</span></span>
>
> <span data-ttu-id="fcbfb-233">Daha fazla bilgi için bkz. [HDInsight ile sanal ağ kullanma](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="fcbfb-233">For more information, see [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md).</span></span>

### <a name="configure-ssh-agent-forwarding"></a><span data-ttu-id="fcbfb-234">SSH aracı iletmeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fcbfb-234">Configure SSH agent forwarding</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcbfb-235">Hello aşağıdaki adımları bir Linux veya UNIX tabanlı sistemi ve Windows 10 Bash ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-235">hello following steps assume a Linux or UNIX-based system, and work with Bash on Windows 10.</span></span> <span data-ttu-id="fcbfb-236">Bu adımlar, sisteminiz için işe yaramazsa, tooconsult hello belgeleri için SSH istemcinizi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-236">If these steps do not work for your system, you may need tooconsult hello documentation for your SSH client.</span></span>

1. <span data-ttu-id="fcbfb-237">Bir metin düzenleyicisiyle `~/.ssh/config` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-237">Using a text editor, open `~/.ssh/config`.</span></span> <span data-ttu-id="fcbfb-238">Bu dosya yoksa, komut satırında `touch ~/.ssh/config` girerek oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-238">If this file doesn't exist, you can create it by entering `touch ~/.ssh/config` at a command line.</span></span>

2. <span data-ttu-id="fcbfb-239">Metin toohello aşağıdaki hello eklemek `config` dosya.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-239">Add hello following text toohello `config` file.</span></span>

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    <span data-ttu-id="fcbfb-240">Hello yerine __ana bilgisayar__ bilgi hello düğümü hello adresiyle toousing SSH bağlanın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-240">Replace hello __Host__ information with hello address of hello node you connect toousing SSH.</span></span> <span data-ttu-id="fcbfb-241">Merhaba önceki örnek hello kenar düğümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-241">hello previous example uses hello edge node.</span></span> <span data-ttu-id="fcbfb-242">Bu giriş, SSH aracı iletmeyi hello belirtilen düğümü için yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-242">This entry configures SSH agent forwarding for hello specified node.</span></span>

3. <span data-ttu-id="fcbfb-243">SSH aracı iletmeyi hello terminal komutu aşağıdaki hello kullanarak test edin:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-243">Test SSH agent forwarding by using hello following command from hello terminal:</span></span>

        echo "$SSH_AUTH_SOCK"

    <span data-ttu-id="fcbfb-244">Bu komut, metin aşağıdaki bilgileri benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-244">This command returns information similar toohello following text:</span></span>

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    <span data-ttu-id="fcbfb-245">Hiçbir şeyin döndürülmemesi, `ssh-agent` özelliğinin çalışmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-245">If nothing is returned, then `ssh-agent` is not running.</span></span> <span data-ttu-id="fcbfb-246">Daha fazla bilgi için hello Aracısı başlatma komut dosyaları bilgilerine bakın [ssh ile ssh-aracı kullanma (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) veya SSH istemcisi belgelerinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-246">For more information, see hello agent startup scripts information at [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) or consult your SSH client documentation.</span></span>

4. <span data-ttu-id="fcbfb-247">Doğruladıktan sonra **ssh aracı** , tooadd aşağıdaki kullanım hello SSH özel anahtar toohello aracınızı çalışıyor:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-247">Once you have verified that **ssh-agent** is running, use hello following tooadd your SSH private key toohello agent:</span></span>

        ssh-add ~/.ssh/id_rsa

    <span data-ttu-id="fcbfb-248">Özel anahtarınızı farklı bir dosyada saklanıyorsa, yerini `~/.ssh/id_rsa` hello yol toohello dosya ile.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-248">If your private key is stored in a different file, replace `~/.ssh/id_rsa` with hello path toohello file.</span></span>

5. <span data-ttu-id="fcbfb-249">Toohello küme kenar düğümüne veya baş düğümler SSH kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-249">Connect toohello cluster edge node or head nodes using SSH.</span></span> <span data-ttu-id="fcbfb-250">Ardından hello SSH komutu tooconnect tooa çalışan veya zookeeper düğümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-250">Then use hello SSH command tooconnect tooa worker or zookeeper node.</span></span> <span data-ttu-id="fcbfb-251">iletilen hello anahtarı kullanarak Hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-251">hello connection is established using hello forwarded key.</span></span>

## <a name="copy-files"></a><span data-ttu-id="fcbfb-252">Dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="fcbfb-252">Copy files</span></span>

<span data-ttu-id="fcbfb-253">Merhaba `scp` yardımcı programı, kullanılan toocopy dosyaları tooand tek tek düğümden hello küme de olabilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-253">hello `scp` utility can be used toocopy files tooand from individual nodes in hello cluster.</span></span> <span data-ttu-id="fcbfb-254">Örneğin, komut kopyaları hello aşağıdaki hello `test.txt` hello yerel sistem toohello birincil baş düğümünden dizin:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-254">For example, hello following command copies hello `test.txt` directory from hello local system toohello primary head node:</span></span>

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

<span data-ttu-id="fcbfb-255">Yol sonra hello belirtilmezse bu yana `:`, hello dosya hello yerleştirilir `sshuser` giriş dizini.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-255">Since no path is specified after hello `:`, hello file is placed in hello `sshuser` home directory.</span></span>

<span data-ttu-id="fcbfb-256">Örnek kopyaları hello Hello `test.txt` hello dosyasından `sshuser` hello birincil baş düğüm toohello yerel sistemde giriş dizini:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-256">hello following example copies hello `test.txt` file from hello `sshuser` home directory on hello primary head node toohello local system:</span></span>

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> <span data-ttu-id="fcbfb-257">`scp`yalnızca bireysel düğümleri hello kümedeki hello dosya sistemine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-257">`scp` can only access hello file system of individual nodes within hello cluster.</span></span> <span data-ttu-id="fcbfb-258">Merhaba HDFS uyumlu depolama hello küme için kullanılan tooaccess verilerde olamaz.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-258">It cannot be used tooaccess data in hello HDFS-compatible storage for hello cluster.</span></span>
>
> <span data-ttu-id="fcbfb-259">Kullanmak `scp` bir SSH oturumundan kullanmak için bir kaynak tooupload gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-259">Use `scp` when you need tooupload a resource for use from an SSH session.</span></span> <span data-ttu-id="fcbfb-260">Örneğin, bir Python komut dosyasını karşıya yükleyin ve ardından bir SSH oturumunda hello betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fcbfb-260">For example, upload a Python script and then run hello script from an SSH session.</span></span>
>
> <span data-ttu-id="fcbfb-261">Verileri HDFS uyumlu depolama hello doğrudan yükleme hakkında daha fazla bilgi için belgeleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="fcbfb-261">For information on directly loading data into hello HDFS-compatible storage, see hello following documents:</span></span>
>
> * <span data-ttu-id="fcbfb-262">[Azure Depolama kullanarak HDInsight](hdinsight-hadoop-use-blob-storage.md)</span><span class="sxs-lookup"><span data-stu-id="fcbfb-262">[HDInsight using Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span>
>
> * <span data-ttu-id="fcbfb-263">[Azure Data Lake Store kullanarak HDInsight](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="fcbfb-263">[HDInsight using Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcbfb-264">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fcbfb-264">Next steps</span></span>

* [<span data-ttu-id="fcbfb-265">HDInsight ile SSH tüneli kullanma</span><span class="sxs-lookup"><span data-stu-id="fcbfb-265">Use SSH tunneling with HDInsight</span></span>](hdinsight-linux-ambari-ssh-tunnel.md)
* [<span data-ttu-id="fcbfb-266">HDInsight ile sanal ağ kullanma</span><span class="sxs-lookup"><span data-stu-id="fcbfb-266">Use a virtual network with HDInsight</span></span>](hdinsight-extend-hadoop-virtual-network.md)
* [<span data-ttu-id="fcbfb-267">HDInsight’ta kenar düğümlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="fcbfb-267">Use edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md#access-an-edge-node)