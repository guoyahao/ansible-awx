# 更多...

下面每一个方案，都经过实践证明行之有效，希望能够对你有帮助

## 域名绑定

绑定域名的前置条件是：AWX已经可以通过解析后的域名访问。  

虽然如此，从服务器安全和后续维护考量，**域名绑定**步骤不可省却  

AWX 域名绑定操作步骤：

1. 使用 SFTP 登录云服务器
2. 修改 [Nginx 配置文件](/zh/stack-components.md#nginx)，将其中的 **server_name** 项的值 *localhost* 修改为你的域名
   ```text
   ...
      server_name    localhost; # 改为自定义域名
   ...
   ```
3. 保存配置文件，重启[ Nginx 服务](/zh/admin-services.md#nginx)
   ```
   sudo docker pause awx_web
   ```
4. 登录AWX，依次打开：【Settings】>【System】，修改下图的 URL 地址
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/en/awx/awx-seturl-websoft9.png)


## 负载均衡

通过负载均衡处理多台 AWX 并行工作，对于大型企业来说这是一种很常见的部署方案。

AWX是基于Docker部署，处理web的容器名称为：awx_web
