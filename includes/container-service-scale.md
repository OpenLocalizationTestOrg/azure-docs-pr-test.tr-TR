# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="c62ea-101">Container Service kümesindeki aracı düğümlerini ölçekleme</span><span class="sxs-lookup"><span data-stu-id="c62ea-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="c62ea-102">[Azure Container Service kümesini dağıttıktan](../articles/container-service/dcos-swarm/container-service-deployment.md) sonra aracı düğüm sayısını değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c62ea-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need to change the number of agent nodes.</span></span> <span data-ttu-id="c62ea-103">Örneğin, daha fazla kapsayıcı uygulaması veya örneği çalıştırmak için daha fazla aracı gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c62ea-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="c62ea-104">Azure Portal’ı veya Azure CLI 2.0’ı kullanarak bir DC/OS, Docker Swarm veya Kubernetes kümesindeki Aracısı düğüm sayısını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c62ea-104">You can change the number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using the Azure portal or the Azure CLI 2.0.</span></span> 

## <a name="scale-with-the-azure-portal"></a><span data-ttu-id="c62ea-105">Azure Portal’da ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="c62ea-105">Scale with the Azure portal</span></span>

1. <span data-ttu-id="c62ea-106">[Azure Portal](https://portal.azure.com)’da, **Kapsayıcı hizmetleri**’ni bulun ve değiştirmek istediğiniz kapsayıcı hizmetine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c62ea-106">In the [Azure portal](https://portal.azure.com), browse for **Container services**, and then click the container service that you want to modify.</span></span>
2. <span data-ttu-id="c62ea-107">**Kapsayıcı hizmeti** dikey penceresinde **Aracılar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c62ea-107">In the **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="c62ea-108">**VM Sayısı**’nda istenen aracıları düğümü sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="c62ea-108">In **VM Count**, enter the desired number of agents nodes.</span></span>

    ![Portalda bir havuzu ölçeklendirme](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="c62ea-110">Yapılandırmayı kaydetmek için **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c62ea-110">To save the configuration, click **Save**.</span></span>

## <a name="scale-with-the-azure-cli-20"></a><span data-ttu-id="c62ea-111">Azure CLI 2.0 ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="c62ea-111">Scale with the Azure CLI 2.0</span></span>

<span data-ttu-id="c62ea-112">Azure CLI 2.0’ın en son sürümünü [yüklediğinizden](/cli/azure/install-az-cli2) ve bir azure hesabında (`az login`) oturum açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c62ea-112">Make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an azure account (`az login`).</span></span>

### <a name="see-the-current-agent-count"></a><span data-ttu-id="c62ea-113">Geçerli aracı sayısını görme</span><span class="sxs-lookup"><span data-stu-id="c62ea-113">See the current agent count</span></span>
<span data-ttu-id="c62ea-114">Şu anda kümedeki aracıları sayısını görmek için `az acs show` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c62ea-114">To see the number of agents currently in the cluster, run the `az acs show` command.</span></span> <span data-ttu-id="c62ea-115">Bunu yaptığınızda küme yapılandırması gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c62ea-115">This shows the cluster configuration.</span></span> <span data-ttu-id="c62ea-116">Örneğin, aşağıdaki komut `myResourceGroup` kaynak grubundaki `containerservice-myACSName` adlı kapsayıcı hizmetinin yapılandırmasını gösterir:</span><span class="sxs-lookup"><span data-stu-id="c62ea-116">For example, the following command shows the configuration of the container service named `containerservice-myACSName` in the resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="c62ea-117">Komut, `AgentPoolProfiles` altında `Count` değerindeki aracıların sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="c62ea-117">The command returns the number of agents in the `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-the-az-acs-scale-command"></a><span data-ttu-id="c62ea-118">az acs scale komutunu kullanma</span><span class="sxs-lookup"><span data-stu-id="c62ea-118">Use the az acs scale command</span></span>
<span data-ttu-id="c62ea-119">Aracı düğüm sayısını değiştirmek için `az acs scale` komutunu çalıştırın ve **kaynak grubu**, **kapsayıcı hizmeti adı** ve istenen **yeni aracı sayısı** değerlerini girin.</span><span class="sxs-lookup"><span data-stu-id="c62ea-119">To change the number of agent nodes, run the `az acs scale` command and supply the **resource group**, **container service name**, and the desired **new agent count**.</span></span> <span data-ttu-id="c62ea-120">Daha küçük veya daha büyük sayılar kullanarak sırasıyla yukarı veya aşağı ölçeklendirme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c62ea-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="c62ea-121">Örneğin, önceki kümede aracı sayısını 10 yapmak için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="c62ea-121">For example, to change the number of agents in the previous cluster to 10, type the following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="c62ea-122">Azure CLI 2.0, yeni aracı sayısı da dahil olmak üzere kapsayıcı hizmetinin yeni yapılandırmasını temsil eden bir JSON dizesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c62ea-122">The Azure CLI 2.0 returns a JSON string representing the new configuration of the container service, including the new agent count.</span></span>

<span data-ttu-id="c62ea-123">Daha fazla komut seçeneği için `az acs scale --help` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c62ea-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="c62ea-124">Ölçeklendirme konusunda dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="c62ea-124">Scaling considerations</span></span>

* <span data-ttu-id="c62ea-125">Aracı düğüm sayısı 1 ile 100 (dahil) arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c62ea-125">The number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="c62ea-126">Çekirdek kotanız bir küme içindeki aracı düğümlerinin sayısını sınırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="c62ea-126">Your cores quota can limit the number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="c62ea-127">Aracı düğümü ölçeklendirme işlemleri, aracı havuzunu içeren bir Azure sanal makine ölçek kümesine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c62ea-127">Agent node scaling operations are applied to an Azure virtual machine scale set that contains the agent pool.</span></span> <span data-ttu-id="c62ea-128">DC/OS kümesinde, bu makalede gösterilen işlemlerle yalnızca özel havuzdaki aracı düğümleri ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="c62ea-128">In a DC/OS cluster, only agent nodes in the private pool are scaled by the operations shown in this article.</span></span>

* <span data-ttu-id="c62ea-129">Kümenizde dağıttığınız düzenleyiciye bağlı olarak, küme üzerinde çalışan bir kapsayıcının örnek sayısını ayrı olarak ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c62ea-129">Depending on the orchestrator you deploy in your cluster, you can separately scale the number of instances of a container running on the cluster.</span></span> <span data-ttu-id="c62ea-130">Örneğin, bir kapsayıcı uygulamasının örnek sayısını değiştirmek için DC/OS kümesinde [Marathon kullanıcı arabirimini](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="c62ea-130">For example, in a DC/OS cluster, use the [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) to change the number of instances of a container application.</span></span>

* <span data-ttu-id="c62ea-131">Kapsayıcı hizmeti kümesindeki aracı düğümleri için otomatik ölçeklendirme şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="c62ea-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c62ea-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c62ea-132">Next steps</span></span>
* <span data-ttu-id="c62ea-133">Azure Container Service ile Azure CLI 2.0 komutlarını kullanma hakkında [daha fazla örneğe](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="c62ea-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="c62ea-134">Azure Container Service’de [DC/OS aracı havuzları](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="c62ea-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

