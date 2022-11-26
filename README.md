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

#### Customize the Text View

1. Customize the text view using the inspector.
   1. In the preview, Command-click the greeting to bring up the structured editing popover, and choose "Show SwiftUI Inspector".
      1. The popover shows different attributes that you can customize, depending on the type of view you inspect.
      2. If it's not clickable, active Selectable on the left bottom
      - <img src="./images/editing_popover.png" alt="Editing Popover" width="200"/>
   2. Use the inspector to change the text to "Turtle Rock", the name of the first landmark you'll show in your app.
   3. Change the Font modifier to "Title".
      1. This applies the system font to the text so that it responds correctly to the user's preferred font sizes and settings.
      - <img src="./images/swiftui_inspector.png" alt="SwiftUI Inspector" width="200"/>
2. To customize a SwiftUI view, you call methods called modifiers. Modifiers wrap a view to change its display or other properties. Each modifier returns a new view, so it's common to chain multiple modifiers, stacked vertically.
   1. Edit the code by hand to change the padding() modifier to the foreground Color(.green) modifier; this changes the text's color to green.
   - `Text("Turtle Rock").font(.title).foregroundColor(Color.green)`
3. Your code is always the source of truth for the view. When you use the inspector to change or remove a modifier, Xcode updates your code immediately to match.
   1. Open the inspector by Command-clicking on the Text declaration in the code editor, and then choose "Show SwiftUI Inspector" from the popover. Click the color pop-up menu and choose Inherited to change the text color to black again.
   2. Notice that Xcode updates your code automatically to reflect the change, removing the forgroundColor(.green) modifier.
   - <img src="./images/code_editor_popover.png" alt="Code Editor Popover" width="200"/>

#### Combine Views Using Stacks

1. You can use Xcode's structured editing support to embed a view in a container view, open an inspector, or help with other useful changes.
   1. Command-click the text view's initializer to show the structured editing popover, and then choose "Embed in VStack".
      1. <img src="./images/embed_vstack.png" alt="Embed in VStack" width="200"/>
2. Next, you'll add a text view to the stack by dragging a Text view from the library.
   1. Open the library by clicking the plus button (+) at the top-right of the Xcode window, and then drag a Text view to the place in your code immediately below the "Turtle Rock" text view.
   2. Replace the Text view's placeholder text with "Joshua Tree National Park".
3. Customize the location to match the desired layout.
   1. Set the location's font to subheadline.
      1. `.font(.subheadline)`
   2. Edit the VStack initializer to align the views by their leading edges.
      1. By default, stack center their contents alogn their axis and provide context-appropriate spacing.
      2. `VStack(alignment: .leading) {`
4. Next, you'll add another text view to the right of the location, this for the park's state.

   1. In the canvas, Command-click "Joshua Tree National Park", and choose "Embed in HStack".
      1. <img src="./images/embed_hstack.png" alt="Embed in HStack" width="200"/>
   2. Add a new text view after the location, change the placeholder text to "California", the park's state, and then set its font to subheadline.
      1. `Text("California").font(.subheadline)`
   3. To direct the layout to use the full width of the device, separate the park and the state by adding a `Spacer()` to the horizontal stack holding the two text views.
      1. A spacer expands to make its containing view use all of the space of its parent view, instead of having its size defined only by its contents.
   4. Finally, use the `padding()` modifier method to give the landmark's name and details a little more space.

   - ```swift
     struct ContentView: View {
         var body: some View {
             VStack {
                 VStack(alignment: .leading) {
                     Text("Turtle Rock")
                         .font(.title)
                         .foregroundColor(Color.black)
                     HStack {
                         Text("Joshua Tree National Park")
                             .font(.subheadline)
                         Spacer()
                         Text("California")
                             .font(.subheadline)
                     }
                 }
             }
             .padding()
         }
     }
     ```

   - <img src="./images/combine_veiw_stack.png" alt="Combine View using Stack" width="200"/>

#### Create a Custom Image View

1. Start by adding an image to the project's asset catalog.
   1. Find turtlerock@2x.jpg in the project files' Resources folder; drag it into the asset catalog's editor. Xcode creates a new image set for the image.
   2. <img src="./images/adding_image.png" alt="Adding Image" width="600"/>
2. Next, you'll create a new SwiftUI view for your custom image view.
   1. Choose File > New > File to open the template selector again.
   2. In the User Interface section, select "SwiftUI View" and click Next. Name the file CircleImage.swift and click Create.
