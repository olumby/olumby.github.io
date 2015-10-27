---
layout: post
title: "OS X Clean Install (10.11)"
date: 2015-10-01 010:30:00
category: os x
---
### OS X Preferences

```bash
# Set hostname
sudo scutil --set HostName oliver-mba

# Disable window animations
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false

# Enable repeat on keydown
defaults write -g ApplePressAndHoldEnabled -bool false

# Expand save panel by default
defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool tru

# Use current directory as default search scope in Finder
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"

# Show Path bar in Finder
defaults write com.apple.finder ShowPathbar -bool true

# Show Status bar in Finder
defaults write com.apple.finder ShowStatusBar -bool true

# Enable AirDrop over Ethernet and on unsupported Macs
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true

# Set a blazingly fast keyboard repeat rate
defaults write NSGlobalDomain KeyRepeat -int 0

# Avoid creating .DS_Store files on network volumes
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true

# Set a shorter Delay until key repeat
defaults write NSGlobalDomain InitialKeyRepeat -int 12

# Disable disk image verification
defaults write com.apple.frameworks.diskimages skip-verify -bool true &&
defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true &&
defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true

# Disable Safari’s thumbnail cache for History and Top Sites
defaults write com.apple.Safari DebugSnapshotsUpdatePolicy -int 2

# Enable Safari’s debug menu
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true

# Disable smart quotes as it’s annoying for messages that contain code
defaults write com.apple.messageshelper.MessageController SOInputLineSettings -dict-add "automaticQuoteSubstitutionEnabled" -bool false

# Enable the Develop menu and the Web Inspector in Safari
defaults write com.apple.Safari IncludeDevelopMenu -bool true &&
defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true &&
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled -bool true &&
defaults write NSGlobalDomain WebKitDeveloperExtras -bool true

# Show the ~/Library folder
chflags nohidden ~/Library

# Show absolute path in finder's title bar. 
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES
```

### AppStore

* 1Password
* Xcode
* iBooks Author
* Slack
* Tictoc
* Memory Clean
* Unarchiver
* Pages

### Other Apps

* CleanMyMac 2
* Dropbox
* Google Chrome
* PHPStorm
* Sequel Pro
* Sidestep
* Skype
* Spectable
* Sublime Text 3
* Transmission
* Vagrant
* Virtual Box
* VLC Player
* Bartender
* SelfControl
* Handbreak
* Sketch
* Mailbox
* Zeplin
* LICEcap

```bash
# Disable autosave in Sketch
defaults write com.bohemiancoding.sketch3 ApplePersistence -bool no
``` 

### Homebrew

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```bash
brew install ssh-copy-id wget node jpegoptim pngcrush colordiff imagemagick icoutils ack git
```

### Dev

```bash
# SSH Key
ssh-keygen -t rsa -C "me@oliverlumby.com"
```

```bash
# Add the Homestead vagrant box
vagrant box add laravel/homestead
```

```bash
# Install php, composer
brew tap homebrew/dupes
brew tap homebrew/versions
brew tap homebrew/php
brew install php56
brew install composer
```

```bash
# Composer require homestead
composer global require "laravel/homestead=~2.0"
```

```bash
# Inside ~/.bash_profile
alias homestead=~/.composer/vendor/bin/homestead
alias ll="ls -lah"
alias c="clear"
alias art="php artisan"

export PATH="/usr/local/bin:$PATH"
```

```bash
# Source it
source ~/.bash_profile
```

```bash
# Cocoapods
sudo gem install cocoapods
```

### Homestead

```bash
# Mailcatcher
gem install mailcatcher
mailcatcher --http-ip 192.168.10.10
```

### Screenshots

* Automator Service "no input" in "any application"
* Run shell script:

```sh
#!/bin/bash

DATE=$(date +"%Y-%m-%d");
TIME=$(date +"%H.%M.%S");

FILENAME=Screen\ Shot\ $DATE\ at\ $TIME.png;

DB_USER_ID=18301138

DB_BASE_DIR=~/Dropbox/Public/Shots;
DB_BASE_URL=https://dl.dropboxusercontent.com/u;

screencapture -i "$DB_BASE_DIR/$FILENAME";

# user may have escaped out of the screencapture
if [ -f "$DB_BASE_DIR/$FILENAME" ];
then
    URL_FILENAME=$(python -c "import urllib; print urllib.quote('''$FILENAME''')");
    URL_LONG="$DB_BASE_URL/$DB_USER_ID/Shots/$URL_FILENAME";
    # copy long url, if you paste before the shortener returns
    echo $URL_LONG | pbcopy;

    # shorten url via google
    URL_SHORT=$(curl https://www.googleapis.com/urlshortener/v1/url -H 'Content-Type: application/json' -d "{\"longUrl\": \"$URL_LONG\"}" 2>/dev/null | grep goo.gl | cut -f 4 -d '"');

    if [ -n "$URL_SHORT" ]; then
        # we have a short url, copy it
        echo $URL_SHORT | pbcopy;
    fi
fi
```

### Sublime Text 3

```JSON
{
    "bold_folder_labels": true,
    "caret_style": "phase",
    "close_windows_when_empty": true,
    "color_scheme": "Packages/User/SublimeLinter/base16-ocean.dark (SL).tmTheme",
    "draw_white_space": "all",
    "ensure_newline_at_eof_on_save": true,
    "findreplace_small": true,
    "font_face": "Source Code Pro",
    "font_size": 13.0,
    "highlight_modified_tabs": true,
    "ignored_packages":
    [
        "Vintage"
    ],
    "line_padding_bottom": 4,
    "line_padding_top": 4,
    "shift_tab_unindent": true,
    "show_encoding": true,
    "show_full_path": true,
    "show_tab_close_buttons": true,
    "spell_check": true,
    "sublimelinter": true,
    "sublimelinter_mark_style": "fill",
    "tab_size": 4,
    "tabs_medium": true,
    "theme": "Spacegray.sublime-theme",
    "translate_tabs_to_spaces": true,
    "word_wrap": false
}
```

```JSON
{
    "in_process_packages":
    [
    ],
    "installed_packages":
    [
        "Color Highlighter",
        "DocBlockr",
        "Git",
        "Glue",
        "LESS",
        "Markdown Preview",
        "Package Control",
        "PHP Companion",
        "SQF Language",
        "sublime-github",
        "SublimeLinter",
        "Swift",
        "Theme - Phoenix",
        "Theme - Spacegray",
        "Tomorrow Color Schemes"
    ]
}
```
