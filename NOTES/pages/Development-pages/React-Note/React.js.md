
React is a JavaScript library for rendering user interfaces (UI). UI is built from small units like buttons, text, and images. React lets you combine them into reusable, nestable *components.* From web sites to phone apps, everything on the screen can be broken down into components.

React.js, commonly known as React, is an open-source JavaScript library developed by Facebook that is used for building user interfaces, particularly for single-page applications where the user interface needs to be highly dynamic and responsive.

<aside>
💡 Learn react from [https://react.dev/learn](https://react.dev/learn)

</aside>

---
## [[Basic]]
how to write react code, use of react hooks and many more stuffs.

---
## State-Management
While developing a React Application, it is very important to manage the state efficiently for building fully functional applications. As React is growing there are multiple approaches introduced that can help to manage state efficiently depending upon the type of application we are building.

we can achieve state management in react using #Hooks. but if we are in bigger project and we are using basic #useState we have to prop drill through entire application means from root(app) to the the state in entire application.

![[passing_data_prop_drilling.png]]

==Example:== suppose we are building a OMS (order management system), there we need to build a cart system for that we are using #cartState to handle the cart operations. This #cartState  have to use in 2 different places, `cart.tsx` & on  an `add-to-cart-button.tsx`. Now to use the #cartState we have to create it on root(app.tsx) and pass it through out every components in the component-tree. And in future if we decided to re-structure the components we have to restructure the prop-drilling as well.
To avoid this problem we use #context-api in react or other react state-management tools aka libraries.

![[state-management-store.png]]


Now the high level idea is create states inside a store and use it on every component that are required. For this method we don't have to prop-drilling through out the app. 
### [[Redux]]
#redux-toolkit is the most popular & hated state management libraries out there. It gave us full control over the our staes.