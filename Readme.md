##Links:

Descriptor Format of Catalog Entities
> https://backstage.io/docs/features/software-catalog/descriptor-format

Prerequisite
> https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.3/tap/GUID-prerequisites.html#tap-gui

Tanzu Application Platform GUI Yelb Catalog
> https://network.pivotal.io/products/tanzu-application-platform#/releases/1205491/file_groups/6091

TechDocs
> https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.3/tap/GUID-tap-gui-techdocs-usage.html

GitHub Authentication Provider
> https://backstage.io/docs/auth/github/provider

Adding Tanzu Application Platform GUI integrations
> https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.3/tap/GUID-tap-gui-integrations.html

TechDocs CLI
> https://github.com/backstage/techdocs-cli/blob/main/docs/README.md

Configuring CI/CD to generate and publish TechDocs sites
> https://backstage.io/docs/features/techdocs/configuring-ci-cd

Using Cloud Storage for TechDocs generated files
> https://backstage.io/docs/features/techdocs/using-cloud-storage

Demo Artefacts
> https://github.com/andrlange/demo-api

TechDocs CLI

serve: `techdocs-cli serve`

generate: `techdocs-cli generate`

publish: `techdocs-cli publish --publisher-type awsS3 --storage-name tap-demo-bucket --entity default/Location/demo-app-and-api`

> where  namespace=default kind=component metadata.name=demo-app-ms-1

##Hints:

How to configure your tap-values.yml gui section (in this case local minikube):

```
tap_gui:
  service_type: ClusterIP
  ingressEnabled: "true"
  ingressDomain: "example.com"
  app_config:
    app:
      baseUrl: http://tap-gui.example.com
    integrations:
      github: # Other integrations available see NOTE below
        - host: github.com
          token: <YOUR_GITHUB_TOKEN>
    catalog:
      locations:
        - type: url
          target: https://github.com/sample-accelerators/tanzu-java-web-app/blob/main/catalog/catalog-info.yaml
        - type: url
          target: https://github.com/benwilcock/tap-gui-blank-catalog/blob/main/catalog-info.yaml
    backend:
      baseUrl: http://tap-gui.example.com
      cors:
        origin: http://tap-gui.example.com
    auth:
      # see https://backstage.io/docs/auth/ to learn about auth providers
      environment: development
      providers:
        github:
          development:
            clientId: '<YOUR_CLIENT_ID>'
            clientSecret: '<YOUR_CLIENT_SECRET>'
    techdocs:
      builder: external
      publisher:
        type: awsS3
        awsS3:
          bucketName: tap-gui-docs
          credentials:
            accessKeyId: <AWS_ACCESS_KEY>
            secretAccessKey: <AWS_ACCESS_KEY_SECRET>
            region: <AWS_REGION>
            s3ForcePathStyle: s3ForcePathStyle
```

