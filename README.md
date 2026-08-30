<h1 align="center">🛣 Road Trip</h1>

<p align="center">
  <b>A driving game about remembering.</b><br>
  <sub>You hold a lane. The road hands you memories back.</sub>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Unity-6000.0.45f1-000000?style=for-the-badge&logo=unity" />
  <img src="https://img.shields.io/badge/Ankara%20Game%20Jam-e63946?style=for-the-badge" />
  <img src="https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=csharp&logoColor=white" />
</p>

---

There's no level. Only distance.

Each road tile spawns the next one when you cross it, then deletes itself — **constant memory,
infinite road**. Out there, two things happen:

- **Things on the road.** One to three per section, pulled from a pool. Some are obstacles. Some are just there.
- **Things in your head.** Certain triggers surface a memory instead of an object — it plays over the drive, then clears.

And a radio. It starts *silent*. You have to reach over and turn it up.

```
E / Q  →  track          R / T  →  volume
```

## Adding an event is three steps

Make the prefab, implement one interface, drop it in the pool. There's no dispatch code to edit —
the prefab declares where it belongs:

```csharp
if (component is INextRoad)  // ahead, off the driving line
if (component is IInRoad)    // on the road itself
```

## Run it

Open `Ankara Jam/` in **Unity 6**, start from `Scenes/MainMenu.unity`.

---

<sub>Driving is Realistic Car Controller Pro, weather is RainMaker, foliage is CTI/AllSky. Repo
license covers the game code in <code>Prefabs/</code>, <code>Radio/</code> and <code>Scenes/</code>.</sub>
