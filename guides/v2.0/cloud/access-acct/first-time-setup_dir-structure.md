---
layout: default
group:
subgroup:
title: Project directory structure
menu_title: Project directory structure
menu_order:
menu_node:
version: 2.0
github_link: cloud/access-acct/first-time-setup_dir-structure.md
---



## Local project directory structure {#cloud-structure-local}
Not including the Magento application itself, your local project has the following structure:

{% highlight xml %}
├── .git
├── .gitignore
├── .magento
│   ├── routes.yaml
│   └── services.yaml
├── .magento.app.yaml
├── auth.json
├── composer.json
├── composer.lock
├── magento-vars.php
├── php.ini
└── README.md
{% endhighlight %}

<div class="bs-callout bs-callout-info" id="info">
  <p>When you push your local environment to the remote server, our deploy script uses the values defined by configuration files in the <code>.magento</code> directory, then the script deletes the directory and its contents. Your local development environment isn't affected.</p>
</div>

## {{site.data.var.ece}} directories {#cloud-structure-cloud}
The following sections discuss information you need to know about directories in the systems deployed to {{site.data.var.ece}}.

### Magento application root directory
The Magento application root directory is located in different locations depending on the environment:

* [Integration environment]({{ page.baseurl }}cloud/reference/discover-arch.html#cloud-arch-int): the Magento application is located in the `/app` directory.
* [Staging environment]({{ page.baseurl }}cloud/reference/discover-arch.html#cloud-arch-stage): the Magento application is located in the `/<project code>_stg` directory.
* [production]({{ page.baseurl }}cloud/reference/discover-arch.html#cloud-arch-prod): the Magento application is located in the ` /<project code>` directory.

### Writable directories
In Integration, Staging, and Production, *only* the following directories are writable due to security reasons:

*	`var`
*	`pub/static`
*	`pub/media`
*	`app/etc`
*	`/tmp`

<div class="bs-callout bs-callout-info" id="info">
  <p>In Production, each node in the three-node cluster has a <code>/tmp</code> directory that is not shared with the other nodes.</p>
</div>

### Logs
Logs for the integration, staging, and production environments are located under the `/var/log` directory. You can access that directory by opening an SSH tunnel to the environment using the `magento-cloud environment:ssh -e <environment id>` command.

In staging and production environments, the deployment log is located in `/var/log/platform/<project ID>`.

Magento logs are located in the `<magento root dir>/var/log` directory.

#### For more information

*	[auth.json]({{ page.baseurl }}cloud/access-acct/first-time-setup_template.html)
*	[composer.json]()
*	[.magento.app.yaml]({{ page.baseurl }}cloud/project/project-conf-files_magento-app.html)
*	[routes.yaml]({{ page.baseurl }}cloud/project/project-conf-files_routes.html)
*	[services.yaml]({{ page.baseurl }}cloud/project/project-conf-files_services.html)
