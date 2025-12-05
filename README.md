# fabric-ai_custom_pattern-analyze_xml
Custom pattern for reading and displaying top statistics from Apple Music library.xml, including play counts, artists, genres, and songs

This starts my journey with using Github. I will be posting my custom patterns for the framework *fabric-ai* that I create as I go.

This first pattern, called analyze_xml, starts as folows:
- Go into Apple Music on MacOS desktop app (this may be possible on web version as well if you do not have a Mac, not entirely sure though)
- Click `File` > `Library` > `Export Library...`
- Choose you which directory to save it in. you now have your entire music library in its data form as a `.xml` file.

To start using this pattern:
- download fabric-ai with `brew install fabric-ai` if you have Homebrew. I will link the other ways of installing fabric, like linking to daniel's repo for fabric-ai (all credit goes to him).
- I will not go over the steps for setting up fabric-ai, that will be its own dedicated repo later.

- create a custom directory to store your custom-made patterns. mine is in `~/.config/fabric/my-custom-patterns` (it does not matter where, just so long you configure the directory appropriately in fabric's setup
- create a folder with its name being the name of the pattern
- download the markdown file, which contains the specific prompt for this pattern, into that folder.

# You now have set up the pattern for use!
Example usage:
`fabric-ai -p analyze_xml < library.xml` for raw output into the Terminal

`( fabric-ai -p analyze_xml < library ) > ~/Desktop/Music_stats.md` to overwrite the output onto a file called `Music_stats`

`cat library.xml | fabric-ai -p analyze_xml | fabric 'What was my top artist played?'` (1) an alternative way to pass the xml file as input for the model, (2) chaining with `|`, using the outputs of the commands as input for the next

# Notes
- Depending on your situation, your music library might be humongous (like mine, over 2000 songs)! Thus, you will most likely exceed the context length simply because of the massive amount of data being input
- Most of the data in the `.xml` file will not be necessary for such stats. This is where the power of tweaking the pattern and query to your liking.

Thus, feel free to add intermediate steps between exporting your `library.xml` and creating the custom pattern (`system.md`), including, but not limited to:

- Using `grep`, `awk`, or other related tools to parse through the data and extract only the types you need for statistics.
- This means that you can get more personal statistics than just what the pattern has, whatever data is in the `.xml`
- Here is an example that I did:
```grep -iE '<key>Name</key><string>|<key>Artist</key><string>|play count|genre' Library_5.xml > Library_5.txt```
That way I only have the `Play Count`, `Song`, `Artist`, and `Genre` saved in the input file (meaning the analyze_xml doesn't necessarily need `.xml` as the input!)

- Increasing the amount of songs, artists, genre, etc. that the model will output as the ranking. In other words, feel free to increase or decrease the length of the ranking to your heart's content, whether it be the top 100 songs, or top 3.
- Altering the format of the output, the template that was explicated within the `system.md`. Change it to your liking if you don't prefer how the model is formatting the rankings.

## I hope you find this pattern useful, entertaining, and educational. I will be updating this as needed, so nothing here is final.
