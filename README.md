# Ankara Jam — Road Trip

A driving game about **remembering**. You hold a lane down an endless road; the road hands you
memories back.

Made for Ankara Game Jam in Unity 6.

## The idea

The road generates itself as you drive — each tile spawns the next when you cross it, so there is no
level, only distance. Two things happen out there:

- **Roadside events.** Objects spawn on the road or on the shoulder ahead of you, one to three per
  tile section, picked at random from a pool. Some are obstacles. Some are just there.
- **Memories.** Certain triggers surface a UI fragment instead of a physical object — a clip that
  plays over the drive and then clears itself. The further you get, the more of them you have seen.

And a radio, which is the part that makes the drive yours:

| Key | Action |
| --- | --- |
| `E` / `Q` | Next / previous track |
| `R` / `T` | Volume down / up |

It starts silent and fades in — you have to reach over and turn it up.

## How generation works

`SjGameManager` is the singleton holding every spawn pool: road tiles, scenery tiles, events, cars,
UI parents, cutscenes.

`RandomRoadTile` sits on a trigger at the end of each tile. When the player crosses it, it
instantiates a random next tile 360 units further down the Z axis and destroys itself. Constant
memory, infinite road.

`RandomEventManager` populates a section on `Start` with one to three events. Each event prefab
declares where it belongs by which interface it implements:

```csharp
if (component is INextRoad)  CreateNextRoadRandomEvent(spawnObj);  // ahead, off the driving line
if (component is IInRoad)    CreateOnRoadRandomEvent(spawnObj);    // on the road itself
```

So adding a new event type is: make the prefab, implement one of the two interfaces, drop it in the
pool. No dispatch code to edit.

`RandomEventTrigger` handles the memory variant — it walks `spawnUiParents`, clears whatever
fragment is showing, and raises the next one.

## Structure

```text
Ankara Jam/Assets/
  PlayerControls.inputactions   generated Input System bindings
  Prefabs/
    SjGameManager.cs            spawn pools, cutscene list, singleton
    RandomRoadTile.cs           endless road generation
    RandomEventManager.cs       per-section event population
    RandomEventTrigger.cs       roadside + memory-fragment triggers
    IInRoad.cs / INextRoad.cs   placement contracts
    DontCrush.cs
    Gifs/                       ChangeRawImageTexture, RemoveManager, RemoveMemory
  Radio/RadioManager.cs         track cycling and volume
  Scenes/                       MainMenu, gameplay, RadioScene, SampleScene
```

Driving is [Realistic Car Controller Pro](https://assetstore.unity.com/), weather is RainMaker,
foliage is Custom Tree Importer / AllSky / Oak & Poplar packs.

## Running it

Open `Ankara Jam/` in **Unity 6000.0.45f1** or newer and load `Assets/Scenes/gameplay.unity`.
`MainMenu` is the intended entry point.

## Notes

Jam-scope code. Third-party assets in the project are covered by their own licenses — the repository
license applies to the game code under `Prefabs/`, `Radio/` and `Scenes/`.
