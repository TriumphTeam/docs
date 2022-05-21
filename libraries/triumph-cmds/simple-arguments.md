<center><h1>Arguments</h1></center>
<center>
<p>Command argument declaration and options.</p>
</center>

---

By default, the library adds many argument types.

# Common:
* `short`/`Short`
* `int`/`Integer`
* `long`/`Long`
* `float`/`Float`
* `double`/`Double`
* `boolean`/`Boolean`
* `String`
* `Enums` - Any type of enums, for example `Material`.

Additionally, each platform also adds a few default types.

# Bukkit:
* `Material` - Uses `matchMaterial` instead of `valueOf` by overriding default enum behavior.
* `Player`
* `World`

# JDA:
* `User`
* `Member`
* `TextChannel`
* `VoiceChannel`
* `Role`