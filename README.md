# Escape the Digital Fortress (Bonus Project)

A short text adventure. The evil AI has trapped you inside its digital fortress. Explore the rooms, find what you need, and escape. Your decisions determine how the story ends.

The game uses only `prompt()`, `alert()`, `confirm()`, and the browser **console**. There is no DOM manipulation.

## How to run

1. Download or clone this project.
2. Open `index.html` in any modern browser.
3. Follow the pop-ups.

## How to play

Type one of the listed choices into each prompt and press **OK**.

- Capitalization and extra spaces do not matter (`"  CONTROL    room "` works).
- Invalid input shows a message listing the valid options and **changes nothing** in the game.
- Pressing **Cancel** at any prompt quits the game safely.
- Each prompt shows your location, a description, your inventory, and your available choices, so you always know what to do next.

## Why the console is needed

The console holds the full story log. The pop-ups also show the key information (room, inventory, what just happened), so the game is still playable with the console closed.

| Browser / OS | Shortcut |
|---|---|
| Chrome, Edge, Firefox (Windows/Linux) | `F12`, then click the **Console** tab |
| Chrome (Mac) | `Cmd + Option + J` |
| Safari (Mac) | Enable the Develop menu in Settings, then `Cmd + Option + C` |

These instructions appear in the intro pop-up before the game starts, so the console does not need to be open already.

## The world

| Location | What you can do |
|---|---|
| **Prison Cell** | Inspect the cell (a hint points you toward the Control Room) |
| **Control Room** | Search the console for an access card, or try to shut down the AI's security system |
| **Security Gate** | Try to open the gate and escape |

You can travel between any two locations at any time, including back to places you have already visited.

## How the game remembers your actions

| State | Meaning |
|---|---|
| `hasAccessCard` | Set when you find the card. The card can only be collected once, even if you search again. |
| `securityOffline` | Set when you shut down the AI's security system. |

These two values decide what happens at the Security Gate.

## Endings

| Your actions | Result |
|---|---|
| Access card **and** security offline, then escape | **Escape**: you slip out unseen |
| Security active, then escape anyway (after a warning) | **Captured**: the AI's guards catch you |
| No card but security offline, then escape | The gate stays locked and the game continues |

Risky moves ask for confirmation first, so you are never captured by accident.

## Restarting

When the story ends, a `confirm()` offers another game. Choosing OK builds a brand-new game state, so items, decisions, and location are all reset. Pressing Cancel mid-game exits without asking to replay.

## Project structure

```
escape-the-evil-ai/
├── index.html   # Blank page that loads the script
├── script.js    # All game logic
└── README.md
```

## Code overview

| Part | Purpose |
|---|---|
| `ROOMS` | Data for each room: title, special actions, and description |
| `createState()` | Returns a fresh game state (used on every new game) |
| `getChoice()` | Prompts the player, cleans the input, re-asks on invalid input, returns `null` on Cancel |
| `getOptions()`, `showRoom()`, `buildPrompt()` | Build the list of choices and display them |
| `doAction()`, `disableSecurity()`, `tryEscape()` | Handle player actions and endings |
| `playOnce()` | Runs one full playthrough in a loop |
| `main()` | Shows the intro and handles the replay loop |

## Story map

```
        [Prison Cell]
         /         \
[Control Room] --- [Security Gate]
   search card        escape
   disable security
```


