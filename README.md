# Orgmode.nvim (Beta)

Orgmode clone written in Lua for Neovim 0.5.

## Installation

Use your favourite package manager:

* [vim-packager](https://github.com/kristijanhusak/vim-packager):

```lua
packager.add('kristijanhusak/orgmode.nvim')
```

- [packer.nvim](https://github.com/wbthomason/packer.nvim)

```lua
use {'kristijanhusak/orgmode.nvim', config = function()
        require('orgmode').setup{}
end
}
```

- [vim-plug](https://github.com/junegunn/vim-plug)

```vim
Plug 'kristijanhusak/orgmode.nvim'
```

- [dein](https://github.com/Shougo/dein.vim)

```vim
call dein#add('kristijanhusak/orgmode.nvim')
```

## Setup

```lua
require('orgmode').setup({
  org_agenda_files = {'~/Dropbox/org/*', '~/my-orgs/**/*'},
  org_default_notes_file = '~/Dropbox/org/refile.org',
})
```

* **Open agenda prompt**: <kbd>\<Leader\>oa</kbd>
* **Open capture prompt**: <kbd>\<Leader\>oc</kbd>
* In any orgmode buffer press <kbd>?</kbd> for help

### Completion
If you use [nvim-compe](https://github.com/hrsh7th/nvim-compe) and want
to enable autocompletion, add this to your compe config:

```lua
require'compe'.setup({
  source = {
    orgmode = true
  }
})
```

For [completion.nvim](https://github.com/nvim-lua/completion-nvim), just add `omni` mode to chain complete list and add additional keyword chars:
```lua
vim.g.completion_chain_complete_list = {
  org = {
    { mode = 'omni'},
  },
}
vim.cmd[[autocmd FileType org setlocal iskeyword+=:,#,+]]
```

Or just use `omnifunc` via <kbd>\<C-x\>\<C-o\></kbd>

### Gifs
#### Agenda
  ![agenda](https://user-images.githubusercontent.com/1782860/123549968-8521f600-d76b-11eb-9a93-02bad08b37ce.gif)

#### Org file
  ![orgfile](https://user-images.githubusercontent.com/1782860/123549982-90752180-d76b-11eb-8828-9edf9f76af08.gif)

#### Capturing and refiling
  ![capture](https://user-images.githubusercontent.com/1782860/123549993-9a972000-d76b-11eb-814b-b348a93df08a.gif)

#### Autocompletion
  ![autocomplete](https://user-images.githubusercontent.com/1782860/123550227-e8605800-d76c-11eb-96f6-c0a677d562d4.gif)


### Features (TL;DR):
* Agenda view
* Search by tags/keyword
* Repeatable dates, date and time ranges
* Capturing to default notes file/destination
* Archiving (archive file or ARCHIVE tag)
* Calendar popup for easier navigation and date updates
* Various org file mappings:
  * Promote/Demote
  * Change TODO state
  * Change dates
  * Insert/Move/Refile headlines
  * Change tags
  * Toggle checkbox state

### Features (Detailed breakdown):
* Agenda prompt:
  * Agenda view (<kbd>a</kbd>):
    * Ability to show daily(<kbd>vd</kbd>)/weekly(<kbd>vw</kbd>)/monthly(<kbd>vm</kbd>)/yearly(<kbd>vy</kbd>) agenda
    * Support for various date settings:
      * DEADLINE:  Warning settings - example:  `<2021-06-11 Fri 11:00 -1d>`
      * SCHEDULED: Delay setting - example: `<2021-06-11 Fri 11:00 -2d>`
      * All dates - Repeater settings:
        * Cumulate type: `<2021-06-11 Fri 11:00 +1w>`
        * Catch-up type: `<2021-06-11 Fri 11:00 ++1w>`
        * Restart type: `<2021-06-11 Fri 11:00 .+1w>`
      * Time ranges - example: `<2021-06-11 Fri 11:00-12:30>`
      * Date ranges - example: `<2021-06-11 Fri 11:00-12:30>--<2021-06-13 Sun 22:00>`
    * Properly lists tasks according to defined dates (DEADLINE,SCHEDULED,Plain date)
    * Navigate forward (<kbd>f</kbd>)/backward(<kbd>b</kbd>) or jump to specific date (<kbd>J</kbd>)
    * Go to task under cursor in current window(<kbd>\<CR\></kbd>) or other window(<kbd>\<TAB\></kbd>)
    * Print category from ":CATEGORY:" property if defined
  * List tasks that have "TODO" state (<kbd>t</kbd>):
  * Find headlines matching tag(s) (<kbd>m</kbd>):
  * Search for headlines (and it's content) for a query (<kbd>s</kbd>):
* Capture:
  * Define custom templates
  * Fast capturing to default notes file via <kbd>\<C-c\></kbd>
  * Capturing to specific destination <kbd>\<Leader\>or</kbd>
  * Abort capture with <kbd>\<Leader\>ok</kbd>
* Org files
  * Refile to destination/headline: <kbd>\<Leader\>or</kbd>
  * Increase/Decrease date under cursor: <kbd>\<C-a\></kbd>/<kbd>\<C-x\></kbd>
  * Change date under cursor via calendar popup: <kbd>cid</kbd>
  * Change headline TODO state: forward<kbd>cit</kbd> or backward<kbd>ciT</kbd>
  * Open hyperlink or date under cursor: <kbd>\<Leader\>oo</kbd>
  * Toggle checkbox: <kbd>\<C-space\></kbd>
  * Toggle folding of current headline: <kbd>\<TAB\></kbd>
  * Toggle folding in whole file: <kbd>\<S-TAB\></kbd>
  * Archive headline: <kbd>\<Leader\>o$</kbd>
  * Add archive tag: <kbd>\<Leader\>oA</kbd>
  * Change tags: <kbd>\<Leader\>ot</kbd>
  * Promote headline: <kbd><<</kbd>
  * Demote headline: <kbd>>></kbd>
  * Promote subtree: <kbd>\<s</kbd>
  * Demote subtree: <kbd>\>s</kbd>
  * Add headline/list item/checkbox: <kbd>\<Leader\>\<CR\></kbd>
  * Insert heading after current heading and it's content: <kbd>\<Leader\>oih</kbd>
  * Insert TODO heading after current line: <kbd>\<Leader\>oiT</kbd>
  * Insert TODO heading after current heading and it's content: <kbd>\<Leader\>oit</kbd>
  * Move headline up: <kbd>\<Leader\>oK</kb>
  * Move headline down: <kbd>\<Leader\>oJ</kb>
  * Highlighted code blocks (`#+BEGIN_SRC filetype`)

Link to detailed documentation: [DOCS](DOCS.md)

## Development

### Tests
 To run tests, [plenary.nvim](https://github.com/nvim-lua/plenary.nvim) is necessary. Once installed, run:
```
make test
```

### Documentation
Vim documentation is auto generated from [DOCS.md](DOCS.md) file with [md2vim](https://github.com/FooSoft/md2vim).

### Parser
Parser is written manually from scratch. It doesn't follow any parser writing patterns (AFAIK), because I don't have
much experience with those. Any help on this topic is appreciated.

## Plans
* [ ] Support searching by properties
* [ ] Improve checkbox hierarchy
* [ ] Support todo keyword faces
* [ ] Support clocking work time
* [ ] Improve folding
* [ ] Support exporting and publishing (via existing emacs tools)
* [ ] Support archiving to specific headline
* [ ] Support tables
* [ ] Support diary format dates
* [ ] Support evaluating code blocks

## Thanks to
* [@dhruvasagar](https://github.com/dhruvasagar) and his [vim-dotoo](https://github.com/dhruvasagar/vim-dotoo) plugin
  that got me started using orgmode. Without him this plugin would not happen.
* [vim-orgmode](https://github.com/jceb/vim-orgmode) for some parts of the code (mostly syntax)
