# Csharp

## Could not load file or assembly

These ones are always tricky to figure out. However, if you open up the "Developer Command Prompt"
as admin. Which you can find in the start menu. Then use "fuslogvw" to open up the assembly binding log viewer.
In there click settings and turn on "Log bind failures to disk".

I didn't see anything appear in the log viewer BUT now on the yellow error screen I have binding error info and
I can pinpoint the error.
