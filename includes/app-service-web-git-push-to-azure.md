## <a name="push-tooazure-from-git"></a><span data-ttu-id="c8c77-101">Anında iletme tooAzure Git</span><span class="sxs-lookup"><span data-stu-id="c8c77-101">Push tooAzure from Git</span></span>

<span data-ttu-id="c8c77-102">Bir Azure uzak tooyour yerel Git deposu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c8c77-102">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="c8c77-103">Toohello Azure uzak toodeploy uygulamanızı iletin.</span><span class="sxs-lookup"><span data-stu-id="c8c77-103">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="c8c77-104">Merhaba dağıtım kullanıcı oluşturduğunuzda daha önce oluşturulan hello parolayı girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="c8c77-104">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="c8c77-105">Oluşturduğunuz hello parolayı girdiğinizden emin olun [dağıtım kullanıcı yapılandırabilir](#configure-a-deployment-user), değil hello parola toohello Azure portal toolog kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8c77-105">Make sure that you enter hello password you created in [Configure a deployment user](#configure-a-deployment-user), not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="c8c77-106">Merhaba yukarıdaki komut aşağıdaki örneğine benzer toohello bilgileri görüntüler:</span><span class="sxs-lookup"><span data-stu-id="c8c77-106">hello preceding command displays information similar toohello following example:</span></span>
