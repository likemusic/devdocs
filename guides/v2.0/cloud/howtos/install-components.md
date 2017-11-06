---
layout: default
group: cloud
subgroup: How To
title: Install extensions
menu_title: Install extensions
menu_order: 41
level3_menu_node: level3child
level3_subgroup: update-extensions
menu_node:
version: 2.0
github_link: cloud/howtos/install-components.md
functional_areas:
  - Cloud
  - Configuration
---

This topic discusses how to install *extensions*, which can be any of the following:

*	Modules (extend Magento capabilities)
*	Themes (change the look and feel of your {% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}storefront{% endglossarytooltip %} and Admin)
*	Language packages (localize the storefront and Admin)

<div class="bs-callout bs-callout-info" id="info">
  <p>This topic discusses how to install extensions you purchased from Magento Marketplace. You can use the same procedure to install <em>any</em> extension; all you need is the extension's {% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %} name. To find it, open the extension's <code>composer.json</code> file and note the values for <code>"name"</code> and <code>"version"</code>.</p>
</div>

<div class="bs-callout bs-callout-warning">
    <p>You must check in <code>composer.lock</code> to your environment; otherwise, the extension won't load in {{site.data.var.ece}}. That's because we run <code>composer install</code> (which uses <code>composer.lock</code>) and not <code>composer update</code> when we build and deploy the environment.</p>
</div>

To install a extension, you must:

1.	Obtain the {% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}extension{% endglossarytooltip %} from [Magento Marketplace](https://marketplace.magento.com){:target="_blank"} or elsewhere.
1.	[Get the extension's Composer name](#cloud-howto-comp-composer) and version from your purchase history.
2.	In your local {{site.data.var.ece}} project, [update the Magento `composer.json`](#cloud-howto-comp-json) file with the name and version of the extension.
3.	[Push](#cloud-howto-comp-push) the changes to your environment.
4.	[Verify](#cloud-howto-comp-verify) the extension installed properly.

## Create a branch to work in {#getstarted}

{% include cloud/cli-get-started.md %}

## Step 1: Get the extension's Composer name and version {#cloud-howto-comp-composer}
If you already know the extension's Composer name and version, skip this step and continue with [Update Magento's `composer.json`](#cloud-howto-comp-json).

{% include cloud/composer-name.md %}

## Step 2: Update Magento's `composer.json` {#cloud-howto-comp-json}

To update `composer.json`:

1.	If you haven't done so already, change to your environment root directory.
2.	Enter the following commands to update it:

		composer require <component-name>:<version> --no-update
		composer update

	For example:

		composer require pixlee/magento2:1.0.1 --no-update
		composer update
3.	Wait for project dependencies to update.
4. Enter the following commands in the order shown to commit your changes, including `composer.lock`:

  	git add -A
  	git commit -m "<message>"
  	git push origin <environment ID>

If there are errors, see [extension deployment failure]({{ page.baseurl }}cloud/trouble/trouble_comp-deploy-fail.html).

## Step 4: Verify the extension {#cloud-howto-comp-verify}

To verify the extension installed properly, you can check its functionality in the Magento Admin or you can make sure it is enabled as follows:

1.	[SSH to the environment]({{ page.baseurl }}cloud/env/environments-start.html#env-start-ssh) on which the extension is installed.
2.	Enter the following command to display a list of enabled modules:

  	php bin/magento module:status

3.	Verify the extension is listed.

The extension name is in the format `<VendorName>_<ComponentName>`. It will not be in the same format as the Composer name.

#### Related topics
*	[Update components]({{ page.baseurl }}cloud/howtos/update-components.html)
*	[Install optional sample data]({{ page.baseurl }}cloud/howtos/sample-data.html)
*	[Merge and delete an environment]({{ page.baseurl }}cloud/howtos/environment-tutorial-env-merge.html)
