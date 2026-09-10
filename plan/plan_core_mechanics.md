Step 2: Extract & Fork the Core Mechanics
Natural Selection's defining gameplay is its asymmetrical FPS/RTS hybrid nature (Marines with a top-down Commander vs. first-person Aliens). Since you are building a small app, focus on a minimal proof-of-concept: 

 (https://developer.valvesoftware.com/wiki/Natural_Selection)The Top-Down Grid/RTS System: Build a system where a single player can switch to an overhead view, click to place a building (like an Infantry Portal or Resource Tower), and spend points. The First-Person Controller: Create standard touch-screen joystick inputs for Android/iOS alongside keyboard/mouse listeners for PC.

The Networking Layer: Use a lightweight, cross-platform networking solution natively integrated into your engine (like Godot’s High-Level Multiplayer API or Unity’s Netcode for GameObjects).

remember we are using unreal engine.



### Comms

here is an example. 
In Unreal Engine, managing who can talk to whom in a multiplayer FPS (Team-only, Proximity/Tween, or Global chat) is handled by a Communications Layer built on top of RPCs (Remote Procedure Calls) and Gameplay Tags.The cleanest architecture separates the chat logic into a Game State component (for global routing) or a Player Controller / Player State component (for filtering).Core Architecture: Architectural Component OverviewPlayer Controller (PC): Handles local input (typing a message) and sends it to the server.Game State (GS): Routes the message to the correct recipients based on game rules.Player State (PS): Holds the player's team identifier (e.g., Team ID 0 or 1).Character / Pawn: Holds the physical location for proximity-based

we would also want the comms to work as described in the root project folder's readme.md
                   ┌───────────────────────────┐
                   │ Server Receives Message   │
                   └─────────────┬─────────────┘
                                 │
                    [What is the Chat Channel?]
                                 │
         ┌───────────────────────┼───────────────────────┐
         ▼                       ▼                       ▼
    【 Global 】              【 Team 】             【 Proximity 】
         │                       │                       │
Send to ALL controllers.   Does SenderTeamID ==     Does SenderLocation to
                           ReceiverTeamID?         ReceiverLocation <= MaxDistance?
                                 │                       │
                                 ▼                       ▼
                            (If Yes) ➔ Send          (If Yes) ➔ Send


