---
layout: default
group: cloud
subgroup: How To
title: Run a PHP debugger
menu_title: Run a PHP debugger
menu_order: 100
menu_node:
version: 2.0
github_link: cloud/howtos/debug.md
functional_areas:
  - Cloud
  - Setup
---

This topic discusses how to run a {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %} debugger using Xdebug as an example.

### Get started

{% collapsible Click to expand/collapse content %}

{% include cloud/cli-get-started.md %}

{% endcollapsible %}

### Set up Xdebug

{% collapsible Click to expand/collapse content %}

To set up Xdebug:

1.	Open `.magento.app.yaml` in a text editor.
2.	In the `runtime` section, under `extensions`, add `xdebug`.

	An example follows:

		runtime:
		   extensions:
		      - mcrypt
			  - redis
			  - xsl
			  - json
		      - xdebug
3.	Save your changes to `.magento.app.yaml` and exit the text editor.
4.	Add, commit, and push the changes to redeploy the environment:

		git add -A
		git commit -m "Add xdebug"
		git push origin <environment ID>
5.	Get the environment's SSH URL:

		magento-cloud environment:ssh --pipe -e <environment ID>
6.	To use Xdebug, SSH to the environment as follows:

		ssh -R <xdebug listen port>:<host>:<xdebug listen port> <SSH URL>

	For example,

		ssh -R 9000:localhost:9000 pwga8A0bhuk7o-mybranch@ssh.us.magentosite.cloud

{% endcollapsible %}

#### Related topics
*	[Install components]({{ page.baseurl }}cloud/howtos/install-components.html)
*	[Update components]({{ page.baseurl }}cloud/howtos/update-components.html)
*	[Merge and delete an environment]({{ page.baseurl }}cloud/howtos/environment-tutorial-env-merge.html)
