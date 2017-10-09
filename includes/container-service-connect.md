# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="7e485-101">Bir uzak bağlantı tooa Kubernetes, DC/OS veya Docker Swarm kümesi olun</span><span class="sxs-lookup"><span data-stu-id="7e485-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="7e485-102">Azure kapsayıcı hizmeti kümesi oluşturduktan sonra tooconnect toohello küme toodeploy gerekir ve iş yükleri yönetin.</span><span class="sxs-lookup"><span data-stu-id="7e485-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="7e485-103">Bu makalede nasıl tooconnect toohello ana hello VM küme uzak bir bilgisayardan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7e485-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="7e485-104">Merhaba Kubernetes, DC/OS ve Docker Swarm kümeleri yerel olarak HTTP uç noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e485-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="7e485-105">Kubernetes için bu uç noktası güvenli bir şekilde üzerinde sunulan Internet hello ve hello çalıştırarak erişebilirsiniz `kubectl` internet'e bağlı herhangi makineden komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="7e485-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="7e485-106">DC/OS ve Docker Swarm için yerel bilgisayar toohello küme yönetim sisteminden bir güvenli Kabuk (SSH) tüneli oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="7e485-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="7e485-107">Merhaba tünel kurulduktan sonra hello HTTP uç noktaları ve görünüm hello orchestrator'ın web Arabirimi'ni (varsa) Yerel sisteminizden kullanacağınız komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7e485-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7e485-108">Prerequisites</span></span>

