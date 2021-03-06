---
layout: "docs"
title: Drupal Plugin
class: documentation
permalink: /plugins/drupal-plugin/
published: true
---
The Probo Drupal plugin provides an easy way to set Drupal site configuration options in a Probo Build and quickly integrate a Drupal website's repository. To use the Probo Drupal plugin you must declare `plugin: Drupal` in your `.probo.yaml` file. The Drupal plugin's parameters can automate some steps specific to Drupal such as reverting features, running database updates, clearing caches, or performing other build configuration steps. 

The Probo Drupal plugin inherits all [Probo LAMP plugin](/plugins/lamp-plugin/) configuration options. This allows additional Probo Build steps in your `.probo.yaml` file to layer LAMP configuration options and commands on top of the Drupal site specific configuration.

See the <a href="#drupal-plugin-examples" title="Probo Drupal Plugin Examples">Probo Drupal Plugin Examples</a> section below for YAML config examples specific to Drupal.

## Directory Configuration

{: .table .table-striped .table-bordered}
|-------------------------|-------------------------------------|
|`makeFile`               | The name of the [Drush make file](http://www.drush.org/en/master/make/) to run to generate                             the install directory. Accepts a **string** value.                             |
|`profileName`            | The profile name used in creating a symlink to this directory if a Drush make file is                                  specified with the `makeFile` option and used to select the profile to install if the `runInstall`                             option is selected. Accepts a **string** value.                                |
|`runInstall`             | If set, run `drush site-install` to perform a fresh install of the site using the                                      `profileName` as the install profile and allowing the `installArgs` option to configure the                                    install. Accepts a **boolean** value.                                            |
|`installArgs`            | A set of parameters to concatenate onto the `drush site-install` command if the                                        `runInstall` option is set. Defaults to ''. Accepts a **string** value. |
|`siteFolder`             | Specifies the site folder to use for this build (the folder within the Drupal `sites`                                  folder). Defaults to `default`. Accepts a **string** value.             |
| `subDirectory`     |The path to your docroot if it is a subdirectory of your git repository. Accepts a **string** value. |

## Database Configuration

{: .table .table-striped .table-bordered}
|-------------------------|-------------------------------------|
| `database`              |The name of the database to import if specified. Note that this database *must be added as                             an asset separately*. Accepts a **string** value. If you use this parameter, don't add the database with the shell plugin. Do not use the zip format for your compressed database. Use the gzip format.                           |
| `databaseGzipped`       |Whether the database was sent gzipped and whether it should therefore be gunzipped before                               importing. Accepts a **boolean** value.                                         |
| `databaseBzipped`       |Whether the database was sent bzipped and whether it should therefore be bunzipped before                               importing. Accepts a **boolean** value.                                         |

## Settings.php Options

{: .table .table-striped .table-bordered}
|-------------------------|-------------------------------------|
| `settingsRequireFile`      |A file to require at the end of settings.php. This option helps you to avoid checking settings.php into your repository. Accepts a **string** value.|
| `settingsAppend`      |Specify a snippet, such as a variable, to append to the end of the settings.php file. Accepts a **string** value. |

## Additional Options

{: .table .table-striped .table-bordered}
|-------------------------|-------------------------------------|
| `drupalVersion`       |Specifies which version of Drupal you are using so that the appropriate commands can be run. For example, if you specify "8" the `clearCaches` option will run `drush cache-rebuild`. Defaults to 7. Accepts the **integer** values 6, 7, or 8.        |
| `databaseUpdates`     |Determines whether to run `drush updb` after the build is finished. Accepts a                                  **boolean** value.                                                                         |
| `clearCaches`         |Whether to clear all caches using `drush cc all` after the build is finished. Your Drupal site must be version 7 or older to use this option. Defaults to                                           true. Accepts a **boolean** value.                                                 |
| `revertFeatures`      |Whether to revert features using `drush fra` after the build is finished. To use this option, your site must have the [Features module](https://www.drupal.org/project/features) installed. Accepts a                             **boolean** value.                                                                        |

<h2 id="drupal-plugin-examples">Probo Drupal Plugin Examples</h2>

**Using the `Drupal` plugin**

{% for recipe in site.recipes %}
{% if recipe.uid == 'drupal_using_plugin' %}
  {{ recipe.content }}
{% endif %}
{% endfor %}

**Using the Settings Options**

{% for recipe in site.recipes %}
{% if recipe.uid == 'drupal_settings_option' %}
  {{ recipe.content }}
{% endif %}
{% endfor %}

**Setting `LAMPApp` PHP Configuration Options on a Drupal Installation**

{% for recipe in site.recipes %}
{% if recipe.uid == 'lamp_set_php_config_on_drupal' %}
  {{ recipe.content }}
{% endif %}
{% endfor %}
