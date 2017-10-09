## <a name="push-tooazure-from-git"></a>Anında iletme tooAzure Git

Bir Azure uzak tooyour yerel Git deposu ekleyin.

```bash
git remote add azure <URI from previous step>
```

Toohello Azure uzak toodeploy uygulamanızı iletin. Merhaba dağıtım kullanıcı oluşturduğunuzda daha önce oluşturulan hello parolayı girmeniz istenir. Oluşturduğunuz hello parolayı girdiğinizden emin olun [dağıtım kullanıcı yapılandırabilir](#configure-a-deployment-user), değil hello parola toohello Azure portal toolog kullanın.

```bash
git push azure master
```

Merhaba yukarıdaki komut aşağıdaki örneğine benzer toohello bilgileri görüntüler:
