
# MyGUI Engine Structure

This document provides an overview of the underlying engine structure of MyGUI, a library designed for creating graphical user interfaces (GUIs) in applications.

## Main Components of MyGUI

1. **Core Components**:
   - **MyGUI::Gui**: The central class responsible for managing the entire GUI system. It handles the creation, deletion, and updating of widgets.
   - **MyGUI::Widget**: The base class for all GUI elements. It provides common functionality for all widgets, such as rendering, event handling, and parent-child relationships.
   - **MyGUI::LayerManager**: Manages layers of widgets, ensuring proper rendering order.
   - **MyGUI::InputManager**: Handles input events (mouse, keyboard, etc.) and dispatches them to appropriate widgets.

2. **Rendering Components**:
   - **MyGUI::RenderManager**: Abstract class responsible for rendering widgets. The actual rendering is done by specific implementations for different rendering systems (e.g., OpenGL, Direct3D, OGRE).
   - **MyGUI::TextureManager**: Manages textures used by widgets.
   - **MyGUI::VertexBuffer**: Manages vertex buffer objects for rendering.

3. **Resource Management**:
   - **MyGUI::ResourceManager**: Manages resources such as images, fonts, and layouts.
   - **MyGUI::ResourceSkin**: Defines the appearance of widgets using images and other resources.

4. **Event System**:
   - **MyGUI::EventPair**: Template class for defining events and connecting them to handlers.
   - **MyGUI::Delegate**: Implements a delegate system for event handling.

5. **Widget Types**:
   - **MyGUI::Button**, **MyGUI::EditBox**, **MyGUI::Window**, etc.: Various widget types derived from MyGUI::Widget, each providing specific functionality.

## Directory Structure

Let's explore the directory structure to understand where these components are implemented.

- **Common/**: Contains common utilities and base classes used across the library.
- **Engine/**: The core engine of MyGUI, including rendering, input management, and main GUI system.
- **MyGUI/**: The primary include directory for MyGUI, containing public headers for the library.
- **Platform/**: Platform-specific implementations, including different rendering systems and input handling.
- **Tools/**: Various tools for creating and managing GUI resources, such as layout and skin editors.

## Key Classes and Files

1. **MyGUI::Gui**: Implemented in `Engine/src/MyGUI_Gui.cpp`.
2. **MyGUI::Widget**: Base class for all widgets, implemented in `Engine/src/MyGUI_Widget.cpp`.
3. **MyGUI::LayerManager**: Layer management, implemented in `Engine/src/MyGUI_LayerManager.cpp`.
4. **MyGUI::InputManager**: Input handling, implemented in `Engine/src/MyGUI_InputManager.cpp`.
5. **MyGUI::RenderManager**: Abstract rendering manager, implemented in `Engine/src/MyGUI_RenderManager.cpp`.
6. **MyGUI::TextureManager**: Manages textures, implemented in `Engine/src/MyGUI_TextureManager.cpp`.

## High-Level Workflow

1. **Initialization**:
   - MyGUI::Gui is initialized, setting up the core GUI system.
   - MyGUI::RenderManager and MyGUI::TextureManager are initialized based on the chosen rendering system.

2. **Widget Creation**:
   - Widgets are created using MyGUI::Gui methods, such as `createWidget`.
   - Widgets are added to the appropriate layers and parent widgets.

3. **Rendering**:
   - MyGUI::RenderManager manages the rendering loop, drawing widgets in the correct order based on their layers.
   - Vertex buffers and textures are managed by MyGUI::VertexBuffer and MyGUI::TextureManager.

4. **Input Handling**:
   - MyGUI::InputManager captures input events and dispatches them to the appropriate widgets.
   - Widgets handle events and trigger any associated event handlers.

5. **Resource Management**:
   - Resources such as images, fonts, and skins are managed by MyGUI::ResourceManager.
   - Resources are loaded and assigned to widgets as needed.

## Example: Creating a Button

Here’s an example of how a button widget might be created and rendered:

```cpp
// Initialize MyGUI::Gui
MyGUI::Gui* gui = new MyGUI::Gui();
gui->initialise();

// Create a button
MyGUI::Button* button = gui->createWidget<MyGUI::Button>("ButtonSkin", MyGUI::IntCoord(10, 10, 100, 30), MyGUI::Align::Default);
button->setCaption("Click Me!");

// Handle button click event
button->eventMouseButtonClick += MyGUI::newDelegate([](MyGUI::Widget* sender) {
    std::cout << "Button clicked!" << std::endl;
});

// Main loop for rendering and input handling
while (running) {
    gui->injectFrameEntered(elapsedTime);
    gui->injectMouseMove(mouseX, mouseY, mouseZ);
    gui->injectMousePress(mouseX, mouseY, MyGUI::MouseButton::Left);
    gui->injectMouseRelease(mouseX, mouseY, MyGUI::MouseButton::Left);
}

// Shutdown MyGUI
gui->shutdown();
delete gui;
```

This code initializes the MyGUI system, creates a button widget, handles its click event, and runs the main loop for rendering and input handling.

## Conclusion

The engine structure of MyGUI is modular, with clear separation between core GUI management, rendering, input handling, and resource management. Understanding these components and their interactions is crucial for effectively using and extending the MyGUI library.
