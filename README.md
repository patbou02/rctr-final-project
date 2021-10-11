# React Part Time Class Final Project

## Project Links

- [CodeSandbox Link](https://codesandbox.io/s/react-final-project-recipes-kcoo1/)

## Project Description

I will be creating a recipes Application where I can search recipes, get details about them such as ingredients, nutrients and similar recipes.


## Wireframes

### Recipes Page
![Wireframe--Recipes](https://github.com/patbou02/rctr-final-project/blob/main/Wireframe--Recipes2.png)
### Individual Recipe
![Wireframe--Recipes-Detail](https://github.com/patbou02/rctr-final-project/blob/main/Wireframe--Recipe-Detail2.png)

### MVP/PostMVP - 5min

The functionality will then be divided into two separate lists: MPV and PostMVP.  Carefully decided what is placed into your MVP as the client will expect this functionality to be implemented upon project completion.  

#### MVP EXAMPLE
- Home page displaying main list of recipes
- Recipes listings will pull in data from the [Spoontacular API](https://spoontacular.com)
- Clicking on single recipe card will open up more detailed view of recipe containing more information
- Similar recipes will be displayed on a carousel below individual recipes detail
- Bootstrap external library for front end "look and feel" will also provide basic responsiveness functionality

#### PostMVP EXAMPLE

- Ability to filter recipes based on several factors
- Ability for user to favorite a recipe
- Ability for user to add recipes cart
- Polish the responsiveness of the app for multiple types of displays (i.e. mobile, tablet, desktop, etc...)

## Spoontacular API/Endpoints

Spoontacular API will be used to gather food/recipe data that will be served to users. Documentation is available at [Spoontacular's Documentation page](https://spoontacular.com/food-api/docs)

### Endpoint: Random Recipes

```
GET: https://api.spoonacular.com/recipes/random
```
Utilized on initial page load as well as on category (type) pages. Returns random recipes with the possibility to limit the amount of recipes as well as the type using the `number` and `tags` parameters respectively. Filter by size dropdown next to SearchForm changes the `number` parameter value accordingly while input field value changes `tags` parameter.

### Endpoint: Search Recipes

```
GET: https://api.spoonacular.com/recipes/complexSearch
```
Utilized on SearchForm input field value changes. Returns recipes matching searched values entered in input field with the possibility to limit the amount of recipes using the `number` parameter by way of selecting a different size dropdown value.

### Endpoint: Individual Recipe

```
GET: https://api.spoonacular.com/recipes/{id}/information
```
Utilizing each individual recipes ID, the request returns detailed individual recipe information such as ingredients, types of diets, instructions on how to make recipe, recipe steps, etc...

### Endpoint: Recipe Card

```
GET: https://api.spoonacular.com/recipes/{id}/card
```
Also using individual recipe, this endpoint returns the path to a autogenerated recipe card.

### Endpoint: Related Recipes

```
GET: https://api.spoonacular.com/recipes/{id}/similar
```
Based on recipe ID, this endpoint returns recipes similar to initial recipe based on ID. Returned list is limited in information and therefore if more details are needed such as recipe image, then additional call to **Individual Recipe** endpoint will probably be necessary.

## Components
##### Writing out your components and its descriptions isn't a required part of the proposal but can be helpful.

![Components-Architecture](https://github.com/patbou02/rctr-final-project/blob/main/component-architecture2.png)

Based on the initial logic defined in the previous sections try and breakdown the logic further into stateless/stateful components. 

| Component | Description | 
| --- | :---: |  
| App | Top level component. Imports external libraries such as Bootstrap and main styles CSS as well as other child components. | 
| Header | Contains link with logo for use to go back to homepage as well as dynamic page heading. | 
| Navigation | Contains links to different sections of Application such as home and various category random recipe listings. Lifts category name up to `App` in order to be passed down to `Header` for dynamic heading. | 
| Sidebar | Filtering mechanism can be found here were user can select dropdown options, toggles in order to filter and refine search results. | 
| MainContent | Main component which holds state meant to be passed down to specific components based on selected **Route** such as *searchTerm*, *viewBy* as well as *searchType*. Uses **Redirect** otherwise as a fallback to redirect user to home. |
| SearchForm | Contains controlled input text field where values gets pased up as soon as value.length is larger than 3. Also contains select list with "view by" values of 1, 5, 10 or 25. | 
| Recipes | Makes calls to **Spoontacular API** either random or by term depending on whether the term is an empty string (home page only on pageload) or if props term length is larger than 3 (after user enters text in controlled input field). Returns list of recipes using `RecipeCard`.|
| RecipeCard | Builds individual recipe cards based of of props available and creats `Link` using recipe ID to be used by **Route** up in `MainContent`. | 
| RecipeDetails | Inidividual recipe information is displayed by this component. Utilizing available ID, additional API calls are made in order return list of related recipe IDs `getRelatedIDs()`, additional related recipe information/details `getRecipe()` and to generate recipe card `getRecipeCard()`. Some of these elements are displayed inside Bootstrap accordion-type tags. Calls `Carousel` child component. | 
| Carousel | Holds list of related recipes to be displayed in carousel format by calling child component `RelatedRecipe`. | 
| RelatedRecipe | Displays related recipe's title, id and image as well as link to individual recipe details page. |
| Pagination | **Not completed** but will hold dynamic pagination which will allow user to *go to page 5 of 13* depending on available recipes list size and *view by X* dropdown selection. |


## Additional Libraries
[React Boostrap](https://react-bootstrap.github.io/) will be used as a framework for building the Components in a way that these fit as seamlessly as possible with the React methodology and architecture while providing all of the benefits expected from the Boostrap framework.

