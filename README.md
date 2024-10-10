## Automated Testing Kit Demonstration Recipe
Create a Drupal site with Automated Testing Kit (ATK) for demonstration purposes.

This recipe will:
- Install Automated Testing Kit into a fresh Drupal 10.3 (or higher) or Drupal 11 installation.
- Install and configure modules that allow each test to operate (see documentation). 
- Install the Gin theme by calling the kanopi/gin-admin-experience recipe.

## Documentation

https://performantlabs.com/automated-testing-kit/automated-testing-kit

## Installation Instructions

- Start with a fresh Drupal 10.3 (or higher) or Drupal 11 site (recipes are not
  guaranteed to work on existing sites):
```
composer create-project drupal/recommended-project your_new_site
```
- Add Drush:
```
composer require drush/drush
```
- Install the Standard profile using the website UI or with:
```
drush site:install --account-name=admin --account-pass=password -y
```
- Allow composer.json to recognize the Github repo with this recipe:
```
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/performant-labs/atk_standalone"
    }
  ]
```
- Change project stability in composer.json to "dev".
- Add the recipe to your site (it will appear in <project_root>/recipes at
  the same level as web):
```
composer require performant-labs/atk_standalone
```
- Get Drupal to see the new modules:
```
ddev drush cr
```
- Apply the recipe. If using DDEV, Lando or Docksal, do this within the appserver container.

```shell
php core/scripts/drupal recipe ../recipes/atk_demo
```
You should see:
```
[OK] Automated Testing Kit - Demonstration applied successfully
```
Visit the site. See the ATK documentation for instructions on running Cypress or Playwright tests.
