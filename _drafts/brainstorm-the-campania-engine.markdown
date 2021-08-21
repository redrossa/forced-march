---
layout: post
title: "Brainstorm: The Campania Engine"
---

Stripping to its bare mechanics, Forced March has quite a distinct gameplay with a UI overlaid on a
2D aerial map, and game logic working underneath it to give life to the world. The game (future) development will greatly benefit from a game engine customized for its unique mechanic. Introducing: the Campania Engine. The workings of the engine can be divided into three processes: the UI manager, the game logic manager, and the rendering manager. These managers' concerns reside within the bounds of the application, an infinite space implemented as a window. When the engine is built for a specific game, modding is will be done through external assets and codes provided to the game directory; no need to dig into the engine code.

## UI Manager

The UI manager initiates the frame. It handles which objects must be interfaced on the application to the user and which actions must an object perform based on the events input by the user; for UI objects, the UI manager should perform them immediately, but for game objects, the UI manager just registers the user event whose action will be left to the game logic manager. The UI manager is also responsible for loading assets from disk to memory. UI design is specified in loaded code.

## Game Logic Manager

The game logic manager applies game logic to game objects based on real-time events from the previous frame as well as newly registered ones from the UI manager. Game objects hold game states, each update done by the game logic manager every frame on the current states result in new states. Game logic is provided by external codes in the engine directory to be used as embedded scripts.

## Render Manager

The render manager finalizes the frame. It takes all objects that are renderable that must be rendered and draws their sprite assets if they must be drawn and are in view, or plays their audio assets if asked to do so.