3. You're ready to insert the image and modify its display to match the desired design.

   1. Replace the: text view with the image of Turtle Rock by using the `Image(_:)` initializer, passing it the name of the image to display.
      1. You can check the name in the asset catalog's editor.
   2. Add a call to `clipShape(Circle())` to apply the circular clipping shape to the image.
      1. The Circle type is a shape that you can use as a mask, or as a view by giving the circle a stroke of fill.
      2. The shapes of `.clipShape()`:
         1. `Circle()`
         2. `Ellipse()`
         3. `Capsule()`
         4. `RoundedRectangle(cornerRadius: 25.0)`
         5. `Rectangle()`
   3. Create another circle with a gray stroke, and then add it as an overlay to give the image a border.
      1. `.overlay { Circle().stroke(.gray, lineWidth: 4) }`
   4. Next, add a shadow with a 7 point radius.
      1. `.shadow(radius:7)`
   5. Switch the border color to white.

   - ```swift
     import SwiftUI

     struct CircleImage: View {
         var body: some View {
             Image("turtlerock")
                 .clipShape(Circle())
                 .overlay {
                     Circle().stroke(.white, lineWidth: 4)
                 }
                 .shadow(radius: 7)
         }
     }

     struct CircleImage_Previews: PreviewProvider {
         static var previews: some View {
             CircleImage()
         }
     }
     ```

   - <img src="./images/custom_image_view.png" alt="Custom Image View" width="200"/>

#### Use SwiftUI Views From Other Frameworks

- You'll create a map that centers on a given coordinate. You can use the Map view from MapKit to render the map.

1. To get started, you'll create a new custom view to manage your map.

   1. Choose File > New > File, select iOS as the platform, select the "SwiftUI View" template, and click Next.
      1. Name the new file MapView.swift and click Create.
   2. Add an import statement for MapKit, `import MapKit`.
      1. When you import SwiftUI and certain other frameworks in the same file, you gain access to SwiftUI-specific functionality provided by that framework.
   3. Create a private state variable that holds the region information for the map.

      1. You use the @State attribute to establish a source of truth for data in your app that you can modify from more than one view.
      2. SwiftUI manages the underlying storage and automatically updates views that depend on the value.

      - ```swift
        @State private var region = MKCoordinateRegion(
            center: CLLocationCoordinate2D(latitude: 34.011_286, longitude: -116.166_868),
            span: MKCoordinateSpan(latitudeDelta: 0.2, longitudeDelta: 0.2)
        )
        ```

   4. Replace the default Text view with a Map view that takes a binding to the region.
      1. By prefixing a state variable with $, you pass a binding, which is like a reference to the underlying value.
      2. When the user interacts with the map, the map updates the region value to match the part of the map that's currently visible in the user interface.

2. When previews are in static mode, they only fully render native SwiftUI views. For the Map view, you'll need to switch to a live preview to see it render.
   1. Click Live Preview to switch the preview to live mode. You might need to click Try Again or Resume above your preview.
      1. In a moment, you'll see a map centered on Turtle Rock.
      2. You can manipulate the map in live preview to zoom out a bit and see the surrounding area.

#### Compose the Detail View

- You new have all of the components you need - the name and place, a circular image, and a map for the location.
- With the tools you've used so far, combine your custom views to create the final design for the landmark detail view.
- <img src="./images/detail_view.png" alt="Detail View" width="300"/>

1. In the Project navigator, select the ContentView.swift file
2. Embed the VStack that holds the three text views in another VStack.
3. Add your custom MapView tot he top of the stack. Set the size of the Map View with frame(width:height:).
4. Click Live Preview to see the rendered map in the composed view.
   1. You can continue editing the view whiile showing a Live Preview.
5. Add the CircleImage view to the stack.
6. To layer the image view on top of the map view, give the image an offset of -130 points vertically, and padding of -130 points from the bottom of the view.
   1. These adjustments make room for the text by moving the image upwards.
7. Add a spacer at the bottom of the outer VStack to push the content to the top of the screen.
8. To allow the map content to extend to the top edge of the screen, add the ignoresSafeArea(edges: .top) modifier to the map view.
9. Add a divider and some additional descriptive text for the landmark.
10. Finally, move the subheadline font modifier from each Text view to the HStack containing them, and apply the secondary color to the subheadline text.
    1. When you apply a modifier to a layout view like a stack, SwiftUI applies the modifier to all the elements contained in the group.

- ContentView.swift

  - ```swift
      import SwiftUI

      struct ContentView: View {
          var body: some View {
              VStack {
                  MapView()
                      .ignoresSafeArea(edges: .top)
                      .frame(height:300)

                  CircleImage()
                      .offset(y:-130)
                      .padding(.bottom, -130)

                  VStack(alignment: .leading) {
                      Text("Turtle Rock")
                          .font(.title)
                          .foregroundColor(Color.black)
                      HStack {
                          Text("Joshua Tree National Park")
                          Spacer()
                          Text("California")
                      }
                      .font(.subheadline)
                      .foregroundColor(.secondary)

                      Divider()

                      Text("About Turtle Rock")
                          .font(.title2)
                      Text("Descriptive text goes here.")

                  }
                  .padding()

                  Spacer()
              }
          }
      }

      struct ContentView_Previews: PreviewProvider {
          static var previews: some View {
              ContentView()
          }
      }
    ```
