## Automated Testing Kit Demonstration Recipe
Create a demonstration Drupal site with Automated Testing Kit (ATK) for demonstration purposes.

This recipe is designed to:
- Add Automated Testing Kit to a fresh Drupal 10+ installation.
- Add and configure modules that allow each test to operate (see documentation). 
- Add the Gin theme.

## Documentation

https://performantlabs.com/automated-testing-kit/automated-testing-kit

## Installation Instructions

- Start with a fresh Drupal 10+ site (recipes are not guaranteed to work on existing sites):
```
composer create-project drupal/recommended-project your_new_site
```
- Install the 'Standard' profile using the website UI.
- Allow composer.json to recognize recipes:
```  
  "installer-types": ["drupal-recipe"],
  "installer-paths": {
     // Existing entries are here.
     "web/recipes/contrib/{$name}": [
       "type:drupal-recipe"
     ]
  }
```
- Add the recipte patch to composer.json so that Drupal can work with recipes (this will 
  eentually be in core):
```
  "patches": {
    "drupal/core": {
      "Allow recipes to be applied":"https://git.drupalcode.org/project/distributions_recipes/-/raw/patch/recipe.patch"
    }
  }
```
- Allow composer.json to recognize the Github repo with the recipe:
```
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/perfomant-labs/atk_demo"
    }
  ]
```
- Add the recipe to your site:
```
composer require performant-labs/atk_demo
```
- Update dependencies:
```
composer update
```

- Apply the recipe. Note that `core/scripts/drupal` must be
executable with `chmod +x`.

```shell
php core/scripts/drupal recipe recipes/contrib/atk_demo
```

You should see:
```
[OK] Automated Testing Kit - Demonstration applied successfully
```
Clear the cache (`drush cr` or use the UI) and visit the site. See
the documentation for instructions on running Cypress or Playwright tests.
