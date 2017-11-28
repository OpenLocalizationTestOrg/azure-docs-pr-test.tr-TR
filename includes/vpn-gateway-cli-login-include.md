<span data-ttu-id="432ea-101">[az login](/cli/azure/#login) komutuyla Azure aboneliğinizde oturum açın ve ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="432ea-101">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="432ea-102">Oturum açma hakkında daha fazla bilgi için bkz. [Azure CLI 2.0'ı kullanmaya başlama](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="432ea-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

```azurecli
az login
```

<span data-ttu-id="432ea-103">Birden çok Azure aboneliğiniz varsa, hesabın aboneliklerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="432ea-103">If you have more than one Azure subscription, list the subscriptions for the account.</span></span>

```azurecli
az account list --all
```

<span data-ttu-id="432ea-104">Kullanmak istediğiniz aboneliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="432ea-104">Specify the subscription that you want to use.</span></span>

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```