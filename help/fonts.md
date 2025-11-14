# Config help for fonts

List fonts that are available:

```sh
ghostty +list-fonts
```

Show configuration of font-family:

```sh
ghostty +show-config | grep font-family
```

Test with command line:

```sh
ghostty --font-family="Menlo" --font-size=14
```

Some fonts that I like:

- Bitstream Vera and friends because it's highly reliable
- Courier New because it looks like a classic typewriter
- DejaVu and friends because it's good for ebooks
- Iosevka and friends because they are narrow-width
- Fira Code and friends because they have coding ligatures
- FreeMono because GNU makes it 100% free open source
- Source Code Pro

If a font is installed on your system yet isn't in the list of fonts,
Ghostty can still use the font - just specify it directly in your config.

## macOS help

Some fonts (including those installed by Homebrew) aren't properly marked as
monospace in their metadata, so don't appear in the list - but still work.

## macOS homebrew

Install some fonts via homebrew:

```sh
brew install --cask font-hack-nerd-font
brew install --cask font-dejavu-sans-mono-nerd-font
brew install --cask font-inconsolata
brew install --cask font-iosevka-term-nerd-font
brew install --cask font-jetbrains-mono
brew install --cask font-ubuntu-mono
```

## macOS troubleshooting

If there are problems, try using Apple Type Server (ATS).

Try to list all the installed fonts:

```sh
atsutil fonts -list
```

Try to force kill font processes and remove all the font caches:

```sh
sudo killall "fontd"; 
sudo killall "FontAgent"
sudo killall "Font Book"
sleep 2
sudo killall -9 "fontd"; 
sudo killall -9 "FontAgent"
sudo killall -9 "Font Book"
sleep 2
sudo atsutil databases -remove
```

Or manually delete cache files:

```sh
rm -rf ~/Library/Caches/com.apple.FontRegistry/
rm -rf ~/Library/FontCollections/
```

Set permissions:

```sh
sudo chmod 644 /Library/Fonts/* 
sudo chmod 644 ~/Library/Fonts/*
```

If you use brew as a different user, then you may need to copy the brew font
files to the system path, such as via rsync:

```sh
rsync -av /Users/brew/Library/Fonts/* /Library/Fonts/`
rm -f ~/Library/Preferences/com.apple.FontBook.plist
```
