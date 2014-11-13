# React Development Guide

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [File Naming](#file-naming)
- [Directory Structure](#directory-structure)
- [Types](#types)
  - [Simple Components](#simple-components)
  - [Extension Components](#extension-components)
  - [Combination Components](#combination-components)
- [Code Structure](#code-structure)
  - [File layout](#file-layout)
  - [Display Name](#display-name)
  - [Props](#props)
    - [Validation of props](#validation-of-props)
  - [Initial State](#initial-state)
    - [getInitialState](#getinitialstate)
    - [getDefaultProps](#getdefaultprops)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## File Naming

Components should be named using **Pascal case**, be descriptive and be prefixed with **.react.js**.

## Directory Structure

* React components should be placed in a folder called **components** that contians only React components.
* Subfolders can be created to group common components
* Camel case is to be used when the grouping should not be considered part of the component name. ie. **controls/Panel.react.js** and **reusable/Display.react.js**
* Pascal case if the folder name would be part of the component name. ie. **DateTimePicker/Year.react.js** and **DateTimePicker/Month.react.js**

## Types

React components fall into three genearl categories, **simple**, **extension**, and **combination**. 

### Simple Components

These components are designed to be responsible for handling a single purpose and do not contain other simple components. They should be designed in a way that makes them reusable in other parts of an applicaiton. An example of a simple component would be a button.

### Extension Components

These components take a simple component and add functionality that was not provided by the simple component. They can be used to add additional event handlers or logic specific to a use case. These are less common and should be designed to be reusable where appropriate. An example of a extension component would be a drop down button that extends upon a basic button component.

### Combination Components

These components make use of multiple other simple and extended components to produce a component of components. This is useful to group components that when used together serve a single purpose. Combination components should only add functionality that is used to link together the various components contined within. They are often less reusable than the other types of components. An example of a combinaiton component would be an advanced search component that contains the search field along with checkboxes for options and a submit button.

## Code Structure

### File layout

Every React Javascript file should only contain a single React component. React components should use *JSX* when possible and the very first line should be `/** @jsx React.DOM */` to mark the file for *JSX* compiling.

**NOTE: The JSX pragma has been removed in recent versions of React but some third party tools still require it**

Requires should follow the order of:

 * Non-React modules
 * React
 * Third party React components
 * Other React components

To start writing a new React component a empty plain object should be created using camelCase.

    var myComponent = {};

Functions, arrays and objects should then be added to this object.

    myComponent.getInitialState = function() {
        // ...
    };
    
    myComponent.displayName = 'MyComponent';
    // ... and so on ...

Finally your module should export using `React.createClass`.

    module.exports = React.createClass(myComponent);

### Display Name

Every react component must define a display name by adding a `displayName` property to the component. This will provide the React tools exstension in Google Chrome to display the component with the correct name. This name must be in Pascal case.

    myComponent.displayName = 'MyComponent';

### Props

A parent component can pass properties to a child using props. Properties are assign like html attributes and are accessed in the compoent using `this.props`.

#### Validation of props
 
Properties can be validated by using the `propTypes` attribute which contains a object of property keys to validator methods. See [Prop Validation](http://facebook.github.io/react/docs/reusable-components.html#prop-validation)

### Initial State

React has two ways to set the initial state of a component and both have their uses. The first is the `getInitialState` method and the second is the `getDefaultProps` method.

#### getInitialState

This method is used to set the initial state of the component but shouldn't be used to duplicate values from props. See: [Props Anti-Pattern](http://facebook.github.io/react/tips/props-in-getInitialState-as-anti-pattern.html)

#### getDefaultProps

This method is used to provide default values for the properties a component may use. Use this to provide reasonable defaults for properties that a parent may not provide.
