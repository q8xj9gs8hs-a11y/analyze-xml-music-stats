# analyze-xml-music-stats
Custom pattern for reading and displaying top statistics from Apple Music Library.xml, including play counts, artists, genres, songs, and more.

## This fabric pattern, called analyze_xml, starts as folows:
- Go into Apple Music on MacOS desktop app (this may be possible on web version as well if you do not have a Mac, not entirely sure though)
- Click `File` > `Library` > `Export Library...`
- Choose you which directory to save it in. you now have your entire music library in its data form as a `.xml` file.

## To start using this pattern (Mac):
1. Install fabric-ai on your device. If you use Homebrew:

`brew install fabric-ai`

2. Create a custom directory to store your custom-made patterns (e.g. `~/.config/fabric/my-custom-patterns`). It does not matter where, just so long you configure the directory appropriately in fabric's setup (`fabric-ai --setup`).
  
3. Create a folder with its name being the name of the pattern.

4. Download the markdown file, which contains the specific prompt for this pattern, into that folder.

  *or*
```
  git clone https://github.com/q8xj9gs8hs-a11y/analyze-xml-music-stats.git && \
  cd q8xj9gs8hs-a11y/analyze-xml-music-stats && \
  cp system.md ~/.config/fabric/my-custom-patterns/analyze_xml
```

## Example usage:
For raw output into the Terminal:

```fabric-ai -p analyze_xml < Library.xml```

To save the output onto a file called `Music_stats`

```fabric-ai -p analyze_xml -o Music_stats.md``` 

An alternative way to pass the `Library.xml` file as input for the model via chaining with `|`

```cat library.xml | fabric-ai -p analyze_xml | fabric 'What was my top artist played?'```

# Degrees of Freedom
1. Depending on your situation, your music library might be humongous (mine is over 2000 songs). Thus, you will most likely exceed the context length simply because of the massive amount of data being input
  - ***FIX:*** use the `tail` and `head` commands to cut content out for relevancy or plain size control; for example:

```tail -n 300 /path/to/xml/file | fabric -p analyze_xml```
    
2. Most of the data in the `.xml` file will not be necessary. In comes the power of tweaking the pattern and query to your liking. To add intermediate steps between exporting your `Library.xml` and creating the custom pattern (`system.md`), including, but not limited to:
 - ***FIX:*** Using `grep`, `awk`, or other related tools to parse through the data and extract only the types you need for statistics. This means that you can get more personal statistics than just what the pattern has, whatever data is in the `.xml`. Here is an example that I did:

```grep -iE '<key>Name</key><string>|<key>Artist</key><string>|play count|genre' Library_5.xml > Library_5.txt```

This way I only have the `Play Count`, `Song`, `Artist`, and `Genre` saved in the `Library.xml` file (can also be `.txt`).

3. Increasing the amount of songs, artists, genre, etc. that the model will process. In other words, feel free to increase or decrease the length of the ranking to your heart's content, whether it be the top 100 songs, or top 3.
4. Altering the format of the output, the template that was explicated within the `system.md`. Change it to your liking if you don't prefer how the model is formatting the rankings.
