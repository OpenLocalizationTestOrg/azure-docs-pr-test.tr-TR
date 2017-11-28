# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="76d76-101">Kubernetes, DC/OS veya Docker Swarm kümesine uzak bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="76d76-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="76d76-102">Azure Container Service kümesi oluşturduktan sonra, iş yüklerini dağıtmak ve yönetmek için kümeye bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="76d76-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="76d76-103">Bu makalede uzak bir bilgisayardan kümenin ana VM’ine nasıl bağlanacağınız açıklanır.</span><span class="sxs-lookup"><span data-stu-id="76d76-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="76d76-104">Kubernetes, DC/OS ve Docker Swarm kümeleri yerel olarak HTTP uç noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="76d76-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="76d76-105">Kubernetes için, bu uç nokta İnternet’te güvenli bir şekilde kullanıma sunulmuştur ve bu uç noktaya İnternet bağlantısı olan herhangi bir makineden `kubectl` komutunu çalıştırarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="76d76-106">DC/OS ve Docker Swarm için yerel bilgisayarınızdan küme yönetim sistemine bir güvenli kabuk (SSH) tüneli oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="76d76-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span></span> <span data-ttu-id="76d76-107">Tünel oluşturulduktan sonra HTTP uç noktalarını kullanan komutları çalıştırabilir ve düzenleyicinin web arabirimini (varsa) yerel sisteminizden görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="76d76-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="76d76-108">Prerequisites</span></span>

