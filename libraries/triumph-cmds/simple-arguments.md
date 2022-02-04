<center><h1>Arguments</h1></center>
<center>
<p>Command argument declaration and options.</p>
</center>

---

# Simple arguments
By default the library adds many argument types.

**Common:**
* `short`/`Short`
* `int`/`Integer`
* `long`/`Long`
* `float`/`Float`
* `double`/`Double`
* `boolean`/`Boolean`
* `String`
* `Enums` - Any type of enums, for example `Material`.

Aditionally each platform also adds a few default types.

**Bukkit**
* `Material` - Overriden from normal enums to use `matchMaterial` instead of `valueOf`.
* `Player`
* `World`

**JDA**
* `User`
* `Member`
* `TextChannel`
* `VoiceChannel`
* `Role`