* <span data-ttu-id="7e485-109">Bir Kubernetes, DC/OS veya Docker Swarm kümesi [Azure Container Service’e dağıtılır](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7e485-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="7e485-110">Toohello ortak anahtar eklenen toohello Küme dağıtımı sırasında karşılık gelen SSH RSA özel anahtar dosyası.</span><span class="sxs-lookup"><span data-stu-id="7e485-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="7e485-111">Bu komutlarda hello özel SSH anahtarı olan varsayılmaktadır `$HOME/.ssh/id_rsa` bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="7e485-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="7e485-112">Daha fazla bilgi için [macOS ve Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) veya [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) ile ilgili şu yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="7e485-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="7e485-113">Merhaba SSH bağlantısı çalışmıyorsa, çok gerekebilir [SSH anahtarlarını sıfırlama](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="7e485-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="7e485-114">Tooa Kubernetes kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="7e485-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="7e485-115">Bu adımları tooinstall izleyin ve yapılandırma `kubectl` bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="7e485-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="7e485-116">Linux veya macOS, bu bölümde kullanarak toorun hello komutları gerekebilir `sudo`.</span><span class="sxs-lookup"><span data-stu-id="7e485-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="7e485-117">Kubectl yükleyin</span><span class="sxs-lookup"><span data-stu-id="7e485-117">Install kubectl</span></span>
<span data-ttu-id="7e485-118">Tek yönlü tooinstall toouse hello bu araçtır `az acs kubernetes install-cli` Azure CLI 2.0 komutu.</span><span class="sxs-lookup"><span data-stu-id="7e485-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="7e485-119">Bu komut, emin olun toorun, [yüklü](/cli/azure/install-az-cli2) en son Azure CLI 2.0 hello ve tooan Azure hesabı günlüğe (`az login`).</span><span class="sxs-lookup"><span data-stu-id="7e485-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="7e485-120">Alternatif olarak, hello son indirebilirsiniz `kubectl` hello doğrudan istemciden [Kubernetes serbest sayfa](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="7e485-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="7e485-121">Daha fazla bilgi için bkz. [kubectl yükleme ve ayarlama](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="7e485-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="7e485-122">Küme kimlik bilgilerini indirme</span><span class="sxs-lookup"><span data-stu-id="7e485-122">Download cluster credentials</span></span>
<span data-ttu-id="7e485-123">Bulduktan sonra `kubectl` yüklü toocopy hello küme kimlik bilgilerini tooyour makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e485-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="7e485-124">Tek yönlü toodo get hello kimlik bilgileri olan ile Merhaba `az acs kubernetes get-credentials` komutu.</span><span class="sxs-lookup"><span data-stu-id="7e485-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="7e485-125">Merhaba hello kaynak grubunun adını ve hello kapsayıcı hizmeti kaynak hello adını geçirin:</span><span class="sxs-lookup"><span data-stu-id="7e485-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="7e485-126">Bu komut çok hello küme kimlik bilgileri indirmeleri`$HOME/.kube/config`, burada `kubectl` bulunan toobe bekliyor.</span><span class="sxs-lookup"><span data-stu-id="7e485-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="7e485-127">Alternatif olarak, kullanabileceğiniz `scp` hello dosya Kopyala toosecurely `$HOME/.kube/config` hello ana VM tooyour yerel makine üzerinde.</span><span class="sxs-lookup"><span data-stu-id="7e485-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="7e485-128">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7e485-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="7e485-129">Windows üzerinde varsa, Bash Ubuntu Windows, hello PuTTy güvenli dosya kopya istemcisi veya benzer bir aracı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="7e485-130">Kubectl kullanma</span><span class="sxs-lookup"><span data-stu-id="7e485-130">Use kubectl</span></span>

<span data-ttu-id="7e485-131">Bulduktan sonra `kubectl` yapılandırılmış, kümenizdeki düğümlerin hello listeleyerek hello bağlantıyı sınayın:</span><span class="sxs-lookup"><span data-stu-id="7e485-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="7e485-132">Diğer `kubectl` komutlarını deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="7e485-133">Örneğin, hello Kubernetes Pano görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="7e485-134">İlk olarak, bir proxy toohello Kubernetes API sunucunuz çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7e485-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="7e485-135">Merhaba Kubernetes UI artık şu adresten edinilebilir: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="7e485-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="7e485-136">Daha fazla bilgi için bkz: Merhaba [Kubernetes Hızlı Başlangıç](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="7e485-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="7e485-137">Tooa DC/OS ya da Swarm kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="7e485-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="7e485-138">toouse hello DC/OS ve Docker Swarm kümeleri Azure kapsayıcı hizmeti tarafından dağıtılan yerel Linux, macOS ya da Windows sisteminizi bu yönergeler toocreate bir SSH tüneli izleyin.</span><span class="sxs-lookup"><span data-stu-id="7e485-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="7e485-139">Bu yönergeler, SSH üzerinden TCP trafiğini tünellemeye odaklanır.</span><span class="sxs-lookup"><span data-stu-id="7e485-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="7e485-140">Aynı zamanda etkileşimli bir SSH oturumu hello iç küme yönetimi sistemlerinden birini başlatabilirsiniz, ancak bu önerilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="7e485-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="7e485-141">Bir iç sistem üzerinde doğrudan çalışma, yanlışlıkla yapılandırma değişikliği yapma riskini içerir.</span><span class="sxs-lookup"><span data-stu-id="7e485-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="7e485-142">Linux veya macOS’ta SSH tüneli oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e485-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="7e485-143">Linux veya macOS üzerinde SSH tüneli oluşturduğunuzda, bunu hello ilk şey toolocate hello ortak DNS hello yük dengeli asıl adıdır.</span><span class="sxs-lookup"><span data-stu-id="7e485-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="7e485-144">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="7e485-144">Follow these steps:</span></span>


1. <span data-ttu-id="7e485-145">Merhaba, [Azure portal](https://portal.azure.com), kapsayıcı hizmeti kümesini içeren toohello kaynak grubunu bulun.</span><span class="sxs-lookup"><span data-stu-id="7e485-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="7e485-146">Böylece her bir kaynağın görüntülenen hello kaynak grubunu genişletin.</span><span class="sxs-lookup"><span data-stu-id="7e485-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="7e485-147">Merhaba tıklatın **kapsayıcı hizmeti** kaynak'ı tıklayın ve **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="7e485-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="7e485-148">Merhaba **ana FQDN** Merhaba küme altında görüntülenir. **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="7e485-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="7e485-149">Bu adı daha sonra kullanmak için kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7e485-149">Save this name for later use.</span></span> 

    ![Genel DNS adı](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="7e485-151">Alternatif olarak, Başlangıç'ı çalıştırmak `az acs show` kapsayıcı hizmeti komutu.</span><span class="sxs-lookup"><span data-stu-id="7e485-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="7e485-152">Merhaba Ara **ana profil: fqdn** hello komut çıktısı bir özellik.</span><span class="sxs-lookup"><span data-stu-id="7e485-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="7e485-153">Şimdi bir Kabuğu'nu açın ve hello çalıştırın `ssh` değerleri aşağıdaki hello belirterek komutu:</span><span class="sxs-lookup"><span data-stu-id="7e485-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="7e485-154">**LOCAL_PORT** hello tünel tooconnect hello hizmet tarafındaki hello TCP bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="7e485-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="7e485-155">Swarm için bu too2375 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7e485-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="7e485-156">DC/OS için bu too80 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7e485-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="7e485-157">**REMOTE_PORT** tooexpose istediğiniz hello endpoint hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="7e485-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="7e485-158">Swarm için 2375 bağlantı noktasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e485-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="7e485-159">DC/OS için, 80 numaralı bağlantı noktasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e485-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="7e485-160">**Kullanıcı adı** hello kümeyi dağıttığınızda sağlanan hello kullanıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="7e485-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="7e485-161">**DNSPREFIX** hello kümeyi dağıttığınızda sağladığınız hello DNS önekidir.</span><span class="sxs-lookup"><span data-stu-id="7e485-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="7e485-162">**Bölge** kaynak grubunuzun bulunduğu hello bölgedir.</span><span class="sxs-lookup"><span data-stu-id="7e485-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="7e485-163">**Path_to_prıvate_key** [isteğe bağlı] olan hello küme oluştururken sağladığınız ortak anahtar toohello karşılık gelen hello yolu toohello özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="7e485-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="7e485-164">Bu seçeneği ile Merhaba kullanın `-i` bayrağı.</span><span class="sxs-lookup"><span data-stu-id="7e485-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="7e485-165">Merhaba SSH bağlantı noktası 2200'dür ve standart bağlantı noktası 22'hello değil.</span><span class="sxs-lookup"><span data-stu-id="7e485-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="7e485-166">Birden fazla ana VM ile bir kümede bu hello bağlantı bağlantı noktası toohello ilk VM yöneticisidir.</span><span class="sxs-lookup"><span data-stu-id="7e485-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="7e485-167">Merhaba komut çıktısı döndürür.</span><span class="sxs-lookup"><span data-stu-id="7e485-167">hello command returns without output.</span></span>

<span data-ttu-id="7e485-168">Merhaba örneklere bölümleri aşağıdaki hello DC/OS ve Swarm için bakın.</span><span class="sxs-lookup"><span data-stu-id="7e485-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="7e485-169">DC/OS tüneli</span><span class="sxs-lookup"><span data-stu-id="7e485-169">DC/OS tunnel</span></span>
<span data-ttu-id="7e485-170">DC/OS uç noktaları için bir tünel tooopen hello aşağıdaki gibi bir komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7e485-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="7e485-171">80 numaralı bağlantı noktasına bağlanan başka bir yerel işleminizin olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7e485-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="7e485-172">Gerekirse, 8080 bağlantı noktası gibi 80 bağlantı noktasından farklı bir yerel bağlantı noktası belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="7e485-173">Ancak, bu bağlantı noktasını kullandığınızda bazı web kullanıcı arabirimi bağlantıları çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="7e485-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="7e485-174">Aşağıdaki URL'lere (yerel bağlantı noktası 80 varsayılarak) hello aracılığıyla Yerel sisteminizden hello DC/OS uç noktaları artık erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e485-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="7e485-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="7e485-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="7e485-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="7e485-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="7e485-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="7e485-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="7e485-178">Benzer şekilde, bu Tünel üzerinden her uygulama için hello rest API'lerine ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="7e485-179">Swarm tüneli</span><span class="sxs-lookup"><span data-stu-id="7e485-179">Swarm tunnel</span></span>
<span data-ttu-id="7e485-180">tooopen tünel toohello Swarm uç hello aşağıdaki gibi bir komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7e485-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="7e485-181">2375 numaralı bağlantı noktasına bağlanan başka bir yerel işleminizin olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7e485-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="7e485-182">Örneğin, hello Docker arka plan programı yerel olarak çalıştırıyorsanız, varsayılan toouse bağlantı 2375 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7e485-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="7e485-183">Gerekirse, 2375 bağlantı noktasından farklı bir yerel bağlantı noktası belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="7e485-184">Artık hello Docker Swarm kümesi yerel sisteminizde hello Docker komut satırı arabirimi (Docker CLI) kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="7e485-185">Yükleme yönergeleri için bkz. [Docker Yükleme](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="7e485-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="7e485-186">DOCKER_HOST ortam değişkeni toohello hello tünel için yapılandırılmış yerel bağlantı noktası ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7e485-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="7e485-187">Bu tünel toohello Docker Swarm kümesi Docker komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7e485-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="7e485-188">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7e485-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="7e485-189">Windows’da SSH tüneli oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e485-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="7e485-190">Windows’da SSH tünelleri oluşturmak için birden çok seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="7e485-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="7e485-191">Windows veya benzer bir aracı üzerinde Ubuntu Bash çalıştırıyorsanız, bu makalenin macOS ve Linux için gösterilen hello SSH tünel oluşturma yönergeleri izleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7e485-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="7e485-192">Windows alternatif olarak, bu bölümde açıklanmıştır nasıl toouse PuTTY toocreate hello tünel.</span><span class="sxs-lookup"><span data-stu-id="7e485-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="7e485-193">[PuTTY karşıdan](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows sistemi.</span><span class="sxs-lookup"><span data-stu-id="7e485-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="7e485-194">Merhaba uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7e485-194">Run hello application.</span></span>

3. <span data-ttu-id="7e485-195">Merhaba Küme Yöneticisi kullanıcı adı ve hello kümedeki ilk ana hello hello Genel DNS adından oluşan bir ana bilgisayar adı girin.</span><span class="sxs-lookup"><span data-stu-id="7e485-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="7e485-196">Merhaba **ana bilgisayar adı** çok benzer`azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="7e485-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="7e485-197">Merhaba 2200 girin **bağlantı noktası**.</span><span class="sxs-lookup"><span data-stu-id="7e485-197">Enter 2200 for hello **Port**.</span></span>

    ![PuTTY yapılandırması 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="7e485-199">**SSH > Yetkilendirme** öğesini seçin. Bir yol tooyour özel anahtar dosyası (.ppk biçimi) kimlik doğrulaması için ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7e485-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="7e485-200">Bir aracı gibi kullanabilir [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) bu dosya toogenerate hello SSH anahtar kullanılan toocreate hello küme.</span><span class="sxs-lookup"><span data-stu-id="7e485-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![PuTTY yapılandırması 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="7e485-202">Seçin **SSH > tüneller** ve iletilen bağlantı noktalarını hello aşağıdakileri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="7e485-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="7e485-203">**Kaynak Bağlantı Noktası:** DC/OS için 80 veya Swarm için 2375 kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e485-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="7e485-204">**Hedef:** DC/OS için localhost:80 veya Swarm için 2375 kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e485-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="7e485-205">Aşağıdaki örneğine hello DC/OS için yapılandırılmıştır, ancak Docker Swarm için olan benzer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7e485-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7e485-206">Bu tüneli oluştururken bağlantı noktası 80 kullanımda olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7e485-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![PuTTY yapılandırması 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="7e485-208">İşiniz bittiğinde tıklatın **oturum > Kaydet** toosave hello bağlantı yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="7e485-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="7e485-209">tooconnect toohello PuTTY oturumu,'ı tıklatın **açık**.</span><span class="sxs-lookup"><span data-stu-id="7e485-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="7e485-210">Bağlandığınızda, başlangıç bağlantı noktası yapılandırmasını hello PuTTY olay günlüğünde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![PuTTY olay günlüğü](./media/container-service-connect/putty4.png)

<span data-ttu-id="7e485-212">DC/OS için hello tünel yapılandırdıktan sonra erişebilirsiniz hello ilgili Uç noktalara:</span><span class="sxs-lookup"><span data-stu-id="7e485-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="7e485-213">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="7e485-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="7e485-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="7e485-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="7e485-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="7e485-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="7e485-216">Docker Swarm için hello tünel yapılandırdıktan sonra Windows ayarlarını tooconfigure adlı bir sistem ortam değişkeni açmak `DOCKER_HOST` değerini `:2375`.</span><span class="sxs-lookup"><span data-stu-id="7e485-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="7e485-217">Daha sonra Docker CLI hello hello Swarm kümesine erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e485-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e485-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7e485-218">Next steps</span></span>
<span data-ttu-id="7e485-219">Kümenizde kapsayıcıları dağıtma ve yönetme:</span><span class="sxs-lookup"><span data-stu-id="7e485-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="7e485-220">Azure Container Service ve Kubernetes ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7e485-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="7e485-221">Azure Container Service ve DC/OS ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7e485-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="7e485-222">Hello Azure kapsayıcı hizmeti ve Docker Swarm ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7e485-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

