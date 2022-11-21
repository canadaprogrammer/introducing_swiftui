# Introducing SwiftUI

## SwiftUI Essentials

- Learn how to use SwiftUI to compose rich views out of simple ones, set up data flow, and build the navigation while watching it unfold in Xcode's preview.

### Creating and Combining Views

#### Create a New Project and Explore the Canvas

1. Open Xcode and either click "Create a new Xcode project" in Xcode's startup window, or choose File > New > Project.
2. In the template selector, select iOS as the platform, select the App template, and then click Next.
3. Enter "Landmarks" as the product name, select "SwiftUI" for the interface and "Swift" for the language, and click Next. Choose a location to save the project on your Mac.
4. In the Project navigator, select LandmarksApp.swift.
   1. An app that uses the SwiftUI app life cycle has a structure that conforms to the App protocol.
   2. The Structure's body property returns one or more scenes, which in turn provide content for display.
   3. The @main attribute identifies the app's entry point.
5. In the Project navigator, select ContentView.swift.
   1. By default, SwiftUI view files declare two structures.
   2. The first structure conforms to the View protocol and describes the view's content and layout.
   3. The second structure declares a preview for that view.
6. In the canvas, click Resume to display the preview.
   1. If the canvas isn't visible, select Editor > Canvas to show it.
7. Inside the body property, change "Hello, World!" to a greeting for yourself.
   1. As you change the code in a view's body property, the preview updates to reflect your changes.
