# **Essential Vim Settings**

Before we dive into plugins, here are some key settings you might want to tweak in your `~/.vimrc` (Vim configuration file) to improve the overall experience:

#### a. **Enable Line Numbers**

This helps you navigate more easily, especially in larger files.

`set number`

#### b. **Enable Syntax Highlighting**

For better readability, especially when working with markdown or code.

`syntax enable`

#### c. **Enable Line Wrapping**

If you're writing a lot of text, you’ll want to ensure lines don't just scroll off the screen.

`set wrap`

#### d. **Enable Auto-Indentation**

This is especially useful for working with markdown or any formatted writing.

`set smartindent set tabstop=4 set shiftwidth=4 set expandtab`

#### e. **Highlight Search Results**

Makes it easier to see search results as you type.

`set incsearch set hlsearch`

#### f. **Enable Mouse Support** (optional)

If you're comfortable using the mouse occasionally (like for scrolling or selecting), enable mouse support.

`set mouse=a`

---

# **Useful Vim Plugins**

Here are a few essential plugins that can help enhance your experience in Vim. You'll need a plugin manager for Vim, like **vim-plug** or **Vundle**. If you don't have one installed, I recommend using **vim-plug**.

#### a. **Install vim-plug** (if you don’t have it)

1. First, install vim-plug by running this in the terminal:

```Bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

2. Now, you can add the following plugins to your `~/.vimrc` file.

#### b. **Essential Plugins for Vim**

1. **NERDTree** — File explorer for Vim.
    
    - A great plugin to browse and manage your files directly inside Vim.
        
    
    `Plug 'preservim/nerdtree'`
    
    After adding this to your `.vimrc`, run `:PlugInstall` to install it. You can then open NERDTree with the `:NERDTreeToggle` command.
    
2. **fzf.vim** — Fuzzy file finder.
    
    - Makes it super easy to find and open files quickly.
        
    
    `Plug 'junegunn/fzf.vim'`
    
    You will need to install **fzf** itself first. On macOS, you can use `brew install fzf`.
    
3. **vim-markdown** — Markdown support for Vim.
    
    - Adds syntax highlighting, folding, and more for markdown files (great for Obsidian-style notes).
        
    
    `Plug 'plasticboy/vim-markdown'`
    
4. **vim-airline** — Fancy status bar.
    
    - A lightweight and customizable status line plugin to improve your editor's look.
        
    
    `Plug 'vim-airline/vim-airline'`
    
5. **vim-fugitive** — Git integration for Vim.
    
    - A must-have for version control. It lets you run Git commands directly from Vim.
        
    
    `Plug 'tpope/vim-fugitive'`
    
6. **vim-surround** — Add, change, or delete surrounding characters.
    
    - Useful when you need to wrap text in quotes, brackets, parentheses, etc.
        
    
    `Plug 'tpope/vim-surround'`
    
7. **vim-commentary** — Commenting made easy.
    
    - Quickly comment or uncomment code or text.
        
    
    `Plug 'tpope/vim-commentary'`
    
8. **Auto-completion Plugin (coc.nvim)** — Autocomplete for code and text.
    
    - If you want intelligent autocomplete and code suggestions, **coc.nvim** is a powerful option.
        
    
    `Plug 'neoclide/coc.nvim', {'branch': 'release'}`
    
    Note: This plugin requires **Node.js** to work, so you'll need to install it.
    
9. **vim-obsidian** — For working with Obsidian-style Markdown files (optional).
    
    - If you want to have better support for Obsidian markdown files directly in Vim, this plugin can be useful.
        
    
    `Plug 'vvoovv/vim-obsidian'`
    

# **Example  ==.vimrc==  Configuration**

Here’s an example of what your `.vimrc` file might look like after adding some of these settings and plugins:

```Python
" Enable line numbers 
set number  

" Enable syntax highlighting 
syntax enable  

" Auto-indent settings 
set smartindent 
set tabstop=4 
set shiftwidth=4 
set expandtab  

" Enable search highlighting 
set incsearch 
set hlsearch  

" Enable file explorer 
Plug 'preservim/nerdtree' 
 
" Fuzzy file finding 
Plug 'junegunn/fzf.vim' 
 
" Markdown support 
Plug 'plasticboy/vim-markdown' 
 
" Fancy status bar 
Plug 'vim-airline/vim-airline'  

" Git integration 
Plug 'tpope/vim-fugitive'  

" Commenting plugin 
Plug 'tpope/vim-commentary'  

" Surrounding text plugin 
Plug 'tpope/vim-surround'  

" Auto-completion 
Plug 'neoclide/coc.nvim', {'branch': 'release'}  

" Initialize plugin system 
call plug#begin('~/.vim/plugged')  

" Your plugins go here 
Plug 'preservim/nerdtree' 
Plug 'junegunn/fzf.vim' 
Plug 'plasticboy/vim-markdown' 
Plug 'vim-airline/vim-airline' 
Plug 'tpope/vim-fugitive' 
Plug 'tpope/vim-commentary' 
Plug 'tpope/vim-surround' 
Plug 'neoclide/coc.nvim', {'branch': 'release'}

call plug#end()
```

Once you add these plugins and settings to your `.vimrc`, you can install the plugins by running:

`:PlugInstall`

---

# **Other Tips for Using Plugins and Settings**

- **Plugin Management**: To make managing plugins easier, always use a plugin manager like **vim-plug**, **Vundle**, or **Pathogen**.
    
- **Keep It Minimal**: As you start using Vim, try not to overload it with too many plugins. Start with a few and gradually add more as needed.

---
Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  