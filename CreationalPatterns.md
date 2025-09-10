# Factory Method

## When you have an object with multiple types, but the type is determined at runtime
## Example: To-do app, task object, different types - work, personal, etc...

1. Abstract Product - Define the blueprint/Interface for your object
2. Concrete Product - Create classes to conform to your abstract protocol and make all the different types you have 
3. Abstract Creator - Define the blueprint to create your object - this method should return your object
4. Concrete Creator - Create "Factories" which conform to your abstract creator and implement the methods where each function returns a concrete product

# Absatrct Factory

## When you need to create family of related objects
## Example: You got a lucnc combo dela on your app and you can have  pbejcts, appetizer, drink and main course

1. Absatrct Protocols - Define the blueprints/Interfaces for your object - PLURAL
2. Concrete Products - Create classes to conform to your abstract protocol and make all the different types you have 
3. Abstract Factory - Define the blueprints to create your objects - these methods should return your objects - PLURAL
4. Concrete Factory - Create "Factories" which conform to your abstract factory and implement the methods where each function returns a concrete product