* <span data-ttu-id="76d76-109">Bir Kubernetes, DC/OS veya Docker Swarm kümesi [Azure Container Service’e dağıtılır](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="76d76-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="76d76-110">Dağıtım sırasında kümeye eklenen ortak anahtara karşılık gelen SSH RSA özel anahtar dosyası.</span><span class="sxs-lookup"><span data-stu-id="76d76-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="76d76-111">Bu komutlar, özel SSH anahtarının bilgisayarınızda `$HOME/.ssh/id_rsa` içerisinde olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="76d76-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="76d76-112">Daha fazla bilgi için [macOS ve Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) veya [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) ile ilgili şu yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="76d76-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="76d76-113">SSH bağlantısı çalışmıyorsa, [SSH anahtarlarınızı sıfırlamanız](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md) gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="76d76-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="76d76-114">Kubernetes kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="76d76-114">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="76d76-115">Bilgisayarınızda `kubectl` yükleyip yapılandırmak için şu adımları takip edin.</span><span class="sxs-lookup"><span data-stu-id="76d76-115">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="76d76-116">Linux veya macOS’ta `sudo` kullanarak bu bölümdeki komutları çalıştırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="76d76-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="76d76-117">Kubectl yükleyin</span><span class="sxs-lookup"><span data-stu-id="76d76-117">Install kubectl</span></span>
<span data-ttu-id="76d76-118">Bu aracı yüklemenin kolay yollarından biri, Azure CLI 2.0 `az acs kubernetes install-cli` komutunu kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="76d76-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="76d76-119">Bu komutu çalıştırmak için Azure CLI 2.0’ın en son sürümünü [yüklediğinizden](/cli/azure/install-az-cli2) ve bir Azure hesabında (`az login`) oturum açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="76d76-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="76d76-120">Alternatif olarak, en son `kubectl` istemcisini doğrudan [Kubernetes sürümleri sayfasından](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md) indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="76d76-121">Daha fazla bilgi için bkz. [kubectl yükleme ve ayarlama](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="76d76-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="76d76-122">Küme kimlik bilgilerini indirme</span><span class="sxs-lookup"><span data-stu-id="76d76-122">Download cluster credentials</span></span>
<span data-ttu-id="76d76-123">`kubectl` komut satırı aracını yükledikten sonra, küme kimlik bilgilerini makinenize kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="76d76-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="76d76-124">Kimlik bilgilerini almak için başka bir yöntem de `az acs kubernetes get-credentials` komutunu çalıştırmaktır.</span><span class="sxs-lookup"><span data-stu-id="76d76-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="76d76-125">Kaynak grubunun ve kapsayıcı hizmet kaynağının adını geçirin:</span><span class="sxs-lookup"><span data-stu-id="76d76-125">Pass the name of the resource group and the name of the container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="76d76-126">Bu komut, küme bilgilerini, `kubectl` komut satırı aracının bulunmasını beklediği `$HOME/.kube/config` dizinine indirir.</span><span class="sxs-lookup"><span data-stu-id="76d76-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="76d76-127">Alternatif olarak, `scp` komutunu kullanarak, ana VM’deki dosyayı `$HOME/.kube/config` dizininden yerel makinenize güvenli bir şekilde kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="76d76-128">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="76d76-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="76d76-129">Windows kullanıyorsanız, Windows’ta Bash on Ubuntu veya PuTTy güvenli dosya kopyalama istemcisi veya benzer bir araç kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="76d76-130">Kubectl kullanma</span><span class="sxs-lookup"><span data-stu-id="76d76-130">Use kubectl</span></span>

<span data-ttu-id="76d76-131">`kubectl` yapılandırmasını tamamladıktan sonra bağlantıyı test etmek için kümenizdeki düğümleri listeleyin:</span><span class="sxs-lookup"><span data-stu-id="76d76-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="76d76-132">Diğer `kubectl` komutlarını deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="76d76-133">Örneğin, Kubernetes Panosunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-133">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="76d76-134">İlk olarak Kubernetes API sunucusuna bir ara sunucu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="76d76-134">First, run a proxy to the Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="76d76-135">Kubernetes UI sayfasına şu adresten ulaşabilirsiniz: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="76d76-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="76d76-136">Daha fazla bilgi için bkz: [Kubernetes hızlı başlangıç](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="76d76-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="76d76-137">DC/OS veya Swarm kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="76d76-137">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="76d76-138">Azure Container Service tarafından dağıtılan DC/OS ve Docker Swarm kümelerini kullanmak için, yerel Linux, macOS veya Windows sisteminizden SSH tüneli oluşturmaya yönelik bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="76d76-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="76d76-139">Bu yönergeler, SSH üzerinden TCP trafiğini tünellemeye odaklanır.</span><span class="sxs-lookup"><span data-stu-id="76d76-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="76d76-140">İç küme yönetimi sistemlerinin biriyle etkileşimli bir SSH oturumu da başlatabilirsiniz, ancak bunun yapılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="76d76-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="76d76-141">Bir iç sistem üzerinde doğrudan çalışma, yanlışlıkla yapılandırma değişikliği yapma riskini içerir.</span><span class="sxs-lookup"><span data-stu-id="76d76-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="76d76-142">Linux veya macOS’ta SSH tüneli oluşturma</span><span class="sxs-lookup"><span data-stu-id="76d76-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="76d76-143">Linux veya macOS’ta bir SSH tüneli oluşturduğunuzda yapacağınız ilk şey yük dengeli ana sunucuların genel DNS adını bulmaktır.</span><span class="sxs-lookup"><span data-stu-id="76d76-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span></span> <span data-ttu-id="76d76-144">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="76d76-144">Follow these steps:</span></span>


1. <span data-ttu-id="76d76-145">[Azure portal](https://portal.azure.com)’da kapsayıcı hizmet kümenizi içeren kaynak grubuna gidin.</span><span class="sxs-lookup"><span data-stu-id="76d76-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="76d76-146">Her kaynağın görüntülenmesi için kaynak grubu genişletin.</span><span class="sxs-lookup"><span data-stu-id="76d76-146">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="76d76-147">**Kapsayıcı hizmeti** kaynağına ve **Genel Bakış**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="76d76-147">Click the **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="76d76-148">Kümenin **Ana FQDN**’si **Temel Bileşenler** altında görünür.</span><span class="sxs-lookup"><span data-stu-id="76d76-148">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="76d76-149">Bu adı daha sonra kullanmak için kaydedin.</span><span class="sxs-lookup"><span data-stu-id="76d76-149">Save this name for later use.</span></span> 

    ![Genel DNS adı](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="76d76-151">Alternatif olarak, kapsayıcı hizmetinizde `az acs show` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="76d76-151">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="76d76-152">Komut çıktısında **Master Profile:fqdn** özelliğini arayın.</span><span class="sxs-lookup"><span data-stu-id="76d76-152">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="76d76-153">Şimdi bir kabuk açın ve aşağıdaki değerleri belirleyerek `ssh` komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="76d76-153">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="76d76-154">**LOCAL_PORT**, bağlanılacak tünelin hizmet tarafındaki TCP bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="76d76-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="76d76-155">Swarm için bu değeri 2375’e ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="76d76-155">For Swarm, set this to 2375.</span></span> <span data-ttu-id="76d76-156">DC/OS için bu değeri 80'e ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="76d76-156">For DC/OS, set this to 80.</span></span> 
    <span data-ttu-id="76d76-157">**REMOTE_PORT** kullanıma sunmak istediğiniz uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="76d76-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="76d76-158">Swarm için 2375 bağlantı noktasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="76d76-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="76d76-159">DC/OS için, 80 numaralı bağlantı noktasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="76d76-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="76d76-160">**USERNAME** Kümeyi dağıttığınızda sağlanan kullanıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="76d76-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="76d76-161">**DNSPREFIX** Kümeyi dağıttığınızda sağladığınız DNS önekidir.</span><span class="sxs-lookup"><span data-stu-id="76d76-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="76d76-162">**REGION** kaynak grubunuzun bulunduğu bölgedir.</span><span class="sxs-lookup"><span data-stu-id="76d76-162">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="76d76-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] kümeyi oluştururken sağladığınız ortak anahtara karşılık gelen özel anahtar yoludur.</span><span class="sxs-lookup"><span data-stu-id="76d76-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="76d76-164">Bu seçeneği `-i` flag ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="76d76-164">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="76d76-165">SSH bağlantı noktası 2200’dür ve standart bağlantı noktası 22 değildir.</span><span class="sxs-lookup"><span data-stu-id="76d76-165">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="76d76-166">Birden fazla ana VM bulunan kümede bu, ilk ana VM’e bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="76d76-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
  > 

  <span data-ttu-id="76d76-167">Komut çıktı olmadan döndürülür.</span><span class="sxs-lookup"><span data-stu-id="76d76-167">The command returns without output.</span></span>

<span data-ttu-id="76d76-168">Aşağıdaki bölümlerde DC/OS ve Swarm ile ilgili örneklere bakın.</span><span class="sxs-lookup"><span data-stu-id="76d76-168">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="76d76-169">DC/OS tüneli</span><span class="sxs-lookup"><span data-stu-id="76d76-169">DC/OS tunnel</span></span>
<span data-ttu-id="76d76-170">DC/OS uç noktalarına yönelik bir tünel açmak için aşağıdakine benzer bir komut çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="76d76-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="76d76-171">80 numaralı bağlantı noktasına bağlanan başka bir yerel işleminizin olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="76d76-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="76d76-172">Gerekirse, 8080 bağlantı noktası gibi 80 bağlantı noktasından farklı bir yerel bağlantı noktası belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="76d76-173">Ancak, bu bağlantı noktasını kullandığınızda bazı web kullanıcı arabirimi bağlantıları çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="76d76-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="76d76-174">DC/OS uç noktalarına artık, aşağıdaki URL’ler aracılığıyla yerel sisteminizden erişebilirsiniz (yerel bağlantı noktasının 80 olduğu varsayılmıştır):</span><span class="sxs-lookup"><span data-stu-id="76d76-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="76d76-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="76d76-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="76d76-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="76d76-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="76d76-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="76d76-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="76d76-178">Benzer şekilde, bu tünel üzerinden her uygulama için rest API'lerine ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="76d76-179">Swarm tüneli</span><span class="sxs-lookup"><span data-stu-id="76d76-179">Swarm tunnel</span></span>
<span data-ttu-id="76d76-180">Swarm uç noktalarına bir tünel açmak için, aşağıdakine benzer bir komut çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="76d76-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="76d76-181">2375 numaralı bağlantı noktasına bağlanan başka bir yerel işleminizin olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="76d76-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="76d76-182">Örneğin, Docker programını yerel olarak çalıştırıyorsanız, varsayılan olarak 2375 numaralı bağlantı noktasını kullanacak şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="76d76-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span></span> <span data-ttu-id="76d76-183">Gerekirse, 2375 bağlantı noktasından farklı bir yerel bağlantı noktası belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="76d76-184">Şimdi yerel sisteminizde Docker komut satırı arabirimini (Docker CLI) kullanarak Docker Swarm kümesine erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="76d76-185">Yükleme yönergeleri için bkz. [Docker Yükleme](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="76d76-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="76d76-186">DOCKER_HOST ortam değişkeninizi, tünel için oluşturduğunuz yerel bağlantı noktasına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="76d76-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="76d76-187">Docker Swarm kümesiyle tünel oluşturan Docker komutlarını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="76d76-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span></span> <span data-ttu-id="76d76-188">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="76d76-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="76d76-189">Windows’da SSH tüneli oluşturma</span><span class="sxs-lookup"><span data-stu-id="76d76-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="76d76-190">Windows’da SSH tünelleri oluşturmak için birden çok seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="76d76-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="76d76-191">Windows’de Ubuntu üzerinde Bash veya benzer bir araç çalıştırıyorsanız, macOS ve Linux için bu makalenin önceki kısımlarında gösterilen SSH tüneli oluşturma yönergelerini takip edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="76d76-192">Windows’daki bir alternatif olarak, bu bölümde PuTTY kullanarak tünel oluşturma işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="76d76-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="76d76-193">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)’yi Windows sisteminize indirin.</span><span class="sxs-lookup"><span data-stu-id="76d76-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="76d76-194">Uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="76d76-194">Run the application.</span></span>

3. <span data-ttu-id="76d76-195">Kümedeki ilk ana sunucunun küme yöneticisi kullanıcı adı ve genel DNS adından oluşan bir ana bilgisayar adı girin.</span><span class="sxs-lookup"><span data-stu-id="76d76-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="76d76-196">**Ana Bilgisayar Adı** `azureuser@PublicDNSName`’e benzer.</span><span class="sxs-lookup"><span data-stu-id="76d76-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span></span> <span data-ttu-id="76d76-197">**Bağlantı Noktası** için 2200 girin.</span><span class="sxs-lookup"><span data-stu-id="76d76-197">Enter 2200 for the **Port**.</span></span>

    ![PuTTY yapılandırması 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="76d76-199">**SSH > Yetkilendirme** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="76d76-199">Select **SSH > Auth**.</span></span> <span data-ttu-id="76d76-200">Özel anahtar dosyanıza (.ppk biçimi) kimlik doğrulaması için bir yol ekleyin.</span><span class="sxs-lookup"><span data-stu-id="76d76-200">Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="76d76-201">[PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) gibi bir araç kullanarak bu dosyayı kümenin oluşturulması için kullanılan SSH anahtarından oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-201">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![PuTTY yapılandırması 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="76d76-203">**SSH > Tüneller** öğesini seçin ve aşağıdaki iletilen bağlantı noktalarını yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="76d76-203">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="76d76-204">**Kaynak Bağlantı Noktası:** DC/OS için 80 veya Swarm için 2375 kullanın.</span><span class="sxs-lookup"><span data-stu-id="76d76-204">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="76d76-205">**Hedef:** DC/OS için localhost:80 veya Swarm için 2375 kullanın.</span><span class="sxs-lookup"><span data-stu-id="76d76-205">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="76d76-206">Aşağıdaki örnek DC/OS için yapılandırılmıştır, ancak Docker Swarm için olan benzer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="76d76-206">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="76d76-207">Bu tüneli oluştururken bağlantı noktası 80 kullanımda olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="76d76-207">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![PuTTY yapılandırması 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="76d76-209">İşiniz bittiğinde, bağlantı yapılandırmasını kaydetmek için **Oturum > Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="76d76-209">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="76d76-210">PuTTY oturumuna bağlanmak için **Aç**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="76d76-210">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="76d76-211">Bağlandığınızda, bağlantı noktası yapılandırmasını PuTTY olay günlüğünde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-211">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![PuTTY olay günlüğü](./media/container-service-connect/putty4.png)

<span data-ttu-id="76d76-213">DC/OS için tünelini yapılandırdıktan sonra aşağıdakiler üzerinden ilgili uç noktalara erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="76d76-213">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="76d76-214">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="76d76-214">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="76d76-215">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="76d76-215">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="76d76-216">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="76d76-216">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="76d76-217">Docker Swarm için bir tünel yapılandırdıktan sonra `:2375` değeriyle `DOCKER_HOST` adlı bir sistem ortam değişkeni yapılandırmak için Windows ayarlarınızı açın.</span><span class="sxs-lookup"><span data-stu-id="76d76-217">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="76d76-218">Ardından Docker CLI üzerinden Swarm kümesine erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76d76-218">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76d76-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="76d76-219">Next steps</span></span>
<span data-ttu-id="76d76-220">Kümenizde kapsayıcıları dağıtma ve yönetme:</span><span class="sxs-lookup"><span data-stu-id="76d76-220">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="76d76-221">Azure Container Service ve Kubernetes ile çalışma</span><span class="sxs-lookup"><span data-stu-id="76d76-221">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="76d76-222">Azure Container Service ve DC/OS ile çalışma</span><span class="sxs-lookup"><span data-stu-id="76d76-222">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="76d76-223">Azure Container Service ve Docker Swarm ile çalışma</span><span class="sxs-lookup"><span data-stu-id="76d76-223">Work with the Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

