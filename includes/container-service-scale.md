# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="d0c9c-101">Container Service kümesindeki aracı düğümlerini ölçekleme</span><span class="sxs-lookup"><span data-stu-id="d0c9c-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="d0c9c-102">Sonra [Azure kapsayıcı hizmeti kümesini dağıtma](../articles/container-service/dcos-swarm/container-service-deployment.md), toochange hello Aracısı düğüm sayısını gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="d0c9c-103">Örneğin, daha fazla kapsayıcı uygulaması veya örneği çalıştırmak için daha fazla aracı gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="d0c9c-104">Hello Azure portal kullanarak bir DC/OS, Docker Swarm veya Kubernetes kümesindeki Aracısı düğümler hello sayısını değiştirmek veya Azure CLI 2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="d0c9c-105">Azure portal ile Merhaba ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="d0c9c-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="d0c9c-106">Merhaba, [Azure portal](https://portal.azure.com), göz **kapsayıcı hizmetlerini**, toomodify istediğiniz hello kapsayıcı hizmeti'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="d0c9c-107">Merhaba, **kapsayıcı hizmeti** dikey penceresinde tıklatın **aracıları**.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="d0c9c-108">İçinde **VM sayısını**, istenen hello aracıları düğüm sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Merhaba portalı bir havuzda ölçeklendirme](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="d0c9c-110">toosave hello yapılandırma tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="d0c9c-111">Azure CLI 2.0 Hello ile ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="d0c9c-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="d0c9c-112">Olduğundan emin olun, [yüklü](/cli/azure/install-az-cli2) en son Azure CLI 2.0 hello ve tooan içinde günlüğe azure hesabı (`az login`).</span><span class="sxs-lookup"><span data-stu-id="d0c9c-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="d0c9c-113">Merhaba geçerli aracı sayısı bakın</span><span class="sxs-lookup"><span data-stu-id="d0c9c-113">See hello current agent count</span></span>
<span data-ttu-id="d0c9c-114">şu anda aracı toosee hello sayısı hello kümede çalışmasını hello `az acs show` komutu.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="d0c9c-115">Merhaba küme yapılandırmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="d0c9c-116">Örneğin, komut gösterir hello adlı hello kapsayıcı hizmeti yapılandırmasını aşağıdaki hello `containerservice-myACSName` hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d0c9c-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="d0c9c-117">Merhaba komut hello aracılarının hello sayısını döndürür `Count` altındaki `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="d0c9c-118">Kullanım az hello acs ölçek komutu</span><span class="sxs-lookup"><span data-stu-id="d0c9c-118">Use hello az acs scale command</span></span>
<span data-ttu-id="d0c9c-119">toochange hello hello çalıştırmak Aracısı düğümleri sayısı `az acs scale` komutunu ve sağlar hello **kaynak grubu**, **kapsayıcı hizmeti adı**ve istenen hello **yeni aracı sayısı**.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="d0c9c-120">Daha küçük veya daha büyük sayılar kullanarak sırasıyla yukarı veya aşağı ölçeklendirme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="d0c9c-121">Örneğin, toochange hello hello önceki küme too10 aracıların sayısı hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d0c9c-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="d0c9c-122">Hello Azure CLI 2.0 hello kapsayıcı hizmeti hello yeni aracı sayısı dahil olmak üzere, yeni yapılandırmasını hello temsil eden bir JSON dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="d0c9c-123">Daha fazla komut seçeneği için `az acs scale --help` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="d0c9c-124">Ölçeklendirme konusunda dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="d0c9c-124">Scaling considerations</span></span>

* <span data-ttu-id="d0c9c-125">Merhaba Aracısı düğüm sayısı 1 ile 100 (dahil) arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="d0c9c-126">Çekirdek kota hello bir küme içindeki aracı düğümlerin sayısını sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="d0c9c-127">Aracı düğümü ölçeklendirme hello Aracısı havuzunu içeren uygulanan tooan Azure sanal makine ölçek kümesi işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="d0c9c-128">Bir DC/OS kümesinde, bu makalede gösterilen hello işlemleri tarafından yalnızca Aracısı düğümlerine hello özel havuzunda ölçeklenir.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="d0c9c-129">Kümenizdeki dağıttığınız hello orchestrator bağlı olarak hello hello kümede çalışan bir kapsayıcı örnek sayısı ayrı olarak ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="d0c9c-130">Örneğin, bir DC/OS kümesinde hello kullan [Marathon kullanıcı Arabirimi](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello bir kapsayıcı uygulama örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="d0c9c-131">Kapsayıcı hizmeti kümesindeki aracı düğümleri için otomatik ölçeklendirme şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0c9c-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0c9c-132">Next steps</span></span>
* <span data-ttu-id="d0c9c-133">Azure Container Service ile Azure CLI 2.0 komutlarını kullanma hakkında [daha fazla örneğe](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="d0c9c-134">Azure Container Service’de [DC/OS aracı havuzları](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d0c9c-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

