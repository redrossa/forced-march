---
layout: post
title: "Brainstorm: The Campania Engine"
---

Stripping to its bare mechanics, Forced March has quite a distinct gameplay with a UI overlaid on a
2D aerial map, and game logic working underneath it to give life to the world. The game (future) development will greatly benefit from a game engine customized for its unique mechanic. Introducing: the Campania Engine. The workings of the engine can be divided into three processes: the UI manager, the game logic manager, and the rendering manager. These managers' concerns reside within the bounds of the application, an infinite space implemented as a window. When the engine is built for a specific game, modding is will be done through external assets and codes provided to the game directory; no need to dig into the engine code.

## UI Manager

The UI manager initiates the frame. It handles which objects must be interfaced on the application to the user and which actions must an object perform based on the events input by the user; for UI objects, the UI manager should perform them immediately, but for game objects, the UI manager just registers the user event whose action will be left to the game logic manager. The UI manager is also responsible for loading assets from disk to memory. UI design is specified in loaded code.

### Basics of the UI System

A UI object is something that invokes interactivity on the user. It can be in the form of a drawn graphic and/or played audio. The graphical implementation of a UI object is a simple sprite of only four vertices creating a quad. There are many properties that a UI object may possess. An important one is texture, in order to render the object visible on the window. If a texture is not set, the vertices are not drawn (do not exist) on the window, but the object still exists in the program. Audio may also be attached to a UI object. Similarly, if audio is not set, nothing is played. Texture and audio are managed by separate renderers in the render manager, so one that is set may be rendered without the other being set. A UI object may listen to events, action input by the user. An event listener is a property that determines the behavior of a UI object given a specific type of event. A UI object may have many event listeners, but they all must handle different types of events.

Fundamentally, a graphical UI object only has four vertices. How can we create non-rectangular UI objects? The solution lies in its texture. The graphical interactivity of a UI object is limited to the non-transparent, that is non-zero alpha value, pixels of its texture. Suppose we want to create a circular red button with a radius of 20 pixels. If we click it, the color should darken. We shall specify the UI object to be 40 pixels wide and 40 pixels tall. We shall set its texture to a 40 pixel by 40 pixel image that contains a centered red circle and the pixels of the four corners have alpha values of zero. We shall set an on mouse hover listener that divides all the pixel values by a constant. The UI manager checks whether the mouse position is on a non-transparent pixel of the object for all mouse-based events to trigger a listener of that object, so we do not need to manually perform this check. From the perspective of the user, when the mouse is truly on a red pixel of the button, the button darkens. If the mouse was on one of the four corners inside the invisible rectangular region of the object vertices, the button does not darken.

## Game Logic Manager

The game logic manager applies game logic to game objects based on real-time events from the previous frame as well as newly registered ones from the UI manager. Game objects hold game states, each update done by the game logic manager every frame on the current states result in new states. Game logic is provided by external codes in the engine directory to be used as embedded scripts.

## Render Manager

The render manager finalizes the frame. It takes all objects that are renderable that must be rendered and draws their sprite assets if they must be drawn and are in view, or plays their audio assets if asked to do so.