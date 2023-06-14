# Utilizando o novo Spring Authorization Server

### Projeto
- São 3 aplicação Spring Rest
  - auth-server
  - post
  - user

A aplicação de **post** consulta a aplicação de **user**, para buscar os usuários que estão cadastrados nas publicações. Isso é uma integração de backend para backend.

As aplicações **user** e **post** tem banco de dados isolados. 

A aplicação **user** e **auth-server** compartilham o mesmo banco de dados.

As aplicações **post** e **user** serão os **Resource Server** do OAuth2. A aplicação **oauth-server** vai servir o **post** e **user** em dois métodos diferentes de autenticação, utilizando tanto o **authorization-code** quando o **client-credentials**.

**Token**

O **auth-server** utilizará uma chave privada para assinar o token. Já as aplicações **post** e **user** que são os **resource server** usarão a chave pública para validar o token assinado com a chave privada.
```bash
keytool -genkeypair -alias awblog -keyalg RSA -keypass 123456 -keystore awblog.jks -storepass 123456 -validity 3650
```

Os **resource-server** irão carregar sua chave pública do endpoint http://localhost:8082/oauth2/jwks para usar o grant_type **client_credentials**

**Requisitos**

Na API somente os usuário admin podem criar um usuário admin. Qualquer outro usuário pode criar usuário editores dos posts. Somente admins podem listar usuários e buscar por id. Todos os usuários podem ver as publicações. Somente usuários autenticados podem criar publicações.
