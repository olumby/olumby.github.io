---
layout: post
title: OS X Clean Install (10.11)
date: 2015-10-01T10:30:00.000Z
updated: 2015-10-31T00:57:00.000Z
published: true
categories: 
  - os x
  - developer
tags: 
  - install
  - os x
  - developer
  - "el capitan "
  - mac
---

### OS X Preferences

```bash
# Set hostname
sudo scutil --set HostName oliver-mb

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

# Show absolute path in finder's title bar. 
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES

# Show the ~/Library folder
chflags nohidden ~/Library

# Enable AirDrop over Ethernet and on unsupported Macs
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool true

# Avoid creating .DS_Store files on network volumes
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true

# Disable disk image verification
defaults write com.apple.frameworks.diskimages skip-verify -bool true &&
defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true &&
defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true

# Disable Safari’s thumbnail cache for History and Top Sites
defaults write com.apple.Safari DebugSnapshotsUpdatePolicy -int 2

# Enable Safari’s debug menu
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true

# Enable the Develop menu and the Web Inspector in Safari
defaults write com.apple.Safari IncludeDevelopMenu -bool true &&
defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true &&
defaults write com.apple.Safari com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled -bool true &&
defaults write NSGlobalDomain WebKitDeveloperExtras -bool true

# Disable Smart Quotes
defaults write com.apple.messageshelper.MessageController SOInputLineSettings -dict-add "automaticQuoteSubstitutionEnabled" -bool false
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

* Dropbox
* Google Chrome
* Sequel Pro
* Skype
* Spectable
* Sublime Text
* Transmission
* Vagrant
* Virtual Box
* VLC Player
* Handbreak
* Sketch
* Mailbox
* LICEcap
* Little Snitch

### Disable autosave in Sketch

```bash
defaults write com.bohemiancoding.sketch3 ApplePersistence -bool no
``` 

### Homebrew

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```bash
brew install ssh-copy-id wget node jpegoptim pngcrush colordiff imagemagick icoutils ack git
```

```bash
brew install caskroom/cask/brew-cask
brew cask install qlcolorcode  qlstephen qlmarkdown quicklook-json quicklook-csv 
```


### Dev

```bash
# Generate SSH Key
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

### In Homestead

```bash
# Mailcatcher
gem install mailcatcher
mailcatcher --http-ip 192.168.10.10
```

```bash
# ~/.bash_profile
alias pa="php artisan"
alias vssh="ssh vagrant@127.0.0.1 -p 2222"
alias vup="(cd ~/Virtual/Homestead/ && vagrant up)"
alias vhalt="(cd ~/Virtual/Homestead/ && vagrant halt)"
alias vm="vup && vssh"
export PATH="/usr/local/sbin:$PATH"
```

```bash
# Install Cocoapods
gem install cocoapods
```

### Sublime Text

```json
{
    "bold_folder_labels": true,
    "color_scheme": "Packages/Base16 Color Schemes/base16-ocean.dark.tmTheme",
    "draw_white_space": "all",
    "ensure_newline_at_eof_on_save": true,
    "findreplace_small": true,
    "font_face": "Hack",
    "font_options":
    [
        "gray_antialias"
    ],
    "font_size": 12.0,
    "gutter": true,
    "highlight_modified_tabs": false,
    "ignored_packages":
    [
    ],
    "line_numbers": true,
    "line_padding_bottom": 4,
    "line_padding_top": 4,
    "material_theme_accent_red": true,
    "material_theme_disable_folder_animation": true,
    "material_theme_disable_tree_indicator": true,
    "material_theme_small_tab": true,
    "overlay_scroll_bars": "enabled",
    "show_panel_on_build": false,
    "theme": "Material-Theme.sublime-theme"
}
```

```json
{
    "bootstrapped": true,
    "in_process_packages":
    [
    ],
    "installed_packages":
    [
        "AdvancedNewFile",
        "Base16 Color Schemes",
        "Color Highlighter",
        "Fix Mac Path",
        "LESS",
        "Material Theme",
        "Origami",
        "Package Control",
        "PackageResourceViewer",
        "PHP Companion",
        "PHP Getters and Setters",
        "SCSS",
        "Swift"
    ]
}
```
