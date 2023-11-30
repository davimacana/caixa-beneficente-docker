# caixa-beneficente-docker

## Processo de Conteinerização da Aplicação

Este repositório contém os arquivos e instruções necessários para gerar imagens Docker para os componentes da aplicação Caixa Beneficente.

### Frontend:

- **Dockerfile Frontend:** [Dockerfile](https://github.com/davimacana/caixa-beneficente-frontend/blob/feature/container-docker/Dockerfile)

Para gerar o build do frontend:
1. Navegue até a raiz do projeto `caixa-beneficente-frontend`.
2. Execute o comando:
```bash
ng build --configuration=production

```

#### Versões Usadas para o Último Build:

```bash
Angular CLI: 12.2.0
Node: 12.22.12
Package Manager: npm 6.14.16
OS: win32 x64

Angular:
...

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.1202.0 (cli-only)
@angular-devkit/core         12.2.0 (cli-only)
@angular-devkit/schematics   12.2.0 (cli-only)
@schematics/angular          12.2.0 (cli-only)
```

### Backend:

- **Dockerfile Backend:** [Dockerfile](https://github.com/davimacana/caixa-beneficente-backend/blob/feature/container-docker/Dockerfile)

Para gerar o build do frontend:
1. Navegue até a raiz do projeto `caixa-beneficente-backend`.
2. Execute o comando: `mvn clean package`.

#### Versões Usadas para o Último Build:

```bash
Apache Maven 3.9.2 (c9616018c7a021c1c39be70fb2843d6f5f9b8a1c)
Maven home: C:\Desenvolvimento\apache-maven-3.9.2
Java version: 17.0.8.1, vendor: Eclipse Adoptium, runtime: C:\Program Files\Java\Eclipse Adoptium\jdk-17.0.8.101-hotspot
Default locale: pt_BR, platform encoding: Cp1252
OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
```

#### Construir a Imagem:
Após gerar os builds, construa as imagens Docker usando os seguintes comandos:
1. Build imagem Backend:
```bash
docker build -t caixa-beneficente-backend:1.0.0 .
```

2. Build imagem Frontend:
```bash
docker build -t caixa-beneficente-frontend:1.0.0 .
```

#### Tageamento e Push da imagem para o registry:
Após as imagens criadas e testadas é feito o tageamento e push da imagem para o regitry.
1. Tag e Push imagem Frontend:
```bash
docker tag caixa-beneficente-backend:1.0.0 davimacana/caixa-beneficente-backend:1.0.0
docker push davimacana/caixa-beneficente-backend:1.0.0
```
2. Tag e Push imagem Frontend:
```bash
docker tag caixa-beneficente-frontend:1.0.0 davimacana/caixa-beneficente-frontend:1.0.0
docker push davimacana/caixa-beneficente-frontend:1.0.0
```

#### Pull da imagem para no registry:
Para subir as imagens em outro ambiente:
1. Pull das imagens:
```bash
docker login
docker-compose pull
```
2. Subir as imagens com docker-compose:
```bash
docker-compose up
```

