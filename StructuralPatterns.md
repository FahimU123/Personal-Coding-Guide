# Adapter

## "Allows obejcts with incompatible interfaces to collab" - Refactoring Guru
## Example: Your app always shows farenheight, you introduce a new weatherAPI which has everything in Celsisus so you use Adapter pattern for your app so you cna use this API and your app still gets Farenhigt

1. Implement your new library - this is called the adaptee
2. Define the target interface - Createing a protocol which inlcudes a method to convert the data into the necessary format
3. Create the adapter - A class which conforms to your target interface and has a properyy of that target interface type and use DI(dependecy inhection), and implement the method for the target interface 
